# <p align="center">FlappyBird Game</p>

Projeto desenvolvido com HTML, CSS e muito JavaScript puro! Feito para a conclusão dos módulos de **HTML, CSS, JavaScript e Integração entre as três (Manipulação do DOM via JS)** do curso de Desenvolvimento WEB da [Cod3r!](https://www.cod3r.com.br)<br><br>
<a href="https://luaxlz.github.io/HTML-FlappyBird-Game/">Confira o jogo aqui!</a>

## Proposta:

O desafio consiste em criar uma réplica do game FlappyBird utilizando HTML, CSS e JS, afim de solidificar o conhecimento aprendido dos módulos citados e utilizar, em prática, a manipulação do DOM e entender como funciona um código em uma aplicação ativa através de manipulações, criações e coleta de dados.

## Desafios:

O desafio desse projeto era realmente a manipulação do DOM via JS, a parte de HTML e CSS é bem simples, porém tive bastante dificuldade em "me encontrar" na manipulação do DOM, levou um tempo e um pouco mais de leitura para entender o que fazia o que e como as peças se encaixavam, neste projeto utilizei como forma de seleção apenas o `document.querySelector()`.
Foi muito utilizado funções construtoras para criar e depois disso manipular os elementos do jogo como a propria área do game, as barrerias e o passaro como no exemplo:

```JavaScript
function Passaro(alturaJogo) {
    let voando = false
    this.elemento = novoElemento('img', 'passaro')
    this.elemento.src = 'imgs/passaro.png'

    this.getY = () => parseInt(this.elemento.style.bottom.split('px')[0])
    this.setY = y => this.elemento.style.bottom = `${y}px`

    window.onkeydown = e => voando = true
    window.onkeyup = e => voando = false

    this.animar = () => {
        const novoY = this.getY() + (voando ? 8 : -5)
        const alturaMaxima = alturaJogo - this.elemento.clientHeight

        if(novoY <= 0) {
            this.setY(0)
        } else if(novoY >= alturaMaxima) {
            this.setY(alturaMaxima)
        } else {
            this.setY(novoY)
        }
    }
    this.setY(alturaJogo / 2)
}
```

Usei o `this.propriedade` para poder tornar publico quaisquer dados ou funções que julguei necessário, pode-se perceber também o uso massivo de manipulação DOM para movimentação dos elementos e colisão entre os objetos como neste exemplo:

```JavaScript
function colisao(passaro, barreiras) {
    let colidiu = false
    barreiras.pares.forEach(parDeBarreiras => {
        if(!colidiu) {
            const superior = parDeBarreiras.superior.elemento
            const inferior = parDeBarreiras.inferior.elemento
            colidiu = estaoSobrepostos(passaro.elemento, superior) || estaoSobrepostos(passaro.elemento, inferior)
        }
    })
    return colidiu
}
```
