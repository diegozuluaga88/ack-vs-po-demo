# ack-vs-po-demo

Demo template genérico (reutilizable en pitches) · clonado físicamente de `expert-hub` y adaptado para mostrar el flow de **Acknowledgements vs Purchase Orders comparisons** con una regla dura:

> Si un ACK no tiene PO relacionado, se oculta completamente del listado de Comparisons (no aparece, no se puede comparar).

**Base**: `expert-hub@1f58b0e` · 2026-08-13 · `https://expert-hub-seven.vercel.app/` (deploy de expert-hub original).
**Clonado**: 2026-09-01 (nombre original `demo-expert-1` · renombrado a `ack-vs-po-demo` el 2026-09-02).

## Diferencias vs `expert-hub` original

Todas las adaptaciones llevan comentario prefijo `DE1.*` para trazabilidad (el prefijo se preserva histórico · no se renombró junto con el proyecto):

| ID | Adaptación | Archivo |
|---|---|---|
| DE1.0 | Rename package + port 8085 → **8089** + provenance | `package.json` · `vite.config.ts` · `README.md` |
| DE1.1 | Navbar names genéricos (tenant "Dealer 1" · user "Expert 1") | `src/components/Navbar.tsx` · `src/TenantContext.tsx` · `src/context/AuthContext.tsx` |
| DE1.3 | Filtro "ACK sin PO oculto" + 2 mocks huérfanos para probar | `src/Comparisons.tsx` |
| DE1.4 | Comparisons + Transactions default view mode `list` | `src/Comparisons.tsx` · `src/Transactions.tsx` |
| DE1.5 | Tab Transactions oculto (align con premain gostrata.app) | `src/components/Navbar.tsx` |
| DE1.7 | Breadcrumb movido debajo del navbar (era fixed encima) | `src/OCRTracking.tsx` · `src/Comparisons.tsx` |
| DE1.8 | OCR toolbar · pills "Last 30 days" (default) + "Full history" | `src/OCRTracking.tsx` |
| DE1.9 | Rename a `ack-vs-po-demo` · title HTML "Ack vs PO" · favicon Strata | `package.json` · `README.md` · `CLAUDE.md` · `index.html` · `public/favicon.svg` |
| DE1.10 | Pill "Live updates paused" en toolbar OCR (visual-only) · happy path de Create Record ahora abre `PublishedView` standalone (era solo toast) para paridad con gostrata.app premain | `src/OCRTracking.tsx` (import + state + handler + dialog) |
| DE1.11 | Paridad columnas + navbar prod · tabs renombrados 1:1 (Processing · To Review · In Review · Ready to Sync · Completed · Failed) · consolida identified+capturing en Processing · kanban usa `column.statuses` union · pill navbar `OCR Tracking`→`OCR` · chip Live updates paused refinado a ámbar + pill-shape + condicional `in_review > 0` · reubicado al bloque ml-auto | `src/OCRTracking.tsx` · `src/components/Navbar.tsx` |
| DE1.12 | Removido botón "Mark as Completed" (kanban card + list view) · no existe en prod. Handler + import + prop del componente eliminados. Chip Live updates paused sin `bg-background` (fondo transparente para hermanar con toolbar) | `src/OCRTracking.tsx` · `src/components/ocr/OcrDocCard.tsx` |
| DE1.13 | Section title H1 del card `OCR Tracking`→`Expert Hub` (paridad con gostrata.app premain · breadcrumb conserva "Expert Hub > OCR Tracking") | `src/OCRTracking.tsx` |
| DE1.14 | Botón Preflight Sync ahora también visible en cards con status `in_progress` (In Review) · antes solo en `processed` (Ready to Sync) · paridad con prod donde el plane aparece en ambos | `src/components/ocr/OcrDocCard.tsx` · `src/OCRTracking.tsx` |
| DE1.15 | Rectificación DE1.14 · el Preflight Sync en In Review va DESHABILITADO (span con `cursor-not-allowed opacity-70` + tooltip "Awaiting full review") · funcional solo en Ready to Sync (processed) · match prod donde el plane en in_progress se ve lighter con ese hint | `src/components/ocr/OcrDocCard.tsx` · `src/OCRTracking.tsx` |
| DE1.16 | Orden de tabs del navbar sincronizado con prod: `Feedback → OCR → Comparisons` (antes `OCR → Comparisons → Feedback`) · el chat bubble ahora aparece a la izquierda del pill OCR como en gostrata.app premain | `src/components/Navbar.tsx` |

Todo lo demás viene tal cual de `expert-hub@1f58b0e`.

## Stack

React 19 · Vite 7 · Tailwind 3 · TypeScript 5 · Headless UI · Framer Motion · Lucide · recharts · html2canvas · jspdf · workspace local `strata-design-system` (`packages/strata-ds`).

## Scripts

```bash
npm install         # instala + linkea workspace strata-ds
npm run dev         # dev server en http://localhost:8089
npm run build       # scan security + build strata-ds + vite build
npm run scan:security
npm run lint
```

## Sync policy

**No editar el modal `ComparisonReviewModal` ni sus dependencias en `src/components/comparison/*`.** Fuente de verdad = expert-hub. Este proyecto es fork paralelo · si evoluciona expert-hub, re-sync manual con conciencia de las adaptaciones `DE1.*`.
