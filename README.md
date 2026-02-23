# TokeUI Theme for Filament

![TokeUI – Filament Theme](screenshots/cover.png)

A professional Filament theme with a blue sidebar and topbar, plus a rich set of stat card styles. Compatible with Filament 4 and 5. Full light and dark mode support.

---

## Table of contents

- [Features](#features)
- [Requirements](#requirements)
- [How to get the theme](#how-to-get-the-theme)
- [Installation](#installation)
- [Stat Overview — extraAttributes and classes](#stat-overview--extraattributes-and-classes)
- [Screenshots / Appearance](#screenshots--appearance)
- [License](#license)

---

## Features

- **Professional blue sidebar and topbar** — Same look in light and dark mode.
- **Stat card variants** — Colored, pro, bar, and pro plain; use via `extraAttributes` on Stats Overview widgets.
- **Full light and dark mode support** — Consistent styling across themes.
- **Single theme file** — Copy into your project and wire with Vite + panel provider; no Composer package required after purchase.

## Requirements

- PHP 8.2+
- Filament 4 or 5
- Laravel (version compatible with your Filament version)

## How to get the theme

1. **[Purchase TokeUI Theme](https://tokeui.mychariow.shop/prd_j1pzus)** — Complete payment on the product page.
2. **Check your email** — You will receive a **zip file** containing:
   - `theme.css` — The theme file.
   - `README.md` — Short installation guide (same steps as below).
3. **Extract and install** — Follow the [Installation](#installation) steps.

## Installation

After you have the zip and extracted `theme.css`:

### 1. Copy the theme file

Place **theme.css** in your Laravel project at:

```
resources/css/tokeui/theme.css
```

Create the `tokeui` folder under `resources/css/` if it does not exist.

### 2. Configure Vite

Open **vite.config.js** and make two changes:

**a) Add the alias** — The theme imports Filament’s base CSS. Add to `resolve.alias` (and `import path from 'path'` at the top if needed):

```js
import path from 'path';

export default defineConfig({
    resolve: {
        alias: {
            'filament-base-theme': path.resolve(__dirname, 'vendor/filament/filament/resources/css/theme.css'),
        },
    },
    // ...
});
```

**b) Add the theme to the build** — In the Laravel Vite plugin `input` array, add:

```js
input: [
    'resources/css/app.css',
    'resources/js/app.js',
    'resources/css/tokeui/theme.css',
],
```

### 3. Register the theme on your panel

In your panel provider (e.g. `app/Providers/Filament/AdminPanelProvider.php`), add:

```php
->viteTheme('resources/css/tokeui/theme.css')
```

Remove any existing `->viteTheme(...)` or plugin that registered another theme.

### 4. Build

```bash
npm run build
```

Use `npm run dev` during development. You’re all set.

---

## Stat Overview — extraAttributes and classes

Filament **Stats Overview** widgets support HTML attributes on each stat card via `->extraAttributes(['class' => '...'])`. TokeUI Theme provides predefined classes so you can style cards by type (e.g. success, warning, or a solid “pro” look).

### Usage

On each `Stat` in your widget, pass one class per card:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

Stat::make('Revenue', '$12.5k')
    ->description('This month')
    ->extraAttributes(['class' => 'stat-card-emerald']);
```

Use a single class per card (e.g. `stat-card-rose`, `stat-card-blue-pro`, or `stat-card-blue-pro-plain`).

### Available classes

#### Colored variants (gradient value, colored label)

| Class | Appearance |
|-------|------------|
| `stat-card-violet` | Pastel violet background, violet bar and value |
| `stat-card-emerald` | Green (success) |
| `stat-card-rose` | Rose / danger |
| `stat-card-amber` | Amber / warning |
| `stat-card-sky` | Sky blue / info |
| `stat-card-fuchsia` | Fuchsia |
| `stat-card-teal` | Teal |
| `stat-card-orange` | Orange |
| `stat-card-indigo` | Indigo |
| `stat-card-slate` | Neutral grey/slate |

#### “Pro” variants (pastel background, neutral value/label, accent on bar and description)

| Class | Appearance |
|-------|------------|
| `stat-card-blue-pro` | Pastel blue, neutral text, blue accent |
| `stat-card-green-pro` | Pastel green |
| `stat-card-rose-pro` | Pastel rose |
| `stat-card-amber-pro` | Pastel amber |
| `stat-card-violet-pro` | Pastel violet |
| `stat-card-sky-pro` | Pastel sky blue |

#### “Bar” variants (accent bar at bottom, white text in bar)

| Class | Appearance |
|-------|------------|
| `stat-card-bar-orange` | Orange value, orange bottom bar, white text in bar |
| `stat-card-bar-rose` | Rose |
| `stat-card-bar-emerald` | Emerald |
| `stat-card-bar-blue` | Blue |

#### “Pro plain” variants (solid background, all text white)

| Class | Appearance |
|-------|------------|
| `stat-card-blue-pro-plain` | Solid blue background, value/label/description in white |
| `stat-card-green-pro-plain` | Solid green |
| `stat-card-rose-pro-plain` | Solid rose |
| `stat-card-amber-pro-plain` | Solid amber |
| `stat-card-violet-pro-plain` | Solid violet |

---

## Screenshots / Appearance

The theme is shown below in both **light** and **dark** mode. Screenshots are in the `screenshots/` directory.

### 1 — Shop Dashboard

| Light | Dark |
|-------|------|
| ![Shop Dashboard (light)](screenshots/s1-l.png) | ![Shop Dashboard (dark)](screenshots/s1-d.png) |

### 2 — HR Dashboard

| Light | Dark |
|-------|------|
| ![HR Dashboard (light)](screenshots/s2-l.png) | ![HR Dashboard (dark)](screenshots/s2-d.png) |

### 3 — Stat UI View (stat card showcase)

| Light | Dark |
|-------|------|
| ![Stat UI View (light)](screenshots/s3-l.png) | ![Stat UI View (dark)](screenshots/s3-d.png) |

### 4 — Stat cards grid (all theme classes)

| Light | Dark |
|-------|------|
| ![Stat cards (light)](screenshots/s4-l.png) | ![Stat cards (dark)](screenshots/s4-d.png) |

---

## License

Proprietary. Use is subject to the license provided with your purchase.
