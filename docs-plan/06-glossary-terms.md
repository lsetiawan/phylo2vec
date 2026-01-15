# Glossary Terms

This document lists all terminology that should be defined in the documentation glossary.

---

## Core Phylo2Vec Terms

| Term | Definition |
|------|------------|
| **Phylo2Vec vector** | Integer array of length n-1 that uniquely encodes a binary tree topology with n leaves. Each element v[i] indicates the branch where leaf i+1 attaches. |
| **Phylo2Vec matrix** | Array of shape (n-1, 3) that encodes both tree topology and branch lengths. Columns are [topology, branch_length_child, branch_length_parent]. |
| **Ordered tree** | A tree representation where v[i] is constrained to {0, 1, ..., i} for all i. Corresponds to birth-death process trees. |
| **Unordered tree** | A tree representation where v[i] can be any value in {0, 1, ..., 2i} for all i. Represents the full space of binary tree topologies. |

---

## Phylogenetics Terms

| Term | Definition |
|------|------------|
| **Binary tree** | A rooted tree where every internal node has exactly two children. All phylogenetic trees in Phylo2Vec are binary. |
| **Cherry** | A pair of sibling leaves (tips) that share the same immediate parent node. |
| **Cophenetic distance** | The sum of branch lengths (or edge count for topology-only) on the path connecting two leaves through their most recent common ancestor. |
| **Internal node** | A non-leaf node in a tree; represents an ancestral species or divergence point. In Phylo2Vec, internal nodes are labeled n_leaves to 2*n_leaves-1. |
| **Leaf (tip)** | A terminal node in a tree representing an observed taxon. In Phylo2Vec, leaves are labeled 0 to n_leaves-1. |
| **MRCA (Most Recent Common Ancestor)** | The most recent internal node that is an ancestor of both given nodes. |
| **Newick format** | Standard parenthetical notation for representing phylogenetic trees, e.g., "((A,B),(C,D));". |
| **Root** | The topmost node of a rooted tree, representing the common ancestor of all taxa. In Phylo2Vec, the root is always labeled 2*n_leaves. |
| **Topology** | The branching pattern of a tree, independent of branch lengths. |

---

## Tree Manipulation Terms

| Term | Definition |
|------|------------|
| **Rerooting** | Changing the position of the root in a tree, which changes the tree's orientation but not its topology for unrooted comparisons. |
| **Queue shuffle** | An algorithm that reorders a Phylo2Vec vector to satisfy the ordered tree constraint. Produces a label mapping from new to original indices. |
| **SPR (Subtree Prune and Regraft)** | A tree rearrangement operation where a subtree is detached and reattached elsewhere. |

---

## Statistics Terms

| Term | Definition |
|------|------------|
| **Cophenetic correlation** | Correlation between cophenetic distances from two trees; measures tree similarity. |
| **Incidence matrix** | Matrix I where I[i,j] = 1 if leaf i descends from edge j, 0 otherwise. Useful for linear algebra on trees. |
| **Precision matrix** | Inverse of the covariance matrix. Used in phylogenetic regression and graphical models. |
| **Variance-covariance matrix** | Matrix representing the expected covariance between trait values at leaves given a phylogenetic tree and evolutionary model. |

---

## Optimization Terms

| Term | Definition |
|------|------------|
| **GradME** | Gradient-based Minimum Evolution; a continuous optimization method that uses gradient descent on a relaxed Phylo2Vec representation. |
| **Hill climbing** | A discrete optimization method that iteratively improves tree topology by testing local modifications. |
| **Likelihood** | The probability of observing the data (e.g., sequence alignment) given a tree and evolutionary model. |
| **Minimum evolution** | A phylogenetic optimality criterion that minimizes the total tree length (sum of branch lengths). |
| **Substitution model** | A model describing the rates of nucleotide or amino acid substitutions (e.g., GTR, JC, HKY). |

---

## Data Structure Terms

| Term | Definition |
|------|------------|
| **Ancestry matrix** | Array of triplets (child1, child2, parent) describing the parent-child relationships in a tree. |
| **AVL tree** | A self-balancing binary search tree used internally for O(log n) operations. |
| **Edge list** | Representation of a tree as a list of (parent, child) pairs. |
| **Fenwick tree (Binary Indexed Tree)** | Data structure enabling O(log n) cumulative queries, used in efficient tree algorithms. |

