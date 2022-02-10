# Rancher

[Site Oficial](https://rancher.com/)

[Documentação Oficial](https://rancher.com/docs/)



## O que é o RANCHER?

* Plataforma para gerenciamento de infraestrutura baseada em contêineres.

* O Rancher é uma ferramenta opensource que serve para administrar uma infraestrutura de containers. Pelo fato dele ser opensource, é possível contribuir com o código, abrir issues ou até mesmo sugerir novas features no GitHub do projeto.

* Ele aborda os desafios operacionais e de segurança do gerenciamento de vários clusters Kubernetes em qualquer infraestrutura, ao mesmo tempo que fornece às equipes de DevOps ferramentas integradas para a execução de cargas de trabalho em contêineres.

* É uma uma plataforma opensource para gerenciar infraestrutura de Docker e Kubernetes em produção, assim como efetuar deploy de apps usando Docker. O deploy pode ser local ou em servers remotos (Digital Ocean, AWS, GCP, Azure entre outros).

### História e evolução

* __2014__ – Inicio do projeto Rancher, um software para simplificar o trabalho com contêineres. 
* __2015__ – Lançamento do primeira versão do Rancher.
* __2016__ – Adoção do Kubernetes como orquestrador.
* __2020__ – Rancher se tornou parte do SUSE.

### Principais componentes do Rancher

__Administração pela UI (User Interface):__ Você pode administrar todo o seu ambiente através da interface dele que é muito simples e intuitiva.

__Ambientes segmentados:__ Através do Rancher é possível criar diversos ambientes para os seus serviços. Em todos os seus ambientes, você vai ter nodes próprios para cada ambiente. Você pode utilizar essa funcionalidade para criar e separar seus ambientes de homologação e produção, por exemplo.

__Catálogo:__ O Rancher possuo um catálogo com inúmeras ferramentas prontas para serem instaladas no seu ambiente de maneira rápida, como por exemplo: Wordpress, Github, ELK, Grafana, Redis, RabbitMQ, MariaDB, MongoDB, entre outras.

__Autenticaçāo:__ Você pode configurar o controle de acesso ao Rancher através de várias ferramentas, como: Windows AD, Azure AD, GitHub, Ping, Keycloak, AD FS, Okta, FreelPA, OpenLDAP e Google.

__Seleçāo de orquestradores:__ Quando você cria um ambiente, tem a opçāo de selecionar o orquestrador que o Rancher deverá utilizar, podendo ser o Kubernetes, Mesos, Docker Swarm ou o Cattle que é o orquestrador nativo do Rancher e inclusive foi o primeiro a ser lançado como opção de orquestrador quando saiu a versāo beta do Rancher.

__Criaçāo de infraestruturas híbridas:__ Você pode adicionar no seu cluster, hosts que estāo em clouds como AWS, DigitalOcean ou Azure, bem como hosts que estāo em qualquer datacenter On-Premisses.

__Serviços:__ Um serviço pode ser 1 ou vários containeres no Rancher.

__Acesso ao container pela interface gráfica:__ Você pode acessar qualquer um dos seus containers através da interface gráfica e também tem acesso aos logs do container, através da funcionalidade View Logs dentro de cada pod.

![image](https://user-images.githubusercontent.com/66180145/153048891-eeb63cc1-b482-421a-a66d-5ecac27d58ef.png)

## Instalação do Rancher

Podemos instalar o Rancher de duas maneiras, Single Node ou HA - 

Vamos trabalhar com o método de instalação __Rancher em um único nó usando o Docker__ [Referência](https://rancher.com/docs/rancher/v2.5/en/installation/other-installation-methods/single-node-docker/)

* Requisitos:

__SO:__ Ubuntu 20.04

__VCPUs:__ 2

__RAM:__ 8 GB

__HD:__ 20 GB


* Laboratório:

|Função|IP|OS|RAM|CPU|
|----|----|----|----|----|
|Master|10.0.0.112|Ubuntu 20.04|16G|2|
|Worker1|10.0.0.56|Ubuntu 20.04|16G|2|
|Worker2|10.0.0.117|Ubuntu 20.04|16G|2|
|Worker3|10.0.0.8|Ubuntu 20.04|16G|2|

```
apt-get update && apt-get -y upgrade
```

### Docker compativel com o Rancher

[Fonte: ](https://rancher.com/docs/rancher/v2.5/en/installation/requirements/installing-docker/)

```
curl https://releases.rancher.com/install-docker/20.10.sh | sh
```

### Desabilitar o Firewall

```
sudo ufw disable
```


### Instalar o Rancher no Master

```
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher:v2.5.11

```
* Aguarde o processo finalizar: 2 ~ 5 minutos.

### Acessando o Rancher

```
http://<IP_DO_SERVIDOR>:8080 ou http://<IP_DO_SERVIDOR>

```

Fazer a configuração de senha e avançar.

### Criando um cluster e adicionando os Workers

1. Em Global, selecione a opção *add cluster* e faça a configuração do seu cluster.

2. Gerar o comando de instalação nos nós *Workers*.

3. Acessar os Workers e executar o comando.

### Instalar o kubectl e acessar o cluster

[Site Oficial](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

* Configurar o acesso ao cluster

```
mkdir -p ~/.kube
nano ~/.kube/config
```

* Colar a configuração do kubeconfig disponível no Rancher/Cluster






### Troubleshooting

Caso você esteja com algum problema para acessar os nós ou durante o processo de inserção de um no no cluster, você pode limpar seu Iptables. Essa prática só é recomendada para laboratórios, em ambientes reias você deve se aprofundar no iptables.

```
iptables -F
iptabels -X

# Reiniciar o docker
systemctl restart docker
# Refazer o processo
```

```
rm -rf /etc/kuberntes/ssl/
```



