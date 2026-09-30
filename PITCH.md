# BhashaBridge — 2-minute pitch and demo script

## Opening (0:00–0:20)

“India’s best ideas are often multilingual. But when a team speaks in three languages, the person who is not fluent in the dominant language loses context — and the team loses action.

This is **BhashaBridge**: a private, multilingual conversation copilot that runs locally on a Snapdragon-powered HP PC.”

## Show the problem (0:20–0:45)

“Riya speaks Hindi. Arjun speaks English. Neha speaks Kannada. Today, they either slow the meeting down, use a cloud service they may not trust, or leave someone behind.”

Start the demo. Point to the mixed-language transcript.

## Show the magic (0:45–1:15)

“BhashaBridge keeps the original words, translates them live, and turns the conversation into ownership. Notice the three action items: who owns what, and by when.”

Point to the action cards. Say:

“The key insight is that translation is not the end goal. **Shared understanding and accountable action are.**”

## Show Snapdragon fit (1:15–1:40)

“Now I’ll disable the network. The session still works. Speech recognition, translation and action extraction run on-device through a quantized, NPU-first model pipeline. No audio leaves this PC, so it is useful in classrooms, field work and sensitive team meetings.”

If a real offline model is not connected in the demo, say: “This prototype simulates the local inference response; the deployment path is Qualcomm AI Hub / GenieX with a Qualcomm-optimized ASR model and Qwen3 4B.” Never claim a benchmark that has not been measured.

## Close (1:40–2:00)

“BhashaBridge makes Snapdragon AI personal in the most practical way: it gives every voice a place in the conversation, works when connectivity fails, and lets the user delete the memory in one tap.

We are not putting a chatbot on a laptop. We are giving every participant a fair chance to be heard — and every team a trusted next step.”

## Live demo checklist

- Open `index.html` in a Chromium-based browser.
- Keep the browser window at 1280×900 or larger.
- Click **Start listening** once before the pitch, then stop after the offline moment.
- Change the output language dropdown to show the interaction state.
- Do not claim real microphone/model inference unless the native integration is connected.
- Keep the proposal open separately for technical questions.

## Judge Q&A answers

**Why must this be on-device?**  
Because the differentiator is not only latency. Teams may be discussing student records, customer data, unpublished work or community issues. Local processing makes privacy and offline access practical.

**Why not just use a cloud translator?**  
Cloud tools are useful, but they require connectivity, add round-trip delay and may be inappropriate for sensitive conversations. BhashaBridge provides a local baseline and makes the trade-off visible to the user.

**What is the Qualcomm AI Hub contribution?**  
It provides the model library and the optimization/validation path for Snapdragon devices. We will profile ASR and language models, quantize them, and select the best CPU/GPU/NPU route for the target HP configuration.

**How do you prevent hallucinated tasks?**  
Action items are emitted as structured objects only when the model can cite a source utterance. Low-confidence items are shown as suggestions, not silently added to the plan.

**What is genuinely innovative?**  
The product is designed around a mixed-language group’s shared plan, not around a monolingual transcript or generic assistant. Multilingual understanding, local privacy and action extraction are one workflow.