---

## File Format Terms

| Term | Definition |
|------|------------|
| **FASTA** | Text-based format for representing nucleotide or amino acid sequences. |
| **Nexus** | File format that can contain sequence alignments, trees, and other phylogenetic data. |

---

## Glossary File Template

Create at `docs/reference/glossary.md`:

```markdown
# Glossary

Definitions of terms used throughout the Phylo2Vec documentation.

## A

```{glossary}
Ancestry matrix
    Array of triplets (child1, child2, parent) describing the parent-child
    relationships in a phylogenetic tree.

AVL tree
    A self-balancing binary search tree used internally for O(log n) operations
    in Phylo2Vec conversion algorithms.
```

## B

```{glossary}
Binary tree
    A rooted tree where every internal node has exactly two children.
    All phylogenetic trees in Phylo2Vec are binary.

Branch length
    The evolutionary distance associated with an edge in a phylogenetic tree,
    typically measured in expected substitutions per site.
```

## C

```{glossary}
Cherry
    A pair of sibling leaves (tips) that share the same immediate parent node.

Cophenetic distance
    The sum of branch lengths (or edge count for topology-only) on the path
    connecting two leaves through their most recent common ancestor (MRCA).
```

## G

```{glossary}
GradME
    Gradient-based Minimum Evolution. A continuous optimization method that
    uses gradient descent on a relaxed Phylo2Vec representation to find
    optimal tree topologies quickly.
```

## H

```{glossary}
Hill climbing
    A discrete optimization method that iteratively improves tree topology
    by testing local modifications and accepting improvements.
```

## I

```{glossary}
Incidence matrix
    Matrix I where I[i,j] = 1 if leaf i descends from edge j, 0 otherwise.
    Useful for linear algebra operations on phylogenetic trees.

Internal node
    A non-leaf node in a tree representing an ancestral species or divergence
    point. In Phylo2Vec, internal nodes are labeled n_leaves to 2*n_leaves-1.
```

## L

```{glossary}
Leaf
    A terminal node in a tree representing an observed taxon (species, sample,
    etc.). In Phylo2Vec, leaves are labeled 0 to n_leaves-1.
```

## M

```{glossary}
MRCA
    Most Recent Common Ancestor. The most recent internal node that is an
    ancestor of both given nodes.

Minimum evolution
    A phylogenetic optimality criterion that minimizes the total tree length
    (sum of branch lengths).
```

## N

```{glossary}
Newick format
    Standard parenthetical notation for representing phylogenetic trees.
    Example: "((A:0.1,B:0.2):0.3,(C:0.4,D:0.5):0.6);"
```

## O

```{glossary}
Ordered tree
    A Phylo2Vec representation where v[i] is constrained to {0, 1, ..., i}
    for all i. Corresponds to trees generated by birth-death processes.
```

## P

```{glossary}
Phylo2Vec matrix
    Array of shape (n-1, 3) encoding both tree topology and branch lengths.
    Columns: [topology_value, branch_length_to_child, branch_length_to_parent].

Phylo2Vec vector
    Integer array of length n-1 that uniquely encodes a binary tree topology
    with n leaves. Each element v[i] indicates which branch leaf i+1 attaches to.
```

## Q

```{glossary}
Queue shuffle
    Algorithm that reorders a Phylo2Vec vector to satisfy the ordered tree
    constraint. Returns both the reordered vector and a label mapping.
```

## R

```{glossary}
Rerooting
    Changing the position of the root in a tree. This changes the tree's
    representation but not its unrooted topology.

Root
    The topmost node of a rooted tree, representing the common ancestor of
    all taxa. In Phylo2Vec, the root is always labeled 2*n_leaves.
```

## S

```{glossary}
Substitution model
    A model describing the rates of nucleotide or amino acid substitutions
    over evolutionary time. Examples: GTR, JC, HKY, WAG.
```

## T

```{glossary}
Topology
    The branching pattern of a phylogenetic tree, independent of branch
    lengths. Two trees have the same topology if they have the same
    parent-child relationships.
```

## U

```{glossary}
Unordered tree
    A Phylo2Vec representation where v[i] can be any value in {0, 1, ..., 2i}.
    Represents the full space of binary tree topologies with n leaves.
```
```
