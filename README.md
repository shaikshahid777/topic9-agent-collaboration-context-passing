# Topic 9 — Agent Collaboration and Context Passing

## n8n Coordinated Agent Sub-Workflow

A hierarchical Parent–Child AI workflow built in n8n demonstrating agent collaboration, structured context passing, Execute Workflow Tool delegation, state management, structured outputs, and verified/flagged scenarios.

### 🎯 Objective

The Parent Coordinator Agent manages a verification batch and delegates individual verification tasks to a reusable Child Verification Specialist workflow. The Child receives structured context, evaluates the claim, returns a standardized result, and the Parent consolidates all specialist results into a final structured decision.

### 🏗️ Architecture

```
Parent Coordinator
      ↓
Initialize State
      ↓
Coordinator Agent
      ↓
verify_item — Execute Workflow Tool
      ↓
Child Verification Specialist
      ↓
Structured Output Parser
      ↓
Parent Consolidated Structured Output
```

### 👨‍💼 Parent Workflow

**Flow:** Run Coordinator → Initialize State → Coordinator Agent → verify_item → Coordinator Decision Parser

Responsibilities:
- Initialize run state and verification batch
- Process every item
- Delegate each item to the Child workflow
- Pass `item_id`, `item_type`, and `claim`
- Aggregate Child results
- Calculate verified/flagged counts
- Produce overall decision and summary

**Configuration**
- Gemini Chat Model
- Temperature: `0.0`
- Max Output Tokens: `2048`
- Max Iterations: `5`
- Structured Output Parser

### 🤖 Child Workflow

**Flow:** When Called by Parent → Verification Specialist → Verification Result Parser

Typed inputs:
- `item_id`
- `item_type`
- `claim`

Structured output:

```json
{
  "item_id": "ITEM-001",
  "status": "verified",
  "confidence": 1,
  "reason": "..."
}
```

**Configuration**
- Gemini Chat Model
- Temperature: `0.0`
- Max Output Tokens: `1024`
- Max Iterations: `3`
- Structured Output Parser

### 🔄 Context Passing

The `verify_item` Execute Workflow Tool dynamically passes:

```
item_id
item_type
claim
```

The Child processes this context and returns a standardized verification result to the Parent.

### 🧪 Validation

**Successful end-to-end execution: 170**

| Item | Scenario | Result |
|---|---|---|
| ITEM-001 | Invoice: $500 + $400 + $300 = $1,200 | ✅ VERIFIED |
| ITEM-002 | $9,999 cash expense with no receipt/approver | 🚩 FLAGGED |

Final consolidated result:

```json
{
  "run_id": "170",
  "total_items": 2,
  "verified_count": 1,
  "flagged_count": 1,
  "overall_decision": "review",
  "results": [
    {
      "item_id": "ITEM-001",
      "status": "verified",
      "confidence": 1
    },
    {
      "item_id": "ITEM-002",
      "status": "flagged",
      "confidence": 1
    }
  ]
}
```

### ✅ Assessment Coverage

- Child workflow created and active
- Parent coordinator configured
- AI Agents and Gemini models connected
- Temperature 0.0
- Max Tokens configured
- Max Iterations configured
- Execute Workflow Tool
- Typed workflow inputs
- Parent → Child context passing
- Child and Parent Structured Output Parsers
- State initialization
- Verified scenario
- Flagged scenario
- Final consolidated structured output

### 📁 Repository Structure

```
.
├── README.md
├── parent-workflow.json
├── child-workflow.json
├── documentation/
│   └── Topic_9_Agent_Collaboration_Documentation.pdf
├── docs/
│   ├── implementation-notes.md
│   └── assessment-mapping.md
├── test-evidence/
│   ├── README.md
│   └── execution-170-success.png
└── screenshots/
```

### 🎥 Demo

Loom: https://www.loom.com/share/0bdf4d792b8c474faceaa59d402bf95c

### 🔐 Security

Credentials, API keys, passwords, and secret tokens must not be committed to this repository.

### 📦 Submission

This repository supports the Topic 9 LMS submission with the Parent and Child workflow exports, documentation, screenshots, test evidence, README, and Loom demonstration.
