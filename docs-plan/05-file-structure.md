# File Structure and Configuration

This document provides the complete file structure and configuration updates needed for the documentation improvement.

---

## Complete Proposed Structure

```
docs/
├── _config.yml                       # Jupyter Book config (UPDATE)
├── _toc.yml                          # Table of contents (UPDATE)
├── index.md                          # Landing page (NEW - replace README.md link)
│
├── tutorials/                        # LEARNING-ORIENTED (NEW DIRECTORY)
│   ├── index.md                      # Tutorials overview
│   ├── getting-started.md            # Quick start guide
│   ├── core-concepts.ipynb           # Understanding Phylo2Vec
│   ├── demo.ipynb                    # Comprehensive demo (MOVED)
│   ├── working-with-newick.ipynb     # Format conversions
│   └── tree-statistics.ipynb         # Computing metrics
│
├── how-to/                           # TASK-ORIENTED (NEW DIRECTORY)
│   ├── index.md                      # How-to guides overview
│   ├── convert-formats.md            # Format conversion guide
│   ├── manipulate-trees.md           # Tree manipulation guide
│   ├── compare-trees.md              # Tree comparison guide
│   ├── optimize-trees.md             # Optimization guide
│   ├── work-with-datasets.md         # Dataset usage guide
│   ├── use-cli.md                    # CLI usage guide
│   ├── integrate-with-ete.md         # ETE integration guide
│   └── large-scale-trees.ipynb       # Large trees notebook
│
├── reference/                        # INFORMATION-ORIENTED (NEW DIRECTORY)
│   ├── index.md                      # Reference overview
│   ├── api/
│   │   ├── index.rst                 # Full API reference (EXPANDED)
│   │   ├── base.rst                  # Conversion functions
│   │   ├── io.rst                    # I/O functions
│   │   ├── stats.rst                 # Statistics functions
│   │   ├── utils.rst                 # Utility functions
│   │   ├── opt.rst                   # Optimization classes
│   │   └── datasets.rst              # Dataset functions
│   ├── cli.md                        # CLI command reference
│   ├── file-formats.md               # File format specifications
│   └── glossary.md                   # Terminology definitions
│
├── explanation/                      # UNDERSTANDING-ORIENTED (NEW DIRECTORY)
│   ├── index.md                      # Explanation overview
│   ├── phylo2vec-representation.md   # The math behind Phylo2Vec
│   ├── ordered-vs-unordered.md       # Tree types explained
│   ├── algorithm-complexity.md       # O(n log n) algorithms
│   ├── architecture.md               # System architecture
│   └── design-decisions.md           # Design rationale
│
├── optimization/                     # OPTIMIZATION FOCUS (NEW DIRECTORY)
│   ├── index.md                      # Optimization overview
│   ├── demo_opt.ipynb                # Optimization demo (MOVED)
│   ├── hill-climbing.md              # Hill-climbing explained
│   └── gradme.md                     # GradME explained
│
├── installation.md                   # Installation guide (EXISTS)
├── development.md                    # Development guide (EXISTS)
├── CONTRIBUTING.md                   # Contributing guide (SYMLINK - EXISTS)
├── changelog.md                      # Version history (NEW)
├── citation.md                       # How to cite (NEW)
│
├── img/                              # Images (EXISTS)
│   ├── criterion.png
│   ├── fig2.png
│   └── profile.png
│
└── api.rst                           # OLD - TO BE MOVED to reference/api/
```

---

## Key Files to Modify

### 1. `docs/_config.yml` - Updated Configuration

```yaml
# Book settings
title: Phylo2Vec
author: Phylo2Vec developers
logo: img/logo.png  # Add a logo if available

# Execution settings
execute:
  execute_notebooks: "cache"  # Cache notebook outputs for faster builds
  timeout: 300                # 5 minute timeout for cells

# LaTeX settings
latex:
  latex_documents:
    targetname: phylo2vec.tex

# Repository settings
repository:
  url: https://github.com/sbhattlab/phylo2vec
  path_to_book: docs
  branch: main  # Updated from 'master'

# HTML settings
html:
  use_issues_button: true
  use_repository_button: true
  use_edit_page_button: true
  home_page_in_navbar: true
  favicon: img/favicon.ico  # Add if available
  extra_footer: |
    <p>
    <a href="citation.html">Cite Phylo2Vec</a> |
    <a href="https://doi.org/10.1093/sysbio/syae030">Paper</a> |
    <a href="https://doi.org/10.21105/joss.09040">Software</a>
    </p>

# Sphinx settings
sphinx:
  extra_extensions:
    - sphinx.ext.autodoc
    - sphinx.ext.napoleon
    - sphinx.ext.viewcode
    - sphinx.ext.autosummary
    - sphinx.ext.intersphinx
    - sphinx.ext.mathjax
    - numpydoc
  config:
    add_module_names: false  # Changed from True
    autosummary_generate: true
    autodoc_typehints: description
    autodoc_member_order: bysource
    napoleon_google_docstring: false
    napoleon_numpy_docstring: true
    napoleon_include_init_with_doc: true
    numpydoc_show_class_members: false
    numpydoc_show_inherited_class_members: false
    intersphinx_mapping:
      python:
        - "https://docs.python.org/3"
        - null
      numpy:
        - "https://numpy.org/doc/stable/"
        - null
      scipy:
        - "https://docs.scipy.org/doc/scipy/"
        - null
```

### 2. `docs/_toc.yml` - Updated Table of Contents

```yaml
# Table of contents
# Learn more at https://jupyterbook.org/customize/toc.html

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

## New Files to Create

### Index Pages

#### `docs/tutorials/index.md`

```markdown
# Tutorials

