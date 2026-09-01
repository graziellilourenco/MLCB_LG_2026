# ==============================================================================
# GERADOR SINTÉTICO DE DADOS - SAC MÓVEIS RESIDENCIAIS
# ==============================================================================
import pandas as pd
import random

templates = {
    'vendas': {
        's': ['', 'Olá', 'Bom dia', 'Gostaria de saber', 'Por favor'],
        'a': ['quero comprar', 'qual o preco do', 'tem cupom para', 'como faco para adquirir', 'desejo orcamento de'],
        'o': ['sofa retratil 3 lugares', 'conjunto de mesa de jantar', 'guarda roupa casal', 'painel para tv', 'colchao queen size']
    },
    'suporte': {
        's': ['', 'Oi', 'Preciso de ajuda', 'Por gentileza', 'Socorro'],
        'a': ['como montar o', 'onde baixo o manual do', 'estou com duvida no', 'veio faltando parafuso no', 'preciso de assistencia para'],
        'o': ['armario de cozinha', 'rack da sala', 'berco do bebe', 'esquema de montagem', 'manual da estante']
    },
    'trocas_devolucoes': {
        's': ['', 'Olá', 'Por favor', 'Gostaria de solicitar', 'Quero abrir'],
        'a': ['preciso trocar o', 'quero devolver a', 'como solicito o estorno do', 'desejo solicitar a troca da', 'como funciona a devolucao do'],
        'o': ['produto com defeito', 'mesa que veio arranhada', 'cadeira no prazo de 7 dias', 'pedido cancelado', 'item com avaria']
    },
    'reclamacoes': {
        's': ['', 'Urgente', 'Pessimo atendimento', 'Absurdo', 'Quero registrar'],
        'a': ['estou indignado com o', 'quero fazer uma queixa do', 'estou reclamando do', 'produto veio quebrado e o', 'atendimento horrivel do'],
        'o': ['atraso na minha entrega', 'servico de montagem', 'sac que nao responde', 'pos venda da loja', 'estado do meu movel']
    },
    'logistica_entregas': {
        's': ['', 'Olá', 'Bom dia', 'Por gentileza', 'Preciso saber'],
        'a': ['onde esta o meu', 'qual o prazo de entrega do', 'como rastreio a', 'qual a transportadora do', 'quando chega o'],
        'o': ['meu pedido', 'codigo de rastreamento', 'movel comprado', 'status do envio', 'agendamento da entrega']
    }
}

amostras = []
random.seed(42)

for intencao, comp in templates.items():
    for _ in range(20):  # Total: 100 amostras (20 por classe)
        s = random.choice(comp['s'])
        a = random.choice(comp['a'])
        o = random.choice(comp['o'])
        frase = f"{s} {a} {o}".strip().capitalize()
        amostras.append({'texto': frase, 'intencao': intencao})

df_moveis = pd.DataFrame(amostras)
df_moveis.to_csv('dataset_moveis_100.csv', index=False, encoding='utf-8')

print(" Dataset 'dataset_moveis_100.csv' criado com 100 frases distribuidas em 5 intencoes!")

# ==============================================================================
# ATIVIDADE 1: CHATBOT VERSÃO 1 (KNN)
# ==============================================================================
import numpy as np
import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.neighbors import KNeighborsClassifier
from sklearn.pipeline import Pipeline
from sklearn.metrics import classification_report, confusion_matrix
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix, f1_score

# 1. Carregar dataset do CSV
df = pd.read_csv('dataset_moveis_100.csv')

# 2. Divisão Treino e Teste
X_train, X_test, y_train, y_test = train_test_split(
    df['texto'], df['intencao'], test_size=0.30, random_state=42, stratify=df['intencao']
)

# TODO 1: Monte a Pipeline utilizando TfidfVectorizer e KNeighborsClassifier(n_neighbors=3, metric='cosine')
pipeline_nlu = Pipeline([
     ('vectorizer', TfidfVectorizer(ngram_range=(1, 2))),
    ('classifier', KNeighborsClassifier(n_neighbors=3, metric='cosine'))
 ])

# TODO 2: Treine a pipeline com os dados de treino (X_train, y_train)
pipeline_nlu.fit(X_train, y_train)

# TODO 3: Gere as predicoes nos dados de teste e exiba o classification_report e a confusion_matrix
y_pred = pipeline_nlu.predict(X_test)
acc = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred, average='weighted')
print(classification_report(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))

LIMIAR_CONFIANCA = 0.50

print("\n=== INICIANDO BATERIA DE TESTES (10 INPUTS OBRIGATÓRIOS) ===")

for i in range(1, 11):
    print(f"\n[Teste {i}/10]")
    
    # TODO 4: Solicite a frase do usuario via teclado
    frase = input("Digite a frase do cliente: ").strip()
    
    # TODO 5: Extraia as probabilidades e a classe prevista usando predict_proba e predict
    probs = pipeline_nlu.predict_proba([frase])[0]
    maior_prob = np.max(probs)
    intencao = pipeline_nlu.predict([frase])[0]
    
    # TODO 6: Aplique a regra de decisao:
    # Se maior_prob >= LIMIAR_CONFIANCA: imprima a intencao e a probabilidade.
    # Senao: imprima o Fallback encaminhando para atendimento humano.
    if maior_prob >= LIMIAR_CONFIANCA:
      print(f"\n[Intenção: {intencao.upper()} | Confiança: {maior_prob*100:.1f}%]: ",)
      print("Aprovado")
    else:
      print(f"\n[Intenção: {intencao.upper()} | Confiança: {maior_prob*100:.1f}%]: ",)
      print("Fallback")
      print("Nâo consegui entender, sua mensagem sera enviada a um atendente humano.")   
    
    pass
# Atividade 2



