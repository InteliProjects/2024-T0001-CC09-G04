---
title: Otimização de Precificação visando alcançar 100% do CDI em Ativos de Renda Fixa Sintética
author: André Luís Lessa Junior, Cristiane Andrade, Giovana Thomé, Leandro Custódio, Mateus Rafael, Mateus Soares de Almeida, Pedro Munhoz de Souza Rivero
date: Fevereiro de 2024
abstract: _The concept of futures contracts traces back to 17th-century Japan, with rudimentary agreements established for rice production in the Dojima rice market. These contracts, as defined agreements between buyers and sellers, entail fulfilling contractual obligations at a predetermined future time. Basis trading, a key strategy within futures contracts, involves speculators aiming to profit from the convergence of spot and futures prices, though it carries inherent risks due to market uncertainties. Additionally, Machine Learning, particularly Reinforcement Learning (RL), offers a promising approach to optimize pricing strategies, such as synthetic fixed income, aiming for 100% CDI profitability. By leveraging RL algorithms grounded in Markov Decision Processes, agents can learn from success and failure to guide future decisions, addressing challenges in complex decision-making processes. This approach presents opportunities to enhance financial decision-making, particularly in balancing profitability and mitigating wealth transfer. Through exploring the application of RL in pricing strategies, financial institutions can potentially achieve more effective and adaptive approaches to asset management in dynamic market conditions._
---

# Introdução
&emsp; O primeiro registro de um contrato futuro, vem por volta do século XVII, em Osaka no Japão, nessa época, foram estabelecidos contratos futuros rudimentares para a produção de arroz no mercado de arroz de Dojima (MACHADO, TC., 2022).

&emsp; O contrato de futuros é um acordo estabelecido entre o comprador e o vendedor, no qual são definidas todas as obrigações contratuais de ambas as partes. No entanto, o cumprimento dessas obrigações, tanto pelo comprador quanto pelo vendedor, ocorre em um momento futuro, previamente determinado por acordo entre as partes, estipulado no momento em que o contrato foi iniciado (SILVA, E. S., 2016).

&emsp; A estratégia de negociação de base, conhecida também como negociação _cash-and-carry_ no âmbito dos contratos de futuros, desempenha um papel fundamental para uma grande parcela de _traders_ especulativos em busca de lucros através da antecipação da convergência dos preços à vista e dos futuros. Normalmente, essa prática envolve a adoção de uma posição comprada no ativo subvalorizado e uma posição vendida no ativo sobrevalorizado, sendo encerradas quando ocorre a tão esperada convergência. No entanto, é importante ressaltar que a negociação de base não é isenta de riscos. Mudanças inesperadas nos fatores de mercado, como taxas de juros, custos de transporte ou dividendos, podem impactar negativamente a lucratividade. Além disso, as fricções do mercado, como custos de transação e pagamentos de garantias, podem transformar uma suposta arbitragem segura em oportunidades que resultam em negócios desastrosos.(ANGOSHTARI, B., 2018).

&emsp; O campo do Aprendizado de Máquina é crucial dentro do domínio da Inteligência Artificial (IA), permitindo que sistemas inteligentes melhorem seu desempenho em uma determinada tarefa com base na experiência. Conforme destacado por André Ottoni (2017), o Aprendizado de Máquina pode ser categorizado em três principais paradigmas: Aprendizado Supervisionado, Aprendizado Não-Supervisionado e Aprendizado por Reforço. No caso do Aprendizado por Reforço (AR), os algoritmos se baseiam na ideia de aprender através do sucesso e do fracasso, sendo fundamentados nos Processos de Decisão de Markov (PDM)(OTTONI, A. L. C., 2017).

&emsp; Em uma configuração típica de AR, o aprendizado ocorre através da interação direta entre um agente e o ambiente. Nesse contexto, o agente utiliza sensores para perceber o estado atual do ambiente, toma a melhor ação possível e, em seguida, recebe um _feedback_ sobre o par estado-ação. Normalmente, recompensas positivas são atribuídas ao sucesso na tomada de decisão, enquanto recompensas negativas representam penalidades. Assim, o agente acumula essas informações de sucesso e fracasso para orientar suas decisões futuras (OTTONI, A. L. C., 2016).

