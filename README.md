# Hands On Inteligência Artificial em Radiologia - JPR 2022

Este é o passo a passo para o curso Hands On de Inteligência Artificial em Radiologia na JPR 2022.

### Principais objetivos:

* Conhecer os conceitos introdutórios de Inteligência Artificial
* Conhecer como avaliar a performance e capacidade de generalização de um algoritmo de Inteligência Artificial 

### Acknowledgements

This lecture was inspired in Luciano, Errol e Tara presentation at RSNA 2021.

Esta atividade é baseada na "RSNA Spotlight Course 2021 AI Implementation: Building Expertise and Influence''. Session From Theory to Practice: Live Demonstration", realizada por Luciano M. Prevedello e Felipe C. Kitamura.

Os dados utilizados são provenientes do 2019 RSNA Intracranial Hemorrhage Dataset. O artigo que descreve a construção deste dataset pode ser encontrado neste link: [Flanders A.E., Prevedello L.M., Shih G. et al. Construction of a Machine Learning Dataset through Collaboration: The RSNA 2019 Brain CT Hemorrhage Challenge](https://pubs.rsna.org/doi/10.1148/ryai.2020190211)

### Professores

* Felipe C. Kitamura, MD, MSc, PhD
* Eduardo P. Reis, MD

### Monitores

* Victor V. M. Menezes, MD
* Augusto S. Serpa, MD

### Antes de começarmos, vamos lembrar alguns conceitos:

#### O que é Inteligência Artificial?
Inteligência artificial (IA) se referem de forma genérica a programas de computador que simulam funções cognitivas humanas. A principal técnica de IA para o processamento de imagens é a Rede Neural Convolucional.

#### O que é uma Rede Neural Convolucional (CNN)?
As CNNs são modelos inspirados na biologia do córtex visual dos mamíferos. D. H. Hubel e T. N. Wiesel propuseram uma explicação para a maneira como os mamíferos percebem visualmente o mundo ao seu redor usando uma arquitetura em camadas de neurônios no cérebro, e isso, por sua vez, inspirou os engenheiros a tentar desenvolver mecanismos semelhantes de reconhecimento de padrões na visão computacional.

<img src="https://github.com/edreisMD/handsonfigs/blob/master/visualcortex2.jpg" width="500">

Fonte: https://neuwritesd.org/2015/10/22/deep-neural-networks-help-us-read-your-mind/


#### Construindo a arquitetura da Rede Neural Convolucional
#### O que é uma convolução?

Uma convolução é uma operação matemática que consiste em multiplicar uma matriz (a nossa imagem) por um filtro (matriz de pesos)

#### Como o computador enxerga uma imagem?

Através de uma matriz de números estrategicamente orientados.

Considere cada imagem como uma matriz em que o valor de cada pixel corresponde a um número que determina o tom de cinza da imagem

<img src="https://github.com/edreisMD/handsonfigs/blob/master/8_digits.gif" width="300">

Fonte: https://medium.com/@ageitgey/machine-learning-is-fun-part-3-deep-learning-and-convolutional-neural-networks-f40359318721

Portanto, para enxergar os contornos de uma imagem nosso algoritmo vai tentar criar filtros que representem estes contornos em números, como no exemplo abaixo.

<img src="https://github.com/edreisMD/handsonfigs/blob/master/Screen-Shot-2017-07-26-at-6.13.41-PM.png" width="400">

Fonte: https://www.jeremyjordan.me/convolutional-neural-networks/

Veja como esses filtros numéricos  vão percorrer toda a imagem para enxergar os contornos:

<img src="https://github.com/edreisMD/handsonfigs/blob/master/ConvRun.gif" width="400">

Fonte: https://medium.com/mlearning-ai/feature-extraction-using-convolution-1576d9abe07f

E repetiremos essa operação várias vezes para nossa rede enxergar características cada vez mais complexas, gerando filtros de contornos.

#### Depois de definida a arquitetura vamos treinar nossa rede neural.

Treinar uma rede neural consiste basicamente em tentar achar a menor diferença entre o que o algoritmo prediz e a resposta correta (ou ground truth), esta diferença é chamada de perda (loss), quanto menor a perda (loss), mais o seu algoritmo está acertando, consequentemente maior será a acurácia (acc).

<img src="https://i1.wp.com/francescolelli.info/wp-content/uploads/2019/05/NeuralNetworks-input-layer-hidden-layer-output-layer.png?resize=1024%2C670&ssl=1" width="500">

Fonte: https://francescolelli.info/tutorial/neural-networks-a-collection-of-youtube-videos-for-learning-the-basics/

Veja na animação abaixo que a rede neural está buscando o ponto de menor perda (loss) (vermelho), mas para chegar lá ela deve tentar vários caminhos diferentes de forma aleatória, por isso precisamos repetir o processo várias vezes, até chegar no ponto mais baixo. Esse processo se chama Gradient Descent.

<img src="https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/graddescent01.gif" width="500">

Fonte: https://towardsdatascience.com/a-visual-explanation-of-gradient-descent-methods-momentum-adagrad-rmsprop-adam-f898b102325c

Os pesos iniciais do modelo determinam o ponto inicial do "espaço" da loss. Essa é uma das razões porque o processo de treinamento pode dar resultados diferentes para cada vez que você treinar. Isso significa também que você pode ter diferentes resultados do que os mostrados abaixo. Não se preocupe.

Mesmo que haja essa variabilidade no treinamento, uma vez terminado o treinamento e congelados os pesos você sempre obterá o mesmo resultado ao avaliar uma mesma imagem, ou um conjunto de teste.

### Passo a passo:

#### Passo 1: Clique com o botão direito e acesse esse [link](https://teachablemachine.withgoogle.com/train/image) em uma nova aba para o Teachable Machine

Você deve ver este site:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo1.png" width="700">

#### Passo 2: Baixe o arquivo [Experimento 1](https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Experimentos/experiment1.tm) em um local que será fácil para encontrar depois

#### Passo 3: Clique em "Teachable Machine" no canto superior esquerdo e depois em "Open project from file", como abaixo:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo3.png" width="700">

#### Passo 4: Faça o upload do arquivo 1 e aguarde ele ser carregado.

Você deve ver múltiplas imagens de TC de crânio carregadas na plataforma e divididas pela presença ou ausência de hemorragia:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo4.png" width="700">

#### Passo 5: Clique em train model e aguarde finalizar, sem sair da aba. Pode levar um tempinho…

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo5.png" width="700">

#### Passo 6: Na mini-aba do treinamento, selecione "Advanced" e depois "Under the hood"

Com isso, deve surgir uma nova mini-aba lateral e a sua tela deve estar parecida com esta:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo6.png" width="700">

#### Passo 7: Na nova mini-aba lateral, clique em "Calculate Confusion Matrix"

A sua tela deve estar parecida com esta:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo7.png" width="700">

Observe que a acurácia não é tão boa quanto se pode esperar. Isto se deve ao fato do baixo número de casos no experimento (30 normais + 30 com hemorragia)

#### Passo 8: Vamos ver como a rede se sai em uma imagem 

Pegue uma imagem de "hemorragia intracraniana" ou "TC de cranio normal" no google e salve no seu computador. Feche a mini-aba "Under the hood" e, em seguida na aba "Preview", escolha "Input -> File" e arraste a imagem que você salvou no seu computador para esta aba.

A sua tela deve estar parecida com esta:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo8.png" width="700">

Veja como a rede se sai ao longo dos experimentos. Ela terá diferentes performances, devendo se sair melhor no experimento 3 em que o nosso *dataset* tem um número maior de imagens. Mas fique atento pois em cada experimento aboradaremos um conceito diferente!

#### Passo 9: Repita os passos 3 a 8 utilizando agora o arquivo [Experimento 2](https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Experimentos/experiment2.tm)

O seu resultado deve ser parecido com este:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo9.png" width="700">

Observe que a acurácia parece ter aumentado significativamente. No entanto, olhando de perto é possível notar que a matriz de confusão mostra que a maioria dos casos “positivos” foram classificados erroneamente como “negativos”. Isso se deve ao alto desbalanceamento nesse experimento (1000 normais + 30 com hemorragia).


#### Lidando com o desbalanceamento

Modelos que possuem um desbalanceamento das classes (ex: mais tomografias de crânio normais que com hemorragia) tendem a ter decisões sempre a favor da classe majoritária.

Oversampling e Undersampling são técnicas para criar ou remover dados artificialmente para balancear as classes.
* Oversampling: Aumentar a amostra da classe minoritária.
* Undersampling: Reduzir a amostra da classe majoritária.

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/over_under_sampling.png" width="500">

Fonte: https://towardsdatascience.com/a-visual-explanation-of-gradient-descent-methods-momentum-adagrad-rmsprop-adam-f898b102325c

#### Passo 10: Repita os passos 3 a 8 utilizando agora o arquivo [Experimento 3](https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Experimentos/experiment3.tm)

O seu resultado deve ser parecido com este:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo10.png" width="700">

Observe que a acurácia é menor do que no último experimento. No entanto, a matriz de confusão demonstra que a maioria dos casos “positivos” passaram a ser classificados corretamente, apesar de não estar perfeito. Neste experimento nosso dataset foi balanceado (1000 normais + 1000 com hemorragia)

#### Passo 11: Repita os passos 3 a 8 utilizando agora o arquivo [Experimento 4](https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Experimentos/experiment4.tm)

O seu resultado deve ser parecido com este:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo11.png" width="700">

Neste experimento nós estamos treinando um modelo multiclasse para classificar em apenas 1 de 3 classes possíveis (normal, subdural, intraparenquimatoso). Devido ao número limitado de imagens de cada classe (80) para manter o balanceamento, a acurácia não foi satisfatória

#### Passo 12: Repita os passos 3 a 8 utilizando agora o arquivo [Experimento 5](https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Experimentos/experiment5.tm)

O seu resultado deve ser parecido com este:

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/Passo12.png" width="700">

Neste experimento nós também estamos treinando um modelo multiclasse com 3 classes (normal, subdural e intraparenquimatoso). Devido ao pré-processamento realizado para color-code os sangramentos, o modelo foi capaz de obter uma acurácia significativamente maior. Este color-code foi realizado determinando a cor vermelha aos voxels que estavam em uma determinada janela de Unidades Hounsfield. Apesar de esse simples ajuste não tornar o modelo perfeito, ele o ajuda a obter um resultado significativamente melhor.

<img src="https://github.com/edreisMD/HandsOnAIJPR2022/blob/main/Imagens/hemorragia_cor.png" width="400">

Legenda: Normal / Intraparenquimatoso / Subdural


### Parabéns você treinou a sua primeira rede neural!

<img src="https://media.giphy.com/media/RWSuqBwzgQU2A/giphy.gif">

Fonte: https://giphy.com
