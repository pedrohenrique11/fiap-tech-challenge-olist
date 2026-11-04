# Registro de qualidade e decisões

Período analisado: 2017-01-01 a 2018-08-31 (data da compra). Base final: 96.203 pedidos entregues.

Definição de receita: soma do preço dos itens, sem frete. Dados externos: API SIDRA/IBGE (tabelas 6579 e 5938, 2018).

| tabela | problema | linhas_afetadas | decisao | justificativa |
|---|---|---|---|---|
| orders/reviews | Datas armazenadas como texto | 99441 | Convertidas para datetime | Necessário para calcular prazos, atrasos e séries mensais |
| reviews | Pedidos com mais de uma avaliação | 547 | Mantida a avaliação mais recente por pedido | Garante 1 nota por pedido e evita peso duplo |
| items | Vários itens por pedido (1 linha por item) | 9803 | Agregado por pedido antes do join | Evita multiplicar linhas e inflar a receita |
| payments | Vários pagamentos por pedido (parcelas, vouchers) | 2961 | Agregado por pedido antes do join | Evita multiplicar linhas e inflar o valor pago |
| orders | Pontas do período com volume residual (set–dez/2016 e set–out/2018) | 349 | Recorte de 2017-01-01 a 2018-08-31 pela data da compra | Meses incompletos distorcem tendências e comparações |
| orders | Pedidos 'delivered' sem data de entrega | 8 | Removidos da base analítica | Sem data de entrega não é possível medir prazo nem atraso |
| orders | Etapas com datas fora de ordem (ex.: postagem antes da aprovação) | 1382 | Pedido mantido; tempo da etapa incoerente tratado como vazio | Erro de registro na etapa não invalida o prazo total do pedido |
| customers | customer_id é gerado a cada pedido, não identifica a pessoa | 3345 | customer_unique_id usado para recompra, coortes e RFM | Sem isso a recompra apareceria como zero |
| products | Produtos sem categoria | 610 | Categoria preenchida como 'sem categoria' | Mantém os pedidos na análise sem inventar categoria |
| products | Colunas com erro de digitação ('lenght') | 2 | Renomeadas para 'length' | Padronização |
| payments | Pagamentos 'not_defined' ou de valor zero | 12 | Mantidos; receita calculada pelo preço dos itens | Receita não depende da tabela de pagamentos |
| geo | Vários registros de coordenadas por CEP | 981148 | Tabela não utilizada; análise regional feita por UF | UF é suficiente e evita duplicação no join |
| orders | Pedidos não entregues (cancelados, em trânsito etc.) | 2881 | Fora da base analítica; taxa reportada à parte | Só pedidos entregues permitem medir prazo e satisfação |
| items | Pedidos entregues sem itens registrados | 0 | Removidos | Sem itens não há receita, categoria nem seller |