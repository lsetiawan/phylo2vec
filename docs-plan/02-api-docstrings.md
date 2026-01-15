# API Docstring Improvements

This document outlines specific improvements needed for API documentation, including a standard template and detailed examples for key functions.

---

## Current API Documentation Gaps

### Missing from `docs/api.rst`

**Base Conversions**:
- `from_edges`, `to_edges`
- `from_pairs`, `to_pairs`

**Utilities**:
- `queue_shuffle`
- `reroot`
- `reroot_at_random`

**Optimization**:
- `GradME` class
- `gradme_loss` function

**Datasets**:
- `read_fasta`
- `load_descr`

---

## Docstring Enhancement Template

All docstrings should follow this enhanced NumPy-style template:

```python
def function_name(param1, param2, optional_param=None):
    """Short one-line description ending with a period.

    Longer description providing context about what this function does,
    why you would use it, and any important caveats or prerequisites.

    Parameters
    ----------
    param1 : type
        Description of param1.
    param2 : numpy.ndarray
        Description of param2. Shape should be (n_leaves - 1,) for vectors
        or (n_leaves - 1, 3) for matrices.
    optional_param : type, optional
        Description of optional parameter, by default None.

    Returns
    -------
    return_type
        Description of what is returned.

    Raises
    ------
    ValueError
        When input validation fails (describe conditions).

    See Also
    --------
    related_function : Brief description of relationship.

    Notes
    -----
    Mathematical notation or algorithm details.

    References
    ----------
    .. [1] Penn et al. (2024). "Phylo2Vec: a vector representation for
       binary trees." Systematic Biology. https://doi.org/10.1093/sysbio/syae030

    Examples
    --------
    Basic usage:

    >>> import numpy as np
    >>> import phylo2vec as p2v
    >>> v = np.array([0, 1, 2, 3, 4])
    >>> result = p2v.function_name(v)
    >>> print(result)
    expected_output

    With optional parameters:

    >>> result = p2v.function_name(v, optional_param=True)
    >>> print(result)
    different_output
    """
```

---

## Specific Docstring Improvements by Module

### Base Conversions (`phylo2vec/base/`)

#### `from_newick` - Add Examples and See Also

**File**: `py-phylo2vec/phylo2vec/base/newick.py`

```python
def from_newick(newick: str) -> np.ndarray:
    """Convert a Newick string to a Phylo2Vec vector or matrix.

    Parses a phylogenetic tree in Newick format and converts it to the
    Phylo2Vec representation. If branch lengths are present, returns a
    matrix; otherwise returns a vector.

    Parameters
    ----------
    newick : str
        A valid Newick string representing a binary tree. Must end with
        semicolon. Supports optional branch lengths (e.g., "node:0.1").

    Returns
    -------
    numpy.ndarray
        If no branch lengths: vector of shape (n_leaves - 1,) with dtype int.
        If branch lengths present: matrix of shape (n_leaves - 1, 3) with
        dtype float, where columns are [topology, branch_length_child, branch_length_parent].

    Raises
    ------
    ValueError
        If the Newick string is malformed or represents a non-binary tree.

    See Also
    --------
    to_newick : Convert Phylo2Vec back to Newick format.
    from_edges : Convert from edge list representation.
    from_ancestry : Convert from ancestry matrix representation.

    Notes
    -----
    The conversion uses an AVL tree-based algorithm for efficient parsing,
    achieving O(n log n) time complexity for n leaves.

    Leaf labels in the Newick string should be integers from 0 to n-1.
    For trees with taxon names, use `create_label_mapping` first.

    Examples
    --------
    Convert a simple Newick string to a Phylo2Vec vector:

    >>> import phylo2vec as p2v
    >>> newick = "((0,1)4,(2,3)5)6;"
    >>> v = p2v.from_newick(newick)
    >>> v
    array([0, 0, 2])

    Convert a Newick string with branch lengths to a matrix:

    >>> newick_bl = "((0:0.1,1:0.2):0.3,(2:0.4,3:0.5):0.6);"
    >>> m = p2v.from_newick(newick_bl)
    >>> m.shape
    (3, 3)

    Round-trip conversion:

    >>> v_original = np.array([0, 0, 2])
    >>> v_roundtrip = p2v.from_newick(p2v.to_newick(v_original))
    >>> np.array_equal(v_original, v_roundtrip)
    True
    """
```

#### `to_newick` - Add Notes and Examples

**File**: `py-phylo2vec/phylo2vec/base/newick.py`

