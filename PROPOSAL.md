# BhashaBridge
## Private multilingual understanding for every team, classroom and community

**Challenge:** Snapdragon AI Lab Build & Present Challenge 2026  
**Category:** On-device AI · accessibility · productivity  
**Target:** Snapdragon-powered HP PC running Windows  
**Submission status:** Working interaction prototype + implementation and validation plan  

> **One-sentence value proposition:** BhashaBridge turns a mixed-language conversation into a shared, traceable action plan—without sending the conversation to the cloud.

---

## Executive summary for judges

India’s teams, classrooms and community projects are multilingual by default. BhashaBridge is a local-first conversation copilot that transcribes, translates and extracts action items from a mixed-language conversation on a Snapdragon-powered HP PC.

The product is deliberately more focused than a generic chatbot:

- **It makes every participant understandable**, preserving the original utterance beside the translation.
- **It makes the meeting actionable**, extracting only evidence-backed owners, tasks and dates.
- **It makes privacy visible**, keeping audio and derived notes on the PC and providing one-tap deletion.
- **It makes the Snapdragon advantage tangible**, continuing to work without a network connection through a quantized NPU-first model pipeline.

The prototype demonstrates the end-user workflow. The implementation plan below defines the Qualcomm AI Hub model path, the Windows deployment boundary and the measurements required before making performance claims.

## 1. The human problem

A multilingual group can be technically connected yet practically divided. A Hindi-speaking student may understand the idea but miss the English action item. A Kannada-speaking maker may contribute to the prototype but be left out of the written plan. A community worker may have no reliable internet connection at all.

Cloud meeting assistants do not fully solve this problem: they assume connectivity, add round-trip latency and may be inappropriate for sensitive discussions. The result is lost context, unequal participation and tasks that nobody clearly owns.

**Design question:** Can an everyday Snapdragon PC help a group understand one another and leave with a trustworthy plan—privately and offline?

## 2. The solution

BhashaBridge is a **local-first multilingual conversation copilot** with four connected actions:

1. **Listen** — detect speech turns and transcribe supported languages on-device.
2. **Bridge** — show the original text and translate it into each participant’s selected output language.
3. **Act** — extract evidence-backed action items, owners and deadlines into a shared plan.
4. **Forget** — keep the session local by default, make export explicit and delete audio/transcript/derived notes in one action.

The product’s unit of value is not a transcript. It is **shared understanding that becomes accountable action**.

### Primary users

- Student teams collaborating across Indian languages.
- Teachers and learners in multilingual classrooms.
- Small businesses and field teams working with intermittent connectivity.
- Community and maker projects where privacy and low-cost access matter.

### Why this use case is competition-fit

It is easy to understand in a live demo, directly benefits from on-device AI, has a meaningful Indian context, and creates room for Qualcomm AI Hub optimization rather than treating the device as a thin client for a cloud API.

## 3. The 60-second proof demo

The judging demo is intentionally designed as a before/after moment:

1. Start a session with English output selected.
2. Riya speaks Hindi: “We will prepare the solar sensor prototype for next week.”
3. BhashaBridge shows the Hindi original plus the English translation.
4. Arjun responds in English; Neha responds in Kannada.
5. The action panel produces three cards with owner, task, due date and source quote.
6. Disable Wi-Fi / enable airplane mode; the same local workflow continues.
7. Delete the session; the audio, transcript and derived action items disappear.

**Judge takeaway:** Three languages become one plan, while the sensitive conversation stays on the PC.

The current HTML prototype accurately demonstrates the interaction and product states. It does **not** claim that live ASR is already wired into the browser. The final native build will replace the illustrative transcript with measured local inference.

## 4. Why Snapdragon-powered HP PCs

BhashaBridge is designed around the Snapdragon PC rather than merely ported to it:

- **NPU-first inference:** speech, translation and language understanding can be routed through Qualcomm-supported runtimes to reduce CPU load.
- **Heterogeneous compute:** the runtime can select CPU/GPU/NPU execution per model and workload.
- **Offline responsiveness:** local inference removes network round trips and keeps the core experience available when connectivity is absent.
- **Power-conscious sessions:** compact, quantized models and staged inference suit an assistant that may run throughout a class or meeting.
- **Windows accessibility:** microphone, captions, keyboard navigation and export controls work on a familiar PC form factor.

