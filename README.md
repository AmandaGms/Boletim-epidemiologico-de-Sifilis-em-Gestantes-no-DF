# Boletim Epidemiológico — Sífilis em Gestantes no Distrito Federal (2015–2024)

## Sobre o projeto

Este repositório contém os códigos, dados e documentos utilizados na elaboração do Boletim Epidemiológico de Sífilis em Gestantes no Distrito Federal, referente ao período de 2015 a 2024.

O projeto foi desenvolvido no âmbito do Programa de Residência Multiprofissional em Vigilância em Saúde da Fiocruz Brasília, como atividade voltada à aplicação dos princípios de ciência aberta e reprodutibilidade na vigilância em saúde.

O boletim foi desenvolvido utilizando a linguagem R e o R Markdown, permitindo integrar o processamento dos dados, as análises epidemiológicas, os textos interpretativos e as visualizações interativas em um documento dinâmico no formato HTML.

## Objetivo

Descrever o perfil epidemiológico, clínico e laboratorial da sífilis em gestantes no Distrito Federal entre 2015 e 2024, de modo a identificar lacunas assistenciais que possam orientar os profissionais de saúde e fortalecer as ações de vigilância e atenção à saúde da gestante.

## Fonte dos dados

Foram utilizados dados secundários de domínio público provenientes dos sistemas de informação em saúde do Ministério da Saúde, disponibilizados pelo DATASUS.

| Fonte | Arquivos | Descrição |
|---|---|---|
| SINAN | SIFGBR15.dbc a SIFGBR24.dbc | Microdados de sífilis em gestantes |
| SINASC | nascidos_vivos.xlsx | Quantitativo anual de nascidos vivos |
| DATASUS | MUNICNET.DBF | Tabela auxiliar de municípios |
| DATASUS | OCUPANET.DBF | Tabela auxiliar de ocupações |

- **Período:** 2015 a 2024.
- **Recorte territorial:** Distrito Federal, segundo município de residência.
- **Data de extração dos dados:** 20/06/2026.
- **Fonte:** https://datasus.saude.gov.br/

Os arquivos de origem são armazenados localmente na pasta `arquivos_fonte`. A rotina não realiza consultas ou downloads automáticos dos bancos de dados.

## Estrutura do repositório

| Arquivo ou diretório | Descrição |
|---|---|
| `boletim-sifilis.Rproj` | Arquivo de projeto do RStudio |
| `README.md` | Documentação e instruções para reprodução |
| `arquivos_fonte/` | Bancos originais e tabelas auxiliares utilizados no processamento |
| `data/` | Base de dados tratada e processada |
| `scripts/` | Códigos de processamento, análise e geração do boletim |
| `outputs/` | Produto final em formato HTML |
| `.gitignore` | Configuração dos arquivos excluídos do versionamento |

## Descrição dos scripts

### Sifilis_processamentoII.R

Responsável pela importação, consolidação, tratamento e organização dos dados provenientes do SINAN.

As principais etapas realizadas são:

- Importação dos arquivos DBC referentes aos anos de 2015 a 2024;
- Consolidação das bases anuais;
- Seleção dos registros de residentes no Distrito Federal;
- Decodificação das variáveis conforme as categorias do sistema de informação;
- Integração com as tabelas auxiliares de municípios e ocupações;
- Construção de variáveis derivadas, incluindo faixa etária, escolaridade agrupada, ano de diagnóstico e categorias de realização dos testes diagnósticos;
- Exportação da base processada em formato XLSX.

O produto desta etapa é o arquivo `Sifilis_decodificado.xlsx`, armazenado na pasta `data`.

### boletim-sifilis-III.Rmd

Documento dinâmico responsável pela execução do processamento, análise epidemiológica, construção dos indicadores, geração de tabelas e gráficos interativos e apresentação dos resultados.

O documento executa automaticamente o script `Sifilis_processamentoII.R` por meio da função `source()`.

Dessa forma, não é necessário executar manualmente o script de processamento antes da renderização do boletim.

## Metodologia analítica

Foi realizado um estudo descritivo de série temporal, utilizando dados secundários do SINAN e do SINASC.

As análises contemplaram a distribuição temporal dos registros, o perfil epidemiológico, as características clínicas e laboratoriais e o tratamento das gestantes e de suas parcerias sexuais.

Para o cálculo da taxa de detecção, foi utilizado o número de casos por ano de diagnóstico, tendo como denominador o quantitativo de nascidos vivos do respectivo ano, multiplicado por 1.000.

