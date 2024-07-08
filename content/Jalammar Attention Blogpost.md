### [Jalammar Attention Blogpost](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
 - Attention mechanism visualization: [[seq2seq_7.mp4]]
 - Encoder decoder yapıları kendi içlerinde bir RNN
 - Attention mekanizması özelinde encoder ın her statinde üretilen hidden state değerleri decoder a input olarak veriliyor. Bu hidden state değerleri encoder'ın her bir kelime için attention değerlerini içeriyor.
 - Decoder ilk EOS tokenini input olrak alıyor. Her bir time intervalda bir önceki hidden state outputu ile encoder hidden state değerlerini kullanarak decode ediyor.
 - 

