# ARCHITECTURE.md — openclaw-mem

Dos pequeñas apps Flask (panel de memoria y historial de conversaciones) sobre la base SQLite de memoria persistente de OpenClaw. **OpenClaw se retiró el 2026-09-16.**

## Clientes y versiones
- Dos clientes web locales: `web_app.py` (panel de observaciones con búsqueda y filtros) y `history_app.py` (historial de mensajes por canal). Sin iOS ni API pública. Scripts `install.sh`, `start.sh`, `stop.sh`, `uninstall.sh`, `test.sh`, `setup.py`.
- No es un MCP ni tiene ruta en AgentGateway.
- Versión: sin etiquetas.

## Dependencias en ambos sentidos
- **Depende de:** la base SQLite `~/.openclaw-mem/memory.db` que escribía OpenClaw y de Flask.
- **Quién depende de él:** nadie por manifiesto. La memoria de la compañía vive hoy en el brain (`/brain`), no aquí.
- Sin `CONTRACTS.yaml`.

## Stack
- Python 3.10+, Flask, SQLite. `requirements.txt` declara `mcp>=1.0.0` y `httpx>=0.27.0`, **no Flask**: el README pide `pip install flask` aparte.

## Componentes compartidos
- Ninguno.

## Cómo se construye
- Cada app es un fichero único con sus consultas SQL; el arranque lo hace `start.sh`.

## Tests
- `test.sh`; no hay suite de tests unitarios en el repo.

## CI/CD y despliegue
- Sin workflows, sin imagen, sin ArgoCD. Se ejecuta en un Mac (el README usa `/Users/usuario/openclaw-mem`). Tronco: `main`.

## Decisiones y trampas
- El README es incoherente en puertos (dice 5000/5001 en una sección y 5001/5002 en otra): fiarse del código de `web_app.py` y `history_app.py`.
- Propuesta SC-1430: **archivar** (OpenClaw retirado; la memoria vive en el brain). No se archiva en esa épica.

## Reutilización
- Para memoria de agentes: el brain (`/brain`, `brain_search`). Búsquedas: lectura de `README.md`, `requirements.txt`, `web_app.py` (nombres), grep en `~/k8s`: sin consumidores.
