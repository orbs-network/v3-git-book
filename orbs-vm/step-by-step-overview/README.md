# Step by Step Overview

The development process of a new Orbs VM service includes the following steps:\


1. **Select a unique ID** for your service (alpha-numeric characters and dashes).\

2. **Create a local git repository** conforming to the appropriate project structure.\

3. **Implement the logic** of your service in any language and wrap it as a single docker image.\

4. **Write a simple test suite** to verify your service logic locally.\

5. **Push your docker image** to a public docker registry such as [DockerHub](https://hub.docker.com/).\

6. **Deploy your service** by creating a PR (git pull request) to the official Orbs repo on GitHub.\

7. **Wait until service is deployed** by the system, errors and feedback will appear on the PR.\

8. **Analyze execution** of your service in production by examining the network [status page](https://status.orbs.network).
