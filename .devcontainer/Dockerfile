FROM osrf/ros:noetic-desktop-full

# 環境変数を設定
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8

# 基本的なツールをインストール
RUN apt-get update && apt-get install -y \
    sudo \
    lsb-release \
    gnupg \
    curl \
    wget \
    vim \
    git \
    python3-pip \
    # debugのためのツール
    gdb \
    build-essential \
    # X11関連のパッケージ
    x11-apps \
    x11-utils \
    x11-xserver-utils \
    libx11-dev \
    libxext-dev \
    libxrender-dev \
    libxtst-dev \
    libxi-dev

# Gazeboのリポジトリキーとリポジトリを追加
# RUN curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg && \
#     echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null && \
#     apt-get update &&  apt-get install -y  gz-harmonic

# OpenGLとNVIDIA関連のパッケージをインストール
RUN apt-get update && apt-get install -y \
    nvidia-cuda-toolkit \
    libgl1-mesa-glx \
    libgl1-mesa-dri \
    && rm -rf /var/lib/apt/lists/*

# Set up user
ARG UID GID USERNAME GROUPNAME PASSWORD
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER $USERNAME
WORKDIR /home/$USERNAME/workspace

COPY requirements.txt /home/$USERNAME/
RUN pip install --upgrade --no-cache-dir -r /home/$USERNAME/requirements.txt

RUN echo "source /opt/ros/noetic/setup.bash" >> /home/$USERNAME/.bashrc
RUN echo "source ~/workspace/install/setup.bash" >> /home/$USERNAME/.bashrc
USER root
RUN chmod +x /opt/ros/noetic/setup.bash
USER $USERNAME

# エントリーポイントを設定
CMD ["bash"]

