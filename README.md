Autores: 

William Felipe Tsubota e Gabriel C. M.

Linguagem de programação: Python 3.8.3 (anaconda)

Versão da OpenGL e GLSL: Pyopengl 3.1.5 e GLSL 3.3 (shader 330)

Parâmetros fixos (constantes) utilizados na implementação: SIZEOF_FLOAT é o
tamanho do float em bytes, CUBE, CONE, SPHERE e TORUS são constantes para
identificar qual a forma na lista de objetos de cena, WIDTH e HEIGHT.

Informações sobre os arquivos no zip (código do projeto enviado): Projeto é composto
de uma pasta Objects contendo todos arquivos .obj, uma pasta shader330 contendo os
shaders que serão utilizados, código fonte base na raiz do projeto (base.py) e a pasta
Screens, na qual é guardada as screenshots salvadas durante a aplicação.

Funções (implementações) adicionais da aplicação:

def transform(shader, m) -> Passa a matriz model de um objeto para o shader para que
possa ser feito a transformação (rotate, translate, scale ou shear)
def color(shader, m) -> Define a cor do objeto
def lightToShader() -> Passa a lista de luzes para o shader
def camToShader(cam) -> Passa a posição da câmera para o shader (para a variável
viewpos)
def viewToShader(shader) -> Passa a matriz view para o shader
def projToShader(shader) -> Passa a matriz projeção para o shader
def setShadeType(shader)
def setConstantsK(typeReflection, v) -> Seta as constantes k
def initialConstantK()
def screenshot(filename)

Bibliotecas externas:

pywavefront pip install pywavefront
pyrr pip install pyrr
PIL pip install Pillow
pyGLM pip install PyGLM
numpy pip install numpy

Outras informações que achar pertinente:

Foi utilizado o Anaconda na versão 4.8.4 para rodar o projeto.

Foi utilizado uma biblioteca externa (pywavefront) para ler os .OBJs. Ela retorna uma lista
no formato: [t1, t2, n1, n2, n3, p1, p2, p3], em que t são texturas, n, normais e p, posição do
vértice. É essa lista que enviamos ao vbo e acessamos cada tipo de elemento através de
ponteiros na função glVertexAttribPointer()

Utilizamos 6 buffers no vbo, 4 para os objetos e 2 para eixo e luz
Utilizamos uma thread para coletar os comandos digitados no terminal, a forma que coleta
é: pode-se digitar vários comandos separados por linha ou um comando apenas,
independente ele enfileira (primeiro que entra, primeiro que sai) em uma lista (a lista é
commands), e a cada iteração no display desenfileiramos um comando por vez. Ainda sobre
essa thread, há um time.sleep(1), que mostra devagar a execução de cada comando, caso
queira que seja executado rapidamente os comandos, trocar para um valor de 0.14 entre
0.5 (Funciona para o Gabriel, para mim independente do valor ele executa
instantaneamente, achamos que é por causa da diferença de ide utilizada).

No add_shape, a lista que atribuímos ao objeto passado pelo usuário é (id do objeto, o
nome que o usuário passou para esse objeto, matriz identidade para a model, cor do objeto
branco), no qual o id do objeto é o que foi definido no começo do código, e a cor do objeto é
RGB (1,1,1) que é o branco.

Cada comando contém uma lista de string, estando na posição 0 o comando, e nas
subsequentes os argumentos do comando
OBS: Em alguns testes foi preciso esperar um pouco antes de fechar o programa (cerca de
2-4 segundos) depois do comando save, caso contrário uma imagem totalmente preta era
salva

Como instalamos o anaconda:

1 - Instalar o anaconda (importante selecionar para salvar as informações no "path"
terminando a instalação)
2 - Após instalar o anaconda, rodar os seguintes comandos como admin no cmd:

conda install pyopengl
conda install -c conda-forge freeglut
python -m pip install PyOpenGL PyOpenGL_accelerate
