# Relatório Final: Otimização de Precificação visando alcançar 100% do CDI em Ativos de Renda Fixa Sintética

## Descrição do Problema
 Essa operação, conhecida como cash and carry ou basis trading, requer a identificação das combinações de negociações à vista de ações que correspondem aos contratos futuros, buscando alcançar uma rentabilidade próxima de 100% do CDI. O desafio consiste em encontrar o conjunto ideal de soluções que ajustem a rentabilidade do ativo sintético para esse objetivo, com a possibilidade de uma estrutura de termo de rentabilidade que aumente conforme o vencimento do sintético, buscando sempre uma relação não-decrescente entre vencimento e rentabilidade.

## Solução Desenvolvida
### Ambiente de simulação:
  
O ambiente de simulação chamado Marriage, que é uma classe que herda de gym.Env. O objetivo desse ambiente é modelar o processo de casamento de ações à termo com ações à vista em um mercado financeiro.

O método __init__ é o construtor da classe. Ele inicializa os espaços de ação e observação do ambiente, além de carregar os dados das tabelas de termos e de compras, fornecidas como parâmetros. Define também alguns atributos iniciais necessários para o funcionamento do ambiente.

O método reset é chamado no início de cada episódio. Um episódio representa o processo completo de casamento de uma ação à termo. Ele prepara o ambiente para o início de um novo episódio, filtrando as ações à vista disponíveis para casamento com a ação à termo atual e atualizando os atributos do ambiente conforme necessário.

O método step é chamado a cada ação tomada pelo agente no ambiente. Ele implementa a lógica do ambiente em resposta à ação do agente, como casar uma ação à vista com a ação à termo ou não fazer nada. Esse método também calcula a recompensa obtida pelo agente e verifica se o estado atual é terminal.

Além disso, há métodos auxiliares como calculate_current_cdi, calculate_reward, distance_from_ideal_price_calculator e is_terminal_state, que ajudam no cálculo de variáveis importantes do ambiente e na determinação do estado terminal.

Por fim, o método filter_and_order é responsável por filtrar e ordenar as ações à vista disponíveis com base nos critérios fornecidos, para serem consideradas para casamento com a ação à termo atual.

### Treinamento
É uma implementação de um agente DQN (Deep Q-Network), utilizado para aprendizado por reforço. Ele usa a biblioteca TensorFlow para construir e treinar um modelo de rede neural. O agente é capaz de tomar decisões em um ambiente com base em um estado atual e nas recompensas esperadas para as ações possíveis.

A classe DQNA inicializa os parâmetros do agente, como taxa de aprendizado, fator de desconto e probabilidade de exploração. Além disso, define a estrutura da rede neural com camadas densas (fully connected) e compila o modelo para otimização com o algoritmo Adam.

Os métodos compute_action e train são essenciais para a funcionalidade do agente. O primeiro calcula a ação a ser tomada com base no estado atual, utilizando a política de exploração epsilon-greedy para selecionar entre ações aleatórias e ação baseada nas estimativas Q da rede neural. O segundo método é responsável pelo treinamento do modelo, utilizando uma técnica chamada de replay buffer para amostrar experiências passadas e ajustar os valores Q esperados.

A função flatten_dict é utilizada para transformar o estado do ambiente em um formato adequado para entrada na rede neural, achatando estruturas de dados aninhadas em um único vetor.






## Resultados Obtidos:
O modelo final é capaz de produzir casamentos entre boletas a vista e a termo, respeitando a regra de acertar o mais próximo de 100% do cdi. 

#### Dados: 
- Rentabilidade média: 101%
- 40% de amostra total para cdi de 96% a 104%
- 70% de amostra para cdi entre 96% e 110%

#### Distribuição do CDI:   
![cdi](./img/image(4).png)
