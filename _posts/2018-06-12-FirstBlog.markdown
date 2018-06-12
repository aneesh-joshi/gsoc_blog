---
layout: post
title:  "Welcome to Jekyll!"
date:   2018-06-12 16:43:19 +0530
categories: jekyll update
---
<p>I am writing this blog to chronicle my activities and progress as I go about my project for Google Summmer of Code(GSOC), 2018.</p>

<h3>Introduction to my project, Similarity Learning with Neural Networks: </h3>
<p>Similarity Learning tries to develop a function which can measure the similarity between two objects. For example, given two questions, what is the likelihood that they are the same or given a question-answer pair, what is the similarity between them. The advantage of these models is that they abstract the internal representations of their inputs and provide outputs as a simple cosine similarity value between the vectors of its inputs.
Several Similarity Learning models exist, but considering the recent success of deep learning techniques, the project is focusing mainly on the Neural Network based models.</p>

[caption id="attachment_10822" align="aligncenter" width="1320"]<img src="https://rare-technologies.com/wp-content/uploads/2018/05/dssm.png" alt="Example of a similarity learning model, Deep Structured Semantics Model (DSSM)" width="1320" height="554" class="size-full wp-image-10822" /> Example of a similarity learning model, Deep Structured Semantics Model (DSSM)[/caption]

<h3>Community Bonding Period:</h3>
<p>I utilized the Community Bonding period to develop the easiest model I could find in my list of SL models, <a href="https://www.microsoft.com/en-us/research/publication/learning-deep-structured-semantic-models-for-web-search-using-clickthrough-data/" target="_blank">Deep Structured Semantic Model (DSSM)</a>. Luckily, my work was made a lot easier by this awesome repository, <a href="https://github.com/faneshion/MatchZoo" target="_blank">MatchZoo</a>, which has implemented a lot of models and benchmarked them. In fact, MatchZoo was a big influence in my proposal for GSOC. Writing the code for extracting data from the datasets and training a simple model gave me a good feel for the things ahead. The code for this can be found in <a href="https://github.com/RaRe-Technologies/gensim/pull/2050">this </a> PR.</p>

<h3>First 2 weeks of GSOC:</h3>
<p>The first meeting I had with my mentors, <a href="https://github.com/menshikh-iv" target="_blank">Ivan Menshikh</a> and <a href="https://github.com/mandroid6" target="_blank">Mandar Deshpande</a>, set a clear idea for what was needed to be done: </p><p><blockquote>I have to build a script which can evaluate the "goodness" of any given model and then work on developing the best model based on the evaluations made by this script.</blockquote></p><p>This goodness can be measured in terms of metrics like Mean Average Precision(MAP), Normalized Discounted Cumulative Gain(nDCG), etc. </p>
<p>Although MatchZoo had already released scripts to evaluate these metrics and their corresponding benchmarks, it was necessary to cross check it on my own machine. Unfortunately, not all the benchmarks were getting reproduced. For example, some of the outputs I got were half of what they had published. I quickly opened an <a href="https://github.com/faneshion/MatchZoo/issues/103">issue</a> on their repo and they've gone about fixing the bug.</p>
<p>This exercise, however, made me question the credibility of any code not written by me. Ivan had insisted from the beginning that I make my own script and I finally realized the need for it.</p>
<p>The next few days went in understanding the metrics involved in evaluating the models and the corresponding code in MatchZoo. I needed a script which would give in query data, get the results and grade them through the metrics. It was made a bit more challenging because I had to translate my data to a format the model understands.</p>

<h4>The Evaluation script should do the following:</h4>
[caption id="attachment_10838" align="aligncenter" width="749"]<img src="https://rare-technologies.com/wp-content/uploads/2018/05/eval_script_pipeline2.png" alt="Evaluation Pipeline" width="749" height="387" class="size-full wp-image-10838" /> Evaluation Pipeline[/caption]

<p>Since each model has it's own way of representing the data, we need to translate the data format for it to understand. For example, my input data is <code>"hello world"</code>, but the model might have a word-int dicitonary which will translate it to <code>[45, 32]</code></p>

<p>After digging through some more MatchZoo code, I realized that they are saving their outputs in a file after running on the test data. This meant, I can directly take their outputs and run my scripts! They were saving the output in the <a href="https://trec.nist.gov/trec_eval/" target="_blank">TREC</a>(Text REtrival Conference) format and I wrote a script which went through it and scored it. Fortunately, my results and the MatchZoo results were quite close.</p>

<p>It was also decided that as a control case, we will bench mark unsupervised algorithms like word2vec and doc2vec. Word2Vec gave okayish results while doc2vec gave fabulous results! In fact, doc2vec was too good to be true. Only later did I realize that I had trained and tested the model on the same dataset! This small mistake on my side could have lead to some inconsistent results later. I am glad that I caught it early, fear that there are more bugs like it  and pray that I find them if they exist.</p>

<h3>Week 3:</h3>
<p>Currently, I have a full bench marking of all the models using my <a href="https://github.com/aneesh-joshi/gensim/blob/28fa12f185e137dcd6e4634c2ae454f502e0eba2/gensim/similarity_learning/evaluation_scripts/evaluate_models.py">evaluation script</a> whose results are shown below. This presents a good list of models to implement and tune. In deciding which model to use, we checked their metrics scores, time taken to train and memory required. From the current data, it looks like DRMM_TKS gives the best results with acceptable time-to-train and memory. In this week, I will go about implementing this model.</p>
[caption id="attachment_10833" align="aligncenter" width="1113"]<img src="https://rare-technologies.com/wp-content/uploads/2018/05/ranged-benchmarks-mz.png" alt="results of my evaluation script." width="1113" height="409" class="size-full wp-image-10833" /> the table shows the results of my evaluation script.[/caption]
<h3>My Thoughts and Conclusion:</h3>
<p>The last few weeks have been intense! It has been up and down with me getting stuck on some parts and then having a sudden breakthrough. The project is definitely interesting and could be very useful for people who work in this space. I just hope I am able to keep an acceptable pace and do it justice. I look forward to the next few weeks!</p>

