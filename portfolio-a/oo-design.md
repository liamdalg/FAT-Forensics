# OO Design & UML

## High-Level

Fill me in!

## Flask & Python

The core package which the client is giving us is written in Python, so we chose to use Python for our backend instead of Java. If we used Java we'd have to write all the bindings for the package which could take some time and add unecessary complexity to the task. Our client also said that they would like us to use Python over Java as they are more familiar with programming in Python.

For our RESTful API framework we decided to use **Flask**. Flask is a 'microframework', which means that it is very lightweight and easy to use, and does not provide extensive functionality. Therefore, Flask alone is not suitable for deployment, so we needed to also use **gunicorn** on Heroku to act as a WSGI server for Flask.

**Django** is another alternative that we considered, but we felt that it was:

* Too bulky (compared to **Flask** being a lot more lightweight), our actual website isn't that large so we don't need a full stack solution.
* Too much to learn. **Flask** is small and 'one-use'. We make up for the lack of full-stack support by using **Flask** extensions (e.g. **Flask-SQLAlchemy**).

## Database

We use **PostgreSQL** for our database - Heroku uses an *ephemeral filesystem*<sup>1</sup> (i.e. any files written are deleted the moment the dyno is stopped/restarted). This makes **SQLite** unsuitable as it works on memory and you'd lose your database every 24 hours or so, as opposed to Postgres which works over multiple dynos.

In addition, Heroku also has great support for **PostgreSQL**.

## ORM

We decied to use an ORM because they manage the SQL driver for us, which means that we don't need to deal with driver specific syntax and types. Using an ORM also means that we don't have to write any SQL, making our system more secure, and there's a one-to-one mapping between the data in our program and the data stored in the database. We chose **SQLAlchemy** over other ORMs since it has a nice binding with Flask in a package called **Flask-SQLAlchemy**.

For example, here's the model which represents the **Graph** table in the database:
```python
# models.py

db = SQLAlchemy()

class Graph(db.Model):
    graph_id = db.Column(db.Integer, primary_key=True)
    type = db.Column(db.Integer, nullable=False)
    name = db.Column(db.String, nullable=False)
    dataset = db.Column(db.Integer, db.ForeignKey('dataset.dataset_id'))
    data = db.Column(db.JSON, nullable=False)
```

## Graph Library

Our graphs are powered by **Cytoscape.js**, a frontend library for generating graph networks. Cytoscape boasts great features such as:

* Cross-platform using HTML canvas.
* Native exporting to JSON so the user can save or download the graph.
* Large extension pool and easily modifiable.
* Automatic layouts, meaning we don't have do manually define the position of each node.
* Customisable events on each part of the graph.

Cytoscape renders on the frontend using a HTML canvas, which does mean that we rely on the library either being lightweight or the user having sufficient hardware to run it. Since the tool is research-oriented, our client told us to only target the desktop platform and ignore mobile/tablet users, which means that most if not all of our users can run Cytoscape. 

We tested other libraries such as **Sigma.js**, but found that it both runs worse than Cytoscape and lends itself more to densely connected networks rather than a directed graph structure. **D3** was also an option, but we found that D3 is much more generic than Cytoscape and, like Sigma.js, better for dense networks.

Unfortunately, Cytoscape is a large library (1MB+ including other extensions) which could negatively affect the load times of the page. In 2016, the average website had an average script size of 357kb<sup>2</sup>, so we plan to reduce the size of our scripts by using compression and a build tool to bundle the scripts together. 

## References
1. https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem
2. https://www.keycdn.com/support/the-growth-of-web-page-size