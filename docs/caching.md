# Caching 

## Introdução
O caching é uma técnica essencial para sistemas que precisam escalar enquanto
mantêm baixa latência e alta performance. Ao armazenar temporariamente os
dados mais requisitados em locais de acesso rápido, como memória volátil, o
caching reduz significativamente a carga em bancos de dados e sistemas
subjacentes. Essa abordagem é vital para aplicações modernas que atendem
milhões de requisições simultâneas, como e-commerces, serviços de streaming
e redes sociais.
Segundo Newman (2014) em Building Microservices, o caching é um dos pilares
para garantir sistemas responsivos e eficientes, especialmente em arquiteturas
baseadas em microserviços.


## O Que é Caching?
Caching refere-se ao processo de armazenamento de cópias temporárias de
dados ou resultados de operações em um local de acesso mais rápido do que a
origem dos dados. Quando uma aplicação solicita uma informação, o sistema
verifica se ela está disponível no cache:
1. Cache Hit: Os dados são encontrados e retornados rapidamente.
2. Cache Miss: Os dados precisam ser recuperados da fonte original e,
opcionalmente, armazenados no cache para futuras consultas.
O caching é utilizado para dados estáticos (como imagens) e dinâmicos (como
resultados de consultas SQL ou APIs).


## Tipos de Caches
1. Cache de Memória:
    * Utiliza a memória RAM para armazenar dados temporários.
    * Exemplos: Redis, Memcached.
    * Vantagem: Altíssima velocidade de leitura e escrita.
    * Limitação: Dados podem ser perdidos em reinicializações, pois a
      memória é volátil.
2. Cache de Disco:
    * Armazena dados no disco local para acesso rápido.
    * Exemplos: Varnish Cache, sistemas de caching de navegador.
    * Vantagem: Persistência dos dados mesmo após reinicializações.
    * Limitação: Mais lento em comparação ao cache em memória.
3. Cache Distribuído:
    * Caches replicados em diferentes nós para escalabilidade horizontal.
    * Exemplos: Redis em cluster.
    * Vantagem: Alta disponibilidade e escalabilidade para sistemas
      distribuídos.
4. Cache em CDNs (Content Delivery Network):
    * Armazena conteúdo estático (como imagens e vídeos) em servidores
      distribuídos geograficamente.
    * Exemplos: Cloudflare, AWS CloudFront.
    * Vantagem: Reduz latência, especialmente para usuários em diferentes
      regiões.


## Benefícios do Caching
1. Redução de Latência:
    * Respostas rápidas para dados acessados frequentemente,
      melhorando a experiência do usuário.
2. Alívio de Carga no Banco de Dados:
    * Minimiza consultas repetitivas, liberando recursos para outras
      operações críticas.
3. Redução de Custos:
    * Menor uso de processamento e de infraestrutura, especialmente em
      sistemas que operam em nuvem.
4. Escalabilidade:
    * Permite que sistemas lidem com picos de tráfego sem comprometer a
      performance.


## Estratégias de Caching
1. Write-Through Cache:
• Atualiza o cache sempre que os dados são alterados no banco de
dados.
• Vantagem: O cache sempre reflete os dados mais recentes.
• Limitação: Introduz uma pequena latência em operações de escrita.
2. Write-Back Cache:
• Atualiza o banco de dados apenas quando o dado armazenado no
cache é modificado.
• Vantagem: Escritas mais rápidas.
• Limitação: Risco de perda de dados em caso de falha no cache.
3. Cache Invalidation:
• Estratégia para remover ou atualizar dados obsoletos no cache.
• Métodos:
o TTL (Time-to-Live): Define um tempo de vida para os dados no
cache.
o Invalidation Manual: O sistema identifica alterações e remove os
dados do cache.
o Lazy Loading: Atualiza os dados no cache apenas quando
solicitados.
4. Cache-aside Pattern:
• A aplicação verifica o cache primeiro. Em caso de "miss", busca no
banco de dados e atualiza o cache.
• Vantagem: Simplicidade de implementação.
• Limitação: Possibilidade de dados desatualizados no cache


## Estudo de Caso: Netflix
A Netflix utiliza caching extensivamente para entregar conteúdo com baixa
latência para seus usuários. Segundo um estudo publicado pela equipe técnica
da empresa:
• Cache CDN: Arquivos de vídeo e imagens são armazenados em CDNs
distribuídas para otimizar a entrega global.
• Cache Local: Dados relacionados a perfis de usuários e recomendações
são armazenados em cache local para respostas instantâneas.
Com essa estratégia, a Netflix conseguiu reduzir a latência média global em até
80%, garantindo uma experiência consistente mesmo em regiões de baixa
conectividade.


## Implementação Prática
No contexto de um e-commerce, o caching pode ser implementado para otimizar
diferentes aspectos do sistema:
1. Produtos Mais Vendidos:
o Produtos com alta procura podem ter seus detalhes armazenados
em cache, evitando consultas frequentes ao banco de dados.
2. Carrinhos de Compras:
o Armazena temporariamente as informações do carrinho,
proporcionando uma experiência de compra rápida e consistente.
3. Páginas Estáticas:
o A página inicial e páginas de categorias podem ser carregadas
diretamente do cache, reduzindo o tempo de carregamento para os
usuários.


## Desafios e Limitações
1. Coerência de Dados:
• Garantir que os dados armazenados no cache estejam atualizados é
um desafio, especialmente em sistemas dinâmicos.
2. Armazenamento Limite:
• Memória de cache tem capacidade limitada, exigindo estratégias para
priorizar os dados mais importantes.
3. Impacto em Caso de Cache Miss:
• Um grande número de falhas no cache pode sobrecarregar o banco
de dados e o sistema.
4. Dependência de Cache:
• Sistemas altamente dependentes de cache podem enfrentar sérios
problemas em caso de falhas ou invalidações mal gerenciadas.


## Ferramentas e Tecnologias de Caching
• Redis: Ideal para caching em memória em alta escala, com suporte a TTL
e replicação.
• Memcached: Simples e eficiente para cenários de leitura intensiva.
• Cloudflare: Usado para caching em CDN, reduzindo latência para
conteúdo estático.
• Varnish Cache: Focado no cache de páginas web para acelerar o
carregamento.


## Benchmarks e Estudos Relevantes
Um benchmark conduzido pela equipe do Redis Labs mostrou que o uso de
Redis em sistemas distribuídos:
• Aumentou a capacidade de processamento em até 200% para sistemas
com alta concorrência.
• Reduziu o tempo de resposta médio em aplicações de e-commerce para
menos de 50ms.


## Conclusão
O caching é uma técnica indispensável para sistemas que precisam escalar e
oferecer respostas rápidas em ambientes de alta demanda. Quando
implementado de maneira eficaz, ele pode transformar a experiência do usuário
e a eficiência do sistema. No entanto, sua aplicação exige planejamento
cuidadoso para evitar problemas como dados desatualizados ou cache
excessivamente dependente de recursos limitados. Integrar o caching com
outras estratégias, como pools de conexão e CDNs, pode maximizar os
benefícios e garantir a escalabilidade sustentável de sistemas modernos.


## Referências
* Newman, Sam. Building Microservices: Designing Fine-Grained Systems.
O'Reilly Media, 2014.
2. Burns, Brendan. Designing Distributed Systems. O'Reilly Media, 2018.
3. Redis Labs. "Redis Performance Benchmarks." Disponível em: Redis
Labs.
4. Netflix Tech Blog. "Scaling Netflix with Caching Strategies." Disponível
em: Netflix Blog.
