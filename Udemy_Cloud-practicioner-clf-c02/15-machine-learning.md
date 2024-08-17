# Machine Learning

## Amazon Rekognition

- Find objects, people, text, scenes in images and videos using ML
- Facial analysis and facial search to do user verification, people counting
- create a database of "familiar faces" or compare against celebrities
- Use cases:
  - labeling
  - context moderation
  - text detection
  - Face detection and analysis (gender, race, emotions)
  - Face search and verification
  - Celebrity Recognition
  - Pathing (sports, game analysis)

## Amazon Transcribe

- Automatically speech to text
- Uses a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately
- Automatically remove Personally Indetifiable Information (PII) using Redaction
- Supports Automatic Language Identification for multi-lingual audio
- Use cases:
  - transcribe customers service calls
  - automate closed captioning and subtitling
  - generate metadata for media assets to create a fully searchable archive

## Amazon Polly

- Turn text into lifelike speech using deep learning
- Allowing you to create applicatons that talk

## Amazon Translate

- Natural and accurate language translation
- Amazon Translate allows you to localize content - such as websites and applications - for international users and to easily translate large volumes of text efficiently

## Amazon Lex & Connect

### Amazon Lex

- Same technology that Powers Alexa
- automatic speech recognition (ASR) to convert speech to text
- Natural language Understanding to recognize the intent of text, callers
- Helps build chatbots, call center bots

### Amazon Connect

- Receive calls, create contact flows, cloud-based virtual contact center
- can integrate with other CMRs or AWS
- No upfront payments, 80% cheaper than traditional contact center solutions
- Phone call (schedule an appointment) -> call (number defined by Amazon Connect) -> stream (Lex intent recognized) -> invoke -> Lambda -> Schedule -> CRM

## Amazon Comprehend

- Natural Language Processing - NLP
- Fully managed and serverless service
- Uses machine learning to find insights and relationships in text
  - Language of the text
  - Extracts keys, phrases, places, people, brands, or events
  - Understands how positive or negative the text is
  - Analyzes text using tokenization and parts of speech
  - Automatically organizes a collection of text files by topic
- Sample use cases:
  - analyzes customer interactions (emails) to find what leads to a positive or negative experience
  - create and group articles by topics that Comprehend will uncover

## Amazon SageMaker

- Full managed service for developers / data scientists to build ML models
- Typically difficult to do all the processes in one place + provision servers
- Machine learning process (simplified): predicting you exam score
- Hystorical data ... -> Label -> Build -> Train and tune
- Apply model from new data -> prediction
- All this process can be done inside SageMaker

## Amazon Forecast

- Fully managed service that uses ML to deliver highly accurate forecasts
- Example: predict the future sales of a raincoat
- 50% more accurate than looking at the data itself
- Reduce forecasting time from months to hours
- Use cases: product demand Planning, Finantial Planning, Resource Planning

# Amazon Kendra

- Fully managed document search service powered by Machine Learning
- Extract answers from within a document (text, pdf, HTML, PowerPoint, Word, FAQs)
- Natural Langueage search capabilities
- Data sources -> indexing -> answer questions
- Learn from user interactions/ feedback to promote preferred results (incremental Learning)
- Ability to manually fine-tune search results (importance of data, freshness, custom, ...)

# Amazon Personalize

- Fully managed ML-service to build apps with real-time personalized recommendations
- Example: personalized product recommendations/re-ranking customized direct marketing
  - Example: User bought gardening tools, you want to provide recommendations on the next one to buy
- same technology used by Amazon.com
- Amazon S3 or Amazon Personalize API -> read data -> Amazon Personalize -> Customize personalized API -> integrate with email, sms, apps, Websites

# Amazon Textract

- Automatically extracts text, handwriting and data from any scanned document using AI and ML
- Driver License -> Amazon Textract -> result (JSON)
- Extract data from forms and tables
- Read and process any type of documents (PDFs, images)
- Use cases:
  - Finantial services (invoices, finantial reports)
  - Healthcare (medical records, insurance claims)
  - Public sector (tax forms, ID documents, passports)

# Summary

- Rekognition: face detection, labeling, celebrity recognition
- Transcribe: audio to text (ex: subtitles)
- Polly: text to audio
- Translate: translations
- Lex: build conversational bots - chatbots
- Connect: cloud contact center
- Comprehend: natural language processing
- SageMaker: machine learning for every developer and data scientist
- Forecast: build highly accurate forecasts
- Kendra: ML-powered search engine
- Personalize: real-time personalized recommendations
- Textract: extract text and from documents
