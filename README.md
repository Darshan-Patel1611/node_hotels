Here's the updated README file incorporating the changes and adding details about authentication and authorization:

# Node Hotel Application

The **Node Hotel** application is a Node.js-based system developed using the Express.js framework, with MongoDB as the chosen database. This application manages information related to persons (staff) and menu items. It exposes specific endpoints to handle CRUD (Create, Read, Update, Delete) operations for both persons and menu items. Additionally, the application includes authentication and authorization using JWT (JSON Web Tokens) and Passport.js with a local strategy.

## Endpoints

### Authentication & Authorization

The application uses JWT for authentication and Passport.js with a local strategy for user login. Below are the endpoints for user authentication:

- **Sign Up a Person:**
  - Endpoint: `POST /person/signup`
  - Description: Registers a new person with details such as name, role, email, etc., and returns a JWT token.

- **Login a Person:**
  - Endpoint: `POST /person/login`
  - Description: Authenticates a person using username and password, and returns a JWT token.

- **Get Profile:**
  - Endpoint: `GET /person/profile`
  - Description: Retrieves the profile of the authenticated person.

### Persons
- **Add a Person:**
  - Endpoint: `POST /person/signup`
  - Description: Adds a person to the system with details such as name, role, etc.

- **Get All Persons:**
  - Endpoint: `GET /person`
  - Description: Retrieves a list of all persons in the system. Requires JWT authentication.

- **Get Persons by Work Type:**
  - Endpoint: `GET /person/:workType`
  - Description: Retrieves a list of persons based on their work type (e.g., chef, waiter, manager).

- **Update a Person:**
  - Endpoint: `PUT /person/:id`
  - Description: Updates the details of a specific person identified by their ID.

- **Delete a Person:**
  - Endpoint: `DELETE /person/:id`
  - Description: Deletes a person from the system based on their ID.

### Menu Items
- **Add a Menu Item:**
  - Endpoint: `POST /menu`
  - Description: Adds a menu item to the system with details such as name, price, taste, etc.

- **Get All Menu Items:**
  - Endpoint: `GET /menu`
  - Description: Retrieves a list of all menu items in the system.

- **Get Menu Items by Taste:**
  - Endpoint: `GET /menu/:taste`
  - Description: Retrieves a list of menu items based on their taste (e.g., sweet, spicy, sour).

- **Update a Menu Item:**
  - Endpoint: `PUT /menu/:id`
  - Description: Updates the details of a specific menu item identified by its ID.

- **Delete a Menu Item:**
  - Endpoint: `DELETE /menu/:id`
  - Description: Deletes a menu item from the system based on its ID.

## Data Models

### Person
The `Person` data model represents information about staff members in the hotel.

- **Fields:**
  - `name`: String (Person's name)
  - `age`: Number (Person's age)
  - `work`: Enum (Role in the hotel, such as chef, waiter, manager)
  - `mobile`: String (Person's mobile number)
  - `email`: String (Person's email address, unique)
  - `address`: String (Person's address)
  - `salary`: Number (Person's salary)
  - `username`: String (Person's username, unique)
  - `password`: String (Person's password, hashed before saving)

- **Example:**
  ```json
  {
    "name": "John Doe",
    "age": 30,
    "work": "waiter",
    "mobile": "123-456-7890",
    "email": "john@example.com",
    "address": "123 Main Street",
    "salary": 30000,
    "username": "john_doe",
    "password": "securepassword"
  }
  ```

### Menu Item
The `MenuItem` data model represents information about menu items available in the hotel.

- **Fields:**
  - `name`: String (Item's name)
  - `price`: Number (Item's price)
  - `taste`: Enum (Item's taste, such as sweet, spicy, sour)
  - `is_drink`: Boolean (Indicates if the item is a drink, default is `false`)
  - `ingredients`: Array of Strings (List of ingredients, default is an empty array)
  - `num_sales`: Number (Number of sales for the item, default is `0`)

- **Example:**
  ```json
  {
    "name": "Spicy Chicken Curry",
    "price": 12.99,
    "taste": "spicy",
    "is_drink": false,
    "ingredients": ["chicken", "spices", "vegetables"],
    "num_sales": 50
  }
  ```

## Usage

1. **Install Dependencies:**
   ```bash
   npm install
   ```

2. **Start the Server:**
   ```bash
   npm start
   ```

3. **Environment Variables:**
   Create a `.env` file in the root directory and add your MongoDB URI and JWT secret:
   ```env
   MONGO_URI=mongodb://localhost:27017/hotels
   JWT_SECRET=your_jwt_secret
   ```

## Authentication & Authorization
- **JWT Tokens:** The application uses JWT tokens for securing routes. Tokens are generated during user signup and login.
- **Passport.js:** The local strategy is used for authentication, leveraging the `Person` model to verify usernames and passwords.

### Middleware

- **JWT Authentication Middleware:** Verifies the token provided in the request headers.
- **Local Authentication Middleware:** Uses Passport.js to authenticate users with a username and password.

Example usage in routes:

```javascript
const { jwtAuthMiddleware } = require('./jwt');

// Protect routes with JWT middleware
router.get('/profile', jwtAuthMiddleware, (req, res) => {
  res.send('This is a protected route');
});
```

This README should provide a comprehensive overview of the **Node Hotel** application, its functionality, and how to use it.