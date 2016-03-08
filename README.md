11611-proj
==========

Q&A Robot

Our final project for 11-611

Files to execute:
ask.py - Located in src.
answer.py - Located in src.

There are two modules in this project
1. First was the ask program that takes the Wikipedia articles as input and generates a set of questions. 
	a. Used Stanford NLTK sentence segmenter to get a list of sentences. 
	b. The I look for sentence with simple predicate sentences. These represents facts which I can transform into questions. These follow the form NP-VP-Period. 
	c. I also look for Appositions, which is NP followed by another NP separated by comma. This means that the NPs are related. 
	d. Now that I have the predicate sentences, I generate three kinds of questions. 
		i. Binary Question: They are simple yes no questions. To generate these question I invert the position of modal verb and the subject and append a '?' at the end.
		ii. Confounded Binary question: This is same as above but I replace the subjects with its synonym/antonyms taken from word.net relations.
		iii. 'Wh' Questions: I look for specific syntactic structure in the predicate sentences. I used named entity recognition for generating these questions. For that I used stanford NER tagger to identify location, people etc. 
			1) For How question I look for adverbs.
			2) For what questions I look for NPs.
			3) For when questions I look for Location tag by the NER tagger 
		iv. When the appropriate constituent is identified I invert the sentence using the same process as for binary sentences and insert question word in the beginning of the sentences. 
			
2. Second was the answer program which takes Wikipedia articles and a set of questions as input and generates answer. 
	i. For Each I identify the question type. Parsing the question with Stanford parse and seeing the initial labels. This will tell us if the question is binary or 'Wh'. If I am able to determine the type of question then I first invert the subject in question and remove the question word to convert the question to its predicate form. I do this because the predicate form I more likely to be present in the articles. Then I use the co-sine similarity for all the sentences similar to I did for above. I return the sentence with highest value. To verify if the answer was correct or not is yes to implemented. 
	ii. If I am not able to determine the type of question and I scan the document to find the closest sentence to the question. To do this I use co-sine similarity of the tf-idf vector between the question and the sentence. 
