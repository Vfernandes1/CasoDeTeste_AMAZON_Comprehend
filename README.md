#  Estudo da ferramenta Amazon Comprehend

Estudo das ferramentas em nuvens comerciais que fornecem soluções de PLN.

O objetivo desta atividade é realizar um levantamento das ferramentas de PLN presentes em uma nuvem comercial.

Nuvem Comercial escolhida: **Amazon Comprehend**

**O que é o Amazon Comprehend?**

O Amazon Comprehend é um serviço de processamento de linguagem natural (NLP) que usa machine learning para extrair insights sobre arquivos, textos e documentos em si. Ele pode ser utilizado para reconhecimento de entidades, frases-chave, idioma, sentimentos e outros elementos comuns em um documento. A ferramenta do Amazon Comprehend também fornece várias APIs que podem usadas para criar novos produtos baseados na compreensão da estrutura dos documentos, com base no objetivo de implementação.

A ferramenta pode ser considerada um serviço de nuvem comercial pois fornece um sistema embutido, em nuvem, que amplia a capacidade de amazenamento e rede para agregação de sistemas e programas com atuação rápida, fácil e econômica. Sendo assim, o Amazon Comprehend pode ser utilizado para melhorar seus processos de negócios, como atendimento ao cliente, análise de mídia social, pesquisa de mercado, gerenciamento de documentos e muitas outras tarefas.

### Operações nos serviços do Amazon Comprehend

As operações são comandos que determinam o nível de busca, e análise que será feita. O peso e limitação de cada uma das operações é padrão para cada um dos serviços.

Compreensão das operações:
1. Operações Detect: inspeção, análise ou identificação de arquivos singulares, com implementação simples
2. Operações Batch: inspeção, análise ou identificação de arquivos com o "batch" (rede neural) de até 25. 
3. Operações Start: operação que inicia um trabalho assíncrono que examina uma coleção de dados, normalmente, armazenados em um bucket do Amazon S3.

## Serviços

### Detecção de Idioma

Aplicação: Identificação automatica do idioma predominante em determinado arquivo, ou conjunto de textos.

É dos serviços mais simples do Amazon Comprehend, porém eficiente, quando falamos em quantidades enormes de informações, é a detecção da linguagem "dominante" nos arquivos ou documentos analisados. A ferramenta utiliza a norma, ou padrão de conteúdo linguístico e semântico "RFC 5646". O Serviço é bem robusto, contendo mais de 30 idiomas embutidos e por fim retorna um nível de confiança com base na análise feita.

Aqui estão algumas das operações que podem ser utilizadas com esta funcionalidade:

- DetectDominantLanguage

- BatchDetectDominantLanguage

- StartDominantLanguageDetectionJob

Para fins de implementação, pode selecionar a operação "DetectDominantLanguage" que retorna um objeto em formato JSON, como um exemplo. Segue descrito abaixo:

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

Aqui segue um repositório com exemplificação da aplicação do serviço de detecção de idiomas, para tradução e transcrição de relatórios médicos: https://github.com/aws-samples/amazon-translate-with-comprehend-medical

Link da documentação: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-languages.html

---------

### Detecção de Entidades

Aplicação: Identifica e extrai informações relevantes do texto, como nomes de pessoas, organizações, locais, datas, números, entre outros.

Esse serviço da ferramenta, pode ser descrito como um sistema de taggeamento, pois realiza a identificação, e atriubuição de pesos e "tags" para palavras, e textos que forem definidos como entrada. Deste modo, dependendo do objetivo e da arquitetura proposta em sua aplicação, este serviço pode filtrar ou elencar certas tags como mais ou menos relevantes (com base no peso atribuído), de acordo com a busca e levantamento realizado.

Além disso, a partir das tags, há um score do nível de confiança (ou precisão) no qual o Amazon Comprehend, utilizou, para realizar a detecção.

Os tipos de entidades que podem ser definidas, seguem abaixo:

