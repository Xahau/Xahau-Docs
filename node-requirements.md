# Node Requirements

Hardware requirements for nodes (RPC, validator, ...) should be generally along the lines of the specs outlined below.

For specific node use cases (e.g. full history) specs may differ (and grow) over time.

### Nodes should run (reasonably) well for own use with:

* CPU: 6+ cores
* Memory: 16GB+ (32GB advised)
* Disk IO: 10k random RW
* Disk size: 100GB+
* Filesystem: EXT4/XFS/...
* Network IO: 100Mbit+

### Nodes for future (network growth) production use:

<table><thead><tr><th width="140"></th><th width="200">Minimum</th><th width="199">Preferred</th><th>Ideal</th></tr></thead><tbody><tr><td>CPU</td><td>16 cores</td><td>20+ cores</td><td>40+ cores</td></tr><tr><td>Memory</td><td>32GB</td><td>64GB</td><td>128GB+</td></tr><tr><td>Disk IO</td><td>15k random RW</td><td>20k random RW</td><td>30k random RW</td></tr><tr><td>Disk Size</td><td>500GB</td><td>1TB</td><td>2TB</td></tr><tr><td>Filesystem</td><td>XFS</td><td>XFS</td><td>XFS</td></tr><tr><td>Network IO</td><td>500Mbit+</td><td>1Gbit</td><td>10Gbit</td></tr></tbody></table>
