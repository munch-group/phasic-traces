# PtDAlgorithms Trace Repository

This repository contains the central registry for pre-computed elimination traces for the PtDAlgorithms library (phasic).

## Overview

- **Traces** are stored on IPFS (decentralized, content-addressed storage)
- **Registry** (this repo) maps human-readable names to IPFS CIDs
- **Users** download traces automatically via `phasic.trace_repository`

## Usage

### Download a Trace

```python
from phasic import get_trace

# Download and load trace
trace = get_trace("coalescent_n5_theta1")

# Use with SVGD
from phasic.trace_elimination import trace_to_log_likelihood
from phasic import SVGD
import numpy as np

observed_times = np.array([1.2, 2.3, 0.8])
log_lik = trace_to_log_likelihood(trace, observed_times)
svgd = SVGD(log_lik, theta_dim=1, n_particles=100)
results = svgd.fit()
```

### Browse Available Traces

```python
from phasic import TraceRegistry

registry = TraceRegistry()
traces = registry.list_traces(domain="population-genetics")

for t in traces:
    print(f"{t['trace_id']}: {t['description']}")
```

## Contributing a Trace

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions.

Quick overview:

1. Build and record your trace
2. Publish to IPFS using `registry.publish_trace()`
3. Submit pull request to add your trace to `registry.json`

## Registry Structure

See `registry.json` for the complete schema. Each trace entry contains:

- **CID**: IPFS content identifier
- **Description**: Human-readable description
- **Metadata**: Model type, domain, parameters, etc.
- **Files**: Individual file CIDs (trace.json.gz, metadata.json, etc.)

## License

All traces are licensed under the MIT License unless otherwise specified in their metadata.

## References

- **PtDAlgorithms Paper**: [Røikjer, Hobolth & Munch (2022)](https://doi.org/10.1007/s11222-022-10155-6)
- **IPFS Documentation**: https://docs.ipfs.tech/
- **Main Repository**: https://github.com/munch-group/phasic
