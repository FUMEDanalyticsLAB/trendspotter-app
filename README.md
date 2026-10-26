# TrendSpotter

TrendSpotter is a multi-wearable behaviour-change advisor. It turns the data from the wearables you already have into one small habit at a time, in plain language, with a 14-day plan and a supportive circle. It is a wellness proof of concept: it does not diagnose, and all demo data is synthetic.

## Status

- **Live link:** LIVE_LINK_HERE. This is an interactive prototype of the full experience, designed tonight.
- **This repository** contains the Expo app scaffold and the architecture for the next build step: data validation (no number without a source), data coverage, the 14-day review, and synthetic personas. See [ARCHITECTURE.md](ARCHITECTURE.md).
- There are no unit tests yet. They come with the next build step.

## How to run

```bash
npm install
npx expo start            # dev server (press w for web)
npx expo export --platform web   # static web build in dist/
```

## Safety

TrendSpotter gives lifestyle suggestions only. No diagnoses, no medication or diet advice. If you have chest pain, fainting, or trouble breathing, seek care now.

## Team

Team GuideRail: a physician (clinical content and safety review) and an engineer (build and deployment).

## Prior work and credits

- Prior work: the Expo `create-expo-app` template only.
- Detail settings inspired by Dr. Mike Evans's wearable mindsets.
