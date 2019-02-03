# Ansibleが動作するDockerイメージを作成する
## 環境
- python2.*
- ssh
    - ssh user: root
    - ssh password: Omisoka1231


## Ansibleイメージ作成
- SSH接続
- ansible


Local環境でssh-keygenを用いて鍵を作成し、ansible-imageとcentos-image下に設置する
公開鍵の設置
https://qiita.com/HamaTech/items/21bb9761f326c4d4aa65

```
ssh-keygen -t rsa
scp id_rsa.pub root@centos-ansible:/root/.ssh
```




https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#latest-releases-via-apt-ubuntu


### Ansible Playbook
文法チェック
```
ansible-playbook -i ./ansible/inventory ./ansible/test.yml --syntax-check
```

テスト実行
```
ansible-playbook -i ./ansible/inventory ./ansible/test.yml --check --diff
```

実行
```
ansible-playbook -i ./ansible/inventory ./ansible/test.yml --diff
```



## 参考URL
https://docs.docker.com/engine/examples/running_ssh_service/


## 作成手順
```
$ docker build -t ansible-server .
```

```
$ docker run -d -P --name ansible-server ansible-server
$ docker port ansible-server 22
```


$ docker container stop ansible-server
$ docker container rm ansible-server
$ docker image rm ansible-server