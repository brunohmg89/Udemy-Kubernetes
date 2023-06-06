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
    - Necessário criar role de permissão
    ```kubectl get nodes --watch```

- Aula 12: Criando um cluster em nuvem utilizando GCP
    - Acessando a plataforma do GCP pela primeira vez é necessário instalar o Google Cloud CLI <https://cloud.google.com/sdk/docs/install?hl=pt-br>
    - Instalação de algumas features necessárias
    ```Install-Module GoogleCloud```
    ```Set-ExecutionPolicy RemoteSigned```
    ```gcloud components install gke-gcloud-auth-plugin```
    ```gcloud auth plugin```
    ```gcloud auth list```
    - Ir no projeto, depois no cluster e clicar em conectar ao cluster o mesmo dará a linha de comando necessária para conexão com o cluster.
    ```gcloud container clusters get-credentials MEU-CLUSTER --region REGION --project ID-PROJECT```

## Primeiros passos com Kubernetes

- Aula 13: Implementando um aplicativo
    - O que é um POD
    Um POD do Kubernetes é um conjunto de um ou mais conteineres, sendo a menor unidade de uma aplicação Kubernetes. Os PODs são compostos por um conteiner nos casos de uso mais comuns ou por vários conteineres fortemente acoplados em cenários mais avançados. Os conteineres são agrupados nesses PODs para que os recursos sejam compartilhados de modo mais inteligente.
    - O que é YAML (YML)?
    O YAML é uma linguagem de serialização de dados muito usada na escrita de arquivos de configuração.
    O YAML usa um recuo no estilo Python para indicar o aninhamento. É necessário utilizar espaços em branco porque os caracteres de tabulação não são permitidos. Não há símbolos de formato comuns, como chaves, colchetes, tags de fechamento ou aspas. Os arquivos YAML têm a extensão .yml ou .yaml.
    - Criando o primeiro POD, criação do arquivo pod.yaml
    ```kubectl apply -f .\Code\pod.yaml```
    ```kubectl get pod```

Aula 14: Outro exemplo de criação de um POD
    - Mostrando informações adicionais de um POD
    ```kubectl get pod -o wide```
    - Testando APP pelo minikube
    ```minikube ssh```
    ```curl IP-DO-POD```
    - Apagando POD
    ```kubectl delete pod myapp-html```

Aula 15: Criando um arquivo YAML de Deployment
    - Criando o primeiro arquivode deployment.
    - Alterando a quantidade de replicas.
    - Deletando um POD ele recria automaticamente devido a configuração do Deployment

Aula 16: Mais informações sobre um Deployment
    - Aumentando o numero de POD (replicas) via CLI sem precisar alterar o arquivo de Deployment
    ```kubectl scale deployment app-html-deployment --replicas=10```

Aula 17: Expondo um Deployment
    - Comando para exposição do Deployment via CLI
    ```kubectl expose deployment app-html-deployment --type=LoadBalancer --name=app-html --port=80```
    - Verificando exposição
    ```kubectl get service```
    - Expondo service do minikube (O terminal precisa estar aberto)
    ```minikube service --url app-html```

## Seção Docker + Kubernetes    

Aula 18: Criando uma imagem personalizada
    - Criando o diretório Dockerfile, com arquivo dockerfile e um arquivo html
    - Criando uma imagem do Docker
    ```docker build . -t USUARIO/app-html:1.0```
    - Enviando a imagem para o DockerHub
    ```docker login```
    ```docker push USUARIO/app-html:1.0```

Aula 19: Criando um Deployment de um aplicativo
    - Criando um Deployment usando a imagem do DockerHub criada anteriormente
    ```kubectl apply -f .\App1.0\Kubernetes\app-deployment.yaml```
    ```kubectl expose deploy html-deployment --type=LoadBalancer --name=app-html```
    ```minikube service --url app-html```

Aula 20: Atualizando um aplicativo
    - Criando outro diretório App1.1 alterando o arquivo index.html e fazendo um build da nova imagem
    ```docker build . -t USUARIO/app-html:1.1```
    ```docker push USUARIO/app-html:1.1```
    - Aplicando novo Deployment da versão 1.1 do app
    ```kubectl apply -f .\App1.1\Kubernetes\app-deployment.yaml```
    ```minikube service --url app-html```

Aula 21: Criando um Load Balancer por YAML
    - Criando o arquivo YMAL para a exposição do serviço
    ```kubectl apply -f .\App1.1\Kubernetes\app-html-lb.yaml```
    ```minikube service --url app-html-lb```

## Cluster Kubernetes em produção

Aula 22: Criando um NodePort
    - 
