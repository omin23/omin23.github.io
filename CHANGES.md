# Changelog

## 2026-03-16 — Design Fix Pass

### HTML Fixes (`index.html`)

1. **DOCTYPE was commented out** (line 1)
   - `<!-- <!DOCTYPE html> -->` → `<!DOCTYPE html>`
   - Without a DOCTYPE the browser renders in quirks mode, breaking layouts.

2. **Viewport meta missing comma** (line 6)
   - `content="width=device-width initial-scale=1"` → `content="width=device-width, initial-scale=1"`
   - Missing comma caused the viewport meta to be parsed incorrectly, breaking responsive scaling on mobile.

3. **News Aggregation project card was outside `#projects-container`** (lines ~324–352)
   - A premature `</div>` closed the `#projects-container` row before the News Aggregation card, leaving it orphaned outside the row.
   - **Effect:** The card was not affected by the category filter buttons (All / ML-AI / etc.) and its grid column had no parent row, causing layout breakage.
   - **Fix:** Removed the premature `</div>` and corrected the indentation of the card so it sits properly inside the row alongside the other five project cards.

### CSS Fixes (`assets/css/style.css`)

4. **Duplicate `.teal-text` rule** (lines ~519 and ~649)
   - Two separate `.teal-text` declarations existed. The second (later) one lacked the `:hover` state; the first lacked the `text-shadow`.
   - **Fix:** Merged into a single canonical block with both `color`, `text-shadow`, and a `:hover` rule. Removed the duplicate.

5. **"Card Consistency" block overrode gold-glow with `!important`** (lines ~1354–1364)
   - A later block redefined `.card` and `.card:hover` with `!important` flags, replacing the designed gold/blue box-shadow glows (`rgba(255, 203, 5, 0.2)`) with plain black shadows and suppressing the `border-color` change on hover.
   - **Fix:** Removed the entire conflicting block. The original, higher-quality card hover definitions (with gold glow) now take full effect.

6. **Project card descriptions caused inconsistent card-content height**
   - Descriptions varied from 1 to 3+ visible lines, making the content area look uneven across cards.
   - **Fix:** Added CSS line-clamp (max 3 lines) to `.card.medium .card-content p`, added `overflow: hidden` to `.card.medium .card-content`, and normalized description font-size and line-height. All project cards now display a uniform content block.

### Color Scheme
All changes preserve the existing Michigan theme: `#ffcb05` (maize gold), `#00274c` (Michigan blue), `#0a0a0a` (dark background), `#e0e0e0` / `#b0b0b0` (text grays).
