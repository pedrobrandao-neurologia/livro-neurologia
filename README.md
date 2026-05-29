# Semiologia Neurológica — Manual Colaborativo (FM/UnB)

Livro de acesso aberto escrito em **Markdown** e construído com
[**Bookdown**](https://bookdown.org). Cada capítulo é um arquivo de texto; ao
integrar uma alteração ao repositório, o livro é **republicado automaticamente**
na web, em PDF e em EPUB.

---

## Para autores: como publicar uma atualização (sem instalar nada)

1. Abra a página do livro e clique em **✏️ Edit** no topo do capítulo. Isso abre
   o arquivo `.Rmd` correspondente no editor do GitHub.
2. Edite o texto (é Markdown — veja o "kit de escrita" abaixo).
3. Em **Commit changes**, descreva a alteração e confirme (ou abra um
   *pull request*, se preferir revisão).
4. Pronto. Em poucos minutos a *GitHub Action* reconstrói e publica o livro.

> O botão **Edit** aparece porque `_output.yml` aponta para o repositório.
> Troque `SEU-USUARIO/livro-semiologia` pelo caminho real do repositório em
> `index.Rmd` e `_output.yml`.

---

## Kit de escrita (Markdown + Bookdown)

| Quero…                         | Escrevo…                                                            |
|--------------------------------|---------------------------------------------------------------------|
| Título de capítulo + âncora    | `# Título {#id-do-capitulo}`                                        |
| Subtítulo de seção + âncora    | `## Seção {#id-da-secao}`                                           |
| Negrito / itálico              | `**negrito**` · `*itálico*`                                         |
| Citar uma referência           | `[@campbell2020]` (a chave vem do `references.bib`)                 |
| Link interno (entre seções)    | `[exame dos reflexos](#reflexos)`                                  |
| Referência cruzada numerada    | `\@ref(forca)` · tabela: `\@ref(tab:mrc)` · figura: `\@ref(fig:x)` |
| Caixa de destaque              | `::: {.note}` … `:::`                                               |
| Caixa de alerta                | `::: {.warn}` … `:::`                                               |
| Pérola clínica                 | `::: {.pearl}` … `:::`                                              |
| Tabela com legenda numerável   | `Table: (#tab:mrc) Legenda.` antes da tabela pipe                  |

### Adicionar uma figura
Coloque a imagem em `figuras/` e insira:

    ```{r fig-exemplo, fig.cap="Legenda da figura."}
    knitr::include_graphics("figuras/exemplo.png")
    ```

Cite-a no texto com `\@ref(fig:fig-exemplo)`.

### Adicionar uma referência
Acrescente uma entrada BibTeX em `references.bib` e cite-a com `[@chave]`.
A bibliografia (estilo **Vancouver**, numérico) é montada sozinha ao final.

### Criar um novo capítulo
1. Crie o arquivo `NN-nome.Rmd` (ex.: `05-sensibilidade.Rmd`), começando por
   `# Título {#id}`.
2. Adicione o nome do arquivo, na posição desejada, à lista `rmd_files` do
   `_bookdown.yml`.

---

## Para editores: build local (opcional)

Requer R + Pandoc (o RStudio já traz o Pandoc).

    # uma única vez
    install.packages(c("bookdown", "rmarkdown"))

    # construir o livro inteiro (HTML + PDF + EPUB)
    bookdown::render_book("index.Rmd", output_format = "all")

    # apenas o site, com recarga automática enquanto escreve
    bookdown::serve_book()

A saída fica em `_book/`. O PDF exige LaTeX (ex.: `tinytex::install_tinytex()`).

---

## Estrutura do projeto

    index.Rmd            Capa, metadados (YAML) e apresentação
    _bookdown.yml        Ordem dos capítulos e rótulos em português
    _output.yml          Configuração do site (gitbook), PDF e EPUB
    NN-*.Rmd             Capítulos (texto Markdown)
    references.bib       Bibliografia (BibTeX)
    vancouver.csl        Estilo de citação numérico
    style.css            Identidade visual (Spectral + Source Sans, teal)
    preamble.tex         Preâmbulo LaTeX da saída PDF
    figuras/             Imagens dos capítulos
    .github/workflows/   Publicação automática (GitHub Actions)

## Publicação

Ao dar `push` na branch `main`, a Action `build-and-deploy-book` constrói o livro
e o publica na branch `gh-pages`. Em **Settings → Pages**, selecione *Deploy from
branch → gh-pages /(root)*. O site fica em
`https://SEU-USUARIO.github.io/livro-semiologia/`.

> Licença do conteúdo: Creative Commons BY-NC 4.0.
