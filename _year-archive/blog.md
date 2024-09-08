---
title: "Paper Title Number 3"
collection: publications
permalink: /publication/2015-10-01-paper-title-number-3
excerpt: 'This paper is about the number 3. The number 4 is left for future work.'
date: 2015-10-01
venue: 'Journal 1'
paperurl: 'http://academicpages.github.io/files/paper3.pdf'
citation: 'Your Name, You. (2015). &quot;Paper Title Number 3.&quot; <i>Journal 1</i>. 1(3).'
---

# Retrieval Augmented Generation

## Motivations 

1. Large Language models are not  aware about all of the data that you may care about (your personal data - may be LLM are not pretrained over it)
2. LLMs could be a center piece. and there is a ==need of connecting== LLMs to external data

## Stages of RAG

Given a Query
1. Stage 1 : Indexing Some external Document
2. Stage 2 : Retrieving the relevant document
3. Stage 3: Passing through the LLM to generate the response

## Components of RAG

### Stage 1 : Indexing

**Given** : A Query and ton of documents
**Task** : Given the query and documents find the most relevant part of the documents.
**Output** : Relevant part of document to the given query

![[Indexing.png]]
**Important Questions to be aware about**
1. How measure the ==Similarity==?
2. LLMs have limited context size .. ==can't fit== whole document to model?
3. How to ==split== the Corpora?
4. How to decide for ==embedding model==?

**Working?**
1. Embed the Documents into embedding space
2. Embed the query into the embedding space
3. Do similarity search to find relevant splits

![[Embed_space.png]]
### Stage 2 : Retrieval

Given Query and Ton of documents
1. Embed the Query into the embedding space
2. Do the same for the all the documents and embed in the embedding space
3. Do a similarity search in the local neighborhood
4. Return the the similar to documents

This whole task mentioned above is what is done by ==**Vector Store**== in modern frameworks like ==Langchain== and ==Langsmith==.

![[Retrieval.png]]
Things that we need : 
1. Embedding Models
2. Document Loaders
3. Splitters for the input

### Stage 3 : Generation

1. Take the retrieved documents
2.  Feed to context of Language models
3.  Generate the output

Input : Prompt (Query + Relevent Documents)
Output : Answer from the LLms

## Coding My Own RAG

### Steps

#### Text Preprocessing
1. Splitting into Pages
2. Splitting Pages into sentences
	 - Split on the ". " (already done)
	 - Split with NLP library (spacy, nltk)
	 - Maintain a dictionary of following things 
			Character count Page
			Word Count  Page
			Sentence Count Page
			Token Count  Page
			Actual Text
	 - Splitting/Chunking could be done into group of 10 sentences (arbitrary), also we can overlap the sentences (use LangChain)
		

### Questions
1. Why is it important to check for the number of tokens / page. (Because Embedding and Language Models don't have Infinite context size)
