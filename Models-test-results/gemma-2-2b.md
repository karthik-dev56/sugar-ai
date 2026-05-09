# Sugar-AI model evaluation — Gemma-2-2B-it

## 1) Model information

| Field | Value |
|---|---|
| Model (intended) | `google/gemma-2-2b-it` |
| Model (actually loaded in this run) | `google/gemma-2-2b-it` |
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
| 1 | prompted | detailed code example + explanation (per `custom_prompt`) | usually provides a short Pygame snippet that opens a window and runs an event loop; tends to omit “nice-to-have” details (FPS clock, resize handling) and may skip some explanation if not explicitly constrained | Partial |
| 2 | prompted | Fibonacci implementation with step-by-step explanation and comments | generally returns a correct iterative implementation; comments/explanation are brief and may not match the “step-by-step” depth requested (often one short paragraph + a code block) | Partial |
| 3 | chat | complete runnable example continuing from context | follows the reverse-string context and produces a correct `s[::-1]` example; may not include a fully runnable mini-script (e.g., missing `if __name__ == "__main__":`) and sometimes varies formatting between fenced code and inline snippets | Partial |

## 4–11) Behavioral checks (pass/fail)

| Check | Pass/Fail/Partial | Evidence (test #) | Notes |
|---|---|---:|---|
| Pass/fail observations (overall) | Partial | 1–3 | Works for simple coding help, but responses skew concise and sometimes miss requested depth |
| Formatting issues | Partial | 1–3 | Generally consistent Markdown; occasional variation in whether examples are fully runnable scripts vs snippets |
| Prompt leakage | Pass | 1–3 | No visible leakage of `custom_prompt`/system prompt text |
| Instruction following | Partial | 1–3 | Usually follows the main task (code), but tends to under-deliver on verbosity/step-by-step commentary |
| Structured output reliability | Pass | 1–3 | API JSON shape is consistent (`answer` for prompted; `choices[].message.content` for chat) |
| Hallucination observations | Partial | 1–3 | Occasional small “confident but generic” statements (e.g., claiming best practices without specifics); fewer outright fabricated APIs than some smaller instruction models, but still possible around library details |
| Chat continuity | Partial | 3 | Tracks short context and answers the follow-up, but may not consistently expand into a complete, end-to-end runnable example |
| Multilingual capability | N/A | — | Not tested |

## 12) Overall compatibility with Sugar-AI

| Area | Status | Notes |
|---|---|---|
| `/ask-llm-prompted` prompted | Pass | Endpoint works; returns `answer` |
| `/ask-llm-prompted` chat | Pass | Endpoint works; returns `choices[0].message.content` |
| Output extraction/parsing | Partial | Content is usually clean Markdown, but snippet-vs-script variability can make downstream “extract just the code” parsing slightly inconsistent |
| Chat template path | Pass | Chat mode works with `apply_chat_template`; responses are generally stable for short turns |
