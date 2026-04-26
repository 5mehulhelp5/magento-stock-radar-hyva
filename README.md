# Stock Radar — Hyva compatibility

Companion module to `byte8/module-stock-radar` that swaps the Luma RequireJS template for an Alpine.js + Tailwind variant. Uses `hyva.getFormKey()` for CSRF and reads variant SKU updates from a `byte8:stockradar:variant` window event so configurable PDPs subscribe to the right simple SKU.

## Install

```bash
composer require byte8/module-stock-radar-hyva
bin/magento module:enable Byte8_StockRadarHyva
bin/magento setup:upgrade
```

Both `byte8/module-stock-radar` and `hyva-themes/magento2-theme-module` must be installed and enabled.

## What this module does (and doesn't)

- ✅ Swaps the PDP "Notify me" template to a Hyva variant
- ✅ Zero new admin or backend code
- ❌ No new business logic — all validation, dispatch, and email sending lives in the parent module

## Wiring variant SKU into the form

If the PDP is configurable, dispatch the variant SKU when the user picks options:

```javascript
window.dispatchEvent(new CustomEvent('byte8:stockradar:variant', { detail: selectedSimpleSku }));
```

Hyva swatches and select renderers can hook into the `private-content-loaded` event or the swatch click handler to fire this.

## Support

Byte8 Ltd — support@byte8.io
