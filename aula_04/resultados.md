3.1

| Modelo | Acurácia Geral | F1-Score (Weighted) | Principais Erros na Matriz |
| :--- | :--- | :--- | :--- |
| **KNN (K=3)** | 100% | 100% | Não houveram erros |
| **Decision Tree** | 76,67% | 75,00%% | trocas e devoluções |

3.2
- **Comportamento do KNN (10 testes):** [Como o KNN reagiu às variações das frases digitadas e ao fallback?]: Se comportou muito bem em todos os testes, direcionando a frase a intenção correta ou ao fallback quando necessario
- **Comportamento da Decision Tree (8 testes):** [Como a Árvore de Decisão se comportou em comparação ao KNN?] : Se comportou muito mal, dando respostas erradas, mesmo quando falava que a precisão estava 100% correta

- 3.3

- ## 3. Veredito Final
- **Melhor modelo para este projeto:** [KNN ou Decision Tree]: KNN
- **Justificativa técnica:** [Explique a escolha com base nas métricas estatísticas e no comportamento do fallback] o KNN apresentou melhor desempenho por mostrar a acuracia verdadeira, ja a arvore de decisão mostrou respostas erradas
