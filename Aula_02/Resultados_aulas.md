--- RESULTADOS DO LAB 01 ---
Mensagem: 'Quero consultar quanto dinheiro tenho' ==> Intenção Predita: [fazer_pix]
Mensagem: 'Pode me ajudar a fazer um pix?' ==> Intenção Predita: [fazer_pix]
Mensagem: 'Gostaria de cancelar meu cartão de crédito' ==> Intenção Predita: [cancelar_conta]

1 - Os resultados foram incorretos
2 - Adicionar a frase que saiu com intenção errada no dataset de exemplo, e adicioar a inteção correta na lista de inteções 
3 - Ele classifica palavras chaves transformando elas em 0 ou 1 para medir um grau de importancia.

--- RESULTADOS DO LAB 02 ---
Mensagem de Teste: 'Gostaria de devolver o produto que comprei'
Intenção Predita: troca_devolucao

--- Distribuição de Probabilidades por Classe ---
Classe [duvida_frete]: 27.99%
Classe [rastrear_pedido]: 24.54%
Classe [troca_devolucao]: 47.46%

1 - Os resultados foram corretos
2 -  Adicionar a frase que saiu com intenção errada no dataset de exemplo, e adicioar a inteção correta na lista de inteções 
3 - Calcula a probabilidade de uma palavra pentecer a uma intenção dada a quantidade de vezes que essa palavra aparece no treinamento 

--- RESULTADOS DO LAB 3 ---

Codigo com os TODO

import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Dataset de Suporte Técnico
dados_tech = {
    'mensagem': [
        'Esqueci minha senha de acesso', 'Não consigo entrar no sistema', 'Como redefinir minha senha?',
        'A internet esta muito lenta', 'Sem conexao de rede no escritorio', 'Minha conexao caindo toda hora',
        'Impressora nao esta funcionando', 'Nao consigo imprimir documentos', 'Impressora travada com papel'
    ],
    'intencao': [
        'reset_senha', 'reset_senha', 'reset_senha',
        'problema_conexao', 'problema_conexao', 'problema_conexao',
        'suporte_impressora', 'suporte_impressora', 'suporte_impressora'
    ]
}

df3 = pd.DataFrame(dados_tech)

# TODO 1: Separe o dataset em X (coluna 'mensagem') e y (coluna 'intencao')
X = df3['mensagem']
y = df3['intencao']

# TODO 2: Realize a divisão em treino (70%) e teste (30%) com random_state=42
# X_train, X_test, y_train, y_test = ...
X_train, X_test, y_train, y_test = train_test_split (X ,y, test_size = 0.3, random_state=42)

# TODO 3: Instancie o CountVectorizer e ajuste/transforme os dados de treino e teste
# vectorizer = ...
# X_train_vec = ...
# X_test_vec = ...
vectorizer = CountVectorizer()
X_train_vec = vectorizer.fit_transform(X_train)
X_test_vec = vectorizer.transform(X_test)

# TODO 4: Instancie o DecisionTreeClassifier e treine o modelo com .fit()
# modelo_arvore = ...
# modelo_arvore.fit(...)
modelo_arvore = DecisionTreeClassifier(random_state=42)
modelo_arvore.fit(X_train_vec, y_train)

# TODO 5: Gere as predições para o X_test_vec e exiba a acurácia
predicoes = modelo_arvore.predict(X_test_vec)
acuracia = accuracy_score(y_test,predicoes)
print(f"Acurácia do Modelo: {acuracia * 100:.2f}%")

1 - 33.33%. sim, com uma metrica tão pequena, acertar ou errar ja altera o resultado e não garante que o modelo funcionará bem com novos exemplos.
2 - O modelo analisa as palavras da mensagem e identifica a intenção com a qual ela mais se parece
3 - a arvore pode ficar complexa demais e memorizar os exemplos de treinamento, tendo pior desempenho com novas mensagens.



--- RESULTADOS DO LAB 4 ---

Acurácia do Modelo: 100.00%
Mensagem: Gostaria de comprar um voo para Salvador
Intenção prevista: comprar_passagem

Mensagem: Quero desistir da minha viagem
Intenção prevista: comprar_passagem

Mensagem: Preciso conversar com um atendente
Intenção prevista: falar_atendente


