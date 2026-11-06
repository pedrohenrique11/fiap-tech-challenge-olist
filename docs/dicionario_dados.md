# Dicionário de dados: aba fato_pedidos (olist_powerbi.xlsx)

Uma linha por pedido entregue no período analisado.

| coluna | descricao |
|---|---|
| pedido_id | Identificador do pedido |
| cliente_id | Identificador único da pessoa (customer_unique_id) |
| data_compra | Data da compra |
| mes | Mês da compra |
| data_entrega | Data de entrega ao cliente |
| data_prevista | Data de entrega prometida |
| uf_cliente | UF do cliente |
| estado_cliente | Nome do estado (para mapas) |
| regiao_cliente | Região do cliente |
| uf_seller | UF do seller principal |
| regiao_seller | Região do seller |
| rota | UF do seller → UF do cliente |
| interestadual | Seller e cliente em UFs diferentes |
| seller_id | Seller do item mais caro do pedido |
| categoria | Categoria do item mais caro do pedido |
| qtd_itens | Número de itens |
| qtd_sellers | Número de sellers distintos |
| valor_produtos | Receita: soma do preço dos itens (R$) |
| valor_frete | Soma do frete (R$) |
| frete_pct | Frete ÷ valor dos produtos |
| valor_pago | Soma dos pagamentos (R$) |
| forma_pagamento | Forma de pagamento de maior valor |
| parcelas | Maior número de parcelas |
| dias_entrega | Dias da compra à entrega |
| dias_aprovacao | Dias da compra à aprovação do pagamento |
| dias_postagem | Dias da aprovação à entrega à transportadora |
| dias_transporte | Dias da transportadora ao cliente |
| dias_prometidos | Dias da compra à data prometida |
| dias_atraso | Dias entre a entrega e a data prometida (positivo = atraso) |
| atrasado | Entregue após a data prometida |
| status_entrega | No prazo / Atrasado |
| faixa_atraso | Faixa de dias de atraso |
| nota | Nota da avaliação (1 a 5) |
| nota_baixa | Nota 1 ou 2 |
| coorte | Mês da primeira compra do cliente |