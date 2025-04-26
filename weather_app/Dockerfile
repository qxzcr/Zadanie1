# Etap 1: budowanie środowiska
FROM python:3.12-slim as builder

# Ustawiamy katalog roboczy
WORKDIR /app

# Kopiujemy wymagania
COPY requirements.txt .

# Instalujemy zależności do katalogu lokalnego
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# Etap 2: tworzenie finalnego obrazu
FROM python:3.12-slim

# Autor obrazu
LABEL maintainer="Yelyzaveta Zlydnieva"

# Katalog roboczy
WORKDIR /app

# Kopiujemy aplikację
COPY app.py .
COPY templates/ templates/

# Kopiujemy zainstalowane biblioteki z etapu buildera
COPY --from=builder /install /usr/local

# Ustawiamy zmienną środowiskową
ENV PORT=5000

# Otwieramy port
EXPOSE 5000

# Healthcheck, czy aplikacja działa
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
 CMD curl --fail http://localhost:5000 || exit 1

# Startujemy aplikację
CMD ["python", "app.py"]
