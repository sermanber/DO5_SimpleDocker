FROM ubuntu:22.04

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    libfcgi-dev \
    spawn-fcgi \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -r -s /bin/false pickle_rick

COPY main.c .
COPY index.html .

RUN gcc main.c -o main -lfcgi && chown -R pickle_rick:pickle_rick /app

USER pickle_rick

# Запускаем сервер на порту 81 в foreground режиме
CMD ["spawn-fcgi", "-n", "-p", "81", "./main"]