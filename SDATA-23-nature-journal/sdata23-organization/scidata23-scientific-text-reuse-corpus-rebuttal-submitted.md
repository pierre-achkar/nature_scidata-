# Answer to Reviewers
We organize our response into five main areas of concern to reviewers and address each reviewer comment in turn.

## 1. Operationalization of Text Reuse


> **Reviewer #2**:[...] how reuse is defined? Can you provide examples? Is it more than just cut and paste? 

> **Reviewer #2**: You seem to imply that text reuse is equivalent to similarity [...]. The question I have is how do you know whether it is reuse or written independently? Is there additional context or knowledge you have that can prove a reuse relationship between texts beyond similarity? 

We added a new subsection to the Methods section that addresses the commonly used definition and operationalization of the notion text reuse, and its relation to that of text similarity. 

As per prior work, we distinguish "reuse of words" from "reuse of ideas" and focus on the former, as currently no reliable automatic methods of measuring idea reuse are available. Thus, our operationalization of text reuse relies exclusively on detecting syntactic similarity, where we restrict a positive detection to extremely high similarities, requiring more than one multi-word phrase of length 8 words to co-occur in close proximity within two compared documents to be identified as a case of reuse.

Whether a given case of reuse in a given pair of documents has actually been directly copied from one of the two documents, pasted into the other, and then potentially paraphrased, cannot be discerned in this manner. As argued at the outset of our paper, our goal is not to limit ourselves to this one kind of text reuse, but as many kinds as possible, which may range from folklore turns of phrase to paraphrases to boilerplate to verbatim quotations. As our ongoing analyses have already shown, the reuse found at both ends of this spectrum tends to form clusters of documents where the same or near-duplicate versions of phrases / boilerplate texts / quotations are found. All of these authors will have found the "original" from which they derived their versions in one document or other, or have been told how to write it by a co-author, who in turn has picked them up somewhere.

Singular cases of reused text passages from the main bodies of two documents may be indicative of copy-paste-paraphrase reuse, but even here a manual assessment is necessary to rule out other causal factors. As for the case of two authors idenpendently writing choosing more or less the same phrasing, this becomes more and more unlikely the longer the text gets, which is why we choos a conversative least overlap of multiple co-occurring multi-word phrases of length 8.

Seeing as our document collection does not encompass all scientific publications, but only the subset of open access ones, we cannot rule out the existence of other documents for any singular case from which the authors of each document independently reused. Specifically, we do not consider any case of reuse plagiarism (unless manually judged oterhwise by experts), and more generally explicitly refrain from suggesting the purpose, direction, or legitimacy of reuse, as these aspects cannot be captured by a similarity computation. Yet, we expect that future work will include in-depth assessments of selected cases to investigate their nature which is one of the use cases we had in mind.


> **Reviewer #2**: [...] did you consider to capture reuse beyond the text, e.g. reuse of images, reuse of tables, reuse of ideas, etc.? 

We initially considered to also include structural elements (tables, equations), but quickly realized that this task is by comparison a less reliably to be solved using state-of-the-art methods. The lack of appropriate detection technology (most state-of-the-art approaches are only developed for plain text), and that of tools to reliably extract these artifacts from PDF files foreclose any such analysis at scale.

Covering all the different modalities of artifacts found in scientific publications (images, tables, equations, references) requires the development of entirely new approaches tailored to each of them. Similarly, idea reuse is at present out of reach of reliable state-of-the-art technology, as it relates much more to the notion of intertextuality as studied in the digital humanities than surface-level reuse, which current approaches are not (yet) equipped to accurately pick up on. 

Therefore, we opt to limit the current scope of the dataset to establish a baseline for text-based reuse only. We have highlighted the aforementioned limitations in the text. Nonetheless, we are aware of technology being developed for focused subproblems and specific modalities (e.g., see the efforts of Elisabeth Bik to image falsification), and we do hope, that in the not-too-distant future a new analysis and extension of our dataset will become possible.

> **Reviewer #2**: [...] do you infer anything about the direction of reuse (e.g., which text is the source or target)?  

As mentioned above, and as explained now in the "Data Records" section, our operationalization of text reuse does not allow for an explicitly indication of the direction of reuse, as inferring it is highly error-prone. A heuristic to implicitly infer a direction is going by year of publication (i.e. the direction goes from older to newer publications), which can be applied using the metadata we make available for each case. This is also mentioned in the text now. But as mentioned above, for singular cases we cannot rule out the existence of a document outside our collection which is the true original of the two matching passages of text, nor can we rule out the possibility of a antichronological direction, e.g., when papers are published within months from each other. When looking at cluster of cases, they rather form an directed acyclic graph in the time dimension, going back to some unknown root of reuse. We therefore decided against explicitly marking this in the data, as we believe this heuristic has a non-trivial likelihood of being false and should only be applied with caution.