```python
def to_newick(vector_or_matrix: np.ndarray) -> str:
    """Convert a Phylo2Vec vector or matrix to Newick format.

    Transforms the Phylo2Vec representation back to standard Newick
    notation for compatibility with other phylogenetic tools.

    Parameters
    ----------
    vector_or_matrix : numpy.ndarray
        Phylo2Vec vector of shape (n_leaves - 1,) for topology only,
        or matrix of shape (n_leaves - 1, 3) to include branch lengths.

    Returns
    -------
    str
        Newick string ending with semicolon. Internal nodes are labeled
        from n_leaves to 2*n_leaves-1 (leaves are 0 to n_leaves-1,
        internal nodes are n_leaves+1, n_leaves+2, etc.).
        If input is a matrix, branch lengths are included.

    Raises
    ------
    ValueError
        If input is not a 1D or 2D numpy array.

    See Also
    --------
    from_newick : Convert Newick string to Phylo2Vec representation.
    to_edges : Convert to edge list representation.
    to_ancestry : Convert to ancestry matrix representation.

    Notes
    -----
    The conversion uses an AVL tree-based algorithm for efficient pair
    extraction, achieving O(n log n) time complexity for n leaves.

    For a tree with n leaves:
    - Vector v has length n-1
    - v[i] indicates the branch where leaf i+1 attaches
    - Internal nodes are labeled from n_leaves to 2*n_leaves-1
    - The root node is always labeled 2*n_leaves

    Examples
    --------
    Convert a vector (topology only):

    >>> import numpy as np
    >>> from phylo2vec import to_newick
    >>> v = np.array([0, 1, 2])
    >>> newick = to_newick(v)
    >>> print(newick)
    (((0,1)4,2)5,3)6;

    Convert a matrix (with branch lengths):

    >>> m = np.array([[0., 0.1, 0.2],
    ...               [1., 0.3, 0.4]])
    >>> newick = to_newick(m)

    Round-trip conversion:

    >>> v_original = np.array([0, 0, 2])
    >>> v_roundtrip = from_newick(to_newick(v_original))
    >>> np.array_equal(v_original, v_roundtrip)
    True
    """
```

#### `from_edges` / `to_edges` - Add Complete Docstrings

**File**: `py-phylo2vec/phylo2vec/base/edges.py`

```python
def to_edges(v: np.ndarray) -> List[Tuple[int, int]]:
    """Convert a Phylo2Vec vector to an edge list representation.

    An edge list represents the tree as pairs of connected nodes,
    useful for graph-based operations and visualization with libraries
    like NetworkX.

    Parameters
    ----------
    v : numpy.ndarray
        Phylo2Vec vector of shape (n_leaves - 1,).

    Returns
    -------
    edges : List[Tuple[int, int]]
        List of (parent, child) tuples. For a tree with n leaves,
        returns 2*(n-1) edges.

    See Also
    --------
    from_edges : Convert edge list back to vector.
    to_ancestry : Convert to ancestry matrix (includes parent labels).

    Examples
    --------
    >>> import numpy as np
    >>> import phylo2vec as p2v
    >>> v = np.array([0, 2, 2, 5, 4, 1])
    >>> edges = p2v.to_edges(v)
    >>> print(edges[:4])
    [(7, 0), (7, 1), (8, 2), (8, 3)]

    >>> # Reconstruct the vector
    >>> v_reconstructed = p2v.from_edges(edges)
    >>> np.array_equal(v, v_reconstructed)
    True

    Use with NetworkX for visualization:

    >>> import networkx as nx  # doctest: +SKIP
    >>> G = nx.DiGraph(edges)  # doctest: +SKIP
    >>> nx.draw(G, with_labels=True)  # doctest: +SKIP
    """


def from_edges(edges: List[Tuple[int, int]]) -> np.ndarray:
    """Convert an edge list to a Phylo2Vec vector.

    Parameters
    ----------
    edges : List[Tuple[int, int]]
        List of (parent, child) tuples representing a binary tree.

    Returns
    -------
    numpy.ndarray
        Phylo2Vec vector of shape (n_leaves - 1,).

    See Also
    --------
    to_edges : Convert vector to edge list.
    from_ancestry : Convert from ancestry matrix.

    Examples
    --------
    >>> import phylo2vec as p2v
    >>> edges = [(7, 0), (7, 1), (8, 2), (8, 3), (9, 7), (9, 8)]
    >>> v = p2v.from_edges(edges)
    >>> v
    array([0, 0, 2])
    """
```

---

### Statistics (`phylo2vec/stats/`)