&emsp; A precificação de um ativo conhecido como "Sintético de Renda Fixa" envolve a composição de uma posição vendida em um contrato futuro de ações (um derivativo que estabelece a negociação de uma ação em uma data futura a um preço pré-acordado) combinada com uma posição comprada na própria ação objeto do contrato futuro. O resultado dessa operação, então se dá o sintético de renda fixa, com ganho garantido, sendo definido pela diferença do preço do contrato a termo e da negociação a vista da ação. O desafio é identificar as combinações de negociações à vista de ações que correspondam aos contratos futuros. Dependendo das combinações escolhidas, a rentabilidade dos ativos sintéticos pode ser modificada.

&emsp; O obejtivo então desse projeto, é encontrar o conjunto de soluções ideal, definido como aquele que ajusta a rentabilidade do sintético para cerca de 100% do CDI sempre que possível. Com o proposito final de mitigar a transferência de riqueza ultilizando tecnicas de aprendizado por reforço.

&emsp; O Aprendizado por Reforço tem sido amplamente explorado em várias áreas, incluindo robótica, sistemas multiagentes, controle ótimo e otimização. Recentemente, tem se destacado sua aplicação em um domínio específico da otimização: os problemas de otimização combinatória.  

&emsp; Neste artigo, será explorado o uso de técnicas de Aprendizado por Reforço (AR) na otimização da estratégia de precificação de sintético de renda fixa, especificamente no contexto de alcançar 100 por cento do CDI. O desafio da precificação é crucial para a instituição financeira parceira, pois envolve o equilíbrio entre manter o 100 por cento do CDI e mitigar transferencia de riqueza. Tradicionalmente, esse processo é complexo devido à necessidade de considerar uma variedade de variáveis, como características do ativo e do mercado. O AR surge como uma abordagem promissora para resolver esse problema de decisão sequencial.

## Estudos Relacionados
&emsp; Neste segmento, apresentamos estudos relevantes que complementam a compreensão do tema.

### Utilização de contratos futuros e _forwards_ como estratégia de cobertura de risco no mercado europeu de bovinos de carne
&emsp; Este estudo investigou o interesse dos produtores de carne bovina europeus na utilização de contratos futuros e contratos _forward_ como estratégias de cobertura de risco. Em um contexto onde os produtores enfrentam desafios relacionados a fenômenos climáticos e instabilidade econômica, a pesquisa visou compreender as motivações e os obstáculos para a adoção desses instrumentos financeiros. Por meio de uma análise detalhada do setor bovino europeu e português, identificaram-se os principais condicionalismos que afetam as explorações, destacando-se a resiliência socioeconômica. Além disso, foram examinados os mercados futuros de bovinos em países como Austrália, Brasil, Chile e EUA, avaliando-se os benefícios e desvantagens da aplicação dessas estratégias para os produtores. No entanto, não foi possível determinar os fatores que influenciam o interesse dos produtores europeus pela utilização de contratos futuros e contratos _forward_.

### Mercados a Prazo: Futuros, _Forwards_ e _Swaps_:
&emsp; O livro "Mercados a Prazo: Futuros, _Forwards_ e _Swaps_" de Eduardo S.A. Silva oferece uma visão abrangente e detalhada sobre os principais conceitos e instrumentos financeiros relacionados aos mercados futuros, _forwards_ e _swaps_. A obra explora os fundamentos desses mercados, destacando suas características distintas e aplicações práticas. Silva diferencia entre contratos futuros e _forwards_, fornecendo uma compreensão clara das diferenças essenciais entre esses dois tipos de instrumentos financeiros. Além disso, o autor explora o funcionamento dos swaps e sua relevância no contexto financeiro contemporâneo. O livro apresenta exemplos concretos e estudos de caso para ilustrar a aplicação desses instrumentos em diversos cenários e setores da economia. 

