NLP_emma
---
Johennie Helton
July, 2025

# emma_ch1_metrics: example nltk-narrative-metrics

Small learning exercise inspired by *Natural Language Processing with Python* (Bird, Klein, Loper).  
Demonstrates tokenization, POS tagging, and a few simple narrative-adjacent metrics on a **public-domain** text.

- A minimal NLTK script that:
  - tokenizes sentences/words
  - POS-tags tokens
  - reports counts (verbs, adverbs, nouns, adjectives)
  - basic frequency + readability-ish numbers



# emma_ch1_diff_dynprg

- Normalization + sentence splits for emma_ch1_en.txt and emma_ch1_back_en.txt
- Dynamic-programming alignment that allows merges/splits, with SBERT embeddings if available, else TF-IDF
- df_aligned with all the deltas and df_pos_aligned for token-level POS shifts
- Matplotlib visuals and “drift” queries


# Findings

Original sentences: 162
Back-translated sentences: 139
100% of original sentences are covered in the alignment (every original sentence has a mapped counterpart in the back text).
The total span of back sentences covered is 139 (meaning all back sentences are used)
1↔1: 102 sentences match directly one-to-one (same sentence boundaries preserved).
many↔1: 27 cases where multiple original sentences got merged into a single back-translated sentence.
1↔many: 5 cases where a single original sentence was split into multiple back sentences.

* The fact that we have **102 one-to-one** matches (≈63%) is a good sign
most sentences survived translation intact enough to align cleanly.

* **27 many-to-one** cases suggest that the translation process often merged consecutive 
sentences into longer ones. This is common when the translator prefers more fluid prose 
in the target language, then the back translation keeps that merged form.

* **5 one-to-many** cases mean a few original sentences were broken up in translation
possibly due to complex clauses being reinterpreted as separate sentences.


# Alignment Examples
1↔1 (showing 5 of 102)
[34] ↔ [36] (cos=0.345)

ORIG: What a pity it is that Mr. Weston ever thought of her!"

BACK: I wish she were here again.

[40] ↔ [42] (cos=0.440)

ORIG: We must begin; we must go and pay wedding visit very soon."

BACK: We shall be always meeting!

[39] ↔ [41] (cos=0.598)

ORIG: "How often we shall be going to see them, and they coming to see us!--We shall be always meeting!

BACK: And you never have strange moods, my dear.”

“How often we shall go and see them, and they will come and see us!

[41] ↔ [43] (cos=0.604)

ORIG: "My dear, how am I to get so far?

BACK: We must begin; we must go and pay them the wedding visit very soon.”

“My dear, how am I to get so far?

[35] ↔ [37] (cos=0.605)

ORIG: "I cannot agree with you, papa; you know I cannot.

BACK: What a pity Mr. Weston ever thought of her!”

“I cannot agree with you, Papa; you know I cannot.

1↔many (showing 5 of 5)
[141] ↔ [121-122] (cos=0.666)

ORIG: "And have you never known the pleasure and triumph of a lucky guess?-- I pity you.--I thought you cleverer--for, depend upon it a lucky guess is never merely luck.

BACK: I pity you. I thought you more clever, for, believe me, a lucky guess is never merely luck.

[124] ↔ [103-104] (cos=0.848)

ORIG: And after such success, you know!--Every body said that Mr. Weston would never marry again.

BACK: And after such success, you know! Everybody said Mr. Weston would never marry again.

[20] ↔ [21-22] (cos=0.869)

ORIG: How was she to bear the change?--It was true that her friend was going only half a mile from them; but Emma was aware that great must be the difference between a Mrs. Weston, only half a mile from them, and a Miss Taylor in the house; and with all her advantages, natural and domestic, she was now in great danger of suffering from intellectual solitude.

BACK: How was she to bear the change? It was true that her friend was going to live only half a mile from them; but Emma was conscious that there must be a great difference between a Mrs. Weston, only half a mile from them, and a Miss Taylor in the house; and with all her advantages, natural and domestic, she was now in great danger of suffering from intellectual loneliness.

[9] ↔ [9-10] (cos=0.872)

ORIG: Sorrow came--a gentle sorrow--but not at all in the shape of any disagreeable consciousness.--Miss Taylor married.

BACK: Sorrow came-a gentle sorrow-but not in the form of any unpleasant consciousness. Miss Taylor married.

[126] ↔ [106-107] (cos=0.941)

ORIG: Mr. Weston, who had been a widower so long, and who seemed so perfectly comfortable without a wife, so constantly occupied either in his business in town or among his friends here, always acceptable wherever he went, always cheerful-- Mr. Weston need not spend a single evening in the year alone if he did not like it.

BACK: Mr. Weston, who had been a widower for so long, and who seemed so perfectly comfortable without a wife, so constantly occupied either in his business in town or among his friends here, always accepted wherever he went, always cheerful. Mr. Weston did not need to spend a single night of the year alone if he did not like it.

many↔1 (showing 5 of 27)
[106-107] ↔ [91] (cos=0.726)

ORIG: The chances are that she must be a gainer." "Well," said Emma, willing to let it pass--"you want to hear about the wedding; and I shall be happy to tell you, for we all behaved charmingly.

BACK: The odds are that she will be better off.”

“Well,” said Emma, willing to let it go, “you want to know about the wedding; and I shall be happy to tell you, because we all behaved charmingly.

[77-78] ↔ [71] (cos=0.805)

ORIG: Not a speck on them." "Well!

BACK: Not a speck.”

“Well!

[85-86] ↔ [77] (cos=0.848)

ORIG: Who cried most?" "Ah!

BACK: Who cried most?”

“Ah!

[88-90] ↔ [79] (cos=0.850)

ORIG: 'Tis a sad business." "Poor Mr. and Miss Woodhouse, if you please; but I cannot possibly say `poor Miss Taylor.' I have a great regard for you and Emma; but when it comes to the question of dependence or independence!--At any rate, it must be better to have only one to please than two."

BACK: It is a sad business.”

“Poor Mr. and Miss Woodhouse, if you please; but I cannot say ‘poor Miss Taylor.' I have a great regard for you and Emma; but when it comes to the question of dependence or independence… At any rate, it must be better to have only one to please than two.

[95-96] ↔ [82] (cos=0.855)

ORIG: "I am afraid I am sometimes very fanciful and troublesome." "My dearest papa!

BACK: “I am afraid I am sometimes very whimsical and troublesome.”

“My dearest Papa!