#### `cophenetic_distances` - Add Scientific Context

**File**: `py-phylo2vec/phylo2vec/stats/nodewise.py`

```python
def cophenetic_distances(vector_or_matrix, unrooted=False):
    """Compute the cophenetic distance matrix between all leaf pairs.

    The cophenetic distance between two leaves is the sum of branch
    lengths from each leaf to their most recent common ancestor (MRCA).
    For vectors (topology only), this is the number of edges.

    Parameters
    ----------
    vector_or_matrix : numpy.ndarray
        Phylo2Vec vector (ndim == 1) for topological distances, or
        matrix (ndim == 2) for branch length-weighted distances.
    unrooted : bool, optional
        If True, compute distances on an unrooted tree, by default False.

    Returns
    -------
    numpy.ndarray
        Symmetric distance matrix of shape (n_leaves, n_leaves).
        Diagonal elements are always 0.

    See Also
    --------
    pairwise_distances : Generic interface for pairwise metrics.
    cov : Compute variance-covariance matrix.
    get_common_ancestor : Find MRCA of two nodes.

    Notes
    -----
    Cophenetic distances are widely used in phylogenetics for:

    - Tree comparison (cophenetic correlation)
    - Clustering validation
    - Molecular clock hypothesis testing
    - Phylogenetic diversity metrics

    For a tree with branch lengths, the cophenetic distance between
    leaves i and j is:

    .. math::

        d_{ij} = \\sum_{e \\in \\text{path}(i,j)} \\ell_e

    where path(i,j) is the set of edges connecting i and j.

    References
    ----------
    .. [1] Sokal, R. R., & Rohlf, F. J. (1962). "The comparison of
       dendrograms by objective methods." Taxon, 11(2), 33-40.

    Examples
    --------
    Topological distances (vector input):

    >>> import numpy as np
    >>> from phylo2vec.stats import cophenetic_distances
    >>> v = np.array([0, 0, 2])  # Tree: (((0,1),2),3)
    >>> D = cophenetic_distances(v)
    >>> D
    array([[0, 2, 4, 4],
           [2, 0, 4, 4],
           [4, 4, 0, 4],
           [4, 4, 4, 0]])

    Branch length distances (matrix input):

    >>> m = np.array([[0., 0.1, 0.2],
    ...               [0., 0.3, 0.4],
    ...               [2., 0.5, 0.6]])
    >>> D_bl = cophenetic_distances(m)
    """
```

#### `incidence` - Add Sparse Matrix Documentation

```python
def incidence(vector, format="coo"):
    """Compute the incidence matrix of a phylogenetic tree.

    The incidence matrix I has shape (n_leaves, n_edges) where I[i,j] = 1
    if leaf i descends from edge j, and 0 otherwise. This representation
    is useful for linear algebra operations on trees.

    Parameters
    ----------
    vector : numpy.ndarray
        Phylo2Vec vector (ndim == 1).
    format : {"coo", "csr", "csc", "dense"}, optional
        Output format, by default "coo".

        - "coo": Coordinate format (row, col, data lists)
        - "csr": Compressed Sparse Row format
        - "csc": Compressed Sparse Column format
        - "dense": Full numpy array

    Returns
    -------
    numpy.ndarray or sparse representation
        Incidence matrix in the specified format.

    Notes
    -----
    The incidence matrix is related to the cophenetic distance matrix D
    and branch length vector b by:

    .. math::

        D = I \\cdot \\text{diag}(b) \\cdot I^T

    Examples
    --------
    >>> import numpy as np
    >>> from phylo2vec.stats import incidence
    >>> v = np.array([0, 1, 2])
    >>> I = incidence(v, format="dense")
    >>> print(I.shape)
    (4, 6)
    """
```

---

### Utilities (`phylo2vec/utils/`)

#### `queue_shuffle` - Document the Algorithm

**File**: `py-phylo2vec/phylo2vec/utils/vector.py`

