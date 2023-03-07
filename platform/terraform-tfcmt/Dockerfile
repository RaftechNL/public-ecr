FROM alpine:3.13

ARG TERRAFORM_DEFAULT_VERSION=1.3.9
ARG JQ_VERSION=1.6
ARG YQ_VERSION=v4.31.2

RUN apk add --update --no-cache curl ca-certificates bash git wget

# Install jq
RUN curl -sLO https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    mv jq-linux64 /usr/local/bin/jq && \
    chmod +x /usr/local/bin/jq

# Install yq
RUN wget https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64.tar.gz -O - |\
    tar xz && mv yq_linux_amd64 /usr/local/bin/yq

# Install tfcmt
RUN curl -L https://github.com/suzuki-shunsuke/tfcmt/releases/download/v4.0.0/tfcmt_linux_amd64.tar.gz > /usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_DEFAULT_VERSION}/terraform_${TERRAFORM_DEFAULT_VERSION}_linux_amd64.zip \
      && unzip terraform_${TERRAFORM_DEFAULT_VERSION}_linux_amd64.zip \
      && mv terraform /usr/bin/terraform \
      && chmod +x /usr/bin/terraform

ENTRYPOINT ["/bin/bash"]