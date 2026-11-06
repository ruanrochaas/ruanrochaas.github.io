# Portfólio de Ruan Rocha

Site estático. HTML escrito à mão, um arquivo CSS compartilhado, sem build, sem framework, sem dependência de JavaScript para o conteúdo existir.

## Onde cada decisão mora

Três lugares, três perguntas. Este arquivo responde **o que vale hoje na execução** e não contém item em aberto: se está aqui, vale. O documento de marca responde o que a marca comunica e por quê, e é onde ficam as decisões ainda abertas. O CSS e o HTML são o que está no ar.

Quando os três divergem, **o que está no ar vence**, porque é o único verificável.

O procedimento completo (os três estados de uma decisão, o teste de onde escrever, o que fazer quando o documento e a página discordam) está na skill `onde-registrar-decisao`.

## Estrutura

```
index.html                          home
<slug-do-case>/index.html           uma pasta por case
assets/css/site.css                 o sistema visual, único
assets/img/<slug-do-case>/*.jpg     imagens, por case
```

O slug da URL vem do **título do case**, não do nome do projeto original. Em minúsculas, sem acento, separado por hífen. O nome do projeto original aparece dentro do texto, como contexto, nunca na URL.

Caminhos de imagem são relativos (`../assets/img/...`) para que o arquivo abra tanto em servidor quanto direto do disco.

## Regras de escrita

Valem para todo texto do site, sem exceção.

- **Nunca usar travessão (—) nem meia-risca (–) como pontuação.** Substituir por vírgula, dois-pontos, parênteses, ponto e vírgula ou ponto, conforme a função. Hífen de palavra composta é normal. Isso vale também ao revisar texto já escrito.
- **Não nomear empregador, clientes nem concorrentes.** O trabalho roda sob NDA. Escrever no nível do padrão do setor, não da instância: "uma consultoria de inovação", não o nome. Nenhum detalhe que permita identificar um cliente.
- Nada de texto de marca genérico. Se outra pessoa da área pode assinar a mesma frase trocando o nome, a frase não serve.
- Primeira pessoa, sem floreio. O case descreve o que foi decidido e por quê, não vende o resultado.

## Acessibilidade

Verificar antes de publicar qualquer página. Já verificado na página existente, manter ao editar.

- **WCAG 1.1.1.** Toda imagem classificada: decorativa recebe `alt=""` mais `aria-hidden="true"`; informativa recebe descrição do que mostra, não da conclusão; imagem com texto dentro precisa ter o texto transcrito no alt. Não começar alt com "imagem de".
- Aspas retas dentro de `alt="..."` cortam o atributo. Usar aspas tipográficas ou `&quot;`.
- **1.4.11** contraste de componente, **2.4.11** foco não obscurecido, **2.5.8** alvo de no mínimo 44 por 44 pixels.
- Hierarquia de cabeçalhos sem salto de nível. O estilo vem da classe (`.sec-title`, `.lvl`), nunca da tag, para que rebaixar um cabeçalho não mude o tamanho dele.
- Conteúdo em `<div lang="pt-BR">`. Trechos em inglês com `lang="en"`.
- Foco visível: `a:focus-visible` com `outline:2px solid var(--ink)` e `outline-offset:3px`.
- JavaScript só melhora, nunca viabiliza. O botão de topo nasce visível e o script o **esconde**, para que funcione com script desligado.

## Sistema visual

Tema único, claro. Não existe tema escuro e isso é decisão, não pendência.

### Tokens

```css
--bg:#F7F6F3    fundo
--ink:#1A1A1A   texto principal
--ink-2:#3D3B38 texto secundário
--ink-3:#6E6B66 nota, rótulo, apoio
--rule:#A8A5A0  fio de régua, moldura de imagem, borda de tabela
--well:#EFEEEA  campo de fundo de bloco destacado
--accent:#FFFF00 acento
```

