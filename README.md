# SAT

[![Build Status](https://travis-ci.org/CarloLucibello/SAT.jl.svg?branch=master)](https://travis-ci.org/CarloLucibello/SAT.jl)
[![codecov.io](http://codecov.io/github/CarloLucibello/SAT.jl/coverage.svg?branch=master)](http://codecov.io/github/CarloLucibello/SAT.jl?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/CarloLucibello/SAT.jl/badge.svg?branch=master)](https://coveralls.io/github/CarloLucibello/SAT.jl?branch=master)

Heuristic algorithms based on message passing for solving large instances of boolean satisfaction problems ([SAT](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem)).
Consider using [PicoSAT.jl](https://github.com/jakebolewski/PicoSAT.jl) if you are looking
for an exact solver.

## Installation
```julia
Pkg.clone("https://github.com/CarloLucibello/SAT.jl")
```

## Basic usage
```julia
using SAT
cnf = randomcnf(N=1000, k=3, α=0.5) # generate a random k-SAT instance
σ = solve(cnf)
```
The solution `σ` will be a vector of `N`  ints taking values `-1` or `+1`.
## Formulas
Formulas in conjunctive normal form ([CNF](https://en.wikipedia.org/wiki/Conjunctive_normal_form)) can be either read/written to files
```julia
cnf = readcnf("formula.cnf")
writecnf("formula.cnf", cnf)
```
or randomly generated from the k-SAT ensemble
```julia
cnf = randomcnf(N=1000, k=4, α=0.5, seed=17)
```

## Solvers

### BP + reinforcement (default)
Solve random instance with Belief Propagation (BP) inspired procedures.
`r` is the initial value of the reinforcement parameter (`r=0.` default).
`rstep` determines its moltiplicative increment.
```julia
σ = solve(cnf, rstep=0.001, maxiters=1000);
```
If having errors or unable to find a solution, try to reduce `rstep`.
### decimation
TODO
