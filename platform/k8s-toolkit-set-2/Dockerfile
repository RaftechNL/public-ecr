FROM alpine:3.13

ARG KUBECTL_VERSION=1.24.0
ENV KAPP_VERSION=v0.54.0
ARG JQ_VERSION=1.6
ARG YQ_VERSION=v4.31.2

RUN apk add --update --no-cache curl bash git wget

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-amd64 > /usr/local/bin/kapp \
    && chmod +x /usr/local/bin/kapp

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

ENTRYPOINT ["/bin/bash"]