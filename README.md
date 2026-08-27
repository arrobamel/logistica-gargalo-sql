# 🚚 Gargalo Logístico Resolvido: 70% de Impacto com SQL

> **Contexto fictício:** Empresa Logística Ltda com SLA estourado, faturamento e estoque travados.

### 🎯 O Problema
- **4.982 pedidos** analisados no DB Browser for SQLite
- **69,4% dos atrasos** concentrados em 1 fornecedor: Logística Sul = **1.749 atrasos**

### 🔍 QUERY 1: Onde está o gargalo?

```sql
SELECT fornecedor, COUNT(*) as total_atrasos
FROM "Pedidos"
WHERE status = 'atrasado'
GROUP BY fornecedor
ORDER BY total_atrasos DESC;
```

 - Gargalo na Logística Sul (41ms nos 4.982):**
<img width="889" height="566" alt="1" src="https://github.com/user-attachments/assets/a88e2d00-c262-42af-8964-150e9524f650" />



> Insight: Risco concentrado. Só trocar rota da Sul já reduz 70% do gargalo.

### 📅 QUERY 2: É recorrente?

```sql
SELECT strftime('%m/%Y', data_pedido) as mes, COUNT(*) as atrasos
FROM "Pedidos"
WHERE status = 'atrasado' 
AND data_pedido BETWEEN '2026-01-01' AND '2026-03-31'
GROUP BY mes;
```

- Prova de recorrência Jan-Mar/2026:**
<img width="897" height="566" alt="2" src="https://github.com/user-attachments/assets/b216a973-a49e-4ffd-a103-dbc77242f907" />


> Recorrência de ~320 atrasos/mês. Não é pico, é processo.

### 📊 Resultado Final
<img width="897" height="566" alt="4" src="https://github.com/user-attachments/assets/5b2dd179-6cb5-4cbe-beb7-76a42bd44854" />

- Execução: 41ms sem travar
- Recomendação: Troca de rota + renegociação de SLA
- Impacto: -70% do gargalo

  


### 👀 Olha como ficou no Power BI também


Dashboard validando os 4.982 pedidos e o gargalo da Logística Sul.

<img width="902" height="506" alt="gargalo_logistico_" src="https://github.com/user-attachments/assets/0fc3f91b-eb51-4d65-a556-a6f8afcafb6a" />


> Visualização interativa do gargalo: 69,4% concentrado em 1 fornecedor.


### 📁 Arquivos
- `base_logistica_4982_pedidos.db`
- `prints/` com as evidências