```python
def queue_shuffle(v, shuffle_cherries=False):
    """Reorder a Phylo2Vec vector to its ordered (birth-death) form.

    Queue Shuffle produces an equivalent tree with a different taxon
    ordering that satisfies the ordered constraint: v[i] in {0, ..., i}.
    This is essential for GradME optimization and tree space exploration.

    Parameters
    ----------
    v : numpy.ndarray
        Phylo2Vec vector (unordered form allowed).
    shuffle_cherries : bool, optional
        If True, randomly shuffle the order of cherries (sister pairs)
        in the ancestry matrix, by default False.

    Returns
    -------
    v_new : numpy.ndarray
        Reordered Phylo2Vec vector satisfying ordered constraints.
    vec_mapping : List[int]
        Mapping from new leaf indices to original indices.
        vec_mapping[new_index] = original_index

    See Also
    --------
    sample_vector : Sample random vectors (can be ordered or unordered).
    reorder_v : Alternative reordering function.

    Notes
    -----
    The algorithm traverses the ancestry matrix in a queue-based order,
    assigning new leaf labels sequentially. This ensures the output
    is always an ordered tree regardless of input.

    For ordered trees: v[i] in {0, 1, ..., i} for all i
    For unordered trees: v[i] in {0, 1, ..., 2i} for all i

    References
    ----------
    .. [1] Penn et al. (2023). "GradME: Continuous phylogenetic inference
       with gradient descent." Genome Biology and Evolution.
       https://doi.org/10.1093/gbe/evad213

    Examples
    --------
    >>> import numpy as np
    >>> from phylo2vec.utils.vector import queue_shuffle
    >>> v = np.array([0, 0, 1, 5, 8, 5])  # Unordered
    >>> v_ordered, mapping = queue_shuffle(v)
    >>> # v_ordered now satisfies: v_ordered[i] <= i for all i
    >>> all(v_ordered[i] <= i for i in range(len(v_ordered)))
    True
    >>> # mapping shows how leaves were relabeled
    >>> print(mapping)
    [0, 1, 3, 2, 5, 4, 6]
    """
```

#### `get_common_ancestor` - Add Use Cases

```python
def get_common_ancestor(v, node1, node2):
    """Find the most recent common ancestor (MRCA) of two nodes.

    Parameters
    ----------
    v : numpy.ndarray
        Phylo2Vec vector.
    node1, node2 : int
        Node indices. Can be leaf nodes (0 to n_leaves-1) or
        internal nodes (n_leaves to 2*n_leaves-1).

    Returns
    -------
    mrca : int
        Index of the most recent common ancestor.

    Raises
    ------
    ValueError
        If nodes are outside valid range [0, 2*n_leaves].

    See Also
    --------
    cophenetic_distances : Distance to MRCA determines cophenetic distance.
    to_ancestry : Get full ancestry matrix.

    Examples
    --------
    >>> import numpy as np
    >>> from phylo2vec.utils.vector import get_common_ancestor
    >>> v = np.array([0, 0, 2])  # Tree: ((0,1),(2,3))
    >>> # Leaves 0 and 1 are siblings
    >>> mrca_01 = get_common_ancestor(v, 0, 1)
    >>> print(mrca_01)
    4
    >>> # Leaves 0 and 2 share the root as MRCA
    >>> mrca_02 = get_common_ancestor(v, 0, 2)
    >>> print(mrca_02)
    6
    """
```

#### `reroot` - Document Parameters

```python
def reroot(v, node):
    """Reroot a tree at a specified node.

    Changes the root of the tree to be adjacent to the specified node,
    modifying the tree topology accordingly.

    Parameters
    ----------
    v : numpy.ndarray
        Phylo2Vec vector of shape (n_leaves - 1,).
    node : int
        Node to reroot at. Must be in range [0, 2*n_leaves-1].
        - 0 to n_leaves-1: Reroot at a leaf
        - n_leaves to 2*n_leaves-1: Reroot at an internal node

    Returns
    -------
    numpy.ndarray
        New Phylo2Vec vector with tree rerooted.

    See Also
    --------
    reroot_at_random : Reroot at a random node.

    Examples
    --------
    >>> import numpy as np
    >>> from phylo2vec import to_newick
    >>> from phylo2vec.utils.vector import reroot
    >>> v = np.array([0, 0, 2])
    >>> print(to_newick(v))
    ((0,1)4,(2,3)5)6;
    >>> v_rerooted = reroot(v, node=2)
    >>> print(to_newick(v_rerooted))
    # Tree now rooted near leaf 2
    """
```

---

### Optimization (`phylo2vec/opt/`)

#### `HillClimbing` - Expand Class Documentation

**File**: `py-phylo2vec/phylo2vec/opt/_hc.py`

