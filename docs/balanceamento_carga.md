# Distribuindo Demandas para Escalabilidade e Confiabilidade

## Introdução

O balanceamento de carga, ou ***load balancing***, é uma técnica crítica para
distribuir eficientemente as requisições entre múltiplos servidores, assegurando
que nenhum servidor seja sobrecarregado. Isso aumenta a disponibilidade e a
performance do sistema, essencial em cenários de alta demanda. O
balanceamento de carga é fundamental para arquiteturas escaláveis e
resilientes, como em grandes e-commerces, plataformas de mídia e serviços de
streaming.De acordo com Tanenbaum & Steen (2006) em Distributed Systems: Principles
and Paradigms, o balanceamento de carga é vital para garantir a distribuição
equitativa de tarefas em sistemas distribuídos, melhorando a performance e a
tolerância a falhas.


## O Que é Balanceamento de Carga?

O balanceamento de carga envolve a distribuição de requisições de clientes
entre múltiplos servidores. Um load balancer atua como um intermediário,
recebendo todas as requisições e distribuindo-as de acordo com algoritmos
específicos. Isso evita que qualquer servidor individual fique sobrecarregado,
melhorando a disponibilidade e a performance.


## Componentes do Balanceamento de Carga

1. Servidores Backend:
    * Servidores que processam as requisições enviadas pelo load
      balancer.
    * Podem ser instâncias de uma aplicação ou serviços distintos.
2. Load Balancer:
    * O ponto de entrada único para o sistema, responsável por distribuir as
      requisições.
3. Algoritmos de Balanceamento:
    * Determinam como as requisições são distribuídas entre os servidores.


## Tipos de Balanceamento de Carga
1. Baseado em Hardware:
    * Dispositivos dedicados que gerenciam o tráfego de rede.
    * Exemplo: F5 Big-IP, Cisco ACE.
    * Vantagem: Alta performance e segurança.
    * Limitação: Alto custo e menor flexibilidade.
2. Baseado em Software:
    * Implementações de software que rodam em servidores comuns.
    * Exemplos: Nginx, HAProxy, Traefik.
    * Vantagem: Flexibilidade e baixo custo.
    * Limitação: Pode ter performance limitada em comparação aos
      dispositivos de hardware.
3. Balanceamento de Carga DNS:
    * Distribui requisições ao nível de DNS, direcionando clientes para
      diferentes servidores com base em regras de DNS.
    * Exemplos: Amazon Route 53, Cloudflare.
    * Vantagem: Simplicidade e independência de infraestrutura.
    * Limitação: Menor controle e atualização mais lenta de informações de
      balanceamento.


## Algoritmos de Balanceamento
1. Round Robin:
    * Requisições são distribuídas ciclicamente entre os servidores.
    * Simples e eficiente em cargas uniformes.
2. Least Connections:
    * Direciona a requisição para o servidor com menos conexões ativas.
    * Ideal para sistemas onde o tempo de processamento varia entre
      requisições.
3. Weighted Round Robin:
    * Cada servidor recebe um peso, e requisições são distribuídas
      proporcionalmente.
    * Útil quando servidores têm capacidades de processamento diferentes.
4. IP Hash:
    * Direciona as requisições com base no hash do endereço IP do cliente.
    * Garante consistência, útil para sessões que dependem de um servidor
      específico.
5. Health Check:
    * O load balancer verifica regularmente a saúde dos servidores.
    * Requisições não são enviadas para servidores com falhas ou
      problemas.


## Benefícios do Balanceamento de Carga
1. Alta Disponibilidade:
    * Requisições podem ser redirecionadas automaticamente em caso de
      falhas.
2. Melhor Performance:
    * Evita sobrecarga em um único servidor, garantindo tempos de
      resposta consistentes.
3. Escalabilidade Horizontal:
    * Permite adicionar mais servidores conforme necessário, atendendo a
      um maior número de usuários.
4. Confiabilidade:
    * Redundância incorporada, minimizando o impacto de falhas
      individuais.


## Ferramentas e Tecnologias
1. Nginx:
    * Amplamente usado como balanceador de carga reverso.
    * Suporta balanceamento baseado em round robin e least connections.
2. HAProxy:
    * Ferramenta de alto desempenho para balanceamento de carga em
      camadas L4 (TCP) e L7 (HTTP).
3. AWS Elastic Load Balancer:
    * Balanceador de carga gerenciado na nuvem da AWS.
    * Oferece integração nativa com outros serviços da AWS.
4. Traefik:
    * Ideal para ambientes baseados em contêineres, como Docker e
      Kubernetes.


## Estudo de Caso: A Amazon
A Amazon, uma das maiores plataformas de e-commerce do mundo, utiliza
extensivamente balanceamento de carga para garantir alta disponibilidade e
desempenho:
* Global Traffic Management:
    - o Utiliza balanceamento de carga DNS para direcionar tráfego para
          diferentes regiões, garantindo baixa latência e alta disponibilidade
          global.
* Elastic Load Balancing:
    - o O AWS ELB distribui automaticamente o tráfego de entrada entre
          várias instâncias do EC2, escalando conforme necessário para
          lidar com picos de tráfego.
Essa abordagem permitiu que a Amazon mantivesse um serviço rápido e
confiável, mesmo durante eventos de alta demanda como Black Friday e Prime
Day.


## Cenário Prático: Um E-commerce
Imagine um e-commerce que precisa lidar com altos volumes de tráfego durante
promoções:
1. Problema Inicial:
o Um único servidor atende todas as requisições, resultando em
lentidão e falhas durante picos de tráfego.
2. Solução com Load Balancer:
o Implementação de um balanceador de carga (Nginx) para
distribuir requisições entre múltiplos servidores backend.
o Configuração de health checks para monitorar a saúde dos
servidores e redirecionar tráfego em caso de falhas.
3. Resultados:
o Aumento de 80% na capacidade de processamento de
requisições.
o Redução significativa no tempo de resposta e eliminação de
falhas durante picos de acesso.


## Conclusão
O balanceamento de carga é uma técnica indispensável para garantir a
escalabilidade, performance e disponibilidade de sistemas modernos. Ele
permite que aplicações lidem com grandes volumes de tráfego e mantenham
uma experiência de usuário consistente, mesmo durante picos de demanda.
Ferramentas como Nginx, HAProxy e AWS ELB oferecem soluções robustas e
flexíveis para implementação de balanceamento de carga. Contudo, sua
aplicação exige planejamento cuidadoso e monitoramento contínuo para
assegurar que os benefícios sejam maximizados.


## Referências
* Tanenbaum, Andrew S.; Steen, Maarten Van. Distributed Systems:
Principles and Paradigms. Pearson, 2006.
* Nginx Documentation: Load Balancing. Disponível em: Nginx Docs.
* HAProxy Documentation. Disponível em: HAProxy.
* AWS Elastic Load Balancing. Disponível em: AWS ELB