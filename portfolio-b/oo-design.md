# OO Design & UML

## High-level Architecture Diagram

![High-level Diagram](images/oo_hilevel.png)

* Relevant external systems
* Explanation of components

## Static UML Model

![Static UML Model](images/oo_static.png)

We need to pass data between the front-end and back-end and be able to manipulate it on both sides. D3 stores the data in a pure dictionary format (nodes and their links) - we needed to decide if it was best to work directly on the D3 format or another format.

We store trees
Convert D3 graph to python format
Instead of each time
We convert the D3 graph to a Tree format and 
Allows us to specify more specialist, reusable operations without simply a wrapper over the dictionary

Performance loss; converting every time :(
Since we convert the graph every time we receive it from the client, there is a performance loss. This could get very noticeable with larger graphs. However, it is easier to traverse once converted

Pushes dependency away from Tree and to build tree function (needs to be aware of front-end)

Converting the graph into a common format means we condense all the front-end dependency into one conversion function, allowing us to more easily swap out the front-end or update the conversion function with newer versions.

Working directly on the D3 dictionary would have been more difficult as it's in a strange format; the Tree provides an easier way to deal with on Python's end (i.e. we can find a node easily).

Pickling is also better

Helps coupling with dataset - can execute and do more than a regular dict

Helps to split up data

## Dynamic UML Model

![Chart UML Model](images/oo_dynamic.png)

After selecting a node, the user can open the ‘inspect’ view to look at charts relating to the node’s data. The inspect view is split up into tabs for each of the FAT aspects, with different charts for each tab; the charts shown also depend on the current mode (i.e. histogram for fairness & data). We needed a way to transform the node’s data into all available charts.

We chose to depend on the server for the serving of all chart types and the generation of individual chart images & text. The main motivator behind this was that the data returned by the dummy library our client made is perfect for using matplotlib, as it’s in numpy form. We could have downloaded the data and then generated charts on the client side, which, whilst possibly faster for the client, would have taken more code. This also gives us the ability to dynamically choose which charts are shown and adjust what charts look like purely on the server side.

The possible chart types were chosen to be downloaded separately to the actual chart images and texts. It might have been better to combine both to reduce the number of requests from the client to server, but this allows us to display the chart title and possible arguments before the svg/text is loaded, as well as an error message/loading animation for individual charts. We also chose to download the possible chart types per mode rather than mode **and** tab to reduce the number of overall requests.

Whilst the generation of charts and separation of requests increased the required communication between client and server, it gave us more flexibility and power on the server’s side.