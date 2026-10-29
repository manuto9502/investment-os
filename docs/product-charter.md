# Product Charter — Investment OS v1.0
Fecha: 2026-10-28 | Estado: propuesta para validar

## Visión
Crear una plataforma web privada para consolidar inversiones de eToro y Revolut, analizar resultados de forma auditable, registrar decisiones y descubrir patrones estadísticos de comportamiento; incorporar posteriormente señales de TradingView.

## Usuario y ámbitos
Un único usuario. Dos libros analíticos separados: inversión de medio/largo plazo y trading/CFDs. Una vista de patrimonio consolidado los reúne sin confundir riesgo y resultados.

## Preguntas que debe responder
1. ¿Cuánto capital he aportado, retirado y ganado realmente?
2. ¿Qué tengo abierto, con qué exposición a divisas y riesgo?
3. ¿Qué activos, horizontes y estrategias generan resultados netos?
4. ¿Qué desviaciones hay entre mi plan previo y la ejecución?
5. ¿Qué patrones sobreviven al control de tamaño de muestra y costes?

## MVP IN
- Autenticación para un usuario y aislamiento de datos.
- Cuentas: eToro, Revolut; subcuentas y separación entre investing y CFD.
- Ingestión de CSV/XLSX con vista previa, mapeo, errores por fila y reimportación sin duplicados.
- Archivo fuente con checksum y registro de procedencia.
- Modelo canónico de movimientos: compras, ventas, comisiones, dividendos, retenciones, depósitos, retiradas, conversiones FX, intereses, ajustes, splits; CFD soportado por esquema, cálculo exacto sujeto a extractos.
- Ledger de caja por moneda y posiciones por instrumento/cuenta.
- P&L realizado/no realizado cuando existan datos de coste y precios fiables; TWR/MWR solo si hay flujos y valoraciones suficientes, con indicadores de cobertura.
- Historial y exportación de operaciones canónicas; dashboard de control y conciliación.
- Etiquetado manual de tesis, horizonte, estrategia, nivel de riesgo, motivos y emociones autodeclaradas.

## MVP OUT
- Ejecución de órdenes, asesoramiento automático de compraventa, IA predictiva.
- Sincronización garantizada o precios real-time sin comprobar API, permisos, licencia y presupuesto.
- Impuestos oficiales o certificación fiscal; datos orientativos.
- Apps nativas móviles, soporte multiusuario, cripto on-chain automático.
- Backtesting operativo o diagnóstico psicológico a partir de precios solamente.

## KPI de producto
- 100% de las filas clasificadas como importadas, duplicadas, rechazadas o pendientes de revisión.
- 0 duplicados tras importar el mismo archivo dos veces.
- Diferencias de caja/posiciones visibles en conciliación, sin ajustes ocultos.
- 100% de resultados con moneda, periodo y cobertura de datos.
- Cualquier patrón de conducta indica tamaño de muestra, incertidumbre y criterios de cálculo.

## Principios de diseño
Minimalismo editorial y modo oscuro opcional; accesible, responsive, datos primarios claros; avisos cuando los precios están retrasados o faltan datos.

## Riesgos y mitigación
- Extractos incompletos: permitir saldos de apertura explícitos, nunca inventarlos.
- Cuentas mezcladas / divisas: ledger por cuenta y moneda; tipos de cambio con fecha y fuente.
- CFDs: modelar operaciones, financiación nocturna, spreads, leverage y margin por separado.
- Licencias y APIs: adaptadores intercambiables y feature flags.
- Seguridad: permisos mínimos, cifrado, sesiones seguras, RLS, auditoría, pruebas y backups.
