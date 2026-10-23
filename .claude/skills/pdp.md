---
name: pdp
description: Baut eine vollständige Shopify Product Detail Page (PDP) für NATURAPlus™ Produkte. Erstellt alle Custom Liquid Sections und Shopify Theme Texte basierend auf Research und Mechanismus.
user_invocable: true
---

# PDP Skill — NATURAPlus™ Product Detail Page Builder

## Ablauf

Wenn der User `/pdp` aufruft, folge diesem Ablauf:

### Schritt 1: Informationen sammeln

Frage den User nach:

1. **Produktname** — z.B. "HaarVita", "Viturea"
2. **Angle / Zielgruppe** — z.B. "Frauen auf Abnehmspritzen mit Haarausfall", "Frauen mit altersbedingter Blasenschwäche"
3. **Mechanismus** — Die geschlossene Kette: Problem → Ursache → warum andere Lösungen nicht funktionieren → wie das Produkt eingreift → Ergebnis. Beispiel HaarVita GLP-1: Abnehmspritze → Fett wird abgebaut → Östrogen sinkt (weil auch in Fettgeweben produziert) → Östrogen schützt nicht mehr vor DHT → DHT greift Follikel an → Haare fallen aus. Lösung: Sägepalme blockiert DHT + Kürbiskernöl stärkt Follikel.
4. **Wirkstoffe** — Namen, Beschreibung, Tags (z.B. "KALTGEPRESST", "STANDARDISIERT"), Bild-URLs
5. **Empfohlene Einnahme** — Falls abweichend vom Standard (Täglich 2 Kapseln mit Wasser zu einer Mahlzeit)

### Schritt 2: Research durchführen

Führe eine Recherche durch zu:
- Zielgruppe: Ängste, Zweifel, Kaufbarrieren, Desires
- Wirkstoffe: wissenschaftliche Belege, traditionelle Verwendung
- Problem: wie es sich im Alltag der Zielgruppe zeigt
- Konkurrierende Lösungen: warum sie nicht funktionieren (laut Mechanismus)

### Schritt 3: Alle Sections bauen

Baue die Sections in dieser Reihenfolge. Jede Section wird als eigene Datei gespeichert unter `pdp-[sectionname]-[produkt].html`.

---

## PDP Sections — Reihenfolge

### Section 1: Titel (Custom Liquid)

Produktname wird über Shopify Liquid Variable `{{ product.title }}` eingefügt. Brandname NATURAPlus™ ist immer Teil des Produkttitels.

```html
{{ 'https://fonts.googleapis.com/css2?family=Baloo+2:wght@700;800&display=swap' | stylesheet_tag }}

<style>
  .hv-product-title {
    font-family: 'Baloo 2', 'Poppins', sans-serif;
    font-weight: 800;
    color: #2E6E4E;
    font-size: 42px;
    line-height: 1.1;
    letter-spacing: -0.5px;
    margin: 0 0 16px 0;
  }

  @media screen and (max-width: 749px) {
    .hv-product-title {
      font-size: 30px;
    }
  }
</style>

<h1 class="hv-product-title">
  {{ product.title }}
</h1>
```

**Regeln:** Code bleibt gleich. Nur der CSS-Prefix wird pro Produkt angepasst (z.B. `hv-` für HaarVita, `vt-` für Viturea).

---

### Section 2: Benefits (Custom Liquid)

4 Checkmark-Benefits basierend auf Research und Mechanismus. Jeder Benefit hat ein Keyword **fett markiert**.

**Regeln:**
- Benefit 1: Hauptwirkung des Produkts (aus dem Mechanismus)
- Benefit 2: Zweite Wirkung / zweiter Wirkstoff
- Benefit 3: Zeitrahmen für Ergebnisse
- Benefit 4: Natürlichkeit / Sicherheit

**Template:**
```html
<!-- [PRODUKT] Benefits Section -->
<div class="[prefix]-benefits-section">
  <div class="benefits-list">
    <div class="benefit-item">
      <span class="checkmark">✓</span>
      <span class="benefit-text"><strong>[KEYWORD]</strong> [Benefit-Text]</span>
    </div>
    <!-- 3 weitere benefit-items -->
  </div>
</div>
```

**CSS-Konstanten:**
- Background: `#e8f0e4`
- Border-radius: `8px`
- Text-Farbe: `#2d4a2d`
- Checkmark + Bold-Farbe: `#3a5a3a`
- Font-size: 14px (mobile 13px)
- Font: System-Font-Stack

