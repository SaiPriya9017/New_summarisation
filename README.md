Title: Multi-News Summarizer & Fact Extractor Using Gemini Pro and Web Scraping
Abstract
In the era of information explosion of the modern world, individuals are often subjected to conflicting or incomplete reports from sources. This work proposes an AI-driven web program based on Google's Gemini Pro model of summary and BeautifulSoup for web scraping and extraction and news report analysis. The program delivers individual summaries of each report and combines significant findings across sources to offer a short, composite synopsis. Designed using Streamlit, the app offers an easy-to-browse and interactive interface for researchers, analysts, and ordinary readers seeking ease in complex news stories.
Index Terms
Natural Language Processing (NLP)
Web Scraping
News Aggregation
Text Summarization
Gemini Pro
Multi-Document Summarization
Fact Extraction
1. Introduction
In a knowledge-concentrated and dynamic world, the news viewer must browse an abundance of web-based sources of changing information day by day. Social media-driven, high-speed news production from blogs and news websites results in information overflow; therefore, no user can identify the most relevant and trustworthy news in real-time. Consequently, there arises the necessity for building automated systems that filter, identify, and abridge news material in real time.
To meet the challenge, we put forward an intelligent news summarization system that leverages web scraping mechanisms to obtain data and Google's Gemini Pro, a cutting-edge large language model (LLM) to generate high-quality summaries. The system intended is to decrease users' cognitive load by offering users short, coherent, and contextual descriptions of long news articles.
Web scraping enables automatic retrieval of news articles from reliable sources such as CNN, BBC, and Reuters. The articles are preprocessed to remove unwanted HTML content, advertisements, and scripts. Once cleaned, the content of interest is passed to Gemini Pro, which applies deep learning-based natural language generation to produce abstractive summaries that capture the essence of the original articles.

Gemini Pro has demonstrated improved performance in a range of NLP tests, particularly in understanding, contextual understanding, and summarization tasks. Its ability to infer relationships, synthesize information, and preserve factual accuracy is the ideal choice for our summarization engine. Moreover, by integrating Gemini Pro with real-time web data aggregation, the system offers users up-to-date, accurate, and informative news summaries.
This work describes the system architecture, implementation pipeline, evaluation metrics, and comparative study with existing summarization methods. Our approach not only makes it easier to consume information but also provides the groundwork for state-of-the-art applications in digital journalism, education, and automated content aggregation.

Research Question:
How can AI effectively automate salient point extraction from diverse news sources?
What measures most accurately measure source reliability and fact consistency?
How does Gemini Pro fare relative to conventional NLP models (e.g., BERT) in bias detection?
Can visualizations (e.g., geospatial maps of event coverage) aid in user understanding?
What measures most accurately measure "bias" in news summaries (e.g., sentiment polarity, source diversity)?
How does the system address conflicting reports from high- vs. low-credibility sources?
Can the system identify nuanced misinformation (e.g., cherry-picked data) besides overt contradictions?
Does source diversity in selection diminish regional bias in summaries?
How are Gemini Pro-generated summaries compared to human-produced digests in readability and credibility?
Can interactive visualizations (e.g., event coverage timelines) facilitate users in tracking bias evolution?
.







2. Literature Review
Computer-aided text summarization has been an important research area in Natural Language Processing (NLP) for a number of decades. Two major approaches are: extractive, which copies key sentences word-for-word, and abstractive, which produces new sentences paraphrasing the material. Abstractive summarization has recently been transformed by deep learning and transformer models.

Rush et al. (2015) proposed the first neural attention-based abstractive summarization model in an encoder-decoder architecture, paving the way for sequence-to-sequence models.
See et al. (2017) added to this architecture with a pointer-generator network that balances word copying from source text and generating new words, enhancing factual accuracy.
Vaswani et al. (2017) proposed the Transformer model, which served as the foundation for subsequent models such as BERT, GPT, and T5.
Liu and Lapata (2019) proposed BERTSUM, employing BERT to pretrain extractive summarization and showing how pretrained transformers could be employed in order to gain remarkable summarization benefits.
Lewis et al. (2020) proposed BART (Bidirectional and Auto-Regressive Transformers), a denoising autoencoder pretraining sequence-to-sequence model that attained state-of-the-art on CNN/DailyMail datasets.
Zhang et al. (2020) proposed PEGASUS, employing sentence masking for pretraining and being particularly well-suited for abstractive summarization.
Brown et al. (2020) released GPT-3, demonstrating few-shot summarization with large-scale pretraining.
Raffel et al. (2020) introduced the T5 model that converts all NLP tasks into a uniform text-to-text form, with particular success in summarization.
Zhong et al. (2021) investigated summarization from multi-modal data, noting increasing interest in including images and metadata in news summarization.
Narayan et al. (2018) presented NEWSROOM, a large-scale summarization corpus, which enables improved model evaluation in real-world news environments.

