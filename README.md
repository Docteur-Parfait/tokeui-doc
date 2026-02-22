# TokeUI Theme — Installation

This zip contains **theme.css** (the TokeUI Filament theme) and this README. Follow the steps below to install the theme in your Laravel/Filament project.

## 1. Copy the theme file

Place **theme.css** in your project at:

```
resources/css/tokeui/theme.css
```

Create the `tokeui` folder under `resources/css/` if it does not exist.

## 2. Configure Vite

In **vite.config.js**:

**a) Alias** — add to `resolve.alias` (and `import path from 'path'` at the top if needed):

```js
'filament-base-theme': path.resolve(__dirname, 'vendor/filament/filament/resources/css/theme.css'),
```

**b) Input** — add to the Laravel Vite plugin `input` array:

```js
'resources/css/tokeui/theme.css',
```

## 3. Register the theme on your panel

In your panel provider (e.g. `app/Providers/Filament/AdminPanelProvider.php`), add:

```php
->viteTheme('resources/css/tokeui/theme.css')
```

Remove any existing `->viteTheme(...)` or plugin that registered another theme.

## 4. Build

```bash
npm run build
```

(or `npm run dev` for development).

---

For the full documentation (stat card classes, screenshots, usage), see:  
[https://github.com/Docteur-Parfait/tokeui-doc](https://github.com/Docteur-Parfait/tokeui-doc)
