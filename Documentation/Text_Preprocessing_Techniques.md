# 📝 Text Preprocessing with NLTK: A Beginner's Guide

Welcome to this comprehensive guide on text preprocessing with NLTK (Natural Language Toolkit)! 🚀 This notebook will walk you through various essential text preprocessing techniques, explained in simple terms with easy-to-follow code examples. Whether you're just starting out in NLP (Natural Language Processing) or looking to brush up on your skills, you're in the right place!

NLTK provides a powerful suite of tools for processing and analyzing unstructured text data. Let’s dive into the essential preprocessing steps:

## 1. Tokenization

Tokenization splits text into individual words or sentences.

### Sentence Tokenization

```python
import nltk
nltk.download('punkt')
from nltk.tokenize import sent_tokenize

text = "Hello World. This is NLTK. It is great for text processing."
sentences = sent_tokenize(text)
print("Sentence Tokenization:", sentences)
```

### Word Tokenization

```python
from nltk.tokenize import word_tokenize

words = word_tokenize(text)
print("Word Tokenization:", words)
```

## 2. Removing Stop Words

Stop words are common words that might not be useful for analysis (e.g., "is", "the", "and").

```python
from nltk.corpus import stopwords
nltk.download('stopwords')

stop_words = set(stopwords.words('english'))
filtered_words = [word for word in words if word.lower() not in stop_words]
print("Filtered Words:", filtered_words)
```

## 3. Stemming

Stemming reduces words to their root form by chopping off the ends.

```python
from nltk.stem import PorterStemmer
stemmer = PorterStemmer()
stemmed_words = [stemmer.stem(word) for word in filtered_words]
print("Stemmed Words:", stemmed_words)
```

## 4. Lemmatization

Lemmatization reduces words to their base form (lemma), considering the word’s meaning.

```python
from nltk.stem import WordNetLemmatizer
nltk.download('wordnet')

lemmatizer = WordNetLemmatizer()
lemmatized_words = [lemmatizer.lemmatize(word) for word in filtered_words]
print("Lemmatized Words:", lemmatized_words)
```

## 5. Part-of-Speech Tagging

Tagging words with their parts of speech (POS) helps understand grammatical structure.

```python
nltk.download('averaged_perceptron_tagger')

pos_tags = nltk.pos_tag(lemmatized_words)
print("POS Tags:", pos_tags)
```

## 6. Named Entity Recognition

Identify named entities such as names of people, organizations, and locations.

```python
%pip install numpy

nltk.download('maxent_ne_chunker')
nltk.download('words')
from nltk.chunk import ne_chunk

named_entities = ne_chunk(pos_tags)
print("Named Entities:", named_entities)
```

## 7. Word Frequency Distribution

Count the frequency of each word in the text.

```python
from nltk.probability import FreqDist

freq_dist = FreqDist(lemmatized_words)
print("Most Common Words:", freq_dist.most_common(5))
```

## 8. Removing Punctuation

Remove punctuation from the text.

```python
import string

no_punct = [word for word in lemmatized_words if word not in string.punctuation]
print("Words Without Punctuation:", no_punct)
```

## 9. Lowercasing

Convert all words to lowercase.

```python
lowercased = [word.lower() for word in no_punct]
print("Lowercased Words:", lowercased)
```

## 10. Spelling Correction

Correct the spelling of words.

```python
%pip install pyspellchecker

from nltk.corpus import wordnet
from spellchecker import SpellChecker

spell = SpellChecker()

def correct_spelling(word):
    if not wordnet.synsets(word):
        return spell.correction(word)
    return word

lemmatized_words = ['hello', 'world', '.', 'klown', 'taxt', 'procass', '.']
words_with_corrected_spelling = [correct_spelling(word) for word in lemmatized_words]
print("Words with Corrected Spelling:", words_with_corrected_spelling)
```

## 11. Removing Numbers

Remove numerical values from the text.

```python
lemmatized_words = ['hello', 'world', '88', 'text', 'process', '.']

no_numbers = [word for word in lemmatized_words if not word.isdigit()]
print("Words Without Numbers:", no_numbers)
```

## 12. Word Replacement

Replace specific words with other words (e.g., slang with formal words).

