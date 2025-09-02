# picoCTF - Cookie Monster Secret Recipe
###### Solved by @Gunogueiramg

## Desafio: Cookie Monster Secret Recipe
#### Introdução

Este é um desafio da plataforma [picoCTF](https://picoctf.org/). Classificado como nível fácil, ele é ideal para iniciantes no mundo de CTF's, assim como . Esse exercício, incentiva o desafiante em utilizar a [ferramenta de desenvolvedor](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Howto/Tools_and_setup/What_are_browser_developer_tools) do navegador para capturar a flag e assim concluir a tarefa. O desafio explora conceitos de [cookies de navegador](https://pingback.com/br/resources/o-que-sao-cookies/) e  com isso, há um trocadilho com uma história de um monstro que guarda uma receita secreta de um cookie que também pode ser traduzido como biscoito para português.

#### Print do desafio
![Print do desafio](https://i.imgur.com/uLX2Qft.png)

## Description

> *"Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe? Additional details will be available after launching your challenge instance."*
> *(O Monstro dos biscoito escondeu sua receita secreta de biscoito em algum lugar de seu website. Como um aspirante a detetive de biscoito, sua missão é desvendar este delicioso segredo. Você consegue ser mais esperto que o Monstro dos biscoitos e encontrar a receita escondida? Detalhes adicionais estarão disponíveis após o lançamento da sua instância do desafio.)*

#### Além da descrição, há três dicas
## Dicas (Hints)

**Dica 1**
> *"Sometimes, the most important information is hidden in plain sight. Have you checked all parts of the webpage?"*
> *(Às vezes, a informação mais importante está escondida à vista de todos. Você já verificou todas as partes da página?)*

---

**Dica 2**
> *"Cookies aren't just for eating - they're also used in web technologies!"*
> *(Cookies não são apenas para comer - eles também são usados em tecnologias web!)*

---

**Dica 3**
> *"Web browsers often have tools that can help you inspect various aspects of a webpage, including things you can't see directly."*
> *(Navegadores web frequentemente possuem ferramentas que podem te ajudar a inspecionar vários aspectos de uma página, incluindo coisas que você não consegue ver diretamente.)*

#### Interpretando a dica

#### Solução
Ao iniciar a instância do desafio, é aberto uma página web inicial do "Cookie Monster's Secret Recipe" exigindo um usuário e senha para o login.

![print do site](https://i.imgur.com/KkvLBM7.png)



Então, inserindo a string em hexadecimal fornecida no enunciado diretamente na caixa de texto principal (que aceita entradas em hexadecimal, sem a necessidade de conversão prévia), e o trecho conhecido da flag `"crypto{"` na caixa de texto da opção marcada **"Use the ascii key"** (que permite entradas em texto padrão), realizamos a primeira análise:

[![Captura-de-tela-2025-06-13-141610.png](https://i.postimg.cc/6q2y50Cm/Captura-de-tela-2025-06-13-141610.png)](https://postimg.cc/YL7pdQn6)

A ferramenta aplicará o XOR entre os primeiros bytes da string e a palavra `"crypto{"`, revelando a parte inicial da chave secreta utilizada na criptografia:

[![Captura-de-tela-2025-06-13-142408.png](https://i.postimg.cc/xdpHPgy6/Captura-de-tela-2025-06-13-142408.png)](https://postimg.cc/QB5H8Qz7)

Agora que sabemos o começo da chave secreta, `"myXORkey"`, utilizamos essa informação para realizar uma nova operação de XOR. Desta vez, em vez de usar o trecho conhecido da flag, aplicamos diretamente a chave descoberta sobre toda a string em hexadecimal.

[![Captura-de-tela-2025-06-13-143321.png](https://i.postimg.cc/RhSBV12z/Captura-de-tela-2025-06-13-143321.png)](https://postimg.cc/dkxX5CqW)

A própria ferramenta do dcode se encarrega de repetir automaticamente a chave ao longo de toda a entrada — o que é essencial, já que a chave tem apenas 8 bytes, enquanto a string criptografada possui dezenas de bytes. Com isso, conseguimos aplicar corretamente a operação de XOR byte a byte, o que revela o conteúdo original criptografado: a flag completa.

[![Captura-de-tela-2025-06-13-143409.png](https://i.postimg.cc/Sx2psx1j/Captura-de-tela-2025-06-13-143409.png)](https://postimg.cc/21Dt9rDf)

#### Conclusão

Flag:
>`crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}`

Este desafio foi uma excelente aplicação prática dos conceitos fundamentais de criptografia com XOR. Através de um pequeno trecho conhecido da flag, conseguimos deduzir parte da chave secreta utilizada na cifra. A partir disso, utilizamos uma ferramenta online para repetir essa chave ao longo de toda a mensagem criptografada, revertendo o processo de encriptação e revelando a flag completa.

Mais do que simplesmente encontrar a resposta, este exercício reforça a importância de padrões previsíveis em contextos criptográficos. Quando uma parte da mensagem é conhecida — ou pode ser adivinhada —, todo o sistema se torna vulnerável. Essa lição é essencial não só para resolver desafios em CTFs, mas também para compreender os riscos reais em sistemas mal projetados no mundo da segurança da informação.
