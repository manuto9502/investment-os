# Arquitectura técnica v1.0

## Stack objetivo
- Next.js + TypeScript, Tailwind CSS, shadcn/ui.
- PostgreSQL gestionado por Supabase (Auth, RLS, Storage privado); migraciones versionadas.
- Motor financiero como paquete TypeScript puro y determinista; Python solo para investigación/estadística posterior.
- Tests unitarios e integración con Vitest; Playwright para flujos críticos.
- Zod para contratos y validación CSV/XLSX; importación realizada en servidor.
- Job runner / cola opcional en fase posterior.

## Esquema de flujo
CSV/XLSX -> Upload privado -> parser específico de bróker -> previsualización ->
validación semántica -> staging -> mapeo a movimientos canónicos ->
deduplicación -> confirmación -> ledger -> posiciones/P&L -> panel + análisis.

## Seguridad
- Nunca exponer service-role key, bróker secrets o archivos privados al cliente.
- Autenticación, RLS por user_id y comprobación server-side en cada operación.
- Tipos decimales exactos para cantidades y dinero; nunca floats JS para liquidaciones.
- Retención/borrado de archivos configurables, historial de imports y correcciones auditables.
- No guardar contraseñas de bróker. API externa solo lectura si se valida acceso.
- Datos ficticios exclusivamente en pruebas y ejemplos; no subir extractos reales a Git.

## Integraciones previstas
- Revolut: inicialmente extractos de inversión oficiales; comprobar formato real antes del parser definitivo.
- eToro: inicialmente extractos CSV/XLSX; API oficial opcional una vez verificados acceso y condiciones de uso para cuenta personal.
- TradingView: gráficos/alertas webhook en fase posterior; recepción autenticada, idempotente y con registro de errores. No asumir un feed de cotizaciones de TradingView.
- Precios/FX: proveedor independiente con timestamps, licencia, moneda y etiquetas delayed/realtime.

## Decisiones financieras
- Libro de movimientos inmutable; cualquier corrección se registra como ajuste/reverso.
- Identidad de activo por identificador del instrumento + fuente/mercado; ticker NO es clave única.
- FIFO para resultados realizados como criterio de análisis inicial, parametrizable y no declaración fiscal.
- Las transferencias internas no son retornos.
- Base EUR con conservación íntegra de importes en divisa de origen.
- No consolidar CFDs con acciones como si fueran posiciones equivalentes.