---

### Section 3: Einklappbare Reihen (Shopify Theme — nur Text)

Kein Custom Liquid Code nötig — diese werden als Shopify "Einklappbare Reihe" Blöcke im Theme Editor eingefügt. Du lieferst nur den Text.

#### Reihe 1: Beschreibung
- Basierend auf Research
- Wichtige Wörter **fett markiert**
- 2-3 kurze Absätze
- Spricht das Problem der Zielgruppe an und positioniert das Produkt als Lösung
- Endet mit einem kurzen emotionalen Satz

#### Reihe 2: Warum brauchst du NATURAPlus™ [Produkt]?
- Basierend auf Research
- 4-5 Absätze Fließtext
- Absatz 1: Emotionaler Einstieg — das Problem im Alltag
- Absatz 2: Warum andere Lösungen nicht funktionieren
- Absatz 3: Was das Produkt anders macht (Wirkstoffe + Einnahme)
- Absatz 4: Du sollst dich nicht entscheiden müssen (Empowerment)
- Absatz 5: Probier es risikofrei aus (Garantie)

#### Reihe 3: Empfohlene Einnahme (BLEIBT IMMER GLEICH)
```
**Täglich 2 Kapseln** mit Wasser, am besten zu einer Mahlzeit. Regelmäßige Einnahme führt zu den besten Ergebnissen.

Die meisten Kundinnen berichten von sichtbaren Verbesserungen innerhalb von 4 Wochen.
```

#### Reihe 4: Gibt es eine Garantie? (BLEIBT IMMER GLEICH)
```
Ja! Alle NATURAPlus™ Bestellungen sind durch unsere 120-Tage-Geld-zurück-Garantie abgesichert.

Wenn du nicht vollständig zufrieden bist, kontaktiere uns einfach — wir kümmern uns darum, ohne Wenn und Aber.
```

---

### Section 4: Timeline (Custom Liquid)

Scroll-Animation mit 4 Zeitblöcken. Headline + Subtitle + je 3 Benefits pro Block. Alles basierend auf Research und Mechanismus.

**Zeitblöcke:**
- Woche 1-2: Erste Wirkung beginnt
- Woche 3-4: Spürbare Veränderung
- Woche 5-8: Sichtbare Ergebnisse
- Woche 9-12: Volles Ergebnis + emotionaler Payoff

**Regeln:**
- Headline: Emotionaler Satz + Accent-Zeile (kursiv, gold `#D4A843`)
- Subtitle: Erklärt kurz wie das Produkt wirkt + "So verändert sich [Bereich], wenn du täglich zwei Kapseln nimmst:"
- Benefits pro Woche: 3 Stück, mit `<strong>` Keywords
- CTA: Gold-Pill-Button `#E8C840`, Text "Jetzt [Produkt] starten →"
- Garantie-Zeile unter CTA: "🛡 120 Tage Geld-zurück-Garantie"

**CSS-Prefix:** `[kürzel]tl-` (z.B. `hvtl-` für HaarVita, `vttl-` für Viturea)

**CSS-Konstanten:**
- Section-Background: `#e8f0e4`
- Headline-Font: Fraunces, 900, `#2d4a2d`
- Week-Label: Fraunces 700, weiß auf `#2d4a2d`, border-radius 10px
- Benefits: Work Sans 15px, `#2d4a2d`
- Strong: `#152A11`
- Track: `#b8cfb0` (inactive), `#2d4a2d` (active)
- Dots: 16px, gleiche Farben
- CTA: `#E8C840`, schwarz Text, pill-shape (border-radius 50px)

**Fonts laden:**
```css
@import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,700;9..144,900&family=Work+Sans:wght@400;500;600;700&display=swap');
```

**JavaScript:** Scroll-basierte Animation — Dots und Benefits werden sichtbar wenn sie in den Viewport scrollen (75% trigger). Track-Fill wächst mit. `setInterval(update, 30)`.

---

### Section 5: Reviews (Shopify Theme — nur Text)

Kein Custom Liquid Code. Du schreibst **5-7 Reviews** als Text.

