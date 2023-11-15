FROM alpine:3.13

ARG TERRAFORM_DEFAULT_VERSION=1.3.9
ARG JQ_VERSION=1.7
ARG YQ_VERSION=v4.35.2
ARG TFCMT_VERSION=v4.7.1
ARG TFSWITCH_VERSION=0.13.1308
ARG GITHUBCOMMENT_VERSION=6.0.2

RUN apk add --update --no-cache curl ca-certificates bash git wget

# Install jq
RUN curl -sLO https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    mv jq-linux64 /usr/local/bin/jq && \
    chmod +x /usr/local/bin/jq

# Install yq
RUN wget https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64.tar.gz -O - |\
    tar xz && mv yq_linux_amd64 /usr/local/bin/yq

# Install tfcmt
RUN curl -L https://github.com/suzuki-shunsuke/tfcmt/releases/download/${TFCMT_VERSION}/tfcmt_linux_amd64.tar.gz > /usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

RUN curl -L https://github.com/warrensbox/terraform-switcher/releases/download/${TFSWITCH_VERSION}/terraform-switcher_${TFSWITCH_VERSION}_linux_amd64.tar.gz > /usr/local/bin/tfswitch \
      && chmod +x /usr/local/bin/tfswitch

RUN curl -L https://github.com/suzuki-shunsuke/github-comment/releases/download/v${GITHUBCOMMENT_VERSION}/github-comment_${GITHUBCOMMENT_VERSION}_linux_amd64.tar.gz > /usr/local/bin/github-comment \
      && chmod +x /usr/local/bin/github-comment

ENTRYPOINT ["/bin/bash"]