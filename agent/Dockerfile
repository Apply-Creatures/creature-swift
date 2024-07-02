FROM woodpeckerci/woodpecker-agent:next-b8b6efb352-alpine

EXPOSE 3000

ENV WOODPECKER_SERVER=ci.applycreatures.com
ENV WOODPECKER_HEALTHCHECK=false
ENV WOODPECKER_GRPC_SECURE=false
ENV WOODPECKER_HOSTNAME=creature-swift-agent.internal:3000
ENV WOODPECKER_HEALTHCHECK_ADDR=creature-swift-agent.internal:3000
ENV WOODPECKER_MAX_WORKFLOWS=2

ENV WOODPECKER_BACKEND=local

RUN apk add --no-cache git git-lfs bash curl nodejs

RUN mkdir -p /tmp
RUN chmod 1777 /tmp

RUN curl -fsSL https://bun.sh/install | bash

RUN curl -L https://fly.io/install.sh | sh
RUN export PATH=$PATH:$(ls -d /tmp/woodpecker-local-*/home/.fly)
ENV PATH=$PATH:/root/.fly/bin/

ENTRYPOINT ["/bin/woodpecker-agent"]