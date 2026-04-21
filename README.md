# ⚙️ Hermes Agent — Configuración

Configuración para desplegar **Hermes Agent** con Docker Compose.

> ⚠️ **Este repositorio NO incluye API keys ni datos sensibles.**

---

## 📦 Incluye

| Archivo | Descripción |
|---------|-------------|
| `docker-compose.yml` | Gateway + Dashboard + Docker-out-of-Docker |

---

## 🚀 Despliegue Rápido

```bash
# 1. Clonar este repo
git clone https://github.com/FabrizioCurotto/hermes-config.git
cd hermes-config

# 2. Crear directorio de datos con tus API keys
mkdir -p ~/.hermes
cp config.yaml.example ~/.hermes/config.yaml  # O crea manualmente
nano ~/.hermes/.env                             # Añadir tus API keys

# 3. Iniciar (descarga la imagen oficial + arranca contenedores)
docker compose up -d

# 4. Ver logs
docker compose logs -f

# 5. Acceder al dashboard
open http://localhost:9119
```

---

## 🔑 Variables necesarias en `~/.hermes/.env`

```bash
OPENROUTER_API_KEY=sk-or-v1-tuclaveaquí
GITHUB_TOKEN=ghp_tuclaveaquí
TELEGRAM_BOT_TOKEN=123456789:ABCdef...
TELEGRAM_ALLOWED_USERS=           # Tu ID de Telegram
```

---

## 🐳 Docker-out-of-Docker (DooD)

El `docker-compose.yml` monta el socket de Docker del host:

```yaml
volumes:
  - hermes-data:/opt/data
  - /var/run/docker.sock:/var/run/docker.sock  # ← Esto
```

Esto permite que **Hermes** pueda ejecutar `docker build`, `docker run`, etc.

### Permisos en el Host

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 📂 Estructura de Datos

```
~/.hermes/
├── .env              # API keys (NO subir)
├── config.yaml       # Config general
├── SOUL.md          # Personalidad del bot
├── sessions/        # Historial de conversaciones
├── memories/       # Memoria persistente
├── skills/         # Skills instalados
└── state.db        # Base de datos
```

---

MIT License © 2026 FabrizioCurotto
