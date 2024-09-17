# Step by Step Overview

The development process of a new Orbs Lambda cloud function includes the following steps:\


1. **Select a unique ID** for your lambda function (alpha-numeric characters and dashes).\

2. **Create a local git repository** conforming to the appropriate project structure.\

3. **Implement the logic** of your cloud function in JavaScript (or TypeScript).\

4. **Write a simple test suite** to verify your lambda function logic locally.\

5. **Deploy your lambda** by creating a PR (git pull request) to the official Orbs repo on GitHub.\

6. **Wait until your lambda is deployed** by the system, errors and feedback will appear on the PR.\

7. **Analyze execution** of your lambda in production by examining the network [status page](https://status.orbs.network).
