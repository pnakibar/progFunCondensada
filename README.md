Conceitos de programação funcionais condensados!
================================================


####Programação funcional é magia!
Funcional é o paradigma de programação que o estilo da construção e a estrutura de "montagem" como funções matemáticas
Alguns dos conceitos mais importantes são os que, nela se evita amudança de estado e dados mutáveis.
Programação funcional tem as raízes no Cálculo Lambda[1]

Mas chega de enrolação e vamos aos conceitos ;)


###Recursão em calda


###Otimização da recursão em calda


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
				9*(4+5)		2.
				9*9 		3.
				81			4.
```

No ex5, ele imediatamente avalia o segundo argumento da função, que é *loop*. Ao avaliar ele vai entrar em um *loop* infinito e nunca vai sair, nem mesmo vai retornar o valor na função. Já no ex6 como os argumentos são avaliados posteriormente ele não entra em um *loop* infinito, pois não é avaliado.



###Funções de *n* Ordem



###Funções de *Alta* Ordem



###O conceito de *Currying*




[1]: http://en.wikipedia.org/wiki/Lambda_calculusa

