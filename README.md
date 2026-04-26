# Relatório

## Identificação

**Nome(s):** Daniel Gutschwager e Leonardo Leites  
**Matrícula(s):** 00315708 e 00338804

## 1. Comparação experimental (Tarefas 1 - 4)

Executar os algoritmos com `mediumMaze` ou `bigMaze`, reportando:

- custo da solução;
- número de nós expandidos;
- análise dos resultados.

<div style="margin-left: 40px;">

### Tarefa 1 - Busca em Profundidade (DFS / BEP)

#### Resultados - mediumMaze  
Custo da solução: 130  
Número de nós expandidos: 146  

#### Resultados - bigMaze  
Custo da solução: 210  
Número de nós expandidos: 390  

#### Análise dos resultados

Os resultados obtidos confirmam o comportamento esperado da Busca em Profundidade (DFS).

No `mediumMaze`, o algoritmo encontrou uma solução com custo 130, expandindo 146 nós. Já no `bigMaze`, o custo da solução aumentou para 210, com 390 nós expandidos. Esse aumento é esperado devido ao crescimento do espaço de busca.

A DFS explora profundamente um caminho antes de considerar alternativas, o que faz com que encontre soluções rapidamente em alguns casos, porém sem garantir que sejam ótimas. Isso explica os custos relativamente altos das soluções encontradas, especialmente no `bigMaze`.

Além disso, o número de nós expandidos é relativamente menor quando comparado a algoritmos como BFS, pois a DFS não realiza uma exploração sistemática por níveis. Em vez disso, ela segue um único caminho até o fim, retrocedendo apenas quando necessário.


### Tarefa 2 - Busca em Largura (BFS / BEL)

#### Resultados - mediumMaze  
Custo da solução: 68  
Número de nós expandidos: 269  

#### Resultados - bigMaze  
Custo da solução: 210  
Número de nós expandidos: 620  

#### Análise dos resultados

Os resultados obtidos evidenciam o comportamento esperado da Busca em Largura (BFS).

No `mediumMaze`, o algoritmo encontrou uma solução com custo 68, significativamente menor do que o obtido com a DFS, expandindo 269 nós. Já no `bigMaze`, o custo da solução foi 210, com 620 nós expandidos.

A BFS garante encontrar o caminho mais curto em termos de número de ações, o que explica o menor custo observado no `mediumMaze` quando comparado à DFS. No entanto, essa garantia vem com um custo maior de processamento, já que o algoritmo explora todos os estados nível a nível antes de avançar.

Isso se reflete diretamente no número de nós expandidos, que é maior do que na DFS. Esse comportamento ocorre porque a BFS mantém na memória todos os nodos de um nível antes de explorar o próximo.


### Tarefa 3 - Busca de Custo Uniforme (UCS / BCU)

#### Resultados - mediumMaze  
Custo da solução: 68  
Número de nós expandidos: 269  

#### Resultados - bigMaze  
Custo da solução: 210  
Número de nós expandidos: 620  

#### Análise dos resultados

Os resultados obtidos com a Busca de Custo Uniforme (UCS) foram idênticos aos da Busca em Largura (BFS).

No `mediumMaze`, o algoritmo encontrou uma solução com custo 68, expandindo 269 nós. Já no `bigMaze`, o custo da solução foi 210, com 620 nós expandidos. Esse comportamento é perfeitamente esperado no problema de busca de posição (`PositionSearchProblem`), pois o custo de cada movimento no labirinto é sempre igual a 1. 

Quando todos os custos de transição são uniformes, a UCS comporta-se de maneira idêntica à BFS, explorando os estados em anéis de custo constante (nível a nível). 

Dessa forma, a UCS também garante a otimalidade da solução encontrada, à custa de uma exploração sistemática que resulta em um maior número de nós expandidos quando comparada à DFS ou a algoritmos informados com heurísticas.


### Tarefa 4 - Busca A* (A-Star)

#### Resultados - mediumMaze  
Custo da solução: 68  
Número de nós expandidos: 221  

#### Resultados - bigMaze  
Custo da solução: 210  
Número de nós expandidos: 549  

#### Análise dos resultados

Os resultados evidenciam a superioridade e a eficiência da busca informada A* (utilizando a heurística de distância de Manhattan).

