FROM alpine:3.13

ENV KAPP_VERSION=v0.54.0

RUN apk add --update --no-cache curl bash git jq yq gomplate

# Install kapp 
RUN curl -L https://github.com/vmware-tanzu/carvel-kapp/releases/download/${KAPP_VERSION}/kapp-linux-amd64 > /usr/local/bin/kapp \
    && chmod +x /usr/local/bin/kapp

ENTRYPOINT ["/bin/bash"]