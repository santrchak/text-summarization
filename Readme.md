	  _____                       _      
	 / ____|                     (_)     
	| (___   _   _  _ __ ___      _  ___ 
	 \___ \ | | | || '_ ` _ \    | |/ __|
	 ____) || |_| || | | | | | _ | |\__ \
	|_____/  \__,_||_| |_| |_|(_)| ||___/
								_/ |     
							   |__/      

Sum.js
============

[![Build Status](https://secure.travis-ci.org/topliceanu/text-summarization.png)](http://travis-ci.org/topliceanu/text-summarization)

A simple function for summarizing text e.g. for automatically determining the sentences that are most relevant to the context of the corpus.
This library depends on the [underscore](http://documentcloud.github.com/underscore/), [underscore.string](http://epeli.github.com/underscore.string/) and [porter-stemmer](https://github.com/jedp/porter-stemmer) for the moment

Install in node.js
==================
	sudo npm install -g sum

Install in browser
==================
	<script src="/lib/underscore.js"></script>	
	<script src="/lib/underscore.string.js"></script>	
	<script src="/lib/porter-stemmer.js"></script>
	<script src="/sum.browser.js"></script>
	

Quick Start
===========
	var sum = require( 'sum' );
	var bigString = "....";
	var abstract = sum({ 'corpus': bigString });
	

Further Options
===============
	var sum = require( 'sum' );
	var anotherBigString = "...";
	var abstract = sum({
		/**
		 * `corpus`: String - is the string you want to summarize
		 */
		'corpus': anotherBigString,

		/** 
		 * `nSentences`: Number - controls the number of sentences from the original text included in the abstact
		 */
		'nSentences': 3,

		/** 
		 * `nWords`: Number - controls the length in words of the nGram output. Output might be larger as some words are ignored in the algorithm but present in the abstract, for ex. prepositions. When `nWords` is set, `nSentences` is ignored
		 */
		'nWords': 5,
		
		/**
		 * `exclude`: Array[String] - sum.js allows you to exclude from the final abstract, sentences or nGrams that contain any of the words in the `exclude` param
		 */
		'exclude': ['polar', 'bear'], 

		/**
		 * `emphasise`: Array[String] - forces sum.js to include in the summary the sentences or nGrams that contain any the words specified by `emphasise` param.
		 */
		'emphasise': ['magic'] 
	});


Running tests
=============
Run /tests/browser/specrunner.html in your favourite browser.

To run node tests, make sure you have [vows.js](http://vowsjs.org) installed then run

	vows ./tests/node/sum.js 


Goals
=====

This library is intended to be fully `embeddable`. It's purpose is to be used primarly on the `client-side`. 
It should be `self-contained` so no API calls to external services.
It should be as `light` as possible, both in terms of code size and dependencies and above all it must be `fast`.
Because of these constraints, the algorithm used is purely statistical, using [TF IDF](http://en.wikipedia.org/wiki/Tf*idf) to calculate abstracts.
Other methods of text summarization proposed by researchers in [NLP](http://en.wikipedia.org/wiki/Natural_language_processing) and [ML](http://en.wikipedia.org/wiki/Machine_learning) produce better results but are not (to my best of knowledge) practical in the browser context as many of them require intense computation to produce their output.

	
TODO
====
1. add tests to verify the correctness of the actual output
2. currenty the output does not preserve the ending chars of the original sentences
3. make the lib more plugable, e.g allow plugin of custom algorithms, string cleaning rutines, etc.
4. better control for the length of the summary, by words, by letters
5. add more algorithms to calculate abstracts
6. Make the library's inner utility functions available as some of them might be usefull


Licence
=======

(The MIT License)

Copyright (c) 2009-2011 Alex Topliceanu <alext@vibetrace.com>

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
