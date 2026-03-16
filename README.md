# Shopify Theme: Landing Page Assessment

A metafield-driven Shopify landing page built with Liquid sections, responsive on desktop and mobile.

---

## Sections

| File | Section |
|---|---|
| `sections/navbar.liquid` | Navigation bar |
| `sections/hero.liquid` | Hero / Intro |
| `sections/how_it_works.liquid` | How It Works |
| `sections/why_love_us.liquid` | Why You'll Love Us |
| `sections/faqs.liquid` | FAQs |

---

## Metafields Reference

### Navbar (`sections/navbar.liquid`)

The navbar reads links dynamically from the store's `main-menu` link list. If the menu is empty or not configured, it falls back to 4 hardcoded items matching the design reference:

| Fallback label |
|---|
| Log In |
| Our Menus |
| How to Heat |
| About us |

To manage the menu links go to **Online Store → Navigation → Main menu**.

---

### Hero (`sections/hero.liquid`)

| Key | Type | Description | Fallback |
|---|---|---|---|
| `hero_title` | Single line text | Main heading | `'Our product is the best products'` |
| `hero_description` | Single line text | Subheading / description | `'We deliver fast, secure and free...'` |
| `hero_button_label` | Single line text | CTA button label | `'Get Dinner Sorted'` |
| `hero_button_link` | URL | CTA button link | `'#'` |
| `hero_social_proof` | Single line text | Trust line below CTA | `"Trusted by 1000's of Londoners weekly"` |
| `hero_image_desktop` | File (image) | Hero image on desktop | `hero.webp` from Assets |
| `hero_image_mobile` | File (image) | Hero image on mobile | `hero-mobile.webp` from Assets |

### How It Works (`sections/how_it_works.liquid`)

| Key | Type | Description | Fallback |
|---|---|---|---|
| `how_it_works_title` | Single line text | Section title | `'How it works'` |
| `how_it_works_cta_label` | Single line text | CTA button label | `'Get Dinner Sorted'` |
| `how_it_works_cta_link` | URL | CTA button link | `'#'` |
| `how_it_works_steps` | List of metaobjects | Up to 4 step cards | 4 hardcoded fallback steps |

#### Metaobject definition — `how_it_works_step`

| Field | Type | Description |
|---|---|---|
| `step_number` | Single line text | Step number (e.g. `1`) |
| `title` | Single line text | Step title |
| `subtitle` | Multi-line text | Step description |
| `icon_image` | File (image) | Step icon |

### Why You'll Love Us (`sections/why_love_us.liquid`)

| Key | Type | Description | Fallback |
|---|---|---|---|
| `why_love_us_title` | Single line text | Section title | `"Why you'll love us"` |
| `why_love_us_cta_label` | Single line text | CTA button label | `'Get Dinner Sorted'` |
| `why_love_us_cta_link` | URL | CTA button link | `'#'` |
| `why_love_us_image` | File (image) | Right-column image | `why-love-us-image.webp` from Assets |
| `why_love_us_items` | List of metaobjects | Up to 4 benefit items | 4 hardcoded fallback items |

#### Metaobject definition — `why_love_us_item`

| Field | Type | Description |
|---|---|---|
| `title` | Single line text | Benefit title |
| `subtitle` | Multi-line text | Benefit description |
| `icon_image` | File (image) | Benefit icon |

### FAQs (`sections/faqs.liquid`)

| Key | Type | Description | Fallback |
|---|---|---|---|
| `faq_title` | Single line text | Section title | `'FAQs'` |
| `faq_items` | List of metaobjects | Accordion items | 5 hardcoded fallback FAQs |

#### Metaobject definition — `faq_item`

| Field | Type | Description |
|---|---|---|
| `question` | Single line text | FAQ question |
| `answer` | Multi-line text | FAQ answer |

---

## How to Create the Metafields

### 1. Create Metaobject Definitions

Go to **Settings → Custom data → Metaobjects → Add definition** and create the following:

- `how_it_works_step` — fields: `step_number`, `title`, `subtitle`, `icon_image`
- `why_love_us_item` — fields: `title`, `subtitle`, `icon_image`
- `faq_item` — fields: `question`, `answer`

### 2. Create Metafield Definitions

Go to **Settings → Custom data → Pages → Add definition** and add the keys listed above with their respective types.

### 3. Populate Metafields

Go to **Content → Pages → [your page]**, scroll to the **Metafields** section at the bottom, and fill in the values.

---

## Fallback Strategy

All sections include clean fallbacks at two levels:

1. **Text fields** — use Liquid `| default:` to fall back to strings
2. **Images** — check `metafield.value != blank`, if empty, fall back to local assets served via `asset_url`
3. **Metaobject lists** — if the list is empty or not set, render hardcoded HTML content matching the design reference

This ensures every section renders correctly, even before any metafields are configured.

---

## Assets Required

Upload the following files to **Online Store → Themes → Assets**:

> All asset files are available in the `assets/` folder of this repository.

```
hero.webp
hero-mobile.webp
how-it-works-calendar.webp
how-it-works-deliver.webp
how-it-works-microwave.webp
how-it-works-heart.webp
why-love-us-dish-heart.webp
why-love-us-serving-dish.webp
why-love-us-dish-fork.webp
why-love-us-smile.webp
why-love-us-image.webp
logo.webp
```
---

## Theme Check

Validated with `shopify theme check`. Result: **0 errors, 3 warnings**.

The 3 warnings are all `RemoteAsset` on `layout/theme.liquid` and are intentional:

- **Google Fonts** — cannot be served from the Shopify CDN