>  **Reviewer #2**: [...] what happens if blocks are reused from multiple documents. Do you allow for this and reference multiple documents?

Blocks from multiple documents are each added as a single case for every pairwise combination of involved documents; for example, if three texts share the exact same text passage, a total of 3 individual cases would be added to the dataset, and for n documents sharing the same passage (n(n-1))/2. Having the data in this atomic format as opposed to an aggregated version with multiple references in one case allows for efficient postprocessing. Reconstructing the graph is straightforward and we will provide corresponding access software. This (more technical) justification has also been added to the paper.

## 2. Methodological Description

> **Reviewer #1**: The math/symbols and jargon in the text were difficult for a person with no background in computer science [...] It would help if the authors could offer some additional sentences explaining what these concepts mean. 

We have substantially rewritten the Method section of the paper in order to make the explanation of the method more accessible. While technical jargon mathematical notation is still necessary in some places to make our methods transparent and reproducible for other computer scientists researching text reuse detection, we reformulated the overview of the whole process to make it more easy to follow at a conceptual level. Also, in places where notation is inevitable, we added a plain-language description of the process, or an example to ease understanding. 

> **Reviewer #1**: How did the authors limit the comparison to only include papers that were likely to share text? This part, described in 'Text Reuse Detection in Large Document Collections' sounded very vague. How did the authors which papers were likely to share text? [...] In other words, is the section called "source retrieval" the part where the documents are matched first? 

The "Source Retrieval" section indeed specifies how pairs of documents are first identified for further comparison. This is achieved by computing a "fingerprint" for each document, where two documents with sufficiently similar fingerprints are identified as candidate pair for further processing. These fingerprints are constructed using a method that enables us to control the likelihood of missing a pair of documents that actually contains a reuse case and we adjusted this likelihood to be neglible while still saving a significant amout of comparisons. 

This subsequent processing step, i.e. the identification of the exact location of reused text, is described in "Text Alignment". The rewritten overview on the whole process ("Text Reuse Detection in Large Document Collections") as a conceptual overview of the whole process is given first to clarify this process and its properties.

> **Reviewer #1**: What was the minimum set of consecutive words that had to match in order to be counted as a pair? [...]

The minimum consecutive word length is given by the minimum seed length n = 8. The "Technical Validation" section explains how we arrived at this parameter choice. We have expanded the description of this parameter to render its purpose in the overall process more evident.

## 3. Dataset
	
> **Reviewer #2**: Which repositories were used to gather the PDFs? Are these available to download as a part of the dataset (or are they referenced in the metadata [...])? 

PDFs were automatically obtained with web crawling from various sources, including CORE, arXiv, Google Scholar, Semantic Scholar, search engines of University Libraries, etc. Only papers referenced in the CORE dataset are considered in this work, which itself references an original source that can be retrieved. We do not currently offer the collected PDFs for public download due to potential licensing and copyright issues, but are actively searching for a solution to make also this part of our data accessible in the future. For academic use, access to subsets may be shared upon request.

> **Reviewer #2**: You state that you “cross-check and supplement the metadata provided by CORE with additional data from the Microsoft Open Academic Graph” – can you expand on this and say more. How was this done and what additional data was gathered? How were articles matched to the OAG? Using the DOI? 

Matching between the two was conducted using the DOI of an article as unique identifier of both the article and its associated metadata. We added this information to the text. Supplementing in this context means that we add metadata from the OAG that is not already present in the CORE data. The paragraph was reformulated accordingly.

> **Reviewer #2**: It wasn’t clear to me why the dataset only included data up to 2018? 

Only papers up to 2018 are included since we began collecting PDF files starting early 2019. This process relied upon the most recent CORE dataset dump available at that time, which included only publications up to 2018.

> **Reviewer #2**: For this step “we manually map the classification found in the Microsoft Open Academic Graph to the standardized, hierarchical DFG Classification of Scientific Disciplines, Research Areas, Review Boards and Subject Areas” – how was this manual mapping done? How many people did this? Was the process validated? How many categories are there? 

We added a more detailed description of the mapping process as well as a description of the resulting hierarchy. The mapping was carried out independently by three people, with their results being compared and combined into the final mapping. In the few cases where there was disagreement, consensus was reached through discussion between the three annotators as well as double-checking corresponding literature to establish a final gold-standard.

