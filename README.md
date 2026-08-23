# Guia de Estudos: NumPy, SciPy, Pandas e Matplotlib

> Material organizado a partir dos exercícios desenvolvidos no Google Colab. O objetivo é transformar os códigos e resultados em um guia de revisão, explicando os conceitos praticados, a finalidade de cada recurso e os principais cuidados de implementação.

## Sumário

1. [Visão geral](#1-visão-geral)
2. [NumPy](#2-numpy)
3. [SciPy](#3-scipy)
4. [Pandas](#4-pandas)
5. [Matplotlib](#5-matplotlib)
6. [Como as bibliotecas trabalham juntas](#6-como-as-bibliotecas-trabalham-juntas)
7. [Correções e melhorias importantes](#7-correções-e-melhorias-importantes)
8. [Síntese das competências desenvolvidas](#8-síntese-das-competências-desenvolvidas)
9. [Próximos passos recomendados](#9-próximos-passos-recomendados)

---

# 1. Visão geral

Os exercícios apresentaram quatro bibliotecas centrais do ecossistema de análise de dados e computação científica em Python:

| Biblioteca | Principal finalidade |
|---|---|
| **NumPy** | Criar e manipular vetores, matrizes e dados numéricos de maneira eficiente. |
| **SciPy** | Resolver problemas científicos, como integração, otimização, equações diferenciais, álgebra linear e transformadas. |
| **Pandas** | Organizar, limpar, transformar, agrupar e exportar dados tabulares. |
| **Matplotlib** | Criar gráficos para analisar e comunicar os dados. |

Essas bibliotecas se complementam. Um fluxo comum é:

1. gerar ou receber dados;
2. armazená-los em arrays do NumPy ou DataFrames do Pandas;
3. realizar cálculos estatísticos ou científicos com NumPy e SciPy;
4. apresentar os resultados com Matplotlib.

## Importações utilizadas

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

No SciPy, normalmente são importadas apenas as funções necessárias:

```python
from scipy.optimize import minimize
from scipy.integrate import quad, solve_ivp
from scipy.linalg import solve
```

O uso de apelidos como `np`, `pd` e `plt` é uma convenção amplamente adotada em projetos Python.

---

# 2. NumPy

## 2.1 O que é um array

O objeto central do NumPy é o `ndarray`, conhecido simplesmente como **array**. Ele pode representar:

- um vetor de uma dimensão;
- uma matriz de duas dimensões;
- estruturas com três ou mais dimensões.

Exemplo de vetor:

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5, 6])
print(array)
```

Saída:

```text
[1 2 3 4 5 6]
```

Exemplo de matriz:

```python
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
```

A forma do array pode ser consultada com:

```python
print(matriz.shape)
```

Resultado:

```text
(3, 3)
```

Isso indica três linhas e três colunas.

## 2.2 Tipos de dados

O parâmetro `dtype` determina o tipo dos elementos armazenados:

```python
array = np.array([1, 2, 3], dtype=int)
```

Alguns tipos comuns:

- `int`: números inteiros;
- `float`: números decimais;
- `bool`: valores verdadeiros ou falsos;
- `str`: textos.

Arrays do NumPy normalmente guardam elementos de um mesmo tipo, o que permite maior eficiência nas operações numéricas.

## 2.3 Criação de arrays

### `np.array()`

Converte listas Python em arrays:

```python
array = np.array([1, 2, 3, 4])
```

### `np.zeros()`

Cria um array preenchido com zeros:

```python
array_zeros = np.zeros((3, 3))
```

Resultado:

```text
[[0. 0. 0.]
 [0. 0. 0.]
 [0. 0. 0.]]
```

### `np.eye()`

Cria uma matriz identidade:

```python
matriz = np.eye(6, dtype=int)
```

A matriz identidade possui `1` na diagonal principal e `0` nas demais posições.

### `np.arange()`

Cria uma sequência numérica semelhante ao `range()` do Python:

```python
pares = np.arange(2, 21, 2)
```

Resultado:

```text
[ 2  4  6  8 10 12 14 16 18 20]
```

O primeiro argumento é o início, o segundo é o limite final exclusivo e o terceiro é o passo.

### `np.random.rand()`

Gera números decimais aleatórios no intervalo de `0` até antes de `1`:

```python
array = np.random.rand(5, 5)
```

### `np.random.randint()`

Gera números inteiros aleatórios:

```python
array = np.random.randint(1, 101, 20)
```

Nesse caso, são gerados 20 números entre 1 e 100. O limite superior, `101`, não é incluído.

## 2.4 Indexação e fatiamento

A indexação permite acessar posições específicas.

```python
array = np.array([10, 20, 30, 40])
print(array[0])
```

Resultado:

```text
10
```

Os índices começam em zero.

Em uma matriz:

```python
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])

primeira_linha = matriz[0, :]
```

- `0` seleciona a primeira linha;
- `:` seleciona todas as colunas.

Outros exemplos:

```python
primeira_coluna = matriz[:, 0]
elemento = matriz[1, 2]
```

## 2.5 Alteração do formato com `reshape`

O método `reshape()` modifica a organização dos dados sem alterar seus valores:

```python
array = np.arange(1, 13)
matriz = array.reshape(3, 4)
```

Resultado:

```text
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

O número total de elementos precisa ser preservado. Um array com 12 elementos pode virar uma matriz `3x4`, `4x3`, `2x6` ou `1x12`, por exemplo.

No material também foi utilizado:

```python
array_reshaped = np.reshape(matriz, (1, 9))
```

Isso transforma uma matriz `3x3` em uma linha com nove elementos.

## 2.6 Operações elemento a elemento

Quando dois arrays possuem formatos compatíveis, as operações aritméticas são realizadas posição por posição.

```python
array1 = np.array([5, 5, 5, 5, 5])
array2 = np.array([1, 2, 3, 4, 5])

soma = array1 + array2
subtracao = array1 - array2
multiplicacao = array1 * array2
```

Resultado da soma:

```text
[ 6  7  8  9 10]
```

Em matrizes, `*` também representa multiplicação elemento a elemento:

```python
matriz1 = np.array([[1, 2], [3, 4]])
matriz2 = np.array([[1, 2], [3, 4]])

resultado = matriz1 * matriz2
```

Resultado:

```text
[[ 1  4]
 [ 9 16]]
```

Isso **não** é multiplicação matricial.

Para multiplicação matricial, pode-se usar:

```python
resultado = matriz1 @ matriz2
```

ou:

```python
resultado = np.dot(matriz1, matriz2)
```

## 2.7 Produto escalar

O produto escalar de dois vetores multiplica os elementos correspondentes e soma os resultados:

```python
vetor1 = np.array([1, 2, 3])
vetor2 = np.array([4, 5, 6])

produto_escalar = np.dot(vetor1, vetor2)
```

Cálculo:

```text
1×4 + 2×5 + 3×6 = 32
```

O produto escalar é utilizado em álgebra linear, geometria, aprendizado de máquina e cálculo de similaridade entre vetores.

## 2.8 Funções de agregação

Foram praticadas várias funções que resumem os dados:

| Função | Finalidade |
|---|---|
| `np.sum()` | Soma os elementos. |
| `np.mean()` | Calcula a média. |
| `np.median()` | Calcula a mediana. |
| `np.std()` | Calcula o desvio padrão. |
| `np.min()` | Retorna o menor valor. |
| `np.max()` | Retorna o maior valor. |
| `np.cumsum()` | Calcula a soma acumulada. |

Exemplo:

```python
array = np.array([5, 5, 5, 5, 5])

print(np.mean(array))
print(np.std(array))
```

Como todos os valores são iguais, a média é `5` e o desvio padrão é `0`.

## 2.9 Uso do parâmetro `axis`

O parâmetro `axis` determina a direção da operação.

Considere:

```python
matriz = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

### Operação por coluna

```python
np.sum(matriz, axis=0)
```

Resultado:

```text
[5 7 9]
```

### Operação por linha

```python
np.sum(matriz, axis=1)
```

Resultado:

```text
[ 6 15]
```

No exercício da matriz `5x5`, `axis=0` foi usado para somar cada coluna. No exercício final de NumPy, `axis=1` foi usado para encontrar o menor valor de cada linha.

## 2.10 Máscaras booleanas

Uma máscara booleana seleciona elementos que atendem a uma condição.

### Substituir múltiplos de 3

```python
array[array % 3 == 0] = -3
```

A expressão `array % 3 == 0` identifica posições em que o resto da divisão por 3 é zero.

### Limitar valores acima de 50

```python
array[array > 50] = 50
```

Isso aplica um teto de 50.

### Substituir múltiplos de 5

```python
array[array % 5 == 0] = 0
```

As máscaras são uma das formas mais importantes de manipular dados com NumPy sem escrever laços explícitos.

## 2.11 Diagonal de uma matriz

A função `np.fill_diagonal()` altera a diagonal principal:

```python
matriz = np.random.randint(1, 101, (4, 4))
np.fill_diagonal(matriz, 7)
```

Também foi criada uma diagonal crescente:

```python
matriz = np.eye(6, dtype=int)
np.fill_diagonal(matriz, np.arange(1, 7))
```

Resultado:

```text
[[1 0 0 0 0 0]
 [0 2 0 0 0 0]
 [0 0 3 0 0 0]
 [0 0 0 4 0 0]
 [0 0 0 0 5 0]
 [0 0 0 0 0 6]]
```

## 2.12 Moda com `np.unique()`

Para encontrar a moda, foram obtidos os valores únicos e suas frequências:

```python
valores, quantidades = np.unique(array, return_counts=True)
moda = valores[np.argmax(quantidades)]
```

Etapas:

1. `np.unique()` identifica os valores diferentes;
2. `return_counts=True` conta quantas vezes cada valor aparece;
3. `np.argmax()` retorna a posição da maior frequência;
4. essa posição é usada para selecionar a moda.

## 2.13 Normalização Min-Max

A normalização coloca os valores no intervalo entre 0 e 1:

```python
normalizado = (
    (array - np.min(array))
    / (np.max(array) - np.min(array))
)
```

A fórmula é:

```text
valor normalizado = (x - mínimo) / (máximo - mínimo)
```

O menor valor se torna `0`, o maior se torna `1` e os demais ficam proporcionalmente entre esses extremos.

Essa técnica é muito utilizada antes de treinar modelos de aprendizado de máquina ou quando variáveis possuem escalas diferentes.

## 2.14 Correlação

A correlação entre dois arrays foi calculada com:

```python
correlacao = np.corrcoef(array1, array2)[0, 1]
```

O coeficiente costuma variar entre `-1` e `1`:

- próximo de `1`: relação linear positiva forte;
- próximo de `-1`: relação linear negativa forte;
- próximo de `0`: pouca relação linear.

Uma correlação negativa, como a obtida no exercício, significa que valores maiores em um vetor tendem, naquele conjunto, a aparecer associados a valores menores no outro. Isso não prova uma relação de causa e efeito.

## 2.15 Norma e ângulo entre vetores

A norma representa o comprimento de um vetor:

```python
modulo = np.linalg.norm(array)
```

O ângulo entre dois vetores foi obtido por:

```python
produto_escalar = np.dot(array1, array2)
modulo1 = np.linalg.norm(array1)
modulo2 = np.linalg.norm(array2)

cos_angulo = produto_escalar / (modulo1 * modulo2)
angulo = np.arccos(cos_angulo)
angulo_graus = np.degrees(angulo)
```

A fórmula utilizada é:

```text
cos(θ) = (a · b) / (||a|| × ||b||)
```

Essa ideia é utilizada, por exemplo, na similaridade de cosseno.

Uma versão numericamente mais segura seria:

```python
cos_angulo = np.clip(cos_angulo, -1, 1)
```

Isso evita erros causados por pequenas imprecisões de ponto flutuante.

## 2.16 Determinante e matriz inversa

O determinante foi calculado com:

```python
determinante = np.linalg.det(matriz)
```

O determinante é um único número associado a uma matriz quadrada. Entre outras interpretações, ele ajuda a verificar se a matriz possui inversa:

- determinante diferente de zero: a matriz é invertível;
- determinante igual a zero: a matriz é singular e não possui inversa.

A matriz inversa é calculada de outra forma:

```python
inversa = np.linalg.inv(matriz)
```

Portanto, o código que chamou o resultado de `inversionMatriz`, mas utilizou `np.linalg.det()`, calculou o **determinante**, não a inversa.

## 2.17 Resumo dos exercícios de NumPy

| Exercício | Conteúdo praticado |
|---|---|
| Estudo inicial | Criação de arrays, zeros, números aleatórios, soma, média, produto escalar, desvio padrão, fatiamento, `reshape` e determinante. |
| Manipulação de array | Criação de matriz aleatória `3x3`, máximo, mínimo e soma total. |
| Produto escalar | Aplicação de `np.dot()` entre dois vetores. |
| Operações matemáticas | Soma, subtração e multiplicação elemento a elemento entre matrizes. |
| 1 | Geração de 50 inteiros aleatórios entre 10 e 100. |
| 2 | Montagem gradual de uma matriz `2x4` com valores aleatórios. |
| 3 | Criação de vetor-coluna com zeros e alteração das posições de 5 a 10 para 1. |
| 4 | Geração de 100 valores e cálculo de moda e mediana. |
| 5 | Substituição dos múltiplos de 3 por `-3`. |
| 6 | Criação de matriz decimal `5x5` e soma de cada coluna. |
| 7 | Cálculo de correlação entre dois vetores. |
| 8 | Elevação de cada elemento de uma matriz ao quadrado. |
| 9 | Normalização Min-Max de um vetor. |
| 10 | Criação de matriz diagonal com valores de 1 a 6. |
| 11 | Cálculo manual da moda com valores únicos e contagens. |
| Exercício adicional de pares | Geração de dez números pares aleatórios. |
| 12 | Substituição da diagonal principal de uma matriz por 7. |
| 13 | Criação dos pares de 2 a 20 e soma cumulativa. |
| 14 | Diferença entre dois vetores e média das diferenças. |
| 15 | Limitação dos valores maiores que 50. |
| 16 | Conversão de um vetor de 12 posições em matriz `3x4`. |
| 17 | Multiplicação elemento a elemento por uma matriz de posições. |
| 18 | Substituição dos múltiplos de 5 por zero. |
| 19 | Produto escalar, normas e ângulo entre vetores. |
| 20 | Menor valor de cada linha de uma matriz. |

## 2.18 Boas práticas adicionais para NumPy

### Evitar `np.append()` repetidamente em laços

O material criou arrays vazios e utilizou `np.append()` várias vezes. Isso funciona, mas pode ser ineficiente porque um novo array é criado a cada repetição.

Uma alternativa mais direta para gerar 50 números é:

```python
lista = np.random.randint(10, 101, 50)
```

Para gerar dez pares:

```python
pares = np.random.randint(0, 51, 10) * 2
```

### Reproduzir resultados aleatórios

Como os valores são aleatórios, os resultados mudam a cada execução. Para repetir exatamente o mesmo experimento:

```python
rng = np.random.default_rng(42)
array = rng.integers(1, 101, 20)
```

Essa é uma recomendação adicional de organização e reprodutibilidade.

---

# 3. SciPy

## 3.1 Relação entre NumPy e SciPy

O SciPy utiliza os arrays do NumPy e acrescenta algoritmos científicos mais especializados. Nos exercícios foram trabalhados os módulos:

| Módulo | Uso praticado |
|---|---|
| `scipy.integrate` | Integrais e equações diferenciais. |
| `scipy.optimize` | Otimização, ajuste de curvas e raízes. |
| `scipy.fft` | Transformadas de Fourier. |
| `scipy.linalg` | Álgebra linear. |
| `scipy.interpolate` | Interpolação de valores. |
| `scipy.special` | Funções matemáticas especiais. |

## 3.2 Integração numérica com `quad`

A função `quad()` calcula numericamente uma integral definida:

```python
import numpy as np
from scipy.integrate import quad

def f(x):
    return x**2 * np.sin(x)

resultado, erro = quad(f, 0, np.pi)
```

A integral calculada foi:

```text
∫₀^π x² sen(x) dx
```

O resultado numérico foi aproximadamente:

```text
5.869604401089359
```

A função retorna dois valores:

- `resultado`: aproximação da integral;
- `erro`: estimativa do erro numérico.

## 3.3 Integral dupla com `dblquad`

O exercício também calculou uma integral de duas variáveis:

```python
from scipy.integrate import dblquad

def f(y, x):
    return x*y + x**2

resultado, erro = dblquad(
    f,
    0, 2,
    lambda x: 0,
    lambda x: 1
)
```

O intervalo externo de `x` é de 0 a 2, e o intervalo interno de `y` é de 0 a 1.

O resultado foi:

```text
3.666666666666667
```

## 3.4 Equações diferenciais com `solve_ivp`

### Equação de primeira ordem

Foi resolvida a equação:

```text
y' = x - y
```

com condição inicial:

```text
y(0) = 1
```

Código:

```python
from scipy.integrate import solve_ivp


def f(x, y):
    return x - y

solucao = solve_ivp(
    f,
    [0, 10],
    [1],
    t_eval=np.linspace(0, 10, 100)
)
```

Elementos importantes:

- `[0, 10]`: intervalo da variável independente;
- `[1]`: condição inicial;
- `t_eval`: pontos em que a solução será avaliada;
- `solucao.t`: valores da variável independente;
- `solucao.y[0]`: valores aproximados da solução.

### Equação de segunda ordem

Também foi resolvida:

```text
y'' = -y
```

Uma equação de segunda ordem é convertida em um sistema de duas equações de primeira ordem:

```python
def f(x, valores):
    y = valores[0]
    derivada = valores[1]
    return [derivada, -y]
```

Com as condições:

```text
y(0) = 1
y'(0) = 0
```

Código:

```python
solucao = solve_ivp(
    f,
    [0, 10],
    [1, 0],
    t_eval=np.linspace(0, 10, 100)
)
```

A solução apresenta comportamento oscilatório semelhante ao cosseno.

## 3.5 Otimização com `minimize`

A função `minimize()` procura valores de entrada que reduzam uma função ao menor resultado possível.

### Função constante

No exercício introdutório:

```python
def f(x):
    return 10 + 10 + 10
```

A função sempre retorna 30, independentemente de `x`. Portanto, qualquer valor de `x` é um ponto de mínimo e o algoritmo manteve o chute inicial `0`.

Esse exercício demonstra a chamada da função, mas não representa um problema real de otimização, pois não existe variação no resultado.

### Maximização por minimização do negativo

O SciPy possui uma função de minimização. Para maximizar:

```text
-x² + 4x + 1
```

foi minimizado o seu negativo:

```python
def f(x):
    return -(-x**2 + 4*x + 1)

resultado = minimize(f, [0])
```

Resultado aproximado:

```text
x = 2
valor máximo = 5
```

### Otimização com duas variáveis

Foi minimizada a função:

```text
(x - 2)² + (y - 3)²
```

Código:

```python
def f(valores):
    x, y = valores
    return (x - 2)**2 + (y - 3)**2

resultado = minimize(f, [0, 0])
```

O mínimo ocorre próximo de:

```text
x = 2
y = 3
valor mínimo = 0
```

O pequeno resultado numérico próximo de `10⁻¹⁶` deve ser interpretado como zero dentro da precisão computacional.

## 3.6 Busca de raízes com `root`

Uma raiz é um valor em que a função se torna zero.

Foi analisada:

```text
x⁴ - 3x³ + 2 = 0
```

Código simplificado:

```python
from scipy.optimize import root


def f(x):
    return x**4 - 3*x**3 + 2

resultado = root(f, 1)
```

Vários chutes iniciais foram utilizados para procurar raízes diferentes. O código também verificou se uma raiz semelhante já estava na lista, evitando repetições.

Foram encontradas duas raízes reais aproximadas:

```text
1.0
2.9196395658
```

Métodos baseados em chutes iniciais podem convergir para raízes diferentes ou falhar, dependendo do ponto inicial.

## 3.7 Busca de raízes com `brentq`

O método `brentq()` procura uma raiz em um intervalo onde a função troca de sinal.

```python
from scipy.optimize import brentq


def f(x):
    return np.exp(x) - x**2

raiz = brentq(f, -1, 0)
```

Resultado:

```text
-0.7034674225
```

Para usar `brentq`, é necessário que os valores da função nas extremidades do intervalo possuam sinais opostos.

## 3.8 Ajuste de curva com `curve_fit`

Foi ajustada uma função quadrática:

```text
y = ax² + bx + c
```

Código:

```python
from scipy.optimize import curve_fit

x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 5, 7, 8])


def funcao(x, a, b, c):
    return a*x**2 + b*x + c

parametros, covariancia = curve_fit(funcao, x, y)
```

Coeficientes encontrados:

```text
a ≈ -0.07143
b ≈ 1.92857
c ≈ 0.20
```

O `curve_fit()` estima os parâmetros que fazem a curva se aproximar dos pontos observados, normalmente minimizando os erros quadráticos.

## 3.9 Transformada de Fourier

A Transformada de Fourier decompõe um sinal em frequências.

### Transformada direta

```python
from scipy.fft import fft, fftfreq

transformada = fft(sinal)
frequencias = fftfreq(len(t), t[1] - t[0])
```

O resultado da FFT é um vetor de números complexos. Para estudar a intensidade de cada frequência, geralmente se utiliza o módulo:

```python
amplitude = np.abs(transformada)
```

Foram analisados sinais formados por senos e cossenos, como:

```python
sinal = (
    np.sin(2 * np.pi * 5 * x)
    + np.cos(2 * np.pi * 10 * x)
)
```

Esse sinal contém componentes principais próximas de 5 Hz e 10 Hz, considerando a forma como a amostragem foi definida.

### Transformada inversa

A função `ifft()` realiza o processo inverso:

```python
from scipy.fft import ifft

resultado = ifft(sinal_complexo)
```

Ela transforma uma representação no domínio da frequência em uma sequência no domínio original.

## 3.10 Álgebra linear com SciPy

### Matriz inversa

```python
from scipy.linalg import inv

inversa = inv(matriz)
```

Uma matriz inversa `A⁻¹` satisfaz:

```text
A × A⁻¹ = I
```

A matriz precisa ser quadrada e não singular.

### Sistemas lineares

Para resolver:

```text
A × x = B
```

foi utilizado:

```python
from scipy.linalg import solve

resultado = solve(A, B)
```

Exemplo `2x2`:

```python
A = np.array([
    [3, 2],
    [1, 4]
])
B = np.array([5, 6])
```

Solução:

```text
x = 0.8
y = 1.3
```

Também foi resolvido um sistema `3x3`, obtendo valores para `x`, `y` e `z`.

Em problemas reais, `solve(A, B)` costuma ser preferível a calcular explicitamente `inv(A) @ B`, pois é mais direto e numericamente mais adequado.

### Determinante

```python
from scipy.linalg import det

determinante = det(matriz)
```

O exercício calculou o determinante de uma matriz aleatória `6x6`.

### Autovalores e autovetores

```python
from scipy.linalg import eig

autovalores, autovetores = eig(matriz)
```

Para uma matriz `A`, um autovetor `v` e um autovalor `λ` satisfazem:

```text
A × v = λ × v
```

Eles são utilizados em redução de dimensionalidade, sistemas dinâmicos, análise de estabilidade, física e diversos métodos de ciência de dados.

Os resultados podem ser complexos mesmo quando a matriz contém apenas números reais.

## 3.11 Interpolação com `CubicSpline`

A interpolação estima valores entre pontos conhecidos.

```python
from scipy.interpolate import CubicSpline

x = np.array([0, 1, 2, 3, 4])
y = np.array([0, 2, 3, 5, 4])

spline = CubicSpline(x, y)
novos_x = np.linspace(0, 4, 10)
novos_y = spline(novos_x)
```

A spline cúbica cria uma curva suave composta por polinômios de terceiro grau.

Outro exercício utilizou:

```python
x = np.array([1, 2, 3, 4, 5])
y = x**2
```

Os valores intermediários calculados foram exatamente os quadrados esperados:

```text
1.5² = 2.25
2.5² = 6.25
3.5² = 12.25
4.5² = 20.25
```

## 3.12 Funções especiais

Foi usada a função de raiz cúbica:

```python
from scipy.special import cbrt

resultado = cbrt(27)
```

Resultado:

```text
3.0
```

## 3.13 Resumo dos exercícios de SciPy

| Exercício | Conteúdo praticado |
|---|---|
| Exercício introdutório | Uso de `minimize()` em uma função constante. |
| 1 | Integral definida de `x² sen(x)` com `quad()`. |
| 2 | Equação diferencial de primeira ordem com `solve_ivp()`. |
| 3 | Busca de raízes de um polinômio com vários chutes iniciais e `root()`. |
| 4 | Maximização de uma parábola por minimização de sua função negativa. |
| 5 | FFT e criação do vetor de frequências. |
| 6 | Inversão de uma matriz `5x5`. |
| 7 | Interpolação cúbica entre pontos. |
| 8 | Solução de sistema linear `2x2`. |
| 9 | Ajuste de curva quadrática com `curve_fit()`. |
| 10 | Integral dupla com `dblquad()`. |
| 11 | Cálculo de autovalores e autovetores. |
| 12 | Busca de uma raiz em intervalo com `brentq()`. |
| 13 | Determinante de matriz `6x6`. |
| 14 | Minimização de função de duas variáveis. |
| 15 | Transformada inversa de Fourier. |
| 16 | Equação diferencial de segunda ordem convertida em sistema. |
| 17 | Raiz cúbica com `cbrt()`. |
| 18 | Interpolação da função quadrática. |
| 19 | FFT de sinal com frequências de 5 e 10 ciclos por unidade de tempo. |
| 20 | Solução de sistema linear `3x3`. |

## 3.14 Cuidados importantes em SciPy

- Uma função constante não permite identificar um mínimo único.
- `root()` depende do chute inicial e não garante encontrar todas as raízes.
- `brentq()` exige um intervalo válido com troca de sinal.
- Uma matriz aleatória pode ser singular ou numericamente instável.
- Na FFT, imprimir todos os números complexos costuma ser menos informativo do que analisar frequência e amplitude.
- Para amostras periódicas, geralmente é útil criar o eixo temporal com `endpoint=False`:

```python
t = np.linspace(0, 1, 1000, endpoint=False)
```

Essa última observação é uma boa prática adicional para análises de sinais.

---

# 4. Pandas

## 4.1 O que é um DataFrame

O `DataFrame` é uma estrutura tabular com linhas e colunas, semelhante a uma planilha ou tabela de banco de dados.

```python
import pandas as pd

dados = {
    "Produto": ["Arroz", "Feijão", "Macarrão", "Leite", "Café"],
    "Preço": [25.00, 8.50, 6.00, 5.50, 15.00],
    "Quantidade": [10, 20, 15, 30, 8]
}

df = pd.DataFrame(dados)
```

Cada chave do dicionário se torna uma coluna, e cada lista fornece seus valores.

## 4.2 Leitura de arquivos

### Excel

```python
df = pd.read_excel("vendas.xlsx")
```

### CSV

```python
df = pd.read_csv("resultados.csv")
```

No Google Colab, o upload foi feito com:

```python
from google.colab import files
files.upload()
```

E o download com:

```python
files.download("resultados.csv")
```

## 4.3 `head()` e `tail()`

O método `head()` mostra as primeiras linhas:

```python
print(df.head(10))
```

O método `tail()` mostra as últimas:

```python
print(df.tail(5))
```

Eles ajudam a inspecionar rapidamente a estrutura dos dados.

## 4.4 Separação de uma coluna por delimitador

O arquivo de vendas apareceu carregado em uma única coluna, com valores separados por vírgulas. Por isso foi aplicado:

```python
df = df.iloc[:, 0].str.split(",", expand=True)
```

Etapas:

- `df.iloc[:, 0]`: seleciona a primeira coluna;
- `.str.split(",")`: separa o texto em cada vírgula;
- `expand=True`: transforma as partes em novas colunas.

Depois, os nomes foram definidos:

```python
df.columns = [
    "Produto",
    "Quantidade",
    "Valor Unitário (R$)"
]
```

Esse procedimento funcionou para a estrutura encontrada, mas o ideal é corrigir o arquivo de origem ou usar o leitor adequado. Um arquivo realmente delimitado por vírgulas normalmente deveria ser lido com `pd.read_csv()`.

## 4.5 Conversão de tipos

Após separar as colunas, os números ainda podiam estar armazenados como texto. A conversão foi feita com:

```python
df["Quantidade"] = pd.to_numeric(df["Quantidade"])
df["Valor Unitário (R$)"] = pd.to_numeric(
    df["Valor Unitário (R$)"]
)
```

Operações matemáticas e comparações numéricas dependem de tipos corretos.

## 4.6 Filtragem de linhas

### Valores acima de 100

```python
resultado = df[df["Valor Unitário (R$)"] > 100]
```

O resultado foi um DataFrame vazio porque nenhum valor unitário da tabela era superior a R$ 100. Isso não significa que o filtro esteja incorreto; significa apenas que nenhuma linha satisfez a condição.

### Textos iniciados por determinada letra

```python
resultado = df[df["Produto"].str.startswith("B")]
```

Foram selecionados produtos como `Batata` e `Biscoito`.

## 4.7 Criação de colunas calculadas

### Desconto de 10%

```python
df["Desconto"] = df["Valor Unitário (R$)"] * 0.10
```

### Valor total

```python
df["Total"] = (
    df["Valor Unitário (R$)"]
    * df["Quantidade"]
)
```

### Imposto de 5%

```python
df["Imposto"] = df["Total"] * 0.05
```

Esses exemplos mostram como criar variáveis derivadas sem percorrer manualmente cada linha.

## 4.8 Tratamento de valores ausentes

### Remover linhas incompletas

```python
df = df.dropna()
```

O `dropna()` remove linhas que possuem pelo menos um valor ausente.

### Preencher pela mediana

```python
mediana = df["Preço"].median()
df["Preço"] = df["Preço"].fillna(mediana)
```

A mediana é menos sensível a valores extremos do que a média.

No exercício, os preços ausentes foram preenchidos com `14.9`.

### Interpolação linear

```python
df["Vendas"] = df["Vendas"].interpolate(method="linear")
```

Com os dados:

```text
100, ausente, 300, ausente, 500
```

foram estimados:

```text
100, 200, 300, 400, 500
```

A interpolação é mais apropriada quando existe uma ordem natural, como tempo, distância ou posição.

## 4.9 Ordenação

```python
df = df.sort_values(by="Produto")
```

Por padrão, a ordenação é crescente. Para ordem decrescente:

```python
df = df.sort_values(
    by="Valor Unitário (R$)",
    ascending=False
)
```

## 4.10 Agrupamento com `groupby()`

O agrupamento reúne linhas por uma categoria e aplica uma operação de resumo.

```python
resultado = (
    df.groupby("Categoria")["Quantidade"]
    .sum()
)
```

Isso calculou a quantidade total de produtos em cada categoria.

Outro exercício calculou a mediana:

```python
resultado = (
    df.groupby("Categoria")["Valor"]
    .median()
)
```

Resultados:

```text
A = 15
B = 20
C = 35
```

## 4.11 Tabela dinâmica com `pivot_table()`

```python
tabela = pd.pivot_table(
    df,
    values="Quantidade",
    index="Categoria",
    aggfunc="sum"
)
```

A tabela dinâmica produziu um resumo equivalente ao `groupby()` utilizado anteriormente, organizando a soma das quantidades por categoria.

## 4.12 Junção de tabelas com `merge()`

Foram criados dois DataFrames:

```python
df1 = pd.DataFrame({
    "ID": [1, 2, 3, 4],
    "Produto": ["Arroz", "Feijão", "Macarrão", "Café"]
})

df2 = pd.DataFrame({
    "ID": [1, 2, 3, 4],
    "Categoria": ["Grãos", "Grãos", "Massas", "Bebidas"]
})
```

A junção foi realizada por `ID`:

```python
resultado = df1.merge(
    df2,
    on="ID",
    how="inner"
)
```

O `inner` mantém somente chaves existentes nas duas tabelas.

Outros tipos comuns:

- `left`: preserva todas as linhas da tabela da esquerda;
- `right`: preserva todas as linhas da direita;
- `outer`: preserva todas as chaves das duas tabelas.

## 4.13 Valores duplicados

O código verificou duplicidade em cada coluna:

```python
for coluna in df.columns:
    if df[coluna].duplicated().any():
        print(f"A coluna '{coluna}' possui valores duplicados.")
```

Isso responde se uma coluna possui valores repetidos.

Para detectar linhas completamente duplicadas, utiliza-se:

```python
df.duplicated().any()
```

Para remover linhas duplicadas:

```python
df = df.drop_duplicates()
```

## 4.14 Seleção de colunas numéricas

```python
resultado = df.select_dtypes(include="number").mean()
```

Etapas:

1. seleciona apenas as colunas numéricas;
2. calcula a média de cada uma.

No exercício, foram calculadas as médias de `Quantidade` e `Preco`.

## 4.15 Exportação para CSV

```python
df.to_csv("resultados.csv", index=False)
```

O argumento `index=False` evita que o índice do DataFrame seja salvo como uma coluna adicional.

Quando o resultado é uma `Series`, também é possível usar:

```python
resultado.to_csv("resultados.csv")
```

## 4.16 Gráfico diretamente pelo Pandas

```python
df.plot(
    x="Produto",
    y="Quantidade",
    kind="bar"
)
plt.show()
```

O Pandas utiliza o Matplotlib por baixo para criar o gráfico.

## 4.17 Resumo dos exercícios de Pandas

| Exercício | Conteúdo praticado |
|---|---|
| 1 | Criação de DataFrame a partir de um dicionário. |
| 2 | Upload no Colab, leitura de Excel e inspeção com `head()`. |
| 3 | Separação da coluna por vírgulas, conversão numérica e filtro de preços acima de 100. |
| 4 | Criação de coluna de desconto de 10%. |
| 5 | Remoção de valores ausentes com `dropna()`. |
| 6 | Ordenação alfabética dos produtos. |
| 7 | Cálculo do total por produto e exportação para CSV. |
| 8 | Criação de categoria e soma de quantidades com `groupby()`. |
| 9 | Exportação do resultado agrupado. |
| 10 | Leitura do CSV e exibição das últimas cinco linhas. |
| 11 | Preenchimento de preços ausentes pela mediana. |
| 12 | Verificação de valores duplicados em cada coluna. |
| 13 | Tabela dinâmica por categoria. |
| 14 | Junção de duas tabelas com `merge()`. |
| 15 | Interpolação linear de valores ausentes. |
| 16 | Gráfico de barras criado a partir de DataFrame. |
| 17 | Criação de coluna de imposto de 5%. |
| 18 | Filtro de textos iniciados pela letra B. |
| 19 | Média de todas as colunas numéricas. |
| 20 | Mediana de valores agrupados por categoria. |

## 4.18 Pontos de atenção nos exercícios de Pandas

### Estrutura do arquivo de vendas

Embora o arquivo tenha sido lido com `read_excel()`, seu conteúdo apareceu como texto separado por vírgulas em uma única coluna. Isso sugere que a estrutura real não estava organizada como uma planilha Excel convencional.

Uma alternativa seria:

```python
df = pd.read_csv("vendas.csv")
```

ou corrigir a planilha para que cada campo esteja em sua própria coluna.

### Variável `resultado` no exercício 7

Antes de salvar `df`, apareceu:

```python
resultado.to_csv("resultados.csv")
```

Nesse ponto, `resultado` pode vir de uma célula anterior ou nem estar definido. A versão mais segura é manter apenas:

```python
df.to_csv("resultados.csv", index=False)
```

### Categorias atribuídas manualmente

Algumas categorias usadas nos exercícios não correspondem semanticamente aos produtos. Por exemplo, itens de limpeza ou alimentos foram associados a `Eletrônicos` ou `Informática`.

Isso não impede o aprendizado técnico de `groupby()` e `pivot_table()`, mas, em uma análise real, as categorias precisam representar corretamente os dados.

---

# 5. Matplotlib

## 5.1 Estrutura básica de um gráfico

Um gráfico simples pode ser criado com:

```python
import matplotlib.pyplot as plt

plt.plot(x, y)
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")
plt.title("Título")
plt.grid()
plt.show()
```

Elementos principais:

- `plot()`: desenha uma linha;
- `xlabel()`: nome do eixo horizontal;
- `ylabel()`: nome do eixo vertical;
- `title()`: título;
- `grid()`: grade de referência;
- `show()`: exibe a figura.

## 5.2 Gráfico de linha

Foi criada a função cúbica:

```python
x = np.linspace(-10, 10, 100)
y = x**3

plt.plot(x, y)
```

O `np.linspace()` cria valores igualmente espaçados e torna a curva visualmente suave.

Outros gráficos de linha representaram:

- `y = x²`;
- `y = 1/x`;
- `y = x`;
- várias funções na mesma figura.

## 5.3 Gráfico de dispersão

```python
plt.scatter(x, y)
```

O gráfico de dispersão é útil para observar relações entre duas variáveis.

### Cor baseada em uma variável

```python
plt.scatter(x, y, c=y, cmap="viridis")
plt.colorbar(label="Valores de y")
```

A cor passou a representar os valores de `y`.

### Tamanho variável

```python
tamanho = y * 500
plt.scatter(x, y, s=tamanho)
```

O parâmetro `s` controla a área dos marcadores. Esse tipo de gráfico é próximo de um gráfico de bolhas.

## 5.4 Histograma

```python
valores = np.random.randint(0, 101, 500)
plt.hist(valores, bins=10)
```

Um histograma divide os valores em intervalos e mostra quantas observações existem em cada faixa.

O parâmetro `bins=10` define dez intervalos.

Histogramas são úteis para analisar:

- formato da distribuição;
- concentração dos valores;
- assimetria;
- possíveis valores extremos.

## 5.5 Gráfico de barras

```python
plt.bar(categorias, valores)
```

Esse gráfico compara valores entre categorias.

### Barras horizontais

```python
plt.barh(categorias, valores)
```

Barras horizontais podem facilitar a leitura quando os nomes das categorias são longos.

### Valores positivos e negativos

No exercício, as barras receberam cores diferentes conforme o sinal do valor:

```python
cores = [
    "green" if valor >= 0 else "red"
    for valor in valores
]
```

Também foi adicionada uma linha em zero:

```python
plt.axhline(0)
```

### Barras empilhadas

```python
plt.bar(categorias, grupo1, label="Grupo 1")
plt.bar(
    categorias,
    grupo2,
    bottom=grupo1,
    label="Grupo 2"
)
```

O parâmetro `bottom` define onde a nova série começa verticalmente.

Para o terceiro grupo, foi calculada a soma das bases anteriores.

## 5.6 Gráfico de setores

```python
plt.pie(
    porcentagens,
    labels=setores,
    autopct="%1.1f%%"
)
```

O parâmetro `autopct` exibe a porcentagem com uma casa decimal.

Esse gráfico mostra a participação de cada categoria no total. Ele funciona melhor quando existem poucas categorias e diferenças fáceis de perceber.

## 5.7 Subgráficos

Foram colocadas duas funções em áreas separadas da mesma figura:

```python
plt.subplot(2, 1, 1)
plt.plot(x, y1)

plt.subplot(2, 1, 2)
plt.plot(x, y2)

plt.tight_layout()
```

`subplot(2, 1, 1)` significa:

- duas linhas;
- uma coluna;
- primeiro gráfico.

`plt.tight_layout()` ajusta os espaços para reduzir sobreposição.

## 5.8 Faixa ao redor de uma curva

```python
plt.plot(x, y)
plt.fill_between(
    x,
    y - erro,
    y + erro,
    alpha=0.3
)
```

O `fill_between()` preenche a região entre duas curvas.

No exercício, foi utilizada uma margem fixa de `0.2` ao redor do seno. Visualmente, isso representa uma faixa de incerteza. Entretanto, como o valor não foi calculado a partir de uma amostra ou modelo estatístico, ele não deve ser interpretado automaticamente como um intervalo de confiança estatístico real.

## 5.9 Grade e estilos de linha

### Grade personalizada

```python
plt.grid(
    True,
    linestyle="--",
    linewidth=0.5
)
```

### Diferentes estilos de linha

```python
plt.plot(x, y1, linestyle="-")
plt.plot(x, y2, linestyle="--")
plt.plot(x, y3, linestyle=":")
```

Os estilos ajudam a diferenciar séries, inclusive em impressões sem cores.

## 5.10 Limites dos eixos

```python
plt.xlim(-5, 5)
```

O gráfico original de `x²` foi calculado entre `-10` e `10`, mas a visualização foi limitada ao intervalo de `-5` a `5`.

Também existem:

```python
plt.ylim(valor_minimo, valor_maximo)
```

## 5.11 Marcas dos eixos

```python
plt.xticks(np.arange(-10, 11, 2))
plt.yticks(np.arange(0, 101, 10))
```

Isso definiu manualmente os intervalos exibidos nos eixos.

## 5.12 Legenda

Quando existem várias séries:

```python
plt.plot(x, y1, label="y = x")
plt.plot(x, y2, label="y = x²")
plt.legend()
```

O `label` nomeia a série e `legend()` exibe a legenda.

## 5.13 Anotação de texto

```python
plt.text(5, 25, "Ponto x = 5")
```

O texto é posicionado nas coordenadas `x=5` e `y=25`.

Para destacar um ponto com seta, uma alternativa é:

```python
plt.annotate(
    "Ponto x = 5",
    xy=(5, 25),
    xytext=(6, 40),
    arrowprops={"arrowstyle": "->"}
)
```

Essa é uma forma adicional de anotação.

## 5.14 Gráfico 3D

```python
fig = plt.figure()
ax = fig.add_subplot(111, projection="3d")
ax.scatter(x, y, z)
```

Foram configurados três eixos:

```python
ax.set_xlabel("X")
ax.set_ylabel("Y")
ax.set_zlabel("Z")
```

Gráficos 3D podem ser úteis para explorar três variáveis, embora muitas vezes uma visualização 2D com cor ou tamanho seja mais fácil de interpretar.

## 5.15 Salvamento de gráficos

```python
plt.savefig("grafico.pdf")
plt.show()
```

O gráfico foi salvo em PDF antes da exibição.

Uma versão com ajustes adicionais seria:

```python
plt.savefig(
    "grafico.pdf",
    bbox_inches="tight"
)
```

Para imagem rasterizada:

```python
plt.savefig(
    "grafico.png",
    dpi=300,
    bbox_inches="tight"
)
```

## 5.16 Resumo dos exercícios de Matplotlib

| Exercício | Conteúdo praticado |
|---|---|
| 1 | Gráfico de linha da função `y = x³`. |
| 2 | Dispersão com cor baseada em `y` e barra de cores. |
| 3 | Histograma de 500 números aleatórios. |
| 4 | Gráfico de barras com cores diferentes. |
| 5 | Gráfico de setores com porcentagens. |
| 6 | Dois subgráficos para função exponencial e logaritmo. |
| 7 | Dispersão com tamanho de marcador variável. |
| 8 | Curva seno com faixa preenchida ao redor. |
| 9 | Função quadrática com grade tracejada. |
| 10 | Três funções com diferentes cores e estilos de linha. |
| 11 | Barras empilhadas com três grupos. |
| 12 | Limitação do eixo horizontal em uma função quadrática. |
| 13 | Gráfico de dispersão 3D. |
| 14 | Gráfico de barras horizontal. |
| 15 | Gráfico da função `y = 1/x`. |
| 16 | Inclusão de texto em uma coordenada do gráfico. |
| 17 | Salvamento de gráfico em PDF. |
| 18 | Barras positivas e negativas, com linha de referência em zero. |
| 19 | Duas séries no mesmo gráfico com legenda. |
| 20 | Personalização das marcações dos eixos. |

## 5.17 Abordagem orientada a objetos

Nos exercícios, foi usado principalmente o módulo `plt`. Para gráficos mais complexos, a abordagem orientada a objetos costuma oferecer mais controle:

```python
fig, ax = plt.subplots()

ax.plot(x, y)
ax.set_title("Função quadrática")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.grid(True)

plt.show()
```

Essa é uma recomendação adicional para evoluir os estudos.

---

# 6. Como as bibliotecas trabalham juntas

## 6.1 Fluxo conceitual

Um projeto de análise pode seguir esta sequência:

```text
Arquivo ou fonte de dados
          ↓
Pandas: leitura e limpeza
          ↓
NumPy: operações vetorizadas e estatísticas
          ↓
SciPy: modelagem, otimização ou cálculo científico
          ↓
Matplotlib: visualização e comunicação
```

## 6.2 Exemplo integrador proposto

> O exemplo abaixo é uma síntese nova baseada nos conceitos praticados; ele não corresponde a uma única célula do material original.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# 1. Dados tabulares com Pandas
df = pd.DataFrame({
    "mes": [1, 2, 3, 4, 5],
    "vendas": [100, 130, 155, 190, 225]
})

# 2. Conversão para arrays NumPy
x = df["mes"].to_numpy()
y = df["vendas"].to_numpy()

# 3. Modelo linear ajustado pelo SciPy
def reta(x, a, b):
    return a * x + b

parametros, _ = curve_fit(reta, x, y)
a, b = parametros

# 4. Previsões
x_modelo = np.linspace(x.min(), x.max(), 100)
y_modelo = reta(x_modelo, a, b)

# 5. Visualização
fig, ax = plt.subplots()
ax.scatter(x, y, label="Dados observados")
ax.plot(x_modelo, y_modelo, label="Curva ajustada")
ax.set_xlabel("Mês")
ax.set_ylabel("Vendas")
ax.set_title("Evolução das vendas")
ax.legend()
ax.grid(True)
plt.show()
```

Nesse exemplo:

- o **Pandas** organiza os dados;
- o **NumPy** fornece os arrays e o eixo contínuo;
- o **SciPy** estima os parâmetros da reta;
- o **Matplotlib** mostra os dados e o ajuste.

---

# 7. Correções e melhorias importantes

## 7.1 Determinante não é inversa

Código original equivalente:

```python
inversionMatriz = np.linalg.det(a)
```

O nome da variável sugere uma inversão, mas a função retorna o determinante.

Correção:

```python
determinante = np.linalg.det(a)
inversa = np.linalg.inv(a)
```

## 7.2 Rótulo do menor valor

No exercício de máximo e mínimo, o menor valor foi exibido com o texto `Maior número`.

Versão corrigida:

```python
print(f"Maior número: {max_value}")
print(f"Menor número: {min_value}")
```

## 7.3 Multiplicação elemento a elemento versus matricial

```python
A * B
```

multiplica posições correspondentes.

```python
A @ B
```

realiza multiplicação matricial.

A escolha depende do objetivo matemático.

## 7.4 Otimização de função constante

Uma função que sempre retorna 30 não possui um ponto mínimo único. O resultado `x = 0` apenas reflete o chute inicial fornecido.

Para demonstrar melhor a otimização:

```python
def f(x):
    return (x - 3)**2

resultado = minimize(f, [0])
```

Nesse caso, o mínimo ocorre próximo de `x = 3`.

## 7.5 Leitura inadequada do arquivo de vendas

O conteúdo apareceu em uma única coluna separada por vírgulas. Antes de iniciar uma análise, é importante inspecionar:

```python
print(df.head())
print(df.columns)
print(df.dtypes)
```

Se for CSV, use `read_csv()`. Se for Excel, confirme se as colunas estão realmente separadas na planilha.

## 7.6 Referência possivelmente antiga à variável `resultado`

No exercício de exportação, uma chamada a `resultado.to_csv()` apareceu antes do salvamento de `df`. Isso pode gerar erro ou salvar um objeto de outra célula.

Versão direta:

```python
df.to_csv("resultados.csv", index=False)
```

## 7.7 Categorias incoerentes

A operação de agrupamento estava tecnicamente correta, mas algumas classificações não representavam os produtos. Em projetos reais, erros de categorização alteram os totais e podem levar a conclusões incorretas.

## 7.8 Faixa fixa não é automaticamente um intervalo de confiança

O gráfico com `y ± 0.2` criou uma faixa visual. Para chamá-la de intervalo de confiança, seria necessário calcular seus limites a partir de uma amostra, de um modelo ou de uma estimativa estatística adequada.

## 7.9 Valores aleatórios mudam em cada execução

Isso explica por que matrizes, modas, correlações e determinantes podem mudar ao executar novamente as células.

Para resultados reproduzíveis:

```python
rng = np.random.default_rng(42)
```

## 7.10 Precisão numérica

Resultados como:

```text
-2.9999999999999996
```

representam, na prática, `-3`. Pequenas diferenças surgem porque números decimais são representados de forma aproximada no computador.

Uma apresentação arredondada pode ser feita com:

```python
print(round(resultado, 4))
```

ou:

```python
print(f"{resultado:.4f}")
```

---

# 8. Síntese das competências desenvolvidas

Após os exercícios, foram praticadas as seguintes competências:

## NumPy

- criar vetores e matrizes;
- trabalhar com formatos e dimensões;
- acessar linhas, colunas e elementos;
- realizar operações vetorizadas;
- aplicar filtros e substituições por condição;
- calcular estatísticas descritivas;
- trabalhar com diagonal, determinante, norma e produto escalar;
- normalizar dados;
- calcular correlação e ângulo entre vetores.

## SciPy

- calcular integrais simples e duplas;
- resolver equações diferenciais;
- encontrar mínimos, máximos e raízes;
- ajustar curvas;
- aplicar transformadas de Fourier;
- resolver sistemas lineares;
- calcular inversas, determinantes, autovalores e autovetores;
- interpolar valores;
- utilizar funções matemáticas especiais.

## Pandas

- criar DataFrames;
- importar Excel e CSV;
- inspecionar linhas iniciais e finais;
- converter tipos de dados;
- filtrar e ordenar registros;
- criar colunas calculadas;
- tratar valores ausentes;
- verificar duplicidades;
- agrupar e resumir dados;
- criar tabelas dinâmicas;
- combinar tabelas;
- exportar resultados.

## Matplotlib

- criar gráficos de linha, barras, dispersão, histograma e setores;
- representar várias séries;
- criar barras empilhadas e horizontais;
- personalizar títulos, eixos, grades, estilos e legendas;
- alterar limites e marcações dos eixos;
- criar gráficos 3D;
- adicionar texto e faixas visuais;
- salvar gráficos em arquivos.

---

# 9. Próximos passos recomendados

Os próximos estudos podem aprofundar o que já foi praticado:

1. **NumPy avançado**
   - broadcasting;
   - operações por eixo;
   - máscaras compostas;
   - vetorização e desempenho;
   - álgebra linear aplicada.

2. **Pandas para análise real**
   - datas com `to_datetime()`;
   - índices;
   - `loc` e `iloc`;
   - agregações múltiplas;
   - `merge`, `concat` e `join`;
   - tratamento de textos;
   - validação de qualidade dos dados.

3. **Estatística com SciPy**
   - distribuições de probabilidade;
   - testes de hipótese;
   - intervalos de confiança;
   - correlação e regressão;
   - análise de resíduos.

4. **Visualização**
   - abordagem `fig, ax`;
   - múltiplos eixos;
   - escalas logarítmicas;
   - anotações;
   - gráficos preparados para relatórios.

5. **Projeto completo**
   - importar uma base real;
   - limpar os dados;
   - gerar estatísticas descritivas;
   - responder perguntas de negócio;
   - criar gráficos;
   - exportar um relatório final.

---

## Conclusão

O conjunto de exercícios construiu uma base ampla de programação numérica, análise de dados, cálculo científico e visualização. A principal evolução foi sair de operações simples com arrays e avançar para tarefas mais completas, como solução de sistemas, equações diferenciais, ajuste de curvas, limpeza de tabelas, agrupamentos e criação de diferentes tipos de gráficos.

Mais do que memorizar funções, o aprendizado central é reconhecer qual ferramenta usar em cada etapa:

- **NumPy** para cálculos vetorizados;
- **SciPy** para métodos científicos;
- **Pandas** para dados tabulares;
- **Matplotlib** para visualização.
