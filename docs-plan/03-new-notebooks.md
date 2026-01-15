# New Jupyter Notebook Topics

This document outlines the proposed new Jupyter notebooks to expand tutorials and increase adoption.

---

## Current Notebooks

| Notebook | Lines | Cells | Coverage |
|----------|-------|-------|----------|
| `demo.ipynb` | 1,194 | 63 | Core functions, conversions, statistics |
| `demo_opt.ipynb` | 508 | ~25 | HillClimbing, GradME optimization |

---

## Proposed New Notebooks

### Priority 1: Essential for Onboarding

#### `tutorials/getting-started.ipynb` - 5-Minute Quick Start

**Purpose**: Get users running with Phylo2Vec in under 5 minutes.

**Target Audience**: Complete beginners

**Estimated Time**: 5-10 minutes

**Outline**:
1. Installation verification
2. Import phylo2vec
3. Sample your first tree
4. Convert to Newick and visualize
5. Convert back to vector
6. Next steps (links to other tutorials)

**Key Functions**: `sample_vector`, `to_newick`, `from_newick`

**Skeleton**:
```python
# Cell 1: Introduction
"""
# Quick Start with Phylo2Vec

In this 5-minute tutorial, you'll learn how to:
- Sample random phylogenetic trees
- Convert between Phylo2Vec vectors and Newick format
- Visualize trees

**Prerequisites**: Python 3.10+ and phylo2vec installed
"""

# Cell 2: Installation check
import phylo2vec as p2v
print(f"Phylo2Vec version: {p2v.__version__}")

# Cell 3: Sample a tree
import numpy as np
np.random.seed(42)
v = p2v.sample_vector(n_leaves=5)
print(f"Phylo2Vec vector: {v}")
print(f"Shape: {v.shape}")

# Cell 4: Convert to Newick
newick = p2v.to_newick(v)
print(f"Newick format: {newick}")

# Cell 5: Convert back
v_back = p2v.from_newick(newick)
assert np.array_equal(v, v_back)
print("Round-trip successful!")

# Cell 6: Next steps
"""
## What's Next?

- [Core Concepts](core-concepts.ipynb): Understand the math behind Phylo2Vec
- [Working with Newick](working-with-newick.ipynb): Load your own tree files
- [Tree Statistics](tree-statistics.ipynb): Compute distances and metrics
"""
```

---

### Priority 2: Core Understanding

#### `tutorials/core-concepts.ipynb` - Understanding Phylo2Vec

**Purpose**: Deep dive into the mathematical foundation of the Phylo2Vec representation.

**Target Audience**: Users wanting to understand internals, researchers

**Estimated Time**: 30-45 minutes

**Outline**:
1. **Introduction**: What is a phylogenetic tree?
   - Binary trees and their properties
   - Why trees matter in biology

2. **The Newick Format**: Standard representation
   - Syntax and parsing
   - Strengths and limitations

3. **The Phylo2Vec Representation**
   - The bijection explained step-by-step
   - Visual walkthrough with diagrams
   - Vector encoding scheme

4. **Ordered vs Unordered Trees**
   - Definitions with examples
   - When to use each
   - Table from existing demo.ipynb

5. **Matrix Format for Branch Lengths**
   - Structure: [topology, branch_child, branch_parent]
   - Examples with conversions

6. **Why Phylo2Vec?**
   - O(n log n) complexity
   - Memory efficiency
   - Applications

7. **Exercises**
   - Hand-trace vector-to-tree conversion
   - Verify understanding with code

**Key Functions**: `sample_vector`, `to_newick`, `to_ancestry`, `check_vector`

---

#### `tutorials/working-with-newick.ipynb` - Newick Conversions

**Purpose**: Master format conversions for integration with other tools.

**Target Audience**: Users with existing tree files, bioinformaticians

**Estimated Time**: 20-30 minutes

**Outline**:
1. **Loading Trees from Files**
   - `load_newick()` function
   - Handling different Newick variants

2. **Converting to Phylo2Vec**
   - `from_newick()` basics
   - With and without branch lengths

3. **Working with Taxon Labels**
   - Creating label mappings
   - `create_label_mapping()` and `apply_label_mapping()`
   - Real taxon names vs integer indices

4. **Converting Back to Newick**
   - `to_newick()` for vectors and matrices
   - Preserving branch lengths

5. **Integration with ETE4**
   - Visualizing trees
   - Round-trip with ete4.Tree

6. **Common Pitfalls**
   - Non-binary trees
   - Malformed Newick strings
   - Branch length precision

**Key Functions**: `from_newick`, `to_newick`, `load_newick`, `save_newick`, `create_label_mapping`, `apply_label_mapping`

---

### Priority 3: Analysis Workflows

#### `tutorials/tree-statistics.ipynb` - Computing Tree Statistics

**Purpose**: Demonstrate statistical analysis capabilities.

**Target Audience**: Researchers performing phylogenetic analyses

**Estimated Time**: 25-35 minutes

**Outline**:
1. **Cophenetic Distance Matrices**
   - Definition and interpretation
   - `cophenetic_distances()` for vectors vs matrices
   - Visualization with heatmaps

2. **Pairwise Distances**
   - Using `pairwise_distances()`
   - Available metrics

3. **Variance-Covariance Matrices**
   - `stats.cov()` function
   - Interpretation in phylogenetics

4. **Precision Matrices**
   - `stats.precision()` function
   - Use in phylogenetic regression

5. **Incidence Matrices**
   - `stats.incidence()` function
   - Sparse representations
   - Linear algebra with trees

6. **Applications**
   - Tree comparison using cophenetic correlation
   - Phylogenetic signal detection
   - Clustering validation

**Key Functions**: `cophenetic_distances`, `pairwise_distances`, `cov`, `precision`, `incidence`

