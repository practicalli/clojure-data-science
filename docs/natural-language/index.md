# Natural Language Processing Introduction

Natural language processing comprises of a set of computational techniques to understand natural languages such as English, Spanish, Chinese, etc.

Natural Language Processing (NLP) consists of a set of algorithms and tools so that machines can make sense of data available in natural (human) languages such as English, German, French, etc. Although there are traces of NLP research since a long time ago, the concept got well defined in the 1950s, with the breakthrough research work of Alan Turing and Noam Chomsky.

The primary objectives are:

* Understand and implement NLP techniques for sentiment classification, information retrieval (search engines) and topic modeling.

* Understand and implement NLP techniques for uncovering text syntax and structure. That is, predicting part-of-speech tags, parse tree structure, named-entities like people and places, etc.

* Understand and implement NLP techniques for some non-traditional topics such as language identification, spelling correction, and creating word clouds.

* Understand and implement deep learning methods for NLP (also called Deep NLP), and apply them to text generation and language translation. These methods represent the state-of-the-art for advanced tasks such as language translation, question answering, speech recognition and music composition and power systems like the Google Assistant and Amazon Alexa.


## What is Natural Language?

Natural language refers to the medium in which humans communicate with each other. This could be in the form of writings (text) for example emails, articles, news, blogs, bank documents, etc or speech for example lectures, speeches, audio calls, etc. There are trillions of web pages full of natural text, so imagine the scale of data available today.

NLP algorithms often model the hierarchical structure of natural language i.e. characters form words, words form phrases, phrases form sentences, sentences form paragraphs, and paragraphs form documents.

## Applications of NLP

Common NLP applications and use cases:

Document Classification deals with classifying textual documents and assigning it one or multiple categories. Example applications include, classifying news articles into categories like sports, politics, business, technology, etc, or segregating different types of invoices and sales deeds in a large company.

Document Clustering is used to find similar documents and segregate them to form groups. Documents that are closely related will be part of the same group. Example applications include finding similar questions that have already posted in a forum, or finding new published medical research related to a patient's symptoms.

Sentiment Analysis is used to classify text for different sentiments ranging from negative to neutral to positive. This is commonly used to understand customer opinions from product reviews or their posts on social media.

Document Summarization helps to extract the most important and central ideas in a document. For example, one could train a model to summarize a 3000 word article to 200 words. This allows the reader to save time and get the gist, and is often useful for news, research papers, etc.

Named Entity Recognition, also known as entity extraction, identifies named entities and classifies them into categories such as person, organization, location, etc. Such a system can be used by stock investors to follow news corresponding to companies they have invested in, or to get news relating to your favorite sports players and teams from across various news sources.

Question Answering systems are intelligent systems that generate responses to the questions being asked by the user. Such systems often use facts and rules stored in their knowledge base. Many conversational AI and personal assistant solutions (for example Amazon Alexa) are able to perform question answering.

Machine Translation is the task of automatically translating from one natural language to another. This is the task Google translate is performing when you visit a website that is written in a language you do not understand.

## Components of NLP

There are 2 main components of natural language processing - natural language understanding, and natural language generation.


### Natural Language Understanding (NLU)
NLU enables machines to understand the intent or the meaning of the text. The different levels of analysis that NLU requires are as follows:

Morphological Analysis is the analysis of the structure of individual words. A morpheme is defined as the "minimal unit of meaning". For example, the words "care", "cares", "caring", "careless", "careful", "uncaring" are different forms of the same word, with stem "care". Also note that the structure of a word could include a prefix ("un-" in "uncaring") or a suffix ("-less" in "careless").

Syntactic Analysis (also called parsing) involves analysis of words in the sentence for grammar. For example, syntactic analysis is used by Microsoft Word, Google Docs, etc to highlight phrases with incorrect grammar.

Semantic Analysis uses morphological and syntactic knowledge to understand the meaning, intent and purpose of the text as a whole. For example, consider the two sentences "I went to the market in my shorts" vs "I went to the market in the city". In terms of grammar (syntax) the two sentences are equivalent. However, based on semantics (meaning), we know that "in my shorts" refers to "I", whereas "in the city" refers to the "market". Semantic analysis is necessary since grammar leaves a lot of ambiguity, and we implicitly rely on a shared understanding of the world to communicate with each other.

Discourse Analysis is a more advanced stage of NLU where we perform syntactic or semantic analysis in a longer piece of text. That is, the analysis is performed over a paragraph or an entire document, as opposed to a single sentence.


