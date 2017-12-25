lucene-core & lucene-grouping 3.5.0


### Check Cycle
```
cd /Users/wdxxl/Wdxxl_Github/Github/lucene

cycle_finder src/main/java/org/apache/lucene/*.java src/main/java/org/apache/lucene/analysis/*.java src/main/java/org/apache/lucene/analysis/standard/*.java src/main/java/org/apache/lucene/analysis/standard/std31/*.java src/main/java/org/apache/lucene/analysis/tokenattributes/*.java src/main/java/org/apache/lucene/collation/*.java src/main/java/org/apache/lucene/document/*.java src/main/java/org/apache/lucene/index/*.java src/main/java/org/apache/lucene/messages/*.java src/main/java/org/apache/lucene/queryParser/*.java src/main/java/org/apache/lucene/search/*.java src/main/java/org/apache/lucene/search/function/*.java src/main/java/org/apache/lucene/search/grouping/*.java src/main/java/org/apache/lucene/search/payloads/*.java src/main/java/org/apache/lucene/search/spans/*.java  src/main/java/org/apache/lucene/store/*.java  src/main/java/org/apache/lucene/util/*.java  src/main/java/org/apache/lucene/util/fst/*.java  src/main/java/org/apache/lucene/util/packed/*.java > result.log
```

### [j2Objc_Cycle_Finder工具] @Weak & @WeakOuter
```
规则:
    DocumentsWriter -> (field waitQueue with type WaitQueue)
解决方案:
    @Weak final WaitQueue waitQueue = new WaitQueue();

规则:
  PerDocBuffer -> (outer class DocumentsWriter)
解决方案:
    @WeakOuter
     class PerDocBuffer extends RAMFile {
规则:
    ***** Found reference cycle *****
    DoubleCache -> (superclass Cache has (field wrapper with type FieldCacheImpl))
    FieldCacheImpl -> (HashMap<Class<?>, Cache> subtype of (field caches with type Map<Class<?>, Cache>))
    HashMap<Class<?>, Cache> -> (field table with type Node<Class<?>, Cache>)
    Node<Class<?>, Cache> -> (DoubleCache subtype of (field value with type Cache))
    ----- Full Types -----
    Lorg/apache/lucene/search/FieldCacheImpl$DoubleCache;
    Lorg/apache/lucene/search/FieldCacheImpl;
    Ljava/util/HashMap<Ljava/lang/Class<*>;Lorg/apache/lucene/search/FieldCacheImpl$Cache;>;
    Ljava/util/HashMap$Node<Ljava/lang/Class<*>;Lorg/apache/lucene/search/FieldCacheImpl$Cache;>;
解决方案:
    FieldCacheImpl  ->  @Weak private Map<Class<?>,Cache> caches;
    FieldCacheImpl -> Cache -> @Weak final FieldCacheImpl wrapper;
规则:
    ***** Found reference cycle *****
    anonymous:169 -> (field queue with type SpanQueue)
    SpanQueue -> (superclass PriorityQueue<Spans> has (anonymous:169 subtype of (field heap with type Spans)))
    ----- Full Types -----
    Lorg/apache/lucene/search/spans/SpanOrQuery.1;
    Lorg/apache/lucene/search/spans/SpanOrQuery.SpanQueue;
解决方案:
    PriorityQueue<T> ->  @Weak private T[] heap;
规则:
    ***** Found reference cycle *****
    TermsHashPerThread -> (TermVectorsTermsWriterPerThread subtype of (field consumer with type TermsHashConsumerPerThread))
    TermVectorsTermsWriterPerThread -> (field termsHashPerThread with type TermsHashPerThread)
    ----- Full Types -----
    Lorg/apache/lucene/index/TermsHashPerThread;
    Lorg/apache/lucene/index/TermVectorsTermsWriterPerThread;
解决方案:
    TermsHashPerThread ->  @Weak final TermsHashConsumerPerThread consumer;
    TermVectorsTermsWriterPerThread ->   @Weak final TermsHashPerThread termsHashPerThread;
规则:
    ***** Found reference cycle *****
    OutputStreamDataOutput -> (FileOutputStream subtype of (field os with type OutputStream))
    FileOutputStream -> (field fd with type FileDescriptor)
    FileDescriptor -> (OutputStreamDataOutput subtype of (field parent with type Closeable))
    ----- Full Types -----
    Lorg/apache/lucene/store/OutputStreamDataOutput;
    Ljava/io/FileOutputStream;
    Ljava/io/FileDescriptor;
解决方案:
    OutputStreamDataOutput ->  @Weak private final OutputStream os;
规则:
    ***** Found reference cycle *****
    UpgradeIndexMergePolicy -> (superclass MergePolicy has (field writer with type SetOnce<IndexWriter>))
    SetOnce<IndexWriter> -> (field obj with type IndexWriter)
    IndexWriter -> (UpgradeIndexMergePolicy subtype of (field mergePolicy with type MergePolicy))
    ----- Full Types -----
    Lorg/apache/lucene/index/UpgradeIndexMergePolicy;
    Lorg/apache/lucene/util/SetOnce<Lorg/apache/lucene/index/IndexWriter;>;
    Lorg/apache/lucene/index/IndexWriter;
解决方案:
    MergePolicy -> @Weak protected final SetOnce<IndexWriter> writer;
    SetOnce<T> -> @Weak private volatile T obj = null;
    IndexWriter -> @Weak private MergePolicy mergePolicy;
规则:
    ***** Found reference cycle *****
    TimerThread -> (superclass Thread has (field group with type ThreadGroup))
    ThreadGroup -> (TimerThread subtype of (field threads with type Thread))
    ----- Full Types -----
    Lorg/apache/lucene/search/TimeLimitingCollector$TimerThread;
    Ljava/lang/ThreadGroup;
解决方案:
    暂时没找到
```
