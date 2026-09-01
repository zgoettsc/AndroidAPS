# Break-Glass Runbook — CGM and Pump Fallbacks

Print this. Steps are written to be followed under stress, offline.

## 0. One-time xDrip+ install & config (do on every phone)

Install xDrip+ (official APK from github.com/NightscoutFoundation/xDrip → Releases; archive a copy
in the kit — self-signed, never expires). Then on EACH phone:

1. Open xDrip+; skip the first-run wizard (answer **No** to the offers).
2. Settings → **Hardware Data Source → Dexcom G7 / ONE / ONE+**.
3. Settings → **Inter-app settings → Broadcast locally: ON** (Accept Glucose: OFF).
4. Phone Settings → Apps → xDrip+ → Battery → **Unrestricted**; add to **Never sleeping apps**.
5. In AAPS on that phone → Config Builder → **BG Source → xDrip+** (leave BYODA primary if used).

Steps 1–5 are inert plumbing — they do not touch the sensor, so they are safe on all phones.
**Pair the live G7 (Start sensor) on only ONE phone at a time** — the G7 will not feed multiple
phones at once, and pairing a spare can interrupt the phone/app currently reading the sensor.
The end-to-end reading test (BG shows in xDrip+, then in AAPS within ~5 min) can only be done on
the phone that actually holds the sensor.

## A. BYODA fails → switch CGM to xDrip+

Why xDrip+ exists in this kit: xDrip+ can pair and **start a fresh Dexcom G7 session with no
Dexcom account and no internet**. BYODA is the primary collector; xDrip+ is the break-glass
backup and stays idle otherwise.

1. Open **xDrip+** → Settings → Hardware Data Source → **G7 / ONE+**.
2. Settings → Inter-app settings → **Broadcast Data: ON**, Accept Glucose: OFF.
3. If starting a fresh sensor: insert sensor, then xDrip+ will find and pair it (serial shown on
   the applicator). Wait for first reading (up to ~10 min after warmup).
4. In **AAPS** → Config Builder → BG Source → select **xDrip+** (untick BYODA).
5. Confirm a BG value appears on the AAPS home screen within 5–10 minutes.
6. Loop continues automatically once BG flows.

To return to BYODA later: Config Builder → BG Source → BYODA.

**Tested on:** ___________ (date) — retest at every battery top-up that falls on a sensor change.

## B. DASH pods exhausted → Omnipod Eros

Needs: Eros pods + a charged **RileyLink or OrangeLink**.

1. Charge and power on the link device.
2. AAPS → Config Builder → Pump → **Omnipod Eros**.
3. Eros settings → RileyLink selection → pair the link over Bluetooth.
4. Activate an Eros pod (same activation flow as DASH, but radio goes through the link).
5. Confirm green loop.

## C. Pods exhausted → Medtronic (AAA batteries — the long-haul option)

**PENDING VERIFICATION:** record each owned pump's model + firmware here. Loopable models only:
512/712, 515/715, 522/722, 523/723 (fw ≤ 2.4A), 554/754 Veo (fw ≤ 2.6A US / ≤ 2.7A EU-CA).

- Owned pump 1: model ______ firmware ______ loopable? ___
- Owned pump 2: model ______ firmware ______ loopable? ___

1. Pump: set clock, basal profile from the printed settings card, max basal/bolus limits.
2. AAPS → Config Builder → Pump → **Medtronic**; enter pump serial; pair RileyLink as in B.
3. Confirm history read + green loop.

## D. Everything electronic fails → MDI (Layer 0)

Use the printed settings card: total daily dose, basal schedule, ISF, carb ratios, targets,
correction math. Long-acting pen covers basal; rapid pen covers meals/corrections. This card is
the floor — keep it current: reprint whenever the profile changes.
