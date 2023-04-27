# AVC-Sigma

## Aproximação Linear

O processo de aproximação linear é uma maneira de criar um modelo que consegue prever próximos resultados a partir de informações atuais.

A operação é, como o nome já da a entender, uma maneira de tentar criar uma linha que contemple os pontos do DataFrame ou matriz original. 

Para isso, realizamos um processo de "aprendizado", onde, ao longo de um número de épocas (escolhido pelo usuário), vamos corrigindo a matriz de pesos ($W^T$) e o bias ($b$) que modificam a matriz de features ($X$) e nos dão a matriz de estimativa de valores ($Y^{est}$).

Inicialmente, criamos a matriz de pesos $W^T$ e o bias $b$ com valores que não são importantes, ou seja, podem ser aleatórios ou 1, já que eles serão corrigidos ao longo do processo. 

Depois, separamos nossas matrizes originais (matriz $X$ de features e $Y$ de resultados) em $X_{test}$, $Y_{test}$, $X_{train}$ e $Y_{train}$. Treinamos nosso modelo com as matrizes $train$ e testamos a sua efetividade com as matrizes $test$.

O próximo passo é criar nossa função de erro. Nela, tentamos estimar uma matriz $Y$, chegando em $Y^{est}$. Retornamos a média da diferença quadrada entre as duas matrizes (erro). Assim, ficamos com a seguinte conta. 

$$

Y^{est} = W^TX + b

$$

$$
Erro = Média((Y-Y^{est})^2)
$$

Essa função é passada para o gradiente (função *grad*) da biblioteca do autograd. Ela consegue nos retornar automaticamente o vetor gradiente da função erro, vetor esse com a derivada do erro em relação a cada parâmetro da função. O seu retorno é uma tupla, com novos valores de $W_{err}^T$ e $b_{err}$.

Ao longo das épocas, multiplicamos $W_{err}^T$ e $b_{err}$ por $\alpha$, nosso learning rate. Pegamos esse número (erro da função gradiente) e subtraímos dos valores originais de $W^T$ e $b$, os deixando cada vez mais próximos dos números ideais para a função de reta. Temos: 

$$
W^T = W^T - \alpha W_{err}^T
$$

$$
b = b - \alpha b_{err}
$$

No final, temos um $W_{err}^T$ e um $b_{err}$ que se assemelham a equação mais próxima da reta dos pontos originais, criando nosso modelo preditivo.

Checamos a efetividade do modelo por meio de uma comparação. Primeiro, calculamos um $Y^{est}$ para $X^{test}$. Agora, utilizando a função accuracy que nos foi dada pelo professor Tiago Tavares, calculamos a acurácia do modelo. 

O processo ainda não terminou, pois precisamos verificar o modelo comparado a hipótese nula. 

# Hipótese Nula

A hipótese nula é a acurácia de um modelo que sempre categoriza algo como o resultado mais frequente. Nesse caso, temo a quantidade de vezes que o resultado mais frequente ocorreu ($r$) dividida pelo número total de resultados ($N$).

$$
H_{0} = \frac{r}{N}
$$

É important que seu modelo seja funcional e não apenas parecido com a hipótese nula. Um exemplo que ilustra essa necessidade é um que temos 70% dos casos da classe A e 30% de outras classes. Se nosso modelo sempre chutar que um elemento é da classe A ele terá 70% de acurácia, mas isso não significa que ele está correto.