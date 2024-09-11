FROM ubuntu:22.04

# インタラクティブモードにならないようにする
ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /app

ENV DEBIAN_FRONTEND=noninteractive LC_ALL=C.UTF-8 LANG=C.UTF-8

# 起動シェルをshからbashに変更
SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
#   software-properties-common \
#   dirmngr \
#   gnupg2 \
#   wget \
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

# # install R
# RUN wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc \
#   | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc \
#   && add-apt-repository -y "ppa:marutter/rrutter4.0" \
#   && apt-get update -y \
#   && apt-get install -y r-base

# install R version specification
# ここでRのバージョンを指定してください
ENV R_VERSION=4.2.1

RUN apt-get update -qq && apt-get -y install --no-install-recommends \
    ca-certificates \
    build-essential \
    gfortran \
    libreadline-dev \
    xorg-dev \
    libbz2-dev \
    liblzma-dev \
    libxml2-dev \
    libcairo2-dev \
    libsqlite3-dev \
    libmariadbd-dev \
    libpq-dev \
    libssh2-1-dev \
    unixodbc-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libsodium-dev \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Download and install R
RUN wget -c https://cran.r-project.org/src/base/R-4/R-${R_VERSION}.tar.gz \
    && tar -xf R-${R_VERSION}.tar.gz \
    && cd R-${R_VERSION} \
    && ./configure \
    && make -j$(nproc) \
    && make install \
    && cd .. \
    && rm -rf R-${R_VERSION} R-${R_VERSION}.tar.gz

# Rのパッケージをインストール
# 必要なRパッケージのバージョン指定インストール
# RUN Rscript -e "install.packages(c('Rcpp', 'stringr', 'purrr', 'magrittr', 'sets', 'dequer', 'zeallot', 'lubridate', 'readr'), \
#         repos = 'https://cloud.r-project.org/', \
#         version = c('1.0.9', '1.5.0', '1.0.1', '2.0.3', '1.0-21', '2.0-2', '0.1.0', '1.9.2', '2.1.4'))"


# Juliaのバージョンを指定
ENV JULIA_MINOR_VERSION=1.9
ENV JULIA_PATCH_VERSION=2
# Juliaのインストール
RUN wget https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_MINOR_VERSION}/julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    tar -xvzf julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    rm julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION}-linux-x86_64.tar.gz && \
    mv julia-${JULIA_MINOR_VERSION}.${JULIA_PATCH_VERSION} /usr/local/julia && \
    ln -s /usr/local/julia/bin/julia /usr/bin/julia

# # Juliaのパッケージを追加する
# RUN julia -e 'using Pkg; Pkg.add(["DataStructures", "DelimitedFiles", "Distributions", "Primes", "OffsetArrays", "Combinatorics", "StaticArrays", "IterTools", "InvertedIndices"])'

# atcoder-cliのインストール
RUN npm install -g atcoder-cli@2.2.0

# ojのインストール
RUN pip install online-judge-tools==11.5.1

# ユーザーを作成し、ディレクトリの所有権を変更
RUN useradd -m -s /bin/bash atcoder && \
    mkdir -p /home/atcoder/.config && \
    chown -R atcoder:atcoder /home/atcoder/.config && \
    chown -R atcoder:atcoder /app

# ユーザーを切り替える
USER atcoder

# デフォルトシェルをbashに変更
CMD ["/bin/bash"]