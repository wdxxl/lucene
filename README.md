lucene-core & lucene-grouping 3.5.0


### Check Cycle
```
cycle_finder src/main/java/org/apache/lucene/*.java src/main/java/org/apache/lucene/analysis/*.java src/main/java/org/apache/lucene/analysis/standard/*.java src/main/java/org/apache/lucene/analysis/standard/std31/*.java src/main/java/org/apache/lucene/analysis/tokenattributes/*.java src/main/java/org/apache/lucene/collation/*.java src/main/java/org/apache/lucene/document/*.java src/main/java/org/apache/lucene/index/*.java src/main/java/org/apache/lucene/messages/*.java src/main/java/org/apache/lucene/queryParser/*.java src/main/java/org/apache/lucene/search/*.java src/main/java/org/apache/lucene/search/function/*.java src/main/java/org/apache/lucene/search/grouping/*.java src/main/java/org/apache/lucene/search/payloads/*.java src/main/java/org/apache/lucene/search/spans/*.java  src/main/java/org/apache/lucene/store/*.java  src/main/java/org/apache/lucene/util/*.java  src/main/java/org/apache/lucene/util/fst/*.java  src/main/java/org/apache/lucene/util/packed/*.java >> result.log
```
