# Tested with docker.io/library/alpine:3.22.0
FROM docker.io/library/alpine:latest

RUN apk add --no-cache openssh-server

EXPOSE 2222

COPY --chown=root:root --chmod=755 startup.sh /

RUN addgroup -S portfwd && adduser -S portfwd -G portfwd && \
    install -oportfwd -gportfwd -dm700 /ssh-host-keys /ssh-client-keys \
    /home/portfwd/sshd /home/portfwd/.ssh

USER portfwd

COPY --chown=portfwd:portfwd --chmod=644 sshd_config /home/portfwd/sshd/

ENTRYPOINT ["/startup.sh"]
