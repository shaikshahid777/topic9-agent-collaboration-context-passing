# Test Evidence

## Successful End-to-End Run

**Execution:** 170  
**Status:** Success

### Scenario 1 — Verified
- Item: ITEM-001
- Type: invoice
- Claim: Invoice total of $1,200 equals $500 + $400 + $300.
- Result: VERIFIED
- Confidence: 1

### Scenario 2 — Flagged
- Item: ITEM-002
- Type: expense
- Claim: A $9,999 cash expense with no receipt and no approver.
- Result: FLAGGED
- Confidence: 1

### Consolidated Result
- Total items: 2
- Verified count: 1
- Flagged count: 1
- Overall decision: review

## Recommended Screenshots
Capture the following from n8n:
1. Parent workflow canvas
2. Initialize State configuration
3. Coordinator Agent configuration
4. verify_item Execute Workflow Tool
5. Child workflow canvas
6. Child typed inputs
7. Child Structured Output Parser
8. Parent Structured Output Parser
9. Execution 170 success
10. Final consolidated JSON

## Demo
Loom: https://www.loom.com/share/0bdf4d792b8c474faceaa59d402bf95c
