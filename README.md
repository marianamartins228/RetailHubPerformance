<p align="center">
  <img src="https://github.com/user-attachments/assets/3be595b7-e8f7-412b-95f2-15cfdc645eab" width="500"/>
</p>

# Retail Hub - Análise de Performance no Varejo

Este projeto foi desenvolvido em Power BI a partir de um case técnico com foco na análise de vendas no varejo. A base de dados, inspirada na estrutura do Adventure Works, foi adaptada para um cenário internacional, permitindo a análise de diferentes regiões e canais de venda.
O objetivo foi construir um dashboard capaz de apoiar a tomada de decisão por meio da análise integrada de indicadores financeiros, comportamentais e operacionais, como vendas, margem bruta, ticket médio, perfil de clientes e desempenho de entregas.

---

## Premissas do projeto

O desenvolvimento seguiu os seguintes requisitos:

- Relatório desenvolvido em inglês;
- Layout em resolução FHD (1920x1080);
- Navegação entre páginas por meio de botões;
- Exibição de valores em moeda local e em dólar;
- Implementação de controle de acesso por região (Row-Level Security), em que os times de North America, Europe e Australia visualizam apenas seus dados, enquanto o time global possui acesso completo;
- Utilização de pelo menos uma tooltip personalizada;
- Construção de ao menos um gráfico de Pareto.

---

## Preparação e Modelagem dos Dados

Os dados foram estruturados seguindo boas práticas de modelagem dimensional, com separação entre tabelas fato e dimensão. As tabelas de vendas foram consolidadas em uma única fact table, permitindo atualização automatizada conforme novos períodos são adicionados ao modelo.

Principais etapas realizadas:

- Padronização de formatos numéricos (preços, custos e taxa de câmbio);  
- Validação de consistência dos dados;
- Tratamento de valores nulos;
- Verificação de duplicidade em chaves primárias;  
- Análise de outliers com apoio do perfil de colunas.  

Também foi criada uma tabela calendário para suporte às análises temporais, e os relacionamentos foram definidos no padrão estrela (*star schema*).

<img width="1261" height="727" alt="image" src="https://github.com/user-attachments/assets/93cdef0b-8bd3-43a0-b5be-927133f73aba" />

---

## Análise Exploratória dos Dados (EDA)

A análise exploratória permitiu identificar características importantes da base:

- O canal online é tratado como uma única loja, diferentemente das lojas físicas  
- A presença das colunas *Unit Price* e *Net Price* indica a aplicação de descontos  
- Os valores estão originalmente em dólar, com possibilidade de conversão para moeda local via taxa de câmbio  

Essas observações orientaram a construção das métricas e das análises do dashboard.

---

## Funcionalidades do Dashboard

O dashboard foi desenvolvido com foco em interatividade e usabilidade:

- Segmentação dinâmica de moeda (Local vs USD);
- Navegação entre páginas por botões;  
- Menu de filtros oculto acionado por botão;

<img width="200" alt="image" src="https://github.com/user-attachments/assets/49f1236b-003d-4099-8875-f80e86af4ba4" />

  
- Tooltip personalizada para detalhamento de variáveis;

<img width="200" alt="image" src="https://github.com/user-attachments/assets/1edf4bb2-617a-4e41-b3c2-7dea99b9cc8c" />
  
- Drill-through para análise detalhada de vendas;

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/b2c6dc48-1e35-43d0-a8d3-b133a829c1ee" />

  
- Gráfico de Pareto para identificação das principais subcategorias;
- Row-Level Security (RLS) por região utilizando o recurso de Gerenciar Funções.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/33997691-07a1-4e9d-afd5-125d0ce20e76" />

---

## Principais Insights

### Performance de Vendas
- Foram identificadas quedas relevantes nas vendas nos meses de abril de 2018 e 2019, indicando a necessidade de validação com a área de negócio para confirmar se o comportamento é sazonal ou decorrente de inconsistências na base;

<img width="400" alt="image" src="https://github.com/user-attachments/assets/4125a8de-4cdf-49ec-a0ae-63c4e4761663" />

- O canal online representa aproximadamente metade do faturamento total, evidenciando sua relevância estratégica no resultado consolidado;

<img width="400" height="356" alt="image" src="https://github.com/user-attachments/assets/78291501-2d29-4229-9dd6-3e432370700c" />

  
- Em determinados períodos, observou-se crescimento de vendas acompanhado de redução de margem, sugerindo impacto direto do aumento de descontos sobre a rentabilidade.

<img width="400" height="422" alt="image" src="https://github.com/user-attachments/assets/70eec955-8a5b-427d-acbb-d65a47b7b0bb" />
  

### Mix de Produtos
- A análise de Pareto mostrou que cerca de 10 subcategorias (de um total de 32) concentram quase 80% das vendas;  
- Entre essas subcategorias, há predominância de produtos tecnológicos, possivelmente associada ao maior valor agregado desses itens ou à sua relevância no consumo atual.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/2bf9b6de-7362-4c89-ae7a-28bc7eea5f3f" />


### Comportamento dos Clientes
- A base apresenta distribuição equilibrada entre gêneros, sem diferenças significativas de volume;  
- A maior geração de receita está concentrada em clientes a partir dos 51 anos, indicando oportunidades tanto de aprofundamento nesse público quanto de estratégias para atração de consumidores mais jovens;

<img width="400" alt="image" src="https://github.com/user-attachments/assets/7d33a42a-c9f1-45dc-b5e4-bac08625e947" />


- Observa-se volume ligeiramente maior de concessão de descontos para clientes do gênero masculino;  
- A proximidade entre o ticket médio por pedido e por cliente sugere baixa recorrência de compras, indicando potencial oportunidade de atuação em retenção e fidelização.

<img width="300" alt="image" src="https://github.com/user-attachments/assets/35f66228-deed-48b2-b1d3-edb02778664e" />


### Performance por Região
- O ticket médio por cliente não apresenta relação direta com o volume de vendas entre os países;  
- Em alguns mercados, o crescimento parece estar mais associado ao aumento da base de clientes do que ao valor médio gasto, indicando caminhos distintos para estratégias comerciais e de marketing.

<img width="400" alt="image" src="https://github.com/user-attachments/assets/49d548e8-07b0-4c56-b317-b9189d6c3a94" />


### Operações e Entregas
- Na ausência de data estimada de entrega, foi adotado um prazo médio de 2 dias como referência para análise de atraso;  
- Observa-se uma piora histórica no nível de entregas fora do prazo, com leve recuperação a partir de 2020;

<img width="350" alt="image" src="https://github.com/user-attachments/assets/f9335e0a-9b7f-40c5-974c-21c97ba13c24" />
  
- Produtos tecnológicos apresentam maior incidência de atraso, o que pode indicar gargalos específicos na cadeia de suprimentos;  
- O volume de entregas oscila ao longo da semana, sugerindo possíveis ineficiências operacionais ou detalhes de negócio que merecem investigação.
---
## Conclusão

Este projeto demonstra a aplicação de modelagem de dados, análise exploratória e construção de dashboards orientados ao negócio.

A análise permitiu identificar oportunidades relacionadas a:

- Estratégia de descontos  
- Retenção de clientes  
- Eficiência operacional  
- Otimização do mix de produtos  

Link do Dashboard: https://app.powerbi.com/links/itk4NS8uxE?ctid=659ce2b8-0714-4198-8c38-dc9b60aabb57&pbi_source=linkShare&bookmarkGuid=733f4461-6098-4d2a-84a6-704bbb32b63b






