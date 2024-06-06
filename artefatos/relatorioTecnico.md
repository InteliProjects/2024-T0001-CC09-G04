# Relatório ténico

Até o momento (17/02/2024), dados históricos referentes ao problema não foram disponibilizados. As análises foram feitas utilizando os dados presentes no Termo de Abertura do Projeto (TAP).

## 1. Análise de dados históricos

Um modelo de ML (Machine Learning) necessita de dados para seu processo de treinamento. Porém, ao estudar esses dados, podem ser extraídos _insights_ que influenciam na modelagem do ambiente, ações do ambiente, ações do agente e recompensas. Aqui estão uma coletânea de observações que podem vir a ser relevantes no momento da modelagem do modelo:

### 1.1. Intervalo de resultados aceitáveis

A solução ótima do problema é alcançar 100% do CDI nos rendimentos anuais. Porém, como se trata de um problema NP-completo, alcançar a solução ótima é muito custoso. Portanto, foi estipulado um intervalo aceitável de erro em torno do 100%, que varia entre 97% e 105% de rentabilidade em relação à taxa DI. Essas informações foram extraídas de conversas com o parceiro de projeto e dos exemplos trazidos no TAPI, onde foi escolhida a taxa de 124% de rentabilidade (em relação ao CDI) dentre três opções, sendo as outras duas muito acima e muito abaixo desse número.

Isso se relaciona com o _target_ do modelo (recompensas).

### 1.2. É preferível um erro para cima do que para baixo

Como citado no item anterior, a margem aceitável está em torno de 97% a 105% de rentabilidade em comparação ao CDI e podemos observar que há uma margem de 3% para baixo e 5% para cima do ideal de 100%. Isso acontece porque o erro pode ser maior para cima do que para baixo, ou seja, uma função de perda pode ser ajustava para contemplar tais fatos e dar menos penalidades para resultados maiores do que 100% do que menores.

Isso se relaciona com a função de perda e treinamento do modelo (modelagem do ambiente e recompensas).

### 1.3. O agente pode quebrar blocos de pontas à vista

Os casamentos demonstrados no TAPI tem uma combinação perfeita em relação à quantidade de ações, ou seja, existe a mesma quantidade de ações à termo e ações à vista em blocos. Porém, como apontado pelo parceiro de projeto em entrevistas realizadas, esses blocos à vista podem ser quebrados em ações unitárias (fracionárias) para tornar viáveis mais opções de casamentos próximos ao ótimo.

Isso se relaciona com ações do agente.

### 1.4. Variação pequena do ambiente

Como de padrão em modelos de aprendizado por reforço, as ações do agente influenciam no ambiente. Porém, após análise de cenários possíveis, foi concluído que o ambiente não terá variações no ambiente que podem surpreender o agente, ou seja, algo que ele não esteja treinado para lidar. Em outras palavras, o abiente sofrerá pequena variação por fatores externos ao agente.

Isso se relaciona com as ações do ambiente e modelagem do ambiente.


## 2. Mapeamento do Ambiente e Elementos-Chave 
A ideia geral do **aprendizado por reforço** é que um agente procura cumprir uma determinada tarefa, inicialmente com um abordagem de tentativa e erro. Posteriormente, os resultados de cada tentativa, independente de seu sucesso, são utilizados para treinar o agente por meio de um sistema de recompensa/punição e determinar se as ações tomadas são válidas ou não. 

### 2.1 Compreendendo Conceitos Fundamentais

- **Agente:** Refere-se a uma entidade, que pode ser um _software_ ou uma combinação de _software_ e _hardware_, responsável por tomar decisões em um ambiente. Ele interage com o ambiente, tomando ações específicas e recebendo recompensas correspondentes. No contexto de _Reinforcement Learning_, o agente é a entidade que aprende com essas interações.

- **Ambiente:** É a representação física ou virtual do problema a ser resolvido. Pode ser tanto real quanto simulado e é o espaço no qual o agente realiza suas ações e interage.

