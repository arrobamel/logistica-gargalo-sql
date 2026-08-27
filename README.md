# Solucionando Gargalo com SQL - Logística Ltda

Contexto fictício: 4.982 pedidos com SLA estourado.

## Problema
69,4% dos atrasos concentrados em 1 fornecedor: Logística Sul = 1.749 atrasos.

## Query Principal
SELECT fornecedor, COUNT(*) as total_atrasos
FROM "Pedidos"
WHERE status = 'atrasado'
GROUP BY fornecedor
ORDER BY total_atrasos DESC;

## Resultado
- Execução em 41ms
- Recomendação: Troca de rota e renegociação de SLA
- Redução de 70% do gargalo

## Prova de volume
WHERE + BETWEEN + GROUP BY filtrando Jan a Mar/2026 nos 4.982 registros sem travar (DB Browser).
