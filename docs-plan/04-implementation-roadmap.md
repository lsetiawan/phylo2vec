# Implementation Roadmap

This document provides a phased implementation plan for the documentation improvements.

**Total Estimated Effort**: ~100 hours

---

## Phase Overview

| Phase | Focus | Priority | Effort |
|-------|-------|----------|--------|
| 1 | Foundation | Critical | 12 hrs |
| 2 | Core Content | High | 32 hrs |
| 3 | How-To Guides | High | 18 hrs |
| 4 | Advanced Content | Medium | 32 hrs |
| 5 | Polish | Medium | 14 hrs |

---

## Phase 1: Foundation (Critical Priority)

**Goal**: Establish documentation infrastructure and quick wins.

### Tasks

| ID | Task | Description | Effort | Dependencies |
|----|------|-------------|--------|--------------|
| 1.1 | Create directory structure | Create `tutorials/`, `how-to/`, `explanation/`, `reference/`, `optimization/` directories | 2 hrs | None |
| 1.2 | Update `_toc.yml` | New Diátaxis structure with all sections | 1 hr | 1.1 |
| 1.3 | Update `_config.yml` | Add intersphinx for numpy/scipy, numpydoc extension | 1 hr | None |
| 1.4 | Expand `api.rst` | Add all missing functions to API reference | 4 hrs | None |
| 1.5 | Create `glossary.md` | Define phylogenetics terminology | 3 hrs | 1.1 |
| 1.6 | Create `citation.md` | BibTeX entries from README | 1 hr | 1.1 |

### Deliverables
- [ ] Complete directory structure
- [ ] Updated configuration files
- [ ] Complete API reference with all 30+ functions
- [ ] Glossary with all terms defined
- [ ] Citation page with BibTeX

### Commands to Execute

```bash
# Create directories
cd docs
mkdir -p tutorials how-to explanation reference/api optimization

# Create placeholder index files
touch tutorials/index.md
touch how-to/index.md
touch explanation/index.md
touch reference/index.md
touch optimization/index.md

# Move existing notebooks
mv demo.ipynb tutorials/
mv demo_opt.ipynb optimization/
```

---

## Phase 2: Core Content (High Priority)

**Goal**: Develop essential tutorials and conceptual documentation.

### Tasks

| ID | Task | Description | Effort | Dependencies |
|----|------|-------------|--------|--------------|
| 2.1 | Write `tutorials/getting-started.md` | 5-minute quick start guide | 4 hrs | 1.1 |
| 2.2 | Create `tutorials/core-concepts.ipynb` | Understanding Phylo2Vec representation | 8 hrs | 1.1 |
| 2.3 | Improve base module docstrings | Add Examples, See Also to newick.py, edges.py, ancestry.py, pairs.py | 6 hrs | None |
| 2.4 | Improve stats module docstrings | Add Notes, References, Examples to nodewise.py | 4 hrs | None |
| 2.5 | Write `explanation/phylo2vec-representation.md` | Mathematical foundation explained | 6 hrs | 1.1 |
| 2.6 | Write `explanation/ordered-vs-unordered.md` | Tree types explained | 4 hrs | 1.1 |

### Deliverables
- [ ] Quick start tutorial
- [ ] Core concepts notebook (30-45 min tutorial)
- [ ] Enhanced docstrings for base module (8 functions)
- [ ] Enhanced docstrings for stats module (5 functions)
- [ ] Mathematical explanation document
- [ ] Ordered vs unordered explanation

### Files to Modify

```
py-phylo2vec/phylo2vec/base/newick.py    # from_newick, to_newick
py-phylo2vec/phylo2vec/base/edges.py     # from_edges, to_edges
py-phylo2vec/phylo2vec/base/ancestry.py  # from_ancestry, to_ancestry
py-phylo2vec/phylo2vec/base/pairs.py     # from_pairs, to_pairs
py-phylo2vec/phylo2vec/stats/nodewise.py # cophenetic_distances, cov, etc.
```

---

## Phase 3: How-To Guides (High Priority)

**Goal**: Create task-oriented documentation for common workflows.

### Tasks

| ID | Task | Description | Effort | Dependencies |
|----|------|-------------|--------|--------------|
| 3.1 | Write `how-to/convert-formats.md` | Converting between Newick/edges/ancestry | 3 hrs | 1.1 |
| 3.2 | Write `how-to/manipulate-trees.md` | Add/remove leaves, reroot | 3 hrs | 1.1 |
| 3.3 | Write `how-to/compare-trees.md` | Compute distances, statistics | 3 hrs | 1.1 |
| 3.4 | Write `how-to/optimize-trees.md` | Run HillClimbing/GradME | 4 hrs | 1.1 |
| 3.5 | Write `how-to/work-with-datasets.md` | Load built-in datasets | 2 hrs | 1.1 |
| 3.6 | Write `how-to/use-cli.md` | CLI command reference and examples | 3 hrs | 1.1 |

### Deliverables
- [ ] 6 task-oriented how-to guides
- [ ] Each guide solves one specific problem
- [ ] Copy-paste ready code snippets

### How-To Guide Template

