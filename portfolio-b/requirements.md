# Requirements

Our task is to build a very specialist tool, to be used predominantly by experts and business professionals. Because of this, our job is rendered somewhat open ended due to the need for a fully robust tool and code reviewed files. We had to build a sophisticated fundamental framework for the tool, and discussed with our client throughout the project which features should be of priority. Below is the official list of requirements we were given by our client correspondent, Kacper Sokol:         

1. A web application written in Python that can be integrated with our toolbox when it is open sourced in May 2019.
2. Integrated with a dummy implementation of our toolbox to guarantee future compatibility.
3. Single user.
4. 2 modes of operation: composing a computational graph and executing it.
5. Inspecting 3 key aspects of predictive modelling: data, models and predictions.
6. Allowing to inspect fairness, accountability and transparency (with algorithms provided by our toolbox) of predictive modelling pipelines.
7. Allowing the user to interact (create and edit) data processing workflows (graphs) and inspecting their FAT properties at any stage with appropriate visualisations.
8. Providing persistence of data processing workflows and computation outcomes (allow them to be saved, downloaded and restored).

## Stakeholders

| Stakeholder                   | Vested Interest                                                                                                                                                                                                    |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Researchers & Developers      | Researchers & developers interested in machine learning would be the main end users of the product, since they would use the tool to evaluate and optimise their own predictive algorithms.                        |
| Client                        | The client wants to include our product as a frontend to their product, FAT-Forensics. Our product would be used in promotional material for research papers and conferences.                                      |
| Thales UK (Client’s investor) | Naturally, they have a financial interest in the success of the tool. Additionally, they will be continuing on with the development of our tool once we’re finished.                                               |
| Society                       | Nowadays, many decisions are made with the help of AI which have strong social implications on society. If the tool is successful, it could revolutionise the way developers evaluate the FAT of their algorithms. |
| Minority Groups               | Minority groups are frequently misrepresented by predictive algorithms. Our tool will aid developers in creating a more fair and reliable predictive algorithm.                                                    |

## High Level Use-case Diagram

![Use Case Diagram](images/User_case_diagram.png) 

## Use-cases

Since this is ultimately a research tool, there are countless potential use cases depending on what information the user is trying to extract. However, there are some core use cases that all users will need to proceed to make use of our tool. These include opening the initial data graph, adding a child to a node - no matter the graph, instantiating a model or prediction graph from a node, and of course, analysing a node using the inspector tool.

### Opening the Data Graph (from home page):
 	
1. Select dataset from option form
2. Select “create new graph”
3. Name the graph
4. Select “open graph

This will create single node on a graph representing the chosen dataset, but there are alternative flows that a user may want to take, for example:

1. Choose “upload custom”
2. Select “browse” for datasets
3. Choose file from computer
4. “Submit”
5. Choose selected dataset
6. Name graph
7. Open graph

This will create a single node graph representing the dataset uploaded. There are also other alternate flows such as choosing an existing graph that has been saved in the server.

### Adding a Child Node (from any existing graph)

1. Click on desired node
2. Select “add child” in the pop-over
3. Name the new node
4. Add description (optional)
5. Select appropriate transformation, indices, and axis
6. Click “save”

This will apply the chosen transformation to the node and represent it as a child to the node on the graph.

### Convert to Model/Prediction Graph (from data/model graph respectively)

1. Click “execute functions”
2. Click on desired node
3. Click “convert to model”/ “convert to prediction” on the pop-over

This will either open previously formed graph, or instantiate a new one if necessary. This is a case where we have an exceptional workflow, where if a user does not ‘execute functions’, the data stored in the node will not have functions applied, so training a model from it will be futile.

### Inspect

1. Click “execute functions”
2. Click on desired node
3. Click “inspect on the pop-over

From here, the inspector tool will show, showing relevant information. This, similarly to converting to model, has an exceptional workflow, where analytics formed from each node before the functions are applied will be meaningless.

## Functional Requirements

The core functionality of FAT-Forensics, and by extension FAT-Inspector, is to evaluate the FAT of predictive algorithms. To view the FAT metrics, the user needs to access the inspector view; therefore, our main use-case for the tool is the the use of the inspector view.

To achieve our primary use case scenario, we have implemented the relevant functional requirements:

| Requirement                                                                                                                 | Rationale                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| The user must be able to upload a local dataset file.                                                                       | To calculate FAT metrics, the server must have access to the user's dataset.                                           |
| The user must be able to upload a local graph file.                                                                         | To have the ability to restore previous workflow at a later session                                                    |
| The user must be able to start a new graph with a dataset stored on the server.                                             | If the user doesn't have access to a graph, they need to start from scratch.                                           |
| The user must be able save an existing graph to the server.                                                                 | The server needs to have access to the most recent graph to access all nodes, without it the graph cannot be executed. |
| The user must be able to add children to nodes which represent applying the FAT-Forensics transformations                   | To be able to fine tune their classifier and see how different transformations affect the FAT                          |
| The user must be able to execute the node graph, which will apply the functions inside of each node.                        | To make use of said transformations in inspection, model training, and prediction making                               |
| The user must be able to edit the nodes on the graph by changing their name, description, and function.                     | To allow for users to make a mistake without heavily diverting workflow                                                |
| The user must be able to utilise the inspector tool on any node in the graph                                                | This is the critical funtionality of the tool and is the user's sole source of FAT analytica                           |
| The data stored in each node must be preserved on applying the transformations.                                             | The user may be interested in comparing how the FAT changes when different functions are applied.                      |
| The user must be able to train a model and make predictions, using the FAT package, from data and model graphs respectively | To instantiate new graphs from node and further fine tune the classifier with help of the inspector tool               |
| The user must be able to save the state of their graph and export it for later use                                          | To allow for more user friendly and flexible workflow                                                                  |

## Non-functional Requirements

These are some of the most important standards for our system to uphold:

| Requirement                                                         | Rationale                                                                                                              |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| The back-end must be built in Python 3.                             | The client's package, FAT-Forensics, is built in Python 3, and our back-end would need to interact with it.            |
| Python code shall be PEP8 compliant                                 | Our client's team enforces PEP8 on their code, and they will be continuing development of the product.                 |
| The system should be a single user application                      | This is within the scope of our development, and were advised by our client to not extend the capability to multi user |
| The system must be deployable on a web service such as Heroku, AWS. | System needs to be accessible by people without programming experience.                                                |
| The system must be modifiable                                       | Future developers must be able to work on our system so we must comply with their choice of languages                  |
| The system must be supported on Chrome (desktop)                    | This is our target platform and is the only platform necessary at this stage for our client                            |

We have not had need for many functional requirements. This is due to this project being mostly about providing a strong foundation for development of this web app, meaning a lot of standard non-functional requirements such as security, accessibility, and serviceability are not relevant to us.