```python
class HillClimbing(BaseOptimizer):
    """Tree topology optimization using hill-climbing with RAxML-NG.

    This optimizer searches tree space by proposing single-index changes
    to the Phylo2Vec vector and accepting changes that improve the
    likelihood score. Branch lengths are optimized using RAxML-NG.

    Parameters
    ----------
    model : str
        DNA/AA substitution model (e.g., "GTR", "JC", "HKY").
        Passed to RAxML-NG for likelihood computation.
    tol : float, optional
        Minimum improvement required to accept a topology change,
        by default 0.001.
    patience : int, optional
        Number of passes without improvement before stopping,
        by default 3.
    rounds : int, optional
        Number of vector indices to modify per pass, by default 1.
    tree_folder_path : str, optional
        Directory for intermediate tree files, by default "trees".
    random_seed : int, optional
        Seed for reproducibility.
    n_jobs : int, optional
        Number of parallel jobs for proposal evaluation.
    verbose : bool, optional
        Print progress information.

    Attributes
    ----------
    model : str
        The substitution model used.
    best_ : numpy.ndarray
        Best tree found (after calling fit()).
    scores_ : list
        History of likelihood scores during optimization.

    See Also
    --------
    GradME : Gradient-based optimization (faster, approximate).
    list_methods : List available optimization methods.

    Notes
    -----
    Requires RAxML-NG to be installed and accessible in PATH.

    The algorithm:

    1. Start with a random tree
    2. Reorder to birth-death form (queue_shuffle)
    3. For each index i, evaluate all 2i+1 possible values
    4. Accept the best improvement above tolerance
    5. Repeat until patience exhausted

    References
    ----------
    .. [1] Penn et al. (2024). "Phylo2Vec: a vector representation for
       binary trees." Systematic Biology. https://doi.org/10.1093/sysbio/syae030

    Examples
    --------
    >>> from phylo2vec.opt import HillClimbing
    >>> hc = HillClimbing(model="GTR", verbose=True, patience=3)
    >>> result = hc.fit("sequences.fasta")  # doctest: +SKIP
    >>> print(f"Best score: {result.best_score}")  # doctest: +SKIP

    Get the best tree as Newick:

    >>> from phylo2vec import to_newick
    >>> from phylo2vec.utils.newick import apply_label_mapping
    >>> newick = to_newick(result.best)  # doctest: +SKIP
    >>> newick_labeled = apply_label_mapping(newick, result.label_mapping)  # doctest: +SKIP
    """
```

#### `GradME` - Document Continuous Optimization

**File**: `py-phylo2vec/phylo2vec/opt/_gradme.py`

```python
class GradME(BaseOptimizer):
    """Gradient-based tree optimization using minimum evolution.

    GradME uses a continuous relaxation of the Phylo2Vec representation
    with gradient descent to minimize the balanced minimum evolution
    criterion (tree length).

    Parameters
    ----------
    model : str
        Substitution model for distance matrix computation.
    solver : str, optional
        Optax optimizer name, by default "adam".
        Options: "adam", "sgd", "adabelief", "rmsprop".
    learning_rate : float, optional
        Optimizer learning rate, by default 0.1.
    patience : int, optional
        Early stopping patience, by default 10.
    tol : float, optional
        Convergence tolerance, by default 1e-6.
    nesterov : bool, optional
        Use Nesterov momentum if applicable, by default False.
    verbose : bool, optional
        Print progress information.

    Attributes
    ----------
    best_W : numpy.ndarray
        Probability matrix of shape (n-1, n-1) after optimization.
        W[i,j] = P(v[i] = j) for ordered trees.

    See Also
    --------
    HillClimbing : Discrete optimization (slower, exact likelihood).
    gradme_loss : Standalone loss function for custom optimization.

    Notes
    -----
    GradME optimizes path length (sum of branch lengths) rather than
    likelihood, making it faster but less statistically principled
    than maximum likelihood methods.

    Requires JAX and optax: `pip install phylo2vec[opt]`

    References
    ----------
    .. [1] Penn et al. (2023). "GradME: Continuous phylogenetic inference
       with gradient descent." Genome Biology and Evolution.
       https://doi.org/10.1093/gbe/evad213

    Examples
    --------
    >>> from phylo2vec.opt import GradME
    >>> gradme = GradME(model="F81", learning_rate=0.1, patience=20)
    >>> result = gradme.fit("sequences.fasta")  # doctest: +SKIP
    >>> # The best discrete tree
    >>> print(result.best)  # doctest: +SKIP
    >>> # The continuous probability matrix
    >>> print(result.best_W.shape)  # doctest: +SKIP
    """
```

---

## Functions Requiring Documentation Updates

