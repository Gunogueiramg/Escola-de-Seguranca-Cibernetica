# picoCTF - Cookie Monster Secret Recipe
###### Solved by @Gunogueiramg

## Desafio: Cookie Monster Secret Recipe
#### Introdução

Este é um desafio da plataforma [picoCTF](https://picoctf.org/). Classificado como nível fácil, ele é de simples resolução para iniciantes no mundo de CTF's. Esse exercício, incentiva o desafiante em utilizar a [ferramenta de desenvolvedor](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Howto/Tools_and_setup/What_are_browser_developer_tools) do navegador para capturar a flag e assim concluir a tarefa. O desafio explora conceitos de [cookies de navegador](https://pingback.com/br/resources/o-que-sao-cookies/) e  com isso, há um trocadilho com uma história de um monstro que guarda uma receita secreta de um **cookie** que também pode ser traduzido como **biscoito** para o português.

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

#### Interpretando as dicas
As dicas fornecidas conduzem o desafiante em explorar os cookies utilizados no site, através da ferramenta de desenvolvedor no navegador para capturar a flag. 

#### Solução
Ao iniciar a instância do desafio, é aberta uma página web inicial do "Cookie Monster's Secret Recipe" exigindo um usuário e senha para o login.

![print do site](https://i.imgur.com/KkvLBM7.png)

Ao inserir qualquer nome de usuário e senha nos campos e clicar em login, aparece a seguinte mensagem:
> **Acesso Negado (Access Denied)**
>
> *"Cookie Monster says: 'Me no need password. Me just need cookies!'"*
> *(O Monstro das Bolachas diz: 'Eu não preciso de senha. Eu só preciso de cookies!')*
>
> *"Hint: Have you checked your cookies lately?"*
> *(Dica: Você verificou seus cookies ultimamente?)*
> 
Seguindo as dicas para encontrar o cookie, é necessário abri a interface de desenvolvimento com o comando: **Ctrl + Shift + I** e selecionar a aba "Application". No campo de "storage", aparecerá o elemento cookies, como mostra o seguint print:
![print do cookie](https://i.imgur.com/MpzUkre.png)

No campo "Value" dentro do cookies, é possível encontrar a seguinte mensagem encriptada: `"cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzX0E2RkEwN0Q4fQ%3D%3D"`. Através da plataforma [CyberChef](https://gchq.github.io/CyberChef/), partindo o encondig [base64](https://www.redhat.com/en/blog/base64-encoding), ao colocar a sequência encriptada no Input da ferramenta, no Output, podemos ver em texto claro, a flag que estamos procurando:
![print da flag](https://i.imgur.com/pLZrvgz.png)


#### Conclusão

Flag:
>`picoCTF{c00k1e_m0nster_l0ves_c00kies_A6FA07D8}`
>
>Esse foi um excelente desafio introdutório de CTF, uma vez que, explora conceitos de cookies de sessão de navegador e ao mesmo tempo exige que o desafiante descubra qual enconding foi utilizado para codificar a mensagem encontrada. Até encontrar a flag, foi explorados diversos conceitos que certamente serão fundamentais para a resolução de novos desafios.


