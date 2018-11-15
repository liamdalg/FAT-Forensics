# Testing

## Backend

Our backend runs **Flask**, which uses Python. To test this, we use:

* **Pytest** (to test specific assertions)
* **Pylint**; (to test if the program compiles, and if a consistent coding style is used)

A **database** (PostgreSQL) is used alongside Flask, which is also primitively tested (insertion/deletion/format of data).

## Frontend

The frontend is mostly **JS**. There are a few aspects which we can test:

We run **Selenium** on CircleCI to test the usability of the site - it can simulate button activations.

Using **Jest**, we write some unit tests for the graph library we use, **Cytoscape**. These verify that basic functionality works (i.e. adding/deleting nodes).

We could test how the site looks, but we decided against it since changes to the UI are often and sometimes very slight, making it difficult to keep the tests current.

## Testing Workflow

In all, our testing workflow relies on:

* **Local** user testing
* Tests ran on **CircleCI** (during which: all python modules are reinstalled; the database is reset (i.e. a 'clean slate'))

![Testing Workflow](assets/testing-workflow.png)

This assures us that our code works on more than just one machine.

### Why CircleCI?

We looked at different methods of CI and decided on CircleCI because of its **ease of use** and **speed of setup**. We found that **Jenkins** took a lot of setup, including hosting it on our own server, wheras with CircleCI we can operate cloud-based on their servers. **TravisCI** was another contender but ultimately we wanted the ability to deploy our site to Heroku all in one platform.