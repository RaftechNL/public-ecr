FROM alpine:3.13

ARG KUBECTL_VERSION=1.24.0
ENV KAPP_VERSION=v0.54.0

RUN apk add --update --no-cache curl bash git jq yq

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-amd64 > /usr/local/bin/kapp \
    && chmod +x /usr/local/bin/kapp

# Install kubectl
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    mv kubectl /usr/bin/kubectl && \
    chmod +x /usr/bin/kubectl

ENTRYPOINT ["/bin/bash"]