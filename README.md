# health-diet — handover for new chats

**New chat? Read this whole file first, then pick up where `log/` leaves off.**

## Who
Miles, 23, ~91 kg, experienced lifter returning after a layoff (not a novice). Goal: maintenance at ~3,200 kcal until Thanksgiving, then a planned cut starting **Mon Nov 30** (Block 1 to about Jan 10) to lean out the midsection while keeping strength. Budget-conscious. Timezone America/New_York.

## Daily targets (judge by the weekly average, not single days)
| | Target |
|---|---|
| Calories | **Now (to Nov 29): ~3,200 kcal maintenance** (morning weight held ~194 for a week at ~3,150–3,250 actual intake). **Cut Block 1 (Nov 30 → ~Jan 10):** weeks 1–2 at **~3,000**; weeks 3–6 drop to **~2,850** only if the weekly average is not falling ~0.5 lb/week. Christmas and his birthday are maintenance days. Then a maintenance week mid-January and reassess with photos before any Block 2. **Pause rules:** main lifts drop two sessions in a row, loss faster than 1 lb/week, or sleep/mood/relationship with food gets noticeably worse → back to maintenance. Floor ~2,800. The old 192 lb stop rule is retired. |
| Protein | **190–200 g** during the cut |
| Fiber | ~30 g |
| Sodium | aim ~2,300–3,000 mg on most days; not a hard daily cliff. Avoid stacking salty takeout (one restaurant meal a day max, not several days in a row). Keep logging it. |

Preference: trim the love handles without getting smaller. Keep the cut small and short, keep meals big, never suggest a larger deficit. Get calories from clean, whole foods (milk, oil, oats, rice, potatoes, eggs, yogurt, avocado). Fast food, candy and sweets are not a calorie strategy; an occasional soda or treat is fine but never the plan.

**Calorie rule (his):** every day lands **on the target or slightly over, never under.** Plan the day so the last item closes the gap.

Day shape that works: high-volume meals during the day (3 meals of ~700–800 kcal); near bed, **low-volume, calorie-dense** food only (a ~250–400 kcal snack that closes the day: milk, Greek yogurt + seeds/granola, Ryse + milk, plain almonds, granola + milk, occasional Oreos + milk). Easy calorie adds: whole milk, yogurt bowl, olive oil, rice, extra oats, avocado.

## Hard rules
- **Allergies:** bananas and peanuts; among tree nuts his concern is **pistachio and cashew**. **Almonds are fine** (eaten without reaction, incl. Nov 18). Check labels for peanut/pistachio/cashew and 'may contain' warnings; avoid mixed-nut products. Avoid Chick-fil-A and Five Guys (peanut oil).
- **Gut:** history of a hospital visit for constipation. Chia/seeds are always either **cooked into oatmeal** or **ground dry** in the small blade grinder (10–15 s bursts, no liquid). Never raw, whole chia soaking in the gut.
- **Units:** grams for everything. tbsp/tsp is OK for oil/spices. **No cup measures.**
- Recipes: short and low effort. Season generously (he finds small amounts underwhelming).
- Salt reference: ⅛ tsp table salt ≈ 290 mg sodium; ¼ tsp ≈ 575 mg.

## Kitchen facts worth not relearning
- Rolled oats: **80 g oats needs ~320 g whole milk** (240 g is too dry).
- Rice: ~200–220 g cooked per plate. 250 g is too much.
- Potatoes: weigh **raw before oil** and log from the raw weight (e.g. 279 g raw → 194 g cooked). Air fryer russet cubes: ~400 °F, 18–22 min, shake halfway.
- Chicken is done at 165 °F; breaded nuggets go to 170 °F.
- Bell & Evans breaded breast nuggets: weigh frozen; label 112 g = 200 kcal / 21 g protein / 10 g carbs / 9 g fat / 360 mg Na.
- Air-fryer marinara chicken batch (477 g raw): 439 g cooked ≈ 755 kcal / 114 g protein / ~480 mg Na.

## How the system works (set up Nov 7, 2026)
- **This repo** = the handover. A new chat reads this README first.
- **Plate Log** = the daily food log (what he eats, in grams). Claude logs meals from his weights and photos.
- **Recipe Book** = recipes he has cooked, plus the **grocery list**. Claude keeps the grocery list current as the weeks go by: adds what is running low or needed for planned recipes, sizes amounts to the calorie target, and removes things he no longer buys.
- Workflow: he tells Claude what he ate or what he is out of; Claude updates the log and the list.

## Where the data lives (claude.ai artifacts, not in this repo)
- **Plate Log** (daily food log): https://claude.ai/artifact/57R5L2zWjrQuuJHoUzaobD
  - DB collection `data/users/me`, one doc per day: `day-YYYY-MM-DD`
  - Doc shape: `{date, items:[{id, meal, n, fid?, g?, q?, k, p, c, ft, fi, na, t, note?}], updated}`
  - `meal` ∈ Breakfast / Lunch / Dinner / Snack. `t` = ms epoch. k=kcal, p=protein, c=carbs, ft=fat, fi=fiber, na=sodium mg.
  - Always `get` the doc first, then write with `if_version`.
  - Common food ids: b0 chicken breast cooked, b6 whole egg, b7 white rice cooked, b26 egg whites, b44 black beans no salt, cquakerquick oats, cseedtrio365 seed trio (hemp/flax/chia), cmvg02wt09ujc Lucerne whole milk, cmvfyxdlivg7p Kirkland olive oil, csigbroc85 frozen petite broccoli, cmvfydyac94ot Simply Nature whole-milk vanilla yogurt (not Greek).
