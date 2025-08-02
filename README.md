## Frequent Itemset Mining with ECLAT Algorithm

A comprehensive implementation and performance comparison of the ECLAT (Equivalence Class Clustering and bottom-up Lattice Traversal) algorithm using different computational approaches: GPU-accelerated (CuPy) and distributed processing (Apache Spark).

🎯 Project Overview

This project implements three variants of the ECLAT algorithm to analyze their performance characteristics across different data scales and computational paradigms:

- GPU-Optimized ECLAT: Memory-efficient implementation using CuPy with CUDA acceleration.
- GPU-Simple ECLAT: Streamlined GPU implementation focusing on 1-itemsets and 2-itemsets.
- Spark Distributed ECLAT: Distributed processing implementation using Apache Spark RDDs.

📊 Key Results

| Implementation    | Average Runtime | Best Use Case                 |
|-------------------|--------|----------------------------------------|
| Spark Distributed | 8.9s   | Large datasets (>50K transactions)     |
| GPU Optimized     | 26.7s  | Medium datasets (10K-50K transactions) |
| GPU Simple        | 127.4s | Small datasets (<10K transactions)     |

🚀 Features

- Three ECLAT Implementations: Comprehensive comparison across different computational approaches.
- Performance Benchmarking: Runtime and memory usage analysis across multiple data scales.
- Scalability Testing: Evaluation on 20%, 50%, and 100% of the dataset (10K, 25K, 50K transactions).
- Visualization: Automated generation of performance comparison charts.
- Real Dataset: Uses retail transaction data from the FIMI repository.

## 📋 Requirements

### Environment
- Platform: Google Colab (recommended) or local environment with GPU support.
- Python: 3.11+
- GPU: CUDA-capable GPU (Tesla T4 used in testing).

### Dependencies
```bash
pip install cupy-cuda12x
pip install pyspark
pip install matplotlib
pip install psutil
pip install GPUtil
pip install numpy
```

## 🔧 Setup

1. **Open in Google Colab** (recommended)
   - Upload the notebook to Google Colab
   - Upload the retail.dat file to `/content/` directory
   - Run the cell

2. **Download the dataset**
   - Get retail.dat from: http://fimi.uantwerpen.be/data/retail.dat

## 💻 Usage

### Running the Complete Benchmark

```python
# Load and run the main benchmarking function
from eclat_implementations import main
main()
```

### Running Individual Implementations

```python
# Load dataset
data = load_dataset("/path/to/retail.dat", max_transactions=50000)

# Run GPU-optimized ECLAT
gpu_results = run_gpu(data, min_support=100)

# Run Spark ECLAT
spark_results = run_spark(data, min_support=100)

# Run GPU-simple ECLAT
gpu_simple_results = run_gpu_simple(data, min_support=100)
```

## 📈 Performance Results

### Runtime Comparison
- **Small datasets (10K transactions)**: GPU-Simple performs best (2.9s)
- **Medium datasets (25K transactions)**: GPU-Optimized shows good performance (8.5s)
- **Large datasets (50K transactions)**: Spark dominates with consistent performance (7.8s)

### Memory Efficiency
- **GPU implementations**: Consistent ~106-108 MB GPU memory usage
- **Spark implementation**: Gradual increase from 14.4% to 15.7% CPU memory

### Itemset Discovery
- **Spark**: Most comprehensive itemset discovery (2,729 itemsets at 100% scale)
- **GPU-Optimized**: Good coverage with 3-itemset limitation (2,599 itemsets)
- **GPU-Simple**: Limited to 1-2 itemsets (2,039 itemsets)

## 🔬 Technical Highlights

### Algorithm Optimizations
- **Vertical Database Representation**: Efficient TID list storage and intersection
- **GPU Memory Management**: Proactive cleanup to prevent memory overflow
- **Distributed Processing**: RDD-based parallelization with optimal partitioning
- **Scalable Architecture**: Handles datasets up to 50K+ transactions

### Key Innovations
- **Hybrid GPU Approach**: Two GPU variants optimized for different use cases
- **Memory-Efficient Design**: Minimal memory footprint with maximum performance
- **Comprehensive Benchmarking**: Multi-dimensional performance analysis
- **Real-World Dataset**: Evaluation on actual retail transaction data

## 📊 Dataset Information

**Retail Dataset (FIMI Repository)**
- **Source**: http://fimi.uantwerpen.be/data/retail.dat
- **Transactions**: 50,000 retail transactions
- **Items**: 14,414 unique items
- **Average Transaction Length**: 10.22 items
- **Format**: Space-separated item IDs per line

## 🎓 Academic Context

This project was developed as part of a AI and Cloud course assignment, specifically focusing on:
- **Algorithm Implementation**: Hands-on experience with ECLAT algorithm
- **Performance Analysis**: Comparative study across different computational paradigms
- **Scalability Research**: Understanding trade-offs in parallel processing approaches
- **Technical Documentation**: Comprehensive reporting and analysis

## 🙏 Acknowledgments

- **Prof. Damiano Carra, University of Verona ** [Prof. Damiano Carra, University of Verona](https://www.di.univr.it/?ent=persona&id=6412): For suggesting ECLAT algorithm over Apriori for better parallel processing capabilities
- **FIMI Repository**: For providing the retail dataset for evaluation
- **Google Colab**: For providing free GPU resources for experimentation
- **Open Source Libraries**: CuPy, Apache Spark, and other dependencies

---

**Note**: This implementation is primarily designed for educational and research purposes. For production use, consider additional optimizations and error handling.
