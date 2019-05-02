# Development Testing

Our backend is built with Python 3 and Flask, and to test these tools we used:

* **Pytest**: a Python package used to create unit tests which test the core functionality.
* **Werkzeug Test Client**: a client which ships with Flask to create integration tests which tests the Flask routes.

We opted for a **Test-Driven Development (TDD)** process when developing the backend. TDD ensures that components behave exactly as expected, even when the implementation of the components changes and evolves over time. It also provides a ‘sense of security’ - if our tests pass, then we can be confident that the backend is working as expected and the eliminate it as an issue source. Since the backend is critical for the success of our application, we felt that TDD was the best approach for ensuring stability.

On the other hand, a shortcoming of our product is that we did not extensively test the frontend, since we had issues with developing tests. We encountered many hurdles during development, which was caused by our lack of understanding of the client’s field of research, and how it relates to the product we were required to build. Significant portions of the frontend were updated as our understanding of the product improved and we were able to refine and update the design. As a result, we found it difficult to employ a TDD philosophy since the tests would become redundant quickly. Instead, we opted to iteratively add to and refine our application as we went.  

## Continuous Integration & Deployment

Our workflow involved working in separate git feature branches so that we have an isolated workflow. When we push our changes to GitHub, GitHub pushes them to CircleCI. Our CircleCI performs the following steps:

1. Install a fresh image with Python 3 and npm.
2. Install Python dependencies.
3. Install npm dependencies
4. Run Python tests.
5. Build npm packages.
6. If all steps complete successfully, and the current branch is master, deploy to Heroku.

This workflow allowed us to be confident in our application before deploying it. We know that if the application has deployed to Heroku, then it is working as intended (at least as far as our tests show).