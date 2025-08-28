# PRPL Code

Code by the Princeton Robot Planning and Learning group (PI: [Tom Silver](https://tomsilver.github.io/)).

## Repositories

These repositories are meant to be actively maintained and reused across multiple projects.

* [python-starter](https://github.com/tomsilver/python-starter): A template for starting new repositories.
* [python-research-starter](https://github.com/tomsilver/python-research-starter): An example of how to organize a repository for a research project with experiments.
* [relational-structs](https://github.com/tomsilver/relational-structs): Data structures for relations between objects (as in PDDL or bilevel planning).
* [tomsgeoms2d](https://github.com/tomsilver/toms-geoms-2d): Data structures and utilities for simple 2D geometric shapes.
* [pddlgym](https://github.com/tomsilver/pddlgym): Gym environments created from PDDL domains.
* [pddlgym-planners](https://github.com/ronuchit/pddlgym_planners): Interface to PDDL planners for PDDLGym environments.
* [prpl-utils](https://github.com/Princeton-Robot-Planning-and-Learning/prpl-utils): General utilities for motion planning, PDDL planning, heuristic search, Gymnasium utils, and miscellaneous.
* [prpl-llm-utils](https://github.com/Princeton-Robot-Planning-and-Learning/prpl-llm-utils): Utilities for LLMs and VLMs.
* [prpl-perception-utils](https://github.com/Princeton-Robot-Planning-and-Learning/prpl-perception-utils): Utilities for perception.
* [bilevel-planning](https://github.com/tomsilver/bilevel-planning): Code for bilevel planning. Does not include learning or any environment-specific models.
* [pybullet-helpers](https://github.com/tomsilver/pybullet-helpers): Utilities and data structures for planning and simulation with PyBullet.
* [prbench](https://github.com/Princeton-Robot-Planning-and-Learning/prbench): Benchmark environments for physical reasoning with robots.
* [prbench-models](https://github.com/Princeton-Robot-Planning-and-Learning/prbench-models): Models for PRBench baselines.

## Dependency Structure

An edge A->B means that repository A depends on repository B.

<img width="2147" height="1467" alt="deps" src="https://github.com/user-attachments/assets/505c59d0-d31b-489b-8074-70bd75b1b3ea" />

<details>

<summary>Expand to see dependency graph code</summary>

```
digraph deps {
  rankdir=LR;
  node [shape=box, fontsize=12, style=filled, fillcolor=lightgrey];

  python_starter;
  tomsgeoms2d;
  pddlgym;
  prpl_utils;
  prpl_llm_utils;
  prpl_perception_utils;
  pybullet_helpers;

  python_research_starter -> prpl_utils;
  relational_structs -> prpl_utils;
  bilevel_planning -> relational_structs;

  pddlgym_planners -> pddlgym;

  prbench -> relational_structs;
  prbench -> prpl_utils;
  prbench -> tomsgeoms2d;
  prbench -> pybullet_helpers;

  prbench_models -> prbench;
}
```

To update, make changes to the content below, save to `deps.dot`, and run ```dot -Tpng -Gdpi=300 deps.dot -o deps.png```.

</details>


## Why So Many Repositories?

Previously, we developed a monorepo called [predicators](https://github.com/Learning-and-Intelligent-Systems/predicators). There are advantages and disadvantages of a monorepo versus our current setup.

#### Advantages of Current Setup
* The development process is faster because each repo has its own CI checks. For example, we don't run unit tests for other repos when doing a pull request for one.
* Each research project only uses a subset of the repos. It may be easier for new users to find their way around if they don't have the other code in the same repo.
* Smaller repositories with minimal dependencies are easier to install. Users don't need to install every dependency for every project.

#### Disadvantages of Current Setup
* It is harder to stay in sync when multiple changes are happening simultaneously across multiple repositories.
* When one repository depends on another one, we need to regularly reinstall the upstream repository (or use submodules, which has its own challenges).
* Breaking changes may not be identified until new pull requests are opened.

We will revisit this decision over time and see if we can find a solution that has all of the advantages and none of the disadvantages while still maintaining code accessibility for users with different levels of software engineering experience.
