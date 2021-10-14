FROM debian:bullseye-slim

ARG USER=harmony
ARG UID=10000

RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  ca-certificates \
  tzdata \
  bash \
  unzip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN curl https://rclone.org/install.sh | bash
RUN curl -LO https://harmony.one/binary && chmod +x binary && mv binary /usr/local/bin/harmony
RUN harmony -V

# See https://stackoverflow.com/a/55757473/12429735RUN
RUN adduser \
    --disabled-password \
    --gecos "" \
    --shell "/sbin/nologin" \
    --uid "${UID}" \
    "${USER}"

RUN mkdir -p /var/lib/harmony && chown ${USER}:${USER} /var/lib/harmony && chmod 700 /var/lib/harmony
COPY --chown=${USER}:${USER} ./rclone.conf /home/harmony/.config/rclone/rclone.conf

USER ${USER}
WORKDIR /var/lib/harmony

ENTRYPOINT ["harmony"]
