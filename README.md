# zabbix-appliance-aws

Este repositório contém as instruções para subir um container com Zabbix instalado em uma instância AWS, utilizando a aplicação Zabbix Appliance.

## Descrição

O Zabbix é uma ferramenta de monitoramento de rede e aplicações de código aberto. Neste projeto, configuramos o Zabbix Appliance em um ambiente de nuvem utilizando a Amazon Web Services (AWS).

## Pré-requisitos

- Conta na AWS
- Acesso ao AWS Management Console
- Conhecimento básico em AWS EC2 e Docker

## Passo a Passo

### 1. Configuração da Instância EC2

1. Faça login no AWS Management Console.
2. Navegue até a seção **EC2** e clique em **Launch Instance**.
3. Escolha uma Amazon Machine Image (AMI) apropriada (por exemplo, Ubuntu 20.04 LTS).
4. Selecione o tipo de instância de acordo com suas necessidades (t2.micro para fins de teste é suficiente).
5. Configure as configurações da instância, como rede e segurança, garantindo que a porta 10050 e 10051 (usada pelo Zabbix) e a porta 80 (HTTP) estejam abertas.
6. Revise e lance a instância.

### 2. Instalação do Docker

1. Conecte-se à sua instância EC2 via SSH.
2. Atualize o sistema:

    ```sh
    sudo apt update
    sudo apt upgrade 
    ```

3. Instale o Docker:

    ```sh
    sudo apt install docker.io 
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

4. Verifique a instalação do Docker:

    ```sh
    docker --version
    ```

### 3. Baixando e Executando o Zabbix Appliance

1. Baixe a imagem do Zabbix Appliance:

    ```sh
    docker pull zabbix/zabbix-appliance
    ```

2. Execute o container do Zabbix Appliance:

    ```sh
    docker run --name zabbix-appliance -d -p 80:80 -p 10051:10051 zabbix/zabbix-appliance
    ```

### 4. Acessando a Interface do Zabbix

1. Obtenha o endereço IP público da sua instância EC2 no AWS Management Console.
2. No seu navegador, acesse `http://<IP-PUBLICO-DA-SUA-EC2>`.
3. Você deve ver a página de login do Zabbix. Use as credenciais padrão para fazer login:
    - Usuário: Admin
    - Senha: zabbix

### 5. Configurações Adicionais

- Após o primeiro login, é recomendado mudar a senha padrão do usuário `Admin` por questões de segurança.
- Configure os hosts e os parâmetros de monitoramento de acordo com suas necessidades específicas.

## Contribuições

Sinta-se à vontade para contribuir com este repositório enviando pull requests. Qualquer feedback ou melhoria será bem-vindo!

