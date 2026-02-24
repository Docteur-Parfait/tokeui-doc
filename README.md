# TokeUI Theme for Filament

A professional light and dark theme for Filament PHP.

![TokeUI – Filament Theme](screenshots/cover.png)

| Dashboard Light                                 | Dashboard Dark                                 |
| ----------------------------------------------- | ---------------------------------------------- |
| ![Shop Dashboard (light)](screenshots/s1-l.png) | ![Shop Dashboard (dark)](screenshots/s1-d.png) |

## Table of contents

- [Requirements](#requirements)
- [Features](#features)
- [Installation](#installation)
  - [Activating Your License on AnyStack](#activating-your-license-on-anystack)
  - [Installing with Composer](#installing-with-composer)
- [Stat Overview — extraAttributes and classes](#stat-overview--extraattributes-and-classes)
- [Appearance](#appearance)
  - [Shop Dashboard](#shop-dashboard)
  - [HR Dashboard](#hr-dashboard)
  - [Stat UI View](#stat-ui-view)
  - [Stat cards grid](#stat-cards-grid)
  - [Notifications and stat cards](#notifications-and-stat-cards)
- [License](#license)

## Requirements

- PHP 8.2+
- Filament 4 or 5
- Laravel (version compatible with your Filament version)

## Features

- **Professional blue sidebar and topbar** — Same look in light and dark mode.
- **Stat card variants** — Colored, pro, bar, and pro plain; use via `extraAttributes` on Stats Overview widgets.
- **Full light and dark mode support** — Consistent styling across themes.
- **Install via Composer** — After purchase on AnyStack, install the package with Composer and register the plugin on your panel.

## Installation

### Activating Your License on AnyStack

TokeUI Theme uses AnyStack to handle payment, licensing, and distribution. [You can buy it here](https://checkout.anystack.sh/tokeui-filament-theme).

During the purchasing process, AnyStack will provide you with a license key. Once your license key is activated, you can proceed with the Composer installation described below.

### Installing with Composer

Add the TokeUI Theme package to the `repositories` section of your `composer.json` file:

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

Once the repository has been added to the `composer.json` file, you can install like any other Composer package using the `composer require` command:

```bash
composer require tokeui/filament-tokeui-theme
```

Next, you will be prompted to provide your username and password.

```
Loading composer repositories with package information
Authentication required (tokeui-filament-theme.composer.sh):
Username: [license-email]
Password: [license-key]
```

Your username will be your email address and the password will be your license key. For example, let's say we have the following email and license activation:

```
Contact email: your@email.com
License key: 04c21df8f-4890-7024-y2vk-6bny143ta642
```

You will need to enter the above information as follows when prompted for your credentials:

```
Loading composer repositories with package information
Authentication required (tokeui-filament-theme.composer.sh):
Username: your@email.com
Password: 04c21df8f-4890-7024-y2vk-6bny143ta642
```

Configure Vite in your **vite.config.js**:

**a) Add the alias** — The theme imports Filament's base CSS. Add to `resolve.alias` (and `import path from 'path'` at the top if needed):

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

**b) Add the theme to the build** — Add a new item to the `input` array of your Laravel Vite plugin:

```js
input: [
    'resources/css/app.css',
    'resources/js/app.js',
    'vendor/tokeui/filament-tokeui-theme/resources/css/theme.css',
],
```

Run:

```bash
npm run build
```

Register the plugin on your panel (e.g. `app/Providers/Filament/AdminPanelProvider.php`):

```php
use TokeUI\FilamentTokeUITheme\FilamentTokeUIThemePlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->plugin(FilamentTokeUIThemePlugin::make());
}
```

The plugin registers the theme via `vendor/tokeui/filament-tokeui-theme/resources/css/theme.css`. Use `npm run dev` during development.

You're all set!

## Stat Overview — extraAttributes and classes

Filament **Stats Overview** widgets support HTML attributes on each stat card via `->extraAttributes(['class' => '...'])`. TokeUI Theme provides predefined classes so you can style cards by type (e.g. success, warning, or a solid "pro" look).

### Usage

On each `Stat` in your widget, pass one class per card:

```php
use Filament\Widgets\StatsOverviewWidget\Stat;

Stat::make('Revenue', '$12.5k')
    ->description('This month')
    ->extraAttributes(['class' => 'stat-card-emerald']);
```

Use a single class per card (e.g. `stat-card-rose`, `stat-card-blue-pro`, or `stat-card-blue-pro-plain`).

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

### "Pro" variants (pastel background, neutral value/label, accent on bar and description)

| Class                  | Appearance                             |
| ---------------------- | -------------------------------------- |
| `stat-card-blue-pro`   | Pastel blue, neutral text, blue accent |
| `stat-card-green-pro`  | Pastel green                           |
| `stat-card-rose-pro`   | Pastel rose                            |
| `stat-card-amber-pro`  | Pastel amber                           |
| `stat-card-violet-pro` | Pastel violet                          |
| `stat-card-sky-pro`    | Pastel sky blue                        |

### "Bar" variants (accent bar at bottom, white text in bar)

| Class                   | Appearance                                         |
| ----------------------- | -------------------------------------------------- |
| `stat-card-bar-orange`  | Orange value, orange bottom bar, white text in bar |
| `stat-card-bar-rose`    | Rose                                               |
| `stat-card-bar-emerald` | Emerald                                            |
| `stat-card-bar-blue`    | Blue                                               |

### "Pro plain" variants (solid background, all text white)

| Class                        | Appearance                                              |
| ---------------------------- | ------------------------------------------------------- |
| `stat-card-blue-pro-plain`   | Solid blue background, value/label/description in white |
| `stat-card-green-pro-plain`  | Solid green                                             |
| `stat-card-rose-pro-plain`   | Solid rose                                              |
| `stat-card-amber-pro-plain`  | Solid amber                                             |
| `stat-card-violet-pro-plain` | Solid violet                                            |

## Appearance

The theme is shown below in both **light** and **dark** mode.

### Shop Dashboard

| Light                                           | Dark                                           |
| ----------------------------------------------- | ---------------------------------------------- |
| ![Shop Dashboard (light)](screenshots/s1-l.png) | ![Shop Dashboard (dark)](screenshots/s1-d.png) |

### HR Dashboard

| Light                                         | Dark                                         |
| --------------------------------------------- | -------------------------------------------- |
| ![HR Dashboard (light)](screenshots/s2-l.png) | ![HR Dashboard (dark)](screenshots/s2-d.png) |

### Stat UI View

| Light                                         | Dark                                         |
| --------------------------------------------- | -------------------------------------------- |
| ![Stat UI View (light)](screenshots/s3-l.png) | ![Stat UI View (dark)](screenshots/s3-d.png) |

### Stat cards grid

| Light                                       | Dark                                       |
| ------------------------------------------- | ------------------------------------------ |
| ![Stat cards (light)](screenshots/s4-l.png) | ![Stat cards (dark)](screenshots/s4-d.png) |

### Notifications and stat cards

| Light                                                         | Dark                                                         |
| ------------------------------------------------------------- | ------------------------------------------------------------ |
| ![Notifications and stat cards (light)](screenshots/s5-l.png) | ![Notifications and stat cards (dark)](screenshots/s5-d.png) |

## License

Proprietary. Use is subject to the license provided with your purchase.
