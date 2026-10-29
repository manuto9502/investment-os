# Modelo de datos canónico v1.0

## Entidades mínimas
- users(id)
- institutions(id, code, name)
- accounts(id, user_id, institution_id, external_ref_hash, type, base_currency)
- instruments(id, isin, symbol, venue, asset_class, quote_currency, name)
- import_files(id, account_id, sha256, name, uploaded_at, parser_version, status, storage_path)
- import_rows(id, import_file_id, row_number, source_row_hash, raw_payload, parse_status, error_code)
- transactions(id, account_id, instrument_id?, source_transaction_id?, type, occurred_at, settled_at?, source_currency, quantity?, unit_price?, gross_amount?, fees?, taxes?, net_cash_amount?, notes?, import_row_id?, dedupe_key)
- cash_ledger(id, account_id, transaction_id, currency, signed_amount, effect_type)
- lots(id, account_id, instrument_id, opened_transaction_id, original_qty, remaining_qty, cost_basis_currency, cost_basis_amount)
- lot_closures(id, opening_lot_id, closing_transaction_id, qty, assigned_cost, proceeds, realized_pnl)
- valuations(id, account_id?, instrument_id?, observed_at, price, currency, provider, is_realtime)
- fx_rates(id, base_currency, quote_currency, observed_at, rate, provider)
- decisions(id, user_id, account_id?, instrument_id?, transaction_id?, created_at, strategy, thesis, entry_reason, invalidation, planned_risk, emotional_state, notes)
- reconciliation_runs(id, account_id, run_at, status, discrepancy_summary)
- audit_events(id, user_id, entity_type, entity_id, operation, created_at, change_json)

## Contrato de transacción
- Fechas siempre UTC con timezone original preservado si se conoce.
- Cantidades y dinero en DECIMAL con precisión adecuada, no float.
- Venta: quantity positivo en datos canónicos; direction/type determina el signo del efecto.
- Gross / fees / taxes / cash impact nunca se mezclan.
- Faltantes permanecen NULL; nunca convertir falta de comisiones en cero por defecto.
- Un dividendo no se trata como venta; FX como dos patas enlazadas.
- Una importación se identifica por archivo + fila y por clave de negocio cuando exista.
- Fuente de cada dato y transformaciones trazables a la fila original.

## Casos de prueba obligatorios
1. Compra simple, venta completa con comisión.
2. Dos compras + venta parcial, FIFO y posición remanente.
3. Compras USD y presentación EUR con FX histórico.
4. Depósito, retiro y transferencia interna sin P&L artificial.
5. Dividendo con retención y ajuste de efectivo.
6. Importar dos veces el mismo CSV sin duplicar movimientos.
7. Fecha/ticker iguales pero dos órdenes legítimas distintas.
8. Split de acciones sin crear beneficio ficticio.
9. CFD largo/corto, apalancamiento y costes de financiación: verificar reglas con muestra real antes de declarar exactitud.
10. Extracto incompleto y saldo de apertura: error visible y reconciliación pendiente.