`--rule` é para fio, nunca para texto nem para elemento clicável. O amarelo do acento compete com o ouro das imagens do case existente (perto de #FFC800), então **acento só em área sem imagem**.

### Tipografia

Archivo, com fallback Helvetica Neue, Helvetica, Arial. Seis degraus, todos em uso:

| Degrau | Tamanho / entrelinha | Peso | Tracking | Onde |
| --- | --- | --- | --- | --- |
| 01 | 76 / 72 | 600 | -0.03em | título da página |
| 02 | 44 / 48 | 600 | -0.02em | título de seção (`.sec-title`) |
| 03 | 26 / 34 | 500 | -0.01em | subtítulo (`.lvl`, `.lede`) |
| 04 | 17 / 30 | 400 | normal | corpo |
| 05 | 14 / 16 | 500 | 0.14em, caixa alta | rótulo |
| 06 | 11 / 16 | 400 | normal | nota, legenda |

Em telas até 899px: degrau 02 cai para 32/36 e o 03 para 21/28.

### Grade

12 colunas de 80px, medianiz de 24px, container de 1224px, margem de 64px. Tudo em módulo de 8px. Pontos de quebra em 1351px e 899px.

### Componentes

Usar os que existem antes de criar outro. Cada um carrega um significado fixo e repetir o recurso fora dele enfraquece os dois.

| Classe | O que é | Quando usar |
| --- | --- | --- |
| `.sec-title` + `.sec-num` | título de seção com número | abre toda seção |
| `.crit` | bloco de critério: barra de acento de 16px mais campo `--well` | um critério que governa decisão, não um destaque qualquer |
| `.rules` / `.seq` | sequência numerada com régua | passos em ordem |
| `.list-items` | lista com régua | itens sem ordem |
| `.part` | divisor de parte, amarelo pleno | virada de bloco do argumento |
| `.hl` | marca-texto amarelo | a frase que carrega a tese. **Máximo cinco por página.** Mais que isso vira permissão, não critério |
| `.pull` | frase de corte | respiro no meio de texto longo |
| `.quote` | citação | fala de terceiro |
| `.prompt` | bloco `<pre>` recolhido | material bruto, exibido como veio. **Não reescrever o conteúdo de um `<pre>`, nem para trocar travessão** |
| `.shot` / `.shot-wide` | imagem 3:4 e 16:9 | fio de 1px `--rule`, canto reto, sem sombra |
| `.toc` | índice em `<details>`, recolhido | navegação de página longa |
| `.to-top` | botão fixo de voltar ao topo | aparece só depois da primeira dobra |
| `.en` | resumo em inglês em `<details>` | um por página, na primeira tela |

## Cases

| Slug | Título | Estado |
| --- | --- | --- |
| `regras-que-ninguem-escreveu` | As regras que ninguém escreveu | publicado |

## Decisões revistas

Decisão que foi escrita, executada e não funcionou. A execução venceu. Uma linha por item, para que a mesma discussão não recomece do zero.

*(nenhuma registrada ainda)*

Formato: **o que foi decidido** → o que aconteceu ao executar → o que vale agora.

## Pendências conhecidas

- **O texto da home não está escrito.** A estrutura existe; o texto de posicionamento vem do documento de marca e não deve ser inventado aqui.

### Migração pendente do briefing do primeiro case

O documento "Site do case Laranjeira Deco, direção visual" (artefato, 29/10, 4.539 palavras) está desatualizado em relação à página e mistura três naturezas. Destino de cada parte:

| Vai para | Seções |
| --- | --- |
| Este arquivo | Tipografia, Paleta, Grade e espaçamento, Tratamento de imagem, Responsivo |
| Documento de marca | O que a página comunica e o que evita, Testes de aprovação |
| Nenhum dos dois, aposentar | Mapa de slots de imagem, Estrutura da página, A marca na página |

O terceiro grupo descreve a página que agora existe aqui. O HTML passou a ser a verdade sobre isso.

O detalhe que o briefing tem e este arquivo ainda não: espaçamento vertical, medida de texto, faixas de uso da grade, regra de recorte ampliado, formato e peso de imagem.

**Cinco decisões fechadas que nunca voltaram para o documento de marca**, onde ainda constam como não decididas. Pelo acordo, o valor passa a viver aqui e o documento de marca aponta para cá:

- entrelinha e medida para texto longo: 17/30 em medida de 496px
- rótulo em caixa alta: 14px com 0.14em, encerrando a convivência de dois valores
- grade: 12 colunas de 80px, calha 24px, container 1224px, módulo 8px
- favicon: quadrado tinta com a inicial em Archivo 600
- fundo escuro: não existe modo escuro, o escuro é território da imagem

Mais uma correção pendente no documento de marca sobre o critério de numeral de seção em cor com título em preto.

### Em aberto, não trava nada

- hex real do ouro das peças do primeiro case, hoje estimado em tela por volta de #FFC800
- hex real do laranja institucional

Os dois afetam só a regra de restrição do acento amarelo.
