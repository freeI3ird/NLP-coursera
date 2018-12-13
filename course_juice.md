#Course Juice

####Stemming and Lemmitization
1. Stemming and Lemmitization should be done after Spell Checking.
2. **Stemming**: Cuts the suffices from words( suffices: added to make derivatives from a word)
3. **Lemmitization**: Uses the **WordNet** Database to look up for lemmas(root word).
4. E.g: Wolves --> Wolv  **Stemming** and Wolves-->Wolf **Lemmitization**.
5. Try both **Stemming** and **Lemmitization** then choose what works the best.

####Token Normalization
1. Stemming or Lemmitization
2. Capital to lowercase
	- lowercase the beginning of sentences.
    - leave mid-sentence words as they are because they can contain some 		important information e.g Acronyms.
3. Normalize Acronyms
	- eta, e.t.a, E.T.A. --> E.T.A.
	- we can make a list of these acronyms and then normalize them as done 		with E.T.A.

####Text to Feature
#####Bag of Words
	- Count the occurrences of a particular token in our text.
1. We take all the tokens present in our corpus(all the sentences)
2. Each individual text/sentence will be represented as a **vector**,
	where no. of dimensions of vector = no. of tokens consider in step1.
3. So finally we have a matrix where **row = no. of texts in corpus** and **col = size of feature vector/ no. of tokens considered**.
4. This matrix will be a sparsed matrix offcourse.

 ######Problems
    1. Loose word order.
    2. Counters of tokens are not 		Normalized.

 ######Solutions
 1. Preserve ordering: use n-grams.
 	- Too many features due to this
 	- So remove High Frequency n-grams(Articles, prepositions).
 	- Remove Low Frequency n-grams(typos error, rare words)
 	- Keep **Medium Frequency n-grams**.
 		- In medium frequency n-grams those with **Low in frequency** are 		better as they capture some specific detail from the text/document.
	- Frequency of n-grams = no. of documents/text in which token appear/ 		total no. of documents.

 2. Normalize the counters **row-wise** using L-2 Norm or by dividing the 		sum of all counters.

#####Tf-IDF
	- Term Frequency- Inverse Document Frequency
1. Term Frequency
	- frequency of term/n-gram ==t== in document ==d==
	- Measures
		- Binary
		- raw count: **f~t~**
			- no. of occurrences in the document d.
		- term frequency: normalized raw count
			- **f~t~** / (**f~t,1~**+**f~t,2~**+**f~t,3~**+...)
		- log normalization
			- 1 + log(**f~t~**)
			- Say we have two term frequency 1e6 and 1e10, now this shows that both the words are important but if we feed them linearly, machine will learn that one is less important and other more important, but when we feed them on **log scale** both values are not that far and hence the machine will deduce that both are equally important.
2. Inverse Document Frequency
	- ==N== total no. of documents in the corpus |D|
	- |{d->D, t->d}|, total no. of documents in corpus where the term 't' appears.
	- Document Frequency = |{d->D, t->d}| / N
	- **IDF** = N/ |{d->D, t->d}|
	- It tells us the importance of a Term/feature
		- if term appears in very document then it is useless, don't capture any distinguishing information. **IDF** will be low
		- if term appears in few document then **IDF** will be high and it contains some valuable information.

3. TF-IDF = Term-Frequency* Inverse-Document-Frequency
	- It is something like weighing the Term Frequency, it is like: "ok then term/ngram appears many times in our text, but is this Term actually important or not( given by IDF) and how much is its importance( measured by TF-IDF).

4. **USE TF-IDF value in place of counters in Bag of Words**
