# CaseSalesOverview2026

Projeto em Power BI desenvolvido a partir de um case técnico, com foco na análise de vendas no varejo. A base de dados, inspirada na estrutura do Adventure Works, foi adaptada para uma análise internacional com um painel voltado ao acesso de filiais nacionais e internacionais.
Por se tratar do segmento de varejo, a análise foi direcionada ao acompanhamento de métricas-chave como vendas, margem, ticket médio e comportamento de compra dos clientes. Além disso, foram considerados indicadores operacionais, como desempenho de entregas e eficiência logística, permitindo uma visão integrada do negócio e suporte à tomada de decisão estratégica.

## Premissas e orientações do projeto

Para o desenvolvimento deste projeto, foram considerados os seguintes requisitos propostos pelo Case:

- Relatório desenvolvido em inglês;
- Layout em resolução FHD (1920x1080);
- Navegação entre páginas por meio de botões;
- Aplicação de tema personalizado;
- Exibição de valores em moeda local e em dólar;
- Implementação de controle de acesso por região (Row-Level Security), em que os times de North America, Europe e Australia visualizam apenas seus dados, enquanto o time global possui acesso completo;
- Utilização de pelo menos uma tooltip personalizada;
- Construção de ao menos um gráfico de Pareto;

## Leitura + Limpeza & Preparação dos Dados

Inicialmente, foi realizada a organização das tabelas em dois grupos: **dimensão** e **fato**, seguindo boas práticas de modelagem dimensional.
As tabelas de dimensão foram importadas individualmente, enquanto as tabelas de vendas (fato) foram combinadas em uma única tabela. Essa abordagem permite a atualização automatizada dos dados conforme novos períodos (anos) são adicionados à análise.
Em seguida, foi realizada a validação dos tipos de dados e a análise de qualidade das colunas.

- Padronização de valores numéricos: as colunas *Unit Price*, *Net Price*, *Unit Cost* e *Exchange Rate* estavam no formato decimal americano (ponto como separador). Foi realizada a substituição para o padrão local antes da conversão para número decimal;
- Verificação de consistência: não foram identificados erros ou valores ausentes relevantes.
- Tratamento de valores nulos na coluna *Status*, substituídos por "Active", considerando que representam lojas sem registro de fechamento;
- Validação de consistência dos campos *Square Meters* e *Close Date*;
- Verificação de duplicidade em chaves primárias;
- Análise de outliers utilizando o recurso de perfil de coluna.

### Modelagem

- Criação da tabela calendário para suporte às análises temporais;
- Definição dos relacionamentos entre tabelas, estruturando o modelo no padrão estrela (star schema).
<img width="1101" height="747" alt="image" src="https://github.com/user-attachments/assets/9d578957-9d83-4e5b-a621-9b98688d15b9" />

## Análise Exploratória (EDA)

A partir da exploração dos dados, algumas informações se fazem notar:

- O segmento online é tratado como uma única StoreKey, diferentemente das demais lojas que estão segmentadas por país, estado e loja;
- A existência de uma coluna Unit Price e uma coluna Net Price evidencia a possível existência de descontos nas venda;
- Cada preço vem em dólar, sendo possível a conversão para a moeda local a partir da coluna Exchange Rate;

## Recursos e funcionalidades implementadas ao Dashboard

- Segmentação dinâmica de moeda que permite os usuários de diferentes regiões optarem por navegar no dashboard a partir da moeda local ou em dólar:

<img width="373" height="107" alt="image" src="https://github.com/user-attachments/assets/2b488a05-6eef-4be8-82e6-cea260a669b9" />

- Navegação entre as páginas através de botões;
- Menu de filtros oculto acionável por meio de botão;

<img width="380" height="776" alt="image" src="https://github.com/user-attachments/assets/d4bd952d-0eb4-4cce-8df8-a45e28076ea3" />

- Tooltip personalizada para explicar as variáveis Subcategory e Country:

<img width="865" height="362" alt="image" src="https://github.com/user-attachments/assets/0b47d2df-70ca-433e-93a5-255a14d6da32" />

<img width="660" height="323" alt="image" src="https://github.com/user-attachments/assets/6c8c52c9-fddb-4bc4-9b9a-de521be81e22" />

- Detalhamento da variável Sales a partir do recurso DrillThrough;

<img width="1471" height="408" alt="image" src="https://github.com/user-attachments/assets/196bbd81-31bd-4498-aa3a-52d23d69b466" />

- Diagrama de Pareto para identificar as subcategorias responsáveis por quase 80% das vendas;

## Insights obtidos e análise de negócio
- As vendas no mês de abril de 2018 e 2019 sofrem queda significante sendo necessário verificar com a área de negócio se isso realmente ocorre ou se pode ser alguma inconsistência no banco de dados.
- O faturamento da loja online é responsável por metade do faturamento total do grupo.
- O gráfico de Vendas versus Margem produz oportunidade de analisar porque em alguns períodos houve aumento do faturamento e queda da margem. Ao utilizar a segmentação não foi identificada relação com a localidade, mas o card de % Desconto sobre as Vendas notou-se um aumento desse percentual nos períodos em que as vendas subiram e a margem não acompanhou.
- O Diagrama de Pareto que trata do volume de vendas por subcategoria revela que dentra as 32 subcategorias, apenas 10 são responsáveis por quase 80% das vendas e olhando para essas categorias observa-se a predominância de artigos tecnológicos, seja pelo maior valor agregado desses produtos ou realmente o momento que vivemos, onde ter os melhores aparelhos é necessário para conexão.
- Os consumidores estão quase igualmente divididos em relação ao gênero, porém a faixa etária que mais gera receita é mais longeva (de 51 a 65 anos), destacando uma oportunidade para criar incentivos específicos para esses clientes ou novas iniciativas para conquistar os clientes mais jovens.
- Na comparação por gênero do percentual de clientes com desconto é possível notar que o volume é ligeiramente maior para os homens, ainda que exista quase igualdade de população por gênero.
- Os cards de Ticket médio por pedido e Ticket médio por cliente com valores próximos revela que os clientes em média não retornam para comprar novamente, o que é algo a ser investigado pelo time comercial, já que o segmento varejo oferece variabilidade de produtos e um cliente poderia consumir produtos de variadas categorias.
- O ticket médio por cliente em cada país não é proporcional ao volume de vendas, o que pode revelar que os países que vendem mais em média precisam "trazer" mais clientes para que consigam chegar a essa superioridade. As estratégias de marketing para os países que tem baixo faturamento podem ser direcionadas nesse sentido.
- A base de dados não possui coluna com data estimada de entrega, então para fins de análise foi considerado o tempo médio de 2 dias. Com base nesse ponto de corte identifica-se historicamente houve uma piora em relação ao número de pedidos entregues com atraso, com uma leve recuperação a partir de 2020.
- Nos pedidos entregues com atraso também existe predominância de artigos tecnológicos, talvez um gargalo na cadeia de suprimentos tecnológicos? Algo que precisa ser visitado pelo time de logística.
- O gráfico de volume de entregas por dia da semana também ajuda a identificar dias em que a produtividade é menor. Analisando de forma geral observa-se que existe um escalonamento da quantidade de entregas conforme a semana avança, tendo uma queda significativa na sexta-feira e retomando a força no sábado. Porque isso acontece? É importante verificar como funciona a cadência e processo de entregas.

<img width="516" height="372" alt="image" src="https://github.com/user-attachments/assets/3048af5b-a801-487e-bb61-d80400897264" />







