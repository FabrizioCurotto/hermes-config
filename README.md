# ⚙️ Hermes Agent — Configuración

Configuración base para desplegar **Hermes Agent** con Docker Compose.

> ⚠️ **Este repositorio NO incluye API keys ni datos sensibles.**
> Los archivos sensibles están en `.gitignore`.

---

## 📦 Incluye

| Archivo | Descripción |
|---------|-------------|
| `docker-compose.yml` | Gateway + Dashboard + Docker-out-of-Docker |
| `Dockerfile` | Imagen base de Hermes (con Docker CLI) |
| `entrypoint.sh` | Script de inicio del contenedor |
| `config.yaml.example` | Plantilla de configuración |
| `SOUL.md` | Personalidad del agente |

---

## 🚀 Despliegue Rápido

```bash
# 1. Clonar este repo
git clone https://github.com/FabrizioCurotto/hermes-config.git
cd hermes-config

# 2. Configurar variables sensibles (crear .env manualmente)
# Editar config.yaml y crear .env con tus API keys

# 3. Iniciar
docker compose up -d

# 4. Ver logs
docker compose logs -f
```

---

## 🔑 Configuración Sensible (Manual)

### `.env` — API Keys y Tokens

Crear en `~/.hermes/.env`:

```bash
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
TELEGRAM_BOT_TOKEN=123456:ABC-...
```

### `config.yaml` — Configuración General

```bash
cp config.yaml.example ~/.hermes/config.yaml
# Editar con tu editor favorito
```

---

## 🐳 Docker-out-of-Docker (DooD)

El `docker-compose.yml` incluye el socket de Docker del host:

```yaml
volumes:
  - ~/.hermes:/opt/data
  - /var/run/docker.sock:/var/run/docker.sock  # ← Esto
```

Esto permite que **Hermes Agent** pueda:
- Construir imágenes (`docker build`)
- Ejecutar contenedores (`docker run`)
- Orquestar servicios (`docker-compose`)

### Permisos en el Host

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🔄 Estructura de Datos

```
~/.hermes/
├── .env              # API keys (NO subir)
├── config.yaml       # Config general
├── SOUL.md          # Personalidad del bot
├── sessions/        # Historial de conversaciones
├── memories/         # Memoria persistente
├── skills/          # Skills instalados
├── cron/            # Tareas programadas
├── logs/            # Logs de ejecución
├── hooks/           # Webhooks
├── auth.json        # Tokens OAuth (NO subir)
└── state.db         # Base de datos
```

---

MIT License © 2026 FabrizioCurotto
