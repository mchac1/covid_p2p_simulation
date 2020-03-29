# COVID-19 Spread Simulator for Tracing App

Simulator is built using [simpy](!https://simpy.readthedocs.io/en/latest/simpy_intro/index.html).
It simulates human mobility along with infectious disease spreading in a city, where city has houses, grocery stores, parks, workplaces, and other non-essential establishments.
Human mobility simulation is based on Spatial-EPR model. More details on this model are [here](https://www.nature.com/articles/ncomms9166) and [here](https://www.nature.com/articles/nphys1760).
The infection spread in this simulator is modeled according to what is know about COVID-19.
The assumptions about the spread implemented in the simulator are in [docs/inf_spread_simulator_assumptions.md](docs/inf_spread_simulator_assumptions.md)
We plan to update the simulator as more about COVID-19 will be known.

Our understanding of COVID-19 spread is documented in [docs/inf_spread_known.md](docs/inf_spread_known.md). The document will evolve with time.

The simulator is a sub-project of [Peer-to-Peer AI Tracing App](https://mila.quebec/en/peer-to-peer-ai-tracing-of-covid-19/). Read more about the app in Prof. Bengio's [blog post](https://yoshuabengio.org/2020/03/23/peer-to-peer-ai-tracing-of-covid-19/).

## Dependencies
Following `python` packages are required (python>=3.6)
```
simpy
scipy
numpy
```

## How to run it using command line?
Run the simulator as -
```
python simulate.py --n_people 100 --n_stores 100 --n_parks 10 --n_miscs 100 --init_percent_sick 0.01 --outfile data
```

Output will be in `data.pkl`. It is a `list` of `dict`.

### Parameters

```
parser.add_argument( '--n_people', help='population of the city', type=int, default=1000)
parser.add_argument( '--n_stores', help='number of grocery stores in the city', type=int, default=100)
parser.add_argument( '--n_parks', help='number of parks in the city', type=int, default=20)
parser.add_argument( '--n_miscs', help='number of non-essential establishments in the city', type=int, default=100)
parser.add_argument( '--init_percent_sick', help='% of population initially sick', type=float, default=0.01)
parser.add_argument( '--simulation_days', help='number of days to run the simulation for', type=int, default=30)
parser.add_argument( '--outfile', help='filename of the output (file format: .pkl)', type=str, default="")
parser.add_argument( '--print_progress', help='print the evolution of days', action='store_true')
```

### Accessing Simulation Data
Load the output of the simulator as following
```
data = pickle.load(open("data.pkl", 'rb'))
```

## How to run it as a function?
Although not designed with this usage in mind one can still call it like this
```
from simulate import sim
data = sim(n_stores=100, n_parks=50, n_people=100, n_misc=100, init_percent_sick=0.01, print_progress=False)
```

`data` is a `list` of `dict`.

## Semantics of code
`Human` class builds people, and `Location` class builds stores, parks, workplaces, households, and non-essential establishments.

## Semantics of Data
`data` is a `list`. Each entry in the `list` is an event represented as a `dict`.
The detailed information about events is in [docs/events.md](docs/events.md)

## TO DO
- [ ] Improve mobility simulator. [TO DOs here](docs/mobility_tasks.md)
- [ ] Improve infection spread simulator. [TO DOs here](docs/infection_spread_tasks.md)
- [ ] Add tests or sanity checks

## Contributing
To those who are familiar with the Github, please [follow the guidelines here for contributing](https://gist.github.com/MarcDiethelm/7303312).

There are several ways to engage in the project -
1. Contribution by Coding: There are several requirements currently listed in [To Do](#todo)
2. Contribution by Literature Survey: There is so much that we do not know about how COVID-19 spreads. [docs/inf_spread_known](docs/inf_spread_known) is where we are collecting this information. You can open a pull request there or open an issue.

## Collaborators
[@marco-gries](https://github.com/marco-gires), [@marie-pellat](https://github.com/mariepellat), [@teganmaharaj](https://github.com/teganmaharaj) [@giancarlok](https://github.com/giancarlok)
