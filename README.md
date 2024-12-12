# Fractal Dimension Estimation Toolbox

This Python module provides a comprehensive suite of tools for estimating the fractal dimensions of 2D datasets. It incorporates both established and innovative methods such as original box counting, correlation sum, exact box counting, oversampling, temporal sampling, and their generalized versions. This toolbox is particularly suited for researchers and developers investigating spatial patterns, fractal structures, or self-similarity in 2D data.

---

## Features

- **Box Counting**: Supports variations including original box counting, oversampling, and exact box counting methods.
- **Generalized Fractal Dimensions**: Enables the calculation of higher-order fractal dimensions (e.g., q-dimensions).
- **Temporal Sampling**: Offers sub-sampling with variable step sizes in time to estimate fractal dimensions, making it highly suitable for fractal dimension analysis in fixed frame rate videos.
- **Correlation Sum**: Computes correlation dimensions using standard and Takens' methods.
- **Elbow Scale Detection**: Identifies optimal scales for fractal analysis using threshold or regression-based techniques, making it highly suitable for quantitative comparisons of fractal dimensions across different conditions.

---

## Dependencies

- `numpy`
- `scipy`

This library is lightweight and utilizes standard Python scientific libraries. Dependencies can be installed via:
```bash
pip install -r requirements.txt
```
Anaconda users may already have the necessary packages pre-installed.

---

## Functions

### Box Counting
#### `box_counting(points, scales, method="original", oversample_rate=2, return_boxes=False)`
- Computes fractal dimensions using the box counting method.
- **Parameters**:
  - `points`: A 2D array of points (n, 2).
  - `scales`: List of box sizes (scales).
  - `method`: Box counting method (`"original"`, `"oversample"`, or `"exact"`).
  - `oversample_rate`: Rate for oversampling when using the `"oversample"` method.
  - `return_boxes`: If `True`, returns box counts at each scale.
- **Returns**: Fractal dimension, R² value, p-value, and optionally box counts.

#### `box_counting_generalized(points, scales, q=2, return_boxes=False)`
- Computes generalized fractal dimensions, such as Renyi or q-dimensions.
- **Parameters**:
  - `q`: The order of the generalized fractal dimension.
  - Other parameters are identical to those in `box_counting`.

---

### Temporal Sampling
#### `temporal_sampling(points, min_step=1, max_step=2, q=1, start_index=0, return_boxes=False)`
- Estimates fractal dimensions by sampling points with varying temporal intervals.
- **Parameters**:
  - `min_step`, `max_step`: Range of step sizes for sampling.
  - `q`: The order of fractal dimension calculation.
  - `start_index`: Starting index for sampling.
  - `return_boxes`: If `True`, returns sampled points and intermediate results.

---

### Correlation Sum
#### `corr_sum(points, scales, min_gap=1, return_boxes=False)`
- Computes correlation dimensions by analyzing pairwise distances.
- **Parameters**:
  - `scales`: List of distance thresholds for identifying close pairs.
  - `min_gap`: Minimum separation between points to avoid trivial correlations.

#### `corr_sum_takens(points, min_gap=1, scale=None)`
- Implements Takens' method for correlation dimension estimation.
- **Parameters**:
  - `scale`: Distance threshold for valid pairs (optional).

---

### Elbow Scale Detection
#### `find_elbow_scale(xs, init_scales=None, method="threshold", pct_th=0.01, return_boxes=False, init_scale_config=None)`
- Detects the elbow point (optimal scale) for fractal analysis.
- **Parameters**:
  - `xs`: A 2D array of points (n, 2).
  - `init_scales`: List of initial scales for computation (optional).
  - `method`: Method for detecting the elbow point (`"threshold"` or `"regression"`).
  - `pct_th`: Percentage threshold for the `"threshold"` method.
  - `init_scale_config`: Configuration for initializing scales (optional).
- **Returns**: Indices, scales, and the minimum index of the optimal scale.

---

## Usage Example

```python
import numpy as np
from fractal import box_counting

# Generate some fractal-like data
points = np.random.random((100, 2))

# Define scales
scales = np.logspace(-3, 0, num=50)

# Compute fractal dimension
result = box_counting(points, scales, method="original")

print("Fractal Dimension:", result["fd"])
print("R²:", result["r_squared"])
```

Additional examples and tutorials are available in `tests/fractal_tests.ipynb`.

---

## Custom Utility Functions

The module includes a supplementary `utils` library for:
- **Range Detection**: `find_ranges_pct`, `find_ranges_ls`
- **Elbow Point Detection**: `get_reflex`

---

## Reference

Cui, T., Wang, T. *"Exact Box-Counting and Temporal Sampling Algorithms for Fractal Dimension Estimation with Applications to Animal Behavior Analysis."*

---

## Support and Contributions

For technical support, please report issues via the GitHub repository. Contributions are welcome, including bug fixes, feature additions, or general improvements. Submit your changes through a pull request.