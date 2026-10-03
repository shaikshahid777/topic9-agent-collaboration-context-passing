<!-- SHOWCASE_START --><div align="center">[![Typing](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=22&duration=2800&pause=900&color=58A6FF&center=true&vCenter=true&width=900&lines=topic9%20agent%20collaboration%20context%20passing;AI%20%7C%20Automation%20%7C%20Engineering;Explore%20the%20project%20%F0%9F%9A%80)](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing)<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,50:161B22,100:58A6FF&height=110&section=header&text=topic9-agent-collaboration-context-passing&fontSize=26&fontColor=FFFFFF&animation=twinkling&fontAlignY=65" width="100%" alt="Animated project banner"/>

[![Repository](https://img.shields.io/badge/Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing) [![Issues](https://img.shields.io/badge/Report-Issue-red?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/issues/new) [![Stars](https://img.shields.io/github/stars/shaikshahid777/topic9-agent-collaboration-context-passing?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/stargazers) [![Fork](https://img.shields.io/github/forks/shaikshahid777/topic9-agent-collaboration-context-passing?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/fork) [![Profile](https://img.shields.io/badge/Profile-Visit-0A66C2?style=for-the-badge&logo=github)](https://github.com/shaikshahid777)</div>

> ✨ **Project Showcase Mode:** animated banner • interactive navigation • live repository actions

[🚀 Repository](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing) · [🐞 Report Issue](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/issues/new) · [⭐ Star](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/stargazers) · [🔱 Fork](https://github.com/shaikshahid777/topic9-agent-collaboration-context-passing/fork) · [👤 Profile](https://github.com/shaikshahid777)

<!-- SHOWCASE_END -->

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
