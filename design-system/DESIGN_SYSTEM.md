# TBC დიზაინ სისტემა — პროექტის მთავარი გაიდლაინი

ეს დოკუმენტი არის ამ პროექტის **ერთადერთი წყარო დიზაინის საკითხებში** (source of truth). ყველა ახალი UI, კომპონენტი და გვერდი უნდა შეიქმნას აქ აღწერილი ტოკენების (ფერები, ტიპოგრაფია, spacing, radius და ა.შ.) გამოყენებით — არა ხელით შერჩეული hex კოდებით ან ზომებით.

წყარო Figma ფაილები:

| ბიბლიოთეკა | Figma ფაილი |
|---|---|
| Foundation library | `Foundation library — v1.0.9` (`LpJB5rw5bB1J4SHwOb103G`) |
| Light თემა | `TBC light theme — v1.7.6` (`NTOW2uJfNLIbkbPWLVa2lc`) |
| Dark თემა | `TBC dark theme — v1.7.6` (`E9KO7KaKVHhkZC5q138LMi`) |

მანქანურად წასაკითხი ტოკენები ინახება `design-system/tokens/`-ში (`colors.light.json`, `colors.dark.json`, `typography.json`, `spacing.json`, `radius.json`, `opacity.json`, `motion.json`, `shadows.json`) და აგრეგირებულია `tokens.css`-ში — CSS custom properties, რომელიც ავტომატურად ერგება ლაითს/დარქს.

---

## 1. თემირება (Light / Dark)

ყველა სემანტიკური ტოკენი (`color/text/*`, `color/surface/*`, `color/icon/*`, `color/stroke/*`, `color/overlay/*`, `color/illustration/*`) არსებობს ორივე რეჟიმისთვის, **იდენტური სახელით** — მხოლოდ მნიშვნელობა იცვლება თემის მიხედვით. ამიტომ კომპონენტში არასდროს არ იწერება პირდაპირი hex, არამედ ყოველთვის სემანტიკური ტოკენი (მაგ. `color/surface/high/initial`), რომელიც თავად გადაირთვება თემასთან ერთად.

`tokens.css`-ში:

```css
:root {
  --color-surface-high-initial: #FFFFFF; /* light — default */
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { --color-surface-high-initial: #2A3032; }
}
[data-theme="dark"] { --color-surface-high-initial: #2A3032; }
```

ანუ თემა იმართება `<html data-theme="light|dark">`-ით, ან თუ ატრიბუტი არ არის დაყენებული — სისტემურ (`prefers-color-scheme`) პარამეტრზე გადადის ავტომატურად.

---

## 2. ტიპოგრაფია

**ფონტი: `TBC X`** (ქართული/ლათინური/კირილიცა მხარდაჭერით). Letter-spacing ყველგან `0`-ია.

> ⚠️ `TBC X` ფონტის ფაილები (woff2 და ა.შ.) Figma-დან ავტომატურად არ მოდის — ისინი ცალკე უნდა მოგვაწოდოთ ბრენდინგის/დიზაინის გუნდისგან, რომ პროექტში `@font-face`-ით ჩავრთოთ.

ტექსტის სტილების სრული სკალა (`design-system/tokens/typography.json`):

