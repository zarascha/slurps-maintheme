# CANPAN™ Maintheme – CHANGELOG

> [!IMPORTANT]
> Hinweis: Dieses CHANGELOG wird mithilfe von KI erstellt. Trotz sorgfältiger Prüfung können Fehler enthalten sein oder einzelne Änderungen fehlen.

---

## [PRE-LAUNCH] – 29-03-2026

**Basis**: Impact Theme v7.0.1 (unverändert)

### Release-Highlights
- Neue CANPAN-Erlebnisbausteine für Startseite und Produktseite (Story Bubbles, Collection Blocks, Feature Cards, Price Bubble).
- Starke Überarbeitung von Header, Navigation-Drawer, Quick Buy und Warenkorb für besseren Flow.
- Variantengetriebene Theme-Engine für Farben/Titel/CTA auf Produktseiten (live bei `variant:change`).
- `canpan-theme.css` als dediziertes Override-Layer über `theme.css` mit klarer Kaskadenstrategie.
- Umfangreiche Custom-Templates für Blog, Artikel und Shop-Seiten.
- Mehrere Lighthouse-, Accessibility- und Rendering-Fixes.

---

### Added

#### Layout, Foundation
- `assets/canpan-theme.css`: Globale CANPAN-Overrides, Utility-Klassen, Drawer-Stabilisierung, produktseitige Scope-Tokens, Price Bubble, Feature Cards, Social-Proof-, Trust- und Inventory-Elemente.
- `assets/canpan-placeholder.svg`
- `config/settings_schema.json`: Neuer Range-Slider `canpan_drawer_modal_border_radius` (0–40 px, Schritt 2 px, Standard 0) unter „Appearance and spacing" → „Rounding".

#### Neue Sections
- `sections/canpan-story-bubble.liquid`
- `sections/canpan-collection-blocks.liquid`

#### Neue Snippets
- `snippets/canpan-price-bubble.liquid`
- `snippets/canpan-feature-cards.liquid`
- `snippets/canpan-logo-inline.liquid`

---

### Changed

#### Layout, Foundation, Performance
- `layout/theme.liquid`: Google Site Verification Meta hinzugefügt; Viewport auf `width=device-width, initial-scale=1.0` vereinfacht (Lighthouse-Fix); Font-Preloads über Shopify `preload_tag`-Filter; `canpan-theme.css` als globales Stylesheet eingebunden; `canpan-cart.js` als deferred Script nach `theme.js` geladen.
- `snippets/css-variables.liquid`: `--canpan-drawer-modal-border-radius` als neues CSS-Token ergänzt; Cursor- und Checkmark-SVGs als inline Data-URIs eingebettet; 10 `--canpan-*` abgeleitete Farb-Tokens in neuem `:root`-Block.
- `assets/theme.css`: Mehrere Blöcke auskommentiert, deren Styling durch `canpan-theme.css` übernommen wird: `.badge:not(.badge--lg)`, `.line-item__actions`, `.product-quick-add`, `.thumbnail-swatch`, `.block-swatch`, `shopify-account`.

#### Header und Navigation
- `sections/header.liquid`: CANPAN Inline-SVG-Logo (`snippets/canpan-logo-inline.liquid`); Variant Theme Engine – liest `custom_variant.page_appearance`-Metafelder und setzt Header-/Footer-/CTA-Farben als `:root`-CSS-Variablen; JS-Sync bei `variant:change`; Featured-Block-Support im Schema; Header-Abstände angepasst.
- `snippets/navigation-panel.liquid`: Predictive Search direkt im Navigation-Drawer; Featured-Slider im Drawer; Reorganisation des Drawer-Footers (Social/Localization/Account).
- `sections/header-group.json`: Komplett auf CANPAN-Konfiguration gestellt (Drawer-Layout, Menüs, Featured-Inhalte).
- `sections/announcement-bar.liquid`: Preset-Definition für konsistente Instanziierung im Theme-Editor ergänzt.

