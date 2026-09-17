Task 1 — Graph Design

The shared AFLState contains the user query, conversation history, detected intent, tool results, final response, and trace information.

The graph explicitly routes:

factual → direct answer

retrieval → retrieval tool

prediction → prediction tool

off-topic → refusal

The branches converge on response formatting. Explicit routing gives prediction requests a controlled path so probabilistic framing and validation are applied consistently.

Task 2 — Router

The lightweight router detects:

prediction: winner/top-score requests

retrieval: statistics/results requests

factual: general AFL facts/rules/history

off-topic: requests outside AFL

The supplied routing evaluation contains 20 varied queries.

Task 3 — Prediction Tools

The Day 2 match-winner and top-player models are wrapped into the prediction path.

Team aliases are resolved, including examples such as:

Pies → Collingwood Magpies

Cats → Geelong Cats

Lions → Brisbane Lions

Swans → Sydney Swans

Prediction responses include probability and a short grounding explanation based on model features.

The application does not invent a fixture when a requested date is unavailable.

Task 4 — Validation and Fallback

After retrieval/prediction, the validation node checks whether a usable tool result exists.

If a team/player cannot be resolved, or a requested fixture is unavailable, the application asks for clarification instead of guessing.

Unsupported prediction types use a fallback response explaining what the application supports.

Task 5 — End-to-End Testing

Ten end-to-end cases cover:

factual questions

retrieval

match prediction

top-player prediction

off-topic refusal

ambiguous input

unsupported prediction

missing/current-week fixture

multi-turn follow-up
