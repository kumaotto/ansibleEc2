# ansibleEc2

## Ansibleをインストールする
AnsibleにはPython3のインストールが必要なため、入っていなければPython3も入れる。

※ Python
```
brew install python
```

Ansible Intall
```shell
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

## invetoryファイルを作成する
inventoryファイルを作成し、3つのサーバのPublic IPを入力する
/inventory/inventory.ini
```shell
[webservers]
web1 ansible_host=XX.XX.XXX.XXX
web2 ansible_host=XX.XX.XXX.XXX

[dbserver]
db ansible_host=XX.XX.XXX.XXX

[all:vars]
ansible_ssh_user=ubuntu
# ansible_ssh_user=isucon
ansible_ssh_private_key_file=  // プライベートKeyを入力
```

# ubuntuユーザ以外で構成する場合
/roles/*のファイルに存在する `remote_user` の記述を変更する\
→ ユーザ名はコマンドで入力方向で修正中

例) /roles/db/tasks/main.yml
```
- name: "Install MySQL"
  remote_user: ubuntu
  become: True
  command: |
    apt-get -y install mysql-server mysql-client
    
```