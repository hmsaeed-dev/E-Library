# 📚 Data Schema & Bibliographic Catalog

This document details the data architecture, in-memory caching model, JSON record schemas, and the 7 thematic taxonomies of the **Classical E-Library**.

---

## 1. In-Memory Caching & $O(1)$ Lookup Map (`core/data.js`)

Rather than pinging an SQL database or executing redundant network fetches on every navigation event, the data layer ingests [`assets/data/books.json`](../assets/data/books.json) once and constructs two memory structures:

```javascript
let cachedBooks = null;        // Array for sequence iteration & filter operations
const booksMap = new Map();     // O(1) Key-Value lookup indexed by book ID
```

### Performance Characteristics
1. **$O(1)$ Constant-Time Record Resolution:** When a reader clicks a book to view details or trigger a Quick Peek modal, `getBookById(id)` queries `booksMap.get(id)` in $O(1)$ time, delivering zero-latency UI rendering without array traversal.
2. **Zero-Latency In-Memory Search:** Title, author, and genre search queries execute synchronously against the local in-memory array, providing instant keystroke response with no server lag or API rate limits.

---

## 2. Bibliographic Corpus & Taxonomies

The catalog comprises **145 curated volumes** organized into 7 distinct thematic categories representing classical Islamic civilization, philosophy, scientific treatises, and foundational literature:

| Taxonomic Category | Volume Count | Curated Domain & Representative Texts |
| :--- | :---: | :--- |
| **Life & Values** | 28 | Classical ethics, Allama Iqbal's philosophical poetry, introspective moral treatises |
| **History & Civilizations** | 24 | Ibn Khaldun's *Muqaddimah*, Islamic architectural developments, regional histories |
| **Philosophy & Non-Fiction** | 22 | Epistemology, dialectical logic, classical Arabic syntax commentaries |
| **Science & Natural History** | 20 | Foundations of physics, cosmology, optical treatises, biological adaptations |
| **Technology & Computation** | 18 | History of algorithmic computation, discrete logic, mathematical foundations |
| **Literature & Fiction** | 18 | Regional prose, classical allegorical narratives, translated world literature |
| **Nature & Field Studies** | 15 | Observational biology, wilderness accounts, macro perspectives on nature |

---

## 3. JSON Record Schema (`books.json`)

Every volume in [`assets/data/books.json`](../assets/data/books.json) is structured according to a strict, normalized bibliographic schema:

```json
{
  "id": "book-muqaddimah-ibn-khaldun",
  "title": "The Muqaddimah: An Introduction to History",
  "author": "Ibn Khaldun",
  "category": "History & Civilizations",
  "language": "English / Arabic",
  "year": 1377,
  "pages": 492,
  "rating": 4.9,
  "cover": "assets/img/books/covers/muqaddimah.jpg",
  "pdf": "assets/pdfs/muqaddimah.pdf",
  "description": "A pioneering historical and sociological treatise establishing cyclical dynamics of civilization, social cohesion (Asabiyyah), and economic sociology.",
  "featured": true,
  "tags": ["historiography", "philosophy of history", "sociology", "classical"]
}
```

### Attribute Specifications
* `id` *(String)*: Unique URL-safe slug used for deep-linking (`pages/book-details.html?id=...`).
* `category` *(String)*: Binds to the primary filter rail in the catalog view.
* `cover` *(String)*: Relative image path to the compressed front cover asset.
* `pdf` *(String)*: Direct reference to the locally cached document or reader target.
* `tags` *(Array)*: Multi-vector taxonomy for secondary freeform keyword filtering.

---

## 4. Ingestion Infrastructure & Scraping Queues

The `assets/data/` directory also houses the tooling and ingestion queues used during catalog curation:
* **`download_queue.json` & `queue.json`:** Batch queues that pair international standard book numbers (ISBNs) with automated cover-art fetching routines.
* **`AAll Books Data.csv` & `E_Library Database.xlsx`:** Source metadata tables maintaining publisher records, edition years, and file size metrics.
