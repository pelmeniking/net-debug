FROM alpine:latest

RUN apk add --no-cache \
    bash \
    curl \
    bind-tools \
    iputils \
    netcat-openbsd \
    tcpdump \
    nmap \
    traceroute \
    busybox-extras \
    dumb-init

RUN printf "%s\n" \
"=====================================" \
"         Net-Debug Container         " \
"-------------------------------------" \
"Available tools:" \
"bash, curl, dig (bind-tools), ping (iputils)," \
"netcat-openbsd, tcpdump, nmap, traceroute," \
"busybox-extras" \
"=====================================" \
> /etc/motd \
    && echo 'cat /etc/motd' >> /etc/profile \
    && echo 'cat /etc/motd' >> /root/.bashrc

ENTRYPOINT ["/usr/bin/dumb-init","--"]
CMD ["bash","-lc","trap : TERM INT; sleep infinity & wait"]