#### Produktseite, Varianten und Merchandising
- `sections/main-product.liquid`: `canpan-product-theme-scope`-Klasse am Produkt-Root; Sticky Add-to-Cart um Custom Variant Titel, Price Bubble und Discount Badge erweitert; neuer Blocktyp `canpan_feature_cards` im Schema.
- `snippets/product-info.liquid`: Stabilere Blockgruppen-Logik für Offer/Accordion; Varianten-Metafeld-Titel (`custom_variant.title`) als priorisierter Produkttitel; Price-Row mit optionaler Inline Price Bubble; Rendering für `canpan-feature-cards`.
- `snippets/price-list.liquid`: Neuer Split-Price-Modus (`canpan_split_price`); Inline-Bubble-Injektion (`canpan_inline_bubble_markup`); robustere Sale-Logik für Line-item-Preisdarstellung.
- `snippets/product-badges.liquid`: Rainbow Custom Badge; neues Sale-Badge (Coupon-Icon + globale Klasse + verbesserte Vergleichslogik).
- `snippets/product-gallery.liquid`: Alt-Tag-basierte Sichtbarkeit/Filterung (`#mobile`, `#desktop`, `#vorschaubild`, `#Option_Wert`); Preload-Strategie für frühe Grid-Medien optimiert.
- `snippets/media.liquid`: Preload/Fetchpriority-Verhalten angepasst; Breiten-Sets aktualisiert.
- `snippets/product-quick-buy.liquid`: Variantenbasierter CSS-Farb-Scope für CTA-Buttons; Custom Variant Titel, Little Text, Price Bubble und Discount Badge im Quick-Buy-Header; Inventarstatus je Variante im Header.
- `assets/theme.js`: Lesbare URL-Parameter im Variant-Picker (z. B. `?groesse=6mm&kollektion=pinky-blossom`); initiales Variant-Mapping aus lesbaren URL-Parametern; `"title"` und `"canpan-feature-cards"` zu `blockTypes` für partielles Re-Render hinzugefügt; Bundle-Mover für `.product-info__complementary-products` (responsives Repositioning + Debounce); Tawk.to-Integration inkl. Z-Index-Steuerung und Deep-Link `#help-center-widget`.
- `snippets/variant-picker.liquid` & `snippets/product-card.liquid`: Option `kollektion` als Color-/Swatch-Kandidat ergänzt.
- `snippets/option-value.liquid` & `snippets/variant-picker.liquid`: `data-option-value-label` an Variant-Inputs für stabile URL-Slug-Mappings ergänzt.
- `snippets/canpan-feature-cards.liquid`: Metaobjekt-Feldnamen vereinheitlicht – `background_picture` → `background_image`, `text_and_iconcolor` → `text_and_icon_color`, `background_picture_opacity` → `background_image_opacity`.

#### Cart, Drawer, Checkout Flow
- `sections/variant-added.liquid`: Komplett überarbeitet – Success Box, Free Shipping Bar, Mengenanzeige, Payment Icons; CTA-Farben variantenbasiert via `custom_variant.page_appearance`; Custom Variant Titel; Checkout-Button zeigt nur noch `checkout_label`.
- `assets/theme.js`: `addedQuantity` in Cart-Event-Payload eingeführt; Drawer-Preis und -Menge des zuletzt hinzugefügten Items werden live aktualisiert.
- `snippets/free-shipping-bar.liquid`: Inline-SVG-Checkmark-Icon als Liquid-Variable direkt im `reached-message`-Attribut eingebettet.
- `snippets/line-item.liquid`: `custom_variant.title`-Metafeld als Warenkorbtitel; Mobile Remove-Aktion in Preiszeile integriert; Accessibility-Labels auf Custom-Titel umgestellt.
- `sections/cart-drawer.liquid`: Separate Gesamt-Zeile entfernt; Checkout-Button direkt als HTML gerendert (`.canpan-checkout-btn`) mit Label links und Gesamtpreis (`money_with_currency`) absolut rechtsbündig; Recommended Products mit `size: sm`; `cart-discount` mit expliziter `section`-Übergabe; Payment Icons im Drawer-Footer.
- `sections/main-cart.liquid`: `cart-discount` mit expliziter `section`-Übergabe; stabilere Offer-Gruppenlogik; Accessibility-Labels für Remove-Aktion auf Custom-Titel umgestellt.
- `snippets/horizontal-product.liquid`: Quick-Buy-Icon-Buttons + Custom Element für Cart-Recommendation-Handling.

