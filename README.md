# Phishing Detection Chatbot

## O Projeto

O objetivo deste projeto é desenvolver um chatbot para o Telegram que detecta URLs de phishing enviadas pelos usuários. O chatbot utilizará dois modelos de aprendizado de máquina para analisar as mensagens e links suspeitos:

1. **Modelo BERT**: Para classificar a textualidade das mensagens, determinando se o conteúdo contém características típicas de phishing, como urgência e textos persuasivos.
2. **Modelo CNN**: Para classificar URLs, determinando se o link é legítimo ou phishing com base em padrões observados em URLs maliciosas.

O chatbot será capaz de receber tanto textos quanto URLs, analisar esses dados e fornecer uma resposta sobre a possibilidade de serem phishing.

---

## Versão Atual

A versão atual do projeto tem como propósito efetuar a análise exploratória dos dados, bem como desenvolver os módelos iniciais, explorando arquiteturas. 

### BERT
- **Análise Exploratória**: Inicialmente, foi utilizado o [SMS Spam Collection Dataset](https://www.kaggle.com/datasets/uciml/sms-spam-collection-dataset) para desenvolver o modelo. Durante esta etapa, foram analisadas características das mensagens, como comprimentos das mensagens, palavras mais comuns e distribuição de classes alvo. Pode ser visto no arquivo Este é um texto normal e <span style="color:red">Phishing_EDA_BERT.ipynb</span>.
- **O Modelo**: Foi utilizado o modelo DistilBERT, uma versão compacta do BERT, da biblioteca Hugging Face para a tarefa de classificação binária (spam ou não). O DistilBertTokenizer é empregado para transformar textos em tokens, e o modelo DistilBertForSequenceClassification é ajustado para classificar em duas categorias (spam e ham). O treinamento é realizado com o otimizador AdamW e a função de perda do modelo. As métricas de desempenho, como perda, acurácia e F1-score, são monitoradas com o WandB.
- **Status**: O modelo foi treinado e está em funcionamento, e parece ter se ajustado bem aos dados de treinamento. Também observou-se uma necessidade de maior representatividade de mensagens.

### CNN
- **Análise Exploratória**: Foi utilizado o [Web page Phishing Detection Dataset](https://www.kaggle.com/datasets/shashwatwork/web-page-phishing-detection-dataset). Foram verificadas características como distribuição de classes e comprimento de URL. Pode ser visualizado no arquivo Phishing_EDA_CNN.ipynb.
- **O modelo**: O modelo é composto por uma camada de embedding para representação de caracteres, seguida por uma Conv1D que detecta padrões em sequências, uma Global Max Pooling para extrair os recursos mais relevantes, e camadas densas com Dropout para processar interações não lineares e prevenir overfitting, com saída binária para classificar URLs como phishing (1) ou legítimas (0). Foi treinado com o otimizador Adam e função de perda Binary Crossentropy, utilizando early stopping para monitorar a perda e evitar overfitting
- **Status**: O modelo foi treinado e está em funcionamento, com boa acurácia. Contudo, também observou-se uma necessidade de maior representatividade de mensagens: para alguns URLs de phishing novos extraídos do Phishtank, o modelo não detectou padrões.

---

## Próximos Passos

1. **Melhorias nos Modelos**: 
   - Experimentar com diferentes arquiteturas para os modelos (por exemplo, ajustar o número de camadas e neurônios na CNN).
   - Testar outras técnicas de pré-processamento de dados.
   - Adaptar para a linguagem pt-BR.

2. **Chatbot**:
   - Integrar os modelos de detecção diretamente no bot do Telegram, permitindo que o modelo responda em tempo real quando um usuário enviar uma mensagem ou URL suspeita.
   - Adicionar funcionalidades extras ao bot, como a possibilidade de aprender com novos exemplos de phishing enviados pelos usuários.

3. **Avaliação de Performance**:
   - Realizar uma análise mais aprofundada sobre o desempenho dos modelos utilizando métricas como precisão, recall e AUC-ROC.

4. **Expansão dos Datasets**:
   - Adicionar mais exemplos de mensagens de phishing e URLs para melhorar a performance dos modelos.   