### _Optimal Dynamic Basis Trading_
&emsp; Inspirados pelas falhas percebidas no mercado, foi proposto um modelo estocástico que incorpora os movimentos dos preços futuros e à vista, capturando a tendência da base de se aproximar de zero à medida que a maturidade se aproxima, sem necessariamente desaparecer. Em sua essência, os preços à vista e futuros são impulsionados por movimentos brownianos correlacionados, enquanto a base estocástica é representada por uma ponte browniana escalonada.

&emsp; Neste estudo, as estratégias ótimas de negociação são determinadas através da maximização da utilidade sob preferências hiperbólicas de aversão ao risco absoluto. A análise da equação de Hamilton-Jacobi-Bellman permite a derivação das condições exatas para a solução do problema de maximização da utilidade, fornecendo assim estratégias ótimas. Exemplos numéricos são apresentados para ilustrar essas estratégias e examinar os efeitos dos parâmetros do modelo.

### Análise do desempenho do aprendizado por reforço na solução do problema da mochila multidimensional
&emsp; O trabalho visou analisar o desempenho do Aprendizado por Reforço (AR) na resolução do Problema da Mochila Multidimensional (PMM). Utilizando o algoritmo _Q-learning_, foi alcançada a solução ótima em quatro instâncias específicas do problema, enquanto em outras oito instâncias, essa solução não foi alcançada. Foram realizadas análises de sensibilidade dos parâmetros do AR (α, γ, e ε) para compreender sua influência na resolução do PMM.

&emsp; A modelagem matemática por meio de modelos superfície de resposta (RSM) revelou particularidades nas instâncias do PMM em relação aos valores dos parâmetros do AR. Os gráficos da RSM permitiram visualizar o comportamento da resposta (desempenho) em relação aos parâmetros α e γ, identificando regiões que maximizam a resposta ajustada para diferentes instâncias do problema. Em trabalhos futuros, serão aplicados outros métodos de AR, como o SARSA, na resolução do PMM. Além disso, o desempenho da solução do PMM será comparado entre métodos de AR e algoritmos tradicionais, como Programação Dinâmica, Algoritmos Genéticos e Busca Tabu, visando analisar o real esforço computacional entre esses métodos. Também será investigado o comportamento dos parâmetros do AR em outros problemas de otimização combinatória.

# Metodologia

&emsp; O principal livro voltado para aprendizado por reforço, contendo introdução, metodologia e abordagens práticas diz que os problemas de aprendizado por reforço envolvem aprender o que e como fazer algo, visando maximizar um valor numérico de recompensa (SUTTON, R. S.; BARTO, A. G., 2018). A partir desta afirmação, a metodologia adotada para a realização deste projeto envolve a aplicação de técnicas de Aprendizado por Reforço (AR) na otimização da estratégia de precificação de sintético de renda fixa. O objetivo é alcançar 100 por cento do CDI de forma eficiente nos quesitos qualidade e performance. A seguir, são apresentadas as etapas do projeto:

## Definição do Problema
&emsp; O problema consiste em encontrar o conjunto ideal de soluções para que a rentabilidade do CDI alcance 100 por cento. Para isso, é necessário identificar as combinações de negociações à vista de ações que correspondam aos contratos futuros, os quais chamamos de "a termo". A rentabilidade dos ativos sintéticos pode ser modificada dependendo das combinações escolhidas e o desafio é encontrar a combinação ideal que ajuste a rentabilidade do sintético para cerca de 100% do CDI sempre que possível (TAPI, 2024).

## Ambiente de Simulação
&emsp; Para a realização do projeto, o desenvolvimento do ambiente foi feito na linguagem de programação Python, utilizando a biblioteca _OpenAI Gym_. O ambiente de simulação foi projetado para representar o mercado financeiro, permitindo a interação entre o agente e o ambiente. O ambiente é composto por um conjunto de estados, ações e recompensas, que são fundamentais para o aprendizado do agente. a _OpenAI Gym_ é uma biblioteca de código aberto que fornece uma estrutura para desenvolvimento e testes de algoritmos de RL em ambientes simulados (Brockman at al., 2016).

