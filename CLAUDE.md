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

Tema único, claro. Não existe tema escuro e isso é decisão, não pendência: o escuro é território da imagem, não da marca. Toda a paleta e toda verificação de contraste assumem o fundo `--bg`.

### Tokens

```css
--bg:#F7F6F3     fundo
--ink:#1A1A1A    texto principal (16.1:1 sobre --bg)
--ink-2:#3D3B38  texto secundário, nota, legenda, texto em bloco de prompt (10.33:1)
--ink-3:#6E6B66  rótulo, apoio (4.91:1; sobre --well, 4.57:1)
--rule:#A8A5A0   fio de régua, moldura de imagem, borda de tabela (2.27:1)
--well:#EFEEEA   campo de fundo de bloco destacado e de bloco de prompt
--accent:#FFFF00 acento (1.01:1)
```

- Nenhuma combinação de texto abaixo de 4.5:1, inclusive em elemento decorativo. Se não passou no verificador, é erro, não escolha estética.
- `--rule` é para fio, nunca para texto nem para elemento clicável. `--accent` nunca é cor de texto: é massa, com `--ink` por cima quando há texto (16.21:1).
- Uso do acento: `.part`, barra do `.crit`, `.hl` e a faixa `.accent-bar` de 8px que abre o bloco de fecho.
- **Acento só em área sem imagem.** O ouro das imagens do primeiro case (estimado perto de #FFC800) divide a tela com o amarelo e o acento deixa de marcar. Pior: dois amarelos juntos leem-se como do mesmo autor, e um case cujo ponto é separar decisão própria de material herdado não pode borrar essa linha.
- Exceção que existe no ar: a marca manuscrita `.shot-x` (um X em SVG, `#FFFF00`) sobre os recortes ampliados das amostras 1 e 2 do primeiro case. É a única ocorrência de acento sobre imagem.

### Tipografia

Archivo (Google Fonts, pesos 400, 500 e 600 carregados), com fallback Helvetica Neue, Helvetica, Arial, sans-serif. Uma família só. A única exceção é o bloco de prompt, descrito abaixo.

| Peso | Nome | Trabalho |
| --- | --- | --- |
| 400 | Regular | leitura contínua, notas, legendas |
| 500 | Medium | rótulo em caixa alta, subtítulo, cabeçalho de tabela, `strong` |
| 600 | SemiBold | título de página e de seção |

Não usar 700: em redução a 25% o Bold fecha as contraformas de a, e e o, e o SemiBold mantém abertas. É critério verificável, não preferência.

Seis degraus, entrelinha em valor absoluto, não em múltiplo:

| Degrau | Tamanho / entrelinha | Peso | Tracking | Onde |
| --- | --- | --- | --- | --- |
| 01 | 76 / 72 | 600 | -0.03em | título da página, título de divisor (`.part .tt`) |
| 02 | 44 / 48 | 600 | -0.02em | título de seção (`.sec-title`), numeral de sequência (`.seq .n`) |
| 03 | 26 / 34 | 500 | -0.01em | subtítulo (`.lvl`, `h3`), frase de corte (`.pull`), título de item (`.item-t`, `.crit .head`) |
| 03 | 26 / 34 | 400 | -0.01em | abertura sob o título da página (`.lede`) |
| 04 | 17 / 30 | 400 | normal | corpo |
| 05 | 14 / 16 | 500 | 0.14em, caixa alta | rótulo, numeral de seção, rótulo de imagem, cabeçalho de tabela |
| 06 | 11 / 16 | 400 | normal | nota, legenda |

O corpo é 17/30, não 17/28: em medida de 496px, 28 aperta a mancha densa do Archivo. O rótulo é um valor só, 14px com 0.14em; os dois valores que conviviam (13px com 0.12em) acabaram. Os valores abaixo de 900px estão em Responsivo.

**Fora dos seis degraus**, como está no CSS:

- assinatura: 20/24, "Ruan" em 600 e "Rocha" em 400; no fecho 32/38
- citação (`.quote`): 21/30
- descrição de item (`.item-d`): 17/28
- índice: título de parte 16/22 em 500, link 15/22, numeral 13/22 em 500 com 0.12em
- rótulo de divisor (`.part .lb`): 14/18

**A exceção de família: o bloco de prompt.** Texto citado de uma máquina entra em `.prompt`, recolhido por padrão, sem animação na abertura. O `<pre>` usa a pilha monoespaçada do sistema (`ui-monospace`, `SFMono-Regular`, `"SF Mono"`, `Menlo`, `Consolas`, `"Liberation Mono"`, `monospace`) em 14/22, peso 400, `--ink-2` sobre `--well`, com 24px de padding e largura máxima de 720px. Marca mudança de locutor, não mudança de estilo.

### Grade e espaçamento

Módulo base 8px. Todo espaçamento vertical é múltiplo de 8. Espaço vem de módulo, nunca de estimativa.

| | Valor |
| --- | --- |
| Colunas | 12 |
| Largura de coluna | 80px |
| Calha | 24px |
| Container | 1224px |
| Margem lateral | 64px a partir de 1352px; 40px de 900 a 1351px; 20px abaixo de 900px |

Doze é o único número abaixo de 24 divisível por 3 e por 4, e o case pede as duas divisões: três imagens em linha numa seção e quatro em outra, sobre a mesma estrutura. Abaixo de 1352px as colunas ficam fluidas e o container passa a 100%. A grade é guia de construção e nunca aparece como elemento gráfico.

**Faixas de uso**

| Classe | Colunas | Largura | O que ocupa |
| --- | --- | --- | --- |
| `.span-label` | 1 a 2 | 184px | numeral de seção, notas laterais |
| `.span-text` e `.span-half-a` | 3 a 7 | 496px | texto corrido |
| `.span-half-b` | 8 a 12 | 496px | segundo bloco de uma metade |
| `.span-wide` | 3 a 12 | 1016px | título de seção, tabela, sequência e lista com régua |
| `.span-full` | 1 a 12 | 1224px | imagens governantes, divisor de parte, faixa de acento do fecho |

O título de seção em `.span-wide` tem `max-width` de 904px. Alinhamento à esquerda como padrão; a única peça centralizada hoje é a peça final (`.final`). A faixa 1 a 2 fica vazia na maior parte da página, e isso é intencional: é a parede quase vazia que separa espaço construído de sobra.

**Espaçamento vertical**

| Entre | Desktop | Abaixo de 900px |
| --- | --- | --- |
| Topo da página e assinatura | 120px | 72px |
| Rótulo de data e título da página | 56px | 40px |
| Título da página e abertura (`.lede`) | 24px | 24px |
| Fim do cabeçalho e primeira seção | 96px | 64px |
| Seção e seção | 96px | 64px |
| Numeral e título de seção | lado a lado | 12px |
| Título de seção e primeiro parágrafo | 40px | 24px |
| Parágrafo e parágrafo (`.stack`) | 24px | 24px |
| Texto e bloco de imagem, e imagem e texto seguinte | 48px | 48px |
| Imagem e `figcaption` | 16px | 16px |
| Rótulo e legenda | 8px | 8px |
| Linha de imagens e linha de imagens (`.row + .row`) | 32px | 32px |
| Última seção e bloco de fecho | 96px | 64px |
| Faixa de acento e conteúdo do fecho | 48px | 48px |
| Fim do fecho (padding inferior) | 120px | 120px |

**Medida de texto.** O corpo tem 496px de medida (colunas 3 a 7), cerca de 60 caracteres por linha em Archivo. Nenhum parágrafo de corpo passa disso, mesmo quando a seção ocupa faixa maior. Têm medida própria `.lede`, `.pull` e `.prompt` (720px) e o texto da lista de cases da home (62ch).

### Imagem

Imagem que é o argumento entra inteira, sem recorte, e o enquadramento que ela tem é dado do case, não defeito a corrigir. Por isso a caixa usa `contain`, nunca `cover`.

**Caixa (`.shot`).** Proporção 3:4, ou 16:9 em `.shot-wide`. `object-fit: contain`, fundo `--bg`, fio de 1px `--rule`, canto reto, sem sombra, sem placa nem cartão. O fio é uniforme em todas as imagens: uma peça sobre fundo branco dissolveria no papel da página sem ele, e fio só em algumas viraria exceção.

**Rótulo e legenda.** Ficam juntos no `<figcaption>`, abaixo da imagem, a 16px dela. O rótulo (`.label.cap-label`, degrau 05, `--ink-3`, caixa alta) diz o que a imagem é; a legenda (`.note`, degrau 06, `--ink-2`, caixa normal, no máximo duas linhas) diz o que olhar. A fileira de peças de 2017, a marca, os recortes e a peça final são legendados por `.note`, e só parte delas leva rótulo.

**Recorte ampliado.** Quando o argumento depende de detalhe que não sobrevive à escala (numa linha de quatro imagens, cada uma tem 288px de largura), a seção ganha uma segunda linha com recortes do arquivo original: `.row-4.scroller.crops`, caixa 16:9 (`.shot-wide`, cerca de 162px de altura em 288px de largura), mesma borda, e a legenda declara o que se vê. Sem o recorte, a afirmação sobre o detalhe fica inverificável pelo leitor.

**Peças de proporções diferentes (`.strip-2017`).** Fileira de altura fixa de 400px, largura variável (`width:auto`), alinhada pela base, com fio de 1px `--rule`. Caixas iguais distorceriam a escala relativa entre as peças. A marca do projeto sai da fileira: `.brand-mark`, 280px de altura, 48px abaixo, porque é a identidade do projeto, não uma peça da campanha.

**Peça final (`.final`).** Uma imagem, centralizada, `max-height:720px`, com legenda em 720px de largura máxima.

**Marcas manuscritas.** `.shot-x` coloca um SVG centralizado sobre a caixa (46% da largura). `.arrow-host` com `.mk-arrow` põe uma seta em `--ink` entre colunas (64px, some abaixo de 900px). Os dois SVGs levam `aria-hidden="true"`.

**Formato e peso.** JPEG com qualidade 82, lado maior de até 1200px (recortes em 900 por 505, peça final em 765 por 1070). Cada arquivo pesa de 53 KB a 214 KB; as 18 imagens do primeiro case somam cerca de 2.27 MB. Sem `srcset`, sem PNG. Todo alt descreve o que se vê (regra em Acessibilidade).

### Responsivo

| Faixa | Largura | Grade | Margem |
| --- | --- | --- | --- |
| Desktop | a partir de 1352px | 12 colunas, container 1224px | 64px |
| Intermediária | 900 a 1351px | 12 colunas fluidas, container 100% | 40px |
| Estreita | abaixo de 900px | coluna única | 20px |

Os pontos de quebra no CSS são `max-width:1351px` e `max-width:899px`. As margens respeitam `env(safe-area-inset-*)`. Abaixo de 900px todas as faixas de uso passam a ocupar as 12 colunas.

**Escala abaixo de 900px**

| Degrau | Desktop | Estreito |
| --- | --- | --- |
| 01 | 76/72 | 44/44 |
| 02 | 44/48 | 32/36 |
| 03 | 26/34 | 21/28 |
| 04 | 17/30 | 17/28 |
| 05 | 14/16 | 13/16 |
| 06 | 11/16 | 11/16 |

O corpo volta a 17/28 porque a medida encurta e a entrelinha generosa deixa de ser necessária. Só `.label` cai para 13px (o tracking continua 0.14em); cabeçalho de tabela e `.part .lb` ficam em 14px. Também mudam: assinatura do fecho 26/32, `.item-t` e `.crit .head` 21/28, `.seq .n` 32/36, `.part .tt` 44/44, `.quote` 19/28.

**A regra que não pode quebrar: comparação não empilha.** Com `.scroller`, `.row-3` e `.row-4` viram tira de rolagem horizontal: colunas automáticas de 78% (88% em `.crops`), gap de 16px, `scroll-snap-type: x mandatory` com alinhamento no início, sangrando até a borda da tela. A próxima imagem fica parcialmente visível e é esse o indicador. Sem seta, sem ponto, sem instrução escrita. Linha sem `.scroller` empilha em coluna única. A fileira de 2017 segue a mesma lógica (nowrap, snap, altura de 300px) e a marca passa a largura total.

**Outros ajustes.** `.part` com padding de 40px 24px e sem altura mínima; `.crit .body` com padding de 24px; `.seq` com gap de 20px; índice em coluna única; botão de topo a 16px das bordas; `.mk-arrow` some. Tabelas ficam dentro de `.table-scroll` (`min-width:520px`, rolagem horizontal), com o corpo em 17px. Com `prefers-reduced-motion: reduce`, animação, transição e rolagem suave são desligadas.

### Favicon

Quadrado em `--ink` (#1A1A1A), com a letra R em Archivo 600, cor `--bg` (#F7F6F3), centralizada, ocupando cerca de 60% da altura. Em tamanho de favicon a assinatura de duas linhas não se lê, então vai só a inicial.

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

Formato: **o que foi decidido** → o que aconteceu ao executar → o que vale agora.

Todas as linhas abaixo vêm da migração do briefing do primeiro case (06/11/2026), conferida contra `assets/css/site.css` e contra o HTML do case.

- **Subtítulo de abertura (`.lede`) em 500, como o degrau 03** → o CSS usa 400 → vale 400; o 500 fica em `.lvl`, `h3`, `.pull` e títulos de item.
- **Faixa das colunas 3 a 12 com 904px** → dez colunas de 80px com nove calhas de 24px somam 1016px; 904px é o `max-width` do título de seção → vale 1016px em `.span-wide` e 904px só no título.
- **Título de seção a 24px do primeiro parágrafo** → o CSS dá 40px (24px só abaixo de 900px) → vale 40px.
- **Topo da página a 120px do título** → os 120px vão até a assinatura, e o título fica 56px abaixo do rótulo de data → vale 120px e 56px (72px e 40px abaixo de 900px).
- **Última seção a 120px do fecho** → o espaço é o padding da seção, 96px; os 120px estão abaixo do fecho → vale 96px acima e 120px abaixo.
- **Nenhum parágrafo de texto corrido passa de 496px** → `.lede`, `.pull` e `.prompt` usam 720px → vale 496px para corpo e 720px para esses três.
- **Rótulo acima da imagem, e nenhuma imagem sem rótulo** → o rótulo está no `figcaption`, abaixo da imagem, e a fileira de 2017, os recortes e a peça final levam só legenda → vale o que está no HTML.
- **Recorte ampliado com 160px de altura** → o CSS dá só a proporção 16:9, e os 160px são consequência da coluna de 288px → vale 16:9, sem altura fixa.
- **Fileira de 2017 com 320px e marca com 160px** → o CSS dá 400px e 280px → vale 400px e 280px.
- **PNG para as peças de 2017, JPEG com qualidade 85 para as saídas do modelo, largura máxima de 1600px, `srcset` de 800 e 1600** → todos os arquivos são JPEG com qualidade 82, lado maior de 1200px, sem `srcset` → vale o que está no ar.
- **Fileira de 2017 empilha abaixo de 900px** → virou tira de rolagem horizontal → vale a tira.
- **Tabelas com corpo em 15px abaixo de 900px** → o corpo continua em 17px e a tabela rola a partir de 520px de largura → vale o CSS.
- **Seis degraus tipográficos e nenhum tamanho fora deles** → o CSS tem tamanhos próprios para assinatura, citação, descrição de item, índice e rótulo de divisor → vale a lista "Fora dos seis degraus".
- **Não alternar peso dentro da mesma frase** → `strong` em 500 aparece seis vezes no corpo do case → vale `strong` em 500 como único realce de peso no corpo.
- **Barra de marcação de 3px em `--ink`, em três lugares** → `.mark` existe no CSS e nenhuma página o usa; o papel ficou com `.crit` e `.hl` → vale a tabela de componentes; `.mark` fica fora dela.
- **Acento fora de qualquer seção com imagem** → o amarelo de `.hl`, `.crit` e `.part` convive com imagens na mesma seção, e o X de `.shot-x` fica sobre dois recortes → vale "acento só em área sem imagem", com `.shot-x` como a única exceção.

## Pendências conhecidas

- **O texto da home não está escrito.** A estrutura existe; o texto de posicionamento vem do documento de marca e não deve ser inventado aqui.
- **Favicon decidido, ainda não aplicado.** Nenhuma página tem `<link rel="icon">` e não há arquivo de favicon em `assets/`.
- **Resto do briefing do primeiro case.** O detalhe visual foi migrado para este arquivo. Falta mandar "O que a página comunica e o que evita" e "Testes de aprovação" para o documento de marca, e aposentar "Mapa de slots de imagem", "Estrutura da página" e "A marca na página", que descrevem uma página que agora existe aqui.
- **Documento de marca.** Repete valores que vivem aqui (escala, medida, paleta, grade, faixas de uso, favicon) e passa a apontar para este arquivo. Também descreve a página do case de um jeito que o ar contradiz: rótulo de imagem acima, faixa de 904px e acento proibido em qualquer seção com imagem.

### Em aberto, não trava nada

- hex real do ouro das peças do primeiro case, hoje estimado em tela por volta de #FFC800
- hex real do laranja institucional

Os dois afetam só a regra de restrição do acento amarelo.
