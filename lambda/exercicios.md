# Lista de exercícios - Cálculo Lambda
2023/1


## 3.1

a) [V] Seja M e N lambda-termos, então (M N) é uma aplicação que representa a operação de chamada da função M com argumento N.

    Sim, pois representa a operação de substituição M[x <- N] que substitui todas as ocorrências livres de x em M por N.

b) [T] O resultado da substituição λy.(x y)[x ← y] é λz.(y z).

    Sim, pois como y já existe e é uma variável ligada, é substituído por um z equivalente, para que assim x seja substituído por y como variável livre.

c) [F] Não é possível definir um termo lambda que represente uma função de mais de uma variável como soma ou multiplicação. Isso se dá pois abstrações introduzem somente uma variável por vez. 

    Pré-termos: conjunto infinito contável de parâmetros, identificadores, variáveis, e abstrações
    - x, y (Variáveis)
    - @(M,N) (Aplicação)
    - λx.M (Abstração)

    Alfa-equivalência: dois pré-termos M e N são alfa-equivalentes sss eles diferem **somente** na escolha dos nomes de variáveis ligadas.
    Ex.: \x.x y === \z.z y
    Ex.: \x.x x === \z.z z

    Termo lambda: classe de equivalência de pré-termos alfa-equivalentes
    Ex.: [λx.x] = { λx.x, λy.y, λz.z, . . .}

    Resposta: É possível representar uma função de múltiplos argumentos através de um termo lambda que recebe um dos argumentos e devolve um termo que consome os demais. Usando esse mecanismo, passagem de múltiplos argumentos é possível através de aplicações sucessivas.
    Ex.: @TO-DO

d) [F] Considere o termo (x y) \y.\x.(x y). Nele, a primeira ocorrência da variável x é livre e a segunda é ligada, e a primeira e a segunda ocorrências da variável y são livres.

    Falso, pois a segunda ocorrência de y é ligada em \y.

e) [V] Um mesmo termo lambda pode ter mais de um redex e, portanto, beta-reduzir em um passo para dois termos diferentes.
    
    Redex: expressão reduzível, é um subtermo de M com o formato (\x.P) Q, onde seu contractum é P[x <- Q]. Um termo que não contém nenhum redex é chamado de **forma normal**.

    Beta-redução: avalia termos lambda através de substituição. Se a partir da contração de algum redex de M obtivermos N, dizemos que M beta-reduz para N.
    Ex.: (\z.\x.x z) y -> \x.x y
    Ex.: \y.(\x.y x) ((\y.x) y) -> \y.(\x.y x) x -> \y.y x

    Um termo P pode ter diversos redexes e, portanto, avaliar para distintos termos.
    Ex.: w = \x.x x e I = \x.x

f) [F] Se um termo possuir forma normal, então utilizar a estratégia de avaliação estrita (redex mais interno, mais à esquerda) sempre alcança a respectiva forma normal.

    Avaliação normal: redex mais externo, mais à esquerda. Realiza a aplicação sem normalizar a função nem o argumento.

    Avaliação estrita: redex mais interno, mais à esquerda. Normaliza a função e o argumento antes de realizar a aplicação.

    Resposta: A estratégia normal é que garante terminação

g) [F] Existem termos lambda que não possuem variáveis, ou seja, há termos lambda formados apenas por abstrações lambda ou por aplicações lambda.
    
    Termo lambda: classe de equivalência de pré-termos alfa-equivalentes
    Ex.: [λx.x] = { λx.x, λy.y, λz.z, . . .}
    - x, y (Variáveis)
    - @(M,N) (Aplicação)
    - λx.M (Abstração)

    Resposta: em um termo lambda, todas as folhas são variáveis. É impossível ter um termo lambda finito sem conter ao menos uma folha.
    Ex.: λx.M, M é folha, logo M é variável.

## 3.2
a) [V] Em (z x y), temos que z, x e y ocorrem livres.

b) [V] Em \y.(z x y), temos que x e z ocorrem livres e y ocorre ligada.

