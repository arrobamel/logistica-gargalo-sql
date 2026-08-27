# 🚚 Solucionando Gargalo Logístico com SQL - 4.982 Pedidos

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

 - Prova do gargalo (41ms nos 4.982):**
(prints/print1_gargalo.png)

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
(prints/print2_recorrencia.png)

> Recorrência de ~320 atrasos/mês. Não é pico, é processo.

### 📊 Resultado Final
- Execução: 41ms sem travar
- Recomendação: Troca de rota + renegociação de SLA
- Impacto: -70% do gargalo

### 📁 Arquivos
- `base_logistica_4982_pedidos.db`
- `prints/` com as evidências
