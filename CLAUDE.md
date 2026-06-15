# TraderVault App — project notes

## Asset lookup pattern (TradingView-inspired)
Whenever the app needs to look up / pick a tradable asset (symbol), use this pattern:

- **Searchable combobox**: a single search field ("Search asset class or symbol…") with a search icon and a chevron that toggles the dropdown. Focusing or clicking the chevron opens it.
- **Class pills**: `All`, then `Forex`, `Futures`, `Equities`, `Crypto`, `Metals`. The active pill uses the accent style. Pills filter the list by asset class; **All** shows every symbol.
- **Result rows** (TradingView-style): each row = a circular class-colored avatar (class icon on a soft tint) + bold **symbol code** + muted **full name** + a small uppercase class tag. The currently-selected symbol gets a 3px accent left border + accent-soft background.
- **Filtering logic**: if the search box has text, match it against symbol code OR name across **all** classes (ignores the pill). If the box is empty, show the active pill's class (or everything when the pill is `All`).
- **Selection drives downstream logic**: every asset carries `{ sym, name, ptValue, stopPts, unit }`. On select, store the class + symbol and recompute anything asset-dependent (e.g. the Position Calculator: `riskPerUnit = ptValue × stopPts`, `contracts = dollarRisk / riskPerUnit`, capped by Max pos.; result subtitle shows `SYM · $ptValue/pt · stopPts pt stop`, units = the asset's `unit`).
- The asset catalog lives in `App.dc.html` → `btAssets()`. Add new symbols there with the same shape.

Keep all of this in the project's existing token styles (`var(--bg/--subtle/--border/--head/--body/--muted/--accent/--profit/--warn)`); never hard-code new theme colors.
