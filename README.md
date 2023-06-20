# CasoDeTeste_AMAZON_Comprehend

### Detecção de Idioma: Identificação automatica do idioma predominante em determinado arquivo, ou conjunto de textos.

Um dos serviços mais simples do Amazon Comprehend, porém eficiente, quando falamos em quantidades enormes de informações, é a detecção da linguagem "dominante" nos arquivos ou documentos analisados. A ferramenta utiliza a norma, ou padrão de conteúdo linguístico e semântico "RFC 5646". O Serviço é bem robusto, contendo mais de 30 idiomas embutidos e por fim retorna um nível de confiança com base na análise feita.

Aqui estão algumas das operações que podem ser utilizadas com esta funcionalidade:

- DetectDominantLanguage

- BatchDetectDominantLanguage

- StartDominantLanguageDetectionJob

Para fins de implementação, a operação "DetectDominantLanguage" retorna um objeto em formato JSON, segue um exemplo abaixo:

```
{
    "Languages": [
        {
            "LanguageCode": "en",
            "Score": 0.9793661236763
        }
    ]
}
```

### Detecção de Entidades (DetectEntities): Identifica e extrai informações relevantes do texto, como nomes de pessoas, organizações, locais, datas, números, entre outros.

### Análise de Sentimento (DetectSentiment): Analisa o texto e determina se a emoção expressa é positiva, negativa, neutra ou mista.

### Extração de Frases-Chave (DetectKeyPhrases): Identifica as frases mais importantes e significativas em um texto.

### Análise de Tópicos (DetectTopics): Analisa o texto e identifica os tópicos ou temas discutidos.

### Reconhecimento de Entidades Nomeadas Personalizadas (CreateEntityRecognizer): Permite treinar um modelo personalizado para reconhecer entidades específicas do domínio do usuário.

### Detecção de Sentimento em Lote (BatchDetectSentiment): Realiza a detecção de sentimento em lotes de documentos de uma só vez.

### Extração de Frases-Chave em Lote (BatchDetectKeyPhrases): Realiza a extração de frases-chave em lotes de documentos de uma só vez.

### Análise de conteúdo por reconhecimento de voz 

Esta funcionalidade em específico é uma agregação à ferramenta Amazon Transcribe, serviço que transforma o aúdio em texto. Essa agregação permite a utilização do serviço Amazon Comprehend para realizar uma análise com o intuito de capturar o conteúdo da mensagem, palavras pontuais (por exemplo: nome, local, data) e a partir disso realizar inferências de acordo com o objetivo específico.  

Na arquitetura apresentada aqui na documentação a API do Amazon Transcribe pode ser agregada a qualquer serviço frontend, que disponibilize o vídeo, ou arquivo de som. Como é esperado, a documentação utiliza os frameworks da própria AWS, para fazer o armazenamento das informações do arquivo. Neste sentido, o caminho da associação se dá primeiro no Amazon CloudFront, serviço de delivery do vídeo em questão, com agregação da ferramenta Amazon S3, que basicamente faz o armazenamento das inforamções colhidas. Após isso, temos o processamento de uma função Lambda (serviço que roda funções de maneira virtual), apenas para termos de segurança e acesso. E por fim, a utilização do serviço Amazon Transcribe para transcrição dos dados do vídeo ou arquivo de voz, e depois isto é passado para o Amazon Comprehend que realiza a análise de conteúdo, checa entidades (nomes, datas, localização) e pode ser utilizado também para outros tipos de inferência a partir de processamento de linguagem natural.

- Link da documentação: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/analyze-speech-in-real-time-using-amazon-transcribe-and-amazon-comprehend.html
