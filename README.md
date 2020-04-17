# Introdução

Guia de funcionamento para peça de recomendação, após a implementação da **Linx Impulse/ShopBack Tag**, 
o sistema de renderização será acionado, e iniciará o processo de construção de inúmeras estruturas que em conjunto compõem
o Overlay **ShopBack**.
>OBS. Após a implementação da tag, todas as configurações são feitas via painel.

Para qualquer overlay ShopBack, a introdução das Peças é feita via [iFrame](#Posicionamento), o Trackeamento é fieto via
tag Tracking, que por sua vez irá executar todo o gerenciamento de coletas para alimentar os feeds do iFrame.

Abaixo segue um descritivo das sessões que compõem esta documentação:

- iFrames
  - [Posicionamento de iFrames](#Posicionamento)
  - [Conteúdo dos iFrames](#Conteúdo)
  - [Comportamento das Peças](#Comportamento)

- Recomendação
  - [Api de Recomendação ShopBack](#recomendação-shopback)
  - [Api de Recomendação Customizada](#recomendação-customizada)
  - [Triagem de dados via html](#triagem-de-dados-via-html)



# Posicionamento

## Fixo

Por padrão todas as peças ShopBack se posicionam fixamente na tela do usuário, variando apenas os critérios para sua execução, sendo estes inúmeros,
de acordo com as necessidades do cliente sendo concebidos dentro de um range composto por quatro regras base.
> OBS. Lembrando que os demais sistemas de posicionamento também se utilizam dessa base para sua execução.


- *Abandono de tela* : Quando há a intenção do cliente de abandonar a página.
- *Tempo de inatividade* : Opera após um tempo definido de total inércia do cliente dentro da página.
- *Skrollar a página*: Ativa após um número definido de Pixels ser skrollado após o marco zero da página.
- *Evento Customizado*: Este se caracteriza por regras mais restritivas, como interações determindas ou critérios singulares, como origens de navegação especificas.

## Dinâmico

Geralmente usado em alertas, ou popups, trabalha com uma colocação dinâmica que varia de página a página, se baseando
em pontos de referência que são determinados via view, que vão determinando as coordenadas de acordo com as necessidades da regra a que se referem.

## Embedado

Apesar de seu nome, todos os sistemas consistem em um mesmo sistema de embedagem via iFrames, _mais informações no tópico de [Conteúdo](#Conteúdo) nessa sessão_,
porém a este se reserva o nome de embedado devido ao fato de ser uma forma de mimetização de elementos dos sites hospedeiros,
como se está fosse parte integral da estrutura mãe, assim o usuário não dependerá de interações especificas para ser impactado.

Este posicionamento consiste em uma seleção com base em um ponto de referência que uma vez determinada seguirá como critério único de coordenadas.
\n\n\n
# Conteúdo

Por questões de consistência e segurança, a ShopBack optou por fazer a implementação de suas peças via
iFrame, pois é uma excelente forma de evitar conflitos de Javascript e CSS, além de não interferir com semânticas de
S&O.

Atualmente nós utilizamos o [Vue.js](https://vuejs.org/), que constituí uma estrutura consisa, e que não compromete o desempenho da
página permitindo a criação de peças mais complexas e efetivas sem efeitos colaterais. 
\n\n\n
# Comportamento

Para que a peça possa alcançar seu intento, nossa tag trabalha com uma serie de trackeamentos via cookie,
e utms, que são gerenciadas pelas regras de interação das peças, e suas funcionalidades, essas 
que podem ser complementadas por eventos do ga, ou por Apis customizadas.
>OBS. Para informações referente a produtos seguir a sessão [recomendação](#recomendação-shopback)



# Recomendação ShopBack

Por padrão a ferramenta ShopBack, usa como base de produtos um XML, no padrão Google Shopping, fornecido pelos nossos
clientes.

Uma vez este fornecido, a nossa ferramenta usa os dados de navegação dos clientes, coletados pela nossa tag, para criar um
sistema de categorização segmentada, que torna o critério do usuário como pilar central para a eleição dos produtos que
a estes serão recomendados.

Vale Ressaltar que essa receita é feita em um ambiente de algoritmos que estão metrificando nossa base em cenários macro 
(todos os usuários), e micro (o usuário em si), para ter uma forma mais assertiva, em tempo real, e, portanto acaba se tornando
um trabalho automatizado que uma vez ativado se retroalimenta de forma autónoma e sem qualquer interação humana (Preferencialmente*).

Essa recomendação pode ser fornecida pela nossa api integrada que pode ser substituída, pois as peças foram criadas,
dentro de uma estrutura robusta o suficiente para tratar essas informações e portanto permitindo essa mesma dinâmica para apis externas,
saiba mais no tópico [Recomendação Customizada](#recomendação-customizada).


###### * Apesar de sua autonômia, alterações podem ser feitas em tempo de execução.
\n\n\n
# Recomendação Customizada

Dentro das estruturas das peças, podemos implementar qualquer api que sigam o padrão HTTP, ou SOAP, que, portanto 
abrangem uma alta gama de possibilidades e necessidades, de acordo com os clientes.

No caso de recomendações externas temos um sistema de triagem dinâmico que pode ser usado sem a necessidade, de se
comunicar com os nossos servidores, pois esses trabalham de forma paralela às peças e, portanto não conseguiriam trabalhar em conjunto
com apis externas*, pois mesmo depois de o cliente ter saído da página nossa recomendação continua trabalhando, em segundo plano,
esperando as próximas interações deste mesmo usuário.

Evidente que isso pode parecer, menos eficiência, porém, as ferramentas ShopBack, trabalham em paralelos, e, portanto,
é possível ter quase a mesma performance utilizando um SDK, restrito as peças que podem criar uma analise,
sofisticada, porém ágil, que irá nos fornecer uma recomendação capaz de ser tão impactante quanto a nossa padrão.

###### *Pode ser feito em casos muito específicos que demandam mais tempo e integrações a nível backend.




# Triagem de dados via html

Como colocado no tópico [Recomendação ShopBack](#recomendação-shopback), nossa tag se utiliza de informações de navegação,
que servem como parâmetro para a criação do range de recomendações. Porém, existem outras formas, via api, ou via html,
que tendem a ser mais simples e, portanto mais fácil de se serem implementadas.

Portanto, uma vez uma página acessada seu HTML fica disponível possibilitando uma triagem com base em analises, de palavras chaves,
dentro do ```<body>``` da página, e que pode se seguir com base em inúmeros critérios, definidos no escopo da campanha, como categoria,
caracterítica, valor, e outros.

>OBS. Essa triagem é feita pela peça e não pela ferramenta, se utilizando do SDK, o mesmo que usamos na [Recomendação Customizada](#recomendação-customizada)
