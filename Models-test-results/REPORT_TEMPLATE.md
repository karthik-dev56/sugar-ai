# Sugar-AI Model Evaluation Report (Template)

## 1) Model information

| Field | Value |
|---|---|
| Model (intended) | `<org>/<model>` |
| Model (actually loaded) | `<org>/<model>` / `unknown` |
| Revision / hash | `latest` / `<hash>` / `unknown` |
| Runtime | CPU / CUDA |
| Quantization | none / 4-bit (bnb) |
| Transformers version | `<version>` |
| Notes | `<1-line>` |

## 2) Endpoints tested

| Endpoint | Mode | Request type | Result | Notes |
|---|---|---|---|---|
| `/ask` | RAG | query param | Pass / Fail / N/A | |
| `/ask-llm` | direct | query param | Pass / Fail / N/A | |
| `/ask-llm-prompted` | prompted | JSON | Pass / Fail / N/A | |
| `/ask-llm-prompted` | chat | JSON (`chat: true`) | Pass / Fail / N/A | |
| `/debug` | debug/context | query params | Pass / Fail / N/A | |

## 3) Prompt categories

| Category | Test prompt(s) used | Coverage | Notes |
|---|---|---|---|
| Coding how-to | `<prompt>` | Covered / Not covered | |
| Algorithm implementation | `<prompt>` | Covered / Not covered | |
| String manipulation | `<prompt>` | Covered / Not covered | |
| Other | `<prompt>` | Covered / Not covered | |

## 4–11) Behavioral checks (pass/fail)

| Check | Pass/Fail/Partial | Evidence (test #) | Notes (1 line) |
|---|---|---|---|
| Pass/fail observations (overall) |  |  |  |
| Formatting issues |  |  |  |
| Prompt leakage |  |  |  |
| Instruction following |  |  |  |
| Structured output reliability |  |  |  |
| Hallucination observations |  |  |  |
| Chat continuity |  |  |  |
| Multilingual capability | N/A |  | Not tested |

## 12) Overall compatibility with Sugar-AI

| Area | Status | Notes |
|---|---|---|
| Startup load | Pass / Fail / Unknown | |
| `/ask-llm-prompted` prompted | Pass / Fail | |
| `/ask-llm-prompted` chat | Pass / Fail | |
| Output parsing (extracting answer) | Pass / Fail / Partial | |
| Chat template (`tokenizer.apply_chat_template`) | Pass / Fail / Partial | |
| RAG path (`/ask`) | Pass / Fail / N/A | |
| Admin model change (`/change-model`) | Pass / Fail / N/A | |