Step-by-step lessons to help you learn Phylo2Vec from the ground up.

## Getting Started

- [Getting Started](getting-started.md) - Your first 5 minutes with Phylo2Vec

## Core Tutorials

- [Core Concepts](core-concepts.ipynb) - Understanding the Phylo2Vec representation
- [Comprehensive Demo](demo.ipynb) - Full walkthrough of all features

## Topic Tutorials

- [Working with Newick](working-with-newick.ipynb) - Format conversions and file I/O
- [Tree Statistics](tree-statistics.ipynb) - Computing distances and metrics

## What's the difference between Tutorials and How-To Guides?

**Tutorials** are learning-oriented. They take you through a series of steps
to learn concepts. Start here if you're new to Phylo2Vec.

**How-To Guides** are task-oriented. They provide steps to accomplish specific
tasks. Use these when you know what you want to do but need the exact steps.
```

#### `docs/how-to/index.md`

```markdown
# How-To Guides

Practical guides for accomplishing specific tasks with Phylo2Vec.

## Format Conversion
- [Convert Between Formats](convert-formats.md) - Newick, edges, ancestry, pairs

## Tree Manipulation
- [Manipulate Trees](manipulate-trees.md) - Add/remove leaves, reroot trees

## Analysis
- [Compare Trees](compare-trees.md) - Compute distances and statistics
- [Work with Datasets](work-with-datasets.md) - Use built-in datasets

## Optimization
- [Optimize Trees](optimize-trees.md) - Run HillClimbing and GradME

## Tools
- [Use the CLI](use-cli.md) - Command-line interface guide
- [Integrate with ETE](integrate-with-ete.md) - Visualization with ETE toolkit

## Advanced
- [Large-Scale Trees](large-scale-trees.ipynb) - Working with 10,000+ leaves
```

#### `docs/explanation/index.md`

```markdown
# Explanation

Background information and conceptual documentation to deepen your understanding.

## Core Concepts
- [The Phylo2Vec Representation](phylo2vec-representation.md) - Mathematical foundation
- [Ordered vs Unordered Trees](ordered-vs-unordered.md) - Understanding tree types

## Technical Details
- [Algorithm Complexity](algorithm-complexity.md) - Why operations are O(n log n)
- [Architecture](architecture.md) - Rust core and Python/R bindings

## Design
- [Design Decisions](design-decisions.md) - Why Phylo2Vec is designed this way
```

#### `docs/reference/index.md`

```markdown
# Reference

Technical reference documentation for Phylo2Vec.

## API Documentation
- [API Reference](api/index.rst) - Complete function and class documentation

## Tools
- [CLI Reference](cli.md) - Command-line interface commands

## Specifications
- [File Formats](file-formats.md) - Supported file formats
- [Glossary](glossary.md) - Terminology definitions
```

#### `docs/optimization/index.md`

```markdown
# Optimization Methods

Phylo2Vec provides two main optimization methods for phylogenetic tree inference.

## Methods

### [Hill Climbing](hill-climbing.md)
Discrete optimization using RAxML-NG for likelihood computation.
Best for: Small to medium datasets, maximum likelihood inference.

### [GradME](gradme.md)
Gradient-based continuous optimization using minimum evolution.
Best for: Fast exploration, large datasets, GPU acceleration.

## Tutorials
- [Optimization Demo](demo_opt.ipynb) - Hands-on examples

## Quick Comparison

| Feature | HillClimbing | GradME |
|---------|--------------|--------|
| Criterion | Likelihood | Path length |
| Search | Discrete | Continuous |
| Speed | Slower | Faster |
| Accuracy | Higher | Lower |
| GPU support | No | Yes |
| Dependencies | RAxML-NG | JAX, optax |
```

---

## Migration Script

```bash
#!/bin/bash
# Script to migrate documentation structure

cd /Users/lsetiawan/Repos/viss-demo/phylo2vec/docs

# Create new directories
mkdir -p tutorials how-to explanation reference/api optimization

# Move existing notebooks
mv demo.ipynb tutorials/
mv demo_opt.ipynb optimization/

# Create placeholder index files
for dir in tutorials how-to explanation reference optimization; do
    echo "# ${dir^}" > $dir/index.md
    echo "" >> $dir/index.md
    echo "Content coming soon." >> $dir/index.md
done

# Move and rename api.rst
cp api.rst reference/api/index.rst

echo "Migration complete. Review and update _toc.yml and _config.yml manually."
```

---

## Dependencies to Add

Update `pixi.toml` or `pyproject.toml` to include documentation dependencies:

```toml
[project.optional-dependencies]
docs = [
    "jupyter-book>=1.0.0",
    "sphinx>=7.0.0",
    "numpydoc>=1.6.0",
    "sphinx-autodoc-typehints>=1.25.0",
]
```

---

## ReadTheDocs Configuration

The existing `.readthedocs.yaml` should work with the new structure. Verify:

```yaml
version: 2

build:
  os: ubuntu-22.04
  tools:
    python: "3.11"

sphinx:
  configuration: docs/conf.py  # Or use jupyter-book

python:
  install:
    - method: pip
      path: py-phylo2vec
      extra_requirements:
        - docs
```

---

## Verification Commands

After implementing the structure:

```bash
# Verify structure
tree docs/ -L 2

# Build documentation
cd docs
jupyter-book build .

# Check for broken links
jupyter-book build . --builder linkcheck

# Verify no warnings
jupyter-book build . 2>&1 | grep -i warning
```
