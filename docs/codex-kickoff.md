# Encargo inicial para Codex

Eres el ingeniero principal de Investment OS. Lee TODOS los archivos de docs/ y README antes de escribir código. Construye solo F1A (núcleo y pruebas), no todo el roadmap.

Prioridades:
1. Crea monorepo TypeScript con apps/web Next.js y packages/financial-core, packages/data-import y packages/shared.
2. Define migraciones PostgreSQL y políticas RLS para usuario único, sin secretos en frontend.
3. Implementa entidades y contratos de datos en shared, validación con Zod y representación decimal exacta.
4. Implementa el motor de movimientos y ledger por cuenta/divisa; FIFO de posiciones y cálculo de P&L realizado. No implementes aún resultados de CFD sin una especificación validada.
5. Crea fixtures totalmente ficticios y pruebas automáticas para compras, ventas parciales, comisiones, depósitos, retiros, dividendos, FX, split, reimportación, IDs duplicados y datos incompletos.
6. Crea UI mínima con estados vacíos, sin métricas simuladas presentadas como reales.
7. Documenta decisiones en docs/architecture-decisions.md y escribe instrucciones de ejecución local.

Condiciones:
- No conectar a cuentas reales todavía.
- Nunca solicitar ni registrar API keys reales en el código.
- No ejecutar órdenes.
- No inferir campos de CSV no inspeccionados.
- Cada resultado debe tener moneda, periodo y procedencia.
- No proclamar 'rentabilidad total' si faltan operaciones o valoraciones.
- Ejecutar lint, typecheck y tests; resumir qué pasó, qué falta y comandos para reproducirlo.

Criterios de aceptación:
- El mismo movimiento importado dos veces no se contabiliza dos veces.
- Un depósito no genera ganancias.
- Venta parcial con FIFO calcula correctamente lotes restantes.
- Comisiones y FX no desaparecen de los cálculos.
- Los saldos inconsistentes se muestran como pendiente de conciliación, no se corrigen automáticamente.
