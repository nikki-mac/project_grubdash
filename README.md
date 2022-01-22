
# 🍜 🍔 🌮 GrubDash 
⭐ **Backend Project for Thinkful's Software Engineering program** ⭐

❗ **Project Prompt:** 

You've been hired as a backend developer for a new startup called GrubDash! As another developer works on the design and frontend experience, you have been tasked with setting up an API and building out specific routes so that the frontend developers can demo some initial design ideas for the big bosses.

### Learning objectives
This project will test your ability to build APIs with complex validation. Before taking on this project, you should be comfortable with the learning objectives listed below:

- Running tests from the command line
- Using common middleware packages
- Receiving requests through routes
- Accessing relevant information through route parameters
- Building an API following RESTful design principles
- Writing custom middleware functions

For this project, you will be creating a server to access two resources, ```dishes``` and ```orders```, in addition to error handling.
Your server should follow the structure that you've learned in the program. Complete the following tasks to pass the tests: 

### Tasks
- In the ```src/dishes/dishes.controller.js``` file, add handlers and middleware functions to create, read, update, and list dishes. Note that dishes cannot be deleted.
- In the ```src/dishes/dishes.router.js``` file, add two routes: ```/dishes``` and ```/dishes/:dishId```. Attach the handlers (create, read, update, and list) exported from ```src/dishes/dishes.controller.js```.
- In the ```src/orders/orders.controller.js``` file, add handlers and middleware functions to create, read, update, delete, and list orders.
- In the ```src/orders/orders.router.js``` file, add two routes: ```/orders``` and ```/orders/:orderId```. Attach the handlers (create, read, update, delete, and list) exported from ```src/orders/orders.controller.js```.
- Anytime you need to assign a new ```id``` to an order or dish, use the ```nextId``` function exported from ```src/utils/nextId.js```

## 💻 Tech Stack

**Frontend:** JavaScript, React, CSS, Bootstrap

**Backend:** Node, Express, Knex, PostgreSQL

**Deployment:** Vercel


## 🌟 Demo

