Proc de Imagens

Carregando…
Cópia de PDI_aula2_Cores.ipynb
Cópia de PDI_aula2_Cores.ipynb_
Aula 2 - Cores
Profa. Ana Paula

Processamento de Imagens
1. Apresentação
O interesse nos métodos de processamento digital de imagens provém de duas áreas principais de aplicação:

a) melhora das informações visuais para a interpretação humana; e

b) processamento de dados de imagens para armazenamento, transmissão e representação, considerando a percepção automática por máquinas.

2. O que é Processamento de Imagens?
Uma imagem pode ser definida como uma função bidimensional, f (x, y), em que x e y são coordenadas espaciais (plano), e a amplitude de f em qualquer par de coordenadas (x, y) é chamada de intensidade ou nível de cinza da imagem nesse ponto.

[ ]
# Importação das bibliotecas
import cv2
from matplotlib import pyplot as plt
#import matplotlib.pyplot as plt
import numpy as np

!wget "https://hypescience.com/wp-content/uploads/2009/08/arco-iris-lunar-7.jpg" -O dt.jpg
imgNome = './dt.jpg'



--2021-03-19 12:07:27--  https://hypescience.com/wp-content/uploads/2009/08/arco-iris-lunar-7.jpg
Resolving hypescience.com (hypescience.com)... 172.67.131.175, 104.21.10.186, 2606:4700:3032::6815:aba, ...
Connecting to hypescience.com (hypescience.com)|172.67.131.175|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26544 (26K) [image/jpeg]
Saving to: ‘dt.jpg’

dt.jpg              100%[===================>]  25.92K  --.-KB/s    in 0.002s  

2021-03-19 12:07:27 (15.3 MB/s) - ‘dt.jpg’ saved [26544/26544]

[ ]
  img = cv2.imread(imgNome)
  plt.imshow(img)
  print("\nImagem BGR")
  plt.show()


[ ]
dimensions = img.shape
dimensions

(683, 1024, 3)
Neste caso, x=683 e y=1024

[ ]
 #convertendo para RGB
imgrgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(imgrgb)
print("\nImagem RGB")
plt.show()


[ ]
imgNC = cv2.cvtColor(imgrgb, cv2.COLOR_RGB2GRAY)
[ ]
plt.imshow(imgNC,'gray')


[ ]
dimensions1 = imgNC.shape
dimensions1

(333, 500)
2.1 As origens do Processamento Digital de Imagens
Uma das primeiras aplicações das imagens digitais ocorreu na indústria dos jornais, quando as imagens eram enviadas por cabo submarino entre Londres e Nova York.

A implementação do sistema de transmissão de imagens por cabo submarino (cabo Bartlane) no início da década de 1920 reduziu de mais de uma semana para menos de três horas o tempo necessário para transportar uma fotografia pelo oceano Atlântico.

Um equipamento de impressão especializado codificava as imagens para a transmissão a cabo e depois as reconstruía no recebimento

2.2 Exemplos de áreas que utilizam o processamento digital de imagens
Hoje em dia, não existe praticamente mais nenhuma área de empreendimento técnico que não seja impactada de uma forma ou de outra pelo processamento digital de imagens.

As áreas de aplicação do processamento digital de imagens são tão variadas que requerem alguma forma de organização para que todo seu escopo seja incluído. Uma das formas mais fáceis de desenvolver uma compreensão básica da extensão das aplicações do processamento de imagens é categorizar as imagens de acordo com sua fonte (por exemplo, visual, raios X e assim por diante).

A principal fonte de energia para imagens utilizada atualmente é o espectro eletromagnético de energia.

Imagens baseadas na radiação do espectro EM são as mais familiares, especialmente as imagens nas bandas visuais e de raios X do espectro.

Se as bandas espectrais forem agrupadas de acordo com a energia por fóton, obtemos o espectro mostrado na Figura

alt text

2.2.1 Imagens formadas por raios gama
As principais utilidades da formação de imagens por raios gama incluem a medicina nuclear e as observações astronômicas.

imr cabeca

2.2.2 Imagens formadas por raios X
Os raios X estão entre as fontes mais antigas de radiação EM utilizada para a formação de imagens. A mais conhecida utilização dos raios X é no diagnóstico médico, mas eles também são amplamente utilizados na indústria e em outras áreas, como a astronomia.

alt text alt text

2.2.3 Imagens na banda ultravioleta
As aplicações da “luz” ultravioleta são várias. Elas incluem litografia, inspeção industrial, microscopia, lasers, imagens biológicas e observações astronômicas. Ilustramos a formação de imagens nessa banda com exemplos da microscopia e da astronomia.

Sunscreen = Protetor Solar

alt text

2.2.4 Imagens na banda visível e na banda infravermelha
A banda do visível é o que a maioria dos seres humanos enxergam.

imr joelho

A banda infravermelha costuma ser utilizada em conjunção com a banda visível na formação de imagens.

alt text

2.2.5 Imagens na banda de micro-ondas
A principal aplicação da obtenção de imagens na banda de micro-ondas é o radar. A característica singular da aquisição de imagens por radar é sua capacidade de coletar dados em praticamente qualquer região a qualquer momento, independentemente do clima ou das condições de iluminação do ambiente.

alt text

2.2.6 Imagens na banda de rádio
Como no caso da aquisição de imagens no outro extremo do espectro (raios gama), as principais aplicações das imagens obtidas na banda de rádio situam-se na medicina e na astronomia. Na medicina, ondas de rádio são utilizadas em imagens por ressonância magnética (MRI, de magnetic resonance imaging).

imr joelho

Imagem de MRI do Joelho

imr cabeça

Imagem de MRI da Cabeça

O processamento de imagens colorida
É uma área que tem ganhado importância em virtude do aumento significativo da utilização de imagens digitais na Internet.

[ ]
!curl -o google.png https://static.giga.de/wp-content/uploads/2015/08/google-Photos-Backup-screen-rcm1200x627u.jpg
img = cv2.imread('google.png', cv2.IMREAD_UNCHANGED)
plt.imshow(img)


[ ]
RGB_im = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(RGB_im)


[ ]
 b,g,r = cv2.split(img)
[ ]
 r,g,b = cv2.split(RGB_im)
[ ]
from google.colab.patches import cv2_imshow
[ ]
cv2_imshow(b)


[ ]
cv2_imshow(g)


[ ]
cv2_imshow(r)


Para extrairmos as camadas RGB da imagem precisa separar cada camada da matriz:

[ ]
r = img.copy()
r = r[:, :, 0]
g = img.copy()
g = g[:, :, 1]
b = img.copy()
b = b[:, :, 2]
Com os comandos abaixo é possível ver as 3 imagens com um filtro para cada camada:

[ ]
plt.imshow(b,cmap='Blues_r');


[ ]
plt.imshow(r,cmap='Reds_r');


[ ]
plt.imshow(g,cmap='Greens_r');


EXERCÍCIOS
1) Elabore um programa em Python para:

a) ler uma foto sua ou da turma.

b) apresentar o tamanho em x e y da sua foto.

[ ]
from google.colab import drive
drive.mount ('/content/drive/')
Drive already mounted at /content/drive/; to attempt to forcibly remount, call drive.mount("/content/drive/", force_remount=True).
[ ]
import matplotlib.pyplot as plt
import numpy as np
from PIL import Image

target_dir = "/content/drive/My Drive/Imagens/odd-eyed-cat.jpg"
img = Image.open(target_dir)
plt.imshow(img)


2) Considerando o seu programa em Python:

a) Monte uma tabela com comparações do tamanho de 4 fotos.

b) Transforme a sua imagem de RGB para níveis de Cinza, apresente o resultado.

c) Transforme a sua imagem de RGB para HSV, apresente o resultado.

d) Separe as Bandas da sua imagem RGB e apresente o resultado.

e) Separe as Bandas da sua imagem HSV e apresente o resultado.

[ ]
import numpy as np 
import pandas as pd
import cv2 as cv 
from google.colab.patches import cv2_imshow # for google image display
from skimage import io 
from PIL import Image
import matplotlib.pylab as plt
[ ]
r = image.copy()
r = r[:, :, 0]
g = image.copy()
g = g[:, :, 1]
b = image.copy()
b = b[:, :, 2]
[ ]
plt.imshow(b,cmap='Blues_r');

[ ]
plt.imshow(r,cmap='Reds_r');

[ ]
plt.imshow(g,cmap='Greens_r');

[ ]
urls = ["https://upload.wikimedia.org/wikipedia/commons/6/69/June_odd-eyed-cat_cropped.jpg",
        "https://pt.m.wikipedia.org/wiki/Ficheiro:June_odd-eyed-cat_cropped.jpg"]
for url in urls:
  image = io.imread(url)        
  image_2 = cv.cvtColor(image, cv.COLOR_BGR2RGB)

  final_frame = cv.hconcat((image, image_2))
  cv2_imshow(final_frame)
  print('\n')

[ ]
gray_image = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
cv2_imshow(gray_image)


[ ]
image_3 = 255-gray_image
cv2_imshow(image_3)

[ ]
image_4 = (100.0/255)*(gray_image)+100
cv2_imshow(image_4)

[ ]
image_5 = 255.0*(gray_image/255.0)**2
cv2_imshow(image_5)

[ ]
image_6 = cv.cvtColor(image, cv.COLOR_BGR2HSV)
cv2_imshow(image_6)


[ ]
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
from matplotlib import rcParams

%matplotlib inline

# figure size in inches optional
rcParams['figure.figsize'] = 11 ,8

# read images


3) Baixe as imagens disponíveis em:

https://www.dropbox.com/sh/88d8vp9binlnavf/AACd9wE7EqoExwJrVbtOXi3Oa?dl=0

Estas imagens foram obtidas por Drones, na faixa do visível.

a) Implemente um programa em Python para ler uma imagem deste respositório.

b) Apresente a imagem carregada.

[ ]
from google.colab import files
from IPython import display

uploaded = files.upload()


[ ]
display.Image("DJI_0015.JPG", width = 1000)

4) Baixe as imagens disponíveis em:

https://www.dropbox.com/sh/hsrwp7qg7ynfo65/AACtmmJLuiermrg5JWDF50_Wa?dl=0

Estas imagens foram obtidas por câmeras na faixa do infravermelho. Esta aplicação consiste no reconhecimento facial.

a) Implemente um programa em Python para ler uma imagem deste respositório.

b) Apresente a imagem carregada.

[ ]
from google.colab import files
from IPython import display

uploaded = files.upload()

[ ]
display.Image("TD_IR_E_5.jpg", width = 1000)

5) Baixe as imagens disponíveis em:

https://www.dropbox.com/sh/gsvvb2xefqoytum/AABL5OXu9wvkWUp3nUvshHVga?dl=0

Estas imagens foram obtidas na faixa do Raio-X. Esta aplicação consiste na detecção de pessoas com pneumonia.

a) Implemente um programa em Python para ler uma imagem deste respositório.

b) Apresente a imagem carregada.

[ ]
from google.colab import files
from IPython import display

uploaded = files.upload()

[ ]
display.Image("person13_bacteria_50.jpeg", width = 1000)

