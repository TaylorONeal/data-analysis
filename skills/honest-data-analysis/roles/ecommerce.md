# Ecommerce Analyst
*Shopify, Amazon Seller, GA4, order and returns exports*

> **Template stub.** This role is not yet in the canonical `data.ts` ROLES data, so the "what good output looks like" numbers below are intentionally left blank. The structure and the domain gotcha are real. Fill the Claim / Evidence / Calculation / Confidence with figures computed from your own file. Do not invent them; that is the one thing this whole repo exists to prevent.

## Plug into the prompt

- **Data sources:** Shopify order export, Amazon Seller Central, GA4 ecommerce CSV, returns log.
- **Primary metric column:** AOV, conversion rate, repeat-purchase rate, return rate, contribution margin per order.
- **Grouping column:** SKU or category, channel, discount code, new vs returning customer.
- **Time grain:** Daily for traffic and orders. Weekly or monthly for cohort repeat-purchase.

In the Analyze prompt (`references/02-analyze.md`), restate the primary metric and grouping column above before any finding.

## What good output looks like

- **Claim:** _(one specific sentence with a number, computed from your data)_
- **Evidence:** _(source rows, column, aggregation)_
- **Calculation:** _(the actual math)_
- **Confidence:** _(high / medium / low, with sample size and a one-line reason)_

See `roles/marketing.md` for a filled-in example of this block.

## Watch out for

Gross vs net revenue. Figures before returns and refunds overstate performance. Tell the model to state whether every revenue number is gross or net, and to cite the returns column when one exists.

---
Want this role promoted to a full overlay? See `CONTRIBUTING.md`.