- **Recipe Book**: https://claude.ai/artifact/6GXLGi99nWFYz66e2M53dM
  - DB collection `data/users/me/recipebook/recipes`
  - Doc shape: `{title, meal, time, yield, fav, added, tags[], ingredients:[{g,item}], steps[], notes, macros:{k,p,c,ft,fi,na,per,est?}}`
  - **Grocery list** (Groceries tab, `#groceries`): collection `data/users/me/recipebook/grocery`, doc shape `{name, amt, sec, note, staple, need, got, order, added}`. `need`=on this trip, `got`=in cart, `staple`=weekly item that returns to the staples list after Done shopping. Weekly amounts sized for ~3,300 kcal/day.
  - Favorites so far: best-plate-potato-chicken-lentils, air-fryer-russet-cubes. To try: chicken-parm-cubes-pasta.

## Supplements / training notes
- Creatine daily (mixed into shake). NutraBio Super Carb intra-workout. Premier protein shakes.
- Protein powder: Ryse Loaded Protein (whey isolate + concentrate), bought Nov 9. Per scoop (36 g): 140 kcal, 25 g protein, 4 g carbs, 2.5 g fat (2 g sat), 1 g fiber, 230 mg sodium, 45 mg cholesterol. Use to fill gaps (post-gym, short days), not daily.
- Electrolytes: Nuun Sport tablets (300 mg sodium, 1 g sugar), bought Nov 9. One tablet in the Super Carb on gym days only; plain water otherwise. Not LMNT (1,000 mg sodium is too much given his blood pressure).
- OptiFiber (his own choice, not doctor-prescribed): back to DAILY as of Nov 10: 1 scoop with LUNCH (after the gym on gym days), with a full glass of water. Creatine + glutamine with breakfast; no need to wait after glutamine. He was as-needed Nov 6–10; his gut felt better and his weight was steadier on daily use. Keep it consistent so weigh-ins are comparable.
- Coffee: McDonald's iced coffee with sugar-free vanilla.

## Log
See `log/` for dated notes (what changed and why).

## Current plan (set Nov 6, updated Nov 22, 2026)
1. **Food:** ~3,200 kcal now (cut from Nov 30, see targets), protein 190–200 g, fiber ~30 g from food. Late sleeper: keep ~200 kcal for a small slow snack around midnight (Greek yogurt + seeds, or a glass of milk), not a full meal; make the last real meal protein + fiber. He trains fed (breakfast before the gym). Make lunch fuller (add whole milk or oil, or rice instead of potatoes); plates are high-volume but low in calories.
2. **Supplements:** creatine daily, with food or in the shake. Glutamine in the morning is fine to continue (harmless, but weak evidence for gut benefit). OptiFiber daily (since Nov 10). Probiotics optional; restart only if they noticeably helped before.
3. **Water:** drink more on sweaty and gym days, with some electrolytes. Aim for pale-yellow urine.
4. **Gut notes:** when the gut feels off, jot the time and what came before it (meal, coffee, time since the night meds). Look for a pattern after a week.
5. **Caffeine:** medium iced coffee instead of large. Caffeine-free soda at night.
6. **Weigh-ins are optional** (his choice; daily weighing was making him anxious). If he weighs, 2–3 mornings a week and use the average. Never push the scale.
7. **Progress check:** lifts, a weekly waist measurement, and reference photos (taken Nov 22; retake every 3–4 weeks, same spot/lighting/time). Keep the post-workout walk.
8. **Core / posture (home, 3x/week, ~15 min):** dead bug, bird dog or band Pallof press, hollow hold, kettlebell suitcase hold, weighted glute bridge, half-kneeling hip flexor stretch (daily if possible). **No planks** (he hurt his posture doing weighted planks). Equipment: adjustable kettlebell and dumbbell, bands, med balls. Gym split is planned in Gemini; he already does RDLs, reverse lunges, Bulgarian split squats.

## Cut staples (agreed Nov 22; focus on satiety)
Big, filling meals early in the day; lighter at night. Always land on the calorie number or slightly over, never under.
- **Breakfast:** chicken (or lean beef) and egg scramble. Gym days: ~510 kcal, no potatoes/cheese, eaten 1–2 h before training. Rest days: add potato cubes / a little cheese (~860). Recipe Book: `chicken-egg-scramble`.
- **Lunch / main meal:** bowl (ground meat + rice + beans + corn + Greek yogurt/Nando's) or chicken + potatoes. Batch-cook protein (2 lb ground chicken) and potatoes (oven 425°F, 30–35 min) so plates are just weigh-and-heat.
- **Rest of the day:** to be worked out; keep a ~200 kcal slow snack for midnight (Greek yogurt + seeds or milk), not a meal.
- Lean ground beef (90/10 or 93/7, drained) is back in rotation 2–3x/week.

## Food quality preference (Nov 6)
Wants clean food day to day. Do NOT fill calorie gaps with fast food, fries, burgers, fried pies or similar. Use whole-food calories instead: whole milk, yogurt oat bowls, oats, rice, potatoes, eggs, olive oil, cheese, seeds, fruit (never banana), granola without nuts. Occasional treats are fine but should not be the default snack.
