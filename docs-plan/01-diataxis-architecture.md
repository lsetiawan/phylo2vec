# Diátaxis Documentation Architecture

This document outlines the proposed documentation structure following the [Diátaxis framework](https://diataxis.fr/), which organizes documentation into four distinct categories based on user needs.

---

## The Four Documentation Types

| Type | Purpose | User Mode | Content Type |
|------|---------|-----------|--------------|
| **Tutorials** | Learning-oriented | Studying | Lessons |
| **How-To Guides** | Task-oriented | Working | Steps |
| **Reference** | Information-oriented | Working | Facts |
| **Explanation** | Understanding-oriented | Studying | Discussion |

---

## Proposed Directory Structure

```
docs/
├── index.md                          # Landing page with quick overview
│
├── tutorials/                        # LEARNING-ORIENTED
│   ├── index.md                      # Tutorials overview
│   ├── getting-started.md            # First steps (installation + first tree)
│   ├── core-concepts.ipynb           # Understanding vectors/matrices (NEW)
│   ├── demo.ipynb                    # Comprehensive demo (MOVE from root)
│   ├── working-with-newick.ipynb     # Newick conversions tutorial (NEW)
│   └── tree-statistics.ipynb         # Computing distances/statistics (NEW)
│
├── how-to/                           # TASK-ORIENTED
│   ├── index.md                      # How-to guides overview
│   ├── convert-formats.md            # Convert between Newick/edges/ancestry
│   ├── manipulate-trees.md           # Add/remove leaves, reroot
│   ├── compare-trees.md              # Compute distances, statistics
│   ├── optimize-trees.md             # Run HillClimbing/GradME
│   ├── work-with-datasets.md         # Load built-in datasets
│   ├── use-cli.md                    # Command-line interface guide
│   ├── integrate-with-ete.md         # Integration with ETE toolkit
│   └── large-scale-trees.ipynb       # Working with large trees (NEW)
│
├── reference/                        # INFORMATION-ORIENTED
│   ├── index.md                      # Reference overview
│   ├── api/
│   │   ├── index.rst                 # Full API reference (EXPANDED)
│   │   ├── base.rst                  # Conversion functions
│   │   ├── io.rst                    # I/O functions
│   │   ├── stats.rst                 # Statistics functions
│   │   ├── utils.rst                 # Utility functions
│   │   ├── opt.rst                   # Optimization classes
│   │   └── datasets.rst              # Dataset functions
│   ├── cli.md                        # CLI reference
│   ├── file-formats.md               # Supported file formats
│   └── glossary.md                   # Terminology glossary
│
├── explanation/                      # UNDERSTANDING-ORIENTED
│   ├── index.md                      # Explanation overview
│   ├── phylo2vec-representation.md   # The math behind Phylo2Vec (NEW)
│   ├── ordered-vs-unordered.md       # Ordered vs unordered trees (NEW)
│   ├── algorithm-complexity.md       # O(n log n) algorithms explained (NEW)
│   ├── architecture.md               # Rust core + Python/R bindings
│   └── design-decisions.md           # Why certain choices were made
│
├── optimization/                     # Optimization-specific section
│   ├── index.md                      # Optimization overview
│   ├── demo_opt.ipynb                # Existing optimization demo (MOVE)
│   ├── hill-climbing.md              # Hill-climbing method explained
│   └── gradme.md                     # GradME method explained
│
├── development.md                    # Development guide (EXISTS)
├── installation.md                   # Installation guide (EXISTS)
├── CONTRIBUTING.md                   # Contributing guide (EXISTS)
├── changelog.md                      # Version history (NEW)
└── citation.md                       # How to cite (NEW)
```

---

## Updated Table of Contents (`_toc.yml`)

```yaml
format: jb-book
root: index
parts:
  - caption: Getting Started
    chapters:
      - file: installation
      - file: tutorials/getting-started

  - caption: Tutorials
    chapters:
      - file: tutorials/index
      - file: tutorials/core-concepts
      - file: tutorials/demo
      - file: tutorials/working-with-newick
      - file: tutorials/tree-statistics

  - caption: How-To Guides
    chapters:
      - file: how-to/index
      - file: how-to/convert-formats
      - file: how-to/manipulate-trees
      - file: how-to/compare-trees
      - file: how-to/optimize-trees
      - file: how-to/work-with-datasets
      - file: how-to/use-cli
      - file: how-to/integrate-with-ete
      - file: how-to/large-scale-trees

  - caption: Optimization Methods
    chapters:
      - file: optimization/index
      - file: optimization/demo_opt
      - file: optimization/hill-climbing
      - file: optimization/gradme

  - caption: Explanation
    chapters:
      - file: explanation/index
      - file: explanation/phylo2vec-representation
      - file: explanation/ordered-vs-unordered
      - file: explanation/algorithm-complexity
      - file: explanation/architecture

  - caption: API Reference
    chapters:
      - file: reference/index
      - file: reference/api/index
      - file: reference/cli
      - file: reference/file-formats
      - file: reference/glossary

  - caption: Development
    chapters:
      - file: development
      - file: CONTRIBUTING
      - file: changelog
      - file: citation
```

---

## Section Details

### Tutorials Section

**Purpose**: Help newcomers learn Phylo2Vec through hands-on lessons.

| File | Description | Target Audience |
|------|-------------|-----------------|
| `getting-started.md` | Installation and first tree in 5 minutes | Complete beginners |
| `core-concepts.ipynb` | Deep dive into vector/matrix representation | Users wanting to understand internals |
| `demo.ipynb` | Comprehensive walkthrough of all features | All users |
| `working-with-newick.ipynb` | Converting between formats | Users with existing tree files |
| `tree-statistics.ipynb` | Computing tree metrics | Researchers doing analysis |

### How-To Guides Section

**Purpose**: Provide step-by-step instructions for specific tasks.

| File | Solves This Problem |
|------|---------------------|
| `convert-formats.md` | "How do I convert my Newick file to Phylo2Vec?" |
| `manipulate-trees.md` | "How do I add/remove leaves or reroot my tree?" |
| `compare-trees.md` | "How do I compute distances between trees?" |
| `optimize-trees.md` | "How do I infer a tree from sequence data?" |
| `work-with-datasets.md` | "How do I use the built-in datasets?" |
| `use-cli.md` | "How do I use the command-line interface?" |
| `integrate-with-ete.md` | "How do I visualize trees with ETE?" |
| `large-scale-trees.ipynb` | "How do I work with trees with 10,000+ leaves?" |

### Reference Section

**Purpose**: Provide complete, accurate technical information.

| File | Content |
|------|---------|
| `api/index.rst` | Complete API reference with all functions |
| `api/base.rst` | Conversion functions (newick, ancestry, edges, pairs) |
| `api/io.rst` | I/O functions (load, save) |
| `api/stats.rst` | Statistics functions |
| `api/utils.rst` | Utility functions |
| `api/opt.rst` | Optimization classes |
| `api/datasets.rst` | Dataset functions |
| `cli.md` | CLI command reference |
| `file-formats.md` | Supported file formats specification |
| `glossary.md` | Terminology definitions |

### Explanation Section

**Purpose**: Provide conceptual understanding and background.

| File | Explains |
|------|----------|
| `phylo2vec-representation.md` | The mathematical bijection between trees and vectors |
| `ordered-vs-unordered.md` | The difference between tree representations |
| `algorithm-complexity.md` | Why operations are O(n log n) using AVL/Fenwick trees |
| `architecture.md` | How Rust core + Python/R bindings work together |
| `design-decisions.md` | Why the library is designed this way |

---

## Landing Page (`index.md`)

```markdown
# Phylo2Vec Documentation

**Phylo2Vec** is a high-performance Python library for encoding, manipulating,
and analyzing binary phylogenetic trees using a compact integer vector
representation.

## Why Phylo2Vec?

- **Compact**: Represent any tree topology with n leaves using just n-1 integers
- **Fast**: Rust core enables processing trees with millions of leaves
- **Flexible**: Convert between Newick, edge lists, ancestry matrices, and more
- **Analytical**: Compute cophenetic distances, covariance matrices, and more
- **Inference-ready**: Built-in optimization methods for tree search

## Quick Example

\`\`\`python
import numpy as np
from phylo2vec import sample_vector, to_newick, from_newick

# Sample a random tree with 5 leaves
v = sample_vector(n_leaves=5)
print(f"Vector: {v}")  # e.g., array([0, 2, 5, 1])

# Convert to Newick format
newick = to_newick(v)
print(f"Newick: {newick}")  # e.g., ((0,(1,3)5)6,(2,4)7)8;

# Convert back to vector
v_back = from_newick(newick)
assert np.array_equal(v, v_back)  # Round-trip preserves the tree
\`\`\`

## Getting Started

- [Installation](installation.md)
- [Quick Start Tutorial](tutorials/getting-started.md)
- [API Reference](reference/api/index.rst)

## Citing Phylo2Vec

If you use Phylo2Vec in your research, please cite:

**The paper:**
> Penn, M.J. et al. "Phylo2Vec: a vector representation for binary trees."
> *Systematic Biology*, 2024. [DOI: 10.1093/sysbio/syae030](https://doi.org/10.1093/sysbio/syae030)

**The software:**
> Scheidwasser, N. et al. "phylo2vec: a library for vector-based phylogenetic
> tree manipulation." *Journal of Open Source Software*, 2025.
> [DOI: 10.21105/joss.09040](https://doi.org/10.21105/joss.09040)
```
