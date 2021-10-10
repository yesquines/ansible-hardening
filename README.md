# Palestra: Hardening Automatizado - Aumentando a Segurança de Servidores Linux com Ansible

Palestra que visa mostrar como é possível automatizar as configurações e boas práticas de segurança da informação utilizando o Ansible. Para isso serão apresentados na palestra os conceitos do Ansible e de Hardening identificando quais são os melhores meios para conseguirmos chegar até um Security as a Code que possa ser versionado e que tenha uma manutenção mais rápida. E por fim a apresentação de uma execução prática do Ansible em dois servidores garantido algumas configurações de segurança da informação.

## Slides da Palestra

[Palestra-Ansible_Hardening.pdf][1]

## Laboratório (DEMO)

Para a criação do laboratório é necessário ter pré instalado os seguintes softwares:

* [Git][2]
* [VirtualBox][3]
* [Vagrant][4]
* [Ansible][9]

O Laboratório será criado utilizando o [Vagrant][5]. Ferramenta para criar e gerenciar ambientes virtualizados (baseado em Inúmeros providers) com foco em automação.

### Criação do Laboratório

Para criar o laboratório é necessário fazer o `git clone` desse repositório e, dentro da pasta baixada realizar a execução do `vagrant up`, conforme abaixo:

> A infraestrutura desse laboratório está versionada como código no arquivo [Vagrantfile][6]

```bash
git clone https://github.com/yesquines/ansible-hardening
cd ansible-hardening
vagrant up
```

### Comandos do Vagrant

Para melhor utilização, abaixo há alguns comandos básicos do vagrant para gerencia das máquinas virtuais.

Comandos                | Descrição
:----------------------:| ---------------------------------------
`vagrant init`          | Gera o VagrantFile
`vagrant box add <box>` | Baixar imagem do sistema
`vagrant box status`    | Verificar o status dos boxes criados
`vagrant up`            | Cria/Liga as VMs baseado no VagrantFile
`vagrant provision`     | Provisiona mudanças logicas nas VMs
`vagrant status`        | Verifica se VM estão ativas ou não.
`vagrant ssh <vm>`      | Acessa a VM
`vagrant ssh <vm> -c <comando>` | Executa comando via ssh
`vagrant reload <vm>`   | Reinicia a VM
`vagrant halt`          | Desliga as VMs

> Para maiores informações acesse a [Documentação do Vagrant][7]

## Role Ansible Hardening 

A role desse repositório foi criada com o intuito de apresentar um Hardening básico para ambientes Linux. Sua organização está dentro da pasta [roles][7] com a seguinte arquitetura:

```bash
└── ansible-hardening
    ├── defaults
    │   └── main.yml
    ├── handlers
    │   └── main.yml
    ├── README.md
    ├── tasks
    │   ├── disable_unsed_fs_net.yml
    │   ├── limits.yml
    │   ├── login_defs.yml
    │   ├── main.yml
    │   ├── misc.yml
    │   └── ssh_configuration.yml
    ├── templates
    │   ├── login.defs.j2
    │   ├── ssh_config.j2
    │   └── sshd_config.j2
    └── vars
        └── main.yml
```

A role fará a configuração de boas práticas de securança nos servidores provisionados pelo Vagrant, por isso sua execução pode ser realizada seguinte o comandos abaixo:

```bash
ansible-galaxy colletion install ansible.posix community.general
ansible-playbook hardening_role.yml
```

[1]: ./Palestra-Ansible_Hardening.pdf
[2]: https://git-scm.com/downloads
[3]: https://www.virtualbox.org/wiki/Downloads
[4]: https://www.vagrantup.com/downloads
[5]: https://www.vagrantup.com/
[6]: ./Vagrantfile
[7]: https://www.vagrantup.com/docs
[8]: ./roles/
[9]: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
