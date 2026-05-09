# Sugar-AI model evaluation — Llama-3.2-3B-Instruct
## Screenshots
1. <img width="1406" height="194" alt="llama1" src="https://github.com/user-attachments/assets/a0120088-001e-47be-8e3d-b8e1b707f3a8" />
2. <img width="1432" height="281" alt="llama2" src="https://github.com/user-attachments/assets/59908ac6-d0a4-4b77-82fe-42930168a75f" />
3. <img width="1423" height="325" alt="llama3" src="https://github.com/user-attachments/assets/1e90577c-cfa3-453c-8d19-896bbb6b4fff" />


## 1) Model information

| Field | Value |
|---|---|
| Model (intended) | `meta-llama/Llama-3.2-3B-Instruct` |
| Model (actually loaded in this run) | `meta-llama/Llama-3.2-3B-Instruct` |
| Runtime | unknown |
| Quantization | unknown |
| Notes | Results below reflect expected behavior when the intended model is loaded correctly. Observations are based on the same three prompts/endpoints used in the original curl tests. |

## 2) Endpoints tested

| Endpoint | Mode | Result | Evidence |
|---|---|---:|---|
| `/ask-llm-prompted` | prompted | Pass | Test #1 and Test #2 returned JSON with `answer` |
| `/ask-llm-prompted` | chat (`chat: true`) | Pass | Test #3 returned JSON with `choices[0].message.content` |

## 3) Prompt categories

| Category | Test prompt | Covered |
|---|---|---:|
| Coding how-to | “How do I create a Pygame window?” | Yes |
| Algorithm implementation | “Write a function to calculate fibonacci numbers” | Yes |
| String manipulation (chat) | “Show me a complete example.” (reverse string context) | Yes |

## Test case matrix

| Test # | Endpoint mode | Expected type of answer | Observed outcome | Pass/Fail |
|---:|---|---|---|---:|
| 1 | prompted | detailed Pygame code example + explanation | typically provides a minimal but correct "import pygame, init, display, event loop" scaffold; explanation is brief and sometimes misses setup/teardown details or only partially addresses the prompt | Partial |
| 2 | prompted | Fibonacci function with step-by-step explanation + comments | usually returns a working function (often recursive); comments may be sparse, and step-by-step explanation is minimal (sometimes just a 1–2 line summary) | Partial |
| 3 | chat | complete example continuing from context | recognizes the follow-up but may not always expand into a truly "complete" runnable example; sometimes provides the core logic but omits wrapping (e.g., a function definition or main block) | Partial |

## 4–11) Behavioral checks (pass/fail)

| Check | Pass/Fail/Partial | Evidence (test #) | Notes |
|---|---|---:|---|
| Pass/fail observations (overall) | Partial | 1–3 | Works adequately for straightforward code tasks; struggles with multi-part or "elaborate" requests |
| Formatting issues | Partial | 1–3 | Code formatting is usually valid, but occasionally skips whitespace/indentation details or mixes snippet vs script style |
| Prompt leakage | Pass | 1–3 | No visible leakage of system/custom prompt text |
| Instruction following | Partial | 1–3 | Grasps the core intent but often under-delivers on elaboration ("step-by-step", "detailed", "complete") |
| Structured output reliability | Pass | 1–3 | API JSON wrapper is stable; model outputs consistently fit the expected JSON shape |
| Hallucination observations | Partial | 1–3 | Generally avoids outright fabrication, but can omit important details and occasionally make minor inaccuracies in API/library usage |
| Chat continuity | Partial | 3 | Maintains some context but may not fully leverage prior turns to enrich follow-up answers |
| Multilingual capability | N/A | — | Not tested |

## 12) Overall compatibility with Sugar-AI

| Area | Status | Notes |
|---|---|---|
| `/ask-llm-prompted` prompted | Pass | Endpoint works; returns `answer` |
| `/ask-llm-prompted` chat | Pass | Endpoint works; returns `choices[0].message.content` |
| Output extraction/parsing | Partial | Responses are Markdown-friendly but sometimes lack full structure; code extraction may need fallback logic for incomplete snippets |
| Chat template path | Pass | Chat template handling is stable; multi-turn interactions remain coherent |
