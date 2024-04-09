
![[Pasted image 20240113005128.png]]

Control plane: ambiente de gerenciamento K8s, ele gerencia os workers. Dentro do control plane temos alguns componentes muitos importantes, que dão a característica de alta disponibilidade e tolerância a falhas.

Kube API server: servidor de API do K8s, ele serve para expor a camada do K8s, (API) é a partir dessa API que nos nos comunicamos com o kubernetes, ele é escalonavel horizontalmente, quer dizer que ele pode ser escalado com a implementação de mais instâncias. Para ter mais tolerância a falhas.

Cloud controller manager: executa os controladores específicos para o provedor de nuvem, ali esta a lógica para o kubernetes conversar com a nuvem. Ela vincula o seu Cluster com a API da cloud específicada e separa os componentes que interagem com a cloud, a partir dos componentes que interagem com o Cluster. (serviço opcional)

Kube Controller manager: sempre necessito dele para que ele execute os processos de controlador. Ele é o cérebro da orquestração (caso de uso: imagine que um worker node caiu, ele vai tentar subir em um outro worker ou até nele mesmo. Ele vai fazer o possível para a aplicação não parar.) 

ETCD: o banco de dados do tipo chave e valor, é opensource tolerante a falhas. Ele não é exclusivo do kubernetes. Ele funciona como um repositório que armazena todos os dados do Cluster. Ele é totalmente distribuído. (redundância)

Kube-proxy: implementação de um proxy de rede que roda em cada node dentro do Cluster, ele viabiliza a comunicacao com os pods (pods são onde se encontram os containers) ou seja, ele vai atuar na comunicação de rede, dentro e fora do Cluster. Dentro do K8s temos uma implementação de rede, proxy, dns, e por que? Por que o Cluster é muito distribuído por ex eu posso ter uma parte da aplicação rodando em cloud e outra localmente. Nesse caso, como que ele encontra estas maquinas? Através do proxy, junto com o dns do K8s que vai viabilizar toda essa comunicação na hora que o cliente acessar uma aplicação no nosso site.

Recurso Pods: é um recurso que armazena um grupo de containers, é indicado usarmos 2 contêiners dentro de um pod, mas se houver necessidade pode alocar mais. Eles compartilham armazenamento de rede, especificações de como executar containers. 

Por exemplo:

![[Pasted image 20240113011532.png]]
Imagine que ali em pod temos a primeira linha onde existem 3 containers, o primeiro é um Ngnix, o segundo um debian e o terceiro um SQL, em baixo é um server tomcat. Cada um executado separadamente dentro de um contêiner, o pod não executa a aplicação, ele somente contem os containers para fazer a orquestração.

Kube-scheduller: ele observa os pods recém criados sem nenhum node atribuído. Sendo assim, ele ira selecionar um node para executa-ló. O que ele leva em conta para fazer essa distribuição de pods? Por exemplo, o pod 1 vai para o node A, o pod 2 vai lá pro node B. Ele leva uma grande quantidade de informações de pré requisitos para tomar essas decisões, entre elas os principais estão:
- os recursos individuais 
- Recursos coletivos
- Recursos de hardware
- Recursos de software 
- Política de permissao
- localidade dos dados
- Se vai haver interferências entre cargas de trabalho 

Ele não vai sair selecionando aleatoriamente.
Se um node esta sobrecarregado, o schedulle vai ver isso e vai alocar em outro POD.

Kubelet: agente que executa dentro dos workers, ele garante que os containers estejam sendo executados dentro do pod, não podemos executar nenhum containers fora do pod. Ele garante isso. Ele utiliza um recurso chamado PodSpecs, para ver se a execução do pod esta correta.
O kubelet só gerencia containers criados pelo kubernetes.


Container runtime interface (CRI): é uma interface de plugin que vai habilitar nosso kubelet a usar uma variedade de container runtimes, mas por que preciso disso? O K8s não executa nenhum container, o kubelet entra em contato com o runtime, e o runtime é quem vai executar os containers.

![[Pasted image 20240113013450.png]]
Basicamente eu preciso ter meu kubelet, ter um runtime compatível com OCI e meus containers.







