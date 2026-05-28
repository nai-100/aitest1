# xserver-deploy-template
xserver-deploy-template のリポジトリ

Secret名 | 値の取得場所 | 値の例
SSH_HOST | Xserverサーバーパネル → SSHアカウント → ホスト名 | sv*****.xserver.jp
SSH_PORT | Xserverサーバーパネル → SSHアカウント → 接続ポート| 10022
SSH_USERNAME | Xserverサーバーパネル → SSHアカウント → ユーザー名 | xserver契約時のID
SSH_PRIVATE_KEY | PowerShellで cat ~/.ssh/id_ed25519 | clip を実行してクリップボードにコピー | -----BEGIN OPENSSH PRIVATE KEY----- から始まる文字列

==================================================
SSH鍵ペアの作り方
1. 鍵を生成する
PowerShell（Windows）またはターミナル（Mac）を開いて
ssh-keygen -t ed25519 -C "github-actions"
を実行、その後Enterを3回押す。

2. 公開鍵をXserverに登録する
cat ~/.ssh/id_ed25519.pub | clip
を実行してクリップボードにコピー。
Xserverサーバーパネル → SSH設定 → 公開鍵を登録 → 貼り付けて保存。

3. 秘密鍵をGitHub Secretsに登録する
cat ~/.ssh/id_ed25519 | clip
を実行してクリップボードにコピー。
GitHubリポジトリ → Settings → Secrets and variables → Actions → SSH_PRIVATE_KEYに貼り付けて保存。

注意点
秘密鍵はクラウドに置かない
端末ごとに鍵を作る
Xserverには複数の公開鍵を登録できるから、端末ごとに追加していけばOK
GitHub SecretのSSH_PRIVATE_KEYは新しい端末の秘密鍵で上書き更新する
==================================================
