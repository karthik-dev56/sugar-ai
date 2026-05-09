# Sugar-AI model evaluation — Phi-3.5-mini-instruct
## Screenshots
1.<img width="1420" height="213" alt="phi-mc" src="https://github.com/user-attachments/assets/076c4b0a-00d8-429b-92f9-c7773d3f18cf" />
2. <img width="1410" height="274" alt="phi-mc1" src="https://github.com/user-attachments/assets/d016c3d1-f464-4dff-91ef-eb9a09e24340" />
3. <img width="1415" height="381" alt="phi-mc3" src="https://github.com/user-attachments/assets/4df3a204-f160-43d6-b3e4-2bf8fbd72974" />



## 1) Model information

| Field | Value |
|---|---|
| Model (intended) | `microsoft/Phi-3.5-mini-instruct` |
| Model (actually loaded in this run) | `microsoft/Phi-3.5-mini-instruct` |
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
| 1 | prompted | Pygame-based code example + explanation (per `custom_prompt`) | typically produces a compact, correct “create window + event loop” snippet; may omit some operational details (FPS limiting, error handling) and can be light on explanation unless explicitly asked for more | Partial |
| 2 | prompted | Fibonacci function with step-by-step explanation + comments | generally returns a correct iterative solution; tends to keep comments minimal and may not provide a truly “step-by-step” walkthrough beyond a short explanation | Partial |
| 3 | chat | complete runnable example continuing from context | follows the reverse-string request and often provides the correct `s[::-1]` or `reversed()` approach; occasionally the “complete example” is still a snippet rather than a runnable script with sample I/O | Partial |

## 4–11) Behavioral checks (pass/fail)

| Check | Pass/Fail/Partial | Evidence (test #) | Notes |
|---|---|---:|---|
| Pass/fail observations (overall) | Partial | 1–3 | Solid for short, direct answers; less reliable when asked for long “tutorial style” outputs |
| Formatting issues | Partial | 1–3 | Usually provides code fences; sometimes mixes snippet vs full script formatting |
| Prompt leakage | Pass | 1–3 | No visible leakage of system/custom prompt text |
| Instruction following | Partial | 1–3 | Usually follows the core task; may under-deliver on verbosity and “complete runnable example” expectations |
| Structured output reliability | Pass | 1–3 | JSON wrapper is stable and the model tends to produce Markdown-friendly content |
| Hallucination observations | Partial | 1–3 | Can occasionally assert unverified details (e.g., exact library behavior) and may include small code slips if not grounded by explicit constraints |
| Chat continuity | Partial | 3 | Handles short follow-ups, but may not consistently carry context into a polished end-to-end example |
| Multilingual capability | N/A | — | Not tested |

## 12) Overall compatibility with Sugar-AI

| Area | Status | Notes |
|---|---|---|
| `/ask-llm-prompted` prompted | Pass | Endpoint works; returns `answer` |
| `/ask-llm-prompted` chat | Pass | Endpoint works; returns `choices[0].message.content` |
| Output extraction/parsing | Partial | Mostly clean; snippet formatting can vary, which may complicate automated code extraction if needed |
| Chat template path | Pass | Chat template support is stable; responses remain well-formed across turns |
