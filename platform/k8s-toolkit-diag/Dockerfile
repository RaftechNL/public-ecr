# Solution provided by https://github.com/aws/aws-cli/issues/4685#issuecomment-1094307056
FROM python:3-alpine3.13 AS installer

RUN set -ex; \
    apk add --no-cache \
    git unzip groff \
    build-base libffi-dev cmake

ENV AWS_CLI_VERSION=2.9.4
RUN set -eux; \
    mkdir /aws; \
    git clone --single-branch --depth 1 -b ${AWS_CLI_VERSION} https://github.com/aws/aws-cli.git /aws; \
    cd /aws; \
    python -m venv venv; \
    . venv/bin/activate; \
    ./scripts/installers/make-exe

RUN set -ex; \
    unzip /aws/dist/awscli-exe.zip; \
    ./aws/install --bin-dir /aws-cli-bin; \
    /aws-cli-bin/aws --version

FROM alpine:3.13

ARG KUBECTL_VERSION=1.24.0

RUN apk --no-cache add groff curl bash jq yq
RUN apk add --no-cache --update bind-tools

# Install kubectl
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    mv kubectl /usr/bin/kubectl && \
    chmod +x /usr/bin/kubectl

COPY --from=installer /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=installer /aws-cli-bin/ /usr/local/bin/    

ENTRYPOINT ["/bin/bash"]