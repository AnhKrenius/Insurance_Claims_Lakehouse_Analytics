# Performance Benchmark Summary

Gold-layer Delta tables were benchmarked before and after optimization.

## Optimization Techniques
- OPTIMIZE
- ZORDER on CustomerID and PolicyNumber
- File compaction
- Metadata cleanup

## Results
| Metric | Improvement |
|------|------------|
| Read Queries | 61% faster |
| Filter Queries | 74% faster |
| Aggregations | 64% faster |

Benchmarking was performed using Databricks Spark jobs on the FactClaim table.
