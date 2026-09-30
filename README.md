# BhashaBridge submission package

BhashaBridge is a concept and demo package for the Snapdragon AI Lab Build & Present Challenge 2026.

## Files

- `index.html` — interactive, responsive product demo.
- `PROPOSAL.md` — submission-ready concept, technical plan and judging case.
- `PITCH.md` — 2-minute presentation script, demo checklist and judge Q&A.

## Run the demo

No build step or internet connection is required:

```bash
cd /home/ubuntu/snapdragon_ai_lab_submission
python3 -m http.server 8000
```

Then open `http://localhost:8000` in a browser. You can also double-click `index.html`.

## Honest prototype boundary

The current demo is a polished interaction prototype: it illustrates the user experience and the local-inference states, but it does not claim to perform live speech recognition in the browser. The proposal contains the model integration plan. For a final technical submission, connect the UI to a Windows-native local inference service using a Qualcomm AI Hub / GenieX-compatible ASR model, translation model and Qwen3 4B model, then record measured latency, accuracy and power results.

## Recommended final build sequence

1. Validate the target Snapdragon HP PC and Windows runtime.
2. Benchmark a Qualcomm AI Hub-compatible Whisper-family model for Hindi, English and one additional Indian language.
3. Add local translation and Qwen3 4B structured action extraction.
4. Implement confidence cues and source-quote traceability.
5. Package as a Windows desktop application.
6. Run the offline demo and capture measured results for the final presentation.

## Submission hygiene

- Replace any placeholder claims with measured results.
- Credit every model and library used, including license links.
- Confirm the participant owns the proposal and has permission to submit it.
- Submit only one final version, after checking every intake-form field.