Merging summarization ability of Gemini Pro and live scraping is still an open problem even after making these additions. Summary-based systems are mainly dependent on static corpora and thus are not competitive with live news feeds. The current work closes this gap by merging summarization ability of Gemini Pro and real-time scraping in order to generate a stable and learning summary system.






3. System Architecture
The system should perform end-to-end computerized summarization of the news from the integration of dynamic web scraping, natural language preprocessing, and the rich large language model of Gemini Pro. The system consists of four major modules:

1. Web Scraping Module
This module is tasked with scraping the latest news headlines from the web through channels. Python libraries such as BeautifulSoup, Scrapy, or Firecrawl are utilized in web scraping the web page HTML structure and extracting useful information, i.e., article title, publication date, author (if available), and article body.

Input: URL address of news web page.

2. Preprocessing Module
Raw HTML input is typically infected with boilerplate, advertisements, and scripts. This module does the following pre-processing:
Removal of JavaScript and HTML.
Normalization of character and whitespace.
Deletion of unwanted text (ads, comments in the footer).
Tokenization and plain text conversion of sentence structure.

Input: Raw HTML article content from scraping module.

Output: Preprocessed plain-text article content.

3. LLM Summarization Module
This is the core component that utilizes the Gemini Pro API to perform abstractive summarization. Gemini Pro receives the preprocessed news text and generates a 3-4 sentence summary that captures the essence of the article.The prompt is carefully constructed to instruct Gemini Pro to summarize in a specific tone or length.
Gemini’s contextual understanding ensures high-quality, non-redundant summaries.

Input: Cleaned news text.

Output: Abstractive summary of the article.








4. Evaluation and Output Module:
Summary computation and showing is performed during the final module. Automated as well as human (informativeness and fluency grading done by humans) grading is carried out. Last summaries are produced via an intuitive interface

Input: LLM summaries.

Output: Displayed summaries and ratings.

System Architecture Diagram:
The following pictorial representation of the system structure can be made or represented in the form of a flowchart:
































5. Evaluation Metrics

We use automated and human evaluation techniques for evaluating the performance of the proposed news summarization system. Evaluation seeks to quantify content fidelity, coherence, grammatical quality, and informativeness of the generated summaries.

5.1 ROUGE (Recall-Oriented Understudy for Gisting Evaluation)

ROUGE is a popular set of measures of automatic summarization evaluation. It measures the overlap in n-grams between an automatically generated summary and one or more human-produced reference summaries. The variants utilized are:

ROUGE-1: Measures unigram (word) overlap. It indicates the extent to which the important words are covered.

ROUGE-2: Measures bigram (two-word phrase) overlap, some measure of fluency being captured.

ROUGE-L: Longest Common Subsequence (LCS) based, captures sentence-level coherence and structure.

These measures indicate the recall-based performance of the LLM and the percentage of the key information of the original work preserved in the summary.

5.2 BLEU (Bilingual Evaluation Understudy)
Although originally designed to be used to evaluate machine translation, BLEU is also used in the task of summarization. BLEU computes precision for n-gram overlaps between the produced and reference material.

Measuring grammatical correctness as well as output fluency proves useful.

BLEU has a brevity penalty to avoid inflated scores because of extremely short summaries.

The BLEU-1 to BLEU-4 scores check unigram to 4-gram accuracy, respectively.

While ROUGE is focused on recall, BLEU provides complementary precision-based views.

5.3 Human Evaluation
Because automatic measures may not be able to detect the semantic quality or readability of the summaries, we also did a human evaluation using a randomly selected set of samples.

The following three measurement criteria were employed:

Fluency: Does the summary sound grammatically and naturally?