### Natural Language Generation (NLG)

Once the machine understands the natural language, NLG is used to respond in natural language, or to produce written text. Recent applications include chat-bots and personal assistants like Alexa and Siri. In general, NLG systems are more complex than NLU. Some approaches to NLG are:

Content Determination involves deciding what information we need to convey in the generated text. There are pre-built schemas or templates to specify the content. Using knowledge-based rules and pattern detection, the words in these templates are predicted. For example, when Google Assistant is asked the age of a person, it responds "{person_name} is {age} years old. {He/She} was born on {date}."

Planning / Micro-planning involves finding, mixing and merging different sentence representations into more concise representation. For example, if the predicted response for an input is a set of 3 sentences - "Larry is feeling sleepy", "Larry is drinking coffee" and "Coffee is hot", a better concise representation would be "Since Larry is sleepy, he is drinking hot coffee".

Deep Learning is a subfield within machine learning which has proven very successful in applications that require language generation, such as translation and question answering. The last section of this course covers Deep Learning methods for NLP. Whereas the above two approaches involve lots of hand-crafted rules, deep learning can be used in an 'end-to-end' fashion.

## Challenges in NLP

The properties and nature of natural language bring many challenges to NLP. A few of these are discussed below:

Assumed knowledge / common sense: By far the biggest challenge in NLP is that anytime we communicate, we have an inherent assumption about the knowledge the reader has. Even though this knowledge might seem very basic for a human, a computer does not have access to such knowledge. When we say "Fox jumped over the fence" vs "Fox jumped over the building" vs "Fox jumped over the leaf", we know that the first is sensible, second is not possible, and third is too insignificant (and hence weird) to mention. All of this depends on our understanding of a fox, a fence, a leaf, etc.

Volume: A huge amount of text is available online, and in documents within organizations. This large amount of data is a great bonus for machine learning approaches to NLP, but at the same time, it requires our solutions to be computationally efficient.

Variation: Natural language is infinitely wide in terms of vocabulary, dialects, etc. Understanding all these different types of languages and variations in dialects makes NLP much harder than having one standardized language across the globe.

Complex: The way concepts link together to convey meaning is often quite complex for an algorithm to understand. For example, a large percentage of words have different meaning depending on the context in which they are used. Words like "set" and "run" have more than 300 definitions depending on context (homonyms). Consider the word "having" in "Adam is having coffee" vs "Adam is having a good time".

Grammar is vague: Sometimes grammatical rules are not well defined, and often, there are exceptions to grammatical rules. Grammar also leaves ambiguity in possible meanings. We saw this in the "I went to the market" example above. Another example is, "Robert really likes Michael. He is such a charming personality." Based on grammar alone, it is not possible to know whether "he" refers to "Robert" or "Michael".

Expressions: Emotions or sarcasm in written text have proven quite difficult for an algorithm to understand. The literal meaning for "I work 40 hours a week to be this poor" is very different from the intended meaning.

## Approaches to NLP
Broadly there are 3 different ways to approach any problem in NLP.

Computational Linguistics
It is the mathematical or scientific study of language. In this approach, classical linguists devised various language rules for grammar, part-of-speech, etc. The NLP algorithms are based on discrete mathematics such as automata, probability, and co-occurrence statistics of words. Most of the theories given by Noam Chomsky were based on computational linguistics.

## Machine Learning
In machine learning approach, the text data is converted to a numerical vector. These vectors could be based on the frequency of words or how they co-occur with neighbouring words. One such meaningful representation is tf-idf, which we'll see in the next tutorial.

Once the text is transformed to vectors, machine learning algorithms such as Naive Bayes', Support Vector Machine, etc. can be used to classify text data or perform other tasks.

Machine learning methods for NLP have now become so popular that they have mostly taken over computational linguistics. The fact that substantial amount of text is now available to train accurate models is an important contributing factor to this development. The other factor for inclination towards machine learning is that rule-based systems are difficult to scale because the exclusive hand-crafted rules are required for each natural language, while machine learning can be adopted easily across different languages.

## Deep Learning
Deep learning is a subfield of machine learning focused on training models that are more complex and flexible than traditional machine learning models. These methods have achieved state-of-the-art results in problems such as translation and question answering. The increase in processing power and availability of large amounts of textual data has enabled us to train deep neural networks and achieve high accuracy.

## Conclusion
In the upcoming tutorials, we will encounter many of the applications, approaches and challenges described in this article. Wishing you a happy journey in exploring natural language processing. :)

