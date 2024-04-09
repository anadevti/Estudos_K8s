É responsável por fazer a implantação da aplicação 
Por default o k8s rolling updates ou rolling release, que executa uma atualização baseada em um percentual de indisponibilidade de pods. Por default temos no máximo 25% dê indisponibilidade do total de pods que voce tem. Por exemplo, caso eu tiver 4 pods associados a 1 deployment a atualização será feita de um por um, ou seja no mínimo eu terei 75% do status dos meus pods running.

Recreaste deployment: não é muito recomendado utilizar. Pois ele para todas as suas pods e então subir todas as pods com a versão nova da sua aplicação. 

Rollback: voltar ao estado que estava anteriormente.

![[Pasted image 20240117153603.png]]
Nesse diagrama é possível identificar que temos os usuários onde eles acessam o load balancer e ele ira distribuir os usuários para cada uma das aplicações rodando dentro de pods. O ponto é que o k8s vai verificar quais das pods tem menos usuários, se preocupando com a disponibilidade da aplicação. Por exemplo, se vai haver uma atualização ele comeca Pelas pods onde tem menos usuários utilizando, isso mostra ali embaixo no lado esquerdo. Vale lembrar que neste método, se no primeiro pod começar dar ruim ele já para e não derruba os próximos pods.