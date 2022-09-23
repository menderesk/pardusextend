FROM pardus/yirmibir

LABEL org.opencontainers.image.authors="Menderes Keskin" \
      org.opencontainers.image.description="Pardus Yirmibir OpenJDK11. Java uygulamalarınızı dağıtmak ve çalıştırmak için yerli ve millî Linux dağıtımı Pardus Yirmibir'in genişletilmiş konteynerı." \
      org.opencontainers.image.documentation="https://bulutbilisimciler.com" \
      org.opencontainers.image.licenses="GPL v2.0" \
      org.opencontainers.image.title="Pardus Yirmibir Temel Görüntüsü (JDK11)" \
      org.opencontainers.image.url="https://pardus.org.tr/" \
      org.opencontainers.image.vendor="TÜBİTAK" \
      org.opencontainers.image.version="21.2"

ARG OPENJDK_VERSION=11.0.2

ENV TERM=xterm \
    JAVA_HOME=/ortakatman/java11 \
    PATH="${PATH}:/ortakatman/java11/bin" \
    TZ="Europe/Istanbul" \
    ADRES=/ortakatman

ADD ./motd /etc/motd

RUN echo '[ ! -z "$TERM" -a -r /etc/motd ] && cat /etc/motd' \
    >> /etc/bash.bashrc \
    && echo "$(cat /etc/os-release | awk 'NR==2, NR==5{print}')" >> /etc/motd

RUN apt -y update \
    && apt -y upgrade

RUN set -eux \
    && PAKETLER="bash \
        tzdata \
        wget" \
     && apt -y install ${PAKETLER}

RUN mkdir /ortakatman \
    && wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-${OPENJDK_VERSION}_linux-x64_bin.tar.gz \
    && tar -xzvf openjdk-${OPENJDK_VERSION}_linux-x64_bin.tar.gz \
    && mv jdk-${OPENJDK_VERSION} /ortakatman/java11 \
    && rm -f openjdk-${OPENJDK_VERSION}_linux-x64_bin.tar.gz \
    && update-alternatives --install "/usr/bin/java" "java" "/ortakatman/java11/bin/java" 0 \
    && apt clean

WORKDIR /ortakatman

CMD ["bash"]
