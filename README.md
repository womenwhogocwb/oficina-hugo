# Sites estáticos com framework Hugo

Esse tutorial é um material de apoio da oficina [Sites estáticos com framework Hugo](https://www.meetup.com/Women-Who-Go-CWB/events/267913185/), realizada em Curitiba em 15/02/20, que teve como instrutora @knienkotter e como monitoras @amandabrbz e @erikacarvalho.

Nossa ideia é disponibilizar o conteúdo online para que tanto quem esteve quanto quem não esteve presente na oficina possa se beneficiar do conteúdo.

A versão atual compreende apenas as notas sobre **Hugo + Netlify**, mas planejamos adicionar em breve um passo-a-passo para publicação com **Hugo + GitHub Pages**.

🥳 Divirta-se! 

### Sites estáticos

#### O que são?

Um site estático é entregue ao navegador da pessoa usuária exatamente da mesma forma que está armazenado, em contraste a sites dinâmicos.

É baseado principalmente em HTML (__HyperText Markup Language__), que é uma "linguagem de marcação".

O documento HTML é interpretado pelo navegador, que o renderiza e exibe o conteúdo formatado.

#### Principais usos
 
- Site pessoal
- Blog
- Site institucional

#### Exemplos

[Tableless](https://tableless.com.br), [1Password](https://1password.com), [Let's Encrypt](https://letsencrypt.org), [TreinaWeb Blog](https://www.treinaweb.com.br/blog/)

#### Vantagens de usar

- Custo de hospedagem (baixo ou nenhum)
- Performance
- Menos brechas de segurança

#### Desvantagens de usar

- Pra cada atualização é necessário um novo deploy
- Não é ótimo pra atividades que envolvam buscas (portais e e-commerces)

### Sobre o Hugo

- Feito em 🐭[Go](https://go.dev), uma linguagem de programação desenvolvida pela Google
- Rápido
- Simples de usar: com 4 comandos seu site está no ar
- Tem temas prontos disponíveis em [themes.gohugo.io](http://themes.gohugo.io)

## Mão na massa

- Nesse tutorial vamos usar [Hugo](https://gohugo.io) pra construir um site, [Netlify](https://www.netlify.com) pra publicá-lo, [Git](https://git-scm.com) para versionar o projeto e [GitHub](http://github.com) para hospedar o repositório.
- Os comandos informados devem ser digitados no terminal (para quem usa Windows, sugerimos usar o Git Bash). O `$` indica o início de um comando, mas não deve ser digitado.
- Caso precise de mais orientações sobre Git, [esse repositório aqui](https://github.com/womenwhogocwb/oficina-git-github) tem o conteúdo da oficina sobre git e github.

#### ✅ Requisitos para seguir o passo-a-passo

- Ter uma conta no GitHub. Caso não tenha, crie a sua gratuitamente [aqui](http://github.com).
- Ter instalado na sua máquina:

  ⚙️ IDE ou editor de texto de sua preferência. Caso não tenha nenhum, [GoLand](https://www.jetbrains.com/go/) tem um período de 30 dias grátis.

  ⚙️ Git. Caso não tenha, é possível obter gratuitamente [aqui](https://git-scm.com).

### Instalação

#### Windows

As instruções podem ser encontradas [aqui](https://gohugo.io/getting-started/installing/#windows)

#### Mac OS

Sugerimos que seja usado o [Homebrew](https://brew.sh), mas no próprio site do Hugo há mais instruções ([aqui](https://gohugo.io/getting-started/installing/#macos)).

Comando para instalar com Homebrew: `$ brew install hugo`
   
#### Linux
   
Use o package manager da sua distro/de sua preferência, instruções adicionais [aqui](https://gohugo.io/getting-started/installing/#linux)

### Passo-a-passo

1. **Checar versão do Hugo que está instalada**
 
   - Isso permite verificar se a instalação ocorreu e dá a informação necessária para comparar com a "__Minimum Hugo Version__" que o tema precisa

   - Digite o seguinte comando:
     
     `$ hugo version`

2. **Criar novo site**

   - Onde você quiser que seja criada a pasta com todo o projeto, digite o seguinte comando:

     `$ hugo new site meusite`
     
   - Se der certo, você deve receber a seguinte mensagem:
     #### Congratulations! Your new Hugo site is created in <...>

3. **Inicializar o repositório git**

    - Digite os seguintes comandos:
    
      `$ cd meusite`
    
      `$ git init`

4. **Escolher um tema**

   - Nesse tutorial, vamos usar o tema **Noteworthy**
   - No site é possível visualizar outros temas: [themes.gohugo.io](http://themes.gohugo.io)

5. **Configurar o repositório do tema como submodule do seu repositório**    

    - Adicionar o submodule com o seguinte comando:

      `$ git submodule add <url> <path>`

        Exemplo:
        
        `$ git submodule add https://github.com/kimcc/hugo-theme-noteworthy themes/noteworthy`

6. **Trocar o arquivo de configuração**

   - Copiar o arquivo `📄config.toml` da pasta `📂exampleSite` para a raiz do seu projeto (`📂meusite`)
   
   - Onde encontrar o arquivo:
   
   ``` 
   📂meusite    
     └──📂themes    
        └──📂noteworthy
           └──📂exampleSite
              └──📄 config.toml
   ```

   - OBS: Se quiser iniciar seu site com conteúdos para visualizar melhor as possibilidades do tema, copie também a pasta 📂**content**. Você poderá excluir o conteúdo que não é seu mais tarde.

7. **Editar o arquivo de configuração que foi copiado**
   
   - No arquivo `📄config.toml` que foi copiado para a sua pasta `📂meusite`, promover as seguintes alterações: 

      - Adicionar (ou corrigir) `theme = <nome do tema>` com o nome do tema (no caso, `theme = "noteworthy"`)
      - Remover `themesDir = "../.."` (se houver)
      - Alterar o conteúdo do campo `title`
      - Na parte dos links da redes sociais, preencher com as `urls` das páginas que você quiser que sejam exibidas
      - Remover links das páginas que não deseja que sejam exibidas
      - Alterar o valor do campo `description` para a mensagem que deseja que seja exibida no topo do site
      - Promover outras alterações que desejar
   
8. **Alterar a URL base no arquivo de configurações**

   - Primeiro, você deve visitar o endereço que deseja utilizar para verificar se recebe a mensagem `Not Found` - o que indica que o subdomínio está disponível. O endereço será: `https://<NOMEESCOLHIDO>.netlify.com`
      1) Se não estiver disponível, tente outro até que o retorno seja `Not Found`
      2) Se estiver disponível, siga para a linha abaixo
   - Colocar a URL do seu site no campo `baseURL` em `📄config.toml`, dessa forma:
      ```
      baseURL = "https://<NOMEESCOLHIDO>.netlify.com"
      ```
9. **Criar seu primeiro post**

    - Digitar o seguinte comando:
   
      `$ hugo new posts/primeiro-post.md`
     
    - Editar o arquivo que foi criado e adicionar o conteúdo que desejar
      - Onde encontrar o arquivo:
   
      ``` 
      📂meusite    
        └──📂content    
           └──📂posts
              └──📄 primeiro-post.md
      ```
    
      - OBS: Cada post tem um campo `draft`, que pode ter o valor `true` (caso seja ainda um rascunho) ou `false` (caso deva ser publicado). Edite o campo para sinalizar a publicação do post.

    - Repetir quantas vezes desejar para adicionar posts
   
10. **Visualizar o site localmente** (para ver como está ficando 🤓)

    - Digitar o seguinte comando:
      
      `$ hugo server -D`

      - OBS: A flag `-D` força o conteúdo que está sinalizado como draft a ser publicado junto. Caso não deseje que isso aconteça, utilizar o comando sem a flag `-D`.
      
    - Em seu navegador de preferência, visitar o endereço `localhost:1313` (ou o endereço que for informado no próprio terminal após rodar o comando acima)

    - Para parar, apertar `Ctrl + C` no terminal

11. **Configurar a versão do Hugo que será utilizada pela Netlify**

    - Para criar o arquivo, digite o seguinte comando:
     
      `$ touch netlify.toml`
      
    - Edite o arquivo e insira nele o seguinte conteúdo:
    
      ```
      [context.production.environment]
      HUGO_VERSION = "X.XX.X"
      ```
      - OBS: no campo `HUGO_VERSION` deve ser colocado o valor indicado como "__Minimum Hugo Version__" na página do tema. A que foi usada nesse tutorial, para essa versão do **Noteworthy** foi `0.55.2`
      
     - É possível encontrar mais sobre isso [aqui](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)
            
12. **Fazer o commit do seu conteúdo na máquina**

    - Digitar os seguintes comandos:
    
       `$ git status` - para visualizar onde ocorreram alterações
       
       `$ git add .` - para adicionar as alterações à staging area
       
       `$ git commit -m "<título do commit>"` - para realizar o commit
       
     - OBS: caso precise de mais instruções sobre git, visitar [esse repositório aqui](https://github.com/womenwhogocwb/oficina-git-github).

13. **Criar repositório no Git provider de sua preferência** (nesse tutorial, estamos usando o [GitHub](http://github.com))

    - OBS: O repositório não precisa ser público, pois daremos permissão de leitura ao Netlify mais tarde. Pode ser criado como `Private`

14. **Dar push no conteúdo do repositório local para o remoto**

    - Digitar os seguintes comandos:

      `$ git remote add origin https://github.com/<USER>/<REPO>.git` - pra adicionar sua origem remota
        - OBS: o endereço correto poderá ser encontrado na página inicial do seu repositório enquanto não houver um arquivo `README.md`, ou no botão `Clone or download` disponível para ser copiado
      
      `$ git push -u origin master` - para realizar o push

15. **Criar um site dentro do [Netlify](https://www.netlify.com)**

    OBS: caso não tenha uma conta, criar uma usando autenticação via GitHub

    - No Netlify:

      1) Escolher **Git provider**
      2) Escolher o **repositório** no qual você trabalhou durante esse tutorial
      3) Últimas configurações e build

16. **Publicar o site**

    - Via Netlify, isso acontece como o 3º passo da sua configuração do novo site, dentro da própria plataforma.
    
      - OBS: é possível que você receba um erro similar a esse aqui no log do Deploy:
      
        ```
        ERROR <DATA> <HORA> NOTEWORTHY theme does not support Hugo version 0.54.0. Minimum version required is 0.55.2
        ```
      - Se isso ocorrer, volte ao passo 11 para retificar a versão e faça um novo push

17. **Configurar seu domínio customizado** (opcional)

    - Caso utilize um domínio customizado, ele deve ser colocado no campo `baseURL` no passo 8

18. **Editar nome do subdomínio**

    - No site da Netlify, siga o caminho informado abaixo e altere o nome do site para o mesmo que você colocou no campo `baseURL` no passo 8 
    
      ➡️`Settings` -> `Domain management` -> `Domains` -> `Custom domains` -> `...` -> `Edit site name`
    
19. **Pronto!**

    Seu site está no ar e disponível para você alterá-lo.
    
    Sugerimos deletar os posts que tenham sido copiados da pasta `exampleSite` do tema durante a construção.
    
    Lembre-se que sempre que promover alterações no seu repositório local você deve realizar um novo `push` no seu repositório remoto para que as alterações possam ser implementadas!

💡 Precisa de mais dicas? Dá uma olhada [aqui](https://gohugo.io/categories/getting-started) (em inglês).

💻 Colocou seu site no ar com a ajuda desse tutorial? Compartilha nas redes sociais e marca a gente! Nossa arroba é `@womenwhogocwb` tanto no [twitter](https://www.instagram.com/womenwhogocwb/) quanto no [instagram](https://twitter.com/womenwhogocwb) e a hashtag é `#wwgcwb`