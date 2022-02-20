# Execute Tests In Cypress Docker Container

Run Cypress tests inside the Cypress Docker container by running following shell command (you **DO NOT NEED** to install/ run `cypress install` on your localhost/ within the CI pipeline on a VM):

```bash
docker run -it -v $PWD:/e2e -w /e2e cypress/included:3.2.0
```

Explanation of `docker run` command line arguments:

```
 -it          = interactive terminal
 -v $PWD:/e2e = map current folder to /e2e inside the container
 -w /e2e      = set working directy to /e2e
```

Your Cypress project structure should look like this:

```
cypress/
  integration/
    spec.js
cypress.json
```

Source: [Run Cypress with a single Docker command](https://www.cypress.io/blog/2019/05/02/run-cypress-with-a-single-docker-command/)