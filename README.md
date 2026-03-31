# Elephantronics Docs — Developer Guide

## Local development

```bash
# 1. Clone the repo
git clone https://github.com/elephantronics/docs
cd docs

# 2. Install dependencies (Python 3.8+)
pip install -r requirements.txt

# 3. Run live dev server
mkdocs serve
# → opens at http://127.0.0.1:8000
# → auto-reloads on every .md save
```

---

## ➕ Adding a new product (5-minute workflow)

### Step 1 — Create the product page

Copy the template:
```bash
cp docs/_TEMPLATE_new-product.md docs/[category]/[product-slug].md
```

Category folders:
```
docs/solar/
docs/automation/
docs/smart-home/
docs/sbcs-mini-pcs/
```

Edit the new file — replace all `[PLACEHOLDERS]` with real content.

---

### Step 2 — Add to navigation (mkdocs.yml)

Open `mkdocs.yml` and find the right category under `nav:`. Add your product:

```yaml
nav:
  - "☀️ Solar Systems":
    - Overview: solar/index.md
    - Products:
      - SolarEdge Pro 5K: solar/solaredge-pro-5k.md
      - SunPower Elite 8K: solar/sunpower-elite-8k.md
      - GridTie Nano 3K: solar/gridtie-nano-3k.md
      - Your New Product: solar/your-new-product.md    # ← ADD HERE
```

---

### Step 3 — Add a product card to the category index

Open `docs/[category]/index.md` and add a new card inside `<div class="product-grid">`:

```html
<a href="your-new-product/" class="product-card">
  <div class="prod-label">Product Category</div>
  <div class="prod-name">Your Product Name</div>
  <div class="prod-tagline">One sentence description of what it does and who it's for.</div>
  <div class="prod-specs">
    <span class="prod-spec-tag">Key Spec 1</span>
    <span class="prod-spec-tag">Key Spec 2</span>
    <span class="prod-spec-tag">Key Spec 3</span>
  </div>
  <div class="prod-arrow">View documentation →</div>
</a>
```

---

### Step 4 — Preview and push

```bash
mkdocs serve        # preview at localhost:8000
git add .
git commit -m "docs: add [Product Name] documentation"
git push origin main
# → GitHub Actions deploys automatically to docs.elephantronics.com
```

---

## ➕ Adding a new category

1. Create a new folder: `docs/[new-category]/`
2. Create `docs/[new-category]/index.md` — copy an existing category index as your template
3. Add the category to `mkdocs.yml` nav with `- Overview:` and `- Products:` sub-sections
4. Add a new category card to `docs/index.md` inside `<div class="category-grid">`

---

## Page structure conventions

Every product page should follow this order:

```
# Product Name
[badges]
> [one-paragraph product hook]
---
## Quick Start         ← always first, gets user to success fastest
## Technical Specs     ← full specs table
## [Setup Section]     ← wiring / installation / OS setup
## [Config Section]    ← configuration, modes, settings
## [Advanced]          ← optional advanced features
## Troubleshooting     ← always last
```

## Markdown tips

```markdown
!!! tip "Title"         → green tip box
!!! warning "Title"     → yellow warning box  
!!! danger "Title"      → red danger box
!!! note "Title"        → blue note box

=== "Tab A"             → tabbed content
=== "Tab B"

```bash                  → syntax-highlighted code block with copy button
code here
` ``
```

---

## File naming convention

Use lowercase kebab-case for all files:

```
✅  solaredge-pro-5k.md
✅  hmi-panel-10.md
✅  zigbee-relay-16ch.md
❌  SolarEdgePro5K.md
❌  hmi panel 10.md
```
