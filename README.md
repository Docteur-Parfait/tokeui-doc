# TokeUI Theme for Filament

![TokeUI – Filament Theme](screenshots/cover.png)

A professional Filament theme: blue sidebar and topbar, rich stat card styles, full light and dark mode. Compatible with Filament 4 and 5.

---

## Table of contents

- [Features](#features)
- [Requirements](#requirements)
- [How to get the theme](#how-to-get-the-theme)
- [Installation](#installation)
- [Stat Overview — extraAttributes and classes](#stat-overview--extraattributes-and-classes)
- [Notifications and polish](#notifications-and-polish)
- [License](#license)

---

## Features

- **Blue sidebar and topbar** — Same look in light and dark mode.
- **Stat card variants** — Colored, pro, bar, and pro plain via `extraAttributes` on Stats Overview widgets.
- **Light and dark mode** — Consistent styling in both themes.
- **Composer install** — Purchase on AnyStack → license key → install package and register the plugin on your panel.

**Requirements:** PHP 8.2+, Filament 4 or 5, Laravel compatible with your Filament version.

| Light                                           | Dark                                           |
| ----------------------------------------------- | ---------------------------------------------- |
| ![Shop Dashboard (light)](screenshots/s1-l.png) | ![Shop Dashboard (dark)](screenshots/s1-d.png) |

---

## How to get the theme

1. **[Purchase TokeUI Theme](https://checkout.anystack.sh/tokeui-theme?via=arf178)** — Complete payment on AnyStack.
2. **License key** — After purchase, use your account email and the provided license key as Composer credentials.
3. **Install** — Follow the [Installation](#installation) steps below.

---

## Installation

### 1. Add the Composer repository

In `composer.json`, add the AnyStack repository URL from your [AnyStack product page](https://anystack.sh) (e.g. `https://....composer.sh`) to the `repositories` section:

```json
{
  "repositories": [
    {
      "type": "composer",
      "url": "https://tokeui-filament-theme.composer.sh"
    }
  ]
}
```

### 2. Install the package

```bash
composer require tokeui/filament-tokeui-theme
```

When prompted, use your **account email** and **AnyStack license key** as Composer credentials.

### 3. Configure Vite

In **vite.config.js**:

**a) Alias** — The theme imports Filament’s base CSS. Add to `resolve.alias` (and `import path from 'path'` at the top if needed):

```js
import path from "path";

export default defineConfig({
  resolve: {
    alias: {
      "filament-base-theme": path.resolve(
        __dirname,
        "vendor/filament/filament/resources/css/theme.css",
      ),
    },
  },
  // ...
});
```

**b) Theme in build** — Add the theme CSS to the Laravel Vite plugin `input` array:

```js
input: [
    'resources/css/app.css',
    'resources/js/app.js',
    'vendor/tokeui/filament-tokeui-theme/resources/css/theme.css',
],
```

### 4. Register the plugin on your panel

In your panel provider (e.g. `app/Providers/Filament/AdminPanelProvider.php`), register the TokeUI plugin and remove any existing `->viteTheme(...)` or other theme:

```php
use TokeUI\FilamentTokeUITheme\FilamentTokeUIThemePlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->plugin(FilamentTokeUIThemePlugin::make());
}
```

The plugin registers the theme via `vendor/tokeui/filament-tokeui-theme/resources/css/theme.css`.

### 5. Build

```bash
npm run build
```

Use `npm run dev` during development. You’re all set.

| Light                                         | Dark                                         |
| --------------------------------------------- | -------------------------------------------- |
| ![HR Dashboard (light)](screenshots/s2-l.png) | ![HR Dashboard (dark)](screenshots/s2-d.png) |

---

## Stat Overview — extraAttributes and classes

Filament **Stats Overview** widgets accept HTML attributes on each stat card via `->extraAttributes(['class' => '...'])`. TokeUI Theme provides predefined classes to style each card (e.g. success, warning, or a solid “pro” look).

**Usage:** one class per card on each `Stat`:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

Stat::make('Revenue', '$12.5k')
    ->description('This month')
    ->extraAttributes(['class' => 'stat-card-emerald']);
```

Examples: `stat-card-rose`, `stat-card-blue-pro`, `stat-card-blue-pro-plain`.

### Colored variants (gradient value, colored label)

| Class               | Appearance                                     |
| ------------------- | ---------------------------------------------- |
| `stat-card-violet`  | Pastel violet background, violet bar and value |
| `stat-card-emerald` | Green (success)                                |
| `stat-card-rose`    | Rose / danger                                  |
| `stat-card-amber`   | Amber / warning                                |
| `stat-card-sky`     | Sky blue / info                                |
| `stat-card-fuchsia` | Fuchsia                                        |
| `stat-card-teal`    | Teal                                           |
| `stat-card-orange`  | Orange                                         |
| `stat-card-indigo`  | Indigo                                         |
| `stat-card-slate`   | Neutral grey/slate                             |

### “Pro” variants (pastel background, neutral value/label, accent on bar and description)

| Class                  | Appearance                             |
| ---------------------- | -------------------------------------- |
| `stat-card-blue-pro`   | Pastel blue, neutral text, blue accent |
| `stat-card-green-pro`  | Pastel green                           |
| `stat-card-rose-pro`   | Pastel rose                            |
| `stat-card-amber-pro`  | Pastel amber                           |
| `stat-card-violet-pro` | Pastel violet                          |
| `stat-card-sky-pro`    | Pastel sky blue                        |

### “Bar” variants (accent bar at bottom, white text in bar)

| Class                   | Appearance                                         |
| ----------------------- | -------------------------------------------------- |
| `stat-card-bar-orange`  | Orange value, orange bottom bar, white text in bar |
| `stat-card-bar-rose`    | Rose                                               |
| `stat-card-bar-emerald` | Emerald                                            |
| `stat-card-bar-blue`    | Blue                                               |

### “Pro plain” variants (solid background, all text white)

| Class                        | Appearance                                              |
| ---------------------------- | ------------------------------------------------------- |
| `stat-card-blue-pro-plain`   | Solid blue background, value/label/description in white |
| `stat-card-green-pro-plain`  | Solid green                                             |
| `stat-card-rose-pro-plain`   | Solid rose                                              |
| `stat-card-amber-pro-plain`  | Solid amber                                             |
| `stat-card-violet-pro-plain` | Solid violet                                            |

| Light                                         | Dark                                         |
| --------------------------------------------- | -------------------------------------------- |
| ![Stat UI View (light)](screenshots/s3-l.png) | ![Stat UI View (dark)](screenshots/s3-d.png) |

| Light                                       | Dark                                       |
| ------------------------------------------- | ------------------------------------------ |
| ![Stat cards (light)](screenshots/s4-l.png) | ![Stat cards (dark)](screenshots/s4-d.png) |

---

## Notifications and polish

The theme styles notifications and the rest of the UI for a consistent look.

| Light                                                         | Dark                                                         |
| ------------------------------------------------------------- | ------------------------------------------------------------ |
| ![Notifications and stat cards (light)](screenshots/s5-l.png) | ![Notifications and stat cards (dark)](screenshots/s5-d.png) |

---

## License

Proprietary. Use is subject to the license provided with your purchase.