Em ambos os labirintos, o A* encontrou a mesma solução ótima encontrada pela BFS e pela UCS (custo 68 no `mediumMaze` e 210 no `bigMaze`), o que valida que a heurística de Manhattan é admissível para este problema.

A principal diferença, no entanto, reside na eficiência da busca: no `mediumMaze`, o número de nós expandidos caiu para 221 (contra 269 da UCS/BFS) e no `bigMaze` caiu para 549 (contra 620 da UCS/BFS).

O A* consegue manter a garantia de encontrar o caminho de menor custo, mas expande consideravelmente menos nós por utilizar a estimativa heurística (f(n) = g(n) + h(n)) para direcionar a exploração rumo ao objetivo, evitando investigar exaustivamente caminhos que visivelmente se afastam do destino.


</div>



## 2. Modelagem de estado (Corners/Food) — Tarefa 5

Descrever como o estado foi representado. Informar:

- quais aspectos foram incluídos na representação;
- como os cantos visitados são codificados.

<div style="margin-left: 40px;">

### Tarefa 5 - Problema dos Cantos

#### Representação do estado

O estado foi modelado como uma tupla composta por dois elementos:

- posição atual do Pacman  
- conjunto de cantos já visitados  

Formalmente, o estado é representado como:

- `(position, visitedCorners)`

onde:

- `position` é uma tupla (x, y) indicando a posição atual do agente no labirinto  
- `visitedCorners` é uma coleção dos cantos já visitados pelo agente  

#### Aspectos incluídos na representação

A modelagem do estado inclui apenas as informações essenciais para a resolução do problema:

- posição atual do Pacman  
- identificação dos cantos já visitados  

Não foram incluídas informações irrelevantes, como:

- posição dos fantasmas  
- localização de outros alimentos  
- estado completo do jogo (GameState)  

Essa escolha reduz significativamente o espaço de busca e melhora a eficiência do algoritmo.

#### Codificação dos cantos visitados

Os cantos visitados são armazenados como uma tupla contendo as posições dos cantos já alcançados.

A cada movimento:

- se o Pacman alcança um canto ainda não visitado  
- esse canto é adicionado à coleção `visitedCorners`  

A utilização de tupla para controle de estados visitados.

Um estado objetivo é definido quando todos os quatro cantos foram visitados, ou seja, quando o número de elementos em `visitedCorners` é igual a quatro.

Durante a implementação, foi necessário garantir uma representação canônica dos cantos visitados. Inicialmente, estados logicamente equivalentes estavam sendo tratados como diferentes devido à ordem dos elementos na estrutura utilizada.

Por exemplo, as representações `(A, B)` e `(B, A)` correspondiam ao mesmo conjunto de cantos visitados, mas eram consideradas distintas pelo algoritmo, o que resultava em expansão redundante de estados.

Para resolver esse problema, foi utilizada a ordenação dos cantos visitados antes de convertê-los para tupla, garantindo uma representação consistente

</div>

## 3. Heurísticas (admissibilidade + impacto) — Tarefas 6–7

Descrever a heurística utilizada e fornecer justificativa de admissibilidade:

- por que a heurística é admissível;
- qual foi o impacto no desempenho.

<div style="margin-left: 40px;">

### Tarefa 6 - Heurística para o CornersProblem

#### Descrição da heurística

A heurística utilizada considera a distância de Manhattan entre a posição atual do Pacman e os cantos que ainda não foram visitados.

A partir da posição atual, o algoritmo estima o custo restante simulando um percurso guloso: a cada passo, seleciona o canto mais próximo, soma a distância até ele e repete o processo até que todos os cantos tenham sido considerados.

Essa abordagem gera uma estimativa do custo total necessário para visitar todos os cantos restantes.

#### Admissibilidade da heurística

A heurística é admissível pois nunca superestima o custo real da solução.

A distância de Manhattan representa a menor distância possível entre dois pontos em um grid sem considerar obstáculos. Como o labirinto possui paredes, o custo real para alcançar um canto pode ser maior ou igual ao valor estimado, mas nunca menor.

Além disso, a soma dessas distâncias ao longo do percurso guloso continua sendo uma subestimação do custo real, pois não considera desvios obrigatórios causados por paredes nem garante o caminho ótimo entre todos os cantos.

