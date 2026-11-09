# health-diet — handover for new chats

**New chat? Read this whole file first, then pick up where `log/` leaves off.**

## Who
Miles, 23, ~91 kg, lifts (recomp leaning toward a lean bulk). Budget-conscious. Timezone America/New_York.

## Daily targets (judge by the weekly average, not single days)
| | Target |
|---|---|
| Calories | **~3,300 kcal** (set Nov 9: morning weights 196 → 200 → ~193.8 suggest maintenance is higher than thought; goal is a slow gain). Weigh each morning; aim for the weekly average to rise ~0.5–1 lb/week. Extra calories go to carbs/fat, not protein. |
| Protein | **180–200 g** (raised Nov 6 at his request) |
| Fiber | ~30 g |
| Sodium | under 2,300 mg (usually the limit that bites first, especially on fast-food days) |

Preference: goal is a lean bulk or lean maintain. Get extra calories from clean, whole foods (milk, oil, oats, rice, potatoes, eggs, yogurt, avocado). Fast food, candy and sweets are not a calorie strategy; an occasional soda or treat is fine but never the plan.

Day shape that works: 3 meals of ~700–800 kcal plus one planned ~400–500 kcal snack. Easy calorie adds: whole milk, yogurt bowl, olive oil, rice, extra oats, avocado.

## Hard rules
- **Allergies:** bananas, peanuts, tree nuts. Never suggest them.
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
- Electrolytes: Nuun Sport tablets (300 mg sodium, 1 g sugar), bought Nov 9. One tablet in the Super Carb on gym days only; plain water otherwise. Not LMNT (1,000 mg sodium is too much given his blood pressure).
- OptiFiber (his own choice, not doctor-prescribed): as of Nov 6 only as needed, on low-fiber days (under ~25 g from food) or if bowel movements slow or harden. Not daily.
- Coffee: McDonald's iced coffee with sugar-free vanilla.

## Log
See `log/` for dated notes (what changed and why).

## Current plan (set Nov 6, 2026)
1. **Food:** ~3,300 kcal, protein 180–200 g, fiber ~30 g from food, sodium under 2,300 mg. Make lunch fuller (add whole milk or oil, or rice instead of potatoes); plates are high-volume but low in calories.
2. **Supplements:** creatine daily, with food or in the shake. Glutamine in the morning is fine to continue (harmless, but weak evidence for gut benefit). OptiFiber only as needed. Probiotics optional; restart only if they noticeably helped before.
3. **Water:** drink more on sweaty and gym days, with some electrolytes. Aim for pale-yellow urine.
4. **Gut notes:** when the gut feels off, jot the time and what came before it (meal, coffee, time since the night meds). Look for a pattern after a week.
5. **Caffeine:** medium iced coffee instead of large. Caffeine-free soda at night.
6. **Weigh every morning;** check the weekly average each Sunday. Adjust calories by 150–200 if needed.

## Food quality preference (Nov 6)
Wants a lean bulk / lean maintain. Do NOT fill calorie gaps with fast food, fries, burgers, fried pies or similar. Use whole-food calories instead: whole milk, yogurt oat bowls, oats, rice, potatoes, eggs, olive oil, cheese, seeds, fruit (never banana), granola without nuts. Occasional treats are fine but should not be the default snack.
