# Roadmap y puertas de aceptación

## F0 — Especificación y validación de fuentes
- [x] Carta de producto y prioridades.
- [x] Arquitectura conceptual.
- [x] Modelo canónico inicial.
- [ ] Obtener extracto anonimizado de Revolut y eToro, con varias transacciones representativas.
- [ ] Inventariar campos, tipos de operaciones y casos especiales.
- [ ] Confirmar disponibilidad de API de eToro en cuenta propia.
Puerta: mapa de ambos archivos a movimientos sin campos críticos ambiguos.

## F1A — Núcleo y pruebas
- [ ] Repositorio, estructura y entorno local.
- [ ] Esquema SQL, auth, RLS y tests.
- [ ] Ledger determinista y posiciones con pruebas de referencia.
Puerta: pasan los 10 escenarios del modelo de datos.

## F1B — Ingestión y dashboard
- [ ] Carga privada, vista previa, mapeo y errores.
- [ ] Deduplicación e historial de importaciones.
- [ ] Conciliación y vistas patrimonio / movimientos / posiciones.
Puerta: extracto real importado dos veces sin duplicados; diferencias visibles; resultados contrastados manualmente.

## F2 — Trading
- [ ] Diario de operaciones y captura de contexto.
- [ ] Charts; alertas TradingView opcionales.
- [ ] Estadísticas por instrumento, estrategia, periodo.
Puerta: cada estadística documentada y recalculable.

## F3 — Behavioral analytics
- [ ] Patrones predefinidos y contrastes.
- [ ] Control de sesgos, tamaño de muestra y costes.
- [ ] Informes comparativos y revisión de decisiones.
Puerta: no se presentan hipótesis como causalidades ni diagnósticos.

## F4 — Sincronización
- [ ] API eToro solo lectura si permitida.
- [ ] Feeds de mercado y FX conforme a licencias.
- [ ] Monitoreo de fallos, trazabilidad y backfills.
Puerta: sincronización idempotente con reconciliación y alertas de errores.
