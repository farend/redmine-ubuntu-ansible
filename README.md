# redmine-ubuntu-ansible


最小構成でインストールしたUbuntu ServerにRedmineを自動インストールするためのAnsibleプレイブックです。

コマンド6個実行するだけで、あとはしばらく放置すればインストールが完了します。


## 概要

Ansibleを使ってRedmineを自動インストールするためのプレイブックです。以下のwebサイトで紹介されている手順におおむね準拠しています。

[Redmine 3.4をUbuntu Server 16.04.2 LTSにインストールする手順](http://blog.redmine.jp/articles/3_4/install/ubuntu/)


## システム構成

* Ansible 2.8.5
* Redmine 4.0
* Ubuntu Server 18.04.3 LTS
* PostgreSQL
* Apache
* Docker


## Redmineのインストール手順

インストール直後の Ubuntu 18.04 にログインし以下の操作を行ってください。


### Ansibleとgitのインストール

```
apt-get update
apt-get install -y sudo
sudo apt-get install -y python-pip libpython-dev git libssl-dev iproute2
sudo pip install ansible\==2.8.5
```

### playbookのダウンロード

```
git clone https://github.com/farend/redmine-ubuntu-ansible.git
```

### PostgreSQLに設定するパスワードの変更 (推奨)

ファイル `group_vars/redmine-servers` をエディタで開き、 `db_passwd_redmine` を適当な内容に変更してください。これはPostgreSQLのRedmine用ユーザー redmine に設定されるパスワードです。

### playbook実行

下記コマンドを実行してください。Redmineの自動インストールが開始されます。

```
cd redmine-ubuntu-ansible
ansible-playbook -K -i hosts site.yml
```

10〜20分ほどでインストールが完了します。webブラウザで `http://サーバIPアドレス/redmine` にアクセスしてください。Redmineの画面が表示されるはずです。


## ライセンス

MIT License


## 作者

[ファーエンドテクノロジー株式会社](http://www.farend.co.jp/)
