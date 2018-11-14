# OO Design & UML

## High-Level

## Database

> Why not SQLite/any other alternative?

Heroku uses an *ephemeral filesystem*<sup>1</sup> (i.e. any files written are deleted the moment the dyno is stopped/restarted). This makes SQLite unsuitable as it works on memory and you'd lose your database every 24 hours or so, as opposed to Postgres which works over multiple dynos.

In addition, Heroku also has great support for Postgres.

## ORM

## Flask

- lightweight
- don't want full stack
- use extensions for precisely what we want
- our actual website isn't large
- lot to learn - flask easier
- no bogging down

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

Cytoscape renders on the frontend using a HTML canvas, which does mean that we rely on the library either being lightweight or the user having sufficient hardware to run it. Since the tool is research-oriented, our client told us to only target the desktop platform and ignore mobile/tablet users, which means that most if not all of our users can run Cytoscape. We tested other libraries such as **Sigma.js**, but found that it both runs worse than Cytoscape and lends itself more to densely connected networks rather than a directed graph structure. 

Unfortunately, Cytoscape is a large library (1MB+ including other extensions) which could negatively affect the load times of the page. In 2016, the average website had an average script size of 357kb<sup>2</sup>, so we plan to reduce the size of our scripts by using compression and a build tool to bundle the scripts together. 

## References
1. https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem