# Node.js公式イメージを使用
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:18

# ユーザーとグループIDを設定（非rootで実行するため）
ARG USERNAME=node
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# 作業ディレクトリの設定
WORKDIR /workspace

# 必要な依存関係をコピー
COPY package.json ./
COPY pnpm-lock.yaml ./

# 権限問題を防ぐため、必要なディレクトリを事前作成し適切な権限を付与
RUN mkdir -p /workspace/node_modules && \
    chown -R $USER_UID:$USER_GID /workspace /usr/local/share/npm-global /home/$USERNAME && \
    chmod -R 755 /workspace /usr/local/share/npm-global /home/$USERNAME

# 必要なディレクトリを作成し、適切な権限を付与
RUN mkdir -p /workspace/.pnpm-store && \
    chown -R $USERNAME:$USERNAME /workspace/.pnpm-store && \
    chmod -R 755 /workspace/.pnpm-store

# `pnpm` をグローバルインストール
RUN npm install -g pnpm --unsafe-perm

# 必要な依存関係をインストール
RUN pnpm add bcryptjs

# `pnpm install` 実行 (ネットワーク安定性を考慮したオプション付き)
RUN pnpm install --network-concurrency 1 --loglevel warn

# アプリケーションポートを公開
EXPOSE 3000
