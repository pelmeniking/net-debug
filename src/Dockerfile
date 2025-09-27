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
    iperf3 \
    mtr \
    socat \
    jq \
    dumb-init

RUN printf "%s\n" \
"=====================================" \
"         Net-Debug Container         " \
"-------------------------------------" \
"Available tools:" \
"bash, curl, dig, ping, netcat-openbsd," \
"tcpdump, nmap, traceroute, busybox-extras," \
"iperf3, mtr, socat, jq" \
"=====================================" \
> /etc/motd \
    && echo 'cat /etc/motd' >> /etc/profile \
    && echo 'cat /etc/motd' >> /root/.bashrc

ENTRYPOINT ["/usr/bin/dumb-init","--"]
CMD ["bash","-lc","trap : TERM INT; sleep infinity & wait"]