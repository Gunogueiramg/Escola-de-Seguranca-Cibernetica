# picoCTF - RED
###### Solved by @Gunogueiramg

## Desafio: RED
#### Introdução

Este é um desafio da plataforma [picoCTF](https://picoctf.org/). Possui nível fácil como sua  classificação e é bastante intrigante uma vez que ao baixar o arquivo base para a descoberta da flag, nos deparamos somente com a imagem de um pequeno quadrado vermelho. Para a resolução dessa tarefa, foi necessário explorar novos conceitos e conhecimentos acerca de ocultar informações dentro de imagens. 
#### Print do desafio
![Print do desafio](https://i.imgur.com/ABbNYb4.png)

## Description

> *"RED,RED,RED,RED"*
> *(VERMELHO, VERMELHO, VERMELHO, VERMELHO)*

#### O desafio possui três dicas
## Dicas (Hints)

**Dica 1**
> *"The picture seems pure, but is it though?"*
> *(A imagem parece pura, mas será mesmo?)*

---

**Dica 2**
> *"Red?Ged?Bed?Aed?*
> *(Vermelho?Ged?Cama?Aed?)*

---

**Dica 3**
> *"Check whatever Facebook is called now."*
> *(Confira o nome atual do Facebook.)*

#### Interpretando as dicas
As dicas do desafio instigam a analizar a imagem para além do seu aspecto visual para encontrar a flag. É fornecida uma dica forte ao sugerir ao desafiante checar como chama o Facebook agora, que é Meta, claramente um indício para verificar os  [metadados](https://www.techtarget.com/whatis/definition/image-metadata) da imagem.

#### Solução
Ao baixar o conteúdo do desafio, nos deparamos com a seguinte imagem de um simples quadrado vermelho:

![imagem do quadrado](https://i.imgur.com/LOrYRmm.png)

O assunto de metadados de imagens, não é novidades para mim. Já havia conhecimento desse recurso e também como as redes sociais implementam mecanismos para ocultar os metadados originais de uma foto para fins de privacidade e segurança do usuário. Seguindo orientações, baixei e configurei uma máquina virtual Kali Linux no Virtual Box em meu computador. Minha primeira linha de investigação, foi ir atrás de ver os metadados da imagem através de uma ferramenta que já conhecia que é o [exiftool](https://devsecops.puziol.com.br/blog/exiftool). Para salvar o arquivo no kali foi bem simples, bastou arrastar o arquivo da máquina host para a área de trabalho da vm. Para executar o ExifTool, eu instalei com o comando: `sudo apt install exiftool` e para ler o metadado, no terminal executei o seguinte comando:`exiftool ~/Desktop/red.png`. O resultado dos metadados, pode ser observado na imagem abaixo:

![print do terminal metadados](https://i.imgur.com/16xkPkn.png)

Ao me deparar com o metadado da imagem,chamou-me a atenção o campo com o seguinte poema:
> Crimson heart, vibrant and bold,.Hearts flutter at your sight..Evenings glow softly red,.Cherries burst with sweet life..Kisses linger with your warmth..Love deep as merlot..Scarlet leaves falling softly,.Bold in every stroke. 
(Coração carmesim, vibrante e ousado. Corações vibram ao vê-lo. Noites brilham suavemente em vermelho. Cerejas explodem com doce vida. Beijos permanecem com seu calor. Amor profundo como merlot. Folhas escarlates caindo suavemente. Ousado em cada pincelada.)

Fiquei bastante confuso atrás de pistas nesse poema. Após não conseguir decifrar nenhum código nesse trecho, recorri ao instrutor Vinícius que me instruiu que eu pesquisasse sobre [esteganografia](https://olhardigital.com.br/2023/09/27/dicas-e-tutoriais/o-que-e-esteganografia-tecnica-de-esconder-informacoes-em-imagens/) em imagens. Foi pesquisando diferentes ferramentas para fazer esteganografia em imagens que descobri a ferramenta zsteg. Para baixá-la, é necessário executar os seguintes comandos no terminal: `sudo apt install ruby-full` seguido por `sudo gem install zsteg`. Com o seguinte comando: `zsteg ~/Desktop/red.png`, apareceu algo bastante interessante, como podemos ver no print do terminal:

![print da flag codificada](https://i.imgur.com/YNEY1pC.png)

Agora, além do poema, podemos notar um código que se parece muito com uma mensagem codificada em base64. Através do site [CyberChef](https://olhardigital.com.br/2023/09/27/dicas-e-tutoriais/o-que-e-esteganografia-tecnica-de-esconder-informacoes-em-imagens/), com a ferramenta de decodificação de base64, conseguimos finalmente concluir o desafio e obter a flag em texto claro. 

![print da flag](https://i.imgur.com/z3Bc27I.png)

#### Conclusão

Flag:
>`picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}`

Capturar essa flag, foi uma tarefa bastante desafiadora. Pude aprofundar nos conceitos de metadados em imagens e tive contato pela primeira vez com esteganografia. Esse é sem dúvidas um exercício bem completo de captura a flag dentro de uma imagem. Os conceitos aprendidos certamente serão muito úteis para desafios desse mesmo segmento.