**Regeln:**
- Jede Review hat: Vorname, Alter, GLP-1 Marke (oder relevanter Kontext für den Angle), Sterne (4-5), Text
- Reviews adressieren gezielt:
  - **Angst** (z.B. "Ich hatte Angst eine Glatze zu bekommen")
  - **Zweifel** (z.B. "Ich war skeptisch ob es wirklich funktioniert")
  - **Kaufbarriere** (z.B. "Ich habe schon so viel Geld für nichts ausgegeben")
  - **Desire** (z.B. "Endlich kann ich meine Haare wieder offen tragen")
  - **Zeitrahmen** (z.B. "Nach 3 Wochen habe ich die ersten Babyhärchen gesehen")
  - **Vergleich** (z.B. "Biotin hat nichts gebracht, aber HaarVita schon")
  - **Garantie-Bestätigung** (z.B. "Die 120-Tage-Garantie hat mir den Schritt leichter gemacht")
- Alter und Geschlecht müssen zur Zielgruppe passen
- Sprache: Natürlich, authentisch, nicht zu perfekt — wie echte Kunden schreiben
- Mindestens 1 Review die spezifisch den Mechanismus bestätigt

---

### Section 6: Mechanismus (Custom Liquid)

Karte mit Bild/GIF oben und zwei Textabsätzen.

**Regeln:**
- Headline: "So wirkt [Produkt]." — Fraunces 900
- Absatz 1 (Problem): Beschreibt was im Körper passiert (aus dem Mechanismus). Wichtige Begriffe **fett**.
- Absatz 2 (Lösung): Beschreibt wie das Produkt eingreift. Wirkstoffe + Wirkung **fett**.
- Bild-URL muss vom User geliefert werden

**CSS-Prefix:** `[kürzel]mech-` (z.B. `hvmech-`)

**CSS-Konstanten:**
- Section-Background: `#e8f0e4`
- Card-Background: `#f2f7ef`
- Card: max-width 520px, border-radius 16px, box-shadow
- Text: Work Sans 15px (mobile 14px), `#2d4a2d`, text-align left
- Strong: `#152A11`
- Headline: Fraunces 32px (mobile 26px), 900, `#2d4a2d`

---

### Section 7: Garantie (Custom Liquid — BLEIBT IMMER GLEICH)

```html
<section class="np-guarantee">
  <div class="np-g-inner">
    <h2 class="np-g-title">120 Tage Garantie <span class="np-g-title--accent">Risikofrei!</span></h2>
    <p class="np-g-text">Wir sind überzeugt, dass du uns lieben wirst — aber wir verstehen, dass du dir vielleicht noch nicht sicher bist.</p>
    <p class="np-g-bold">Deshalb bieten wir dir eine 120-Tage-Testphase.</p>
    <p class="np-g-text">Wenn du aus irgendeinem Grund nicht zufrieden bist, kannst du es innerhalb von 120 Tagen nach Lieferdatum zurückgeben — und bekommst dein Geld vollständig zurück.</p>
    <button type="button" class="np-g-cta" onclick="window.scrollTo({top: 900, behavior: 'smooth'});">Jetzt bestellen und sparen</button>
  </div>
</section>
```

**CSS-Konstanten:**
- Background: `#cfe7f5` (hellblau)
- Title-Font: Baloo 2, 800, `#1f5c34`
- Accent: `#6cb6e8` (blau)
- Body-Font: Poppins, 16px, `#3d5a4c`
- CTA: `#f0cd4a` (gelb), pill-shape, `#1f5c34` Text

---

### Section 8: Ingredients (Custom Liquid — BLEIBT GLEICH sofern nicht befohlen)

Slider mit einer Karte pro Wirkstoff. Pro Karte: Bild, Name, Tag, Beschreibung, Footnote.

**Was pro Produkt angepasst wird:**
- Wirkstoff-Namen
- Bild-URLs
- Tags (z.B. "KALTGEPRESST", "STANDARDISIERT")
- Beschreibungstext
- Footnote

**CSS-Prefix:** `hv-ing-`

**CSS-Konstanten:**
- Section-Background: `#e8f0e4`
- Card-Background: `#f2f7ef`
- Title: 32px, 900, italic, `#2d4a2d`
- Name: 20px, 800, `#2d4a2d`
- Tag: 11px, 700, underline, `#3a5a3a`
- Arrows: 44px circle, border `#2d4a2d`

---

### Section 9: FAQ (Shopify Theme — nur Text)

Kein Custom Liquid Code. Du schreibst **4 spezifische Fragen + Antworten** basierend auf Research.

