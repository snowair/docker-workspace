FROM snowair/debian:php-base

RUN apt-get update && apt-get install -y tshark --force-yes  --no-install-recommends && apt-get autoremove -y && apt-get clean -y  \
    && rm -rf /var/lib/apt/lists/* \

CMD ["/bin/bash"]