> **Reviewer #1**: The results are provided as two large dataset on Zenodo. The smaller set consisted of just lists of DOIs without annotation of which texts were reused where which seemed not very useful. The larger set - presumably containing the text similarity sets - was provided as a huge file in JSON format and I was not sure how to download this or read it. Could the authors maybe provide an easy-to-review set of e.g. 100 cases of text reuse so I could review these? A plagiarism dataset with only one paper seems not very useful. I would have expected the results to be presented as paper 1 vs paper 2, not just a list of papers. (Reviewer 2)

The Zenodo repository does consists of the mentioned two files. One (`publications.tar.gz`) includes all publications as preprocessed by us (even those for which no reuse cases could be identified) to make our method fully reproducible and serve as baseline for statistical analysis of the identified reuse cases. The other, much larger one(`cases.tar.gz`), contains the actual identified cases in a "Paper A vs. Paper B" format, including the exact matched text parts in each. We revised the "Data Records" section to include a more detailed description of the corpus format and what each of the two files contains. Also, as requested, we include a reviewer sample of 100 randomly drawn cases with the resubmission.

> **Reviewer #1**: On page 4, it says 'first involved publication as a, and to the second as b' - does this mean that paper a is the oldest and paper b the newest?
> 
> **Reviewer #1**: How does the output of the search look like? Does the output define which text is likely to be original, and which is not? 

The paragraph in question was rephrased and extended to more clearly state that no directionality is implied by the denomination (see our corresponding discussion above). The a/b naming is not referring to older/newer, but just to uniquely identify each side of the comparison. We explicitly refrain from establishing a direction in our collected reuse cases (i.e. "a copied from b"), as given the available metadata, this at best could be based on publication time. Since year of publication is (a) not present for all included publications, and (b) is only an insufficient proxy for time of writing, basing a classification on it is error-prone at best. Yet, such a heuristic could be employed for downstream analyses, as the year of publication is present for the majority of the included papers, but we caution to use it only on controlled subsets.

> **Reviewer #2**: Do you ignore any matches from within the same text (e.g., abstract text could repeat content from the article)? 

Yes. Texts are only compared across documents, not within a document itself. This is to limit the dataset to a clearly defined scope of text reuse. This is now explicitly stated in the "Source Retrieval" subsection. However, we see "internal reuse" is an interesting research subject in itself, and natural extension of the work presented here. Our methods and detection code are applicable  without further modification to also detect such cases, and we are currently working on doing this as well.

# 4. Ethics & Bias

> **Reviewer #2**: Are there any ethical issues with the dataset? Should academic authors have the ability to retract articles? Should consent be given by authors? Just because it is open science data doesn’t mean it should be used. What if the data was used unethically? For example, to publicise and target academics who reuse text legitimately? 

> **Reviewer #2**: What other biases may have crept into the creation of the dataset?

> **Reviewer #2**: How representative is the dataset of scientific fields? Are there any collection or sampling biases? 

We added a subsection "Ethical Considerations" to the usage notes that explicitly discusses the ethics and possible bias in both creating and using the dataset. Overall, we took a consensus of best practices for dataset creation into account. Our considerations cover three important areas: (1) privacy of the individuals included in the data, (2) effects of biases on downstream use, and (3) dataset usage for unintended, harmful purposes.


# 5. Miscellaneous

> **Reviewer #1**: The work of Debora Weber-Wulff (not this reviewer!) could be mentioned somewhere - her group has done a lot of work on plagiarism detection, and some credit could be given. 

Selected works of Debora Weber-Wulff supplied ample grounding in the section on the operationalization of text reuse and the distinction between reuse and plagiarism.

> **Reviewer #1**: From my own experience, some review papers consist of many reused sentences, from multiple older sources, and I imagine that a visualization of some kind (e.g. network or heatmap) would show fascinating results. I would personally love to have some part of this tool available to test smaller sets of papers, e.g. a set of 20 papers suspected to be similar, and have an output in a format that would visualize (e.g. highlight) the textual similarities. 

Such a tool is planned as future research on our end, but was, by the instructions given for this journal, out of scope for the data descriptor paper presented here. Moreover, developing an expert system and retrieval tool for this dataset that enables text reuse scholars outside computer science to analyze the data without having to rely on collaborators from computer science to preprocess it, is a new research of its own right.

Although the author guidelines discourage the inclusion of examples, the editors followed the reviewers' suggestions and allowed for them to be included. The "Usage Notes" section now includes several example cases featuring different types of reuse occurring in the corpus.

> **Reviewer #2**: It would have been helpful to include a descriptive summary or profile of the dataset (e.g., age range, average size of articles, etc.). 

> **Reviewer #2**: What is the number of articles across fields, for example? This could be included in a descriptive summary of the dataset. 
 
Including an in-depth analysis of the dataset is explicitly discouraged for articles in this journal as the paper is just meant to be a dataset descriptor.


