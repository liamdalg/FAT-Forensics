# Requirements

## Stakeholders:

When creating a research tool of this type, it is very important to keep our stakeholders in mind. Our users' experience with the product must be seamless and straight-forward as misinterpreting the data recieved may have severe knock-on effects to future research or development of a product. This could then negatively impact the consumers of products affected by research using our tool.
As well as this we must take into account investor and future development of our tool so we must create clean and efficient code that is understandable and logically neat.

### Developers

it is of upmost importance that if a developer plans to release a feature than recognises patterns in human interaction that the results are consistent across any one person that is using. For example a facial recogistion app - if the app is unreliable for users of particular races then it could heavily hinder the trust put in the product by its consumers and give the company a bad name.

### Consumers of Minority Groups

When creating ai features, companies usually use more the more abundant subculture of the area. this can lead to inaccurate results for people of the minorities that are not rfairly represented in the machine learningdatasets. this would quite frankly be an insult to a person who has invested their money into a product.

### Investors and Future Developers

We must create a clean work environment in effort to make the investors of Anthopometrics pleased with their invesment and want to keep backing the research of our client. This is also important to accommodate for future development on our product after we have finished.

### Researchers

Researchers may wish to see the connetations of less informed ai systems based on the (lack of) information we give it. With data this intricate and complex, it can be very hard to understand and take useful information from it. This leaves the job to us to create a sophisticated way of representing the data for ease of use.

![Use Case Diagram](assets/Usecase_diagram.png)

## Functional Requirements

The goal of the project is for researchers to easily assess and investigate social aspect of their predictive models. To help with this, we must comply to the following functional requirements:

- Ability to upload a dataset.
- Ability to load previously saved datasets.
- Ability to perform function on dataset from given pythn package to create new, altered dataset.
- Ability to name altered dataset along with a description.
- Ability to revert to older versions of said dataset without deleting later versions.
- Ability to view models and predictions based on current chosen dataset.
- Ability to manupulate graph views to see more details on area of interest.
- Ability to enter "inspector view" where it is possibble to compare datasets and view fairness analytics based on data in set after functions applied along with comparisons with other sets.
- Ability to export reports into pdf files.
- On screen guidance and logically organise for ease of use and readability.
- Ability to save datasets.

## Non-Functional Requirements

- It should have a user-friendly interface. Google have released a plugin called "what-if tool", for their TensorFlow visualisation framework called TensorBoard. It is similar with our project but it has a limitation of interacting only with TensorFlow models. We want to have larger audience and higher impact so we are making our project clear to use and the overall design should be simple but professional. This is the goal that we believe to be most paramount as we must ensure that researchers can use our product efficiently and easily to eliminate mistakes when handling important data, and that it is a more useful experience than the "what-if" tool.
- Since we have lots of graphs and data appear on our interface and our user would mainly choose to use a tablet for this, we won't implement a smartphone version for the project.
- The project should be able to be updated or changed to meet client's requirements.
- The system can only be changed by the admins of the project and all the data must be kept safe so they are not suspected, or disputed.
- The size of the project cannot be too large because we don't want it to be super slow when we load data. We should compress and tidy our code to minimise loading time.