#### Footer, Popup, Kundenkonto
- `sections/footer.liquid` & `sections/footer-group.json`: Footer auf CANPAN-Copy, -Menüs und Policy-Darstellung angepasst; mobile Copyright/Policy/Cookie-Hinweise erweitert.
- `sections/overlay-group.json`: Overlay-Konfigurationen für Newsletter-Popup, Cart-Drawer, Search-Drawer und Privacy-Banner angepasst.
- `sections/newsletter-popup.liquid`: Formular-Capture-Fix; optimiertes Bild-Loading.
- `sections/main-customers-login.liquid`: Stabileres Recover-Form-Verhalten.
- `sections/main-password.liquid`: Inhaltlich/visuell neu konfiguriert (Newsletter-Flow, Hinweise, vereinfachter Footer).
- `snippets/icon.liquid`: Success- und Lock-Icons auf CANPAN-spezifische Varianten umgestellt.
- `snippets/article-comments.liquid`: Gravatar-Requests entfernt; lokales Initialen-Badge genutzt.
- `snippets/pickup-availability.liquid`: `custom_variant.title`-Metafeld in Pickup-Dialogen verwendet.

#### Lokalisierung, Konfiguration und Templates
- `locales/de.json`: CTA-Texte, Cart-Wording, Newsletter-Copy, Free-Shipping-Texte, Placeholder und Label-Anpassungen.
- `config/settings_schema.json`: Schrift-Defaults auf `assistant_n4` gesetzt.
- `config/settings_data.json`: Komplett auf CANPAN-Branding und Shop-Konfiguration angepasst (Farben, Typografie, soziale Profile, Cart-Schwelle etc.).
- `templates/product.json`: Metafeld-Namespace `custom-shop` → `custom_shop`; Dot-Notation für alle Shop-Metafeld-Referenzen; `socialproof_picture_1/2` → `socialproof_image_1/2`.
- `templates/index.json`: Startseite auf CANPAN-Sections und -Konfiguration umgestellt; Metafeld-Referenz auf Dot-Notation.
- `templates/cart.json`, `templates/collection.json`, `templates/list-collections.json`, `templates/search.json`, `templates/password.json`: Auf CANPAN-Konfiguration und -Sektionen angepasst.

---

### Fixed

- `sections/slideshow.liquid`: LCP/Preload-Optimierungen.
- `sections/newsletter-popup.liquid` & `sections/main-customers-login.liquid`: Variablennamenkonflikte im Form-Capture bereinigt.
- `snippets/product-info.liquid` & `sections/main-cart.liquid`: Blockgruppen-Wrapper-Bugs behoben.
- `sections/cart-drawer.liquid` & `sections/main-cart.liquid`: `cart-discount` erhält jetzt die `section`-Referenz explizit übergeben (verhindert fehlerhaftes Rendering in Drawer-Kontext).
- `assets/canpan-theme.css`: Rechter Scrollbar-Button der `.canpan-featured-slider`-Komponente auf Desktop korrekt positioniert (war am Drawer-Rand abgeschnitten).
- `assets/canpan-theme.css`: Asymmetrischen vertikalen Abstand der Variantenoption im Cart-Drawer auf Desktop behoben (`line-height: 1` und `margin-bottom: 0` nur noch im Mobile-Breakpoint gesetzt).
- Theme-Check/Accessibility-Fixes in Story-Komponente (Placeholder, `width`/`height`, Alt-Handling).

---

### Dependencies

Mehrere neue Features setzen strukturierte Metafields voraus:
- `custom_variant.page_appearance` (Color-Metaobject mit `footer_background_color`, `footer_text_and_icon_color`, `cta_button_background_color`, `cta_button_text_color`, `header_background_color`, `header_text_and_icon_color`)
- `custom_variant.title`
- `custom_variant.little_text`
- `custom_variant.benefits`
- `custom_variant.bubble_division`
- `custom_variant.bubble_comparison_price`
- `custom_shop.featured_partners` (in `sections/footer-group.json`, `templates/index.json`)
- `custom_shop.story_bubbles` (in `templates/page.canny.json`)
- `custom_shop.socialproof_image_1/2`, `custom_shop.socialproof_name_1/2` (in `templates/product.json`)
