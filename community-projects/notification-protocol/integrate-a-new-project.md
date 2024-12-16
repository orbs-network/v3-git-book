# Integrate a New Project

### How to integrate a new project

Integrating notifications for a new project requires implementing a small [web3](https://github.com/ChainSafe/web3.js)-compatible JavaScript class and creating a new [PR](https://docs.github.com/en/github/collaborating-with-pull-requests) to add the class to this repo.

### Example - low health notification for Aave

This notification aims to protect Aave users from liquidation by notifying them when their position health factor drops below 1.1:

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeUq586Y2GHoFSUPKPCEvvaS2ellXmyYAjoEbX4yR5g9gSWcUoSSUmjWtMGlmVSEqyuG62A_tMZSTvCumCAarLDxU3RbNBsAw7ndqHxdXhyiXWvjxycy2dEpKFp3mO3L00s6bvFMcYXOkmsP9_zb82h-c-f?key=PQMpZ1E3MCh7GiRyPT59fw" alt=""><figcaption></figcaption></figure>

### Documentation and more examples

Formal TypeScript type definitions for the class interface are available [here](https://github.com/open-defi-notification-protocol/projects/blob/master/interfaces.ts). Explore example integrations to different projects by browsing the different directories in this repo.

### Testing your integration

Before submitting the PR, you should test your integration manually. Let's assume that you're integrating a new lending project called "SuperLend". You've git cloned this repo locally, created your new integration in the new directory superlend and created the following new files:

`/superlend/project.json`\
`/superlend/near-liquidation.js`

To test your integration for the near liquidation notification do the following:

1. Make sure you're in the repo root
2. Run `npm install`
3. Create `/_test/dev-keys.json` (see example in that directory) containing your API key for a web3 service like Infura or Alchemy
4. Create `/_test/test-superlend.js` for your test, you can copy one of the other example test files
5. Run node `./_test/test-superlend.js`

### &#x20;Execution environment

These JavaScript classes are constantly executed by protocol alert nodes in order to analyze new blocks of on-chain data for notifying protocol subscribers. Alert nodes are currently supported on the [Orbs Network](https://orbs.com/) and executed by the public validators of the network.

#### Recent Community Contributions

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfbb6JaOKWTfqypYiOi4XqTqf7UZCeJYVM6TPa53E8Z_V9JYaHaVQ5ICfnWa-mXkI8OlP5eIh9IVozpABm5mhQpKmnQn72jU0LS-D1_vnU-bophhoPQoQXXlinofI8MWqwASRINce7GOK4Wi4xP9bvfCD8?key=PQMpZ1E3MCh7GiRyPT59fw" alt=""><figcaption></figcaption></figure>
