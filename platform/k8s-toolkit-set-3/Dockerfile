FROM bitnami/minideb:bullseye

ENV KAPP_VERSION=v0.63.3
ARG JQ_VERSION=1.7.1
ARG QBCONF_VERSION=1.0.0

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

# Install yq mikefarah/yq:4.44.3
COPY --from=mikefarah/yq@sha256:5b3d851bf28b04ef902fee86305f4dd7e063919c1cafedab2042adb16221c025 /usr/bin/yq /usr/bin/yq

# Install gomplate
COPY --from=hairyhenderson/gomplate:stable /gomplate /bin/gomplate

ENTRYPOINT ["/bin/bash"]