- **"ITEM_COMERCIAL":** Um produto de marca
- **"DATE":** Uma data completa (por exemplo, 25/11/2017), dia (terça-feira), mês (maio) ou hora (8h30)
- **"EVENT:"** Um evento, como por exemplo um festival, concerto, eleição, etc.
- **"LOCATION:"** Um local específico, como país, cidade, lago, prédio etc.
- **"ORGANIZAÇÃO:"** Grandes organizações, como governo, empresa, religião, equipe esportiva, etc.
- **"PESSOA":** Grupos de pessoas, apelidos, personagens fictícios
- **"QUANTIDADE":** Uma quantia quantificada, como moeda, porcentagens, números, bytes etc.
- **"TITLE":** Um nome oficial dado a qualquer criação ou trabalho criativo, como filmes, livros, músicas, etc.
- **"OTHER":** Entidades que não se encaixam em nenhuma das outras categorias de entidades

As operações para detectar entidades em um documento ou conjunto de documentos, são:

1. DetectEntities

2. BatchDetectEntities

3. StartEntitiesDetectionJob

  Segue um exemplo abaixo do output, fornecido pela operação "DetectEntities":

  ```
  {
    "Entities": [
        {
            "Text": "today",
            "Score": 0.97,
            "Type": "DATE",
            "BeginOffset": 14,
            "EndOffset": 19
        },
        {
            "Text": "Seattle",
            "Score": 0.95,
            "Type": "LOCATION",
            "BeginOffset": 23,
            "EndOffset": 30
        }
    ],
    "LanguageCode": "en"
  }
  ```

Para uma aplicação com maior nível de complexidade, há também o serviço de Reconhecimento de Entidades Nomeadas Personalizadas (com a operação "CreateEntityRecognizer"), que permite treinar um modelo personalizado para reconhecer entidades específicas do domínio do usuário. Isto seria um passo além, seguindo o mesmo core apresentado pelo serviço de Reconhecimento de Entidades padrão do Amazon Comprehend.

Segue repositório com código exemplificando a aplicação da customização no reconhecimento de entidades: https://github.com/aws-samples/amazon-custom-entity-recognition-textract-comprehend

Link para a documentação: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-entities.html 

---------

### Análise de Sentimento

Aplicação: Analisa o texto e determina se a emoção expressa é positiva, negativa, neutra ou mista.

Esse serviço em específico, têm como principal função, determinar o sentimento do conteúdo em documentos de texto codificados em UTF-8 (formato que assegura que não nenhum erro de caracteres). É importante também ressaltar que o serviço faz esta análise a partir de textos e documentos na mesma linguagem.

Na análise, é retornado o sentimento mais provável para o texto e as respectivas pontuações (nível de confiança da predição realizada) para cada um dos sentimentos no determinado texto.

Dentro das classificações especificadas pelo serviço, os textos podem ser:

- Positivo: O texto expressa um sentimento geral positivo.

- Negativo — O texto expressa um sentimento geral negativo.

- Misto — O texto expressa sentimentos positivos e negativos.

- Neutro — O texto não expressa sentimentos positivos ou negativos.

As operações que podem ser utilizadas para análise de sentimento, são:

1. DetectSentiment

2. BatchDetectSentiment

3. StartSentimentDetectionJob

Segue abaixo um exemplo do output retornado pelo serviço, utilizando a operação "DetectSentiment":

```

{
"SentimentScore": {
        "Mixed": 0.030585512690246105,
        "Positive": 0.94992071056365967,
        "Neutral": 0.0141543131828308,
        "Negative": 0.00893945890665054
    },
    "Sentiment": "POSITIVE",
    "LanguageCode": "en"
}

```

É importante ressaltar também, que mediante a necessidade de uma análise mais expressiva, com base na compreensão granular, em relação ao sentimentos de acordo com entidades anteriormente definidas, ou em relação a contextos específicos, há a possibilidade de se usar o serviço de Sentimento direcionado. O serviço em questão funciona como um upgrade da análise de sentimento, com a determinação do sentimento a nível de entidade para em cada documento de entrada em tempo real, agregando maior expressividade na inferência em relação aos dados de saída que serão obtidos. 

Link para a documentação: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-sentiment.html / https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-targeted-sentiment.html