- **Estado:** Refere-se à condição atual do sistema, compreendendo o agente e o ambiente, em um determinado momento. Cada vez que o agente realiza uma ação, o ambiente fornece um novo estado e uma recompensa correspondente.

- **Política:** É a estratégia adotada pelo agente para tomar decisões sobre qual ação executar com base no estado atual do ambiente. A política é continuamente atualizada para buscar um comportamento ideal.

- **Recompensa:** Orienta as ações do agente, sendo utilizada para determinar a política ideal. Se uma ação tomada pelo agente em um estado específico é desejável, a recompensa é positiva; caso contrário, é negativa ou nula.

Para entender melhor o problema, é feito a seguinte modelagem

Diariamente é precificado um ativo chamado 'sintético de renda fixa'. Esse ativo consiste em uma posição vendida em termo de ação, combinada com uma posição comprada na mesma ação, resultando em um ganho definido pela diferença entre o preço do contrato a termo e o da negociação à vista. Essa operação é conhecida como _cash and carry_ ou _basis trading_. O objetivo é encontrar combinações de negociações à vista de ações que correspondam aos contratos a termo, buscando uma rentabilidade próxima a 100% do CDI. Se necessário, ajustamos a estrutura de rentabilidade em função do vencimento do sintético, garantindo uma relação não-decrescente entre vencimento e rentabilidade.

- AGENTE: O agente, no contexto do problema, será o gestor do fundo, responsável por tomar as principais decisões relacionadas aos casamentos das boletas à vista e a termo. Ele é encarregado de encontrar as combinações ideais que maximizem os ganhos do fundo.

- POLÍTICA: A política adotada pelo agente é tomar ações que visem maximizar o ganho do fundo. Isso envolve a tomada de decisões estratégicas sobre quais boletas devem ser casadas, de modo a otimizar os retornos financeiros.

- AMBIENTE: O ambiente consiste no mercado financeiro no qual o fundo opera, incluindo os ativos disponíveis para compra e venda, as condições de mercado e as flutuações nos preços dos ativos.

- AÇÃO: A ação realizada pelo agente é a tomada de decisão sobre quais boletas devem ser casadas. Isso envolve selecionar as combinações de produtos à vista e a termo que oferecem o melhor potencial de retorno para o fundo.

- RECOMPENSA: A recompensa para o agente é alcançada quando ocorre um casamento perfeito de uma boleta, resultando em um retorno que se aproxima o mais possível de 100% do CDI. Quanto mais próximo o retorno estiver desse objetivo, maior será a recompensa para o agente.


### 2.2 Ações que o agente pode realizar
O agente que atua como intermediário entre as operações de venda e compra "Broker", precisa analisar os produtos de compra a vista e venda a termo, e com base nisso buscar um casamento entre estes produtos, de forma que sejam criados agrupamentos de produtos de compra que se complementem e formem o valor de um produto de venda a termo. Este conjunto de produtos deve buscar o mais próximo possível de 100% de CDI.

### 2.3 Como essas ações afetam o ambiente
Esta ação faz com que um produto de renda fixa sintético seja criado, pois como no produto de venda a termo, o pagamento com juros futúros é garantido por parte do vendedor, os compradores tem certeza de que obterão lucros futuros. Mas, como este processo contem muitos passos manuais, é possível que as respostas encontradas não sejam otimizadas e que o tempo de operação seja elevado em muitos casos.

### 2.4 Recompensas associadas a diferentes estados e ações
Ao realizar o casamento entre produtos de compra a vista, o algoritmo pode receber recompensas associadas ao quão próximo do CDI o conjunto de produtos chega.

### 2.5 Importância desse mapeamento para a modelagem
Este mapeamento é fundamental para que seja possível observar o problema de forma abrangente e encontrar formas de definir oque o algoritmo deve buscar otimizar.
