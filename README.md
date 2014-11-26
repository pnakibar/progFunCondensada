Conceitos de programação funcionais condensados!
================================================


####Programação funcional é magia!
Funcional é o paradigma de programação que o estilo da construção e a estrutura de "montagem" como funções matemáticas
Alguns dos conceitos mais importantes são os que, nela se evita amudança de estado e dados mutáveis.
Programação funcional tem as raízes no Cálculo Lambda[1]

Mas chega de enrolação e vamos aos conceitos ;)


###Recursão
A recursão em calda é a solução funcional para o laço *while* e *for* da programação imperativa tradicional. A função se chama até atingir o resultado desejado e então retorna o valor.

```python
def fatorial(x):
      if (x == 1):
            return 1
      else
            return x * fatorial(x-1)
```
Obs.: Note que essa solução é um padrão para o loop e ele sempre vai seguir uma estrutura parecida com a da função fatorial.
Porém a recursão em calda gasta uma grande quantidade de memória, e a solução para isso é:

#####Otimização recursão em calda
```python
def fatorial(num):
      def fatorialLoop(num, acumulador):
            if (num == 1):
                  return acumulador
            else:
                  return fatorialLoop(num-1,acumulador*num)

      return fatorialLoop(num, 1)

print(fatorial(4))
```

Algumas linguagens não aceitam essa otimização, como o Python, porem alguns dialetos de Lisp, como racket suportam.

```lisp
(define (fact x)
  (if (= x 0) 1
      (* x (fact (- x 1)))))

(define (fact x)
  (define (fact-tail x accum)
    (if (= x 0) accum
        (fact-tail (- x 1) (* x accum))))
  (fact-tail x 1))
```

###*Call by Value vs. Call by Name*

*Call by Value* imediatamente avalia os parâmetros da função (i.e. resolve a função) e retorna o seu valor, ao contrário de *Call by Name* que deixa para avaliar os valores depois.



Exemplo em uma função:
```python
def f(x,y) = x*x
```
Se utilizarmos o *CBV* a função se resolveria da seguinte forma:
```python
#ex1:
f(3, 2) :    3*3     1.
            6       2.
#ex2:
f(4+5, 9):   f(9,9)  1.
            9*9     2.
            81      3.
```

Note que no segundo exemplo a função *4+5* é resolvida (avaliada) imediatamente.

Agora, utilizando o *CBN*:
```python
#ex3:
f(3, 2):     3*3     1.
            6       2.

#ex4:
f(4+5, 9):   (4+5)*(4+5) 1.
            9*(4+5)     2.
            9*9         3.
            81          4.

```
Note como no exemplo 3 não se teve diferença em relação ao metódo *CBV*, justamente pois ele não está realizando nenhuma avaliação neste momento. Porém, no ex4 ele está realizando a avaliação *4+5*, e isso faz com que a função tenha um passo a mais que a outra, justamente para avaliar a conta. E ela faz isso por último, ao contrário do *CBV*, que faz isso assim que for possível.

Generalizando a situação com uma função de *loop* (que é uma função que se chama infinitamente), para poder visualizar ainda mais a diferença entre *CBV* e *CBN*:

```python
#ex5: Call by value
f(4+5, loop): 	infinito	1.

#ex6: Call by name
f(4+5, loop)	(4+5)*(4+5)	1.
			9*(4+5)     2.
			9*9 		3.
			81		4.
```

No ex5, ele imediatamente avalia o segundo argumento da função, que é *loop*. Ao avaliar ele vai entrar em um *loop* infinito e nunca vai sair, nem mesmo vai retornar o valor na função. Já no ex6 como os argumentos são avaliados posteriormente ele não entra em um *loop* infinito, pois não é avaliado.


###Funções de *Alta* Ordem
Linguagens funcionais tratam funções como valores de primeira classe, i.e., eles podem ser retornados por uma função ou passado como argumento. As Funções de Alta Ordem são todas as funções que recebem funções como parâmetro ou retornam funções como resposta. Um exemplo desse tipo de função é a derivada de cálculo, que recebe uma função e retorna uma outra função, isso permite uma maior flexibilidade na construção do programa, deixando a criação de funções muito mais dinâmica.
Funções de primeira ordem recebem e retornam valores normais, como inteiros.

```python
#função que retorna uma função
def dividirPor(x):
      return lambda n:n/x

dividirPorCinco = dividirPor(5)
dividirPorCinco(50) #retorna 10

#função que recebe uma função e retorna um valor normal
def foo(x,a):
      return x(a)

def bar(a):
      return a*a

print(foo(bar,4)) #retorna 16
```

###Lambda ou Funções Anônimas
São funções que não tem nome. Geralmente são utilizadas para serem passadas como argumento para funções de alta ordem ou como resultado de uma.
```python
lista = [1,2,3,4,5]
novaLista = list(map(lambda n:n*n, lista)) 
#esta função recebe uma função como argumento e aplica ela para todos elementos da lista e retorna uma nova lista
print(novaLista) #[1, 4, 9, 16, 25]

a = lambda x,y:x*y
print(a(5,6))

```

###*Currying*
Currying é um conceito Introduzido por Moses Schönfinkel e depois desenvolvido por Haskell Curry e que consiste em aninhar várias funções de alta ordem para formar uma função.
Ex.:
```python
dividirPor = lambda x: lambda y: y/x
div5 = dividirPor(5)
div5(20) #retorna 4
dividirPor(5)(20) #retorna 4
```

###Map, Filter, Reduce








[1]: http://en.wikipedia.org/wiki/Lambda_calculus

