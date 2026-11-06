# Olist: a logística como freio da satisfação e da recompra

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/[seu-usuario]/olist-logistica-satisfacao/blob/main/notebooks/olist_analise.ipynb)

Tech Challenge, Fase 1 · FIAP Pós Tech Data Analytics · [Seu nome]

Relatório executivo para investidores construído a partir do dataset público de e-commerce da Olist (Kaggle), com dados de jan/2017 a ago/2018, enriquecido com dados do IBGE.

**Tese:** a Olist cresceu rápido, mas os atrasos logísticos derrubam a satisfação e a recompra. Corrigir a entrega nas rotas críticas destrava valor.

## Entregáveis

| Entregável | Link |
|---|---|
| Apresentação executiva | [Abrir a apresentação](https://claude.ai/artifact/Fjwb6KYg9TB1mXduzHrRxP) |
| Vídeo (até 5 min) | [link do vídeo] |
| Notebook com toda a análise | [`notebooks/olist_analise.ipynb`](notebooks/olist_analise.ipynb) |
| Dashboard Power BI | [`dashboard/`](dashboard/) |

## Principais achados

| Tema | Achado |
|---|---|
| Crescimento | Pedidos +140% (jan–ago/2018 vs. jan–ago/2017), mas estáveis em ~6,6 mil/mês ao longo de 2018 |
| Receita | SP responde por 38% da receita e o Sudeste por 65%; AM, RR e AP compram menos do que a renda indica (IBGE) |
| Logística | 6,8% dos pedidos atrasam (13% no Nordeste, 21% em Alagoas); 74% do tempo de entrega está no transporte |
| Rotas críticas | 10 rotas somam 37% dos atrasos com só 19% dos pedidos |
| Satisfação | Nota média de 4,3 no prazo vs. 2,3 com atraso; 65% das reclamações falam de entrega |
| Recompra | Só 3,0% dos clientes compram de novo (2,5% quando a 1ª compra atrasou) |
| Previsão | ~6,3 mil pedidos/mês até fev/2019 (suavização exponencial; erro de 5% no teste) |

## Recomendações

1. **Rotas críticas:** renegociar transportadoras e rever prazos nas 10 rotas com mais atrasos acima da média (ex.: SP→RJ, SP→BA).
2. **Sellers pontuais:** ranking de pontualidade e mais destaque para quem posta em até 2 dias.
3. **Recompra:** programa de relacionamento após a 1ª entrega no prazo, com foco em clientes de alto valor.

Simulação: sem atrasos, a nota média subiria de 4,16 para 4,29.

## Estrutura do repositório

```
olist-logistica-satisfacao/
├── notebooks/olist_analise.ipynb   # análise completa, da ingestão à previsão
├── data/processed/                 # tabelas tratadas que alimentam o Power BI
├── reports/figures/                # 18 gráficos gerados pelo notebook
├── reports/achados.json            # todos os números citados no relatório
├── docs/qualidade_dados.md         # registro de problemas e decisões de tratamento
├── docs/dicionario_dados.md        # dicionário da tabela fato_pedidos
├── dashboard/                      # layout, tema, medidas DAX e guia do Power BI
└── requirements.txt
```

## Como reproduzir

1. Clique no botão **Abrir no Colab** acima.
2. No Colab, use **Ambiente de execução → Executar tudo**.

O dataset é baixado automaticamente do Kaggle (`olistbr/brazilian-ecommerce`) via `kagglehub`, e os dados do IBGE pela API SIDRA. Ao final, o notebook gera as pastas `data/processed/`, `reports/` e `docs/`, além de um `.zip` com tudo.

Para rodar localmente: `pip install -r requirements.txt` e abra o notebook no Jupyter.

> As tabelas para o Power BI ficam em `data/processed/olist_powerbi.xlsx`, com uma aba por tabela.

## Dados e governança

- **Fonte:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (9 tabelas, ~100 mil pedidos) e IBGE/SIDRA (tabelas 6579 e 5938, 2018).
- **Recorte:** jan/2017 a ago/2018 pela data da compra; meses das pontas têm volume residual.
- **Base analítica:** 96.203 pedidos entregues, uma linha por pedido. Itens e pagamentos são agregados por pedido antes dos cruzamentos.
- **Receita:** soma do preço dos itens, sem frete.
- **Cliente:** identificado por `customer_unique_id`.
- **Qualidade:** cada problema encontrado, as linhas afetadas e a decisão tomada estão em [`docs/qualidade_dados.md`](docs/qualidade_dados.md).

## Tecnologias

Python (pandas, matplotlib, seaborn, Prophet, statsmodels, NLTK), Google Colab, Power BI e dados públicos do IBGE.
