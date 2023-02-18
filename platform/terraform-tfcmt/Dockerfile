FROM alpine:3.13

ARG TERRAFORM_DEFAULT_VERSION=1.3.9

RUN apk add --update --no-cache curl ca-certificates bash git jq

# Install tfcmt
RUN curl -L https://github.com/suzuki-shunsuke/tfcmt/releases/download/v4.0.0/tfcmt_linux_amd64.tar.gz > /usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_DEFAULT_VERSION}/terraform_${TERRAFORM_DEFAULT_VERSION}_linux_amd64.zip \
      && unzip terraform_${TERRAFORM_DEFAULT_VERSION}_linux_amd64.zip \
      && mv terraform /usr/bin/terraform \
      && chmod +x /usr/bin/terraform

ENTRYPOINT ["/bin/bash"]