| ჯგუფი | სტილი | წონა | ზომა | line-height |
|---|---|---|---|---|
| Display | `display/xl` | Bold (700) | 56 | 1.5 |
| Display | `display/l` | Bold (700) | 44 | 1.5 |
| Headline | `headline/xl/bold` \| `/medium` | Bold / Medium | 36 | 1.5 |
| Headline | `headline/l/bold` \| `/medium` | Bold / Medium | 32 | 1.5 |
| Headline | `headline/m/bold` \| `/medium` | Bold / Medium | 28 | 1.5 |
| Headline | `headline/s/bold` \| `/medium` | Bold / Medium | 24 | 1.5 |
| Title | `title/xl/bold` \| `/medium` \| `/regular` | 700/500/400 | 28 | 1.5 |
| Title | `title/l/bold` \| `/medium` \| `/regular` | 700/500/400 | 24 | 1.5 |
| Title | `title/m/bold` \| `/medium` \| `/regular` | 700/500/400 | 20 | 1.5 |
| Title | `title/s/bold` \| `/medium` \| `/regular` | 700/500/400 | 16 | 1.7 |
| Title | `title/xs/bold` \| `/medium` \| `/regular` | 700/500/400 | 14 | 1.7 |
| Body | `body/l/bold` \| `/medium` \| `/regular` \| `/link` | 700/500/400/400 | 20 | 1.7 |
| Body | `body/m/bold` \| `/medium` \| `/regular` \| `/link` | 700/500/400/400 | 16 | 1.7 |
| Body | `body/s/bold` \| `/medium` \| `/regular` \| `/link` | 700/500/400/400 | 14 | 1.7 |
| Body | `body/xs/bold` \| `/medium` \| `/regular` \| `/link` | 700/500/400/400 | 12 | 1.7 |
| Label | `label/l/medium` \| `/regular` | 500/400 | 16 | 1.5 |
| Label | `label/m/medium` \| `/regular` | 500/400 | 14 | 1.5 |
| Label | `label/s/medium` \| `/regular` | 500/400 | 12 | 1.5 |
| Button | `button/xl` | Bold | 16 | 24px (ფიქსირებული) |
| Button | `button/l` | Bold | 14 | 20px (ფიქსირებული) |
| Button | `button/m` | Bold | 12 | 16px (ფიქსირებული) |
| Button | `button/s` | Bold | 10 | 14px (ფიქსირებული) |

`link` ვარიანტები ვიზუალურად identical არიან შესაბამის `regular`-თან, თუმცა ცალკე ტოკენად არსებობს, რადგან ჩვეულებრივ `color/text/link/*`-თან წყვილდება.

---

## 3. ფერები

ყველა ფერადი ტოკენი აწყობილია სქემით `color/{კატეგორია}/{როლი}/{მდგომარეობა}`. ქვემოთ — ორივე თემის სრული მნიშვნელობები (გამოტანილია `design-system/tokens/colors.light.json` / `colors.dark.json`-დან).

### 3.1 Text

| ტოკენი | Light | Dark |
|---|---|---|
| `text/strong/default` | `#141719` | `#F9FAFA` |
| `text/strong/inverted` | `#FFFFFF` | `#141719` |
| `text/soft/default` | `#555F62` | `#A5AAAC` |
| `text/softer/default` | `#6F787B` | `#899194` |
| `text/disabled/default` | `#A5AAAC` | `#555F62` |
| `text/primary/initial \| hovered \| pressed` | `#00ADEE` / `#0094CC` / `#0077A5` | იგივე |
| `text/secondary/initial \| hovered \| pressed` | `#5236E4` / `#3D23BC` / `#2C1B84` | `#A49DF5` / `#8679F9` / `#6853F7` |
| `text/link/initial \| hovered \| pressed` | `#00ADEE` / `#0094CC` / `#0077A5` | იგივე |
| `text/positive/initial \| hovered \| pressed` | `#008043` / `#006737` / `#004F2B` | `#1ABE6A` / `#0A9E56` / `#008043` |
| `text/negative/initial \| hovered \| pressed` | `#E5002F` / `#B60023` / `#8D001C` | `#F78583` / `#F94850` / `#E5002F` |
| `text/info/initial \| hovered \| pressed` | `#00ADEE` / `#0094CC` / `#0077A5` | იგივე |
| `text/warning/initial \| hovered \| pressed` | `#876C00` / `#6E5700` / `#554200` | `#E6C230` / `#C5A316` / `#A68700` |

(`inverted`/`dark`/`light` ვარიანტები — იხ. `colors.*.json`, გამოიყენება inverted/on-color surfaces-ზე ტექსტისთვის.)

### 3.2 Icon

