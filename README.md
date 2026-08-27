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
<img width="889" height="566" alt="1" src="https://github.com/user-attachments/assets/a88e2d00-c262-42af-8964-150e9524f650" />



> Insight: Risco concentrado. Só trocar rota da Sul já reduz 70% do gargalo.

     ### 📅 QUERY 2: É recorrente?

```sql
     SELECT substr(data_pedido, 4, 7) as mes_ano, COUNT(*) as atrasos
     FROM "Pedidos"
     WHERE status = 'atrasado'
     GROUP BY mes_ano;


- Prova de recorrência Jan-Mar/2026:**
<img width="897" height="566" alt="2" src="https://github.com/user-attachments/assets/b216a973-a49e-4ffd-a103-dbc77242f907" />


> Recorrência de ~320 atrasos/mês. Não é pico, é processo.

### 📊 Resultado Final
<img width="897" height="566" alt="4" src="https://github.com/user-attachments/assets/5b2dd179-6cb5-4cbe-beb7-76a42bd44854" />

- Execução: 41ms sem travar
- Recomendação: Troca de rota + renegociação de SLA
- Impacto: -70% do gargalo

### 📁 Arquivos
- `base_logistica_4982_pedidos.db`
- `prints/` com as evidências