## Algoritmos Utilizados

### DQN - _Deep Q-Network_
&emsp; O DQN é um modelo de _Reiforcement Learning_ que funciona com base no modelo _Q-Learning_, que é uma abordagem clássica de otimização de políticas. O _Q-Learning_ tem como objetivo a aprender uma política ótima para determinar as ações de um agente a serem tomadas dentro de um ambiente, procurando de maximizar a recompensa ao longo dos episódios. 

&emsp; O DQN além de buscar a política ótima, faz o uso de uma rede neural para se aproximar da função Q, cuja determina qual a recompensa esperada para cada ação possível de ser tomada com base no estado atual.

&emsp; Para realizar este cálculo, cada camada da rede neural recebe informações referentes ao estado atual, e com isso determina qual a possível recompensa que pode ser obtida ao decidir tomar determinadas ações no futuro. Após o final de um episódio no processo de treinamento, a rede é atualizada com base nos resultados finais obtidos, e este processo é repetido _n_ vezes até que o modelo consiga balancear os pesos de forma a conseguir discernir diferentes cenários e conseguir tomar decisões melhores.

&emsp; O DQN é muito útil para lidar com casos em que os estados e o número de ações possíveis possuem uma dimensionalidade elevada. Além de ter uma grande capacidade de generalização, podendo se adaptar a ambientes semelhantes após o treinamento, consequentemente sendo mais escalável, de acordo com o site Guia de Hospedagem (2022).

### PPO - _Proximal Policy Optimization_

&emsp; Algoritmo lançado pela _OpenAI_ em 2017, busca otimizar a geração de políticas de um agente, possuindo uma grande simplicidade de implementação e parametrização, uma grande taxa de compreensão do problema e ao mesmo tempo um bom desempenho.

&emsp; O PPO funciona com uma lógica de tentativa e erro, na qual o agente é aprimorado pouco a pouco, sem mudanças bruscas, possibilitando que o agente consiga aprimorar suas políticas de uma forma que os resultados sejam mais próximos do objetivo, mas que a solução final não se diferencie muito da abordagem inicial.

&emsp; Após realizadas as primeiras experiências e obter as recompensas iniciais, a etapa inicial é calcular a função de valor de resolução, usando como base experiências passadas para o cálculo de uma recompensa esperada. Após isso, o agente toma uma ação considerando as recompensas esperadas e, ao tomar essa ação, uma nova recompensa é obtida, assim a função de qualidade é calculada. Essa função tem como objetivo principal demonstrar a perda de valor, ou seja, a diferença entre a recompensa esperada e a recompensa obtida.

&emsp; Então, o modelo é atualizado de forma sutil, estas modificações baseiam-se na forma como o modelo determina as recompensas esperadas e nas perdas resultantes, melhorando gradativamente as políticas e se aproximando cada vez mais de uma solução otimizada. Lembrando que o PPO realiza estas atualizações de forma. Medium (2023).

## Arquitetura do Agente
Para a implementação do agente, implementamos a classe DQNA (DQN _Agent_), possuindo as seguintes funções:

```
def __init__()

def flatten_dict()

def compute_action()

def update_exploration_probability()

def store_episode()

def train()
```

### init
inicia os métodos da classe, os quais são:
- **self.n_actions:** define o número de ações possíveis que o agente pode tomar (casar ou não fazer nada)
- **self.lr:** taxa de aprendizado
- **self.gamma:** fator de desconto
- **self.exploration_proba:** probabilidade de escolher testar uma possibilidade sem considerar a qualidade "explorar"
- **self.exploration_proba_decay:** taxa de desconto da probabilidade de exploração (usada para diminuir a probabilidade de exploração a cada fim de episódio)
- **self.batch_size:** Número de experiências
- **self.memory_buffer:** Lista que armazena as experiências passadas
- **self.max_memory_buffer:** tamanho máximo de experiências que podem ser armazenadas no _buffer_
- **self.model:** Rede neural

