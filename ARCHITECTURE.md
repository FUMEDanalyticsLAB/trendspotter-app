# TrendSpotter architecture (MVP)

TrendSpotter is a wellness proof of concept: an Expo app (Expo Router, TypeScript) exported to static web. There is no backend, no account and no model call at runtime. All demo data is synthetic.

## Flow

Landing (`/`) -> Onboarding (`/onboarding`) -> Tabs: Today (`/today`), Plan (`/plan`), Circle (`/circle`).

## Data types (`src/lib/types.ts`)

```ts
type Sourced<T> = { value: T; source_id: string };   // every shown number carries a source_id

type Night = {
  date: string;                       // YYYY-MM-DD
  missing: boolean;                   // true when the wearable sent nothing
  sleep_start: Sourced<string | null>; // "HH:MM", 24 h clock
  steps: Sourced<number | null>;
};

type Persona = {
  id: 'A' | 'B';
  label: string;
  synthetic: true;
  bedtime: string;                    // default chosen bedtime "HH:MM"
  history: Night[];                   // last 14 nights, used by Today cards
  plan_nights: Night[];               // next 14 nights, used by the Plan daily check
};

type Mindset = 'dismisser' | 'anxious' | 'lite' | 'devotee';  // default 'lite'
type Concern = 'sleep';               // activity and stress are "coming next"
```

## Rules in code

| Rule | Where |
|---|---|
| No number without a `source_id` | `src/lib/validator.ts` (`requireSource`, `validatePersona`) |
| Coverage line | `src/lib/coverage.ts` |
| Kept check and kept count | `src/lib/review.ts`. A night is kept when sleep start is within 30 minutes of the chosen bedtime (either side). Missing nights are not kept |
| Card facts | `src/lib/cards.ts` builds sourced facts from a persona; derived values get a derived `source_id` |
| All copy from the content table | `content/rules.json`, filled with `src/lib/text.ts` |

## Shared files (frozen after Phase 1)

`content/rules.json`, `content/personas.json`, `scripts/make_personas.ts`, `src/lib/*`, `src/theme.ts`, `src/store/settings.tsx`, `src/components/*`, `src/app/_layout.tsx`, `src/app/(tabs)/_layout.tsx`.

## File ownership

| Worker | Owns |
|---|---|
| Lead | Shared files above, `README.md`, `.github/workflows/*`, `app.json`, `package.json` |
| W1 (landing, onboarding) | `src/app/index.tsx`, `src/app/onboarding.tsx` |
| W2 (Today) | `src/app/(tabs)/today.tsx` |
| W3 (Plan, Circle) | `src/app/(tabs)/plan.tsx`, `src/app/(tabs)/circle.tsx` |

## Tests

`npm test` runs Node's built in test runner on `src/lib/*.test.ts` (Node strips TypeScript types natively). Lib files import each other with explicit `.ts` extensions so they run under both Node and Metro.
