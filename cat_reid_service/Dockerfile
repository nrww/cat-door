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
    apt-get install -y git curl wget ffmpeg libsm6 libxext6

ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache

RUN git clone https://github.com/nrww/Cat-Re-ID-service

# RUN wget -o vits16_cat.ckpt https://www.dropbox.com/scl/fi/bt5res9g9aqi3ep36bej3/vits16_cat.ckpt?rlkey=izpxikhd02vsgvlhl6ywjt1v3&st=8plg158a
# RUN wget -o img.tar.gz https://www.dropbox.com/scl/fi/hsa4awbn6f67mdchszaix/img.tar.gz?rlkey=mmfqt6bhva7dmkeq1xv6cndqj&st=0owr3274
# RUN wget -o val_vec.pd https://www.dropbox.com/scl/fi/enai883ajbnudi5zefq44/val_vec.pd?rlkey=gfjseimigtoyjdpyoykjnlrkr&st=tpwwzb9d
# RUN tar -xzf /app/img.tar.gz  && rm /app/img.tar.gz

ENTRYPOINT ["python", "./Cat-Re-ID-service/main.py"]
