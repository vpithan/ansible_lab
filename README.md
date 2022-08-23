# ansible_lab

Projeto responsavel por documentar os estudos da ferramenta ansible.

#### SSH

É necessário por a chave key.pub no arquivo **/home/vagrant/.ssh/authorized_keys** assim conseguimos executar o playbook sem senha.

#### Playbooks

Ex:

```sh
ansible-playbook --private-key ~/.ssh/key -i inventory.ini playbooks/install_nginx.yml 
```