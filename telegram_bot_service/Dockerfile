FROM python:3.9-slim as builder
WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc

COPY requirements.txt .
RUN pip wheel --no-cache-dir --no-deps --wheel-dir /app/wheels -r requirements.txt

FROM python:3.9-slim

WORKDIR /app

COPY --from=builder /app/wheels /wheels
COPY --from=builder /app/requirements.txt .

RUN pip install --no-cache /wheels/*

RUN apt-get update && \
    apt-get install -y git curl

ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache

RUN git clone  https://github.com/nrww/Cat-Telegram-Bot
ENTRYPOINT ["python", "/app/Cat-Telegram-Bot/main.py"]
