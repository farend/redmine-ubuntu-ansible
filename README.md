# redmine-ansible
公式のredmineのansibleインストーラーが最新バージョンで動作しなかったため修正解決していくついでに関連パッケージの更新やパッケージのそぎ落としをしていく
※ansibleの指定先がlocalhostですのでansibleを実行したサーバーにredmineやその他コンポーネントがインストールされますまたapacheの待ち受けが直下でredmineになります。

## システム構成
* Ubuntu Server 18.04.2 LTS
* PostgreSQL 10
* Apache 2
* ruby 2.5.3
* Redmine 4.0-stable

こちらの数字は設定ファイル等で固定されていますより新しいリリースがあり利用したい場合は別途書き換える必要があります。

### Ansibleとgitのインストール

```
sudo apt update
sudo apt install software-properties-common git
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
環境によっては(初期言語やdocker内など)別途インストールが必要なパッケージ
```
sudo apt install language-pack-ja
```

### playbookのダウンロード
```
git clone https://github.com/16dyui/redmine-ubuntu-ansible.git
```

### PostgreSQLに設定するパスワードの変更 (推奨)
ファイル `group_vars/redmine-servers` をエディタで開き、 `db_passwd_redmine` を適当な内容に変更してください。これはPostgreSQLのRedmine用ユーザー redmine に設定されるパスワードです。

### playbook実行
下記コマンドを実行してください。Redmineの自動インストールが開始されます。
```
cd redmine-ubuntu-ansible
ansible-playbook -K -i hosts site.yml
```
10〜20分ほどでインストールが完了します。webブラウザで `http://サーバIPアドレス` にアクセスしてください。Redmineの画面が表示されるはずです。
