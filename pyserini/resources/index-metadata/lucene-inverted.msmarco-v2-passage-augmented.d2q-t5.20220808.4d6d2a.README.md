# msmarco-v2-passage-augmented-d2q-t5

Lucene index of the MS MARCO V2 augmented passage corpus, with doc2query-T5 expansions.

Note that there are two variants:

+ `msmarco-v2-passage-augmented-d2q-t5` (26G uncompressed): stores term frequencies only, which supports bag-of-words queries, but no phrase queries and no relevance feedback. There is no way to fetch the raw text.
+ `msmarco-v2-passage-augmented-d2q-t5-docvectors` (111G uncompressed): stores term frequencies and the docvectors, which enables pseudo-relevance feedabck.

These indexes were generated on 2022/08/08 at Anserini commit [`fbe35e`](https://github.com/castorini/anserini/commit/4d6d2a5a367424131331df2a8e9e00e6a9c68856) on `damiano` with the following commands:

```bash
nohup target/appassembler/bin/IndexCollection -collection MsMarcoV2PassageCollection \
  -generator DefaultLuceneDocumentGenerator -threads 18 \
  -input /scratch2/collections/msmarco/msmarco_v2_passage_augmented_d2q-t5/ \
  -index indexes/lucene-index.msmarco-v2-passage-augmented-d2q-t5.20220808.4d6d2a/ \
  -optimize \
  >& logs/log.msmarco-v2-passage-augmented-d2q-t5.20220808.4d6d2a.txt &

nohup target/appassembler/bin/IndexCollection -collection MsMarcoV2PassageCollection \
  -generator DefaultLuceneDocumentGenerator -threads 18 \
  -input /scratch2/collections/msmarco/msmarco_v2_passage_augmented_d2q-t5/ \
  -index indexes/lucene-index.msmarco-v2-passage-augmented-d2q-t5-docvectors.20220808.4d6d2a/ \
  -storeDocvectors -optimize \
  >& logs/log.msmarco-v2-passage-augmented-d2q-t5-docvectors.20220808.4d6d2a.txt &
```

In May 2024, indexes were repackaged to adopt a more consistent naming scheme.
