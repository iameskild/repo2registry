FROM ubuntu:22.04

ARG GCP_SA_CREDENTIALS

ENV RESTIC_VERSION="0.15.0"
ENV GCLOUD_VERSION="417.0.0"

RUN apt-get update && \
    apt-get install wget bzip2 curl zip apt-transport-https ca-certificates gnupg -y

# Install restic from source
RUN wget -O restic.bz2 https://github.com/restic/restic/releases/download/v${RESTIC_VERSION}/restic_${RESTIC_VERSION}_linux_amd64.bz2 && \
    bunzip2 restic.bz2 && \
    chmod +x restic && \
    mv restic /usr/local/bin/

# Install gcloud CLI
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | tee /usr/share/keyrings/cloud.google.gpg && \
    apt-get update -y && apt-get install google-cloud-sdk -y
      

ENTRYPOINT [ "restic" ]