**Regeln:**
- Die Fragen sollen psychologisch die Kaufbarrieren der Zielgruppe überwinden
- Frage 1: Adressiert die Hauptangst / den größten Zweifel
- Frage 2: Adressiert Kompatibilität mit bestehendem Verhalten (z.B. "Kann ich es zusammen mit meiner Spritze nehmen?")
- Frage 3: Adressiert Zeitrahmen / Erwartungsmanagement
- Frage 4: Adressiert Vergleich mit Alternativen / warum das hier anders ist
- Antworten: Kurz, direkt, beruhigend. 2-3 Sätze pro Antwort.

**Standard-FAQs die immer zusätzlich rein kommen (nicht von dir geschrieben):**
- Gibt es eine Geld-zurück-Garantie?
- Wie nehme ich die Kapseln ein?
- Was ist NATURAPlus™?

---

## Design System Konstanten

### Farben
| Token | Hex | Verwendung |
|-------|-----|------------|
| Deep Green | `#24421F` / `#2d4a2d` | Primary, Headlines, Track |
| Dark Text | `#152A11` | Strong/Bold Text |
| Sage BG | `#e8f0e4` | Section Backgrounds |
| Card BG | `#f2f7ef` | Karten-Hintergrund |
| Off-White | `#FAFAF8` | Review BG |
| Gold | `#D4A843` | Sterne, Akzente |
| CTA Yellow | `#E8C840` / `#f0cd4a` | CTA Buttons |
| Guarantee Blue | `#cfe7f5` | Garantie-Section BG |
| Title Green | `#2E6E4E` | Produkt-Titel |
| Muted Green | `#5a7a5a` | Subtitles |
| Check Green | `#3a5a3a` | Checkmarks, Tags |
| Track Inactive | `#b8cfb0` | Timeline Track |

### Fonts
| Font | Gewicht | Verwendung |
|------|---------|------------|
| Baloo 2 | 700, 800 | Produkt-Titel, Garantie-Headline |
| Fraunces | 400, 700, 900 | Section Headlines (Custom Liquid) |
| Work Sans | 400-700 | Body Text (Custom Liquid) |
| Poppins | 400, 700 | Garantie-Section Body |
| System Stack | — | Benefits, Ingredients |

### CSS-Prefix Konvention
Format: `[Produktkürzel][Sektionskürzel]-`
- Beispiel HaarVita: `hv-` (title), `hvtl-` (timeline), `hvmech-` (mechanism), `hvrw-` (reviews), `hv-ing-` (ingredients)
- Beispiel Viturea: `vt-` (title), `vttl-` (timeline), `vtmech-` (mechanism), etc.
- Garantie bleibt immer `np-g-` (brand-level)

### Allgemeine Regeln
- **Sprache:** Deutsch, Du-Form, DACH-Markt
- **Brandname:** NATURAPlus™ — immer mit ™
- **Garantie:** 120 Tage Geld-zurück-Garantie — immer gleich
- **Alle Custom Liquid Blöcke:** Self-contained — eigenes CSS, eigene Fonts, keine Theme-Abhängigkeit
- **Mobile-First:** Alle Sections responsiv, font-sizes kleiner auf mobile
- **Max-Width:** Content-Bereiche max 520-620px
- **Tonalität:** Empathisch, direkt, lösungsorientiert. Keine medizinischen Versprechen. Natürliche Sprache wie eine Freundin die einen Tipp gibt.

---

## Output Format

Wenn du die PDP baust, liefere:

1. **Custom Liquid Sections als HTML-Dateien:**
   - `pdp-titel-[produkt].html`
   - `pdp-benefits-[produkt].html`
   - `pdp-timeline-[produkt].html`
   - `pdp-mechanismus-[produkt].html`
   - `pdp-garantie-[produkt].html` (nur bei erstem Produkt, danach wiederverwenden)
   - `pdp-ingredients-[produkt].html`

2. **Shopify Theme Texte als Markdown-Datei:**
   - `pdp-texte-[produkt].md` — enthält:
     - Einklappbare Reihe: Beschreibung
     - Einklappbare Reihe: Warum brauchst du NATURAPlus™ [Produkt]?
     - 5-7 Review-Texte (mit Name, Alter, Marke/Kontext, Sterne, Text)
     - 4 FAQ Fragen + Antworten