Icon-ტოკენები **ზუსტად იმეორებს** შესაბამის `text/*` ტოკენებს (იგივე hex, ცალკე namespace სემანტიკისთვის) — `icon/strong/default`, `icon/soft/default`, `icon/primary/*`, `icon/secondary/*`, `icon/positive/*`, `icon/negative/*`, `icon/info/*`, `icon/warning/*` და ა.შ. იხ. ცხრილი 3.1-ში იგივე მნიშვნელობებით.

> Dark თემის icon-ტოკენების ნაწილი (`icon/soft`, `icon/softer`, `icon/disabled`, `icon/secondary` და სხვ.) გამოყვანილია ამ 1:1 შესაბამისობის პრინციპიდან — Light თემაში ეს დადასტურებულია ყველა მნიშვნელობაზე; Dark-ში პირდაპირ დადასტურებულია მხოლოდ `icon/strong/default = #F9FAFA`. თუ საჭიროა 100%-იანი სიზუსტე, შემიძლია დამატებით გადავამოწმო Figma-ს "Icon colors" გვერდი Dark ფაილში.

### 3.3 Surface

| ტოკენი | Light | Dark |
|---|---|---|
| `surface/canvas/initial` | `#F9FAFA` | `#23282A` |
| `surface/low/initial` | `#F3F5F6` | `#1A1E1F` |
| `surface/lower/initial` | `#EEF1F1` | `#171B1C` |
| `surface/high/initial` | `#FFFFFF` | `#2A3032` |
| `surface/higher/initial` | `#F6F8F8` | `#31383A` |
| `surface/highest/initial` | `#EEF1F1` | `#424A4D` |
| `surface/popover/initial` | `#FFFFFF` | `#31383A` |
| `surface/primary/initial \| hovered \| pressed` | `#00ADEE` / `#0094CC` / `#0077A5` | იგივე |
| `surface/secondary/initial \| hovered \| pressed` | `#6853F7` / `#5236E4` / `#3D23BC` | `#8679F9` / `#6853F7` / `#5236E4` |
| `surface/positive/initial \| hovered \| pressed` | `#008043` / `#006737` / `#004F2B` | `#0A9E56` / `#008043` / `#006737` |
| `surface/negative/initial \| hovered \| pressed` | `#E5002F` / `#B60023` / `#8D001C` | `#F94850` / `#E5002F` / `#B60023` |
| `surface/warning/initial \| hovered \| pressed` | `#E6C230` / `#C5A316` / `#A68700` | იგივე |
| `surface/*/disabled` | `#E9EBEC` | `#424A4D` |

ყოველ `surface/*`-ს ასევე აქვს `hovered`/`pressed` ვარიაცია და ნაწილს — `inverted-*`, `light-*`, `dark-*` ქვე-ვარიანტები ფიქსირებული (თემისგან დამოუკიდებელი) surface-ებისთვის. სრული სია — `colors.light.json` / `colors.dark.json`.

### 3.4 Stroke

| ტოკენი | Light | Dark |
|---|---|---|
| `stroke/softer/initial` | `#EEF1F1` | `#31383A` |
| `stroke/soft/initial` | `#E1E4E5` | `#424A4D` |
| `stroke/strong/initial` | `#D1D5D6` | `#6F787B` |
| `stroke/stronger/initial` | `#BCC1C2` | `#A5AAAC` |
| `stroke/primary/initial \| hovered` | `#00ADEE` / `#0094CC` | იგივე |
| `stroke/secondary/initial \| hovered` | `#6853F7` / `#5236E4` | იგივე |
| `stroke/positive/initial \| hovered` | `#008043` / `#006737` | `#0A9E56` |
| `stroke/negative/initial \| hovered` | `#E5002F` / `#B60023` | იგივე |
| `stroke/warning/initial \| hovered` | `#E6C230` / `#A68700` | იგივე |

თითოეულს ასევე აქვს `subtle/initial` და `subtle/hovered` — მსუბუქი, დაბალკონტრასტიანი ვარიანტი (მაგ. `stroke/positive/subtle/initial`: `#A9F3B9` ორივე თემაში).

### 3.5 Overlay

