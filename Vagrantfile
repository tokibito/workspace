# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  config.ssh.forward_agent = true
  # config.vm.synced_folder "#{Dir.home}/work", "/work"
  config.vm.provision :shell, inline:<<-EOS
    # Add deadsnakes repository
    add-apt-repository -y ppa:deadsnakes/ppa

    # Add Google Cloud SDK Repository
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

    # Add NodeJS repository
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

    # Update package list
    export DEBIAN_FRONTEND=noninteractive
    apt-get update --allow-unauthenticated

    # Generic development
    apt-get install -y \
      tree \
      zip \
      unzip \
      build-essential \
      language-pack-ja-base \
      language-pack-ja

    # Japanese locale
    update-locale LANG=ja_JP.UTF-8

    # Set timezone
    timedatectl set-timezone Asia/Tokyo

    # Python development
    apt-get install -y \
      python3.7 \
      python3.7-dev \
      python3.7-venv

    # NodeJS development
    apt-get install -y nodejs

    # Requirements AppEngine SDK
    apt-get install -y \
      ca-certificates \
      curl \
      git \
      libcurl4-openssl-dev \
      libffi-dev \
      libjpeg-dev \
      libmysqlclient-dev \
      libpng12-dev \
      libpq-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt1-dev \
      libz-dev \
      mercurial \
      wget \
      zlib1g-dev

    # Google Cloud SDK
    apt-get install -y \
      google-cloud-sdk

    # MySQL development
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    apt-get install -y \
      mysql-server \
      mysql-client \
      libmysqlclient-dev

    # ngrok
    if [ ! -e /usr/local/bin/ngrok ]; then
      wget -q https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip -O /tmp/ngrok-stable-linux-amd64.zip
      unzip -o /tmp/ngrok-stable-linux-amd64.zip -d /usr/local/bin/
    fi

    # Google Cloud SQL Proxy
    # if [ ! -e '/usr/local/bin/cloud_sql_proxy' ]; then
    #   wget -q https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O /usr/local/bin/cloud_sql_proxy
    #   chmod +x /usr/local/bin/cloud_sql_proxy
    # fi
  EOS
end
