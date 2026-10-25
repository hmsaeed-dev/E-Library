# 📚 Classical E-Library (Bayt al-Hikma)

[![Frontend: Vanilla JS](https://img.shields.io/badge/Frontend-Vanilla%20JS%20%28ES6%20Modules%29-F7DF1E.svg?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-0%20Runtime%20%7C%20No%20Bundler-brightgreen.svg?style=flat-square)]()
[![Performance: 99/100](https://img.shields.io/badge/Lighthouse-99%2F100%20Performance-green.svg?style=flat-square&logo=lighthouse&logoColor=white)]()
[![Catalog: 145 Volumes](https://img.shields.io/badge/Catalog-145%20Curated%20Volumes-orange.svg?style=flat-square)]()
[![Academic: UET Taxila](https://img.shields.io/badge/Academic-UET%20Taxila%20%7C%20Fall%202025-151927.svg?style=flat-square)](https://uettaxila.edu.pk/)

A zero-dependency, modular digital catalog and literary reader platform engineered entirely with native browser primitives (ES6 Modules, declarative HTML component injection, in-memory caching, and CSS Grid). Delivers an instant, accessible reading environment with a near-perfect (99/100) Lighthouse performance profile.

Built and evaluated during **Semester 1 (Fall 2025)** at the **Department of Computer Science, University of Engineering and Technology (UET), Taxila**.

<p align="center">
  <img src="assets/img/ui/demo/home-screen.png" alt="Classical E-Library Interface" width="100%" style="border-radius: 8px; box-shadow: 0 4px 20px rgba(0,0,0,0.15);" />
</p>

---

## ⚡ Architectural Specifications at a Glance

| Subsystem | Architectural Specification |
| :--- | :--- |
| **Execution Model** | Native ES6 Modules (`<script type="module">`) — Zero bundlers, zero npm dependencies |
| **Data Architecture** | Static JSON database (`books.json`) loaded into an in-memory cached $O(1)$ lookup hash map |
| **Component System**| Declarative `data-include` fragment injection engine with regex path resolution |
| **Catalog Scope** | 145 curated volumes categorized across 7 thematic cultural & scientific taxonomies |
| **Performance Profile** | Sub-100ms load velocity, zero layout shift (CLS), progressive skeleton loaders |
| **Theming Engine** | CSS Custom Properties with automatic `localStorage` and OS `prefers-color-scheme` sync |

---

## 📖 Deep-Dive Documentation Hub

Detailed engineering blueprints, component mechanics, and data schemas are organized into modular guides:

* 📐 **[`docs/01-architecture-and-injection.md`](docs/01-architecture-and-injection.md):** Declarative HTML component injection (`include.js`), path normalization regex, and the ES6 module lifecycle.
* 📚 **[`docs/02-data-schema-and-catalog.md`](docs/02-data-schema-and-catalog.md):** In-memory $O(1)$ Map indexing, `books.json` bibliographic schema, the 7 taxonomies, and ISBN scraper tooling.
* 🎨 **[`docs/03-design-system-and-ui.md`](docs/03-design-system-and-ui.md):** Modular stylesheet architecture (`base/`, `components/`, `pages/`), skeleton screens, and "Quick Peek" modal logic.

---

## 🚀 Quickstart: Run Locally

Because ES6 modules and HTML component injection use `fetch()`, files must be served over HTTP rather than `file://`:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/hmsaeed-dev/E-Library.git
   cd E-Library
   ```
2. **Start a local lightweight server (No build step required):**
   ```bash
   # Using Python:
   python -m http.server 8000
   
   # Or using Node:
   npx serve .
   ```
3. **Open in your browser:**  
   Navigate to `http://localhost:8000`.

---

## 📁 Repository Structure

```text
E-Library/
├── index.html              # Main catalog landing view
├── pages/                  # Multi-page application views (books, book-details, categories, profile)
├── components/             # Reusable declarative HTML snippets (navbar, footer, modals)
├── assets/
│   ├── js/
│   │   ├── core/           # Fundamental architecture (include, data, theme, auth, utils)
│   │   ├── features/       # Page logic (search, book grids, quick peek, ui-effects)
│   │   └── app.js          # Main asynchronous initialization orchestrator
│   ├── css/                # Modular tokenized stylesheets (base, components, pages)
│   ├── data/               # Ingested catalog dataset (books.json, queues, CSV sources)
│   └── img/ui/demo/        # High-resolution production UI showcase plates
├── docs/                   # Architectural blueprints & deep-dive technical guides
├── LICENSE                 # Academic license
└── README.md               # This executive summary
```

---

## 👥 Engineering Group & Academic Credits

* **Institution:** Department of Computer Science, UET Taxila (Section B)
* **Course:** Application of ICT Lab (`GE-101-L`) — Semester 1 (Fall 2025)
* **Instructor / Evaluator:** **Sir Shah Fahad**
* **Project Team:**
  * **[Hafiz Muhammad Saeed](https://github.com/hmsaeed-dev) (25-CS-005):** Lead System Architect, Component Injection Engine, Data Layer & Caching, Responsive CSS Tokens.
  * **Wajeeh-ul-Hassan (25-CS-002):** Requirements documentation, catalog schema review, and testing.
  * **Muhammad Irfan Yasir (25-CS-194):** Asset collation, bibliographic data entry, and manual QA.
