FROM summerwind/actions-runner:ubuntu-22.04

ARG TERRAFORM_DEFAULT_VERSION=1.6.4
ARG JQ_VERSION=1.7
ARG YQ_VERSION=v4.35.2
ARG TFCMT_VERSION=v4.7.1
ARG GITHUBCOMMENT_VERSION=6.0.3
ARG QBCONF_VERSION=1.0.0
ARG TFMIGRATE_VERSION=0.3.19
ARG TERRAFILE_VERSION=0.8
ARG YOR_VERSION=0.1.185


RUN sudo curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && sudo unzip awscliv2.zip \
    && sudo ./aws/install

RUN type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y) \
    && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && sudo apt update \
    && sudo apt install gh -y    

RUN sudo apt install -y -q vim groff \
    && sudo apt-get clean \
    && sudo rm -rf /var/cache/apt/archives /var/lib/apt/lists/*   

# Install qbconf
RUN sudo curl -sSL https://github.com/RaftechNL/qbconf/releases/download/${QBCONF_VERSION}/qbconf_linux_amd64.tar.gz | sudo tar -xz && \
    sudo mv qbconf_linux_amd64 /usr/local/bin/qbconf

# Install yq 4.33.3
COPY --from=mikefarah/yq@sha256:11da99074a0a985650669ab49b392733a8439bf31291e64aa6d012f7a5d98dfd /usr/bin/yq /usr/bin/yq
COPY .jq /root/.jq 

# Install gomplate
COPY --from=hairyhenderson/gomplate:stable /gomplate /bin/gomplate

# install tfcmt
RUN sudo curl -sSL  https://github.com/suzuki-shunsuke/tfcmt/releases/download/${TFCMT_VERSION}/tfcmt_linux_amd64.tar.gz | sudo tar xvz -C /tmp \
      && sudo mv /tmp/tfcmt usr/local/bin/tfcmt \
      && sudo chmod +x /usr/local/bin/tfcmt

# install terraform-switcher/
RUN sudo curl -L https://raw.githubusercontent.com/warrensbox/terraform-switcher/release/install.sh | sudo sh && /usr/local/bin/tfswitch -d $TERRAFORM_DEFAULT_VERSION

# install tfmigrate
RUN sudo curl -sSL  https://github.com/minamijoyo/tfmigrate/releases/download/v${TFMIGRATE_VERSION}/tfmigrate_${TFMIGRATE_VERSION}_linux_amd64.tar.gz | sudo tar xvz -C /tmp \
      && sudo mv /tmp/tfmigrate usr/local/bin/tfmigrate \
      && sudo chmod +x /usr/local/bin/tfmigrate

RUN sudo curl -sSL https://github.com/coretech/terrafile/releases/download/v${TERRAFILE_VERSION}/terrafile_${TERRAFILE_VERSION}_Linux_x86_64.tar.gz | sudo tar xvz -C /tmp \
      && sudo mv /tmp/terrafile usr/local/bin/terrafile \
      && sudo chmod +x /usr/local/bin/terrafile

RUN sudo curl -sSL https://github.com/bridgecrewio/yor/releases/download/${YOR_VERSION}/yor_${YOR_VERSION}_linux_amd64.tar.gz | sudo tar xvz -C /tmp \
      && sudo mv /tmp/yor usr/local/bin/yor \
      && sudo chmod +x /usr/local/bin/yor

RUN sudo curl -sSL https://github.com/suzuki-shunsuke/github-comment/releases/download/v${GITHUBCOMMENT_VERSION}/github-comment_${GITHUBCOMMENT_VERSION}_linux_amd64.tar.gz | sudo tar xvz -C /tmp \
      && sudo mv /tmp/github-comment usr/local/bin/github-comment \
      && sudo chmod +x /usr/local/bin/github-comment    