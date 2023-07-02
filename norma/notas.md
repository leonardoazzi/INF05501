# Conceitos 

## Cardinalidade
Quantidade de elementos que um dado conjunto possui

|A|: Cardinalidade do conjunto A.

- Para conjuntos finitos, cardinalidade é um número Natural

## Conjuntos contáveis
O conjunto X é contável sss X é finito ou existe bijeção f: Naturais->X.

O conjunto X é incontável sss X é infinito e não existir bijeção Naturais -> X.

## Conjuntos incontáveis

- Conjunto potência: incontável
  - Conjunto {0,1}^naturais é incontável
    - Conjunto de funções de naturais para bool
  - Conjunto Nat^Nat não é contável

- Teorema de Cantor
  - Seja A um conj. qualquer, não existe nenhuma função bijetora entre A e Potência(A)

## Funções computáveis

Uma função f:A1 X ... X Ak -> B é efetivamente computável caso exista um dispositivo M que, ao receber valores de entrada (a1,...,ak), gera de forma automatizada, em um número infinito de passos, o valor f(a1,...,ak).

## Funções não efetivamente computáveis

Aplicação do teorema de Cantor, funções devem ser contáveis.

## Linguagens formais

- Alfabeto (Σ): qualquer conjunto finito.
- Palavra: uma palavra sobre o alfabeto Σ é uma sequência finita de símbolos de Σ.
- Fecho de Kleene (Σ*): conjunto de todas a palavras sobre Σ.
- Linguagem formal (L): subconjunto de Σ*.

Se Σ é finito, logo Σ* é contável.

## Programas

Conjunto de operações e testes em P. Sequência ou histórico.

- Monolítico
  - r_i   F   r_k
  - r_i   F   r_T   r_F
- Iterativo
  - Componente sequencial (;)
  - Componente condicional (if-then-else)
  - Componente de iteração (while-do) (do-while)
- Recursivo
  - fat(fat(x))

## Máquinas

Um conjunto de estados possíveis.

## Computação

Programa (P) com entrada (X) para máquina (M).

## Função computada

<P,M>: X -> Y
- <P,M>(x) é indefinida se a computação é infinita
- <P,M>(x) M_saída(v_f) se a computação é finita e (r_f,v_f) é a última configuração da computação

## Equivalência de programas

P1 é M eq. P2 sss <P1,M> = <P2,M>

* Para máquinas muito poderosas, é indecidível determinar M equivalência

- Equivalência forte de programas
  - Quando <P1,M> = <P2,M> para **qualquer máquina M**

recursivos > monolíticos > recursivos

## Simulação

N simula M sss para qualquer P de M existem:
- um programa Q de N
- uma função de codificação c: X_M -> X_N
- uma função de decodificação d: Y_N -> Y_M 
tal que <P,M> - d * <Q,N> * c

M e N são **equivalentes** sss
- M simula N
- N simula M

## Máquina Universal

M é uma máquina universal sss simula **qualquer** outra máquina N.

# Máquina NORMA

Máquina de infinitos registradores.

- X: entrada

- Y: saída

- ABCD...abcd...: registradores

Cada registrador armazena um número natural, sem limite de tamanho. Para cada registrador, é associado uma operação e um teste.

## Estruturas de dados

NORMA -> funções unárias

- Pares
  - Codificação: Teorema fundamental da aritmética
  - Ex.: pair(a,b) = 2^a * 3^b

## NORMA^k

k registradores de entrada e um reg. de saída.

Teorema: para todo k>1, NORMA simula NORMA^k

## NORMA_2

Somente X e Y (entrada e saída).

Teorema: NORMA_2 simula NORMA.