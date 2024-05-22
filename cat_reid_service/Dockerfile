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

RUN git clone https://github.com/nrww/Cat-Re-ID-service

ADD https://www.dropbox.com/scl/fi/bt5res9g9aqi3ep36bej3/vits16_cat.ckpt?rlkey=izpxikhd02vsgvlhl6ywjt1v3&st=8plg158a&dl=0 /app/Cat-Telegram-Bot/
ADD https://www.dropbox.com/scl/fi/49jpyulyvs67d06fxhp0o/img.tar?rlkey=qo52ifnsq2yqjo21w10x2tosg&st=34lugw1h&dl=0 /app/Cat-Telegram-Bot/

ENTRYPOINT ["python", "/app/Cat-Telegram-Bot/main.py"]