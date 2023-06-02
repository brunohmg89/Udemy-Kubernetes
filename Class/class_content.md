# Kubernetes - Udemy

## Introdução

- Aula 1: Infraestrutura, Cloud, Microsserviços, Docker e Cluster
    - Explicação sobre o modelo cliente-servidor.
    - Explicação sobre infraestutura
    - Explicação sobre Cloud
    - Explicação sobre virtualização
    - Explicação sobre microsserviços
    - Explicação sobre container
    - Explicação sobre docker
    - Diferença entre virtualização e container
    - Explicação sobre cluster

- Aula 2: O que é Kubernetes
    - Explicação sobre Kubernetes

## Laboratório local de estudos

- Aula 3: Instalando o minikube
    - Explicando sobre o minikube, ferramenta utilizada para usar o kubernetes na máquina local, não recomendado para utilização em ambiente de produção.
    - Site instalação do minikube <https://minikube.sigs.k8s.io/docs/start/>

- Aula 4: Instalando o Docker Desktop

- Aula 5: Instalando o minikube utilizando o virtual box para S.Os mais antigos

- Aula 6: Instalando o Docker, Minikube e kubectl no Linux

## Cluster Kubernetes em Produção (AWS/GCP)

- Aula 7: Arquitetura básica do cluster Kubernetes
    - Componentes do Kubernetes
        - Ao implantar o Kubernetes você obtém um cluster.
        Um cluster Kubernetes consiste em um conjunto de servidores de processamento, chamados nós, que executam aplicações em conteineres. Todo o cluster possui ao menos um servidor de processamento (Worker Node) e um servidor de gerenciamento (Master Node)
        - O que é um cluster Kubernetes?
        Um Kubernetes cluster é um conjunto de nós que executam aplicativos em conteineres
        Kubernetes cluster é um conjunto de máquinas usadas para executar aplicações em conteineres. Quando você executa o Kubernetes, está executando um cluster.
        No mínimo, um cluster contém um plano de controle (Master Node) e pelo menos uma máquina ou nó (Worker Node)
        - O servidor de processamento (Worker) hospeda os Pods que são componentes de uma aplicação. O ambiente de gerenciamento gerencia os nós de processamento e os Pods no Cluster. Em ambientes de produção, o ambiente de gerenciamento é geralmente executado em múltiplos computadores, provendo tolerância a falhas e alta disponibilidade.
    - Componentes da camada de gerenciamento
        - Os componetes da camada de gerenciamento tomam decisões globais sobre o cluster, bem como detectam e respondem aos eventos do cluster.
        Os componentes da camada de gerenciamento podem ser executados em qualquer máquina do cluster. Contudo, para simplificar, os scripts de configuração normalmente iniciam todos os componentes da camada de gerenciamento na mesma máquina.
            - kube-apiserver
            O servidor de API do kubernetes valida e configura dados para os objetos presentes no cluster, que incluem Pods, serviços, controladores de replicação e outros. O API Server atende as operações e fornece o frontend para o estado compartilhado do cluster por meio do qual todos os outros componentes interagem.
            - etcd
            etcd é um armazenamento de valor em cluster. Ele ajuda a viabilizar atualizações automáticas mais seguras, coordena a programação de trabalhos em hosts e ajuda a configurar redes de sobreposição para containers.
            etcd é um componente importante de vários outros projetos. Ele se destaca por ser o armazenamento de dados principal do Kubernetes.
            - kube-scheduler
            kube-scheduler é um processo que atribui Pods a nós. Ele determina quais nós são os posicionamentos válidos para cada Pod na fila de agendamento de acordo com as restrições e os recursos disponíveis. O kube-scheduler então classifica cada Node válido e vincula o Pod a um Node adequado.
            - kube-controller-manager
            No Kubernetes, um controlador é um loop que observa o estado compartilhado do cluster por meio do kube-apiserver e faz alterações tentando mover o estado atual para o estado desejado.
        - Administração da camada de gerenciamento
            - kubeadm: O comando para criar o cluster.
            - kubelet: O componente que executa em todas as máquinas no seu cluster e cuida de tarefas como a inicialização de Pods e contêineres.
            - kubectl: A ferramenta de linha de comando para interação com o cluster.
        - Amazon EKS
        O Amazon Elastic Kubernetes Service é um serviço gerenciado de Kubernetes que descarta a necessidade de instalar e operar a camada de gerenciamento do cluster. Ele é certificado como compatível com o Kubernetes, portanto, você pode migrar qualquer aplicativo com facilidade para o EKS.

- Aula 8: Custos de um Cluster Kubernetes em nuvem (AWS)
    - Mostrando uma estimativa de custos na AWS

- Aula 9: AWS CLI e credenciais de acesso
    - Configurando a AWS CLI e credenciais de acesso
    - Site com a AWS CLI <https://aws.amazon.com/pt/cli/>
    - Configurando Access Key na AWS para conexão com o AWS CLI
        ```aws configure```

- Aula 10: Criando um cluster em nuvem utilizando o AKS
    - Verificando o status de criação do Cluster via AWS CLI
    ```aws eks --region sa-east-1 describe-cluster --name kubernetes-lab --query cluster.status```
    - Atualizar o arquivo de configuração local para que funcione o kubectl no cluster da nuvem (atualizando o arquivo .config dentro do seu user/.kube)
    ```aws eks --region sa-east-1 update-kubeconfig --name kubernetes-lab```

- Aula 11: Adicionando Nodes ao Cluster
    - Criando Nodes dentro do Cluster no EKS
    