### flatten_dict
Função responsável por receber o valor do estado (cujo é recebido em um dicionário) e transformá-lo em um _array_.

### compute_action
Toma uma ação com base no _exploration probability_ e retorna a atualização dos q_values.

### update_exploration_probabilit
Usa o exploration_proba_decay para reduzir a taxa de exploração do agente, fazendo com que cada vez mais ele tenda a exploitar mais.

### store_episode
Armazena a experiência no _memory buffer_. Caso o _buffer_ esteja cheio, ele escolhe a informação mais antiga e substitui pela nova.

### train
Com base nas experiências do _memory buffer_, treina o modelo, atualizando assim sua política.

## Configuração Experimental
primeiro definimos as variáveis iniciais:
- **env:** Instância da classe _Marriage_ (ambiente), cujo recebe de parâmetro as tabelas de produtos de compra e de venda 
- **state_size:** tamanho do estado
- **action_size:** número de ações possíveis
- **max_iteration_ep:** limitador de ações por episódio (apenas no treinamento)
- **agent:** instância da classe DQNA (Agente)
- **total_steps:** contador de passos
- **cdi_array:** _array_ que armazena o CDI atual
- **infos_array:** _array_ que armazena informações do final do episódio
- **num_rows_term:** número de episódios (é definido pela quantidade de termos)
- **batch_size:** número de experiências necessário que precisa ser atingido para realizar o treinamento

Após isso, criamos um _loop_ que usa o valor de num_rows_term para iterar todos os casos. Caso a variável terminate_all seja _True_, o episódio é encerrado. Caso contrário, ele prossegue com o a próxima ação. Caso a ação for tomada, o agente retorna as informações do estado é parte para o próximo _step_.

Ao encerrar o episódio, o agente treina a rede e começa um novo episódio.

## Métricas de Avaliação

&emsp; Para avaliar a eficácia do agente, foram utilizadas métricas que permitem medir o desempenho do modelo em relação ao objetivo de alcançar 100 por cento do CDI. O próprio cálculo trabalha com a Taxa Interna de Retorno (TIR), que é uma métrica financeira que mede a rentabilidade de um investimento ao longo do tempo. A TIR é calculada com base no fluxo de caixa gerado por um investimento, considerando o valor do dinheiro no tempo.

&emsp; Dado o cálculo de TIR que é usado dentro da estrutura do cálculo de CDI, a métrica de avaliação é a própria rentabilidade do investimento, que é comparada com o CDI. A métrica de avaliação é calculada como a diferença entre a rentabilidade do investimento e o CDI, sendo que o objetivo é minimizar essa diferença, buscando alcançar 100 por cento do CDI. A partir deste resultado, avaliamos o desempenho do agente em relação ao objetivo de otimização da estratégia de precificação de sintético de renda fixa usando cálculos de Erro Quadrático Médio (MSE) para encontrar a diferença entre a rentabilidade do investimento e o CDI e Desvio Padrão (DP) para avaliar a dispersão dos resultados.

# Trabalhos Relacionados

&emsp; A busca pela otimização do processo de casamento de ativos à vista e futuros não são recentes e diversas abordagens foram propostas para resolver esse problema, como aplicação de otimização linear (SIERVO S. Juliano, 2017), algoritmos genéticos, entre outras técnicas. Dentre as abordagens e avaliações de resultados, a que trouxe mais proximidade e consistência com o objetivo de alcançar 100 por cento de CDI foi a utilização de aprendizado por reforço com algoritmos de Deep Learning (GABRIEL L. A. 2021).

&emsp; O estudo de 2017 propôs a utilização de Programação Linear para a seleção de carteiras de investimento, com o objetivo de maximizar o retorno esperado e minimizar o risco. Ao decorrer do estudo, observou-se que o autor utilizou modelos de Programação Linear, Método Simplex e Teoria Moderna de Portifólio para a resolução do problema. Ao final de sua dissertação, o autor concluiu e provou que é possível ter uma carteira de investimento com poucos ativos e com uma certa rentabilidade esperada (SIERVO S. Juliano, 2017).

