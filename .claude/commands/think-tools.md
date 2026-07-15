---
allowed-tools: Read, Glob, Grep, LS, Bash(python3:*), Bash(find:*), Bash(git log:*), Bash(git diff:*)
description: Extended thinking + tool use for multi-step problems requiring both deep reasoning and live data/code access. Use for security reviews, architecture analysis of real codebases, debugging with codebase exploration.
---

# /think-tools — Extended Thinking with Tool Use

You are in **EXTENDED THINKING + TOOL USE MODE**. You must reason deeply between each tool call, not just after all tools complete.

## Problem to Solve
$ARGUMENTS

---

## CRITICAL: HOW THINKING WORKS WITH TOOLS

Thinking happens **between** tool calls, not during them. The correct mental model:

```
User request
    ↓
[THINK] → Which tool do I need first? What am I looking for?
    ↓
Tool call (Grep / Read / Bash)
    ↓
[THINK] → What did this tell me? What do I need next? Any surprises?
    ↓
Tool call (another tool based on thinking)
    ↓
[THINK] → Do I have enough information? What's my conclusion?
    ↓
Final answer
```

**Do not chain tool calls without thinking between them.** Each tool result should be processed with a reasoning step before the next call.

---

## THINKING BLOCK PRESERVATION (CRITICAL FOR TOOL USE)

When tool use is involved across multiple API turns, thinking block signatures MUST be preserved.

```python
def run_agentic_loop(client, messages, tools, model="claude-sonnet-4-6"):
    """
    Correct implementation: preserves thinking blocks across tool calls.
    """
    while True:
        response = client.messages.create(
            model=model,
            max_tokens=16000,
            thinking={"type": "enabled", "budget_tokens": 10000},
            tools=tools,
            messages=messages
        )
        
        # CRITICAL: append full response content (including thinking blocks)
        # to messages before next turn — never strip thinking blocks
        messages.append({
            "role": "assistant",
            "content": response.content  # includes thinking + tool_use blocks
        })
        
        if response.stop_reason == "end_turn":
            break
            
        if response.stop_reason == "tool_use":
            tool_results = []
            
            for block in response.content:
                if block.type == "tool_use":
                    # Execute the tool
                    result = execute_tool(block.name, block.input)
                    tool_results.append({
                        "type": "tool_result",
                        "tool_use_id": block.id,
                        "content": result
                    })
            
            # Add tool results to conversation
            messages.append({
                "role": "user",
                "content": tool_results
            })
    
    return messages, response

def execute_tool(name, inputs):
    """Map tool names to actual implementations."""
    tools_map = {
        "read_file": lambda i: open(i["path"]).read(),
        "bash": lambda i: subprocess.run(i["command"], capture_output=True, text=True).stdout,
        # add your tools here
    }
    return json.dumps(tools_map[name](inputs))
```

**What happens if you strip thinking blocks before passing back:**
```
API Error: thinking block signature mismatch
# The signature is a cryptographic hash of the conversation context.
# Modifying any prior message (including stripping thinking blocks)
# invalidates the signature and the API rejects the request.
```

---

## COMMON ERRORS AND FIXES

```python
# ERROR 1: Modifying previous content
messages[-1]["content"][0]["thinking"] = "my edited version"  # BREAKS signature

# FIX: Never touch previous content
# Pass it back exactly as received

# ERROR 2: Stripping thinking blocks to save tokens
content_without_thinking = [b for b in response.content if b.type != "thinking"]
messages.append({"role": "assistant", "content": content_without_thinking})  # BREAKS

# FIX: Pass all blocks including thinking
messages.append({"role": "assistant", "content": response.content})

# ERROR 3: Using temperature with thinking
response = client.messages.create(
    temperature=0.7,           # INCOMPATIBLE
    thinking={"type": "enabled", "budget_tokens": 5000},
    ...
)  # API error

# FIX: Remove temperature when using thinking
```

---

## TOOL DEFINITION FORMAT

```python
tools = [
    {
        "name": "tool_name",
        "description": "Clear description of what this does and when to use it",
        "input_schema": {
            "type": "object",
            "properties": {
                "param_name": {
                    "type": "string",
                    "description": "What this parameter controls"
                }
            },
            "required": ["param_name"]
        }
    }
]
```

---

## EXECUTION PROTOCOL FOR THIS SESSION

### Step 1: Think about the problem
Before using any tool, reason through:
- What information do I need?
- Which tool gets me there fastest?
- What would a surprising or unexpected result look like?

### Step 2: Use tools deliberately
Each tool call must have a clear hypothesis it is testing or information it is retrieving.

### Step 3: Think after each tool result
- Does this confirm or contradict my hypothesis?
- What does this change about my approach?
- What is the minimum next tool call needed?

### Step 4: Synthesize
When you have enough information, stop calling tools and synthesize. Don't call tools for information you already have.

---

## OUTPUT FORMAT

### Reasoning Summary
Brief summary of what you discovered through tool use and thinking.

### Findings
Concrete, evidence-backed conclusions. Cite specific files, line numbers, function names where relevant.

### Recommendations / Implementation
Actionable next steps or complete implementation. No speculation — only what the evidence supports.

### Confidence
What you are certain about vs. what required assumptions. What additional information would change your conclusions.