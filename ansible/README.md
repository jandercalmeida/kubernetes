# Deploy cluster kubernetes com Ansible


Instale um SO (Debian ou Ubuntu) em quantas máquinas quiser.

Configure o arquivo de hosts do seu ansible com grupos de hosts "masters" e "workers", setando o endereço de cada um.

No diretório playbooks, crie os respectivos arquivos "k8s-install_kube.yaml" e "k8s-join_worker.yaml"

Adapte os itens abaixo conforme seu ambiente:
```
  remote_user: user
  become: yes
  become_method: su
  become_user: root
```

Execute a task:
```ansible-playbook k8s-install_kube.yml -k -K```

```ansible-playbook k8s-join_worker.yml -k -K```