Dessa forma, a heurística sempre retorna valores menores ou iguais ao custo real, garantindo a admissibilidade.

#### Resultados   
Número de nós expandidos: 692  

#### Impacto no desempenho

A utilização da heurística reduziu significativamente o número de nós expandidos.

Sem heurística (BFS), o problema mediumCorners exigia a expansão de mais de 2000 nós. Com a heurística aplicada ao A*, esse número foi reduzido para 692 nós.

Essa redução demonstra que a heurística conseguiu direcionar a busca de forma eficiente, evitando a exploração de regiões irrelevantes do espaço de estados.

Como resultado, o algoritmo tornou-se consideravelmente mais rápido e eficiente, mantendo a garantia de encontrar uma solução ótima.

### Tarefa 7 - Heurística para o FoodSearchProblem

#### Descrição da heurística

A heurística utilizada agora é baseada em uma **Árvore Geradora Mínima (MST - Minimum Spanning Tree)** combinada com a distância até a comida mais próxima. 

Para estimar o custo restante para coletar todas as comidas, o algoritmo faz o seguinte:
1. Constrói uma MST conectando todas as bolinhas de comida restantes, utilizando a distância de Manhattan entre elas como peso das arestas.
2. Calcula a distância de Manhattan da posição atual do Pacman até a bolinha de comida mais próxima.
3. A heurística final é a soma do custo da MST com a distância até essa comida mais próxima.

#### Admissibilidade da heurística

A heurística **É admissível** e consistente.

Para que a heurística seja admissível, ela não pode superestimar o custo real. O custo real para coletar todas as comidas obrigatoriamente envolve viajar do Pacman até alguma comida, e depois viajar por todas as comidas restantes. 
A MST construída com distâncias de Manhattan representa o menor custo necessário apenas para conectar todos os pontos de comida no grid (ignorando as paredes). Somar a distância do Pacman à comida mais próxima fornece uma estimativa de limite inferior sólida para o problema de roteamento. Como a distância de Manhattan relaxa a restrição das paredes (podendo atravessá-las), o valor calculado sempre será menor ou igual à distância real que o Pacman terá que percorrer no labirinto.

Com isso, garantimos a otimalidade da busca A* e passamos no teste de consistência do autograder com sucesso.

#### Resultados   
Número de nós expandidos: 7137 (no tabuleiro `trickySearch`)

#### Impacto no desempenho

A utilização desta heurística informada e admissível trouxe uma grande melhoria de desempenho, reduzindo drasticamente o espaço de busca explorado.

Sem heurística (BCU/A* com heurística nula), o algoritmo expande mais de 16.000 nós no tabuleiro `trickySearch`, levando vários segundos para concluir. Com a heurística baseada em MST, o número de nós expandidos cai para apenas 7137. Isso não só agiliza imensamente a obtenção da resposta, mas atende aos requisitos de nós expandidos propostos pela disciplina (ficando bem abaixo do teto de 9000 nós para a nota máxima 4/4), demonstrando o forte poder que heurísticas baseadas em relaxamento de grafos e conectividade têm em problemas que se assemelham ao do caixeiro viajante (TSP).

</div>

## 4. Declaração de uso de IA

Ferramentas de Inteligência Artificial foram utilizadas como apoio complementar ao longo da elaboração deste trabalho, principalmente na organização textual, revisão de explicações e consulta de conceitos.

O ChatGPT foi empregado principalmente para auxiliar na geração, refinamento e polimento dos textos descritivos presentes no relatório, contribuindo para maior clareza, coesão e estruturação das explicações relacionadas às tarefas desenvolvidas.

Além disso, o NotebookLM foi utilizado como ferramenta de suporte para consulta e organização de conteúdos, auxiliando na localização de informações sobre as atividades propostas, bem como na revisão de conceitos abordados em aula, como algoritmos de busca, heurísticas e propriedades teóricas.

Ressalta-se que a implementação prática, desenvolvimento dos algoritmos, testes, depuração e compreensão técnica das soluções permaneceram sob responsabilidade do autor, sendo as ferramentas de IA utilizadas como suporte de produtividade, organização e revisão textual.