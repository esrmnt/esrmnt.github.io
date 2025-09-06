---
layout: post
title: "RAG: Information Retrieval - How Does Search Actually Work?"
date: 2025-09-05 23:40:00 +0000
tags:
- rag
- ai
---

So, you want to build a Retrieval-Augmented Generation (RAG) system—something that can answer questions by pulling in the right info from your own documents, not just what it “knows” from training. But how does your RAG system actually *find* the right stuff to feed the AI? That’s where Information Retrieval (IR) comes in. This post is your friendly guide to the search techniques powering RAG, with practical tips for making your system smarter and more helpful.

### Why Is Search So Tricky in RAG?

When you’re building a RAG system, you’re not just searching the web—you’re searching your own messy, real-world data. People ask questions in all sorts of ways, your documents might be PDFs, emails, or notes, and you need to find the right info *fast* so your AI can generate a good answer. No single search trick is enough. That’s why RAG systems use a mix of clever techniques—each with its own superpowers and quirks.

### The Three Big Ideas in RAG Search

#### 1. Keyword Search: The Old Reliable

Let’s start with the classic. In a RAG system, keyword search is like Ctrl+F on steroids. It looks for documents that have the *exact* words your user typed. It doesn’t care about word order or meaning—just whether the words are there.

##### How Does It Work in RAG?

Imagine every document and query as a giant checklist of words. If your user asks, “How do I reset my router?” the search engine checks which docs have those words. The more matches, the better. This is often your first line of defense for technical or fact-based queries.

##### TF-IDF: Smarter Word Counting

But not all words are equal! “Router” is more important than “the.” That’s where TF-IDF comes in:

- **TF (Term Frequency):** How often does a word show up in a document?
- **IDF (Inverse Document Frequency):** How rare is that word across *all* your docs?

So, rare and relevant words get a boost. The formula looks fancy, but the idea is simple: reward documents that use your special words, not just common ones.

##### BM25: The Upgrade

BM25 is like TF-IDF’s cooler, more practical cousin. It:
- Doesn’t over-reward documents that repeat a word a million times
- Adjusts for document length (so long docs aren’t unfairly punished)

You can even tweak how much you care about word frequency or length. In RAG, BM25 is a go-to for fast, reliable retrieval.

**Why Use Keyword Search in RAG?**

*Pros:*
- Super fast and reliable
- Easy to understand and debug
- Always finds exact matches (great for troubleshooting or FAQs)

*Cons:*
- Misses synonyms (“car” vs “automobile”)
- Can’t handle different word forms
- Needs the *exact* words to work


#### 2. Semantic Search: When Meaning Matters in RAG

What if you want your RAG system to “get” what the user means, not just what they type? Enter semantic search! Instead of matching words, it matches *ideas*.

##### How Does It Work in RAG?

Semantic search uses AI models to turn your docs and queries into “embeddings”—fancy math representations that capture meaning. If two pieces of text mean the same thing (even if the words are different), their embeddings will be close together. So, “How do I reset my router?” and “Router reset instructions” will be seen as similar!

##### Why Is This Cool for RAG?

- Finds synonyms and related ideas (great for user questions in their own words)
- Handles paraphrasing (“troubleshoot wifi” vs “fix wireless connection”)
- Works across languages and writing styles

But…
- It’s slower and needs more computing power
- Sometimes it misses the importance of exact words (not ideal for legal or technical docs)
- The results can feel a bit mysterious (“Why did it pick *that*?”)

#### 3. Metadata Filtering: The Bouncer at the Door (for RAG)

Sometimes, your RAG system needs to filter results by things like date, author, or document type. That’s where metadata filtering comes in. Think of it as a bouncer who only lets in documents that meet certain rules (“Only show me docs from this year!”).

It’s super fast and great for narrowing things down, but it can’t rank results by relevance or understand content. It just follows the rules you set. In RAG, it’s often used to pre-filter your doc set before running the heavier searches.

### Hybrid Search: Why Not Both in RAG?

Here’s the secret sauce for RAG: the best systems mix and match all these methods! Hybrid search means you get the precision of keywords, the smarts of semantic search, and the filtering power of metadata—all working together to find the best context for your AI to use.

How? Usually, your RAG pipeline runs keyword and semantic searches in parallel, filters the results, and then combines them using clever math (like Reciprocal Rank Fusion, which basically rewards results that show up high on both lists).

You can even adjust how much weight to give each method, depending on your use case. It’s like tuning your own RAG search engine!

### How Do We Know If RAG Search Is Good?

You built a RAG system—how do you know it’s finding the right stuff for your AI to answer well? That’s where evaluation comes in. Some common ways to measure RAG search quality:

- **Precision:** Of the results you got, how many were actually useful for answering the question?
- **Recall:** Of all the useful info out there, how much did you find?
- **Precision@K:** How good are the *top* results? (Because your AI usually only sees the top few!)
- **MAP and MRR:** Fancier ways to reward systems that put the best answers right at the top.

In practice, you’ll use a mix of these to tune and test your RAG system. And don’t forget: real user feedback is gold!

### Building RAG Search in the Real World

Some practical stuff to keep in mind for a RAG system:

- **Keyword search** is cheap and fast
- **Semantic search** needs more resources (think: GPUs, vector databases)
- **Hybrid search** is a balancing act—trade speed for quality as needed

Tips for RAG:
- Precompute as much as possible (like embeddings)
- Cache popular results
- Use “approximate” search for huge datasets
- Always test with real queries and real people

### What’s Next for RAG Search?

RAG and search are moving fast! New models, better indexing methods, and smarter hybrid techniques are popping up all the time. Things to keep an eye on, but then the search isn’t magic — I suppose it’s a mix of smart tricks, old and new. 