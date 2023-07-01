# Cálculo Lambda (λ)

## Sintaxe

λx.x y = `\x.(x y)`
- (x y): escopo de λx
- x y: aplicação @(x,y)

## Numerais de Church
    0 = \f x.x
        \f - operação
        \x - base
        x - 0 vezes f sobre x

    1 = \f x.f x
        \f - operação
        \x - base
        f x - 1 vez f sobre x
    
    2 = \f x.f(f (f x))
        \f - operação
        \x - base
        f (f x) - 2 vezes f sobre x

    n = \f x. f(f(f ... (f x))), (f x) n vezes

## Sucessor
    succ = \n. \A B. A (n A B)

        (n A B) - @(A,B), n vezes
        A (n A B) - @(A,B), n+1 vezes

## Adição
    add = \n1 n2. n1 succ n2
        n1 vezes o succ de n2

    add2 = \n1 n2. \A B. n1 A (n2 A B)

## Multiplicação
    = (\x. add n2 x)
        Dado um número x, soma n2 a x

    mult = \n1 n2. n1 (\x. add n2 x) 0
        Dado um número x, soma n2 a x, n1 vezes a sobre o valor inicial 0

## Teste Zero
    \n. n (operação) (caso base)
        - Se n rodar 0 vezes sobre a operação, retorna caso base
        - Se n rodar no mínimo uma vez, retorna operação
  
    isZero = \n. n (\x.false) (true)

## Pares
    pair M N = \ m n c. c m n
        onde c é controle
        m e n são passados como parâmetros de c

    fst = \p. p true
    snd = \p. p false

## Predecessor
    swap = \p. pair (snd p) (fst p)
        Constrói um novo par invertendo a ordem dos elementos do par original

    shiftInc = \p. pair (snd p) (succ (snd p))
        Constrói um novo par com 
            - o primeiro elemento composto pelo segundo elemento (snd) do par original (p)
            - o segundo elemento composto pelo sucessor (succ) do segundo elemento (snd) do par original (p)

    pred = \n. fst(n shiftInc (pair 0 0))
        Constrói o par (n-1, n) e extrai o n-1
    

## Revisão pra Prova 1

### Parte 1 - Conceitos e NORMA
- Conjunto contável / incontável
  - Provar
    - Codificação de triplas ou somar componentes e comparar, se for igual comparar componente a componente
- Algoritmos, programas, máquinas, computação, função computada, equivalência de programas e equivalência de máquinas
  - Algoritmo: conceito
  - Programa: conceito, descrição de algoritmos em uma linguagem, definição formal (monolíticos, iterativos*)
    - Monolíticos: fluxogramas, instruções rotuladas  
  - Máquinas: entrada, saída, estados, função entrada/saída, interpretações das operações, interpretações dos testes
  - Computação: sequência de snapshots, programa + entrada
    - norma: (rótulo, memória)
    - para ou não para
  - Função computada: relação entre entradas e saídas
    - Funções parciais (pode entrar em loop) [Norma é naturais para naturais]
  - Equivalência de programas:
    - Em uma máquina, quando tem a mesma f computada
  - Equivalência forte:
    - Programas equivalentes entre máquinas diferentes
  - Equivalência de Máquinas:
    - Simulação
      - M simula N e N simula N: Nenhum do conjunto de funções computadas de um é maior que outro (não faz mais coisas que outra)
      - Quando tem E/S diferentes, precisa de codificação e decodificação possível e demonstrável
- NORMA
  - Definição, aritmética
  - Estrutura de dados (codificação)
  - Endereçamento direto e indireto
    - NORMA2 simula NORMA
    - Programa Universal
  - Exercícios de programação

### Parte 2 - Lambda
- Expressões regulares
  - Não consegue fazer tal coisa
- Cálculo Lambda
  - Entender código, análise de função computada, saber simular, fazer programa a partir de descrição da máquina
  - Variável, abstração e aplicação
  - Alfa-equivalência
  - Booleanos, if/else
  - Sucessor, predecessor
  - Listas
  - Recursividade, operador de ponto fixo
  - NORMA simula lambda


## Cheatsheet do Rodrigod
```haskell
-- Combinadores basicos
 i  = \x. x ; 
 k  = \x y. x;        
 s  = \x y z. x z (y z);

-- Combinador de ponto fixo      
 fix      = \f. (\x. f (x x)) (\x. f (x x)) ;

-- Logica booleana
 true     =  \a b. a ;
 false    =  \a b. b ;
 if       =  \c a b. c a b ;
 and      =  \a b. a b a ;
 or       =  \a b. a a b ;
 not      =  \p. p false true ;
 xor      =  \a b. (or (and (not a) b) (and a (not b))) ;
 sss      =  \a b. (not (xor a b)) ;

-- Pares
 pair     = \a b c. c a b ;
 fst      = \p. p true ;
 snd      = \p. p false ;

-- Numeros naturais
 zero     = \f x. x ;
 succ     = \n p. \q. p (n p q) ;
 pred     = \n. fst (n (\p.(pair (snd p) (succ (snd p)))) (pair zero zero)) ;
 add      = \m n p q. (m p) (n p q) ;
 sub      = \m n. (n pred) m ;
 isZero   = \n. n (\x. false) true ;
 equal    = \m n. and (isZero (sub m n)) (isZero (sub n m)) ;
 lessEq   = \m n. isZero (sub m n) ;
 great    = \m n. not ( isZero (sub m n)) ;
 greatEq  = \m n. isZero (sub n m) ;
 less     = \m n. not (isZero (sub n m)) ;
 mult     = \m n p q. m (n p) q ;
 div      = fix (\M. \m n. if (less m n) zero (succ (M (sub m n) n))) ;
 mod      = fix (\M. \m n. if (less m n) m (M (sub m n) n)) ; 
 exp      = \m n. n m ;
 fatorial = fix (\M. \n. if (isZero (pred n)) 1 (mult n (M (pred n)))) ;

-- Listas
 empty    = \x. true ;
 cons     = \h t. pair h t ;
 isEmpty  = \l. l (\x y.false) ;
 head     = fst ;
 tail     = snd ;
 length   = fix (\M. \l. if (isEmpty l) 0 (succ (M (tail l)))) ;

>> isEmpty (cons 2 empty)
```