---

### Priority 4: Tree Manipulation

#### `tutorials/tree-manipulation.ipynb` - Manipulating Trees

**Purpose**: Master tree modification operations.

**Target Audience**: Users modifying tree structures

**Estimated Time**: 20-30 minutes

**Outline**:
1. **Adding Leaves**
   - `add_leaf()` function
   - Where can leaves be added?
   - Effect on vector representation

2. **Removing Leaves**
   - `remove_leaf()` function
   - Maintaining tree validity

3. **Rerooting Trees**
   - `reroot()` at specific node
   - `reroot_at_random()` for sampling
   - Effect on topology representation

4. **Queue Shuffle**
   - Converting unordered to ordered
   - `queue_shuffle()` with mapping
   - Why this matters for optimization

5. **Common Ancestor Queries**
   - `get_common_ancestor()` function
   - Use cases in analysis

6. **Practical Examples**
   - SPR-like operations
   - Tree comparison after manipulation

**Key Functions**: `add_leaf`, `remove_leaf`, `reroot`, `reroot_at_random`, `queue_shuffle`, `get_common_ancestor`

---

### Priority 5: Advanced Topics

#### `how-to/large-scale-trees.ipynb` - Working with Large Trees

**Purpose**: Best practices for trees with 10,000+ leaves.

**Target Audience**: Users with large-scale genomic data

**Estimated Time**: 30-40 minutes

**Outline**:
1. **Memory Considerations**
   - Vector vs matrix storage
   - Estimating memory usage

2. **Benchmarking Conversion Times**
   - Scaling behavior
   - Comparison with other libraries

3. **Sparse Matrix Operations**
   - When to use sparse format
   - `incidence()` with format parameter

4. **Batch Processing**
   - Processing multiple trees
   - Memory-efficient patterns

5. **Parallel Computation**
   - Using `n_jobs` parameter
   - When parallelization helps

6. **Integration with Rust Core**
   - Direct Rust bindings
   - Maximum performance tips

**Key Functions**: `sample_vector`, `cophenetic_distances`, `incidence`, optimization classes with `n_jobs`

---

#### `how-to/cli-tutorial.ipynb` - Command-Line Interface

**Purpose**: Use CLI effectively for scripting and quick experiments.

**Target Audience**: Users preferring CLI workflows

**Estimated Time**: 15-20 minutes

**Outline**:
1. **Available Commands**
   - `phylo2vec samplev`
   - `phylo2vec samplem`
   - `phylo2vec from_newick`
   - `phylo2vec to_newick`

2. **Sampling Trees**
   - `phylo2vec samplev 10` examples
   - Options and flags

3. **Format Conversions**
   - Piping Newick strings
   - Reading from files

4. **Scripting Examples**
   - Bash one-liners
   - Integration with other tools

5. **Output Formats**
   - JSON output
   - CSV output

**Key Commands**: All CLI commands

---

## Notebook Standards

All notebooks should follow these standards:

### Header Cell Template

```python
"""
# Notebook Title

Brief description of what the user will learn.

**Prerequisites**:
- Python 3.10+
- phylo2vec installed (`pip install phylo2vec`)
- [Optional dependencies if any]

**Estimated time**: X minutes

**What you'll learn**:
1. First learning objective
2. Second learning objective
3. Third learning objective
"""
```

### Import Cell Template

```python
# Standard imports
import numpy as np
import phylo2vec as p2v

# Version check
print(f"NumPy version: {np.__version__}")
print(f"Phylo2Vec version: {p2v.__version__}")

# Set random seed for reproducibility
np.random.seed(42)
```

### Section Headers

Use markdown cells with clear hierarchy:
- `# Main Title` (only at top)
- `## Section`
- `### Subsection`
- `#### Minor heading`

### Code Cell Guidelines

1. **One concept per cell**: Don't combine unrelated operations
2. **Print outputs explicitly**: Don't rely on notebook auto-display
3. **Add comments**: Explain non-obvious operations
4. **Show expected output**: Include output in committed notebook

### Exercise Template

```python
"""
## Exercise X: Title

**Task**: Description of what to do.

**Hint**: Optional hint for difficult exercises.
"""

# Your code here
# ...

# Solution (hidden in separate cell or collapsed)
```

### Cleanup Cell

```python
# Cleanup temporary files
import os
import shutil

if os.path.exists("temp_trees"):
    shutil.rmtree("temp_trees")
```

---

## Notebook Development Priority

| Priority | Notebook | Effort | Rationale |
|----------|----------|--------|-----------|
| 1 | `getting-started.ipynb` | 4 hrs | Essential for onboarding |
| 2 | `core-concepts.ipynb` | 8 hrs | Foundation for understanding |
| 3 | `working-with-newick.ipynb` | 6 hrs | Most common use case |
| 4 | `tree-statistics.ipynb` | 6 hrs | Core analysis workflows |
| 5 | `tree-manipulation.ipynb` | 6 hrs | High user demand |
| 6 | `large-scale-trees.ipynb` | 6 hrs | Advanced users need |
| 7 | `cli-tutorial.ipynb` | 4 hrs | Alternative interface |

**Total estimated effort**: ~40 hours

---

## Existing Notebooks: Recommended Changes

### `demo.ipynb`

- **Action**: Move to `tutorials/demo.ipynb`
- **Rename**: Consider renaming to `comprehensive-demo.ipynb`
- **Updates**:
  - Add header cell with prerequisites
  - Add time estimate
  - Improve section organization

### `demo_opt.ipynb`

- **Action**: Move to `optimization/demo_opt.ipynb`
- **Rename**: Consider renaming to `optimization-demo.ipynb`
- **Updates**:
  - Add header cell
  - Add more explanation of GradME
  - Include parameter tuning guidance
