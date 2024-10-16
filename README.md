-   [A Tipping Point – VIDI Project](#a-tipping-point-vidi-project)
    -   [1. Algorithm to visually explore the factors associated with
        climate change
        adaptation](#algorithm-to-visually-explore-the-factors-associated-with-climate-change-adaptation)
    -   [2. Database of articles about individuals’ and societies’
        factors associated with climate change
        adaptation](#database-of-articles-about-individuals-and-societies-factors-associated-with-climate-change-adaptation)
        -   [Validating the data using
            ASReview](#validating-the-data-using-asreview)
        -   [Cleaning the text and adding the articles’ researchers’
            affiliation and researched
            countries](#cleaning-the-text-and-adding-the-articles-researchers-affiliation-and-researched-countries)
    -   [3. Two applications of the algorithm and the
        database](#two-applications-of-the-algorithm-and-the-database)
        -   [(a) Patterns in Reported Adaptation Constraints: Insights
            from Peer-Reviewed Literature on Flood and Sea-Level
            Rise](#a-patterns-in-reported-adaptation-constraints-insights-from-peer-reviewed-literature-on-flood-and-sea-level-rise)
        -   [(b) Incremental and Transformational Climate Change
            Adaptation Factors in Agriculture Worldwide: A Natural
            Language Processing Comparative
            Analysis](#b-incremental-and-transformational-climate-change-adaptation-factors-in-agriculture-worldwide-a-natural-language-processing-comparative-analysis)

In this repository, you will find a summary of all the projects where I
was involved as a post-doc at [TU Delft](https://www.tudelft.nl/en/tpm),
Netherlands.

# A Tipping Point – VIDI Project

**Abstract** Climate change is one of the most pressing topics of the
21st century. As the time to mitigate its possible impacts has passed,
now it is important that individuals and societies start to adapt. This
makes the study of individuals’ and societies’ drivers and constraints
to climate change adaptation of paramount importance, but so far there
is a lack of standardized information to analyze such topics worldwide.
To fill this gap, we designed a pipeline to derive databases using
peer-reviewed articles’ text. We use Machine Learning and Natural
Language Processing to extract the articles’ findings. Then, we derived
a database that, later, we used to perform descriptive and statistical
analyses of climate change adaptation to floods and sea-level rise, as
well as, to study farmers’ incremental and transformational adaption
worldwide. We argue that the use of transparent methodologies to derive
data from text is increasingly necessary as, in general, the amount of
literature grows exponentially.

The main three outcomes for this project are:

1.  An algorithm to visually explore the factors associated with climate
    change adaptation.
2.  A database of articles about individuals’ and societies’ factors
    associated with climate change adaptation.
3.  Usage of the algorithm and the database to study two different
    climate change topics: (a) adaptation to floods and sea-level rise,
    and (b) farmers’ incremental and transformational adaptation to
    climate change.

In the following sections I further elaborate on them.

**Acknowledgments** This work was supported by the Netherlands
Organization for Scientific Research NWO VIDI grant number 191015. This
is the main project to which I was part of. For it, I worked together
with the [SC3](http://www.sc3.center/) members: [Prof. Tatiana
Filatova](http://www.sc3.center/team/tatiana-filatova/) (Principal
Investigator) and the PhD candidates [Thorid
Wagenblast](http://www.sc3.center/team/thorid-wagenblast/) and [Joos
Akkerman](http://www.sc3.center/team/joos-akkerman/).

## 1. Algorithm to visually explore the factors associated with climate change adaptation

**Abstract** The fast-growing number of research articles makes it
problematic for scholars to keep track of the new findings related to
their areas of expertise. Furthermore, linking knowledge across
disciplines in rapidly developing fields becomes challenging for complex
topics like climate change that demand interdisciplinary solutions. The
rise of machine learning-supported text analysis has been instrumental
in processing thousands of articles. Yet, how text relationships are
built remains a Black-Box for domain experts, making it difficult to
relate connected concepts to existing theories conceptualizing
cause-effect relationships and permitting hypothesis building and
testing. This paper presents an approach to sensibly use Natural
Language Processing by extracting variable relations and synthesizing
their findings using networks while relating to key concepts dominant in
relevant disciplines. As an example, we apply our methodology to analyze
farmers’ adaptation to climate change and compare the results with
mainstream text summarization methods. Furthermore, we validate our
methodology by asking experts to score and compare the outcomes. Results
show that using Natural Language Processing and networks descriptively
offer an interpretable way to synthesize literature review findings that
outperform mainstream text summarization methods. This methodology gives
not only the direction and the frequency of the association between the
words but also the frequency the word appears in the articles, which is
instrumental when performing literature reviews.

This work is currently under revisions in a journal. The working paper
can be accessed [here](https://arxiv.org/abs/2306.09737) and the codes
to reproduce and replicate the work are
[here](https://github.com/SofiaG1l/NLPnetworks4LR).

## 2. Database of articles about individuals’ and societies’ factors associated with climate change adaptation

The data for our two applications comes from Scopus (ELSEVIER, 2023).
The data was retrieved in two batches: during the last week of August
2022, and during the last week of January 2024. We derived the data from
articles that were about human adaptation to climate change and that
belonged to the categories: Multidisciplinary, Social Sciences, Arts and
Humanities, and Environmental Science. For both batches, we searched for
articles related to adaptation to climate change using search terms
related with climate change (e.g. “climat\[a-z\]\* change”,“…”).

### Validating the data using ASReview

The first data batch was retrieved during the last week of August 2022,
resulting in 30,000 articles. As not all of the articles were about the
studied topic (factors associated with undertaken CCA measures), we
needed to categorize the articles as “relevant” or “irrelevant.” For
this, we organized a labeling session where, besides us, eight PhD
candidates experts in CCA participated. To simplify labelers work, we
performed a Non-Negative Matrix Factorization on the articles’ titles
and abstracts and then give the labelers the articles corresponding to
one cluster.

Using the articles clustered in that way, we categorized 5% of the
articles as relevant or irrelevant to the study of CCA using ASReview
(ASReview LAB developers, 2022). To train the participants, we explained
the problem to them and we showed them several examples of the type of
articles’ abstract that were useful to our study (Appendix B). In terms
of the active learning classifier, we used the following settings:
feature extraction technique – TF-IDF; classifier – Naïve Bayes; query
strategy – Mixed (95% Maximum and 5% Random); and balance strategy –
Dynamic resampling (Double). The labeling session lasted 4 hours and, at
the end, we had 1600 labeled articles where 33% were relevant.

To classify the rest of the articles, we trained a simple perceptron
classifier with a Binary Cross Entropy and Sigmoid loss function
(BCEWithLogitsLoss function from the python package PyTorch (PyTorch,
n.d.)). We split the labeled database into 64% training, 16% validation,
and 20% test sets. The model had 79% accuracy and resulted in 2438
articles classified as related to human adaptation to climate change.

To validate that the 2438 articles were about human adaptation to
climate change and that they talked about the possible drivers and
constraints, we (together with a student assistant and two PhD
candidates) read the abstracts from the articles and when the article
was relevant we downloaded its pdf. This final step took between
December 2022 and February 2023, and resulted in the retrieval of around
842 articles.

The second data batch was retrieved during the last week of January
2024. For this, we constraint the search to articles published between
August 2022 and January 2024. This resulted in 10279 articles. To
categorize the data as relevant and irrelevant, we used the 842 articles
obtained for the first batch to update the simple perceptron classifier
with a Binary Cross Entropy and Sigmoid loss function. This gave us 548
articles, which we manually validated and downloaded their pdfs. The
second batch of data consists of 253 articles.

### Cleaning the text and adding the articles’ researchers’ affiliation and researched countries

To clean the text, we followed the steps 1 to 4 showed and explain in
[our algorithm article](https://arxiv.org/abs/2306.09737). In this step,
we also add the authors’ affiliation and the articles’ researched
countries. The authors’ affiliation was extracted from Scopus metadata.
The articles researched countries were extracted coding an algorithm
that uses sentences’ Name-Entity-Recognition (NER) together with the
“en\_core\_web\_trf” spaCy model (spaCy, n.d.-a) to extract the
articles’ Geopolitical entity (GPE), Locations (LOC), and Nationalities
(NORP). The algorithm tries to identify the country based on the GPE,
LOC, and NORP. It follows the next sequence. It starts in the title, if
it does not find the country based on the GPE, LOC, and NORP, then it
moves to the abstract. Finally, if it does not find the country neither
in the title nor in the abstract, then it looks for the region (such as,
North America, Sub-Saharan Africa) using regex. By doing this, we
identified all the authors’ affiliation and 83% of the countries and
regions studied. We validated the results by manually checking 22% of
the articles.

The codes to reproduce and replicate the work are
[here](https://github.com/SofiaG1l/Data_CCA).

## 3. Two applications of the algorithm and the database

### (a) Patterns in Reported Adaptation Constraints: Insights from Peer-Reviewed Literature on Flood and Sea-Level Rise

**Abstract** Understanding which climate change adaptation constraints
manifest for different actors – governments, communities, individuals
and households – is essential, as adaptation is turning into a matter of
survival. Though rich qualitative research reveals constraints for
diverse cases, methods to consolidate knowledge and elicit patterns in
adaptation constraints for various actors and hazards are scarce. We
fill this gap by analyzing associations between different adaptations
and actors’ constraints in adaptation to climate-induced floods and
sealevel rise. Our novel approach derives textual data from
peer-reviewed articles (published before February 2024) by using natural
language processing, supervised learning, thematic coding books, and
network analysis. Results show that social capital, economic factors,
and government support are constraints shared among all actors. With
respect to adaptation types, communities are frequently associated with
maladaptation, while individuals and households are frequently
associated with transformational adaptation.

This work is currently in the second round of revisions in a journal.
The working paper can be accessed
[here](https://osf.io/preprints/socarxiv/3cqvn). The codes to reproduce
and replicate the work are
[here](https://github.com/SofiaG1l/FloodSLR_CCA). The final database
that results from the analysis is stored in DANS under:

-   Gil-Clavel, Sofia; Filatova, Tatiana, 2024, “Interrelated Climate
    Change Adaptation Measures and Factors”,
    <https://doi.org/10.17026/SS/PYZCXK>, DANS Data Station Social
    Sciences and Humanities, DRAFT VERSION;
    FloodsSLRDataFrame\_Phase1.csv \[fileName\].

### (b) Incremental and Transformational Climate Change Adaptation Factors in Agriculture Worldwide: A Natural Language Processing Comparative Analysis

**Abstract** Climate change is expected to adversely affect agriculture
worldwide. This is especially true if farmers fail to at least
incrementally adapt early in the twenty-first century, and fail to
pursue the transformational adaptation necessary to withstand future
climate changes. Many publications discuss the underlying mechanisms of
autonomous adaptation to climate change using quantitative, qualitative,
and mixed methods. However, the review of empirical evidence on
adaptation is usually performed on articles with quantitative data using
metanalysis, omitting much of the vast body of literature evidence based
on qualitative work. We address this gap by performing a comparative
analysis of factors associated with farmers’ climate change adaptation
in both quantitative and qualitative literature using Natural Language
Processing and generalized linear models. By retrieving publications
from Scopus, we derive a database with metadata and associations from
both quantitative and qualitative findings. We use the derived data as
input for generalized linear models to analyze whether farmers’ climate
change adaptation factors differ by type of adaptation (incremental
vs. transformational) and across different regions of the world. Results
show that factors related to informal institutions’ adaptive capacity
are more likely to be associated with transformational adaptation than
with incremental adaptation. Regarding world regions, results highlight
uneven access to income and infrastructure, with farmers in high-income
countries having an advantage, whereas farmers in low- and middle-income
countries require these the most for effective adaptation to climate
change.

This work is currently in the second round of revisions in a journal.
The working paper can be accessed
[here](https://osf.io/preprints/socarxiv/3dp5e) and the codes to
reproduce and replicate the work are
[here](https://github.com/SofiaG1l/Farmers_CCA). The final databases
that result from the analysis is stored in DANS under:

1.  Gil-Clavel, Sofia; Filatova, Tatiana, 2024, “Interrelated Climate
    Change Adaptation Measures and Factors”,
    <https://doi.org/10.17026/SS/PYZCXK>, DANS Data Station Social
    Sciences and Humanities, DRAFT VERSION; FarmersDataFrame\_Phase1.csv
    \[fileName\].

2.  Gil-Clavel, Sofia; Filatova, Tatiana, 2024, “Interrelated Climate
    Change Adaptation Measures and Factors”,
    <https://doi.org/10.17026/SS/PYZCXK>, DANS Data Station Social
    Sciences and Humanities, DRAFT VERSION;
    FarmersDataFrame\_Phase2\_AllConnections.csv \[fileName\].
