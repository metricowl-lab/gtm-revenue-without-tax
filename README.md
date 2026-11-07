# Revenue Without Tax

A web variable template that works out revenue without VAT, GST or sales tax from a price that includes it. It returns the amount without tax, or the tax itself, rounded to the decimal places you choose.

## Why

GA4 reports `value` as revenue, and Google Ads uses it for return on ad spend. UK, EU, Australian and New Zealand prices usually include tax, so sending them as they are overstates revenue by the tax rate. This template fixes the event's `value`; item prices in `items` still include tax unless you change them at source. More in [VAT in GA4 revenue for UK stores](https://www.metricowl.co.uk/article/vat-in-ga4-revenue-uk-stores) and [Canadian sales tax in GA4 revenue](https://www.metricowl.co.uk/article/canadian-sales-tax-ga4-revenue).

## Set up

1. Add the template from the gallery, or import `template.tpl` under **Templates**.
2. Create a variable from it, for example **Value without tax**. Set **Amount including tax** to your value variable, such as a Data Layer Variable for `ecommerce.value`.
3. Choose **Remove a tax rate** (for example 20 for UK VAT), or **Subtract a tax amount** if your site already sends the tax.
4. Use `{{Value without tax}}` as the `value` in your GA4 purchase tag and your ad platforms' conversion tags.
5. Optionally, create a second variable with **Return** set to **The tax**, and send it as GA4's `tax` parameter.

## Settings

| Setting | What it does |
|---|---|
| Amount including tax | The value with tax included. A plain number, such as `120` or `120.00`. |
| How to remove the tax | **Remove a tax rate** or **Subtract a tax amount** |
| Tax rate (%) | For a rate. `20` turns 120 into 100. |
| Tax amount | For an amount. For example `ecommerce.tax`. |
| Return | The amount without tax, or the tax |
| Decimal places | 2 by default, up to 10 |

## Things to know

- **Mixed rates:** if your shop sells items at different rates, such as zero-rated children's clothes, **Subtract a tax amount** is more accurate than one rate for everything.
- **Not a number:** if the amount isn't a plain number, such as `£120` or `12 GBP`, the variable returns `undefined` rather than a wrong value.
- **Refunds:** negative amounts stay negative and round the same way.
- **Tax amounts:** with **Subtract a tax amount**, a tax larger than the amount gives a negative result, so check the variable you map it to.
- **Exact rounding:** the maths is done in whole pence or cents, so floating-point error can't tip a half-penny the wrong way, and the amount without tax plus the tax always adds back up to the original amount. The amount without tax is rounded first and the tax is what's left, so at an exact half-penny the tax can come out a penny lower. With 2 decimal places this holds for any realistic order value; with 10 it holds up to about 900,000.
- **Decimal places** are capped at 10.

## Permissions

None. The template only does arithmetic on the values you give it.

## Licence

Apache License 2.0. See [LICENSE](LICENSE).

Built and maintained by Marc Alexander at [Metric Owl](https://www.metricowl.co.uk), a GA4 and Google Tag Manager consultancy in London. Issues and suggestions are welcome.
