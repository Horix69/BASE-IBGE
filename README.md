# Observatório de Dados Públicos — protótipo v0.1

Portal estático em HTML/CSS/JavaScript criado a partir da auditoria dos arquivos `censobr-main.zip` e `microdadosBrasil-master.zip` enviados pelo usuário.

## O que funciona nesta versão
- Página inicial responsiva.
- Catálogo pesquisável e filtrável com 17 entradas: 11 famílias de bases documentadas em `microdadosBrasil` e seis funções/conjuntos do `censobr`.
- Links para os repositórios originais.
- Seção de pesquisa urbana e painel geográfico demonstrativo, claramente marcado como em preparação.
- Nota metodológica separando metadados/código de microdados efetivamente processados.
- Funciona como site estático; não requer backend para esta fase.

## Limitações importantes
- **Nenhum microdado de Censo, PNAD ou PNAD Contínua foi processado nesta versão.** O catálogo deriva dos metadados e documentação presentes nos ZIPs.
- A única referência a um arquivo de microdados em `censobr` encontrado no ZIP foi um ZIP identificado como `microdata_2022_controlado_fake.zip`; ele não é uma base nacional real apropriada para indicadores do portal.
- Os períodos exibidos para `microdadosBrasil` refletem a cobertura dos metadados presentes no pacote, não uma verificação de que os arquivos originais ainda estão acessíveis ou de que todas as rotinas executam em ambiente atual.
- A documentação atual do `censobr` e a do pacote histórico `microdadosBrasil` têm escopos distintos; a cobertura deve ser conferida para cada conjunto antes de publicar séries.
- O ambiente usado para esta auditoria não tem R instalado, portanto os pacotes R não foram executados nem suas dependências instaladas.

## Rodar localmente
Abra `index.html` em um navegador. Como o catálogo está embutido em `catalog.js`, a busca funciona sem servidor local.

## Publicar online — GitHub Pages
1. Crie um repositório no GitHub.
2. Envie `index.html`, `styles.css`, `app.js`, `catalog.js` e a pasta `data/`.
3. Em **Settings → Pages**, selecione a branch principal e a pasta raiz (`/root`).
4. Salve e aguarde o GitHub publicar o endereço do site.

Para domínio próprio, configure-o posteriormente em Pages/DNS.

## Arquitetura recomendada para a versão com indicadores reais
- ETL e validação: R (`censobr`, `survey`, `arrow`, `dplyr`) ou Python quando fizer sentido.
- Armazenamento analítico: Parquet + DuckDB para agregados e dados consultados frequentemente.
- Camada web: frontend estático consumindo JSON/CSV agregados ou API pequena quando houver necessidade de consultas dinâmicas.
- Geografia: geometrias oficiais e tabelas de correspondência com código territorial, mantendo a versão da malha e o ano de referência.
- Privacidade: publicar apenas agregados adequados; não disponibilizar microdados identificáveis ou dados sujeitos a restrições.

## Próxima prova de conceito sugerida
Começar com uma tabela agregada de população e domicílios do Censo para municípios, com ano, código IBGE, indicador, valor, unidade, fonte, método e data de processamento. Validar o fluxo antes de expandir para PNAD Contínua, RAIS/CAGED e demais bases.
