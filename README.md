# AffectAI — Emotion-Driven Reasoning Agent (from scratch)

A minimal, extensible affective computing core that models emotions (VAD), appraises events (OCC-inspired),
lets emotions influence decisions, and learns online from text feedback. No external ML packages.

## Features
- **Emotion state** (Valence–Arousal–Dominance) with decay and persistence.
- **Personality** → baseline & sensitivity.
- **OCC-like appraisal** of events (goal-aligned vs. goal-blocking, salience).
- **Text ingestor** with online-learnable lexicon for valence/arousal.
- **Emotion policy** that biases action selection and output tone.
- **Console demo** to test end-to-end.

## Quick Start
```bash
# 1) Create solution structure
# (Already included in this zip — just open the folder)
# 2) Build & run
dotnet build
dotnet run --project src/AffectAI.ConsoleDemo
```

## Using It In Your App (high level)
1. Construct `Personality` → get baseline → create `EmotionState`.
2. For each input (text/event):
   - Appraise with `OCCAppraiser` → delta.
   - Analyze text with `TextIngestor` → delta.
   - Combine deltas, `ApplyDelta`, then `TickDecay` between turns.
3. Derive policy via `EmotionPolicy` and use it to pick actions or set UI tone.
4. Collect **feedback** and call `TextIngestor.LearnFromFeedback("term", new EmotionVector(v,a,0))` to adapt.
5. Persist with `StateStore.Save/Load`.

## Extending
- Add **Dominance** modulation from text (e.g., using modality cues: "must", "cannot").
- Swap `SimpleReasoner` with RL policy that uses `EmotionState.Current` as part of the state vector.
- Add multimodal channels (prosody, vision) by converting features to VAD deltas.
- Implement **mood vs. emotion**: mood = slow-moving baseline drift; keep emotions fast.

## License
MIT
