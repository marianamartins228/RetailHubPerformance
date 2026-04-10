# CaseSalesOverview2026

Projeto em Power BI desenvolvido a partir de um case técnico, com foco na análise de vendas no varejo. A base de dados, inspirada na estrutura do Adventure Works, foi adaptada para uma análise internacional com um painel voltado ao acesso de filiais nacionais e internacionais.
Por se tratar do segmento de varejo, a análise foi direcionada ao acompanhamento de métricas-chave como faturamento, margem, volume de vendas, ticket médio e comportamento de compra dos clientes. Além disso, foram considerados indicadores operacionais, como desempenho de entregas e eficiência logística, permitindo uma visão integrada do negócio e suporte à tomada de decisão estratégica.

## Premissas e orientações do projeto

Para o desenvolvimento deste projeto, foram consideradas as seguintes premissas:

- Relatório desenvolvido em inglês;
- Layout em resolução FHD (1920x1080);
- Navegação entre páginas por meio de botões;
- Aplicação de tema personalizado;
- Exibição de valores em moeda local e em dólar;
- Implementação de controle de acesso por região (Row-Level Security), em que os times de North America, Europe e Australia visualizam apenas seus dados, enquanto o time global possui acesso completo;
- Utilização de pelo menos uma tooltip personalizada;
- Construção de ao menos um gráfico de Pareto;
- Aplicação de análise Top N, com agrupamento dos demais elementos na categoria "Outros".

## Leitura & Exploração Inicial + Limpeza & Preparação dos Dados
Inicialmente, foi realizada a organização das tabelas em dois grupos: **dimensão** e **fato**, seguindo boas práticas de modelagem dimensional.
As tabelas de dimensão foram importadas individualmente, enquanto as tabelas de vendas (fato) foram combinadas em uma única tabela. Essa abordagem permite a atualização automatizada dos dados conforme novos períodos (anos) são adicionados à análise.
Em seguida, foi realizada a validação dos tipos de dados e a análise de qualidade das colunas.
### Fact Sales
- Ajuste no formato de datas: devido a inconsistências na conversão direta para `date`, foi necessário converter inicialmente para `datetime` e, posteriormente, para `date`;
- Padronização de valores numéricos: as colunas *Unit Price*, *Net Price*, *Unit Cost* e *Exchange Rate* estavam no formato decimal americano (ponto como separador). Foi realizada a substituição para o padrão local antes da conversão para número decimal;
- Verificação de consistência: não foram identificados erros ou valores ausentes relevantes.
### Customers
- Ajuste no formato de datas, conforme realizado na tabela de vendas.
### Products
- Adequação dos tipos de dados (texto e número decimal) conforme necessidade.
### Stores
- Ajuste no formato de datas;
- Tratamento de valores nulos na coluna *Status*, substituídos por "Active", considerando que representam lojas sem registro de fechamento;
- Validação de consistência dos campos *Square Meters* e *Close Date*;
- Verificação de duplicidade em chaves primárias;
- Análise de outliers utilizando o recurso de perfil de coluna.
### Modelagem
- Criação da tabela calendário para suporte às análises temporais;
- Definição dos relacionamentos entre tabelas, estruturando o modelo no padrão estrela (star schema).
<img width="1101" height="747" alt="image" src="https://github.com/user-attachments/assets/9d578957-9d83-4e5b-a621-9b98688d15b9" />

## Análise Exploratória (EDA)

## Insights obtidos e análise de negócio