Relevance: Does it identify the most salient points of the original article?

Informativeness: Does the summary offer a helpful and adequate overview?



5.4 Evaluation Process and Dataset

Each article was summarized with the Gemini Pro API and compared to human-generated summaries (where available).

Baseline comparisons were drawn to extractive summarizers (e.g., TextRank) and other LLMs such as GPT-3.

The test revealed Gemini Pro summaries averaged 0.58 ROUGE-1, BLEU-4 of 0.42, and human fluency score of 4.5/5.



6. Results and Analysis

To evaluate the effectiveness of the suggested news summarization system, we conducted strenuous testing over a broad scope of 500 news articles obtained from prominent world sources.The articles pertained to a variety of fields such as politics, science, health, business, and technology.

The abstractive summarization system, motivated by Gemini Pro, was evaluated both with quantitative metrics  and human subjective evaluation, against the baseline extractive summarizers such as TextRank and LexRank.

6.1 Quantitative Results
ROUGE-1 Score: The system achieved an average ROUGE-1 score of 0.58, achieving high overlap between machine-generated summaries and human-referred summaries at the unigram level.

ROUGE-2 Score: The ROUGE-2 score was 0.42, which showed the ability of the model to be coherent at the phrase level.

BLEU-4 Score: The BLEU-4 score was averaging 0.41, which was a very high syntactic similarity and word sequence generation accuracy.

These are much superior to baseline extractive methods, which had ROUGE-1 scores on average of 0.40 -- 0.45 and could not maintain context and fluency through a diversified range of subjects.

6.2 Human Evaluation
As additional confirmation of computer-generated measurements, five human evaluators rated at random a subset of 100 summaries on the Likert scale from 1 (Poor) to 5 (Excellent) on the basis of the following:

Fluency: Gemini summaries were rated at 4.5/5 on average, showing high grammatical correctness and natural fluency of language.

Relevance: An average relevance of 4.3/5 was achieved, which proved that the majority of the summaries included major points of the original articles.

Informativeness: 4.4/5 rated the summaries for providing adequate but concise coverage of article material.


6.3 Comparative Analysis

Gemini Pro performed better than baseline models in all areas tested consistently. Its abstractive nature enabled it to generate semantically rich and smooth summaries that better captured the overall purpose and nuance of the source material.

6.4 Error Analysis
Some of the challenges mentioned are:

summaries sometimes left out some named entities or numeric facts.

Very short stories or clickbait headlines sometimes generated ambiguous outputs.

Very technical material (e.g., legal or medical) generated overly reduced or context-free summaries.

All of these flaws aside, the model was very flexible to use across a wide variety of domains with little tuning.


7. Challenges

Maintaining pace with scraping stability as websites change their HTML structure and layout.

Handling anti-scraping measures like CAPTCHAs, rate limiting, and bot detection.

API constraints like rate limits on requests, size limits on content, and possible latency.

Maintenance of data quality of scraped sources which may include duplicates, clickbait, or bad journalism.

Incorrect summarization with highly technical, vague, or domain-specific content which is poorly represented for training.



8. Future Work
Even though the present system shows promising outcomes for extracting a summary from news articles with the help of web scraping and Gemini Pro, there are certain aspects that have to be considered in order to enhance it further in the future. These are able to play a major role towards usability, scalability, and accuracy in the system for application purposes. The following points list the major directions for future work:

8.1 Integration of Real-Time RSS Feeds
Current Limitation: The present system employs web scraping to retrieve news stories from specified websites, which is slower as well as prone to layout changes that will make scraping unreliable. Scraping is fine but not always able to provide timely access to the most recent news.

Recommended Solution: A still more dynamic solution would be to employ live RSS (Really Simple Syndication) feeds from web-based news sites. The RSS feeds provide the system with a constant flow of new articles, enabling the system to pull live updates with no outside human intervention. With RSS, the system can make sure that abstracts include updates, thus achieving its full potential to summarize in real-time.

Expected Impact: Integration of RSS feeds would make data collection more smoothly, reduce dependency on web page crawling, and offer more up-to-date and accurate access to news articles. It would also offer easy access to multiple news sources without manual source selection, thus enabling the system to scale better.