| ტოკენი | Light | Dark |
|---|---|---|
| `overlay/backdrop` | `#0F1215` | იგივე |
| `overlay/darken/soft \| subtle` | `#001E2D` | იგივე |
| `overlay/lighten/soft \| subtle` | `#FFFFFF` | იგივე |

(ეს ტოკენები, როგორც წესი, გამოიყენება opacity-სთან ერთად — იხ. §5 Opacity — modal/backdrop ფენებისთვის.)

### 3.6 Illustration

| ტოკენი | Light | Dark |
|---|---|---|
| `illustration/primary` \| `-subtle` | `#00ADEE` / `#CEE5FB` | `#00ADEE` / `#005F86` |
| `illustration/positive` \| `-subtle` | `#26D273` / `#DDF8DF` | `#26D273` / `#006737` |
| `illustration/negative` \| `-subtle` | `#F94850` / `#FCDBD9` | `#F94850` / `#680014` |
| `illustration/warning` \| `-subtle` | `#FAD64D` / `#FBF0D5` | `#FAD64D` / `#6E5700` |
| `illustration/neutral` \| `-inverted` | `#E9EBEC` / `#FFFFFF` | `#31383A` / `#23282A` |

### 3.7 საბაზისო (core) პალიტრა — Foundation library

Semantic ტოკენების უკან დგას raw/core პალიტრა (Foundation library, გვერდი "🎨 Color tokens"), ორგანიზებული ჯგუფებად:

- **Neutrals:** Steelgrey (21 საფეხური, `00`–`21`)
- **Brand:** Tbc, Concept, Capital, Saba, Wealth, Business, Hi (თითოეული 10 საფეხური, `10`–`100`)
- **Extended palette:** Yellow, Lime, Green, Teal, Blue, Indigo, Purple, Pink, Red (თითოეული 10 საფეხური, `10`–`100`)

ეს ბაზისური ჰექს-კოდები (მაგ. `core/color/blue/70 = #0052C1`, `core/color/business/10 = #EDF1FB`) ცალკე არ ამოვწერე ცხრილში მოცულობის გამო (200+ swatch) — თუ დაგჭირდებათ, მაგ. გრაფიკებისთვის/დიაგრამებისთვის, გეტყვით და ცალკე amoვწერ ზუსტ hex-ებს.

---

## 4. Spacing

`core.spacing.*` — 4px-ის ჯერადებზე აგებული სკალა:

```
2, 4, 8, 12, 16, 24, 32, 40, 48, 56, 64, 72, 80, 96, 120, 160, 200, 240 (px)
```

## 5. Border radius

```
core.border.radius.2  = 2px
core.border.radius.4  = 4px
core.border.radius.6  = 6px
core.border.radius.8  = 8px
core.border.radius.10 = 10px
core.border.radius.12 = 12px
core.border.radius.round = 1000px   /* სრულად მომრგვალებული (pill/circle) */
```

## 6. Opacity

```
100% = FF   90% = E6   80% = CC   70% = B3   60% = 99
50%  = 80   40% = 66   30% = 4D   20% = 33   10% = 1A
```

## 7. Shadows (elevation)

| ტოკენი | Light | Dark |
|---|---|---|
| `shadow/bottom/s` | `0 0 1px #001E2D33, 0 2px 8px -1px #001E2D08` | `0 0 1px #FFFFFF1F, 0 2px 12px -1px #14171929` |
| `shadow/bottom/m` | `0 0 1px #001E2D33, 0 12px 12px -4px #001E2D14` | `0 0 1px #FFFFFF1F, 0 12px 12px -4px #14171929` |
| `shadow/bottom/l` | `0 0 1px #001E2D33, 0 21px 21px -5px #001E2D14` | `0 0 1px #FFFFFF3D, 0 21px 21px -2px #1417193D` |
| `shadow/top/s` | `0 0 1px #001E2D33, 0 -2px 8px -1px #001E2D08` | `0 0 1px #FFFFFF1F, 0 -2px 12px -1px #14171929` |