&emsp; Já o estudo de 2021 propôs uma abordagem de transformação das predições em posições de compra e de venda, apresentando um ambiente completo de tomada de decisão e algoritmos de Reinforcement Learning para encontrar posições diretas de compra e venda. Para desenvolvimento de sua pesquisa, o autor utilizou A2C e PPO2 e, ao final, comparou as abordagens de Reinforcement Learning com as abordagens convencionais do mercado financeiro e concluiu que as abordagens de Reinforcement Learning apresentaram uma performance e um equilíbrio melhor (GABRIEL L. A. 2021).

# Resultados
&emsp; Durante o processo de desenvolvimento do projeto, foram trabalhadas algumas abordagens, implementações de ambiente, algoritmos e arquiteturas de agentes. Ainda que o projeto tenha sido promissor, o modelo do grupo não gerou resultados satisfatórios, não alcançando o objetivo de 100 por cento do CDI. Dentre as duas abordagens de algoritmos utilizadas, o DQN e o PPO, apenas o DQN apresentou resultados, com uma dispersão baixa dos resultados e um erro médio quadrático pequeno. No entanto, o desempenho do modelo ainda não foi satisfatório, sendo de 30 por cento o número de casamentos que estão no range, que é entre 96 e 104 por cento do CDI, em relação ao total de casamentos realizados.

&emsp; Para melhor entendimento dos dados apresentados anteriormente, foi gerado um gráfico de distribuição dos valores para entender se o modelo está convergindo para um valor específico. O gráfico apresenta uma distribuição normal, com a maior parte da distrubuição dos valores entre 80 e 120 por cento do CDI, o que indica que o modelo ainda não está convergindo para o valor esperado de 100 por cento do CDI. É possível perceber isto no gráfico a seguir.

![Distribuição dos Valores](/artigo/img/distribuicao-dos-valores.png)

&emsp; Para entender mais diretamente como está o processo de output do algoritmo, foi gerada uma tabela que mostra o CDI alcançado, a quantidade de ativos à vista selecionada, a quantidade requerida pelo ativo futuro e a média de preço à vista, que é possível ver abaixo.

![Tabela de Casamentos](/artigo/img/tabela-casamentos.png)

&emsp; Com os últimos testes feitos no modelo, o grupo extraiu algumas informações com melhores resultados do que relatado na versão anterior. O modelo em sua versão final apresentou uma rentabilidade média de 101 por cento do CDI utilizando 40 por cento da amostra total entre 96 e 104 por cento do CDI e utilizando 70 por cento da amostra total, a rentabilidade ficou entre 90 e 110 por cento do CDI. É possível visualizar a distribuição na figura a seguir.

![Distribuição do Modelo Final](/artigo/img/distribuicao-modelo-final.jpg)

&emsp; Além disso, foi gerado um gráfico da distribuição Gaussiana do CDI com o intuito de identificar e entender o comportamento do agente e suas tomadas de decisão. É possível perceber que a dispersão se manteve estreita e que a distribuição dos valores se manteve normal, além da média do CDI que ficou em 0,8, como apresentado na figura abaixo.

![Distribuição Gaussiana](/artigo/img/gaussiana-modelo.jpg)

&emsp; Por fim, o modelo final foi testado com apenas 10 termos, a fim de termos uma tabela de fácil apresentação e entendimento pelo grupo, onde foi gerado o gráfico a seguir. Com esta representação visual, é de maior entendimento as informações que foram apresentadas anteriormente sobre os 40 e com os 70 por cento da amostra. Seguindo a mesma linha de raciocínio, mas com um número muito pequeno, especificamente para visualização.

![Distribuição com 10 termos](/artigo/img/distribuicao-10-termos.jpg)


# Conclusão

