# Contributing Traces to the Repository

Thank you for contributing to the PtDAlgorithms trace repository!

## Quick Start

### 1. Build Your Model

```python
from phasic import Graph
import numpy as np

def your_callback(state):
    # Your model logic
    ...
    return [(next_state, base_weight, [coefficients])]

graph = Graph(
    state_length=...,
    callback=your_callback,
    parameterized=True,
    nr_samples=...
)
```

### 2. Record Trace

```python
from phasic.trace_elimination import record_elimination_trace

trace = record_elimination_trace(graph, param_length=...)
```

### 3. Publish to IPFS

```python
from phasic import TraceRegistry

metadata = {
    "model_type": "coalescent",
    "domain": "population-genetics",
    "param_length": 1,
    "vertices": 5,
    "description": "Clear, concise description",
    "author": "Your Name <email@domain.com>",
    "tags": ["coalescent", "kingman"],
    "license": "MIT"
}

registry = TraceRegistry()
cid = registry.publish_trace(
    trace=trace,
    trace_id="unique_descriptive_name",
    metadata=metadata,
    submit_pr=True
)
```

### 4. Submit Pull Request

1. Fork this repository
2. Add your trace entry to `registry.json` (format printed by publish_trace)
3. Submit pull request
4. Maintainer will review and merge

## Naming Conventions

- Use lowercase with underscores: `model_type_n_params`
- Include key parameters: `coalescent_n10_theta2`
- Be descriptive but concise: `structured_coalescent_2pop_mig`

## Quality Guidelines

1. **Documentation**: Include clear description and tags
2. **Metadata**: Fill all relevant fields
3. **Testing**: Verify trace works before publishing
4. **Reproducibility**: Include construction code when possible
5. **Citation**: Cite papers/methods used

## Questions?

Open an issue or contact: kaspermunch@birc.au.dk
