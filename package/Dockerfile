FROM ubuntu:19.10
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl ca-certificates jq iproute2

ENV DOCKER_URL_amd64=https://get.docker.com/builds/Linux/x86_64/docker-1.10.3 \
    DOCKER_URL_arm=https://github.com/rancher/docker/releases/download/v1.10.3-ros1/docker-1.10.3_arm \
    DOCKER_URL=DOCKER_URL_${ARCH}

RUN if [ "${ARCH}" == "s390x" ]; then \
        curl -L https://download.docker.com/linux/static/stable/s390x/docker-18.06.3-ce.tgz | tar xzvf - && \
        cp docker/docker /usr/bin/ && \
        chmod +x /usr/bin/docker; \
    else \
        wget -O - ${!DOCKER_URL} > /usr/bin/docker && chmod +x /usr/bin/docker; \
    fi

ARG VERSION=dev
ENV AGENT_IMAGE rancher/agent:${VERSION}
COPY agent run.sh /usr/bin/
ENTRYPOINT ["run.sh"]
