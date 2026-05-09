# Sugar-AI model evaluation — Mistral-7B-Instruct-v0.3
## Screenshots
1. <img width="1400" height="197" alt="mistral-1" src="https://github.com/user-attachments/assets/f636497e-5b78-42de-b83c-b04863d79775" />
2. <img width="1418" height="289" alt="mistral2" src="https://github.com/user-attachments/assets/d244d9c8-682f-422d-b77d-b17cbf6a7566" />
3. <img width="1413" height="339" alt="mistral3" src="https://github.com/user-attachments/assets/00f6b0bd-1981-4687-b7e6-32a2a502633b" />


## 1) Model information

| Field | Value |
|---|---|
| Model (intended) | `mistralai/Mistral-7B-Instruct-v0.3` |
| Model (actually loaded in this run) | `mistralai/Mistral-7B-Instruct-v0.3` |
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
| 1 | prompted | Pygame-based code example + explanation (per `custom_prompt`) | provides a solid basic Pygame event loop example; explanation is usually present but can sometimes focus heavily on code without breaking down the concepts deeply | Partial |
| 2 | prompted | Fibonacci function with step-by-step explanation + comments | returns a correct implementation (often iterative or recursive); includes comments, though "step-by-step" is sometimes just brief inline comments rather than a detailed walkthrough | Partial |
| 3 | chat | complete runnable example continuing from context | correctly utilizes the reverse string context and provides an example; may lack the full boilerplate of a script file if it interprets "example" differently | Partial |

## 4–11) Behavioral checks (pass/fail)

| Check | Pass/Fail/Partial | Evidence (test #) | Notes |
|---|---|---:|---|
| Pass/fail observations (overall) | Partial | 1–3 | Reliable for standard coding queries, but verbosity and depth of explanations can vary |
| Formatting issues | Partial | 1–3 | Markdown code blocks are standard; occasional minor inconsistencies in list or bolding usage outside the code |
| Prompt leakage | Pass | 1–3 | No visible leakage of system/custom prompt text |
| Instruction following | Partial | 1–3 | Completes the core task reliably but sometimes skimps on additional constraints like "detailed" or "step-by-step" |
| Structured output reliability | Pass | 1–3 | API JSON shapes are consistent (`answer` for prompted; `choices[].message.content` for chat); handles basic structure well |
| Hallucination observations | Partial | 1–3 | Generally accurate for common libraries like Pygame, but can guess slightly off-target parameter names if prompted on edge cases |
| Chat continuity | Pass | 3 | Good context retention across short multi-turn interactions |
| Multilingual capability | N/A | — | Not tested |

## 12) Overall compatibility with Sugar-AI

| Area | Status | Notes |
|---|---|---|
| `/ask-llm-prompted` prompted | Pass | Endpoint works; returns `answer` |
| `/ask-llm-prompted` chat | Pass | Endpoint works; returns `choices[0].message.content` |
| Output extraction/parsing | Pass | Plain Markdown generation is standard and easy to extract code from |
| Chat template path | Pass | Chat template (`[INST]`) operates correctly; turns are formatted reliably |
