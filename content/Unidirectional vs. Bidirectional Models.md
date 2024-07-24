The main difference lies in how they read and utilize context during training and inference: unidirectional models focus on preceding context, while bidirectional models use both preceding and following contexts to understand language more comprehensively.
### Unidirectional Models

- **Processing Direction**: These models process text in one direction only, typically from left to right.
- **Contextual Understanding**: They generate predictions based on the context that precedes a given word. For example, when predicting the next word in a sentence, they only consider the words that come before it.
- **Examples**: OpenAI's GPT (Generative Pre-trained Transformer) is a prominent example of a unidirectional model. It reads text from left to right to predict the next word in a sequence.
- **Usage**: Suitable for tasks like text generation where the future context isn't known at prediction time.
- "Such restrictions are sub-optimal for sentence-level tasks, and could be very harmful when applying fine-tuning based approaches to token-level tasks such as question answering, where it is crucial to incorporate context from both directions." (BERT)

### Bidirectional Models

- **Processing Direction**: These models process text in both directions, meaning they consider both the left and right contexts of a word simultaneously.
- **Contextual Understanding**: They generate predictions based on the full context of a sentence or passage. This allows for a more comprehensive understanding of the text.
- **Examples**: BERT (Bidirectional Encoder Representations from Transformers) by Google is a well-known bidirectional model. It reads text in both directions to understand the context of each word.
- **Usage**: Suitable for tasks requiring a deeper understanding of context, such as question answering and named entity recognition.