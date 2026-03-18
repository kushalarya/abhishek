🔥 Fix: Make It Energetic (Not Pop)
✅ Principle 1 — Reduce Saturation (CRITICAL)

Instead of neon colors → use slightly muted / deeper tones

❌ Current (too pop)
#00C2FF
#FFD60A
#FF3B30
✅ Improved (athlete tone)
Swim → #3AA6D0   /* deeper water blue */
Bike → #C9A227   /* warm gold */
Run  → #D94A3A   /* burnt red */

👉 Same meaning, but:

more serious

more endurance athlete

less “gaming UI”

✅ Principle 2 — Don’t Use All 3 Together Everywhere

This is HUGE.

👉 Only show all 3 colors in special moments

Example:

Use all 3 ONLY for:

hero headline

divider gradient

logo identity

linear-gradient(90deg, #3AA6D0, #C9A227, #D94A3A);
Everywhere else:

Use ONE color at a time

👉 This creates focus + power

✅ Principle 3 — Use Dominant + Accent (60-30-10 Rule)

Use:

60% → dark base (#000025)

30% → ONE main color (blue OR yellow OR red)

10% → accent highlight

Example page sections:
🏊 Swim section
background: #000025;
accent: #3AA6D0;
🚴 Bike section
accent: #C9A227;
🏃 Run section
accent: #D94A3A;

👉 Now it feels like:

progression, not chaos

✅ Principle 4 — Use Neutrals to Calm It Down

Very important:

Neutrals make strong colors feel intentional

Add:

--surface: #0A0B2E;
--card: #12133A;
--border: #1E204A;

👉 This creates:

depth

breathing space

premium feel

🔥 Final Refined Palette (Your Version)
/* Base */
--palette-primary: #000025;
--palette-surface: #0A0B2E;

/* Swim (primary brand color) */
--palette-swim: #3AA6D0;

/* Bike (secondary accent) */
--palette-bike: #C9A227;

/* Run (intensity accent) */
--palette-run: #D94A3A;

/* Text */
--palette-text: #E6E8F2;
--palette-muted: #8A8FB2;
⚡ Advanced Trick (This Will Change Everything)
Use “activated color” instead of constant color

Instead of:

SWIM BIKE RUN (all colored always ❌)

Do:

SWIM BIKE RUN (default muted)
        ↑
   only one lights up
Example:
.swim, .bike, .run {
  color: #8A8FB2; /* muted */
}

.swim.active {
  color: #3AA6D0;
}

👉 Now it feels like:

focus, motion, progression