Qualcomm AI Hub provides the model discovery, optimization and device-validation path. Its current platform supports optimized models, custom-model workflows and on-device deployment; the final implementation will benchmark the selected models on the actual target HP configuration before locking the model profile.

## 5. Technical implementation

### 5.1 End-to-end architecture

```text
Microphone
  → voice activity detection + speaker-turn segmentation
  → multilingual ASR
  → language identification + translation
  → Qwen3 4B (structured action extraction)
  → confidence + source-quote validation
  → local encrypted session store
  → Windows UI: transcript, translation and action plan
```

### 5.2 Model and runtime plan

| Stage | Candidate implementation | Snapdragon optimization step | Output |
|---|---|---|---|
| Speech activity | Lightweight VAD | CPU/NPU profiling; avoid running the LLM on silence | Speech segments |
| Transcription | Qualcomm AI Hub-compatible Whisper-family ASR | Quantize, compile and benchmark on target HP PC | Timestamped text + confidence |
| Translation | Compact open-source multilingual model for launch languages | Compare NPU and CPU paths; cache repeated language direction | Original + translated text |
| Understanding | **Qwen3 4B Hardware Optimized** or equivalent Qualcomm AI Hub model | Quantized structured generation with constrained JSON schema | Action objects |
| Optional vision | OCR model for whiteboards and worksheets | Add only after speech MVP meets latency target | Text blocks with source image |
| Runtime | GenieX / Qualcomm AI Runtime, with ONNX Runtime where appropriate | Profile memory, thermals, latency and battery | Device-ready local service |

**Launch language scope:** English, Hindi and one additional Indian language selected after a measured accuracy/latency comparison. The product will expand language coverage only after testing; it will not claim universal Indian-language support without evidence.

### 5.3 Trustworthy action extraction

Every action item is represented as:

```json
{
  "owner": "Arjun",
  "task": "Share the test plan",
  "due": "Friday",
  "source_quote": "I’ll own the test plan and share it by Friday.",
  "confidence": 0.94
}
```

The UI shows the source quote. If the model cannot identify an owner, task and supporting utterance, it returns a suggestion or no action instead of silently inventing one.

### 5.4 Privacy and data lifecycle

- Audio is processed locally and is not sent to a remote API.
- Retention is off by default; the user explicitly chooses whether to keep a session.
- Local persistence uses OS-protected storage in the Windows build.
- Export is user initiated and clearly labeled.
- Delete removes source audio, transcript, translations and derived action items.
- A persistent “processing locally” indicator makes the privacy boundary visible.
- Low-confidence transcription/translation is marked rather than presented as certain.

## 6. Judging criteria evidence map

### A. Technical Implementation

**What is implemented now:** responsive interaction prototype, transcript/translation/action-item workflow, local-status states, language selector and start/stop interaction.

**What will be demonstrated in the final native build:** a Windows local inference service, Qualcomm AI Hub-optimized ASR, structured action extraction, offline execution and deletion lifecycle.

**Evidence to submit:**

- Target-device model and runtime versions.
- Before/after model optimization results.
- Latency and memory logs for each pipeline stage.
- Offline test recording.
- Accuracy test set and error examples.
- Short screen recording showing source-quote traceability and deletion.

### B. Application Use Case & Innovation

BhashaBridge is not “a chatbot with translation.” Its innovation is the combination of:

1. mixed-language conversation support,
2. local privacy and offline access,
3. transparent translation with original text preserved, and
4. evidence-backed conversion from speech to shared ownership.

The concept has a clear social utility without requiring users to learn a new workflow: they speak, read the bridge, and leave with a plan.

### C. Deployment & Accessibility

- Windows desktop packaging for Snapdragon-powered HP PCs.
- First-run model bundle installation; core use thereafter without internet.
- Light and quality model profiles for device variability.
- Keyboard-accessible controls and high-contrast captions.
- Clear speaker labels, readable type and original-text fallback.
- Optional text-only mode for users who cannot or do not want to use a microphone.
- No mandatory account or cloud service for the core workflow.

### D. Presentation & Documentation

The package includes a timed pitch, live-demo sequence, technical README, judge Q&A, scorecard and this proposal. The story is structured around one memorable proof point—**airplane mode plus useful output**—and avoids presenting unmeasured UI values as benchmark results.