🌟[Click here for live demo](https://starter-grub-dash-front-end.vercel.app/dashboard)🌟


## Screenshots

![App Screenshot](https://res.cloudinary.com/strive/image/upload/w_1000,h_1000,c_limit/1fc7f916e2146e659f7934a73b103e25-home.png)


## Run Locally

Clone the project

```bash
  git clone https://github.com/nikki-mac/project_grubdash.git
```

Go to the project directory

```bash
  cd project_grubdash
```

Install dependencies

```bash
  npm install
```

Start the server

```bash
  npm run start
```


## Running Tests

To run tests, run the following command

```bash
  npm run test
```


## 📓 Project Requirements and Acceptance Criteria
### Project rubric
For your project to pass, all of the following statements must be true:

- All tests are passing.
- All middleware and handler functions have a single responsibility and are named functions.
- All data passed between middleware and handler functions uses ```response.locals```.
- All chained method calls on a ```route(...)``` end with ```all(methodNotAllowed)```.
- All update handlers guarantee that the ```id``` property of the stored data cannot be overwritten.

### Routes
To complete this project, you will create the following routes:

#### ```GET /dishes```
This route will respond with a list of all existing dish data.

- Example request:
```
GET http://localhost:5000/dishes
```
- Example response:
```
{
  "data": [
    {
      "id": "d351db2b49b69679504652ea1cf38241",
      "name": "Dolcelatte and chickpea spaghetti",
      "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
      "price": 19,
      "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350"
    }
  ]
}
```

#### ```POST /dishes```
This route will save the dish and respond with the newly created dish.

- **Validation**
    - If any of the following validations fail, respond with a status code of ```400``` and an error message.
        - **Validation ------------ Error message**:
            - ```name``` property is missing ------------ "Dish must include a name"
            - ```name``` property is empty ```""``` ------------ "Dish must include a name"
            - ```description``` property is missing ------------ "Dish must include a description"
            - ```description``` property is empty ```""``` ------------ "Dish must include a description"
            - ```price``` property is missing ------------ "Dish must include a price"
            - ```price``` property ```0``` or less ------------ "Dish must have a price that is an integer greater than 0"
            - ```price``` property is not an integer ------------ "Dish must have a price that is an integer greater than 0"
            - ```image_url``` property is missing ------------ "Dish must include a image_url"
            - ```image_url``` property is empty ```""``` ------------ "Dish must include a image_url"

- Example request:
```
POST http://localhost:5000/dishes
```
- Body:
```
{
  "data": {
    "name": "Dolcelatte and chickpea spaghetti",
    "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
    "price": 19,
    "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350"
  }
}
```
- Example response:

Status ```201```
```
{
  "data": {
    "id": "d351db2b49b69679504652ea1cf38241",
    "name": "Dolcelatte and chickpea spaghetti",
    "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
    "price": 19,
    "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350"
  }
}
```

### ```GET /dishes/:dishId```
This route will respond with the dish where ```id === :dishId``` or return ```404``` if no matching dish is found.

- Example request:
```
GET http://localhost:5000/dishes/3c637d011d844ebab1205fef8a7e36ea
```

- Example response:

Status ```200```
```
{
  "data": {
    "id": "d351db2b49b69679504652ea1cf38241",
    "name": "Dolcelatte and chickpea spaghetti",
    "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
    "price": 19,
    "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350"
  }
}
```

### ```PUT /dishes/:dishId```
This route will update the dish where ```id === :dishId``` or return ```404``` if no matching dish is found.

- **Validation**
    - The update validation must include all of the same validation as the ```POST /dishes``` route, plus the following:
        - **Validation ------------ Error message**:
            - ```:dishId``` does not exist ------------ "Dish does not exist: ${dishId}".
            - ```id``` in the body does not match ```:dishId``` in the route ------------ "Dish id does not match route id. Dish: ${id}, Route: ${dishId}"

*Note: The ```id``` property isn't required in the body of the request, but if it is present, it must match ```:dishId``` from the route.*

- Example request:
```
PUT http://localhost:5000/dishes/3c637d011d844ebab1205fef8a7e36ea
```
- Body:
```
{
  "data": {
    "id": "3c637d011d844ebab1205fef8a7e36ea",
    "name": "Century Eggs",
    "description": "Whole eggs preserved in clay and ash for a few months",
    "image_url": "some-valid-url",
    "price": "17"
  }
}
```
- Example response:
```
{
  "data": {
    "id": "3c637d011d844ebab1205fef8a7e36ea",
    "name": "Century Eggs",
    "description": "Whole eggs preserved in clay and ash for a few months",
    "image_url": "some-valid-url",
    "price": "17"
  }
}
```

### ```GET /orders```
This route will respond with a list of all existing order data.

- Example request:
```
GET http://localhost:5000/orders
```
- Example response:

Status ```200```
```
{
  "data": [
    {
      "id": "5a887d326e83d3c5bdcbee398ea32aff",
      "deliverTo": "308 Negra Arroyo Lane, Albuquerque, NM",
      "mobileNumber": "(505) 143-3369",
      "status": "delivered",
      "dishes": [
        {
          "id": "d351db2b49b69679504652ea1cf38241",
          "name": "Dolcelatte and chickpea spaghetti",
          "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
          "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350",
          "price": 19,
          "quantity": 2
        }
      ]
    }
  ]
}
```

### ```POST /orders```
This route will save the order and respond with the newly created order.

- **Validation**
    - If any of the following validations fail, respond with a status code of ```400``` and an error message.
        - **Validation ------------ Error message**:
            - ```deliverTo``` property is missing ------------ "Order must include a deliverTo"
            - ```deliverTo``` property is empty ```""``` ------------ "Order must include a deliverTo"
            - ```mobileNumber``` property is missing ------------ "Order must include a mobileNumber"
            - ```mobileNumber``` property is empty ```""``` ------------ "Order must include a mobileNumber"
            - ```dishes``` property is missing ------------ "Order must include a dish"
            - ```dishes``` property is not an array ------------ "Order must include at least one dish"
            - ```dishes``` array is empty ------------ "Order must include at least one dish"
            - a dish ```quantity``` property is missing ------------ "Dish ${index} must have a quantity that is an integer greater than 0"
            - a dish ```quantity``` property is zero or less ------------ "Dish ${index} must have a quantity that is an integer greater than 0"
            - a dish ```quantity``` property is not an integer ------------ "Dish ${index} must have a quantity that is an integer greater than 0"

- Example request:
```
POST http://localhost:5000/orders
```
- Body:
```
{
  "data": {
    "deliverTo": "308 Negra Arroyo Lane, Albuquerque, NM",
    "mobileNumber": "(505) 143-3369",
    "status": "delivered",
    "dishes": [
      {
        "id": "d351db2b49b69679504652ea1cf38241",
        "name": "Dolcelatte and chickpea spaghetti",
        "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
        "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350",
        "price": 19,
        "quantity": 2
      }
    ]
  }
}
```

*Note: Each dish in the Order's ```dishes``` property is a complete copy of the dish, rather than a reference to the dish by ```ID```. This is so the order does not change retroactively if the dish data is updated some time after the order is created.*

- Example Response:

Status ```201```
```
{
  "data": {
    "id": "5a887d326e83d3c5bdcbee398ea32aff",
    "deliverTo": "308 Negra Arroyo Lane, Albuquerque, NM",
    "mobileNumber": "(505) 143-3369",
    "status": "delivered",
    "dishes": [
      {
        "id": "d351db2b49b69679504652ea1cf38241",
        "name": "Dolcelatte and chickpea spaghetti",
        "description": "Spaghetti topped with a blend of dolcelatte and fresh chickpeas",
        "image_url": "https://images.pexels.com/photos/1279330/pexels-photo-1279330.jpeg?h=530&w=350",
        "price": 19,
        "quantity": 2
      }
    ]
  }
}
```

### ```GET /orders/:orderId```
This route will respond with the order where ```id === :orderId``` or return ```404``` if no matching order is found.

- Example request:
```
GET http://localhost:5000/orders/f6069a542257054114138301947672ba
```
- Example response:

Status ```200```
```
{
  "data": {
    "id": "f6069a542257054114138301947672ba",
    "deliverTo": "1600 Pennsylvania Avenue NW, Washington, DC 20500",
    "mobileNumber": "(202) 456-1111",
    "status": "out-for-delivery",
    "dishes": [
      {
        "id": "90c3d873684bf381dfab29034b5bba73",
        "name": "Falafel and tahini bagel",
        "description": "A warm bagel filled with falafel and tahini",
        "image_url": "https://images.pexels.com/photos/4560606/pexels-photo-4560606.jpeg?h=530&w=350",
        "price": 6,
        "quantity": 1
      }
    ]
  }
}
```

### ```PUT /orders/:orderId```
This route will update the order where ```id === :orderId```, or return ```404``` if no matching order is found.

- **Validation**
    - The update validation must include all of the same validation as the ```POST /orders``` route, plus the following:
        - **Validation ------------ Error message**:
            - ```id``` of body does not match ```:orderId``` from the route ------------ "Order id does not match route id. Order: ${id}, Route: ${orderId}."
            - ```status``` property is missing ------------ "Order must have a status of pending, preparing, out-for-delivery, delivered"
            - ```status``` property is empty ```""``` ------------ "Order must have a status of pending, preparing, out-for-delivery, delivered"
            - status property of the existing order === "delivered" ------------ "A delivered order cannot be changed."

*Note: The ```id``` property isn't required in the body of the request, but if it is present it must match ```:orderId``` from the route.*

- Example request:
```
PUT http://localhost:5000/orders/3c637d011d844ebab1205fef8a7e36ea
```
- Body:
```
{
  "data": {
    "deliverTo": "Rick Sanchez (C-132)",
    "mobileNumber": "(202) 456-1111",
    "status": "delivered",
    "dishes": [
      {
        "id": "90c3d873684bf381dfab29034b5bba73",
        "name": "Falafel and tahini bagel",
        "description": "A warm bagel filled with falafel and tahini",
        "image_url": "https://images.pexels.com/photos/4560606/pexels-photo-4560606.jpeg?h=530&w=350",
        "price": 6,
        "quantity": 1
      }
    ]
  }
}
```
- Example response:
```
{
  "data": {
    "id": "f6069a542257054114138301947672ba",
    "deliverTo": "Rick Sanchez (C-132)",
    "mobileNumber": "(202) 456-1111",
    "status": "delivered",
    "dishes": [
      {
        "id": "90c3d873684bf381dfab29034b5bba73",
        "name": "Falafel and tahini bagel",
        "description": "A warm bagel filled with falafel and tahini",
        "image_url": "https://images.pexels.com/photos/4560606/pexels-photo-4560606.jpeg?h=530&w=350",
        "price": 6,
        "quantity": 1
      }
    ]
  }
}
```

### ```DELETE /orders/:orderId```
This route will delete the order where ```id === :orderId```, or return ```404``` if no matching order is found.

- **Validation**
    - The delete method must include the following validation:
        - **Validation ------------ Error message**:
            - ```status``` property of the order !== "pending" ------------ "An order cannot be deleted unless it is pending."

- Example request:
```
DELETE http://localhost:5000/dishes/3c637d011d844ebab1205fef8a7e36ea
```
- Example response:

Status ```204``` and no response body.