Repositório com aplicação real do serviço de análise de sentimento, fornecido pelo Amazon Comprehend: https://github.com/tanyazyabkina/AWS_Comprehend_Sentiment_Analysis

---------

### Extração de Frases-Chave 

Aplicação: Identifica as frases mais importantes e significativas em um texto.

O serviço de Extração de Frases-Chave permite identificar as "frases-chave" do substantivo encontradas no texto. Sendo assim, as frases-chave podem ser definidas como termos importantes que representam o conteúdo principal do texto.

O Amazon Comprehend, a partir deste serviço, retorna uma coleção de frases-chave que identificou no texto de entrada. Para cada frase-chave, a resposta fornece o texto da frase-chave, onde a frase-chave começa e termina, e o nível de confiança que a ferramenta tem na precisão da detecção.

As operações para este serviço são:

1. DetectKeyPhrases
2. BatchDetectKeyPhrases
3. StartKeyPhrasesDetectionJob 

Link da documentação: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-key-phrases.html

Vídeo de exemplificação da utilização do serviço de extração de frases-chave, do Amazon Comprehend: https://www.youtube.com/watch?v=UoNKG1A_X40

--------


### Análise de conteúdo por reconhecimento de voz 

Esta funcionalidade em específico é uma agregação à ferramenta Amazon Transcribe, serviço que transforma o aúdio em texto. Essa agregação permite a utilização do serviço Amazon Comprehend para realizar uma análise com o intuito de capturar o conteúdo da mensagem, palavras pontuais (por exemplo: nome, local, data) e a partir disso realizar inferências de acordo com o objetivo específico.  

Na arquitetura apresentada aqui na documentação a API do Amazon Transcribe pode ser agregada a qualquer serviço frontend, que disponibilize o vídeo, ou arquivo de som. Como é esperado, a documentação utiliza os frameworks da própria AWS, para fazer o armazenamento das informações do arquivo. Neste sentido, o caminho da associação se dá primeiro no Amazon CloudFront, serviço de delivery do vídeo em questão, com agregação da ferramenta Amazon S3, que basicamente faz o armazenamento das inforamções colhidas. 

Após isso, temos o processamento de uma função Lambda (serviço que roda funções de maneira virtual), apenas para termos de segurança e acesso. E por fim, a utilização do serviço Amazon Transcribe para transcrição dos dados do vídeo ou arquivo de voz, e depois isto é passado para o Amazon Comprehend que realiza a análise de conteúdo, checa entidades (nomes, datas, localização) e pode ser utilizado também para outros tipos de inferência a partir de processamento de linguagem natural.

Link da documentação: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/analyze-speech-in-real-time-using-amazon-transcribe-and-amazon-comprehend.html

Aplicação real do Amazon Comprehend e Amazon Transcribe para Podcast: https://github.com/aws-samples/amazon-transcribe-comprehend-podcast

-----------------------

## Referências

Documentação do Amazon Comprehend - Como Analisar Sentimentos:
Amazon Web Services. Amazon Comprehend – Como Analisar Sentimentos. Disponível em: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-sentiment.html. Acesso em: 20 jun. 2023.

Documentação do Amazon Comprehend - Como Analisar Sentimentos Segmentados:
Amazon Web Services. Amazon Comprehend – Como Analisar Sentimentos Segmentados. Disponível em: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-targeted-sentiment.html. Acesso em: 20 jun. 2023.

Documentação do Amazon Comprehend - Como Extrair Frases-Chave:
Amazon Web Services. Amazon Comprehend – Como Extrair Frases-Chave. Disponível em: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-key-phrases.html. Acesso em: 20 jun. 2023.

Documentação do Amazon Comprehend - Como Extrair Entidades:
Amazon Web Services. Amazon Comprehend – Como Extrair Entidades. Disponível em: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-entities.html. Acesso em: 20 jun. 2023.

Documentação do Amazon Comprehend - Como Detectar Idiomas:
Amazon Web Services. Amazon Comprehend – Como Detectar Idiomas. Disponível em: https://docs.aws.amazon.com/pt_br/comprehend/latest/dg/how-languages.html. Acesso em: 20 jun. 2023.
