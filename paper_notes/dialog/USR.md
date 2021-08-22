# USR: An Unsupervised and Reference Free Evaluation Metric for Dialog Generation

**Unsupervised Reference-free Evaluation Metric**

- Time & resource costly to rely on human judgement for evaluation of language generative models

## Intro

### Standard Auto-Evaluation Metrics

- **BLEU**
- **F-1**
- **METEOR**
- **ROUGE**

These standard auto-evaluation metrics have shortcomings:

1. _One-to-many_ nature of dialogue
2. Human evaluation of dialogue incorporates _multiple_ qualities (appropriateness, interesting, consistency), while automatic metrics condense these characteristics into one _uninterpretable metric_
3. it is difficult to _generalize_ what a _good_ dialogue is.

### USR

Rather than focusing on the _ground truth response_ of a dialogue, USR measures the _desired qualities_ of a good dialogue (appropriateness, consistency, etc.)

### Datasets

- [PersonaChat](https://arxiv.org/pdf/1801.07243.pdf)
- [Topical-Chat](https://m.media-amazon.com/images/G/01/amazon.jobs/3079_Paper._CB1565131710_.pdf)

### Human Analysis

4 Models were used to generate output in response to Topical Chat, while 3 were used for Persona Chat.

In addition to the models, there are the newly human generated response, as well as the original ground truth response.

Annotaters evaluated the responses based on the following categories:

- _Understandable_ (0 - 1): Is the response understandable given the previous context?
- _Natural_ (1 - 3): Does the response seem to be
  something that a person would naturally say?
- _Maintains Context_ (1 - 3): Does the response
  serve as a valid continuation of the preceding
  conversation?
- _Interesting_ (1 - 3): Is the response dull or
  interesting?
- _Uses Knowledge_ (0 - 1): Given the fact that
  the response is conditioned on, how well does
  the response use that fact?
- _Overall Quality_ (1 - 5): Given your answers
  above, what is your overall impression of the
  quality of this utterance?

### Automatic Metrics

- **F-1** - Computs _word overlap_ between generated response and ground truth by taking the harmonic mean of precision and recall.
- **BLEU** - Word overlap metric calculating n-gram precision between generated response and ground truth. brevity penalty to punish shorter sentences (otherwise precision favors shorter sentences). BLEU found to correlate poorly with human judgement.
- **METEOR** - Improvement from BLUE.
- **ROUGE-L** - Identifies largest common subsequence between generated output and reference sequence.
- **Greedy Matching** - Embedding-based - greedily matches each word from the generated output to a reference word based on their cosine similarity (Cosine of the angle between to vectors) of their embeddings. The final score is an average of all these similarities.

- **Embedding Average** - computes _sentence embedding_ for both generated output & reference sentences. Then, the score becomes the cosine similarity of the average embedding for both generated output & references.

- **BERTScore** - Uses a pretrained BERT model to greedily match each word in a reference response to one in the generated outputs - computing the recall of generated sequences. Good for tasks with a _limited_ set of references | bad for _one-to-many_ dialogue tasks.

### Evaluating USR

The metrics of USR were correlated with human evaluations (considered the source of ground truth).

Newly generated human responses scored best in terms

### Random Notes

- **Spearman correlation** - Captures the linear correlation between two variables
- **Pearson correlation** - Captures whether the data can be explained through a monotomic function (only increasing or only decreasing)
