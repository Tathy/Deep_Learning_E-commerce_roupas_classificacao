# :dress: Classificação de imagens de roupas

[Link do Google Colab](https://colab.research.google.com/drive/1_4rKJc8nuVvR_xQie4uFQg8OyJX05xPJ?usp=sharing)

### Sobre o projeto

* Estudo introdutório sobre Deep Learning, TensorFlow e Keras.

* E-commerce fictício de roupas, as roupas à venda devem ser classificadas em categorias para facilitar as buscas dos clientes no site.

* **Dataset:** [Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist) que contém pequenas imagens (28x28) de roupas em escala de cinza, associadas a 10 classes.

# Estruturação do modelo

* Serão 3 camdas, uma de entrada, uma escondida e uma de saída.

* Na primeira camada, Camada 0, a imagem será "achatada" para um array de pixels de uma única dimensão.

* Na Camda 1, é feita a comunicação com a camada de entrada. Neste caso, será uma camada densa, totalmente conectada com a anterior.
  * Foram difinidos 256 neurônios com função de ativação ReLu.

* Na Camada 2, de saída, foi definida quantidade de classes do dataset, totalmente conectada com a anterior.

# Redução de perda / Aumento de acurácia

## Normalização do dataset

* As imagens estavam em escala de cinza e os pixels assumiam valores em um intervalo de [0, 255].

* Foi feita uma normalização, dividindo todos os valores do dataset de treino por 255, o que resultou em uma normalização para o intervalo [0, 1].

* Esta normalização reduziu a perda do modelo significativamente - valor que pode se alterar dependendo da execução. 

* Reduzir a amplitude numérica que a rede precisou processar ajudou a evitar a perda de informações sem influenciar na identificação visual das imagens. 

<div align="center">
  <img src="https://github.com/Tathy/Deep_Learning_E-commerce_roupas_classificacao/blob/main/imgs/imgs_normalizacao.png?raw=true"/>
</div>

* Apesar de ter funcionado neste caso específico, nem sempre o processo de normalização será vantajoso. 

## Reestruturação das camadas escondidas

* Neste momento do estudo, o modelo possuía 3 camadas. Foram acrescentadas camadas escondidas para observação das alterações nos valores de perda de informação.

* Da segunda camada para a camada de saída haviam conexões de 256 para 10. 

* A ideia do próximo passo era afunilar estas conexões criando camadas internediária e verificar se a perda é reduzida.
	* Acréscimo da segunda camada escondida, com 128 neurônios e função de ativação ReLu. Houve pequena diminuição de perda.
	* Acréscimo da terceira camada escondida, com 64 neurônios e função de ativação ReLu. Houve aumento de perda, valor maior do que o observado com apenas uma camada escondida.

* Aumentar a quantidade de camadas escondidas, tornando a rede mais profunda, nem sempre trará benefícios para o modelo, além de poder aumentar significativamente o tempo de execução em modelos de aplicação real.

* Tanto a quantidade de neurônios quanto as funções de ativação precisarão de uma exploração, um processo mais subjetivo do que exato.

* Dropout: inativa algumas ligações entre duas camadas, como se os neurônios estivessem inativos

## Aumento no número de épocas

* Épocas são os contatos que o modelo tem com o dataset no processo de aprendizagem, em que os ajustes de pesos das conexões são feitas entre os neurônios.

* O tempo de execução tem um aumento linear, diretamente proporcional à execução com somento uma época.

* No modelo do estudo, a perda foi diminuido gradativamente, mas mesmo sendo um dataset de estudo, o aumento de tempo necessário já foi considerável.

# Validação e Testes

#### Acurácia
* A acurácia irá medir o quanto o modelo está acertando.
* O ideal é que, à medida que o modelo é reestruturado, a perda diminua e a acurácia aumente.

#### Predição e Teste
* A Softmax, usada na camada de saída, retorna a probabilidade de uma entrada pertencer a cada categoria.
* No primeiro item do dataset o retorno foi [0., 0., 0., 0., 0., 0., 0., 0., 0., 0.99999994]. Ou seja, foi calculada uma probabilidade de quase 100% da imagem representar um item da última classe.
* O teste é feito anlisando-se a acurácia da predição sobre o conjunto de teste.
	
#### Conjunto de Validação

* A Validação foi feita com um modelo de 10 épocas, com 20% do conjunto de treino.
* Os gráficos de acurácia e perda das etapas de treino e teste sugerem que o modelo sofreu Overfitting, ou seja, está tão especializado nos padrões das imagens de treinamento que não consegue interpretar novas imagens, do conjunto de validação.

<div align="center">
  <img src="https://github.com/Tathy/Deep_Learning_E-commerce_roupas_classificacao/blob/main/imgs/overfitting.png?raw=true"/>
</div>

* Para evitar o oferfitting, pode-se manter a quantidade de épocas no intervalo em que os resultados estão mais estáveis. Onde a tendência da perda e da acurácia estão favoráveis no treino e os resultados na validação ainda estão próximos.

## Referências

* Estudo desenvolvido acompanhando o curso [Deep Learning parte 1: Keras](https://cursos.alura.com.br/course/deep-learning-introducao-com-keras), da Alura.

:seedling:
