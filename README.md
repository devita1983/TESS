# TESS
# Science Discovery Engine (SDE) 

Lendo uma divulgação que esta no https://www.earthdata.nasa.gov/learn/articles/sde 

O texto trata do lançamento da Science Discovery Engine (SDE), uma ferramenta que disponibiliza vastas quantidades de informações científicas da NASA em um único local, facilitando o acesso e a colaboração da comunidade científica. A criação da SDE faz parte do compromisso da NASA em estabelecer e encorajar práticas de ciência aberta. O desenvolvimento da SDE envolveu um grande esforço da equipe de pesquisadores e desenvolvedores, que trabalharam por dois anos e compilaram quase 1 milhão de documentos, conjuntos de dados e ferramentas. A SDE foi apresentada na American Geophysical Union (AGU) 2022 Fall Meeting e o objetivo é tornar os dados e informações da NASA mais acessíveis e úteis para a comunidade científica.

Segunndo a líder das operações da equipe SDE e pesquisadora da NASA e membro da equipe OSSI - Kaylin Bugbee diz: 

"Para mim, a coisa mais empolgante sobre o SDE é como ele torna a riqueza de dados e informações de ciência aberta da NASA mais acessível a uma comunidade cada vez maior de usuários. Esta maior acessibilidade abrirá novos caminhos para a descoberta científica e incentivará mais pessoas a fazer uso dos dados e informações de ciência aberta que a NASA fornece"

Além do que foi mencionado no texto, pode ser interessante colaborar com informações sobre como a SDE funciona e como os pesquisadores podem utilizá-la para acessar os dados da NASA. Também pode ser relevante falar sobre as principais vantagens e desafios de se trabalhar com dados científicos em grande escala, bem como sobre o papel da ciência aberta na aceleração do progresso científico e tecnológico. Outra informação útil pode ser sobre como a comunidade científica pode colaborar e contribuir para a melhoria contínua da SDE, oferecendo feedback e sugestões para aprimorar a plataforma e torná-la ainda mais útil para todos os envolvidos.

Resumidamente todo o texto fala sobre a criação da SDE, uma plataforma que reúne informações científicas da NASA de maneira organizada e acessível para pesquisadores. Antes da SDE, essas informações estavam dispersas em mais de 128 fontes diferentes, tornando difícil a busca por dados específicos. Com a SDE, os pesquisadores podem economizar tempo na busca por informações e dados científicos. A SDE continuará a ser aprimorada com a adição de mais conteúdo e recursos, permitindo colaboração e inovação dentro e entre as diferentes disciplinas científicas.

Depois de ler o texto e acessei um dos artigos do projeto, um deles era  o TESS - https://heasarc.gsfc.nasa.gov/docs/tess/ 

# O que significa TESS

TESS significa Transiting Exoplanet Survey Satellite - É um projeto de telescópio espacial liderado pelo Instituto de Tecnologia de Massachusetts para o programa de pequena exploração da Nasa. O custo desse projeto foi 200 milhões USD (2013) 

Mas vocês devem estar perguntando... Porque o TESS é importante? 

O satélite TESS (Transiting Exoplanet Survey Satellite) é importante porque é um telescópio espacial que tem como objetivo descobrir novos planetas fora do nosso sistema solar, também conhecidos como exoplanetas. Através da observação de pequenas quedas no brilho de estrelas distantes, o TESS pode detectar planetas em trânsito, isto é, quando passam em frente à sua estrela hospedeira, bloqueando parte da luz desta. Essas informações são utilizadas para determinar a massa, tamanho e outras características dos exoplanetas. A descoberta desses exoplanetas é fundamental para a compreensão da formação e evolução de sistemas planetários, e pode ajudar a responder questões fundamentais sobre a existência de vida em outros planetas.

Tenho feitos alguns testes com alguns dados da documentação https://heasarc.gsfc.nasa.gov/docs/tess/ porém, quando tentei outros dados e tive problemas para baixar curvas de luz de um banco de um banco de dados, talvez por não ter a estrutura para baixa-los. 

Mas vamos a prática, o que consegui por em prática baseando nos estudos apresentados na documentação https://heasarc.gsfc.nasa.gov/docs/tess/. Mas antes de tudo você deve saber do que se trata esse código:

Este é um código em Python que usa a biblioteca Lightkurve para procurar e processar dados do telescópio Kepler.

Primeiro, é feita a atualização da biblioteca Lightkurve. Em seguida, importa-se a biblioteca Lightkurve e a biblioteca numpy.

Então, é feita uma busca por um arquivo de pixel alvo com o nome "KIC 7461601" usando o método search_targetpixelfile da biblioteca Lightkurve. O parâmetro "author" é definido como "Kepler" e o "cadence" é definido como "long". O resultado da busca é baixado usando o método download e armazenado na variável tpf_example. Em seguida, o método plot é usado para plotar a imagem do arquivo de pixel alvo, com a máscara de abertura definida como "pipeline" e novamente sem especificar a máscara de abertura.

O mesmo processo é repetido para outro arquivo de pixel alvo com o nome "KIC 2437317". No entanto, o parâmetro "quality_bitmask" é definido como "hard" para obter uma melhor qualidade de dados. O método plot é usado para plotar a imagem do arquivo de pixel alvo, com a máscara de abertura definida como "pipeline".

Em seguida, o arquivo de pixel alvo é convertido em uma curva de luz usando o método to_lightcurve, com a máscara de abertura definida como "pipeline". A curva de luz é plotada usando o método plot.

Em seguida, as curvas de luz são novamente plotadas com diferentes máscaras de abertura: "threshold", "all" e uma máscara personalizada criada usando o método create_threshold_mask com um limiar definido como 1. Essas curvas de luz são sobrepostas em um único gráfico usando o método normalize e plot.

Finalmente, outro arquivo de pixel alvo com o nome "KIC 2437901" é baixado com o parâmetro "quality_bitmask" definido como "hard". No entanto, este arquivo de pixel alvo é classificado como "crowded", o que significa que há muitas estrelas próximas que podem interferir nos dados. O processamento desse arquivo pode ser mais desafiador e pode exigir técnicas adicionais.

# Objetivo de Aprendizagem ao final do tutorial você: 

Entenda como usar a fotometria de abertura para transformar uma série de imagens bidimensionais em uma série temporal unidimensional.

* Ser capaz de determinar a abertura mais útil para fotometria em um alvo Kepler/K2 .
* Crie sua própria curva de luz para um único trimestre/campanha de dados Kepler/K2
* Fonte: http://heasarc.gsfc.nasa.gov

Introdução Este tutorial faz parte de uma série sobre como lidar com dados Kepler e K2 com Astropy e Lightkurve. Como você viu anteriormente nesta série, o Lightkurve fornece utilitários que permitem criar sua própria curva de luz a partir de um arquivo de pixel de destino Kepler ou K2 . Neste tutorial, veremos os princípios por trás do processo de realização de fotometria de abertura em um alvo. Em seguida, entraremos em detalhes e aprenderemos como personalizar nossas aberturas para aproveitar ao máximo nossos dados.

* Primeiro devemos instalar o Lightkurve, na primeira tentativa de instalar deu um erro então fiz uma mudança conforme a fonte,  caso o python fosse desatualizado ou até mesmo tivesse algumas mudanças no Lightkurve. Use ! Python -m pip install Lightkurve --upgrade para instalar o Lightkurve.

Depois de Instalado devemos fazer a importação do lightkurve e do matplotlib para visualização 

* import lightkurve as lk
* import numpy as np
* %matplotlib inline

* A fotometria é definida como o processo de medir o brilho de um objeto astronômico. Especificamente, faremos fotometria de série temporal: medindo esse brilho ao longo do tempo. Telescópios como o Kepler usam câmeras com dispositivos de carga acoplada (CCD) ( Kepler Instrument Handbook , Seção 4) para obter imagens de seus alvos em intervalos regulares — esse intervalo é conhecido como cadência — e realizamos fotometria para transformar cada imagem em uma medição de fluxo .
Você pode ver como a luz desta estrela se espalha pelo TPF. O processo de escolha de quais pixels usar para fotometria é chamado de definição de abertura. Ao adicionar o fluxo em vários pixels, obtemos uma medição mais precisa do brilho do objeto.

Para exibir o gráfico utilize: 

* tpf_example = lk.search_targetpixelfile("KIC 7461601", author="Kepler", cadence='long', quarter=10).download()
* tpf_example.plot(aperture_mask='pipeline');
* tpf_example.plot();

![image](https://user-images.githubusercontent.com/117879893/219692121-c30b065b-55aa-4e7f-981c-b6d7d3bd957c.png)

* E os pixels que não usamos? Pense em uma fotografia granulada: observamos a mesma coisa em todos os dados CCD, mas é mais difícil reconhecer a olho nu em fotografias de telescópios com pixels grandes. Esse ruído granulado é chamado de “ruído de tiro” e surge de flutuações na corrente que alimenta um dispositivo eletrônico de coleta de fótons. Para a fotometria de abertura, precisamos nos preocupar com o ruído de disparo, pois ele domina o que vemos no “fundo” de uma imagem, ou seja, a luz que vemos em pixels que não possuem luz do nosso alvo. Na realidade, a maioria dos pixels será algum tipo de combinação de “sinal” e “fundo”. Quando escolhemos nossa abertura para fotometria, procuramos otimizar a quantidade de sinal que coletamos e minimizar a contribuição do ruído de fundo.

É assim que a abertura usada pelo pipeline Kepler se parece para nossa estrela de exemplo:

![image](https://user-images.githubusercontent.com/117879893/219692828-edc75b14-cd33-49b8-86fc-0fcbf59814eb.png)

* Você pode não esperar que a abertura da estrela tenha esse formato - afinal, as estrelas são fontes pontuais. Em muitos casos, as estrelas no Kepler parecerão circulares, como seria de esperar. No entanto, na borda do plano focal, alguns alvos podem aparecer borrados em uma direção. E mesmo para uma estrela com propagação circular, a abertura pode ter uma forma diferente. A maneira como a propagação da luz interage com o detector é definida por algo chamado função de dispersão de ponto (PSF) ou função de resposta de pixel (PRF). O PSF/PRF do Kepler é descrito em detalhes na Seção 3.5 do Kepler Instrument Handbook .

* Começaremos baixando um arquivo de pixel de destino. Vamos usar os dados de longa cadência do Kepler para observar KIC 2437317, uma estrela que apresenta variações de brilho devido à rotação ( Reinhold & Gizon, 2015 ). Estamos baixando o trimestre 10, pois houve uma perda mínima de dados durante este trimestre ( Manual de características de dados do Kepler , seção 4.1).

![image](https://user-images.githubusercontent.com/117879893/219693342-debeac55-2be5-4599-b264-4f862d68827c.png)

* Observe que esse TPF é mais lotado do que o que vimos na Seção 1. Ainda podemos apontar quais pixels provavelmente contêm o sinal da estrela e quais são dominados por ruído. No entanto, há também uma estrela de fundo neste TPF: o pixel brilhante à esquerda. Queremos evitar captar o sinal dessa estrela.

Podemos usar Lightkurve para plotar a abertura do pipeline:

![image](https://user-images.githubusercontent.com/117879893/219693439-9047b89d-b386-4eff-9358-6ccb116f74e7.png)

* Observe os picos em torno de 935 e 970 dias. Isso coincide com as interrupções na coleta de dados durante as quais o Kepler foi apontado para a Terra para fazer o downlink dos dados. Essas quebras estão associadas a pequenas mudanças de foco do telescópio Kepler , causadas pelos efeitos térmicos associados ao apontar a antena do Kepler em direção à Terra. Esses picos artificiais são uma forma de ruído sistemático.

![image](https://user-images.githubusercontent.com/117879893/219693563-71bbd212-0921-4c03-8518-f34a66740d93.png)

* Podemos fazer uma comparação lado a lado das curvas de luz resultantes normalizando-as da seguinte maneira:

![image](https://user-images.githubusercontent.com/117879893/219693645-26d68434-8b89-454b-8c1d-714cddb13f92.png)

* Nossa estrela é bastante brilhante, com uma magnitude Kepler de 14,6, então não vemos muita variação nos níveis de ruído entre essas três curvas de luz. Mas, como você pode ver, usar todos os pixels significa incluir a luz da estrela de fundo que dilui o sinal da nossa estrela, tornando a rotação mais difícil de detectar a olho nu. Por outro lado, usar todos os pixels reduz o ruído sistemático perto dos dias 935 e 970, porque as mudanças de foco do telescópio têm menos impacto quando uma máscara de grande abertura é usada.

A curva de luz da máscara de limite parece menos diluída do que aquela que usa todos os pixels, mas ainda parece marcadamente diferente da curva de luz da abertura do pipeline. Podemos usar outra das funções de Lightkurve para ver por que esse é o caso:

![image](https://user-images.githubusercontent.com/117879893/219694188-8f43aba6-e1b6-4954-9ed4-1fb156458dee.png)

#### Esta é a máscara de limite padrão de 3 desvios padrão de Lightkurve e, para este TPF, há apenas um pixel com fluxo acima desse corte. Observe como as aberturas Lightkurve funcionam: os pixels marcados Truena matriz de máscara de abertura são os usados ​​para fotometria.

* Depois será feito máscaras próprias booleanas como esta. Mas usando a função create_threshold_mask() para tentar reproduzir a máscara do pipeline. Visto que o TPF acima tem muito mais pixels brilhantes do que fracaos, espera-se uma mediana brilhante, então será feito um limite mais baixo. 

![image](https://user-images.githubusercontent.com/117879893/219695380-3eb0763e-6825-4be6-b489-798dd35bea6b.png)

* Agora recriamos a máscara do pipeline, que podemos usar para realizar a fotometria novamente. Como seria de esperar, produz os mesmos resultados que a máscara de pipeline:

![image](https://user-images.githubusercontent.com/117879893/219695466-a8b6d3b2-2281-4d69-bcb5-cf72a2859529.png)

### Criando uma abertura de limiar personalizada com Lightkurve

* Agpra vamos ver como realizar fotometria de abertura com uma abertura personalizada. Vamos mudar para uma estrela diferente, KIC 2437901. Esta estrela é uma gigante vermelha oscilante (Colman et al., em preparação), mas estamos interessados ​​nela porque foi processada usando um grande TPF, e há um segunda estrela brilhante capturada na imagem.

![image](https://user-images.githubusercontent.com/117879893/219695922-4587866e-6ee4-4274-899f-0beb26df6c30.png)

* Vamos nos concentrar naquela estrela no canto superior direito. Não é capturado na abertura do pipeline, mas é um achado fortuito no TPF, então podemos realizar nossa própria fotometria nele com uma abertura personalizada. Vamos ver como é a máscara de limite para este TPF:

![image](https://user-images.githubusercontent.com/117879893/219696170-804d12ec-e336-4be7-b6f7-9175fd60f1a6.png)

* Vamos plotar isso em cima do TPF, assim: 

![image](https://user-images.githubusercontent.com/117879893/219696492-d21983f3-580b-475b-bbf7-3362806d9851.png)

##### OPS, Nossa abertura personalizada ainda seleciona a estrea brilhante no centro. Quando o método de limite produz várias regiões contíguas, o compoartamento padrão do método é retornar a região mais próxima do centro. Podemos modificar esse comportamento passando um reference_pixelargumento para especificar a região que mais nos interessa. O argumento é definido de forma que reference_pixel=(0,0) se refira ao canto inferior esquerdo. Assim selecionamos a região no canto superior direito. 

![image](https://user-images.githubusercontent.com/117879893/219697012-56592792-3836-4cc6-84ce-ca2044521f23.png)

* Agora podemos realizar a fotometria de abertura usando esta máscara:

![image](https://user-images.githubusercontent.com/117879893/219697111-7594fc1b-2939-4b44-89a8-b182dc3f0c6d.png)

#### Parece que há algum sinal nesta estrela - um período de dois dias! Na verdade, esta estrela é KIC 2437948, uma provável binária (Colman et al., em preparação).

* Usando o NumPy para criar manualmente uma matriz de máscara de abertura. Para esta estrela, fária sentido selecionar uma zona 3x3 no canto superior direito da imagem. Isso pode ser complicado: os arrays 2D Numpy indexam o eixo y primeiro e são impressos com o índice zeroth y na parte superior do array, equando um array plotado coloca o zero na parte inferior, como em um gráfico normal. 

![image](https://user-images.githubusercontent.com/117879893/219697786-20d4ce55-5df4-4a3c-a248-5511751a3856.png)

* Vamos plotar a máscara personalizada em cima do TPF. Observe que o eixo y em nossa matriz aparece invertido, conforme descrito acima. Ao lidar com imagens e matrizes NumPy, é uma boa prática plotá-las todas as vezes e garantir que você esteja vendo o que espera.

![image](https://user-images.githubusercontent.com/117879893/219697894-69554ba0-10a3-4078-b331-9acb20174433.png)

### Recortando uma estrela de fundo

Usando a função cutout() de Lightkurve , podemos emular o processo de criação de uma máscara de limite apenas nos pixels nos quais estamos interessados. Este método é adequado apenas para grandes TPFs com uma estrela de fundo claramente separada, como o caso de KIC 2437901 e KIC 2437948.

![image](https://user-images.githubusercontent.com/117879893/219698018-8a59e715-c760-4971-81bf-1434c0b557c4.png)

![image](https://user-images.githubusercontent.com/117879893/219698071-bdb44d74-b9c6-4bcd-85d5-3b8961a70dbe.png)

* Este ainda é um objeto TargetPixelFile , então podemos usar todas as mesmas funções:
* Infelizmente, a máscara de limite seleciona apenas um pixel aqui. Mas com um TPF menor, também é mais conveniente selecionar pixels individuais para nossa máscara:

![image](https://user-images.githubusercontent.com/117879893/219698343-59bef92d-bcc2-40c6-891c-8922b02abd5b.png)

![image](https://user-images.githubusercontent.com/117879893/219698399-492fa59a-f804-4e21-8eba-ed7468b5c54e.png)

### Sobre este caderno 

Autora: Isabel Colman ( isabel.colman@sydney.edu.au) Atualizado em: 2020-09-15

When using Lightkurve, we kindly request that you cite the following packages:

* lightkurve
* astropy
* astroquery
* tesscut 

#### Você pode tentar fazer o processo passo-a-passo, ja que o desafio é fazer! seria facil postar todo código para reprodução, mas quebrar a cabeça é o verdadeiro sentido, então aqui está o link para os primeiros passos https://heasarc.gsfc.nasa.gov/docs/tess/step0-install-lightkurve.html# boa queimação do cerebro! 

Boa sorte!

* E aqui está o TESS em relação a Terra - QUE COISA LINDAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA! 
![image](https://user-images.githubusercontent.com/117879893/219701720-42892dd7-8704-4f9a-af52-3c0f06da6b75.png)

Fonte
![image](https://user-images.githubusercontent.com/117879893/219701852-1184be01-cb69-48c7-98f0-f2dbec763390.png)


