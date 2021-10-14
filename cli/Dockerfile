FROM debian:bullseye-slim

ARG USER=harmony
ARG UID=10000

RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  ca-certificates \
  tzdata \
  bash \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN curl -LO https://harmony.one/hmycli && chmod +x hmycli  && mv hmycli /usr/local/bin/hmy
RUN hmy cookbook


# See https://stackoverflow.com/a/55757473/12429735RUN
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "${UID}" \
    "${USER}"

RUN mkdir -p /var/lib/harmony/blskeys && chown -R ${USER}:${USER} /var/lib/harmony && chmod -R 700 /var/lib/harmony

USER ${USER}

ENTRYPOINT ["bash"]
