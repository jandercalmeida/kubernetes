# Deploy cluster kubernetes com Ansible


1. Instale um SO (Debian ou Ubuntu) em quantas máquinas quiser.

2. Configure o arquivo de hosts do seu ansible com grupos de hosts "masters" e "workers", setando o endereço de cada um.

3. No diretório playbooks, crie os respectivos arquivos "k8s-install_kube.yaml" e "k8s-join_worker.yaml"

4. Adapte os itens abaixo conforme seu ambiente:
```
  remote_user: user
  become: yes
  become_method: su
  become_user: root
```

5. Execute a task:

Instale o ambiente kubernets em todos os nodes:<br>
```ansible-playbook k8s-install_kube.yml -k -K```

Acesse o node master e inicie o kubeadm no node master (crie seu arquivo yaml para isso):
```
kubeadm config images pull
kubeadm init --control-plane-endpoint=<IP ou FQDN MASTER> --pod-network-cidr=10.244.0.0/16 | tee kubeadm.init.out
```

Insira os nodes workers no cluster:<br>
```ansible-playbook k8s-join_worker.yml -k -K```
