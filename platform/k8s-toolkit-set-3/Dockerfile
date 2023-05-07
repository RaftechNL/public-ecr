FROM bitnami/minideb:bullseye

ARG KAPP_VERSION=v0.55.0
ARG JQ_VERSION=1.6
ARG QBCONF_VERSION=0.16.0

RUN install_packages curl ca-certificates git

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-amd64 > /usr/local/bin/kapp \
    && chmod +x /usr/local/bin/kapp

# Install jq
RUN curl -sLO https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    mv jq-linux64 /usr/local/bin/jq && \
    chmod +x /usr/local/bin/jq

# Install qbconf
RUN curl -sSL https://github.com/RaftechNL/qbconf/releases/download/${QBCONF_VERSION}/qbconf_linux_amd64.tar.gz | tar -xz && \
    mv qbconf_linux_amd64 /usr/local/bin/qbconf

# Install yq 4.33.3
COPY --from=mikefarah/yq@sha256:11da99074a0a985650669ab49b392733a8439bf31291e64aa6d012f7a5d98dfd /usr/bin/yq /usr/bin/yq

# Install gomplate
COPY --from=hairyhenderson/gomplate:stable /gomplate /bin/gomplate

ENTRYPOINT ["/bin/bash"]