```markdown
# How to [Task]

## Problem
[One sentence describing the task]

## Solution

### Prerequisites
- phylo2vec installed
- [Other requirements]

### Steps

#### Step 1: [Action]
```python
# Code
```

#### Step 2: [Action]
```python
# Code
```

## Complete Example

```python
# Full working example
```

## See Also
- [Related how-to guide](link)
- [API reference](link)
```

---

## Phase 4: Advanced Content (Medium Priority)

**Goal**: Develop advanced tutorials and optimization documentation.

### Tasks

| ID | Task | Description | Effort | Dependencies |
|----|------|-------------|--------|--------------|
| 4.1 | Create `tutorials/working-with-newick.ipynb` | Deep dive into format conversions | 6 hrs | 2.1 |
| 4.2 | Create `tutorials/tree-statistics.ipynb` | Computing distances and metrics | 6 hrs | 2.4 |
| 4.3 | Create `how-to/large-scale-trees.ipynb` | Working with large trees | 6 hrs | 4.2 |
| 4.4 | Write `explanation/algorithm-complexity.md` | AVL trees, Fenwick trees, O(n log n) | 4 hrs | 2.5 |
| 4.5 | Improve opt module docstrings | HillClimbing, GradME, gradme_loss | 6 hrs | None |
| 4.6 | Write `explanation/architecture.md` | Rust core + Python/R bindings | 4 hrs | 1.1 |

### Deliverables
- [ ] 2 advanced tutorial notebooks
- [ ] Large-scale trees how-to notebook
- [ ] Algorithm complexity explanation
- [ ] Enhanced optimization docstrings
- [ ] Architecture documentation

### Files to Modify

```
py-phylo2vec/phylo2vec/opt/_hc.py      # HillClimbing
py-phylo2vec/phylo2vec/opt/_gradme.py  # GradME, gradme_loss
```

---

## Phase 5: Polish (Medium Priority)

**Goal**: Quality assurance and final touches.

### Tasks

| ID | Task | Description | Effort | Dependencies |
|----|------|-------------|--------|--------------|
| 5.1 | Create `changelog.md` | Version history from git tags | 3 hrs | 1.1 |
| 5.2 | Review cross-references | Verify all See Also links work | 2 hrs | 2.3, 2.4, 4.5 |
| 5.3 | Test code examples | Run all docstring examples | 4 hrs | All docstrings |
| 5.4 | Create section index pages | Index pages for tutorials, how-to, etc. | 3 hrs | 3.*, 4.* |
| 5.5 | Version and compatibility | Add Python version badges, compatibility notes | 2 hrs | 5.4 |

### Deliverables
- [ ] Changelog with all versions
- [ ] All cross-references validated
- [ ] All code examples tested
- [ ] Polished index pages
- [ ] Version compatibility information

### Testing Checklist

```bash
# Test documentation build
cd docs
jupyter-book build .

# Verify no warnings
# Check all links resolve
# Verify notebooks execute

# Test docstring examples
cd py-phylo2vec
pytest --doctest-modules phylo2vec/
```

---

## Quality Metrics

### Documentation Coverage

| Metric | Current | Target | Measurement |
|--------|---------|--------|-------------|
| API functions documented | ~60% | 100% | Count in api.rst |
| Functions with Examples | ~20% | 100% | Docstring audit |
| Diátaxis sections complete | 1/4 | 4/4 | Section count |
| Tutorial notebooks | 2 | 7+ | File count |
| How-to guides | 0 | 7 | File count |
| Explanation articles | 0 | 5+ | File count |

### Quality Criteria

**Docstrings**:
- [ ] All public functions have docstrings
- [ ] All docstrings follow NumPy style
- [ ] All docstrings have Parameters, Returns, Examples
- [ ] All examples are tested and working
- [ ] Cross-references (See Also) are complete

**Tutorials**:
- [ ] Each tutorial has clear learning objectives
- [ ] Tutorials build on each other progressively
- [ ] All code cells execute without errors
- [ ] Expected outputs are shown
- [ ] Links to related content provided

**How-To Guides**:
- [ ] Each guide solves one specific problem
- [ ] Prerequisites clearly stated
- [ ] Code is copy-paste ready
- [ ] Edge cases addressed

---

## Review Checklist

Before each phase completion:

- [ ] `jupyter-book build docs/` completes without errors
- [ ] All notebooks execute successfully
- [ ] All internal links resolve
- [ ] All external links valid
- [ ] Spelling and grammar checked
- [ ] Consistent terminology throughout
- [ ] Version numbers current
- [ ] Citation information correct

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Docstring examples break with API changes | Add doctest to CI pipeline |
| Large notebooks slow to load | Split into smaller notebooks |
| Cross-references become stale | Automated link checking in CI |
| Inconsistent style | Create style guide, use linting |

---

## Success Criteria

The documentation improvement is considered successful when:

1. **Completeness**: All 30+ public API functions documented with examples
2. **Accessibility**: New user can get started in under 5 minutes
3. **Findability**: Any question answerable within 3 clicks
4. **Accuracy**: All code examples execute correctly
5. **Maintainability**: Documentation builds without warnings
6. **Adoption**: Contributor questions about usage decrease

---

## Maintenance Plan

After initial implementation:

1. **Monthly**: Review and update any broken links
2. **Per Release**: Update changelog, check API doc accuracy
3. **Quarterly**: Review analytics for missing topics
4. **Annually**: Major restructuring if needed