&emsp; O projeto não apresentou resultados satisfatórios, estando distante do objetivo de alcançar 100 por cento do CDI. Ainda que o modelo tenha apresentado uma dispersão baixa dos resultados, o desempenho do modelo ainda não foi satisfatório, com os casamentos atendendo a apenas 30 por cento do range esperado. A distribuição dos valores apresentou uma normalidade, com a maior parte dos valores entre 80 e 120 por cento do CDI, mas ainda fugindo do range de 96 a 104 por cento do CDI, que é a média ideal para a etapa de treinamento do MVP. Em sua versão final, o modelo melhorou seus resultados, mas ainda não atingiram o objetivo, como foi possível entender e visualizar na seção anterior.

&emsp; Para trabalhos futuros, é sugerido que sejam realizadas melhorias no modelo, como a implementação de novas arquiteturas de agentes, otimização dos hiperparâmetros, aumento do número de episódios e aprimoramento do ambiente de simulação e aprimorar o modelo para que o agente realize casamentos de forma simultânea. Além de aprimorar a avaliação de resultados, com a inclusão de métricas adicionais e a realização de testes para validar a eficácia do modelo. Por fim, é recomendado utilizar métricas mais avançadas para identificar falhas no modelo e ajustar a estratégia de precificação de sintético de renda fixa, visando alcançar 100 por cento do CDI de forma eficiente.


# Referências Bibliográficas

ANGOSHTARI, B.; LEUNG, T. Optimal Dynamic Basis Trading. 2018. Disponível em: <http://arxiv.org/abs/1809.05961>. Acesso em: 29 fev. 2024.

MACHADO TC. Utilização de contratos futuros e forwards como estratégia de cobertura de risco no mercado europeu de bovinos de carne. Lisboa: FMV. ISA-Universidade de Lisboa. 2022 march

OTTONI, A. L. C.; NEPOMUCENO, E. G.; OLIVEIRA, M. S. DE. Análise do desempenho do aprendizado por reforço na solução do problema da mochila multidimensional. Revista Brasileira de Computação Aplicada, 2017.

SILVA, E. S. Mercados a Prazo: Futuros, Forwards e Swaps. [s.l.] Vida Economica Editorial, [s.d.]. Janeiro de 2016

SUTTON, R. S.; BARTO, A. G. Reinforcement Learning: An Introduction. 2. ed. Cambridge: MIT Press, 2018.

TAPI, Inteli. Otimização de Precificação visando alcançar 100% do CDI em Ativos de Renda Fixa Sintética. 2024.

BROOKMAN at al. OpenAI Gym. 2016. Disponível em: <https://gym.openai.com/>. Acesso em: 31 mar. 2024.

Guia de Hospedagem. O que é Reinforcement Learning vs Deep Q-Network (DQN). 2022. Disponível em: <https://guiadehospedagem.com.br/glossario/o-que-e-reinforcement-learning-vs-deep-q-network-dqn/>. Acesso em: 31 mar. 2024.

Medium. A Comprehensive Guide to Proximal Policy Optimization (PPO) in AI. 2023. Disponível em: <https://medium.com/@oleglatypov/a-comprehensive-guide-to-proximal-policy-optimization-ppo-in-ai-82edab5db200>. Acesso em: 31 mar. 2024.

SIERVO S. Juliano. Aplicação de Programação Linear na Seleção de Carteiras de Investimento. 2017. Disponível em: <https://repositorio.ufscar.br/bitstream/handle/ufscar/9209/Aplica%C3%A7%C3%A3o%20de%20Programa%C3%A7%C3%A3o%20Linear%20na%20Sele%C3%A7%C3%A3o%20de%20Carteiras%20de%20Investimento.pdf?sequence=1&isAllowed=y>. Acesso em 08 abr. 2024.

GABRIEL L. A. Deep Reinforcement Learning aplicado ao mercado de ações. 2021. Disponível em: <https://repositorio.fgv.br/server/api/core/bitstreams/905d5eb2-a05e-4966-ba4b-c88fae0943cd/content>. Acesso em 08 abr. 2024.

KRASHENINNIKOVA, E. et al. Reinforcement learning for pricing strategy optimization in the insurance industry. Engineering applications of artificial intelligence, v. 80, p. 8–19, 2019.

