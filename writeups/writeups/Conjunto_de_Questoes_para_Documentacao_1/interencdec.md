# picoCTF - Interencdec
###### Solved by @Gunogueiramg

## Desafio:Interencdec
#### Introdução

Este desafio da plataforma [picoCTF](https://picoctf.org/) é classificado como fácil e ele fornece ao desafiante um arquivo com uma mensagem codificada e propõe a descoberta da flag através de mais de um processo de codificação. Em seu enunciado, com as tags do exercício, temos pistas que confirmam o foco do exercício: `Cryptography` e também quais tipos de codificação serão necessários para concluir o desafio: `base64` e `caesar`   
#### Print do desafio
![Print do desafio](https://i.imgur.com/AUNiPU6.png)

## Description

> *"Can you get the real meaning from this file."*
> *(Você consegue entender o significado real deste arquivo?.)*

#### O desafio fornece uma única dica
## Dica (Hint)

**Dica**
> *"Engaging in various decoding processes is of utmost importance"*
> *(O envolvimento em vários processos de decodificação é de extrema importância)*


#### Interpretando as dicas
Com essa dica em mãos, já se sabe que decodificar uma só vez a mensagem não será suficiente para obter a flag. 

#### Solução
Ao fazer o download do arquivo base do desafio. nos deparamos com a seguinte mensagem: `YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyeG9OakJzTURCcGZRPT0nCg==`. Utilizando a ferramenta "Cipher Identifier" do site [dcode](https://www.dcode.fr/cipher-identifier) para identificar qual o tipo de codificação, está presente no arquivo, ele retorna que o encoding utilizado mais provável é o [base64](https://www.redhat.com/en/blog/base64-encoding)
![print do resultado encoding](https://i.imgur.com/MdsYWK8.png)

O mesmo site, fornece uma [ferramenta de decodificação de codificação base64](https://www.dcode.fr/base-64-encoding) e ao submeter a mensagem do arquivo, obtém-se a seguinte mensagem: `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ=='`. Podemos ver claramente que a mensagem ainda se encontra codificada. Diante dessa nova mensagem codificada, quando eu estava desenvolvendo o desafio, tive problemas ao prosseguir, uma vez que ao submetê-la no "Cipher Identifier" novamente, ele me retornou resultados com pouca precisão. Foi nesse momento que a ajuda do instrutor Vinícius foi muito importante para o prosseguimento do desafio. Ele me aconselhou a pegar somente o conteúdo da mensagem encriptada entre as aspas: `d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ==` e me informou que mensagens terminadas com dois sinais de igualdade, indicam um forte indício que o código em questão se trata de uma codificação base64. Com esses direcionamentos, submeti mais uma vez o código, agora somente com o conteúdo entre as aspas, no decodificador de base64. Como resultado, tive a seguinte mensagem: `wpjvJAM{jhlzhy_k3jy9wa3k_lh60l00i}`. Nota-se mais uma vez que a mensagem ainda não está em texto legível, porém, pela primeira vez fica clara a aparição das chaves presentes na mensagem. Chaves essas que são uma espécie de máscara para as flags do picoCTF. Com essa nova informação em mãos fui ao site [site112](https://site112.com/cifra-de-cesar-codificar-descodificar) para tentar decodificar utilizando a [Cifra de César](https://www.splunk.com/en_us/blog/learn/caesar-cipher.html). Escolhi esse caminho pois além de constar no enunciado do desafio a Cifra de César, eu já tinha conhecimento que nesse tipo de codificação, a mensagem original, sofre um deslocamento de posições à direita e que o segredo para descobrir a mensagem, é justamente identificar qual foi o deslocamento utilizado. No site, realizei alguns testes das possíveis posições, partindo do deslocamento 1 à direita. Foi quando cheguei no deslocamento 7, que encontrei a flag do desafio.

![Print da flag](https://i.imgur.com/VvOhGH1.png)

#### Conclusão
Flag:
>`picoCTF{caesar_d3cr9pt3d_ea60e00b}`
>
>Esse desafio foi excelente para conhecer e entender melhor os tipos de criptografia e as ferramentas de decodificação utilizadas. Uma vez conhecidos esses métodos, nos próximos CTF's certamente terei um melhor direcionamento para a descoberta das novas flags.


