FROM debian:buster-slim

ENV KUBECTL_VERSION=v1.12.2
ENV HELM_VERSION=v2.9.1

RUN apt-get update && \
    apt-get install -y ca-certificates curl git openssl default-mysql-client unzip
RUN curl https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
    -o /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl && \
    curl https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz \
    -o helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    tar -zxvf helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    rm -rf linux-amd64 && \
    rm helm-${HELM_VERSION}-linux-amd64.tar.gz
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install

ADD tidb-operator /charts/e2e/tidb-operator
ADD tidb-cluster /charts/e2e/tidb-cluster
ADD tidb-backup /charts/e2e/tidb-backup
ADD manifests /manifests/e2e

ADD bin/ginkgo /usr/local/bin/
ADD bin/e2e.test /usr/local/bin/
ADD bin/webhook /usr/local/bin/
ADD bin/blockwriter /usr/local/bin/
ADD bin/apiserver /usr/local/bin/
