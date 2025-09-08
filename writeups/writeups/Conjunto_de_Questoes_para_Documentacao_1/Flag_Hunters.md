# picoCTF - Flag Hunters
###### Solved by @Gunogueiramg

## Desafio: Flag Hunters
#### Introdução

Este desafio da plataforma [picoCTF](https://picoctf.org/) é bem completo e envolve uma análise cuidadosa de código para a capturara da flag. Para a resolução desse exercício, é necessário compreender o que são injeções em códigos e como elas podem ser um vetor de ataque importante.

#### Print do desafio
![Print do desafio](https://i.imgur.com/fpieEXU.png)

## Description

> *"Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it? There might be something in it for you.
The program's source code can be downloaded here.
Additional details will be available after launching your challenge instance."*
> *(As letras saltam dos versos para o refrão, como uma chamada de subrotina. Há um refrão oculto que este programa não imprime por padrão. Você consegue imprimi-lo? Pode haver algo nele para você. O código-fonte do programa pode ser baixado aqui.Mais detalhes estarão disponíveis após o lançamento da sua instância de desafio.)*

#### Além da descrição, há três dicas
## Dicas (Hints)

**Dica 1**
> *"This program can easily get into undefined states. Don't be shy about Ctrl-C."*
> *(Este programa pode facilmente entrar em estados indefinidos. Não tenha vergonha de usar Ctrl-C.)*

---

**Dica 2**
> *"Unsanitized user input is always good, right?"*
> *(A entrada de dados do usuário não sanitizada é sempre boa, certo?)*

---

**Dica 3**
> *"Is there any syntax that is ripe for subversion?."*
> *(Existe alguma sintaxe que seja propícia à subversão?)*

#### Interpretando as dicas
Essas dicas são muito importantes para o entendimento e conclusão do desafio. São instruções úteis, especialmente a 2 em que fala sobre a entrada de dados, onde está a vulnerabilidade do sistema e é o vetor de ataque para a captura da flag.

#### Solução
O desafio fornece um código fonte em python que pode ser acessado nesse link: [Código Flag Hunters](https://github.com/Gunogueiramg/Escola-de-Seguranca-Cibernetica/blob/main/códigos/flag_hunters.py). A interpretação desse código é essencial para a solução do desafio. Ao clicar em "Launch Instance", é gerado um código para se conectar via netcat para poder interagir com a instância. Ao copiar e executar o código no terminal, é apresentado as primeiras linhas da canção:
![print da estrofe](https://i.imgur.com/1tDAxWF.png)
Quando o código pede a interação, minha intuição foi escrever `(Singalong here!);`. Porém ao digitar essa entrada ou qualquer outra, o código simplesmente continua sua execução e exibe a mensagem que você escreveu:
![print da estrofe](https://i.imgur.com/t3ty3EJ.png) 
Foi nesse ponto que fiquei perdido e a ajuda do instrutor Vinícius foi fundamental. Ele me alertou sobre o início do código a flag é chamado no código em "secret_intro"
![print da estrofe](https://i.imgur.com/EfLvNse.png) .
Porém ao executar o código no terminal, ele pula esse trecho e começa a exibir a música. Então para encontrar a flag, é necessário de alguma forma, levar a execução do códgio para esse início. O código utiliza a variável lip, como mostra no print abaixo, para pular para diferentes trechos da música.
![print da estrofe](https://i.imgur.com/i9vRPZC.png) 
Dessa forma, é necessário manipular o código através da entrada para levar sua execução para o início do programa e mostrar o trecho secreto da música. Para isso, quando o programa nos dá abertura, inserimos o comand`;RETURN 0`. É necessário esse ponto e vírgula antes do return, pois, quando o valor da entrada cai nesse for `for line in song_lines[lip].split(';'):`, o ";" separa o coteúdo 'Crowd', que é ignorado pelas condições e o "RETURN 0", cai na seguinte condicional, do print mostrado logo acima. O valor zero do Return é atribuido a variável lip e através de `song_lines[lip]`, Com lip agora valendo 0, o programa, em seu próximo ciclo, buscará a linha em  `song_lines[0]` , executando o trecho secreto da música e revelando a flag.

![print da flag](https://i.imgur.com/Z2I5SKC.png) 

#### Conclusão

Flag:
>`picoCTF{picoCTF70637h3r_f0r3v3r_a5202532}`
>
>Esse foi sem dúvidas o exercício mais desafiador entre os 4. No entanto, foi muito importante para entender a importância de sanitizar a entrada do usuário para restringir seu acesso à funções que possa colocar todo o sistema em risco. 
