Demo
Foram testadas quatro frases:
- Compra de imóvel: identificada corretamente com 80,4%.
- Aluguel de imóvel: identificada incorretamente como manutenção, com 58,9%.
- Vazamento no banheiro: confiança baixa de 39,1%; fallback acionado.
- Segunda via do boleto: identificada corretamente com 55,4%.
LAB 01
A Regressão Logística foi substituída pela Árvore de Decisão. O sistema continuou funcionando, mas apresentou uma classificação errada mesmo indicando 100% de confiança.
LAB 02
O limite de confiança foi alterado de 50% para 65%. Com isso, três das quatro mensagens acionaram o fallback. A tela também passou a mostrar o corte aplicado de 65%.
LAB 03
Foi adicionada a intenção cancelar_contrato, com cinco frases de treinamento e uma resposta própria. Duas das quatro frases de teste foram identificadas corretamente. As outras duas acionaram o fallback.
Conclusão
Os laboratórios funcionaram. Porém, a quantidade de frases de treinamento ainda é pequena, causando algumas classificações erradas e respostas com baixa confiança.
