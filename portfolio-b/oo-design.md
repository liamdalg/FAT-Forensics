# OO Design & UML

## High-level Architecture Diagram

![High-level Diagram](images/oo_hilevel.png)

For our RESTful API framework we decided to use **Flask**. Flask is a 'microframework', which means that it is very lightweight and easy to use, but does not provide extensive functionality. **Django** is another alternative that we considered, but it's use-case its for highly database driven websites. Flask is much smaller scale, and we can make up for any lack of functionality by using extensions.

Flask's default HTTP server runs on **Werkzeug**; a fine choice for development, but it is not efficient enough at large scales in production. Two popular alternative choices are **NGINX** and **gunicorn** (sometimes even both together). Flask and gunicorn are **WSGI** (Web Server Gateway Interface) compliant, while **NGINX** is not - therefore, we chose to use **gunicorn** to invoke our Flask application. 

We used React because a team member already had experience with it, and it allows us to develop stateful, reusable components. The graph is rendered using D3 and a third-party package which combines React and D3; this was required because D3 and React have conflicting ways of manipulating the DOM. To compile the frontend code, we used Babel + Webpack which allowed us to use modern Javascript (ES6) features without worrying about compatibility issues.

## Static UML Model

![Static UML Model](images/oo_static.png)

We need to pass data between the front-end and back-end and be able to manipulate it on both sides. D3 stores the data in a pure dictionary format (nodes and their links) - we had to decide if it was best to work directly on the D3 format or another format.

We convert the D3 dictionary into an internal structure called Tree. This allows us to implement more specialist, reusable operations instead of a wrapper over the dictionary. Since we convert the graph every time we receive it from the client, there is a performance loss. This could get very noticeable with larger graphs. However, it is much easier to traverse once converted (i.e. we can find a node quicker); working directly on the D3 dictionary would have been more difficult as it's in a strange format. 

Converting the graph into a common format means we condense all the front-end dependency into one conversion function, allowing us to more easily swap out the front-end or update the conversion function with newer versions. Storing the data on the server (pickling) is also better since we can store the data/model/prediction **with** the tree; we would have to create a class to unify them somehow or store the files separately with a key which would not be as elegant.

Even though there is a speed trade-off in storing our data in a Tree, it enables our code to be more succinct and readable.

## Dynamic UML Model

![Chart UML Model](images/oo_dynamic.png)

After selecting a node, the user can open the ‘inspect’ view to look at charts relating to the node’s data. The inspect view is split up into tabs for each of the FAT aspects, with different charts for each tab; the charts shown also depend on the current mode (i.e. histogram for fairness & data). We needed a way to transform the node’s data into all available charts.

We chose to depend on the server for the serving of all chart types and the generation of individual chart images & text. The main motivator behind this was that the data returned by the dummy library our client made is perfect for using matplotlib, as it’s in numpy form. We could have downloaded the data and then generated charts on the client side, which, whilst possibly faster for the client, would have taken more code. This also gives us the ability to dynamically choose which charts are shown and adjust what charts look like purely on the server side.

The possible chart types were chosen to be downloaded separately to the actual chart images and texts. It might have been better to combine both to reduce the number of requests from the client to server, but this allows us to display the chart title and possible arguments before the svg/text is loaded, as well as an error message/loading animation for individual charts. We also chose to download the possible chart types per mode rather than mode **and** tab to reduce the number of overall requests.

Whilst the generation of charts and separation of requests increased the required communication between client and server, it gave us more flexibility and power on the server’s side.