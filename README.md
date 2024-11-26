# redmine-ubuntu-ansible


最小構成でインストールしたUbuntu ServerにRedmineを自動インストールするためのAnsibleプレイブックです。

`ansible-playbook` を実行するだけで、あとはしばらく放置すればインストールが完了します。


## 概要

Ansibleを使ってRedmineを自動インストールするためのプレイブックです。以下のwebサイトで紹介されている手順におおむね準拠しています。

[Redmine 6.0 をUbuntu 24.04 LTSにインストールする手順](https://blog.redmine.jp/articles/6_0/install/ubuntu24/)

## システム構成

* Ansible 2.17.5
* Redmine 6.0
* Ubuntu Server 24.04 LTS
* PostgreSQL 16.4
* Apache (Railsの実行にはPassengerを使用)
* Ruby 3.3.6

## Redmineのインストール手順

インストール直後の Ubuntu Server にログインし以下の操作を行ってください。


### Ansibleと必要パッケージのインストール

[Installing Ansible on specific operating systems — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu) を参考にして Ansible をインストールします。

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

git や [PostgreSQL の操作](https://docs.ansible.com/ansible/latest/collections/community/postgresql/postgresql_db_module.html) で必要なパッケージをインストールします。

```bash
sudo apt update
sudo apt install git python3-psycopg2
```

### playbookのダウンロード

```
git clone https://github.com/farend/redmine-ubuntu-ansible.git
```

### PostgreSQLに設定するパスワードの変更 (推奨)

ファイル `group_vars/redmine-servers` をエディタで開き、 `db_passwd_redmine` を適当な内容に変更してください。これはPostgreSQLのRedmine用ユーザー redmine に設定されるパスワードです。

### playbook実行

下記コマンドを実行してください。Redmineの自動インストールが開始されます。

> [!NOTE]
>
> "BECOME password"にsudoを実行するためのパスワードを入力してください。

```
cd redmine-ubuntu-ansible
ansible-playbook -K -i hosts site.yml
```

10〜20分ほどでインストールが完了します。webブラウザで `http://サーバIPアドレス/redmine` にアクセスしてください。Redmineの画面が表示されるはずです。


## ライセンス

MIT License


## 作者

[ファーエンドテクノロジー株式会社](http://www.farend.co.jp/)
