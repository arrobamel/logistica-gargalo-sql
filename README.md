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