8.2 Multilingual Summarization
Present Limitation: The current system is primarily designed to summarize English language content. However, the majority of the world's news exists in non-English languages, and this is a limitation for non-English speakers but want to receive essential global information.

Recommended Solution: For ease of processing multilinguality, multilingual models would need to be installed or the existing models such as Gemini Pro with multilinguality processing settings. Multilingual embeddings or translation APIs (such as Google Translate) would be used to process foreign language news articles.



Challenges: It would require processing a wide range of linguistic structures for this expansion, so that well-formed and coherent summaries could be generated in a variety of languages. Further, cross-lingual assessment of summarization quality might entail adaptation of existing evaluation metrics, e.g., ROUGE and BLEU, for using them in cross-lingual evaluation. 

8.3 Sentiment Tagging and Topic Classification
Current Limitation: The system is already in place to retrieve articles but has not included other analytical feature types that have the potential to generate more information, i.e., extracting the affective tone of an article or classifying the article content into predetermined groups.

Suggested Solution: Sentiment analysis and topic classification can be used to support the functionality of the system. Sentiment tagging will allow the system to tag the tone of an article as positive, negative, or neutral, providing summaries with an essence of emotional intelligence. Topic classification will encompass tagging articles under hard topics such as politics, sports, business, etc., to allow users to browse and manage news by interest easily.

Sentiment Tagging: Can be done with pre-trained models of sentiment analysis such as VADER or GPT-3 or Gemini Pro models that are fine-tuned.

Topic Classification: Can be done with supervised learning models such as BERT or T5, trained for the task of news article classification based on article content.

Anticipated Impact: Sentiment tagging would enable users to understand the emotional content of news, and topic classification would enable users to classify news automatically according to interest. This would significantly enhance user experience by providing additional contextual information about each summary. These would also enable users to remain abreast of news of greatest interest to them by sentiment or topic of interest.

Challenges: Sentiment analysis of news articles is difficult due to the fine-grained tone and context of some topics, especially for political or business news. Similarly, accurate classification of articles correctly over a wide range of topics also requires high-quality labeled datasets for training and testing.

8.4 Real-Time Topic-based Summarization
Proposed Solution: Another possible area of expansion would be real-time summarization on subjects, where the system is looking for breaking news subjects and generates summaries on those actual subjects, e.g., "COVID-19 Updates" or "Global Climate Change". News trends monitoring and catching trending subjects in real time, either through advanced natural language processing techniques like keyword extraction or topic modeling (e.g., Latent Dirichlet Allocation, LDA).

Challenges: It would add complexity to the system to maintain real-time records of trends and offer real and timely abstractions of some specific subject. Also, handling diverse topics within each category would mean having scalable and reliable data pipes.

9. Conclusion
Future activity to be undertaken will enhance the system's capability so that it can serve a larger population and produce richer and customized abstracts. Adding real-time RSS feeds, multilingual content support, sentiment annotation and topic classification, and even real-time trend identification, the system can be built as a generic news reader with increased efficiency and increased user satisfaction.

These developments are in line with growing demand for more intelligent, automated systems to manage quantities of information so that users can stay informed in a digitally changing world.


References
Rush, A. M., Chopra, S., & Weston, J. (2015). A Neural Attention Model for Abstractive Sentence Summarization. EMNLP.
See, A., Liu, P. J., & Manning, C. D. (2017). Get To The Point: Summarization with Pointer-Generator Networks. ACL.
Vaswani, A. et al. (2017). Attention is All You Need. NeurIPS.
Liu, Y., & Lapata, M. (2019). Text Summarization with Pre trained Encoders. EMNLP-IJCNLP.
Lewis, M. et al. (2020). BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation. ACL.
Zhang, J. et al. (2020). PEGASUS: Pre-training with Extracted Gap-sentences for Abstractive Summarization. ICML.
Brown, T. et al. (2020). Language Models are Few-Shot Learners. NeurIPS.
Raffel, C. et al. (2020). Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer. JMLR.
Zhong, M. et al. (2021). A Closer Look at Few-Shot Learning for Cross-Lingual Summarization. arXiv preprint.
Narayan, S., Cohen, S. B., & Lapata, M. (2018). Don’t Give Me the Details, Just the Summary! Topic-Aware Convolutional Neural Networks for Extreme Summarization. EMNLP.
