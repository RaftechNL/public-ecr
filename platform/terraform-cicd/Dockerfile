FROM python:3.9-slim AS installer

RUN set -ex; \
    apt-get update && apt-get install \
    git unzip groff \
    libffi-dev cmake python3-distutils -y -q 

ENV AWS_CLI_VERSION=2.13.36

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

# FROM debian:stable-slim
FROM bitnami/minideb:bullseye

ARG TERRAFORM_DEFAULT_VERSION=1.6.4
ARG JQ_VERSION=1.7
ARG YQ_VERSION=v4.35.2
ARG TFCMT_VERSION=v4.7.1
ARG GITHUBCOMMENT_VERSION=6.0.3
ARG QBCONF_VERSION=1.0.0
ARG TFMIGRATE_VERSION=0.3.19
ARG TERRAFILE_VERSION=0.8
ARG YOR_VERSION=0.1.185

RUN apt update \
    && apt install -y -q curl vim git groff gpg

RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt update \
    && apt install -y -q gh \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives /var/lib/apt/lists/*

# Install jq
RUN curl -sLO https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    mv jq-linux64 /usr/local/bin/jq && \
    chmod +x /usr/local/bin/jq

# Install qbconf
RUN curl -sSL https://github.com/RaftechNL/qbconf/releases/download/${QBCONF_VERSION}/qbconf_linux_amd64.tar.gz | tar -xz && \
    mv qbconf_linux_amd64 /usr/local/bin/qbconf

# Install yq 4.33.3
COPY --from=mikefarah/yq@sha256:11da99074a0a985650669ab49b392733a8439bf31291e64aa6d012f7a5d98dfd /usr/bin/yq /usr/bin/yq
COPY .jq /root/.jq 

# Install gomplate
COPY --from=hairyhenderson/gomplate:stable /gomplate /bin/gomplate

RUN curl -sSL  https://github.com/suzuki-shunsuke/tfcmt/releases/download/${TFCMT_VERSION}/tfcmt_linux_amd64.tar.gz | tar xvz -C /tmp \
      && mv /tmp/tfcmt usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

RUN curl -L https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh | sh && /usr/local/bin/tfswitch -d $TERRAFORM_DEFAULT_VERSION

RUN curl -sSL  https://github.com/minamijoyo/tfmigrate/releases/download/v${TFMIGRATE_VERSION}/tfmigrate_${TFMIGRATE_VERSION}_linux_amd64.tar.gz | tar xvz -C /tmp \
      && mv /tmp/tfmigrate usr/local/bin/tfmigrate \
      && chmod +x /usr/local/bin/tfmigrate

RUN curl -sSL https://github.com/coretech/terrafile/releases/download/v${TERRAFILE_VERSION}/terrafile_${TERRAFILE_VERSION}_Linux_x86_64.tar.gz | tar xvz -C /tmp \
      && mv /tmp/terrafile usr/local/bin/terrafile \
      && chmod +x /usr/local/bin/terrafile

RUN curl -sSL https://github.com/bridgecrewio/yor/releases/download/${YOR_VERSION}/yor_${YOR_VERSION}_linux_amd64.tar.gz | tar xvz -C /tmp \
      && mv /tmp/yor usr/local/bin/yor \
      && chmod +x /usr/local/bin/yor

RUN curl -sSL https://github.com/suzuki-shunsuke/github-comment/releases/download/v${GITHUBCOMMENT_VERSION}/github-comment_${GITHUBCOMMENT_VERSION}_linux_amd64.tar.gz | tar xvz -C /tmp \
      && mv /tmp/github-comment usr/local/bin/github-comment \
      && chmod +x /usr/local/bin/github-comment

COPY --from=installer /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=installer /aws-cli-bin/ /usr/local/bin/    


ENTRYPOINT ["/bin/bash"]