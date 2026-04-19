# 🔴 R$ 486.719 em capital imobilizado — identificados antes do balanço fechar

**Sistema de Perfil de Eficiência e Risco | Contoso Retail**

> Um varejista com centenas de lojas não sabe quais unidades estão acumulando estoque morto — até o trimestre fechar no vermelho. Este projeto resolve esse problema antes que ele vire prejuízo no balanço.

---

## O problema real

Em operações de varejo, estoque parado não é apenas ineficiência — é capital de giro imobilizado que poderia estar financiando produtos de alta rotatividade. A pergunta que nenhum sistema operacional tradicional responde com clareza:

> *"Qual é o risco financeiro real do meu estoque hoje, loja por loja, produto por produto?"*

---

## O que este sistema faz

Em vez de apenas listar quantidades em estoque, o sistema calcula a **exposição financeira real** de cada item — cruzando custo de inventário com probabilidade de obsolescência baseada em tempo de prateleira (Aging).

**Três saídas concretas:**

| Saída | O que responde |
|-------|----------------|
| **VaR por loja** | Qual unidade concentra maior risco de perda iminente? |
| **Ranking de produtos críticos** | Quais SKUs estão imobilizando capital sem perspectiva de giro? |
| **Alerta executivo automático** | 🔴 Ação imediata ou 🟢 monitoramento — sem subjetividade |

---

## Resultado gerado

```
--- RELATÓRIO DE AUDITORIA IA ---
Unidade Analisada: 199 | Perfil: Risco Crítico/Perda
Similaridade com Benchmark (Loja 200): 100.00%
Exposição Financeira (VaR): R$ 486.719,24
🔴 AÇÃO RECOMENDADA: Alto Valor em Risco. Iniciar queima de estoque ou transferência.
```

A Loja 199 apresenta operação idêntica ao benchmark (Loja 200) em estrutura, mas com R$ 486 mil em capital em risco — o que isola o problema como **falha operacional, não estrutural**. Decisão direcionada, sem achismo.

---

## Como funciona

### 1. Extração e engenharia de dados (SQL Server)
```sql
SELECT StoreKey, ProductKey, UnitCost, OnHandQuantity, 
       Aging, InventoryTotalCost 
FROM vw_FactInventory_Snapshot
```
Views otimizadas sobre `FactInventory` e `FactSales` com milhões de registros.

### 2. Perfis de risco com pesos calibrados (Python/Pandas)
```python
mapa_perfil = {
    1: "Eficiência Máxima",   # peso: 2%
    2: "Operação Saudável",   # peso: 5%
    3: "Alerta Leve",         # peso: 10%
    4: "Risco Moderado",      # peso: 25%
    5: "Gargalo Logístico",   # peso: 50%
    6: "Perda de Margem",     # peso: 75%
    7: "Risco Crítico/Perda"  # peso: 95%
}

df['Valor_Em_Risco'] = df['InventoryTotalCost'] * df['Probabilidade_Perda']
```
Pesos baseados em padrões de Controladoria e curva de depreciação para bens de consumo.

### 3. Similaridade de Cosseno entre lojas (Scikit-learn)
```python
# Normalização para eliminar viés por tamanho da loja
matriz_norm = (matriz_lojas - matriz_lojas.min()) / (matriz_lojas.max() - matriz_lojas.min())

sim_matrix = cosine_similarity(matriz_norm)
```
O modelo identifica "lojas gêmeas" operacionalmente — permitindo benchmarking justo e isolamento de anomalias.

---

## Arquitetura do projeto

```
SQL Server (ContosoRetailDW)
    └── vw_FactInventory_Snapshot  ──►  Python (Pandas)
                                            ├── Perfil de Aging (1-7)
                                            ├── Cálculo de VaR
                                            ├── Similaridade de Cosseno
                                            └── Motor de Alerta Executivo
                                                    └── Streamlit Dashboard
```

---

## Stack técnico

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![SQL Server](https://img.shields.io/badge/SQL_Server-ContosoRetailDW-red?logo=microsoftsqlserver)
![Pandas](https://img.shields.io/badge/Pandas-Data_Engineering-150458?logo=pandas)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Cosine_Similarity-F7931E?logo=scikit-learn)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualização-4C72B0)
![Streamlit](https://img.shields.io/badge/Streamlit-Dashboard-FF4B4B?logo=streamlit)

---

## Contexto profissional

Este projeto foi desenvolvido com base em 10 anos de experiência operacional em gestão de inventário e auditoria de estoque no varejo. Os perfis de risco e os pesos de probabilidade de perda foram calibrados com base em padrões reais de Controladoria e dinâmicas de depreciação observadas na operação.

**Não é um exercício acadêmico — é a resposta técnica a um problema que eu vivi.**

---

## Próximos passos

- [ ] Deploy do dashboard Streamlit com dados mockados (acesso público)
- [ ] Integração com alertas automáticos por e-mail (SMTP)
- [ ] Modelo preditivo de demanda para redução proativa de Aging

---

## Autor

**Jefferson da Silva Araújo**  
Analista de Dados | Logística & Supply Chain | Python · SQL · Machine Learning

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Jefferson_Araujo-0A66C2?logo=linkedin)](https://www.linkedin.com/in/jeffersona-analise-dados)
[![GitHub](https://img.shields.io/badge/GitHub-JeffGideon216-181717?logo=github)](https://github.com/JeffGideon216)
[![Portfólio BI](https://img.shields.io/badge/Portfólio-Power_BI-F2C811?logo=powerbi)]( https://bit.ly/4cDSp4x)
