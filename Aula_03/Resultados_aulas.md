--- RESULTADOS DO LAB 01 --- 
1 - Sem a remoção do stopwords, os dados a serem analisados ficam maiores e prejudica o codigo, deixando ele lento e com maior tempo de execução.
2 - Analisa as palavras chaves individuais e pares de palavras.
3 - Tirando as genericas e deixando apenas as individuias, o codigo consegue trazaer uma resposta mais certeira, já que a separação ajuda a criar um filtro e da menos margem de erro.


--- RESULTADOS DO LAB 02 --- 
1 - Precisão de acerto
2 - O resultado deve ser uma diagonal com 1, no caso do codigo, esta errado
3 - Porque não da para medir com precisão com os dados altamente desbalanceados


--- RESULTADOS DO LAB 03 --- 

# ============================================================
# LAB 03 - AULA 03 (MLCB): Scikit-Learn Pipeline (Modo TODO)
# ============================================================
import pandas as pd
from sklearn.pipeline import Pipeline
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

dados_rh = {
    'mensagem': [
        'Como solicitar minhas ferias?', 'Quero agendar meu periodo de ferias',
        'Onde baixo meu holerite do mes?', 'Preciso do comprovante de rendimentos',
        'Como cadastrar meu atestado medico?', 'Onde envio o atestado de consulta?'
    ],
    'intencao': [
        'solicitar_ferias', 'solicitar_ferias',
        'obter_holerite', 'obter_holerite',
        'enviar_atestado', 'enviar_atestado'
    ]
}

df3 = pd.DataFrame(dados_rh)

# TODO 1: Separe o dataset em X ('mensagem') e y ('intencao')
X = df3['mensagem']
y = df3['intencao']

# TODO 2: Realize o train_test_split com test_size=0.33 e random_state=42
X_train, X_test, y_train, y_test = train_test_split(
  df3['mensagem'], df3['intencao'], test_size=0.33, random_state=42
)

# TODO 3: Monte o Pipeline encapsulando o TfidfVectorizer e a LogisticRegression
pipeline = Pipeline([
     ('vectorizer', TfidfVectorizer(stop_words=['de', 'o', 'meu', 'minhas'])),
     ('classifier', LogisticRegression())
 ])


# TODO 4: Treine o pipeline completo com .fit() usando os dados de treino brutos
# pipeline.fit(...)
pipeline.fit(X_train, y_train)

# TODO 5: Faca a predicao nos dados de teste brutos e exiba a acuracia
predicoes = pipeline.predict(X_test)
print(f"Acuracia via Pipeline: {accuracy_score(y_test, predicoes) * 100:.2f}%")

2 - Ele faz o encapsulamento e o pré-processamento em um unico objeto

3 - Porque ele ja fez o pré processamento
