# Ball Leved — Microsoft Store PWA

Upload these files to the root of a GitHub repository, enable GitHub Pages, then package the HTTPS site using PWABuilder for Microsoft Store.

## Gameplay
Two free attempts per browser installation (stored locally); one play is consumed when starting a run. Match 3+ same-colored bubbles. Unattached bubbles drop. The ceiling moves downward every 5 shots. No timer. Game ends when bubbles cross the danger line.

## Real Microsoft Store billing integration
The game uses `window.getDigitalGoodsService('https://store.microsoft.com/billing')` and `PaymentRequest` with the Microsoft Store payment method. It does **not** simulate payment or award plays after a client-only response.

Create these **consumable** in-app products in Microsoft Partner Center and use these exact InAppOfferToken values (or change PACKS in app.js):

- `ballleved_5` — 5 plays — USD 5
- `ballleved_7` — 7 plays — USD 7
- `ballleved_10` — 10 plays — USD 10
- `ballleved_13` — 13 plays — USD 13

Set regional prices in Partner Center. The UI displays actual regional Store prices when available. Billing APIs only work in eligible Store-installed Windows PWAs, not ordinary browser previews.

**Important: not yet production-ready for paid consumables.** Implement a secure backend for Microsoft purchase-token verification, idempotent grants, user identity, durable play balances, restore/reconciliation, and Store consumption/fulfillment before enabling sales. The current purchase UI initiates genuine Store checkout, but intentionally never credits paid plays without verification. The two free plays are local-only and not tamper-resistant. See Microsoft Digital Goods API docs: https://learn.microsoft.com/en-us/microsoft-edge/progressive-web-apps/how-to/digital-goods-api