## 7. Validation plan and success thresholds

The final build will be evaluated on a named Snapdragon-powered HP PC using a scripted multilingual set and a small user test. Targets are **acceptance thresholds for the prototype**, not current claims:

| Measure | Method | Target before final submission |
|---|---|---|
| End-of-utterance to translated text | 30 scripted utterances, median and p95 | Median ≤ 2.0 s; p95 ≤ 4.0 s |
| Action-item precision | 50 labeled utterance groups | ≥ 90% precision; zero invented owners in the test set |
| Action-item recall | Same labeled groups | ≥ 80% recall for explicit tasks |
| Offline reliability | 10 complete sessions with network disabled | 10/10 sessions complete core workflow |
| Translation usefulness | 5–10 multilingual participants, 5-point rating | ≥ 4.0/5 average usefulness |
| Memory stability | 30-minute session | No crash; bounded memory growth |
| Power impact | 30-minute local session vs idle baseline | Record and disclose measured delta |
| Privacy behavior | Inspect network and deletion lifecycle | No audio egress; deleted session unrecoverable through the app |

If a target is missed, the result will be disclosed with the mitigation—smaller model, narrower language scope, or a clearer confidence fallback—instead of being hidden.

## 8. Deployment plan

### Phase 1 — working vertical slice

English + Hindi + one additional language; local ASR; translated captions; action JSON; offline demo; deletion.

### Phase 2 — Snapdragon optimization

Compile and profile each model through Qualcomm AI Hub / supported runtimes. Compare CPU, GPU and NPU routes; select the best latency/power profile for the target HP PC.

### Phase 3 — user hardening

Add confidence cues, editable transcript, source quotes, noise/ accent tests, accessibility review and model-bundle versioning.

### Phase 4 — expansion

Add more languages, whiteboard OCR, classroom mode and optional Arduino UNO Q sensor-event capture. These are extensions, not dependencies for the core judging demo.

## 9. Risks, ethics and mitigations

| Risk | Mitigation |
|---|---|
| Accent/noise lowers ASR quality | VAD, confidence cues, editable transcript and tested microphone guidance |
| Translation loses nuance | Preserve original text; mark low confidence; allow correction |
| Hallucinated task or owner | Constrained schema, source quote required, precision threshold and user confirmation |
| Device variation | Light/quality profiles and target-device benchmarks |
| Sensitive conversations | Local-only default, explicit export, one-tap deletion and no silent sync |
| Language coverage overclaim | Launch with measured languages; publish limits honestly |
| Model/license risk | Maintain a model inventory, license links and attribution in the repository |

BhashaBridge is an assistive productivity tool, not a legal, medical or official translation authority. The product communicates uncertainty and keeps the human in control.

## 10. Originality and ownership

This proposal and the BhashaBridge interaction prototype were created for this submission package. The participant owns the original concept and submission materials. Any third-party model, runtime or library used in implementation will be listed with its license and attribution; third-party rights are not claimed as participant-owned intellectual property.

## 11. Why BhashaBridge can win

- **Technically credible:** the architecture maps to Qualcomm AI Hub model optimization and Snapdragon heterogeneous compute.
- **Visibly differentiated:** airplane mode plus a useful multilingual action plan demonstrates on-device value immediately.
- **Humanly memorable:** the judges can see a person being included, not just a model producing text.
- **Deployable:** Windows PC packaging, model profiles, offline-first behavior and accessible controls are defined.
- **Responsible:** privacy, uncertainty, attribution and claims discipline are part of the product design.

> **Winning message:** We are not putting a chatbot on a laptop. We are giving every participant a fair chance to be heard—and giving every team a trusted next step.

## 12. Sources

- Qualcomm, “Snapdragon AI Lab,” https://www.qualcomm.com/snapdragon/ai-lab
- Qualcomm AI Hub, https://aihub.qualcomm.com/en-US
- Qualcomm AI Hub model library, https://aihub.qualcomm.com/en-US/compute/models
- Qualcomm, “Qualcomm AI Hub Expands to On-Device AI Apps for Snapdragon-Powered PCs,” 21 May 2024, https://www.qualcomm.com/news/releases/2024/05/qualcomm-ai-hub-expands-to-on-device-ai-apps-for-snapdragon-powe
- Challenge brief supplied by the participant, including eligibility, submission and evaluation criteria.
