# JPR2022

### Hands On Inteligência Artificial em Radiologia

Este é o passo a passo para o curso Hands On de Inteligência Artificial em Radiologia na JPR 2022.

### Principais objetivos:

* Conhecer os conceitos introdutórios de Inteligência Artificial
* Conhecer como avaliar a performance e capacidade de generalização de um algoritmo de Inteligência Artificial 

### Acknowledgements

Esta atividade é uma adaptação do "RSNA Spotlight Course 2021 AI Implementation: Building Expertise and Influence''. Session From Theory to Practice: Live Demonstration", realizada por Luciano M. Prevedello e Felipe C. Kitamura.

Os dados utilizados são provenientes do 2019 RSNA Intracranial Hemorrhage Dataset. O artigo que descreve a construção deste dataset pode ser encontrado neste link: [Flanders A.E., Prevedello L.M., Shih G. et al. Construction of a Machine Learning Dataset through Collaboration: The RSNA 2019 Brain CT Hemorrhage Challenge](https://pubs.rsna.org/doi/10.1148/ryai.2020190211)

### Professores

* Felipe C. Kitamura, MD, MSc, PhD
* Eduardo P. Reis, MD

### Monitores

* Victor V. M. Menezes, MD
* ABC

### Antes de começarmos, vamos lembrar alguns conceitos:

#### O que é Inteligência Artificial?
Inteligência artificial (IA) se referem de forma genérica a programas de computador que simulam funções cognitivas humanas. A principal técnica de IA para o processamento de imagens é a Rede Neural Convolucional.

#### O que é uma Rede Neural Convolucional (CNN)?
As CNNs são modelos inspirados na biologia do córtex visual dos mamíferos. D. H. Hubel e T. N. Wiesel propuseram uma explicação para a maneira como os mamíferos percebem visualmente o mundo ao seu redor usando uma arquitetura em camadas de neurônios no cérebro, e isso, por sua vez, inspirou os engenheiros a tentar desenvolver mecanismos semelhantes de reconhecimento de padrões na visão computacional.

![Visual Cortex](https://github.com/edreisMD/handsonfigs/blob/master/visualcortex2.jpg)

Fonte: https://colocar


#### Construindo a arquitetura da Rede Neural Convolucional
#### O que é uma convolução?

Uma convolução é uma operação matemática que consiste em multiplicar uma matriz (a nossa imagem) por um filtro (matriz de pesos)

#### Como o computador enxerga uma imagem?

Através de uma matriz de números estrategicamente orientados.

Considere cada imagem como uma matriz em que o valor de cada pixel corresponde a um número que determina o tom de cinza da imagem

![8Pixels](https://github.com/edreisMD/handsonfigs/blob/master/8_digits.gif)

Fonte: https://colocar

Portanto, para enxergar os contornos de uma imagem nosso algoritmo vai tentar criar filtros que representem estes contornos em números, como no exemplo abaixo.

![4Conv](https://github.com/edreisMD/handsonfigs/blob/master/Screen-Shot-2017-07-26-at-6.13.41-PM.png)

Fonte: https://colocar

Veja como esses filtros numéricos  vão percorrer toda a imagem para enxergar os contornos:

![ConvRun](https://github.com/edreisMD/handsonfigs/blob/master/ConvRun.gif)

Fonte: https://colocar

E repetiremos essa operação várias vezes para nossa rede enxergar características cada vez mais complexas, gerando filtros de contornos.

#### Depois de definida a arquitetura vamos treinar nossa rede neural.

Treinar uma rede neural consiste basicamente em tentar achar a menor diferença entre o que o algoritmo prediz e a resposta correta (ou ground truth), esta diferença é chamada de perda (loss), quanto menor a perda (loss), mais o seu algoritmo está acertando, consequentemente maior será a acurácia (acc).

![NN](https://i1.wp.com/francescolelli.info/wp-content/uploads/2019/05/NeuralNetworks-input-layer-hidden-layer-output-layer.png?resize=1024%2C670&ssl=1)

Fonte: https://francescolelli.info/tutorial/neural-networks-a-collection-of-youtube-videos-for-learning-the-basics/

Veja na animação abaixo que a rede neural está buscando o ponto de menor perda (loss) (vermelho), mas para chegar lá ela deve tentar vários caminhos diferentes de forma aleatória, por isso precisamos repetir o processo várias vezes, até chegar no ponto mais baixo. Esse processo se chama Gradient Descent.

![Gradient Descent](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/graddescent01.gif)

Reference: https://towardsdatascience.com/a-visual-explanation-of-gradient-descent-methods-momentum-adagrad-rmsprop-adam-f898b102325c

Os pesos iniciais do modelo determinam o ponto inicial do "espaço" da loss. Essa é uma das razões porque o processo de treinamento pode dar resultados diferentes para cada vez que você treinar. Isso significa também que você pode ter diferentes resultados do que os mostrados abaixo. Não se preocupe.

Mesmo que haja essa variabilidade no treinamento, uma vez terminado o treinamento e congelados os pesos você sempre obterá o mesmo resultado ao avaliar uma mesma imagem, ou um conjunto de teste.

### Passo a passo:

#### Step 1: Download the [file for Experiment 1 here](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/experiments/experiment1.tm?raw=true) and save it somewhere you can find it later.

#### Step 2: Right click on the [teachable machine link here](https://teachablemachine.withgoogle.com/train/image) and choose "Open in a new tab" (or hold CTRL key + left mouse click)

You should see this website:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/image04.png)

#### Step 3: Click on the left upper corner to open the menu and then click on "Open project from file" as below:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/image05.png)

#### Step 4: Upload the file from Experiment 1 (Step 1) and wait for it to load.

You should see multiple head CT images loaded onto the platform organized by presence or absence of hemorrhage:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/image06.png)

#### Step 5: Click on train and wait for it to finish. It may take a while for the training to start.

After training, experiment 1 should look like this:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/experiment1.png)

Notice that the accuracy is not as good as one may expect from a machine learning model. This is due to the limited number of cases in this experiment (30 normal + 30 hemorrhage)


#### Step 6: Repeat steps 3 to 5, but now load the [file for Experiment 2 here](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/experiments/experiment2.tm?raw=true)

After training, experiment 2 should look like this:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/experiment2.png)

Notice that the accuracy seems to have improved significantly. However, a closer look at the confusion matrix shows that most of the positive cases have been misclassified as negative. This is due to the heavy class imbalance thas was simulated in this experiment (1000 normal + 30 hemorrhage).

#### Step 7: Repeat steps 3 to 5, but now load the [file for Experiment 3 here](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/experiments/experiment3.tm?raw=true)

After training, experiment 3 should look like this:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/experiment3b.png)

Notice that the accuracy is lower than in the last experiment. However, a closer look at the confusion matrix shows that it is indeed correctly classifying most of the positive cases, although still nor perfect. In this experiment our dataset was balanced (1000 normal + 1000 hemorrhage).

#### Step 8: Repeat steps 3 to 5, but now load the [file for Experiment 4 here](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/experiments/experiment4.tm?raw=true)

After training, experiment 4 should look like this:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/experiment6.png)

In this experiment we are training a multiclass model to predict only 1 of 3 classes (normal, subdural, intraparenchymal). Because of the limited number of images in each class (80) to keep it balanced, the accuracy is not impressive. Now let's compare it to experiment 5 (next step).

#### Step 9: Repeat steps 3 to 5, but now load the [file for Experiment 5 here](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/experiments/experiment5.tm?raw=true)

After training, experiment 5 should look like this:

![Screenshot](https://github.com/kitamura-felipe/RSNASpotlight2021/blob/main/images/experiment7.png)

In this experiment we are also training a multiclass model with 3 classes (normal, subdural, intraparenchymal). Because of the preprocessing step done to color-code the bleedings, the model is able to achieve a significantly higher accuracy. This color-coding was done by assigning the red color to voxels that where within a certaing range of Hounsfield Units. Although this simple thresholding rule is not perfectly accurate to identify bleedings, it helps the model achieve a better result.
