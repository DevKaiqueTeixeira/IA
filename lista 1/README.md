README DESENVOLVIDO BASEADO NOS MEUS COMENTÁRIOS FEITOS DURANTE O PROJETO NÃO FOI FEITO OLHANDO PRO EXERCICIO APENAS MEUS COMENTÁRIOS ANOTADOS DURANTE TODO O PROCESSO, não é possive visualizar mas existe!

<img width="1777" height="782" alt="image" src="https://github.com/user-attachments/assets/c25ff9f5-74a4-4f64-8066-f1d94ce81174" />



# 🐍 Resumo dos Estudos de Python

Este README reúne os principais conceitos, comandos e lógicas que aprendi durante a resolução dos exercícios de Python.

## 📌 Fundamentos

### `print()`

Usado para exibir informações na tela, como textos, números e variáveis.

```python
print("Olá")
```

### `input()`

Usado para receber informações digitadas pelo usuário.

```python
nome = input("Digite seu nome: ")
```

Quando recebemos números, normalmente precisamos converter o tipo:

```python
numero = int(input("Digite um número: "))
```

### `f-string`

O `f` antes das aspas permite colocar variáveis diretamente dentro do texto.

```python
nome = "Kaique"
print(f"Olá, {nome}")
```

### Operadores matemáticos

`**` representa potenciação:

```python
2 ** 2  # 4
2 ** 3  # 8
```

Parênteses podem ser utilizados para priorizar uma operação matemática:

```python
resultado = (2 + 3) * 4
```

### Operador `%`

Retorna o resto de uma divisão.

```python
10 % 2  # 0
11 % 2  # 1
```

Isso é muito útil para verificar números pares e ímpares:

```python
if numero % 2 == 0:
    print("Par")
else:
    print("Ímpar")
```

Também pode ser utilizado na lógica de números primos.

---

# 🔄 Estruturas de Repetição

## `for` e `range()`

O `for` permite repetir uma determinada ação.

```python
for i in range(0, 11):
    print(i)
```

O `range()` não inclui o último número. Portanto, `range(0, 11)` percorre de `0` até `10`.

Isso pode ser utilizado, por exemplo, para criar uma tabuada:

```python
for i in range(1, 11):
    print(numero * i)
```

## `while`

O `while` mantém o código executando enquanto uma condição for verdadeira.

Pode ser utilizado para criar programas que continuam funcionando até o usuário escolher sair.

---

# 📋 Listas e Dicionários

## `len()`

Retorna a quantidade de elementos ou caracteres.

```python
len("Python")
```

Também pode ser utilizado em listas e matrizes.

Em uma matriz:

```python
len(matriz)
```

retorna a quantidade de linhas.

Já:

```python
len(matriz[0])
```

retorna a quantidade de colunas.

## `append()`

Adiciona um elemento ao final de uma lista.

```python
lista.append(numero)
```

## `count()`

Retorna quantas vezes determinado elemento aparece.

```python
lista.count(5)
```

## `not in`

Permite verificar se um elemento ainda não existe.

```python
if numero not in lista:
    lista.append(numero)
```

Isso é útil para evitar valores repetidos.

---

# 🔢 Funções úteis do Python

## `sum()`

Soma os valores de uma lista.

```python
sum(lista)
```

## `min()` e `max()`

Retornam respectivamente o menor e o maior valor.

```python
min(lista)
max(lista)
```

## `sort()`

Ordena uma lista em ordem crescente.

```python
lista.sort()
```

Para ordem decrescente:

```python
lista.sort(reverse=True)
```

---

# 🔢 Fatorial

O Python possui uma função pronta através da biblioteca `math`:

```python
import math

math.factorial(numero)
```

Também é possível calcular manualmente usando `for`.

Uma operação como:

```python
resultado *= i
```

é uma forma abreviada de:

```python
resultado = resultado * i
```

O mesmo conceito vale para `+=`, `-=`, `/=` etc.

---

# 🔢 Sequência de Fibonacci

A biblioteca `sympy` possui uma função para Fibonacci.

Também é possível implementar a sequência manualmente.

Um conceito importante aprendido foi a atribuição simultânea:

```python
a, b = a + b, a
```

O Python primeiro calcula os valores do lado direito e depois atribui cada resultado às variáveis da esquerda.

---

# 🎲 Números Aleatórios

A biblioteca `random` permite gerar valores aleatórios.

```python
import random

random.randint(1, 6)
```

O `randint()` pode ser utilizado para sortear números dentro de um intervalo.

Isso foi utilizado em exercícios como:

* Sorteio de números;
* Dados de 1 a 6;
* Senhas aleatórias;
* Jogos.

---

# 🔤 Strings e Caracteres

## Inverter uma string

O `[::-1]` percorre a string de trás para frente.

```python
texto[::-1]
```

Também podemos definir outros passos:

```python
texto[::2]
```

Nesse caso, percorremos de 2 em 2.

---

# 🔠 `ord()` e `chr()`

Cada caractere possui uma representação numérica.

Por exemplo:

```python
ord("A")
```

retorna `65`.

E:

```python
chr(65)
```

retorna `"A"`.

Isso foi utilizado para trabalhar com letras, geração de senhas e principalmente na implementação da **Cifra de César**.

---

# 🔐 Cifra de César

A lógica consiste em transformar cada letra em um número, deslocá-la no alfabeto e depois transformar novamente em uma letra.

O alfabeto possui 26 posições, então utilizamos:

```python
valor % 26
```

O `% 26` permite criar um ciclo.

Por exemplo, se estivermos próximos do final do alfabeto e o deslocamento ultrapassar `Z`, o cálculo volta para o início:

```text
X → Y → Z → A → B
```

