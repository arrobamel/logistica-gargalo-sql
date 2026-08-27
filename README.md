```

- Prova do gargalo (41ms nos 4.982):**
<img width="889" height="566" alt="1" src="https://github.com/user-attachments/assets/61155fbe-0b26-44b7-9c5e-90279396b65f" />
<img width="889" height="566" alt="1" src="https://github.com/user-attachments/assets/a88e2d00-c262-42af-8964-150e9524f650" />



> Insight: Risco concentrado. Só trocar rota da Sul já reduz 70% do gargalo.
@@ -33,11 +34,14 @@ GROUP BY mes;
```

- Prova de recorrência Jan-Mar/2026:**
<img width="897" height="566" alt="2" src="https://github.com/user-attachments/assets/d3daa740-bcf5-424a-bac2-7a6fcd2ca246" />
<img width="897" height="566" alt="2" src="https://github.com/user-attachments/assets/b216a973-a49e-4ffd-a103-dbc77242f907" />


> Recorrência de ~320 atrasos/mês. Não é pico, é processo.

### 📊 Resultado Final
<img width="897" height="566" alt="4" src="https://github.com/user-attachments/assets/5b2dd179-6cb5-4cbe-beb7-76a42bd44854" />

- Execução: 41ms sem travar
- Recomendação: Troca de rota + renegociação de SLA
- Impacto: -70% do gargalo
