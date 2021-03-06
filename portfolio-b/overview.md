# Overview

## Client Description

Our client is a research project at the University of Bristol, specializing in the analysis of **Fairness, Accountability and Transparency** (**FAT**) of predictive modelling. This was a 6-month pilot project that aimed to develop a Python toolkit that could be used for FAT research and possibly a deployment of FAT methods to monitor predictive algorithms. Their goal is to create a platform with such functionality that is accessible to a wide scope of users, even those with minimal knowledge and experience with **ML** (**machine learning**) systems.

## Application Domain

The tool is to be used for teaching (University of Bristol Interactive AI Centre for Doctoral Training) and research purposes. The client has a Python toolbox, which will be accessed by our product, which aims to unify the FAT research landscape by implementing state-of-the-art algorithms. The tool has two modes of operation:

* **Research** where the user can load it into an interactive Python session, e.g. a Jupyter Notebook, and investigate FAT aspects of a problem at hand.
* **Deployment** where the API of the tool can be used to provide analytics that, in turn, can be used for dash-boarding or monitoring of all components of predictive analytics: **Data**, **Models** and **Predictions** (**DMP**).

Our product will make use of the latter mode of operation and brings the functionality of the package to a wider audience by allowing them to interact with our toolbox via a 'drag and drop'/'point and  click' workflow rather than writing code directly.

## The Problem

In recent years, we have seen a massive rise in the number of hugely consequential decisions, such as court trials, being influenced by the models of predictive algorithms. This means that drastic alterations to people’s lives are partially subject to patterns in the ‘training data’ used to teach these systems. The problem is that this leaves these decisions vulnerable to influence from systematic oppression. This happens when there is a misrepresentation of marginalised communities in our records, which is undoubtedly the case, and learning algorithms start seeing features such as ethnic background as a dependent variable. 

Furthermore, there is very little in the way of universal regulations or tools in regards to testing these systems, with perhaps Google’s ‘What If’ tool being the best that is currently available. This tool is massively complicated, with a very steep learning curve, and in fact, our client specified that he did not like this tool due to its excessive complexity. Our client hopes to solve this problem with the FAT-Inspector web tool. The Python package provided is designed to perform the computation necessary for analysing predictive algorithms at each stage of classification (i.e. DMP). Our job is to create an intuitive tool to actualize the functionality of this package, for effective and perspicuous workflow.

## Our Vision

To fulfil the needs of this tool, our application had to be able to perform and interface all functionality necessary to review and refine classification algorithms. This includes transformations of data, training models with different datasets, tuning of models, performing splits on predictions based on various factors, and ultimately use FAT-Forensics’ inspector tool for fairness analysis. While most of the back-end functionality of this, like training the models, is taken care of by the FAT package, it was up to us to interface all functionality to the UI of the tool. Our tool represents workflow using node graphs; we allow users to upload their own dataset, creating an individual node representing said dataset. From here, they can add children to the node graph by choosing a transformation. The call to convert any data node to a model instantiates a new ‘model graph’, where the root node represents the model trained using its parent data node. This works similarly with predictions, where the model graph can be added to or taken from by applying functionality from the package, with each model node being able to be used form a prediction graph subject to transformation. At each level of the graph, and from any node instance in that graph, the inspector tool can be called, equipped with different analytics to represent the classifier respective to which stage of classification users are dealing with. This effectively gives users the ability to optimise their classifiers by fine-tuning parameters of the algorithm at each stage dependent on their implications of fairness, thus fulfilling our requirements.
