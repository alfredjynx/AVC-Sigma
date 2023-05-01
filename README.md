# AVC-Sigma

<!-- Aqui é Reservado para Análise de Dados -->

## *Aviso Importante*
* Todas as descrições de código e modelos matemáticos estão no arquivo `demo.ipynb`. Os testes foram salvos em arquivos *.csv* para não ser necessário a execução dos modelos (principalmente os de Clasificação Linear).

## Resumo de Testes

Inicialmente, fizemos dois testes de *Classificação Linear* com o DataFrame inteiro, tendo resultados que não nos diziam muito, não traziam informações claras. Isso é consequência de termos uma hipótese nula muito alta (95%). Tivemos dois testes, mudando apenas as colunas do DataFrame que eram contempladas pela matriz $X$ (features) do modelo de classificação linear. Os dois modelos nos mostraram que era preciso tratar o dataframe antes de iniciar o processo de criação de modelo.

Por isso, todos os modelos (*Classificação Linear e Árvore de Decisão*) a partir desse ponto tiveram um DataFrame tratado. Esse novo DataFrame inicial tem uma hipótese nula de 50%. Em termos simples, metade dos pacientes contemplados tiveram um AVC e a outra metade não teve. 

Além disso, para evitar repetições nesse arquivo *README.md*, todos os testes tiveram o mesmo processo de criação da matriz $Y$ (medições). Ela apenas possui os valores referentes ao paciente ter tido ou não um AVC, ou seja, apenas contempla essa coluna do *avc-data.csv*.

### Classificação Linear

### Testes
Abaixo estão os resultado dos testes com o DataFrame ajustado para a hipótese nula descrita acima. As diferenças entre um classificador e o outro estão inteiramente na matriz de features que cada um utiliza para realizar o *train-test-split* (com cada um contemplando certas colunas do *avc-data.csv* original.)

Foram realizados 100 iterações de cada modelo, com o resultado final sendo a acurácia média de cada um. Isso foi feito para minimizar a variância entre versões do exato mesmo modelo. 

#### Teste 1
* Foram representadas todas as colunas possíveis de serem transformadas em valores booleanos na matriz $X$ (features). Isso significa que há informações relacionadas a hipertensão, doenças cardiovasculares, gênero, status civil, trabalho, residência e utilização de tabaco na matriz de features. O resultado final foi uma acurácia média de 62.54%. 

#### Teste 2
* Foram representadas apenas as colunas relacionadas a condições médicas (hipertensão, condição cardiovascular) e informações sobre o paciente ser ou não fumante na matriz $X$ (features). O resultado final foi uma acurácia média de 66.51%.

#### Teste 3
* Foram representadas apenas as colunas relacionadas a condições médicas (hipertensão, condição cardiovascular), informações sobre o paciente ser ou não fumante e às condições de trabalho dele na matriz $X$ (features). O resultado final foi uma acurácia média de 62.95%

#### Teste 4
* Foram representadas apenas as colunas relacionadas a condições médicas (hipertensão, condição cardiovascular), informações sobre o paciente ser ou não fumante, condições de trabalho e gênero na matriz $X$ (features). O resultado final foi uma acurácia média de 66.28%.


### Árvore de Decisão

Acredito ser importante ressaltar que os modelos por *Árvore de Decisão* são muito mais rápidos dos que os *Classificadores Lineares*. Isso é pertinente pois as média de acurácia desses modelos forma feitas com 1000 iterações de cada, ao invés de 100 (como nos *Classificadores Lineares*).

### Testes
Aqui, também foram ajustados os DataFrames originais, mantendo uma hipótese nula de 50%. Assim como os testes anteriores, as diferenças entre um classificador e o outro estão inteiramente na matriz de features que cada um utiliza para realizar o *train-test-split* (com cada um contemplando certas colunas do *avc-data.csv* original.)

O resultado final dos testes é a acurácia média de cada modelo. Isso foi feito para minimizar a variância entre versões do exato mesmo modelo. 

#### Teste 1
* Foram representadas todas as colunas possíveis de serem transformadas em valores booleanos na matriz $X$ (features). Isso significa que há informações relacionadas a hipertensão, doenças cardiovasculares, gênero, status civil, trabalho, residência e utilização de tabaco na matriz de features. O resultado final foi uma acurácia média de 58.15%. 

#### Teste 2
* Foram representadas todas as colunas possíveis do DataFrame original, incluindo as que continuam com valores numéricos e não booleanos (glicose, bmi e idade). O resultado final foi uma acurácia média de 67.24%. 

#### Teste 3
* Foram representadas as colunas relacionadas a condições médicas, fisiológicas e relacionadas a fumar. O resultado foi uma acurácia média de 66.42%.

#### Teste 4
* Foram representadas apenas as colunas relacionadas a glicose, bmi, idade, condições médicas (hipertensão, condição cardiovascular), informações sobre o paciente ser ou não fumante, condições de trabalho e gênero na matriz $X$ (features). O resultado foi uma acurácia média de 70.60%.

## Resultados

O modelo com melhor desempenho foi o *Teste 4* da *Árvore de Decisões*. O modelo contempla as seguintes colunas em sua matriz de features ($X$): 

* avg_glucose_level
* bmi
* age
* hypertension
* heart_disease
* gender_Female
* gender_Male 
* gender_Other
* work_type_Govt_job
* work_type_Never_worked
* work_type_Private
* work_type_Self-employed
* work_type_children
* smoking_status_Unknown
* smoking_status_formerly smoked
* smoking_status_never smoked
* smoking_status_smokes

Abaixo, estão algumas citações dos resumos de artigos científicos relacionados a fatores de risco de AVCs (Acidente Vascular Cerebral). 

"Em relação aos fatores de risco não modificáveis foi evidenciado que as chances de AVC duplicam após os 55 anos de idade, o sexo masculino é o mais acometido pelo AVC em idades inferiores aos 85 anos, os negros têm cerca de duas vezes mais chances de AVC do que os brancos e os hispânicos tem 1,5 vezes mais chances de AVC do que não-hispânicos. Já em relação aos fatores de risco modificáveis, a hipertensão arterial sistêmica foi apontada como o mais comum deles, além da fibrilação atrial, diabetes mellitus, dislipidemia, obesidade e o tabagismo que pode inclusive dobrar o risco de AVCI." - Marianelli (2020)

"Como fatores de risco para o AVC em jovens foram encontrados a obesidade, hipertensão arterial, diabetes mellitus, sedentarismo, pré disposições genéticas, doença ateromatosa, fibrilação atrial, uso de anticoncepcional oral combinado e mixoma auricular" - Pompermaier, Charlene (2020)

"Observou-se que os principais fatores não modificáveis são: idade, sexo, raça, localização geográfica e hereditariedade. Já os principais fatores modificáveis são: hipertensão, fibrilação atrial, diabetes melito, dislipidemia, obesidade e o tabagismo." - de Sousa Rodrigues, Mateus (2017)

Como fatores mencionados, estão: idade, tabagismo, sexo , hipertensão, obesidade, raça, hereditariedade, localização geográfica, uso de anticoncepcionais, diabetes, sedentarismo, doença ateromatosa, frequência cardíaca irregular (fibrilação atrial) e dislipidemia. 

No nosso modelo, temos representados: idade, tabagismo, sexo (gênero), hipertensão e obesidade (bmi). Além desses, contemplamos fatores como trabalho e histórico de doenças cardíacas (pode ou não indicar fibrilação atrial). 

Portanto, é razoável de se concluir que nosso modelo está condizente com dados reais e observados em relatórios médicos sobre causas de AVCs. 

## Bibliografia
* Pompermaier, Charlene, et al. "Fatores de risco para o acidente vascular cerebral (AVC)." *Anuário Pesquisa e Extensão Unoesc Xanxerê 5* (2020): e24365-e24365.
* Marianelli, Mariana, Camila Marianelli, and Tobias Patrício de Lacerda Neto. "Principais fatores de risco do avc isquêmico: Uma abordagem descritiva." *Brazilian Journal of Health Review* 3.6 (2020): 19679-19690.
* de Sousa Rodrigues, Mateus, Leonardo Fernandes, and Ivan Martins Galvão. "Fatores de risco modificáveis e não modificáveis do AVC isquêmico: uma abordagem descritiva." *Revista de medicina* 96.3 (2017): 187-192.
