# Docker Compose — PostgreSQL

Plantilla reutilizable y optimizada para levantar una base de datos PostgreSQL con Docker Compose.

## 📄 docker-compose.yml

```yaml
services:
  postgres:
    image: postgres:16-alpine
    container_name: postgres_db
    restart: unless-stopped
    ports:
      - '${POSTGRES_PORT:-5432}:5432'
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-postgres}
      POSTGRES_DB: ${POSTGRES_DB:-my_database}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ['CMD-SHELL', 'pg_isready -U ${POSTGRES_USER:-postgres} -d ${POSTGRES_DB:-my_database}']
      interval: 5s
      timeout: 5s
      retries: 5
      start_period: 10s
    networks:
      - app_network

volumes:
  postgres_data:
    name: postgres_data

networks:
  app_network:
    name: app_network
    driver: bridge
```

## ⚙️ Variables de entorno (.env)

```env
POSTGRES_DB=my_database
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_PORT=5432
```

## 🚀 Comandos útiles

```bash
# Iniciar contenedor en segundo plano
docker compose up -d

# Ver logs en tiempo real
docker compose logs -f postgres

# Detener el contenedor sin borrar datos
docker compose down

# Detener y borrar volúmenes de datos (reset completo de BD)
docker compose down -v

# Acceder a la terminal de PostgreSQL (psql)
docker compose exec -it postgres psql -U postgres -d my_database
```