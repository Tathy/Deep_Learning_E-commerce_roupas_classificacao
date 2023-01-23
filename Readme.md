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

## Referências

* Estudo desenvolvido acompanhando o curso [Deep Learning parte 1: Keras](https://cursos.alura.com.br/course/deep-learning-introducao-com-keras), da Alura.

:seedling:
