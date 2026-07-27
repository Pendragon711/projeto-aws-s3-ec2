# Projeto AWS — Implementação de servidor web utilizando Amazon S3 e Amazon EC2

## Visão geral

Este projeto foi desenvolvido com o objetivo de praticar conceitos de computação em nuvem utilizando a plataforma AWS.

A implementação envolveu a criação de uma infraestrutura básica utilizando Amazon S3 para armazenamento de arquivos, Amazon EC2 para provisionamento de uma máquina virtual e configuração de um servidor web automatizado através de um script de inicialização (User Data).

O projeto aborda conceitos fundamentais de Cloud Computing, infraestrutura como serviço (IaaS), redes virtuais e automação de recursos na nuvem.
## Arquitetura do projeto

A arquitetura desenvolvida utiliza serviços AWS integrados para armazenamento, computação, rede e controle de acesso.

Serviços utilizados:

- **Amazon S3**
  - Armazenamento do arquivo `user-data.txt`.
  - Gerenciamento de objetos dentro do bucket.

- **Amazon EC2**
  - Provisionamento da máquina virtual.
  - Execução do servidor web.

- **Amazon VPC**
  - Configuração da rede virtual da infraestrutura.
  - Definição da sub-rede utilizada pela instância.

- **Security Groups**
  - Controle das regras de entrada e saída da instância.
  - Liberação de acesso HTTP através da porta 80.
  
  ## 1. Amazon S3 — Armazenamento do script de inicialização

Foi utilizado o serviço **Amazon S3 (Simple Storage Service)** para armazenar o arquivo `user-data.txt`, que contém o script utilizado posteriormente durante a configuração automática da instância EC2.

O bucket foi utilizado como repositório de armazenamento do arquivo de configuração, permitindo sua utilização durante o processo de provisionamento da infraestrutura.

### Criação do bucket S3

Foi criado um bucket no Amazon S3 para armazenamento dos objetos utilizados no projeto.

![Bucket S3](imagens/01-s3-bucket.png)

### Arquivo armazenado no bucket

Dentro do bucket foi disponibilizado o arquivo `user-data.txt`, contendo o script de inicialização utilizado pela instância EC2.

![Objeto S3](imagens/03-s3-objeto-user-data.png)

## 2. Amazon EC2 — Provisionamento da instância

Foi realizada a criação de uma instância **Amazon EC2 (Elastic Compute Cloud)** para disponibilizar o ambiente computacional responsável pela execução do servidor web.

A instância foi configurada utilizando uma imagem Amazon Linux e recursos adequados para um ambiente de laboratório e testes.

### Configuração inicial da instância

Durante a criação da instância foram definidos os seguintes parâmetros:

- Sistema operacional: **Amazon Linux 2023**
- Tipo de instância: **t3.micro**
- Região: **us-east-1 (N. Virginia)**
- Zona de disponibilidade: **us-east-1a**

![Criação da instância EC2](imagens/05-ec2-criacao.png)

### Seleção da AMI

Foi utilizada a imagem:

**Amazon Linux 2023 kernel-6.1 AMI**

Essa imagem foi escolhida como sistema operacional base para a execução do servidor.

![AMI Amazon Linux](imagens/06-ec2-ami-nome.png)

### Escolha do tipo de instância

Foi selecionada a instância:

**t3.micro**

Essa configuração fornece recursos computacionais adequados para aplicações de baixo consumo e ambientes de testes.

![Tipo de instância t3.micro](imagens/07-t3-micro.png)

## 3. Configuração de rede e segurança

A instância EC2 foi configurada dentro de uma infraestrutura de rede utilizando **Amazon VPC (Virtual Private Cloud)**.

Foram definidos a VPC, a sub-rede e as regras de acesso necessárias para permitir a comunicação com o servidor web.

### Configuração da VPC

Foi utilizada a VPC:

**LabVPC**

A VPC é responsável por fornecer o ambiente de rede isolado onde os recursos AWS são executados.

![Configuração da VPC](imagens/09-vpc.png)

### Configuração da sub-rede

A instância foi provisionada em uma sub-rede localizada na Zona de Disponibilidade:

**us-east-1a**

![Configuração da sub-rede](imagens/10-subnet.png)

### Configuração do Security Group

Foi criado um grupo de segurança para controlar o tráfego de entrada da instância.

Configuração aplicada:

- Nome: **Lab-SG**
- Regra de entrada: **HTTP**
- Porta liberada: **80/TCP**

Essa configuração permite o acesso ao servidor web através do protocolo HTTP.

![Security Group](imagens/11-security-group.png)

## 4. Armazenamento e automação da instância

### Configuração de armazenamento

A instância EC2 foi configurada utilizando um volume **Amazon EBS (Elastic Block Store)** para armazenamento persistente.

Configuração utilizada:

- Tipo de volume: **gp3**
- Capacidade: **8 GiB**

O Amazon EBS fornece armazenamento persistente que permanece associado à instância EC2 durante seu ciclo de vida.

![Configuração de armazenamento EBS](imagens/12-armazenamento-ebs.png)

---

### Automação utilizando EC2 User Data

Durante a criação da instância foi configurado o recurso **EC2 User Data**.

O arquivo `user-data.txt`, armazenado anteriormente no Amazon S3, foi utilizado como script de inicialização para automatizar a configuração do ambiente.

O script é executado durante o primeiro boot da instância e realiza a instalação e configuração do servidor web automaticamente.

![Configuração do User Data](imagens/13-user-data-configurado.png)

## 5. Resultado final

Após a conclusão das configurações, a instância EC2 foi provisionada com sucesso e permaneceu em estado de execução.

O ambiente foi configurado com:

- Instância EC2 utilizando Amazon Linux 2023;
- Servidor web configurado automaticamente através de User Data;
- Acesso HTTP habilitado através do Security Group;
- Armazenamento persistente utilizando Amazon EBS.

![Instância EC2 em execução](imagens/15-instancia-running.png)

---

## 6. Conhecimentos aplicados

Durante o desenvolvimento deste projeto foram praticados conceitos fundamentais de computação em nuvem:

- **Amazon EC2** — criação e gerenciamento de máquinas virtuais na AWS;
- **Amazon S3** — armazenamento e gerenciamento de objetos;
- **Amazon VPC** — configuração de redes virtuais na nuvem;
- **Security Groups** — controle de acesso e regras de firewall;
- **Amazon EBS** — armazenamento persistente para instâncias;
- **EC2 User Data** — automação de configuração durante inicialização;
- **Modelo IaaS (Infrastructure as a Service)** — utilização de infraestrutura sob demanda.

---

## 7. Aprendizados

Este laboratório permitiu aplicar na prática o processo de provisionamento de recursos na AWS, desde o armazenamento de arquivos de configuração até a criação e configuração de uma instância EC2.

A atividade reforçou conceitos de arquitetura em nuvem, segurança de rede, automação e integração entre diferentes serviços AWS.