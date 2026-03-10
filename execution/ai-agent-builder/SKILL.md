---
name: ai-agent-builder
description: Design and implement AI agent systems, autonomous workflows, and multi-step AI pipelines. Use this skill when building AI agents, agentic workflows, tool-using AI systems, multi-agent pipelines, or any system where an AI model takes actions, uses tools, or makes sequential decisions. Trigger when someone says "build an AI agent", "automate this workflow with AI", "I want the AI to do X autonomously", or describes a multi-step task they want AI to handle end-to-end.
---

# AI Agent Builder

## What Is an Agent?

An agent is an AI model that:
1. Takes a goal or task as input
2. Decides what actions to take (using tools, calling APIs, writing code)
3. Executes those actions
4. Observes the results
5. Continues until the task is complete

The key property: **the model controls the execution loop**, not your code.

---

## Agent Architectures

### 1. Single Agent (Linear)
One model executes a sequence of tool calls.
```
User Goal → Agent → [Tool Call] → [Observe] → [Tool Call] → [Observe] → Done
```
**Best for**: Focused tasks with a clear end state (research a topic, fill a form, generate a report)

### 2. Planner + Executor
One model creates a plan; another executes each step.
```
User Goal → Planner → [Step 1, Step 2, Step 3] → Executor → [Execute Each] → Done
```
**Best for**: Complex tasks that benefit from upfront planning (coding projects, data pipelines)

### 3. Multi-Agent (Orchestrator + Specialists)
One orchestrator routes subtasks to specialized agents.
```
User Goal → Orchestrator → [Research Agent] ↘
                         → [Writer Agent]    → Combine → Output
                         → [Editor Agent]   ↗
```
**Best for**: Tasks that require different expertise (build product: research + design + code)

### 4. Critic / Evaluator Loop
Agent generates output; critic scores and requests revisions.
```
Generate → Critique → Revise → Critique → [Accept if score ≥ threshold]
```
**Best for**: High-quality outputs (writing, code, analysis)

---

## Tool Design

Tools are the agent's hands. Well-designed tools = capable agents.

### Tool Design Principles
1. **Atomic**: Each tool does one thing
2. **Idempotent**: Calling the same tool twice doesn't break things
3. **Descriptive**: Tool name + description tells the model when and how to use it
4. **Safe defaults**: Prefer read operations; gate write/delete operations

### Tool Schema Template (OpenAI format)
```json
{
  "name": "search_web",
  "description": "Search the web for current information. Use when you need up-to-date facts, recent events, or information not in your training data.",
  "parameters": {
    "type": "object",
    "properties": {
      "query": {
        "type": "string",
        "description": "The search query. Be specific."
      },
      "num_results": {
        "type": "integer",
        "description": "Number of results to return (1-10)",
        "default": 5
      }
    },
    "required": ["query"]
  }
}
```

### Common Tool Categories

| Category | Examples |
|----------|---------|
| **Information retrieval** | web_search, read_file, query_database, get_page |
| **Code execution** | run_python, run_bash, execute_sql |
| **Data transformation** | parse_csv, extract_json, format_output |
| **External actions** | send_email, create_ticket, post_message, call_api |
| **File operations** | read_file, write_file, list_directory |
| **Memory** | save_note, retrieve_note, update_context |

---

## System Prompt Patterns

### Goal-Oriented Agent Prompt
```
You are an AI agent that [specific role].

## Your Task
[Clear description of the goal]

## Available Tools
[List tools and when to use each]

## Constraints
- [What you must NOT do]
- [Limits on tool usage]
- Ask for clarification if [specific ambiguous situations]

## Output Format
When complete, output: [expected format]

## Stopping Condition
You are done when: [clear completion criteria]
```

### Chain-of-Thought Instruction
Add to any agent prompt:
```
Before taking each action, think through:
1. What information do I have?
2. What do I need to find out?
3. What's the best next action?
4. What could go wrong?

Show your reasoning before each tool call.
```

---

## Agent Implementation (Python)

### Simple Agentic Loop
```python
import anthropic

client = anthropic.Anthropic()

def run_agent(goal: str, tools: list, max_iterations: int = 10) -> str:
    messages = [{"role": "user", "content": goal}]
    
    for iteration in range(max_iterations):
        response = client.messages.create(
            model="claude-opus-4-5",
            max_tokens=4096,
            tools=tools,
            messages=messages
        )
        
        # Add assistant response to history
        messages.append({"role": "assistant", "content": response.content})
        
        # Check if we're done
        if response.stop_reason == "end_turn":
            # Extract final text response
            return next(b.text for b in response.content if b.type == "text")
        
        # Execute tool calls
        tool_results = []
        for block in response.content:
            if block.type == "tool_use":
                result = execute_tool(block.name, block.input)
                tool_results.append({
                    "type": "tool_result",
                    "tool_use_id": block.id,
                    "content": str(result)
                })
        
        # Add tool results to history
        if tool_results:
            messages.append({"role": "user", "content": tool_results})
    
    return "Max iterations reached"

def execute_tool(name: str, input: dict) -> str:
    # Route to your tool implementations
    tools_map = {
        "search_web": search_web,
        "read_file": read_file,
        # ... add your tools
    }
    return tools_map[name](**input)
```

---

## Safety & Control Patterns

### Human-in-the-Loop Gates
Add approval steps before irreversible actions:
```python
REQUIRE_APPROVAL = ["send_email", "delete_file", "post_message", "make_payment"]

def execute_tool(name, input):
    if name in REQUIRE_APPROVAL:
        confirmed = ask_human_approval(name, input)
        if not confirmed:
            return "Action cancelled by user"
    return tools_map[name](**input)
```

### Budget Controls
```python
MAX_TOOL_CALLS = 50
MAX_COST_USD = 1.00
tool_call_count = 0
estimated_cost = 0.0
```

### Sandboxing Code Execution
- Never execute agent-generated code in production environment
- Use isolated containers (Docker) or sandboxed runners (e2b, Modal)
- Whitelist allowed operations; deny everything else

---

## Reliability Patterns

### Retry with Backoff
```python
import time

def call_with_retry(fn, max_retries=3):
    for attempt in range(max_retries):
        try:
            return fn()
        except Exception as e:
            if attempt == max_retries - 1:
                raise
            time.sleep(2 ** attempt)  # 1s, 2s, 4s
```

### Checkpoint / Resume
Save agent state after each tool call so you can resume after failure:
```python
def save_checkpoint(step, messages, results):
    with open(f"checkpoint_{step}.json", "w") as f:
        json.dump({"messages": messages, "results": results}, f)
```

### Structured Output for Reliability
For predictable agent outputs, use JSON mode or structured output:
```python
response = client.messages.create(
    model="claude-opus-4-5",
    system="Always respond with valid JSON matching this schema: {...}",
    messages=[...]
)
output = json.loads(response.content[0].text)
```

---

## Agent Evaluation Checklist

- [ ] Can the agent complete the core task end-to-end?
- [ ] Does it handle tool failures gracefully?
- [ ] Does it avoid infinite loops? (max iteration guard)
- [ ] Are destructive actions gated behind approval?
- [ ] Is cost bounded? (max tokens, max iterations)
- [ ] Is execution observable? (logs every tool call + result)
- [ ] Can it be resumed after failure?
- [ ] Has it been tested with adversarial inputs?
