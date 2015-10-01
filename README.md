# NetworkDiscovery.jl

Smart Social Network Discovery using the POMDP framework.

A report describing this project is located in [doc/report.pdf](https://github.com/sisl/NetworkDiscovery.jl/blob/master/doc/report.pdf).

The ipython notebooks in [notebooks](https://github.com/sisl/NetworkDiscovery.jl/tree/master/notebooks) contain basic usage examples.

This code was designed to be used with the [POMDPs.jl](https://github.com/sisl/POMDPs.jl) framework. Unfortunately changes to this framework will probably make this code incompatible, so it will have to be updated to be used in the future.

The MCTS solver used for this is implemented in [POMCP.jl](https://github.com/sisl/POMCP.jl).

## Installation

```
julia> Pkg.clone("https://github.com/sisl/NetworkDiscovery.jl")
```

## Important elements of the code

### NetworkDiscovery.jl includes the most important structures.

* `CommunityNetwork` represents a social network with each vertex affiliated with a community, a `CommunityNetwork` object functions as the state of the POMDP.

* `CommunityAffiliationPOMDP` describes an entire problem, with the probing budget, statistical information for generating the network, etc.

* `ProbeNode` and `GuessAffiliation` are the types that represent actions. The `Neighborhood` type represents the observation.

### heuristic_belief.jl includes a data structure to hold the portion of the graph revealed by probing

* `RevealedGraph` holds all the edges and nodes revealed by probing. This structure is used by both the heuristic policy and the MCTS policy.

### heuristics.jl contains the heuristic policy

* `DiscoveryHeuristic` simply holds a probing policy and an affiliation-guessing policy. On steps 1 through T (see the report), it uses the `probing` policy to decide which vertex to probe; on step T+1, it uses the `guess` policy to guess the target node affiliation.

* `ProbeHighestDegree` probes the node with the highest revealed degree (see report)

* `GuessBasedOnNeighbors` guesses the target node affiliation as described in the report.

### problems.jl includes code to generate social networks and POMDP problems

### pomdp.jl includes a function to let the MCTS planner know what actions are available at what times

### visualization.jl includes code to automatically create svg images of the networks in ipython notebooks
