## MVC Architecture

 Model-View-Controller (MVC) architecture is  **a design pattern that separates an application into three main components: Model, View, and Controller**. Each component has its own role in a project.

**Components**

-   **Model:** Handles data logic
-   **View:** Displays information from the model to the user
-   **Controller:** Controls the data flow into a model object and updates the view whenever data changes

[Expressjs Docs](https://expressjs.com/)

![enter image description here](https://www.freecodecamp.org/news/content/images/size/w1600/2021/04/MVC3.png)

For large projects, We divide MVC in more fine layer architecture like these follows:

![enter image description here]([https://www.freecodecamp.org/news/content/images/size/w1600/2021/04/MVC3.png](https://photos.google.com/search/_tra_/photo/AF1QipOYglWj-9rn9Y4J0tiJshP8uyeP8Sr4eQr1wpFD))

## Controller
[Middleware Docs](https://expressjs.com/en/guide/writing-middleware.html) 

### Basic Concepts:

1.  **Middleware Functions**:
    
    -   Middleware in Express is implemented as functions.
    -   These functions have access to the `request` (`req`) and `response` (`res`) objects, and they can modify the request, response, or terminate the request-response cycle.
2.  **Middleware Execution Order**:
    
    -   Middleware functions are executed in the order they are defined. Order matters in determining the flow of your application.
3.  **Next Function**:
    
    -   Middleware functions receive a third argument, `next`. Calling `next()` passes control to the next middleware in the pipeline. If `next()` is not called, the request-response cycle stops.
4.  **Application-Level and Route-Level Middleware**:
    
    -   Middleware can be defined at the application level (affecting all routes) or at the route level (affecting specific routes).

**Examples:**

```Javascript
const  express  =  require('express');

const  PORT  =  3000;

const  app  =  express(); // create a express server object

function  mylogger  = (req, res, next) => {

	console.log("Logging from middleware 1");

	// return res.json({msg: "done"}); // it will not go to next middleware because it will return from here

	next(); // calls the next middleware

}

function  extlogger  = (req, res, next) => {

	console.log("Logging from middleware 2");

	next(); // calls the next middleware

}

const  middleware  = [mylogger, extlogger]

// when somebody hits here it will go first mylogger , extlogger and then here last middleware

app.get('/home', middleware, (request, response) => {

	console.log("Last middleware"); // last middleware act as controller

	response.send("hi there, welcome to get");

	// response.json({

	// 		message: "OK get"

	// })

});
  

app.listen(PORT, () => {

	console.log(`Example app listening on port ${PORT}`)

})
```
- middleware + controller combined form big picture of Controllers
- middleware is the first interaction of controller
- last middleware is consider as controller because it finally send the request to the backend
- In middleware we can do request validation, that checks it follows the contract of API or not
- In Controller, forward req to backend logic like models and it prepares the response object
- It's always recomended Never do any kind of response object retuning without the return keyword.
- There is one more layer segregation in middleware i.e Routes
- Rgistration of middleware & Controller are in the Routes
- These three 3 makes Big picture of controller.

## Model 

- First layer of model is services, in services we writte our business logic.
- Services will depend on another layer callled repository layer.
- The role of repository layer is do db interaction.
- There is another folder along with Repository layer is seed, it is used for testing purpose for local prject.
- There is another folder called migration, It represent chnages in the schema at multiple time
- There is seprate folder called schema or models, for connect db 
- Trigger, stored procedure and define scema are in the model folder
- There is one another seprate folder called extra
- In this extra folder, config, utils and error handles

All the above folder comes under one folder i.e src/ and another folder called like test folder.

## Microservices vs. monolithic architecture

**Monolithic Architecture:**

-   A monolithic architecture is a traditional model of software design where all components are tightly integrated into a single, self-contained unit.
-   Monoliths are characterized by a single codebase that couples all business concerns together.
-   Updates and changes to a monolithic application require updating the entire codebase, making them restrictive and time-consuming.

**Advantages of Monolithic Architecture:**

-   Fast development speed due to a single codebase.
-   Easy deployment as the entire application is contained in one executable file or directory.
-   Simplified testing and debugging since all code is located in one place.

**Disadvantages of Monolithic Architecture:**

-   Slower development speed as the application grows.
-   Scalability challenges, as individual components cannot be scaled independently.
-   Reliability issues, as an error in one module can affect the entire application.
-   Barrier to technology adoption, as changes affect the entire application.
-   Lack of flexibility, constrained by technologies used in the monolith.

**Microservices Architecture:**

-   Microservices architecture consists of independently deployable services, each with its own business logic and database.
-   Services operate with specific goals, and updating, testing, deployment, and scaling occur within each service.
-   Microservices decouple major business concerns into separate, independent code bases.

**Advantages of Microservices Architecture:**

-   Agility, flexible scaling, and continuous deployment.
-   Highly maintainable, testable, and independently deployable.
-   Technology flexibility and high reliability.
-   Enables faster software updates and supports continuous integration and delivery.
-   Facilitates experimentation with new features and easy fault isolation.

**Disadvantages of Microservices Architecture:**

-   Development sprawl can lead to slower development and operational performance.
-   Exponential infrastructure costs as each microservice requires its own resources.
-   Added organizational overhead to coordinate updates and interfaces.
-   Debugging challenges due to distributed logs and complex business processes.
-   Lack of standardization and clear ownership as the number of services and teams grow.

**Migrating from Monolithic to Microservices:**

-   When monolithic applications grow too large and scaling becomes a challenge, migration to microservices may be considered.
-   A migration strategy, tooling, and management of expectations are critical during the transition.
-   Embracing a culture shift towards DevOps and balancing speed with reliability is essential for a successful migration.
