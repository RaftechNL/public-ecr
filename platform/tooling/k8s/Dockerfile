FROM alpine:3.13

ARG HELM_VERSION=3.10.2
ARG KUBECTL_VERSION=1.24.0
ARG KUSTOMIZE_VERSION=v4.5.7
ENV KAPP_VERSION=v0.54.0

RUN apk add --update --no-cache curl ca-certificates bash git jq 

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-arm64 > /usr/local/bin/kapp \
      && chmod +x /usr/local/bin/kapp

# Install helm (latest release)
RUN curl -sL "https://get.helm.sh/helm-v${HELM_VERSION}-linux-arm64.tar.gz" | tar -xvz && \
    mv linux-arm64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    rm -rf linux-arm64

# Install kubectl
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/arm64/kubectl && \
    mv kubectl /usr/bin/kubectl && \
    chmod +x /usr/bin/kubectl

# Install kustomize (latest release)
RUN curl -sLO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2F${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_arm64.tar.gz && \
    tar xvzf kustomize_${KUSTOMIZE_VERSION}_linux_arm64.tar.gz && \
    mv kustomize /usr/bin/kustomize && \
    chmod +x /usr/bin/kustomize

ENTRYPOINT ["/bin/bash"]