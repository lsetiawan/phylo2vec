# Phylo2Vec Documentation Improvement Plan

**Version**: 1.6.0
**Target Audience**: Researchers, bioinformaticians, computational biologists, and developers
**Framework**: Jupyter Book with Sphinx extensions
**Estimated Total Effort**: ~100 hours

---

## Executive Summary

This plan outlines a comprehensive documentation improvement strategy for Phylo2Vec following the Diátaxis framework and Scientific Python community best practices. The improvements will increase adoption and support contributors by providing clear, well-organized documentation.

---

## Plan Documents

| Document | Description |
|----------|-------------|
| [01-diataxis-architecture.md](./01-diataxis-architecture.md) | Diátaxis-compliant documentation structure |
| [02-api-docstrings.md](./02-api-docstrings.md) | API docstring improvements with examples |
| [03-new-notebooks.md](./03-new-notebooks.md) | New Jupyter notebook topics |
| [04-implementation-roadmap.md](./04-implementation-roadmap.md) | Phased implementation plan |
| [05-file-structure.md](./05-file-structure.md) | File structure and configuration |
| [06-glossary-terms.md](./06-glossary-terms.md) | Glossary terms to define |

---

## Current State Analysis

### Strengths
- Jupyter Book with Sphinx extensions already configured
- NumPy-style docstrings throughout (good quality)
- Two functional demo notebooks covering core and optimization features
- ReadTheDocs integration working
- JOSS paper provides excellent scientific context
- 80 test functions across 8 test files
- CLI interface with 4 commands

### Gaps Identified
- No clear separation between tutorials, how-to guides, reference, and explanation
- API reference (`docs/api.rst`) is incomplete - missing several functions
- Missing conceptual documentation explaining the Phylo2Vec representation
- No task-oriented how-to guides
- Limited contributor documentation beyond development setup

### Current Documentation Files
```
docs/
├── _config.yml          # Jupyter Book config
├── _toc.yml             # Table of contents
├── api.rst              # API reference (incomplete)
├── installation.md      # Installation guide
├── development.md       # Development guide
├── CONTRIBUTING.md      # Contributing guide (symlink)
├── README.md            # README (symlink)
├── demo.ipynb           # Main tutorial (63 cells)
└── demo_opt.ipynb       # Optimization tutorial (508 lines)
```

---

## Public API to Document

### Base Conversions (8 functions)
- `from_newick`, `to_newick`
- `from_ancestry`, `to_ancestry`
- `from_edges`, `to_edges` *(missing from api.rst)*
- `from_pairs`, `to_pairs` *(missing from api.rst)*

### I/O (4 functions)
- `load`, `load_newick`, `save`, `save_newick`

### Sampling (2 functions)
- `sample_vector`, `sample_matrix`

### Statistics (5 functions)
- `cophenetic_distances`, `pairwise_distances`, `cov`, `precision`, `incidence`

### Utilities (7+ functions)
- `add_leaf`, `remove_leaf`, `check_vector`
- `queue_shuffle`, `reorder_v` *(missing from api.rst)*
- `reroot`, `reroot_at_random` *(missing from api.rst)*
- `get_common_ancestor`

### Optimization (4 items)
- `HillClimbing` class
- `GradME` class *(missing from api.rst)*
- `gradme_loss` *(missing from api.rst)*
- `list_methods`

### Datasets (3+ functions)
- `load_alignment`, `load_fasta`, `list_datasets`
- `read_fasta`, `load_descr` *(missing from api.rst)*

---

## Key Goals

1. **Expand user-facing API documentation** with comprehensive docstrings and examples
2. **Apply Diátaxis framework** for documentation structure
3. **Expand Jupyter notebook demos** for contributors and adoption
4. **Follow Scientific Python community best practices**

---

## References

- [Scientific Python Documentation Guide](https://learn.scientific-python.org/development/guides/docs/)
- [Diátaxis Framework](https://diataxis.fr/)
- [NumPy Documentation Style Guide](https://numpydoc.readthedocs.io/en/latest/format.html)
- [Jupyter Book Documentation](https://jupyterbook.org/)
