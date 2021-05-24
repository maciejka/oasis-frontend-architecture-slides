# Oasis Frontend
## architecture + practices
## =
## effective process



## Disclaimer
* this is about tech, but
* any particular tech is not that important
* tech is applied by certain people to solve a specific task
* trilateral fit between tech, people and a task



## Disclaimer
what is described below is an account of the particular balance of the three that over the years we found to work for Oasis frontends



## Problem
* agile = iterative, incremental
* high quality
* long life span
* developed by a team(cross functional)



## People
* open to general purpose programmers
* usually proficient at frontend javascript
* don't need to be blockchain experts to provide usefull input



## Toolbox
general purpose tools _composed_ to act in harmony:
* Typescript
* React with theme-ui(dai-ui) for the views
* RxJS for everything else



# Composition
Ideas/Patterns/Practices



## Functional programming
* simple subset of "functional programing"
* immutability, higher order functions, curry
* goes well with React, RxJS
* easier to reason about functions than objects



## Modularization
* loosely coupled modules
* explicit dependencies
* late binding, application setup at runtime
* modules available to presentations via react hooks
* 'poor man's' dependency injection


## Modularization/Examples
* module: [vaultHistory.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/vaultHistory/vaultHistory.ts)
* dependency setup: [AppContext.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/components/AppContext.ts)



## Bussines logic separation
* state model data based
* explicit representation
* independent of presentation
* module based implementation



## Logicless presentations
* logicless = look is the only concern
* little use of `useState`
* parallel work on presentation and bussines logic
* multiple presentation modes possible (browser vs native client)


## Bussines logic separation/Examples
* simple model: [vaultHistoryEvents.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/vaultHistory/vaultHistoryEvents.ts)
* advanced model: [manageVault.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/manageVault/manageVault.ts#L182)
* presentation: [ManageVaultButton.tsx](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/manageVault/ManageVaultButton.tsx#L88)
* deserves workshop on its own



## RxJs Everywhere
bussines logic implemented as rx pipelines:
* blockchain transactions
* data transformations
* user input
* backend services


## RxJs Everywhere/Examples
* transactions: [reclaimCollateral.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/reclaimCollateral/reclaimCollateral.ts#L27), [proxyActions.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/blockchain/calls/proxyActions.ts#L286)
* data transformations/backend: [vaultHistory.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/vaultHistory/vaultHistory.ts#L103)
* user input: [ilksFilters.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/ilks/ilksFilters.ts#L16)



## Development process
* healthy dose of usual [agile practicies](https://en.wikipedia.org/wiki/Agile_software_development#Agile_software_development_methods)
* healthy = _not too much, not too little_



## Notable practicies
* storybooks
* pipeline unit tests
* both productivity and quality control



## Focus
![19th century](images/surgery%20in%20the%20nineteenth%20century.jpg)



## Focus
![modern century](images/modern%20surgery.jpg)



## Pipeline unit testing
* bussines logic at the pipeline level
* pipelines mockable thanks to explicit dependencies
* speeds up development, regression tests


## Pipeline unit testing/Examples
[manageVault.test.ts](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/manageVault/tests/manageVault.test.ts#L179)



## Storybooks
* fixes "operating field" for the iterative act of ui development
* speeds up exhaustive exploration of ui state space
* communication tool - generated on each commit, available to non technical team members
* quality control aspect:
    * "manual" visual inspection
    * automated visual testing (to be integrated)


## Storybooks/Examples
* [manage-waiting-for-approval](https://storybook.oasis.app/6d862b8/index.html?path=/story/managevault--manage-waiting-for-approval)
* [ManageVaultView.stories.tsx](https://github.com/OasisDEX/oasis-borrow/blob/5db192af0287e6e6e426109d7f2d09a72cf8fba3/features/manageVault/stories/ManageVaultView.stories.tsx#L264)




## Hypothesis
it should be easier to develop with pipeline unit tests and storybooks than without
* better focus
* quick iterative feedback
* works for storybooks
* not so clear with pipeline unit tests



## Test piramid
* basic unit tests
* pipeline unit tests
* storybooks
* minimal functional tests (endtest.io)



## Unequal battle against entropy
_The second law of thermodynamics, in principle, states that a closed system's disorder cannot be reduced, it can only remain unchanged or increase. A measure of this disorder is entropy. This law also seems plausible for software systems; as a system is modified, its disorder, or entropy, tends to increase. This is known as software entropy._

[wikipedia](https://en.wikipedia.org/wiki/Software_entropy)


## The end




## Scrapbook

## Using RxJS to build bussiness models
* pipelines created by functions
* parameters are explicit, treated as dependencies
* late binding, application setup/arming in AppContext.ts
* pipelines available to views via hooks: `useAppContext`, `useObservable`
* non functional aspects like caching configurable at setup time



### `AppContext.ts` setup dependencies
* create pipelines that forms bussines model of the app
* model distributed to the views via React context
* models that require parameters at the moment of usage are just curried and memoized functions



### React RXJS glue
* `useAppContext`
* `useObservable`


### Backend data processing
Examples


### Handling user input
* reducer pattern rxjs way
* state machines when necessary managed by pipelines
Examples: simple, complicated


## Blockchain access
Osis Commons
* web3context - web3react based
* connectors: mm, hw wallets, wallet link/connect, others
* call definitions
* transactions definitions
* transactions.ts module
