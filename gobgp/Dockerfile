FROM ubuntu:22.04
RUN apt-get update && \
    apt-get remove -y binutils && \
    apt-get install -y \
        python3 \
        python3-pip \
        wget && \
    rm -rf /var/lib/apt/lists/*
COPY ./requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt
RUN wget https://github.com/osrg/gobgp/releases/download/v1.32/gobgp_1.32_linux_amd64.tar.gz && \
    tar -xzvf gobgp_1.32_linux_amd64.tar.gz && \
    mv gobgp /usr/local/bin/gobgp && \
    mv gobgpd /usr/local/bin/gobgpd && \
    rm gobgp_1.32_linux_amd64.tar.gz
COPY ./gobgpd.conf /root/gobgp/gobgpd.conf
COPY ./entrypoint.sh /root/gobgp/entrypoint.sh
COPY ./startup.sh /root/gobgp/startup.sh
RUN chmod +x /root/gobgp/entrypoint.sh && \
    chmod +x /root/gobgp/startup.sh
ENTRYPOINT ["/root/gobgp/entrypoint.sh"]
