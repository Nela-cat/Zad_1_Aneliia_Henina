# Dockerfile
# Zadanie 1.1 - Aplikacje w chmurze
# Autor: Aneliia Henina

# Etap 1: Instalacja zależności
FROM python:3.10-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
RUN rm requirements.txt

# Etap 2: Obraz finalny
FROM python:3.10-slim
WORKDIR /app
# Instalacja curl dla HEALTHCHECK
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
COPY --from=builder /usr/local/lib/python3.10/site-packages/ /usr/local/lib/python3.10/site-packages/
COPY --from=builder /usr/local/bin/ /usr/local/bin/
COPY . /app

# Sprawdzanie stanu kontenera
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8000 || exit 1

# Uruchomienie aplikacji
CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8000", "--log-level", "debug"]