დარქ თემაში ჩრდილი უფრო "ნათელა" ტონშია (თეთრი ბაზაზე გამჭვირვალობით), რაც ჩვეულებრივი პრაქტიკაა dark UI-ებში კონტურის წასაკვეთად.

## 8. Motion

**Duration:**

| ტოკენი | მნიშვნელობა | გამოყენება |
|---|---|---|
| `duration.70` | 70ms | მიკრო-ინტერაქციები: text field, toggle, button |
| `duration.110` | 110ms | მიკრო-ინტერაქციები |
| `duration.200` | 200ms | მცირე მანძილის მოძრაობა |
| `duration.300` | 300ms | ნოტიფიკაციები, dropdown-ები, popover-ები |
| `duration.400` | 400ms | გვერდის ტრანზიციები, დიდი ობიექტების მოძრაობა |
| `duration.500/600/800` | 500/600/800ms | დიდი, ექსპრესიული ანიმაციები |

**Easing:**

| ტოკენი | Cubic-bezier | გამოყენება |
|---|---|---|
| `easing.linear` | `[0, 0, 1, 1]` | მხოლოდ opacity/ფერის ცვლილება |
| `easing.ease-in` | `[0.4, 0, 0.1, 1]` | ობიექტი ჩანს დასაწყისში, ქრება ბოლოს |
| `easing.ease-out` | `[0.5, 0, 0.2, 1]` | ობიექტი ჩნდება/შედის ხედვაში |
| `easing.ease-in-out` | `[0.6, 0, 0.4, 1]` | ობიექტი ხედვაშია დასაწყისშიც და ბოლოშიც |

## 9. Iconography

Foundation library-ს გვერდი **"🎈 Global icons"** შეიცავს:

- TBC-ს და Concept-ის ბრენდ-ლოგოებს (Logomark, Wordmark GE/EN ვარიანტებით)
- ასობით პროდუქტ-აიქონს, დაჯგუფებულს კატეგორიებად, ყოველი ორი ვარიანტით: **`-outlined`** და **`-filled`** (მაგ. `shield-outlined` / `shield-filled`, `bulb-outlined` / `bulb-alt-filled` და ა.შ.)

აიქონები 24×24 საბაზისო grid-ზეა აგებული და იღებენ ფერს `color/icon/*` ტოკენებიდან (§3.2), ანუ ცალკე dark/light ვერსია არ სჭირდებათ — `currentColor`/token-driven fill საკმარისია.

---

## 10. რაც ჯერ არ არის ამოღებული

გამოგზავნილი Figma ბმულები ყველა **ფაუნდეიშენ/ტოკენ** გვერდებს წარმოადგენდა (ფერი, ტიპოგრაფია, spacing, radius, opacity, motion, icons). **კონკრეტული UI-კომპონენტების** (Button, Input, Card, Modal, Badge, Tabs და ა.შ.) spec/variant გვერდები ჯერ არ მისვლია — ეს ცალკე node-ბმულებით უნდა გამომიგზავნოთ (component library ფაილიდან), რომ იგივე პრინციპით ავაწყო component-level გაიდლაინი (ზომები, states, padding-ები ტოკენებზე მიბმული).

---

## 11. გამოყენების წესი კოდში

1. არასდროს ჩაწეროთ პირდაპირი hex/px მნიშვნელობა კომპონენტში — მხოლოდ `design-system/tokens/tokens.css`-ის CSS variables (`var(--color-surface-high-initial)`, `var(--core-spacing-16)` და ა.შ.).
2. თემის გადართვა ხდება `<html data-theme="light">` / `data-theme="dark"` ატრიბუტით; მისი არარსებობისას სისტემური პარამეტრი მუშაობს ავტომატურად.
3. ახალი კომპონენტის დიზაინისას პირველად შემოწმდეს, არსებობს თუ არა შესაბამისი სემანტიკური ტოკენი (`color/surface/...`, `color/text/...` და ა.შ.) — ახალი ნედლი ფერი არ დაემატება, თუ Figma-ს ტოკენებში არ არსებობს.
