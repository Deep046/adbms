```javascript
db.bankdata.find({Location:"Goa"}).count()
```
753
```javascript 
db.bankdata.find({Location:"Goa"}).explain("executionStats")
```
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'bank.bankdata',
    indexFilterSet: false,
    parsedQuery: { Location: { '$eq': 'Goa' } },
    queryHash: '9770E4A2',
    planCacheKey: '9770E4A2',
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    winningPlan: {
      stage: 'COLLSCAN',
      filter: { Location: { '$eq': 'Goa' } },
      direction: 'forward'
    },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 753,
    executionTimeMillis: 39,
    totalKeysExamined: 0,
    totalDocsExamined: 34000,
    executionStages: {
      stage: 'COLLSCAN',
      filter: { Location: { '$eq': 'Goa' } },
      nReturned: 753,
      executionTimeMillisEstimate: 1,
      works: 34001,
      advanced: 753,
      needTime: 33247,
      needYield: 0,
      saveState: 34,
      restoreState: 34,
      isEOF: 1,
      direction: 'forward',
      docsExamined: 34000
    }
  },
  command: { find: 'bankdata', filter: { Location: 'Goa' }, '$db': 'bank' },
  serverInfo: {
    host: 'MSI',
    port: 27017,
    version: '7.0.6',
    gitVersion: '66cdc1f28172cb33ff68263050d73d4ade73b9a4'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 104857600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 104857600,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted'
  },
  ok: 1
}

```javascript
db.bankdata.createIndex({Location:1})
```
Location_1
```javascript
db.bankdata.getIndexes()
```
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { Location: 1 }, name: 'Location_1' }
]
```javascript
db.bankdata.find({Location:"Goa"}).explain("executionStats")
```
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'bank.bankdata',
    indexFilterSet: false,
    parsedQuery: { Location: { '$eq': 'Goa' } },
    queryHash: '9770E4A2',
    planCacheKey: '264C0465',
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    winningPlan: {
      stage: 'FETCH',
      inputStage: {
        stage: 'IXSCAN',
        keyPattern: { Location: 1 },
        indexName: 'Location_1',
        isMultiKey: false,
        multiKeyPaths: { Location: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { Location: [ '["Goa", "Goa"]' ] }
      }
    },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 753,
    executionTimeMillis: 52,
    totalKeysExamined: 753,
    totalDocsExamined: 753,
    executionStages: {
      stage: 'FETCH',
      nReturned: 753,
      executionTimeMillisEstimate: 6,
      works: 754,
      advanced: 753,
      needTime: 0,
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1,
      docsExamined: 753,
      alreadyHasObj: 0,
      inputStage: {
        stage: 'IXSCAN',
        nReturned: 753,
        executionTimeMillisEstimate: 6,
        works: 754,
        advanced: 753,
        needTime: 0,
        needYield: 0,
        saveState: 0,
        restoreState: 0,
        isEOF: 1,
        keyPattern: { Location: 1 },
        indexName: 'Location_1',
        isMultiKey: false,
        multiKeyPaths: { Location: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { Location: [ '["Goa", "Goa"]' ] },
        keysExamined: 753,
        seeks: 1,
        dupsTested: 0,
        dupsDropped: 0
      }
    }
  },
  command: { find: 'bankdata', filter: { Location: 'Goa' }, '$db': 'bank' },
  serverInfo: {
    host: 'MSI',
    port: 27017,
    version: '7.0.6',
    gitVersion: '66cdc1f28172cb33ff68263050d73d4ade73b9a4'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 104857600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 104857600,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted'
  },
  ok: 1
}