Assim conseguimos deslocar as letras sem sair dos limites do alfabeto.

---

# 🧮 CPF

Para validar um CPF, utilizamos os primeiros dígitos para realizar multiplicações e somas.

Depois calculamos:

```python
resto = soma % 11
```

Dependendo do resto, o próximo dígito verificador será `0` ou:

```python
11 - resto
```

O mesmo processo é realizado para calcular o segundo dígito.

---

# 🔍 Busca Binária

A Busca Binária trabalha com uma lista **ordenada**.

Primeiro encontramos o meio:

```python
meio = (inicio + fim) // 2
```

O `//` realiza uma divisão inteira, descartando a parte decimal.

Depois comparamos o elemento do meio com o valor procurado.

* Se for igual, encontramos o elemento.
* Se o valor procurado for maior, procuramos na direita.
* Se for menor, procuramos na esquerda.

A grande vantagem é que não precisamos percorrer a lista inteira. A cada comparação, eliminamos aproximadamente metade das possibilidades.

---

# 🔄 Algoritmos de Ordenação

## Bubble Sort

O Bubble Sort compara elementos vizinhos.

Se o elemento da esquerda for maior que o próximo, eles são trocados.

Esse processo continua até que a lista esteja ordenada.

```text
[5, 2, 8]

5 > 2 → troca

[2, 5, 8]
```

## Insertion Sort

O Insertion Sort pega um elemento por vez e coloca esse elemento na posição correta dentro da parte da lista que já está ordenada.

A ideia é semelhante a organizar cartas na mão:

```text
[parte ordenada] + [novo elemento]
```

O novo elemento é comparado com os anteriores até encontrar sua posição correta.

---

# 🔁 Recursividade

Uma função recursiva é uma função que chama ela mesma.

Ela normalmente possui uma condição responsável por determinar quando a recursão deve parar.

```python
def exemplo(numero):
    if numero == 0:
        return
    exemplo(numero - 1)
```

A condição de parada é fundamental para evitar uma execução infinita.

---

# 🔤 Frequência de Palavras e Letras

Para contar palavras, podemos utilizar:

```python
palavras = texto.split()
```

O `split()` separa uma string em partes, normalmente utilizando os espaços.

Depois podemos percorrer cada palavra:

```python
for palavra in palavras:
```

Um dicionário pode armazenar a palavra e sua quantidade:

```python
contagem = {}
```

Na primeira vez que uma palavra aparece, ela recebe `1`.

Quando aparece novamente:

```python
contagem[palavra] += 1
```

Assim:

```text
Python → 1
Python → 2
Python → 3
```

A mesma lógica pode ser utilizada para calcular a frequência de letras.

---

# 🎯 FizzBuzz

A lógica do FizzBuzz utiliza o operador `%`.

* Divisível por `3` → `Fizz`
* Divisível por `5` → `Buzz`
* Divisível por ambos → `FizzBuzz`

```python
if numero % 3 == 0 and numero % 5 == 0:
    print("FizzBuzz")
```

---

# 🎮 Exercícios e Jogos

Alguns exercícios permitiram aplicar os conceitos anteriores em programas mais completos.

### Jogo da Forca

A lógica utilizada foi criar:

1. Uma lista contendo as letras da palavra.
2. Uma segunda lista inicialmente preenchida com `_`.
3. A cada tentativa correta, o caractere correspondente é colocado no índice correto.
4. O jogo continua enquanto a palavra ainda não foi descoberta.

### Tabuleiro

Foi necessário utilizar listas e índices para representar as posições do tabuleiro.

Esse exercício ajudou a compreender melhor como trabalhar com estruturas bidimensionais.

---

# 🔀 Anagramas

Para verificar anagramas, não é necessário que as palavras tenham significado.

O importante é que elas possuam as mesmas letras na mesma quantidade, independentemente da ordem.

Exemplo:

```text
amor
roma
```

São anagramas porque possuem as mesmas letras.

---

# 🧮 Calculadora

Foi desenvolvido um modelo de calculadora utilizando operadores e condições.

A estrutura permite adicionar novos operadores sem precisar modificar toda a lógica do programa.

---

# 🔑 Geração de Senhas

As letras maiúsculas possuem códigos de `65` a `90` na tabela ASCII.

Podemos gerar números aleatórios nesse intervalo, convertê-los utilizando `chr()` e formar uma senha aleatória.

A quantidade de caracteres pode ser definida pelo usuário.

---

# 📚 Principais aprendizados

Durante os exercícios, os principais conceitos praticados foram:

* `print()` e `input()`;
* Conversão de tipos com `int()`;
* `if`, `elif` e `else`;
* `for`, `while` e `range()`;
* Listas e dicionários;
* `append()`, `count()`, `len()`, `sum()`, `min()` e `max()`;
* `sort()` e `reverse`;
* Operadores matemáticos;
* Operador `%`;
* Funções;
* Recursividade;
* Strings e manipulação de caracteres;
* `ord()` e `chr()`;
* Bibliotecas como `math`, `random` e `sympy`;
* Algoritmos de ordenação;
* Busca Binária;
* Bubble Sort;
* Insertion Sort;
* Cifra de César;
* Validação de CPF;
* Frequência de palavras e letras;
* Geração de números e senhas aleatórias;
* Desenvolvimento de pequenos jogos e aplicações.

## 🚀 Conclusão

Os exercícios ajudaram a transformar conceitos básicos de Python em problemas práticos. Além de aprender a sintaxe da linguagem, o principal aprendizado foi desenvolver **lógica de programação**, entendendo como dividir um problema em pequenas etapas e utilizar estruturas de repetição, condições, listas, funções e algoritmos para chegar a uma solução.