Os procedimentos metodológicos detalhados e a interpretação dos resultados estão disponíveis no próprio boletim epidemiológico.

## Ferramentas e dependências

O projeto foi desenvolvido utilizando:

- Linguagem R;
- RStudio;
- R Markdown;
- Pandoc;
- HTML, CSS e JavaScript.

### Principais pacotes utilizados

| Pacote | Finalidade |
|---|---|
| pacman | Gerenciamento e carregamento de pacotes |
| read.dbc | Leitura dos arquivos DBC do DATASUS |
| foreign | Leitura dos arquivos DBF |
| dplyr | Manipulação e transformação dos dados |
| tidyr | Organização das bases de dados |
| stringr | Manipulação de dados textuais |
| openxlsx | Importação e exportação de planilhas |
| forcats | Manipulação de variáveis categóricas |
| ggplot2 | Construção de gráficos |
| ggtext | Formatação textual dos gráficos |
| ggiraph | Construção de gráficos interativos |
| gt | Construção e formatação de tabelas |
| tidytext | Processamento de dados textuais |
| wordcloud2 | Construção de nuvem de palavras |
| here | Gerenciamento dos caminhos do projeto |
| knitr | Execução dos blocos de código |
| rmarkdown | Renderização do documento dinâmico |
| remotes | Instalação de pacotes provenientes do GitHub |

As dependências complementares são instaladas e carregadas pelos próprios scripts.

## Como reproduzir o boletim

### 1. Instalar os programas necessários

Instale o R e o RStudio:

- R: https://cran.r-project.org/
- RStudio: https://posit.co/download/rstudio-desktop/

### 2. Obter o repositório

Na página do repositório no GitHub, selecione a opção **Code > Download ZIP**.

Extraia os arquivos em uma pasta de sua preferência, mantendo a estrutura original do projeto.

### 3. Abrir o projeto

Abra o arquivo `boletim-sifilis.Rproj` no RStudio.

### 4. Verificar os arquivos de origem

Certifique-se de que a pasta `arquivos_fonte` contém os arquivos DBC de sífilis em gestantes referentes ao período de 2015 a 2024, as tabelas auxiliares MUNICNET.DBF e OCUPANET.DBF e a planilha nascidos_vivos.xlsx.

Caso os arquivos não estejam disponibilizados no repositório, deverão ser obtidos nas respectivas fontes e adicionados à pasta.

### 5. Executar o boletim

Execute no console do RStudio:

```r
dir.create("outputs", showWarnings = FALSE)

rmarkdown::render(
  input = "scripts/boletim-sifilis-III.Rmd",
  output_dir = normalizePath("outputs"),
  output_file = "boletim-sifilis-III.html"
)
```

Na primeira execução, será necessária conexão com a internet para a instalação dos pacotes que ainda não estiverem disponíveis no ambiente R.

### 6. Acessar os resultados

Durante a execução do documento, serão realizadas automaticamente as seguintes etapas:

1. Instalação e carregamento das dependências;
2. Importação dos arquivos de origem;
3. Processamento dos dados;
4. Exportação da base tratada para a pasta data;
5. Importação da base processada;
6. Construção dos indicadores, tabelas e gráficos;
7. Geração do boletim epidemiológico em HTML.

O produto final estará disponível na pasta `outputs` e poderá ser aberto em um navegador de internet.

## Produto final

O boletim epidemiológico apresenta:

- Distribuição temporal dos casos e taxa de detecção;
- Perfil epidemiológico por faixa etária, raça/cor, escolaridade e ocupação;
- Idade gestacional no momento do diagnóstico;
- Classificação clínica;
- Testagem diagnóstica;
- Tratamento da parceria sexual;
- Esquema de tratamento da gestante;
- Considerações finais e recomendações para a vigilância em saúde.

[Acessar o arquivo do boletim epidemiológico](outputs/boletim-sifilis-III.html)

## Ciência aberta e reprodutibilidade

A organização deste repositório busca garantir a transparência das etapas de processamento e análise dos dados, permitindo que outros pesquisadores compreendam, reproduzam e adaptem a metodologia utilizada.

A disponibilização das bases de dados deverá respeitar as normas de privacidade e proteção de dados aplicáveis.

## Autoria

**Autoria:** Amanda Gomes dos Santos
Programa de Residência Multiprofissional em Vigilância em Saúde — Fiocruz Brasília.

2026.
