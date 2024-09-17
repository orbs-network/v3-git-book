# Deploying to Production

## Before you deploy

1. Make sure your project conforms to the strict directory structure specified in [Project Template](project-template.md).\

2. Make sure your [test suite](testing-locally.md) is passing and you're confident that the code is working.\

3. Make sure you're only using NPM packages from the [allowed list](index.js-implementation/allowed-packages.md).\

4. If your lambda sends transactions, make sure you have enough funding for gas costs, as described under [Sending Transactions](index.js-implementation/sending-transactions.md).

## Deploy your lambda

To deploy your lambda, submit a PR ([pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)) to the official Orbs Lambda repo on GitHub.

GitHub repo: [https://github.com/orbs-network/orbs-lambda](https://github.com/orbs-network/orbs-lambda)

Once your PR is submitted, circleCI will go over it and run some sanity tests to make sure it conforms with our guidelines. It produces error messages so you can get an underrating of what's wrong.

Additional errors and feedback over your PR will appear in GitHub as comments. If your PR is merged successfully, there were no errors in the submission.

Your lambda may take several hours until it starts executing in production by the validators of the network. Validators synchronize lambda changes automatically several times a day.