| Function | File | Current State | Required Additions |
|----------|------|--------------|-------------------|
| `from_newick` | `base/newick.py` | Good | Examples, See Also |
| `to_newick` | `base/newick.py` | Good | Notes, Examples |
| `from_edges` | `base/edges.py` | Basic | Full docstring |
| `to_edges` | `base/edges.py` | Basic | Full docstring |
| `from_pairs` | `base/pairs.py` | Basic | Full docstring |
| `to_pairs` | `base/pairs.py` | Basic | Full docstring |
| `cophenetic_distances` | `stats/nodewise.py` | Basic | Notes, References, Examples |
| `pairwise_distances` | `stats/nodewise.py` | Basic | Examples |
| `cov` | `stats/nodewise.py` | Basic | Mathematical formula, Examples |
| `precision` | `stats/nodewise.py` | Basic | Mathematical formula, Examples |
| `incidence` | `stats/nodewise.py` | Basic | Format examples, sparse matrix usage |
| `add_leaf` | `utils/vector.py` | Basic | Examples, edge cases |
| `remove_leaf` | `utils/vector.py` | Basic | Examples, return value clarity |
| `queue_shuffle` | `utils/vector.py` | Detailed | Simplify, add examples |
| `reroot` | `utils/vector.py` | Good | More examples |
| `reroot_at_random` | `utils/vector.py` | Basic | Examples, use cases |
| `get_common_ancestor` | `utils/vector.py` | Basic | Examples |
| `HillClimbing` | `opt/_hc.py` | Good | Algorithm description, more examples |
| `GradME` | `opt/_gradme.py` | Good | More examples, solver options |
| `gradme_loss` | `opt/_gradme.py` | Minimal | Full documentation needed |
| `load_alignment` | `datasets/` | Basic | Examples, available datasets |
| `list_datasets` | `datasets/` | Minimal | Full documentation needed |

---

## Expanded API Reference (`docs/api.rst`)

```rst
API Reference
=============

.. currentmodule:: phylo2vec

Core Conversion Functions
-------------------------

Functions for converting between Phylo2Vec vectors/matrices and other
tree representations.

Newick Format
^^^^^^^^^^^^^

.. autosummary::
    :nosignatures:
    :toctree: generated/

    from_newick
    to_newick

Ancestry Format
^^^^^^^^^^^^^^^

.. autosummary::
    :nosignatures:
    :toctree: generated/

    from_ancestry
    to_ancestry

Edge List Format
^^^^^^^^^^^^^^^^

.. autosummary::
    :nosignatures:
    :toctree: generated/

    from_edges
    to_edges

Pairs Format
^^^^^^^^^^^^

.. autosummary::
    :nosignatures:
    :toctree: generated/

    from_pairs
    to_pairs

Input/Output
------------

Functions for reading and writing trees to files.

.. autosummary::
    :nosignatures:
    :toctree: generated/

    load
    load_newick
    save
    save_newick

Sampling
--------

Functions for generating random trees.

.. autosummary::
    :nosignatures:
    :toctree: generated/

    sample_vector
    sample_matrix

Statistics
----------

Functions for computing tree statistics and distances.

.. currentmodule:: phylo2vec.stats

.. autosummary::
    :nosignatures:
    :toctree: generated/

    cophenetic_distances
    pairwise_distances
    cov
    precision
    incidence

Tree Manipulation
-----------------

Functions for modifying tree structure.

.. currentmodule:: phylo2vec.utils.vector

.. autosummary::
    :nosignatures:
    :toctree: generated/

    add_leaf
    remove_leaf
    check_vector
    queue_shuffle
    reorder_v
    reroot
    reroot_at_random
    get_common_ancestor

Newick Utilities
----------------

Helper functions for Newick string manipulation.

.. currentmodule:: phylo2vec.utils.newick

.. autosummary::
    :nosignatures:
    :toctree: generated/

    apply_label_mapping
    create_label_mapping
    find_num_leaves
    remove_branch_lengths
    remove_parent_labels

Matrix Utilities
----------------

.. currentmodule:: phylo2vec.utils.matrix

.. autosummary::
    :nosignatures:
    :toctree: generated/

    check_matrix

Optimization
------------

Classes and functions for phylogenetic tree inference.

.. currentmodule:: phylo2vec.opt

.. autosummary::
    :nosignatures:
    :toctree: generated/

    HillClimbing
    GradME
    gradme_loss
    list_methods

Datasets
--------

Functions for accessing built-in datasets.

.. currentmodule:: phylo2vec.datasets

.. autosummary::
    :nosignatures:
    :toctree: generated/

    list_datasets
    load_alignment
    load_fasta
    load_descr
    read_fasta
```
