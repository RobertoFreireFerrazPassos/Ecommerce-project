# Ecommerce-project

### Technical details:

- Use Task.WhenAll
- Use IHttpClientFactory
- Use structure built-in logging
- Use Health Checks
- Use Token Cancelation 
- Use Polly policies
- Use UnitTests with NSubstitute
- Entity framework Core: Migrations for managing database schema changes, N + 1 Problem, Concurrency and Improved performance and reduced memory usage
- Use Model Validation
- DI
- Use Identity and roles and claims
- Use Swagger

## Frontend Web Application:

### Technical details:

- Use blazor server side
- Registration and Authentication will be secure but simple (JWT and not oauth)

### Features:

- User Registration and Authentication
- Product Catalog: Order by price, filter by category, pagination. Implement search functionality for finding products quickly. Include product names and prices. 
- Product Details Page: Include product name, quantity, description and price.
- Shopping Cart: Enable users to add products to their shopping cart. Display the cart's content, quantities, and prices. Allow users to edit or remove items from the cart.
- Checkout Process: Simple page for users to review and complete their orders. No shipping and billing information.
- Order History: Allow users to view their order history and track the status of current orders. Status: Order Placed. Order Processing (This status means that the order is being prepared for shipment. It includes tasks like product picking, packing, and labeling.), Shipped and Complete.
- Product Availability and Inventory Status: Implement inventory management and restocking notifications for administrators.
- Multilingual: Support multiple languages.
- Analytics and Reporting: For administrators. Analyze sells by category.

## API gateway:

### Technical details:

- Not controllers. Only middlewares.
- Authentication: Add middleware for authentication JWT
- Request Routing: Json file to redirect request to the proper APIs.
- Rate Limiting: Implement rate limiting policies.
- Caching: Implement caching for Shopping Cart
- Request and Response Transformation: The front end must not change the request if possible for new for versioning APIs. The API gateway should modify requests and responses to adapt to a new request format for a newer API version.
- Error Handling: Centralized error handling and error message standardization are essential. The API gateway can catch errors from backend services and return consistent error responses to clients.
- API Composition: The API gateway must orchestrate calls to various microservices, aggregate the data, and return it to the client as a single response.
- Logging: The API gateway should log requests and responses.
- Security: Protect against common web application security threats, such as cross-site scripting (XSS) and cross-site request forgery (CSRF).
- Add Health Checks to the APIs.

### Features:

All requests will go through this API.
Access user service for authentication and authorization
Access Product Service
Aggregate orders accessing Order Service and Product Service using SKU.
Aggregate Cart accessing Cart from Cache Data/Shopping Cart Service and Product Service using SKU.
Access Analytics Service

## User Service:

Responsible for user management, including registration, login, and user profiles. Handles authentication and authorization.

Data Stored:

- User account details (username, email, password).
- User profiles (name).

## Shopping Cart Service

Allow users to add and remove products from their cart.

### Technical details:

Data Stored:

- Cart items (Sku, UserId, quantities)

## Product Service:

Manages product information, including details, categories, pricing, and availability. Provides functionalities for searching, filtering, and listing products. Handles inventory and stock management.

### Technical details:

CQRS

- Command: Use Entity Framework 
- Query : Use SQL with dapper

Data Stored:

- Product information (name, description, category, SKU, price, stock availability).

## Order Service:

Handles the creation, management, and fulfillment of orders and order status

### Technical details:

Data Stored:

- Order details (SKU, quantities, prices, status).

## RabbitMQ:

- It will send order event to Analytics Service asynchronously

## Analytics Service:

Analyze sells by category and see Order History

### Technical details:

Data Stored:

- Order History

