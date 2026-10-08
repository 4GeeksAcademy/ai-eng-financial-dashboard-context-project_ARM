# Estado del proyecto

## Implementado según el código

- Frontend de dashboard con tarjetas KPI y gráficos de ingresos/gastos y margen; la pantalla carga `/api/metrics` (`frontend/src/App.tsx`; `frontend/src/components/dashboard/`).
- API FastAPI con endpoint de salud, movimientos y endpoints adicionales de métricas, filtros y segmentos (`backend/app/routes.py`).
- Hay pruebas backend de rutas/filtros (`backend/tests/test_routes.py`) y pruebas frontend de utilidades financieras (`frontend/src/lib/financial-utils.test.ts`). La existencia de pruebas no implica que todas las rutas o cálculos estén completamente cubiertos.
- Documentación de arranque y configuración Docker está en `README.md`, `README.es.md` y `docker-compose.yml`.

## Estado de validación conocido

No consta en esta sesión una ejecución satisfactoria de las suites. El usuario informó que `npm test` falló con `vitest: not found` y que `npm ci` no pudo crear `frontend/node_modules/@babel` por un error de permisos. Esos reportes describen el estado de instalación comunicado en la conversación, no un resultado de tests del código. No se afirma que las pruebas pasen ni que Docker haya sido ejecutado.

## Deuda o discrepancias observables

- La cabecera fija `2024 - Full Year` contrasta con las fechas relativas a `date.today()` del generador backend (`frontend/src/App.tsx`; `backend/app/routes.py`).
- `frontend/src/lib/mock-data.ts` no aparece usado por el flujo principal, que obtiene movimientos desde la API (`frontend/src/App.tsx`).
- El generador llama a `random.seed(seed)` del módulo global (`backend/app/routes.py`).
- CORS está configurado con `allow_origins=["*"]` y `allow_credentials=True` (`backend/app/main.py`).
- Algunas pruebas backend de resumen/alertas comprueban forma o propiedades generales, en vez de fijar resultados numéricos; véanse `backend/tests/test_routes.py` y el detalle de `findings.md` (TST-01).
- No se ve configuración de base de datos en Compose ni integración de persistencia en los archivos inspeccionados (`docker-compose.yml`; `backend/requirements.txt`; `backend/app/routes.py`).

## Prioridades técnicas posibles (no comprometidas)

Como siguientes comprobaciones opcionales, se podría resolver primero el bloqueo local de instalación para poder ejecutar las pruebas; después, verificar numéricamente las métricas afectadas por cambios y revisar la correspondencia entre periodo mostrado y rango de datos. Son propuestas derivadas de los puntos anteriores, no un roadmap aprobado ni una promesa de trabajo.