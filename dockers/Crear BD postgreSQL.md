```YAML
services:
  db:
    image: postgres:14.3
    container_name: teslo_db
    restart: always

    ports:
      - '5432:5432'

    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}

    volumes:
      - ./postgres:/var/lib/postgresql/data

    healthcheck:
      test: ['CMD-SHELL', 'pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}']
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s

    networks:
      - teslo_network

networks:
  teslo_network:
    driver: bridge
```

.env
POSTGRES_DB=teslo_db
POSTGRES_USER=teslo_user
POSTGRES_PASSWORD=teslo_password