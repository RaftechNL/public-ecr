FROM alpine:3.13

ARG HELM_VERSION=3.10.2
ARG KUBECTL_VERSION=1.24.0
ARG KUSTOMIZE_VERSION=v4.5.7
ENV KAPP_VERSION=v0.54.0
ARG JQ_VERSION=1.6
ARG YQ_VERSION=v4.31.2

RUN apk add --update --no-cache curl bash git wget

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-amd64 > /usr/local/bin/kapp \
      && chmod +x /usr/local/bin/kapp

# Install helm (latest release)
RUN curl -sL "https://get.helm.sh/helm-v${HELM_VERSION}-linux-amd64.tar.gz" | tar -xvz && \
    mv linux-amd64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    rm -rf linux-amd64

RUN apk add --no-cache groff curl bash wget
RUN apk add --no-cache --update bind-tools

# Install kubectl
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    mv kubectl /usr/bin/kubectl && \
    chmod +x /usr/bin/kubectl

# Install jq
RUN curl -sLO https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 && \
    mv jq-linux64 /usr/local/bin/jq && \
    chmod +x /usr/local/bin/jq

# Install yq
RUN wget https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64.tar.gz -O - |\
    tar xz && mv yq_linux_amd64 /usr/local/bin/yq


# Install kustomize (latest release)
RUN curl -sLO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2F${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    tar xvzf kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    mv kustomize /usr/bin/kustomize && \
    chmod +x /usr/bin/kustomize


ENTRYPOINT ["/bin/bash"]