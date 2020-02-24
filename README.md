## Notas sobre Hugo + Netlify

#### Sites estáticos

- **O que são?**

   Um site estático não depende de processamento no servidor - é entregue pro navegador da pessoa usuária exatamente como está armazenado, em contraste a sites dinâmicos.

   É baseado principalmente em HTML (HyperText Markup Language), que é uma "linguagem de marcação".

   O documento HTML é interpretado pelo navegador, que o renderiza e exibe o conteúdo formatado.

- **Principais usos**
 
   Site pessoal, blog, site institucional

- **Exemplos**

   [Tableless](https://tableless.com.br), [1Password](https://1password.com), [Let's Encrypt](https://letsencrypt.org), [TreinaWeb Blog](https://www.treinaweb.com.br/blog/)

- **Vantagens de usar**

   - Custo de hospedagem (nenhum ou baixo)
   - Performance
   - Menos brechas de segurança

- **Desvantagens de usar**

   - Pra cada atualização é necessário um novo deploy
   - Não é ótimo pra atividades que envolvam buscas (portais e e-commerces)
   - Não é dinâmico

#### Sobre o Hugo

- Feito em [Go](https://go.dev), uma linguagem de programação desenvolvida pela Google
- Rápido
- Simples de usar: com 4 comandos seu site está no ar
- Tem temas prontos disponíveis em [themes.gohugo.io](http://themes.gohugo.io)

#### Mão na massa

- Nesse tutorial vamos usar [Hugo](https://gohugo.io) pra construir um site, [Netlify](https://www.netlify.com) pra publicá-lo, [Git](https://git-scm.com) para versionar o projeto e [GitHub](http://github.com) para hospedar o repositório remoto.

1. Instalação

   - Windows

     🆘🆘🆘

   - Mac OS
   
     Sugerimos que seja usado o [Homebrew](https://brew.sh)

     Comando para instalar com Homebrew: `$ brew install hugo`
     
   - Linux
   
     Use o package manager da sua distro/de sua preferência

2. Checar versão

   - Digite o seguinte comando:
     
     `$ hugo version`

3. Criar novo site

   - Na altura onde você quiser que seja criada a pasta com todo o projeto, digite o seguinte comando:

     `$ hugo new site meusite`
     
   - Se der certo, você deve receber a seguinte mensagem:
     #### Congratulations! Your new Hugo site is created in <...>

4. Inicializar o repositório git

    - Na altura da pasta `meusite`, digite o seguinte comando:
    
      `$ git init`

5. Escolher um tema

   - Escolher um tema no site: [themes.gohugo.io](http://themes.gohugo.io)
   - Nesse tutorial, vamos usar o tema `Noteworthy`

6. Configurar o repositório do tema como submodule do seu repositório    

    - Setar o submodule com o seguinte comando:

      `$ git submodule add <url> <path>`

        Exemplo:
        `$ git submodule add https://github.com/kimcc/hugo-theme-noteworthy themes/noteworthy`

7. Copiar todo o conteúdo da pasta **exampleSite** (que está dentro de `themes/noteworthy`) para a raiz do seu projeto (`meusite`)

   - OBS: isso ajudará a visualizar as possibilidades do tema, mas o conteúdo pode ser deletado mais tarde

8. Editar o arquivo de configuração `config.toml` da sua pasta `meusite`
   - Adicionar (ou corrigir) `theme = <nome do tema>` com o nome do tema (no caso, `theme = "noteworthy"`)
   - Remover `themesDir = "../.."` (se houver)
   - Alterar `title`
   - Preencher com as `urls` das páginas que você quiser que sejam exibidas
   - Remover links das páginas que não deseja que sejam exibidas
   - Alterar `description` para a mensagem que deseja que seja exibida no topo do site
   - Promover outras alterações que desejar
   
9. Visualizar o site localmente

   - Digitar o seguinte comando:
      
      `$ hugo server -D`

     OBS: Cada post tem um campo `draft`, que pode ter o valor `true` (caso seja ainda um rascunho) ou `false` (caso deva ser publicado). A flag `-D` força o conteúdo que está sinalizado como draft a ser publicado junto. Caso não deseje que isso aconteça, utilizar o comando sem a flag `-D`.

   - Em seu navegador de preferência, visitar o endereço `localhost:1313` (ou o endereço que for informado no próprio terminal após rodar o comando acima)

   - Para parar, apertar `Ctrl + C` no terminal

10. Criar seu primeiro post

    - Digitar o seguinte comando:
   
      `$ hugo new posts/primeiro-post.md`
     
    - Editar o arquivo que foi criado e adicionar o conteúdo que desejar
    
    - Repetir quantas vezes desejar

11. Criar repositório no Git provider de sua preferência (nesse tutorial, estamos usando o [GitHub](http://github.com))

    - OBS: Não precisa ser público, pois daremos permissão de leitura ao Netlify mais tarde

12. Fazer o commit do seu conteúdo na máquina

    - Digitar os seguintes comandos:
    
       `$ git status` - para visualizar onde ocorreram alterações
       
       `$ git add .` - para adicionar as alterações à staging area
       
       `$ git commit -m "<título do commit>"` - para realizar o commit
       
     - OBS: caso precise de mais instruções sobre git, visitar [esse repo aqui](https://github.com/womenwhogocwb/oficina-git-github).

13. Dar push no conteúdo do repositório local para o remoto

    - Digitar os seguintes comandos:

      `$ git remote add origin https://github.com/<USER>/<REPO>.git` - pra adicionar sua origem remota
      
      `$ git push -u origin master` - para realizar o push

14. Criar um site dentro do [Netlify](https://www.netlify.com)

    OBS: caso não tenha uma conta, criar uma usando autenticação via GitHub

    - No Netlify:

      1) Escolher **Git provider**
      2) Escolher o **repositório** no qual você trabalhou durante esse tutorial
      3) Últimas configurações e build

15. Publicar o site

    - Via Netlify, isso acontece como o 3º passo da sua configuração do novo site, dentro da própria plataforma.

      > OBS: é possível que você receba um erro similar a esse aqui
      >
      >     ERROR <DATA> <HORA> NOTEWORTHY theme does not support Hugo version 0.54.0. Minimum version required is 0.55.2
      >
      > para definir a versão do Hugo que a Netlify deve usar, é necessário criar um arquivo chamado `netlify.toml` na altura da raiz do seu projeto com o seguinte conteúdo:
      >
      >     [context.production.environment]
      >     HUGO_VERSION = "0.XX.X"
      >
      > mais sobre isso [aqui](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)

16. Configurar seu domínio customizado (opcional)

17. Editar nome do subdomínio (opcional)

    - Em `Settings` -> `Domain management` -> `Domains` -> `Custom domains`

18. Editar `baseURL` em `config.toml`
 
    - Copiar a URL do seu site e colar no campo `baseURL`

19. Realizar novo `push` no seu repositório remoto para que as alterações possam ser implementadas
    
20. **Pronto!** Seu site está no ar e disponível para você alterá-lo. Sugerimos deletar os posts que tenham sido copiados da pasta `exampleSite` do tema durante a construção.

💡 Precisa de mais dicas? Dá uma olhada [aqui](https://gohugo.io/getting-started/quick-start/) (em inglês).