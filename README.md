# GMI Invoice Flight Animation

> Endlos-Loop. Rechnungen fliegen von links nach rechts. **Keine Scroll-Interaktivität** — also nicht das Problem von früheren Lottie-Versuchen.

## Files

| Datei | Was es ist |
|---|---|
| `invoice-1.svg` | Klassisches Rechnungs-Icon mit Header-Band |
| `invoice-2.svg` | Receipt mit zackiger Unterkante |
| `invoice-3.svg` | Rechnung mit hervorgehobenem Total-Bar |
| `animation-loop.html` | Komplette Animation, embed-fertig (inline-SVGs, currentColor) |

> **Hinweis zum Ordnername:** "Lottie Animation" als Sammelbegriff — die technische Umsetzung ist hier **CSS + SVG**, kein echtes Lottie-JSON. Für eine reine Loop-Animation ohne Scroll-Reaktivität ist das die einfachere und stabilere Wahl. Falls echtes Lottie nötig wird, AE-Datei → Bodymovin-Export → JSON.

---

## Integration — drei Wege

### Weg 1: GitHub Pages Iframe (schnell, wie beim FDS-Header)
1. Ordner committen in einem neuen oder bestehenden GitHub-Repo
2. GitHub Pages aktivieren → URL z.B. `https://wanjadoering.github.io/gmi-animations/Lottie%20Animation/animation-loop.html`
3. In Axure oder finaler Website per Inline-Frame einbinden:
```html
<iframe src="DEINE-GITHUB-PAGES-URL" width="100%" height="120" style="border:0; background:transparent;"></iframe>
```

### Weg 2: Inline-Code (cleanest, für finale Website-Implementation)
- Den gesamten Inhalt von `animation-loop.html` kopieren (`<style>` + `<div class="flight-zone">…</div>`)
- Direkt in die Hero-Komponente der Website einbauen
- Dev-Team kann CSS-Variablen anpassen wie sie wollen

### Weg 3: SVGs einzeln nutzen
- Die drei `.svg`-Dateien sind eigenständig nutzbar — z.B. als Icons in der Sektion "Why this connection", in der FAQ, oder anderswo wo Rechnungs-Symbolik passt

---

## Customizing — CSS-Variablen

In `animation-loop.html` oben im `:root` Block änderst du:

```css
:root {
  --invoice-color: #44a4dc;  /* Brand-Farbe (Cyan) */
  --duration: 4.2s;          /* wie lange ein Icon von links nach rechts braucht */
  --stagger: 0.7s;           /* Pause zwischen den Icons */
  --invoice-w: 44px;         /* Basisgröße */
}
```

**Schneller wirken lassen:** `--duration` auf 3s · `--stagger` auf 0.5s
**Dezenter wirken lassen:** `--duration` auf 6s · `--stagger` auf 1.2s

---

## Was diesmal anders ist als beim alten Lottie-Problem

Du hattest erwähnt, dass früher das Lottie-Embedding Probleme hatte — speziell bei Scroll-Reaktivität.

Diese Animation:
- **läuft permanent**, ist nicht von Scroll-Position abhängig
- braucht **kein Lottie-Player-JS** (keine 250 KB Extra-Library)
- ist **pures CSS** — funktioniert in jedem Browser ohne Setup
- hat eingebaut **`prefers-reduced-motion`** Fallback (für Nutzer mit Animations-Allergie)

Falls trotzdem Probleme auftauchen, sind die Punkte zum Debuggen:
1. Iframe-CSP / `frame-ancestors` Header im CMS prüfen
2. Wenn die SVG-Farbe nicht durchschlägt: `currentColor` braucht eine Eltern-Element-Farbe (`.invoice { color: #44a4dc; }`)
3. Bei flackernder Animation auf älteren Geräten: `will-change: transform, opacity` ist drin, sollte helfen

---

## Vorschau

`animation-loop.html` einfach im Browser öffnen → siehst die Animation in voller Viewport-Größe.

Stand: 28.05.2026 · Wanja · GMI Marketing
