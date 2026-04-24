FROM python:3.12-slim-bookworm AS builder

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y --no-install-recommends gcc python3-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt ./

RUN pip install --no-cache-dir --prefix=/install -r requirements.txt "setuptools<81"

FROM python:3.12-slim-bookworm

WORKDIR /usr/src/app

COPY --from=builder /install /usr/local

COPY . .

RUN opentelemetry-bootstrap -a install

ENV RECOMMENDATION_PORT=1010
