# 公式Node.jsイメージを使用
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:18

# コンテナ内の作業ディレクトリを設定
WORKDIR /workspace

# 必要な依存関係をインストールするために必要なファイルをコピー
COPY package.json ./
COPY pnpm-lock.yaml  ./
# pnpmをインストール
RUN npm install -g pnpm

# pnpmを使って依存関係をインストール
RUN pnpm install

# ポート3000を公開
EXPOSE 3000
