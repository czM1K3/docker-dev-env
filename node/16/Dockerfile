FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG KEYRING=/usr/share/keyrings/nodesource.gpg

RUN apt update \
	&& apt upgrade -y \
	&& apt install -y zsh git build-essential curl wget sudo vim \
	&& chsh root -s /usr/bin/zsh \
    && adduser --shell /usr/bin/zsh vscode \
    && usermod -aG sudo vscode \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

COPY .config/starship/starship /usr/local/bin/starship

COPY .config/.zshrc /root/.zshrc
COPY .config/.zshrc /home/vscode/.zshrc

COPY .config/starship.toml /root/.config/starship.toml
COPY .config/starship.toml /home/vscode/.config/starship.toml

RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | tee "/usr/share/keyrings/nodesource.gpg" >/dev/null \
    && gpg --no-default-keyring --keyring "/usr/share/keyrings/nodesource.gpg" --list-keys \
    && echo "deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_16.x jammy main" | tee /etc/apt/sources.list.d/nodesource.list \
    && echo "deb-src [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_16.x jammy main" | tee -a /etc/apt/sources.list.d/nodesource.list

RUN apt update \
    && apt install -y nodejs \
    && apt clean -y

RUN npm i -g yarn pnpm