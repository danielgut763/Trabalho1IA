# Relatório

## Identificação

**Nome(s):** Daniel Gut... Leonardo Leites  
**Matrícula(s):** xxxxxxxx e 00338804

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

</div>

## 3. Heurísticas (admissibilidade + impacto) — Tarefas 6–7

Descrever a heurística utilizada e fornecer justificativa de admissibilidade:

- por que a heurística é admissível;
- qual foi o impacto no desempenho.

## 4. Declaração de uso de IA

Declarar se foi utilizado algum sistema de IA generativa, como ChatGPT, Claude ou Copilot, e como foi utilizado.

## Observação

O formato é livre, mas o documento deve conter todas as informações acima. A identificação deve ficar no início e ser fácil de localizar. As demais informações podem ser organizadas em seções diferentes.
