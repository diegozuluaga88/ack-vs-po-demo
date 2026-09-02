# ack-vs-po-demo · Demo template · clon de expert-hub

**Contexto**: fork paralelo de `expert-hub` (base `1f58b0e` · 2026-08-13) para demo genérico enfocado en Ack↔PO comparisons. Nombre original `demo-expert-1` · renombrado a `ack-vs-po-demo` el 2026-09-02. Adaptaciones marcadas con prefijo histórico `DE1.*` (no renombrado para preservar trazabilidad). Ver README.md para detalles.

**Regla dura**: no editar código en `src/components/comparison/*` ni el `ComparisonReviewModal` · fuente de verdad = expert-hub.

---

# Strata Design System — Reglas para este proyecto

Antes de crear o modificar cualquier componente, consultar el MCP server `strata-ds`:

```
get_overview          → contexto completo (usar al iniciar trabajo nuevo)
get_laws              → leyes absolutas del DS
get_tokens            → referencia de tokens CSS/Tailwind
get_rules(category)   → reglas: color-tokens | brand-colors | containers-and-cards | buttons-and-actions | icons
get_anti_patterns     → errores documentados a evitar
search_governance(q)  → búsqueda en toda la governance
```

Ver instrucciones completas en: `c:/Users/User/Documents/design-system/CLAUDE.md`