```python
lemmatized_words = ['hello', 'world', 'gr8', 'text', 'NLTK', '.']
replacements = {'NLTK': 'Natural Language Toolkit', 'gr8': 'great'}

replaced_words = [replacements.get(word, word) for word in lemmatized_words]
print("Words with Replacements:", replaced_words)
```

## 13. Synonym Replacement

Replace words with their synonyms.

```python
from nltk.corpus import wordnet

lemmatized_words = ['hello', 'world', 'awesome', 'text', 'great', '.']

def get_synonym(word):
    synonyms = wordnet.synsets(word)
    if synonyms:
        return synonyms[0].lemmas()[0].name()
    return word

synonym_replaced = [get_synonym(word) for word in lemmatized_words]
print("Words with Synonyms:", synonym_replaced)
```

## 14. Extracting Bigrams and Trigrams

Extract bigrams (pairs of consecutive words) and trigrams (triplets of consecutive words).

```python
from nltk import bigrams, trigrams

bigrams_list = list(bigrams(lemmatized_words))
print("Bigrams:", bigrams_list)

trigrams_list = list(trigrams(lemmatized_words))
print("Trigrams:", trigrams_list)
```

## 15. Sentence Segmentation

Split text into sentences while considering abbreviations and other punctuation complexities.

```python
import nltk.data

text = 'Hello World. This is NLTK. It is great for text preprocessing.'

# Load the sentence tokenizer
tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')

# Tokenize the text into sentences
sentences = tokenizer.tokenize(text)

# Print the tokenized sentences
print("Segmented Sentences:", sentences)
```

## 16. Identifying Word Frequencies

Identify and display the frequency of words in a text.

```python
from nltk.probability import FreqDist

lemmatized_words = ['hello', 'hello', 'awesome', 'text', 'great', '.', '.', '.']

word_freq = FreqDist(lemmatized_words)
for word, freq in word_freq.items():
    print(f"{word}: {freq}")
```

## 17. Removing HTML Tags

Remove HTML tags from the text.

```python
%pip install bs4

from bs4 import BeautifulSoup

html_text = "<p>Hello World. This is NLTK.</p>"
soup = BeautifulSoup(html_text, "html.parser")
cleaned_text = soup.get_text()
print("Cleaned Text:", cleaned_text)
```

## 18. Detecting Language

Detect the language of the text.

```python
%pip install langdetect

from langdetect import detect

language = detect(text)
print("Detected Language:", language) # `en` (for English)
```

## 19. Tokenizing by Regular Expressions

Use Regular Expressions to tokenize text.

```python
text = 'Hello World. This is NLTK. It is great for text preprocessing.'

from nltk.tokenize import regexp_tokenize

pattern = r'\w+'
regex_tokens = regexp_tokenize(text, pattern)
print("Regex Tokens:", regex_tokens)
```

## 20. Remove Frequent Words

Remove frequent words (high-frequency words) from a list of tokens.

```python
import nltk

# Input text
text = "Natural language processing is a field of AI. I love AI."

# Tokenize the text
tokens = nltk.word_tokenize(text)

# Calculate the frequency of each word
fdist = nltk.FreqDist(tokens)

# Remove the most common words (e.g., the top 10% by frequency)
filtered_tokens = [token for token in tokens if fdist[token] < fdist.N() * 0.1]

print("Tokens Without Frequent Words:", filtered_tokens)
```

## 21. Remove Extra Whitespace

Tokenize the input string into individual sentences and remove leading or trailing whitespace from each sentence.

```python
import nltk.data

# Text data
text = 'Hello World. This is NLTK. It is great for text preprocessing.'

# Load the sentence tokenizer
tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')

# Tokenize the text into sentences
sentences = tokenizer.tokenize(text)

# Remove extra whitespace from each sentence
sentences = [sentence.strip() for sentence in sentences]

# Print the tokenized sentences
print("Sentences Without Extra Whitespace:", sentences)
```

# Conclusion 🎉

Text preprocessing is a crucial step in natural language processing (NLP) and can significantly impact the performance of your models and applications. With NLTK, you have a powerful toolset that simplifies and streamlines these tasks.

I hope this guide provides you with a solid foundation for text preprocessing with NLTK. As you continue your journey in NLP,

 remember that preprocessing is just the beginning. There are many more exciting and advanced techniques to explore and apply in your projects.

Happy coding! 💻