c) [F] Em`(\y.x y)(\x.y), temos que x e y são ligadas na primeira ocorrência de cada (da esquerda para a direita).

d) [F] Em x y z (\z.\y.x y z), temos que x, y e z são livres na segunda ocorrência de cada (da esquerda para a direita).

## 3.3
Marque a alternativa incorreta sobre a operação de substituição.

E. `(\x.x z)[x <- y] = \x.y z`

    Errado, pois x está ligado. Deveria resultar \x.x z

# 3.4
B. \x.z

# 3.5
B. (\x.x \x.x) Forma normal

# 3.6
true = \a.\b.a
false = \a.\b.b
if = \a.\b.\c.a b c
OU lógico (inclusivo)? True se um ou ambos operandos forem true

or =  \a b. a a b ;
se for a, then a
se não for a then b
    se b for true, é true
    se b for false, é false


# 3.7

((λy.λx.(3 ∗ x) + y) 2) 11

```haskell
let
  add      = \m n p q. (m p) (n p q) ;
  mult     = \m n p q. m (n p) q ;
in
  ((\y.\x.(add (mult 3 x) y)) 2) 11
```


# 3.8
```haskell
let 
   
    -- Logica booleana
    true     =  \a b. a ;
    false    =  \a b. b ;
    if       =  \c a b. c a b ;
    not      =  \p. p false true ;

    -- Pares
    pair     = \a b c. c a b ;
    fst      = \p. p true ;
    snd      = \p. p false ;

    succ     = \n p. \q. p (n p q) ;
    pred     = \n. fst (n (\p.(pair (snd p) (succ (snd p)))) (pair 0 0)) ;

    sub      = \m n. (n pred) m ;

    isZero   = \n. n (\x. false) true ;

    less     = \m n. not (isZero (sub n m)) ;

    shorter = \p. if (less (fst p) (snd p)) (fst p) (snd p)

in
    shorter (pair 3 2)
```


# 3.9
    ((λx.λy.x y) (λx.z)) x)
    ((\x.\y.x y) (\x.z) x)
    ((\y.(\x.z) y) x)
    ((\y.z) x)
    z

# 3.10
- Entrada: pair x y, x e y são numerais de Church
- Saída: 
  - Se pair 0 0, devolve 0
  - Se não, devolve mdc x y
  

```haskell
    pair = \a b c. c a b ;
    true     =  \a b. a ;
    false    =  \a b. b ;
    if       =  \c a b. c a b ;
    and      =  \a b. a b a ;
    or       =  \a b. a a b ;
    not      =  \p. p false true ;
    isZero = \n. n (\x.false) (true);
    

     -- Extrair fst p e snd p
     -- Avaliar se os dois são 0
        -- Se sim, devolver 0
        -- Se não, calcular mdc (fst p) (snd p)

    isZeroPair = \p. (or (isZero (fst p)) (isZero (snd p)));
    mdc = ?
    teste = \p. if (isZeroPair p) 0 (mdc (fst p) (snd p));

```

# 3.11

(a) 

```haskell
let

true = \a b. a;
false = \a b. b;
if = \t e1 e2. t e1 e2;
pair = \a b c. c a b;
fst = \p. p true;
snd = \p. p false;
succ = \m. \p q. p (m p q);
add   = \m n p q. (m p) (n p q) ;

swap = \p. pair (snd p) (add (fst p) (snd p));



in

  swap (pair 1 2)
```

(b) R: Fibonacci

(c) 

```haskell
let

  true = \a b. a;
  false = \a b. b;
  if = \t e1 e2. t e1 e2;
  pair = \a b c. c a b;
  fst = \p. p true;
  snd = \p. p false;
  succ = \m. \p q. p (m p q);
  add   = \m n p q. (m p) (n p q) ;
  mult     = \m n p q. m (n p) q ;

 somaPar = \p. pair (snd p) (add (fst p) (snd p));

  multPar = \p. pair (mult (fst p) (snd p)) (succ (snd p));

  foo = \m.fst(m multPar (pair 1 1));

in

  multPar (pair 1 2)
```

(d) 

foo 0 => 1

foo 1 => 1

foo 2 => 2

foo 3 => 6

foo 4 => 24

Fatorial de x

n! = 1 se n = 0, n*(n-1)! se n>0