<h1> Atividade 12 - DevSecOps - Linux </h1>

1. Subir uma VM e Instalar um servidor Oracle Linux na ultima versao disponivel;
2. Mudar a VLAN da VM para BRIGDE e fazer os ajustes necessarios;
3. Criar uma apresentação de slides com 1 slide para cada um dos topicos:
3.1 - O que faz o comando systemctl docker status?
3.2 - Onde esta localizado o arquivo de configuração da placa de rede?
3.3 - Qual o comando usado para conectar em outro servidor?
3.4 - O que faz o comando rmdir?
4. Configurar a relação de confiança entre as duas VMs;
5. Fazer o versionamento da atividade;
6. Fazer a documentação explicando o processo de instalação do linux.

INSTALAÇÃO DO LINUX

Para esta atividade usaremos a versão 8.6 da distribuição Oracle. É importante que a instalação seja feita com as seguintes caracteristicas: 

-Minimal Install;
-Fuso horário de acordo com SP;
-Ativação da placa de rede enp0s3;
-Criação de pelo menos 1 usuário.

Após a instalação da VM, faremos o processo de configuração da VLAN, onde mudaremos a adaptação da rede para modo "Bridge" através do próprio gerenciador da VM (no nosso caso o VirtualBox).

Feita as configurações iniciais necessárias, podemos iniciar a maquina virtual e começar preparar o ambiente para a execução da atividade.

O primeiro comando que executamos foi o "yum upadate" onde iremos fazer todas as atualizações disponíveis para nosso sistema. Isso evita uma série de erros de compatibilidade, caso alguma aplicação da nossa máquina esteja desatualizada.

Vamos também preparar a aréa que será responsável pelo versionamento da nossa máquina virtual. Para esta atividade criamos uma pasta dentro do nosso ambiente oracle e nomeamos como "VMV". Para essa pasta, iremos transferir todos os arquivos que iremos modificar e faremos o versionamento a partir da nossa máquina hospedeira. Para isso é necessário que fassamos o compartilhamento da nossa pasta "VMV" para a sistema operacional externo. Usamos o Servidor de arquivos SAMBA do prório Linux. Foi necessário a instalação do app SAMBA através do comando "yum install samba samba-client cifs-utils". Também fizemos modificações necessárias para permissão do compartilhamento da pasta no arquivo "smb.conf" localizado em "/etc/samba/smb.conf". Nesse ponto, fazermos nosso primeiro versionamento da máquiva nomeado como "Versão 1.0 - Servidor SAMBA".

INSTALAÇÃO DO DOCKER

Para cumprir um dos requisitos de demonstração da atividade (3.1 O que faz o comando systemctl docker status?) precisamos fazer a instalação do Docker na nossa VM através de alguns comandos 

"yum install yum-utils" - Que provê o yum config manager para criação do repositório Docker.

"yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo" - seta o repositório para download do Docker.

"yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin" - Instala as dependências do Docker.

Após a intalação faremos o primeiro teste de funcionamento do Docker através do comando "docker run hello-world".

Então demostramos o comando "systemctl status docker"


RELAÇÃO DE CONFIANÇA

Para relação de confiança utilizaremos o SSH (Secure Shell) que é um protocolo usado para fazer login em sistemas remotos de forma segura. 

iremos estabelecer uma relação de confiança entre a "VMPB" e uma nova maquina virtual que chamamos de "relação". Como nas máquinas já estão disponíveis as dependencias do OpenSSH iremos partir apenas paras os comandos de relação. caso não estivessem, precisariamos baixar o OpenSSH através do comando "yum install openssh-server".

no ambiente da "VMPB" iremos digitar o seguinte comando "ssh-keygen -b 1024 -t rsa".

com as chaves pública e privada já criadas, precisamos transferir a chave pública para a máquina na qual queremos fazer a relação. No nosso caso, a VM "relação". Para isso usamos um comando específico para isso "ssh-copy -i ~/.ssh/id_rsa.pub root@192.168.2.112".

Assim temos nossa relação de confiança estabelecida. 
Nesse ponto fazemos 2 versionamentos. Um para os arquivos ssh na "VMPB" (Versão 1.1 - VMPB). E outro para os arquivos de ssh na VM "relação" (Versão 1.1 - VMRelação).





