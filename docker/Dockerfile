FROM ubuntu:18.04
COPY CloudServicesRootCA.crt CloudServicesCA-G2.crt /usr/local/share/ca-certificates/
RUN sed -i 's/archive\.ubuntu\.com/us\.archive\.ubuntu\.com/' /etc/apt/sources.list && \
apt-get update -y --fix-missing && apt-get install -y --fix-missing inetutils-ping curl build-essential gnupg2 jq git openssl wget netcat ca-certificates && \
update-ca-certificates && \
# install pivnet
wget --no-check-certificate -O /usr/local/bin/pivnet $(curl -s https://api.github.com/repos/pivotal-cf/pivnet-cli/releases/latest | grep browser_download_url | grep linux | cut -d '"' -f 4) && \
chmod +x /usr/local/bin/pivnet && \
# install pks cli
pivnet login --api-token RyYyf5v1LUyuvKZHqxNQ && pivnet download-product-files -p pivotal-container-service -r 1.6.1 -i 579531 -d /usr/local/bin/ && mv /usr/local/bin/pks-linux-amd64* /usr/local/bin/pks && chmod +x /usr/local/bin/pks && \
# install kubectl
pivnet download-product-files -p pivotal-container-service -r 1.6.1 -i 527933 -d /usr/local/bin/ && mv /usr/local/bin/kubectl-linux-amd64* /usr/local/bin/kubectl && chmod +x /usr/local/bin/kubectl && \
wget --no-check-certificate https://get.helm.sh/helm-v3.1.1-linux-amd64.tar.gz && \
tar -zxvf helm-v3.1.1-linux-amd64.tar.gz && \
mv linux-amd64/helm /usr/local/bin/
