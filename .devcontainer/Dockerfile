FROM ubuntu:22.04

# インタラクティブモードにならないようにする
ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /app

# 起動シェルをshからbashに変更
SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

## INSTALL R
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg2 \
  wget \
  time \
  tzdata \
  tree \
  git \
  curl \
  python3 \
  python3-pip

  # タイムゾーンの設定
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Install Node.js (using Node.js 19 as an example)
RUN curl -fsSL https://deb.nodesource.com/setup_19.x | bash - && \
    apt-get install -y nodejs

RUN wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc \
  | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc \
  && add-apt-repository -y "ppa:marutter/rrutter4.0" \
  && apt-get update -y \
  && apt-get install -y r-base

# Juliaのバージョンを指定
ENV JULIA_MINOR_VERSION=1.10
ENV JULIA_PATCH_VERSION=5
# Juliaのインストール
RUN wget https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_MINOR_VERSION}/julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    tar -xvzf julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    rm julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    mv julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION} /usr/local/julia && \
    ln -s /usr/local/julia/bin/julia /usr/bin/julia


# atcoder-cliのインストール
RUN npm install -g atcoder-cli@2.2.0

# ojのインストール
RUN pip install online-judge-tools==11.5.1

# # acc configの設定を行う
# RUN acc config default-task-choice all
# RUN acc config template julia

# # atcoderユーザーを作成し、/appディレクトリの所有権を変更
# RUN useradd -m -s /bin/bash atcoder && \
#     chown -R atcoder:atcoder /app

# ユーザーを作成し、ディレクトリの所有権を変更
RUN useradd -m -s /bin/bash atcoder && \
    mkdir -p /home/atcoder/.config && \
    chown -R atcoder:atcoder /home/atcoder/.config && \
    chown -R atcoder:atcoder /app

# ユーザーを切り替える
USER atcoder

# デフォルトシェルをbashに変更
CMD ["/bin/bash"]