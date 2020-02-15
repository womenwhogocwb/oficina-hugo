## Notas sobre Hugo

#### Sites estáticos

- O que é um site estático?

   Um site que não depende de processamento no servidor - é entregue pro navegador da pessoa usuária exatamente como está armazenado, em contraste a sites dinâmicos.

   É baseado principalmente em HTML (HyperText Markup Language), que é uma "linguagem de marcação".

   O documento HTML é interpretado pelo navegador, que o renderiza e exibe o conteúdo formatado.

- Vantagens de usar: custo de hospedagem, performance, menos brechas de segurança

   Principais usos: site pessoal, blog, sites institucionais

   Exemplos: Tableless, 1Password, Let's Encrypt, TreinaWeb Blog

- Desvantagens de usar: pra cada atualização é necessário um novo deploy, não é ótimo pra atividades que envolvam buscas (portais e e-commerces), não é dinâmico

#### Sobre o Hugo

- Feito em Go, uma linguagem de programação desenvolvida pela Google
- Rápido
- Simples de usar: com 4 comandos seu site está no ar
- Tem temas prontos disponíveis em [themes.gohugo.io](http://themes.gohugo.io)

#### Mão na massa

1. Instalação

   - Windows

     🆘🆘🆘

   - Mac OS ou Linux com Homebrew

     `$ brew install hugo`

2. Checar versão

   `$ hugo version`

3. Criar novo site

   `$ hugo new site meusite` - na altura do repositório que você vai querer usar

   #### Congratulations!

4. Escolher um tema

   - Escolher no site: [themes.gohugo.io](http://themes.gohugo.io)
   - Pra oficina, vamos usar o tema `Noteworthy`

5. Configurar o tema

    - na altura do repositório

       `$ git init`

    - setar o submodule da seguinte forma:

      $ git submodule `<url>` `<destino>`

        Exemplo:
        `$ git submodule add https://github.com/kimcc/hugo-theme-noteworthy themes/noteworthy`

6. Copiar todo o conteúdo da pasta **exampleSite** para a sua raiz

7. Editar `config.toml`
   - Em `config.toml` alterar `theme = <nome do tema>`
   - Em `config.toml` remover `themesDir = "../.."`

8. Visualizar site local

   - `$ hugo server -D`

     obs: cada post tem um campo `draft`, que pode ser `true` (caso seja ainda um rascunho) ou `false` (caso deva ser publicado). a flag -D força o conteúdo que é draft a ser publicado junto.

   - com um navegador, visitar o endereço `localhost:1313`

   - para parar, apertar `Ctrl + C`

9. Editar arquivo de configuração

   - Título
   - Outras infos

10. Criar primeiro post

     - `$ hugo new post/primeiro-post.md`
     - inserir conteúdo dentro do arquivo que foi criado

11. Criar repositório no [GitHub](http://github.com)

    - não precisa ser público, pois daremos permissão ao Netlify mais tarde

12. Fazer o commit do seu conteúdo na máquina

    - `$ git status`
    - `$ git add .`
    - `$ git commit -m "<título do commit>"`

13. Dar push no conteúdo do repo local pro remoto

    - `$ git remote add origin https://github.com/<user>/<repo>.git`
    - `$ git push -u origin master`

14. Criar um site dentro do Netlify

    obs: caso não tenha uma conta, é só criar uma usando GitHub

    - Escolher Git provider
    - Escolher Repositório
    - Últimas configurações e build

15. Publicar o site

    - se for via Netlify, isso acontece como o 3º passo da sua configuração do novo site, dentro da própria plataforma.

      > obs: é possível que você receba um erro similar a esse aqui
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

18. Editar `baseURL` em `config.toml` conforme a URL do seu site
