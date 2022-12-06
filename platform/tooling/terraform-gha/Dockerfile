FROM alpine:3.13

ARG TERRAFORM_DEFAULT_VERSION=1.3.6

RUN apk add --update --no-cache curl ca-certificates bash git jq 

# Install tfswitch (latest release)
RUN curl -L https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh | bash \
      && tfswitch ${TERRAFORM_DEFAULT_VERSION}

# Install tfcmt
RUN curl -L https://github.com/suzuki-shunsuke/tfcmt/releases/download/v4.0.0/tfcmt_linux_amd64.tar.gz > /usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

# Install github-comment
RUN curl -L https://github.com/suzuki-shunsuke/github-comment/releases/download/v5.0.0/github-comment_5.0.0_linux_amd64.tar.gz > /usr/local/bin/tfcmt \
      && chmod +x /usr/local/bin/tfcmt

ENTRYPOINT ["/bin/bash"]