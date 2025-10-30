## Fullstack Developer Test Challenge
A Small microservice application that uses event driven communication, caching, and implementing clean, modular architecture
By : Wesly

### How to run
- Make sure you have configured .env file in each subfolder
- You can just copy the .env.example into .env for each subfolder
#### Running using `docker-compose`
```bash
docker compose up --build
```
To run locally, you can view instruction in each subfolder

### Layered Architecture

This project follows a **Layered Architecture** pattern, which separates the application into distinct layers to improve maintainability, scalability, and testability. Each layer has a clear responsibility:

- **Controller / Delivery Layer** → Handles incoming requests (e.g., HTTP, message queues) and sends responses back to the client. It acts as the entry point of the application and delegates business logic to the Service layer.

- **Service Layer** → Contains the core business logic and application rules. This layer coordinates data flow between the Controller and Repository layers, ensuring that business processes are executed correctly.

- **Repository Layer** → Responsible for data access and persistence. It interacts directly with the database or external data sources, performing operations such as querying, saving, updating, and deleting data.

- **DTO / Model Layer** → Defines the data structures used across layers.  
  - **DTO (Data Transfer Object)**: Used to transfer data between layers or to the client, ensuring encapsulation and validation of exposed data.  
  - **Model / Entity**: Represents the core domain objects that map directly to database tables or business concepts.

### Example request (using cURL)
##### `POST /products`
```shell
curl --request POST \
  --url http://localhost:5555/api/products \
  --header 'content-type: application/json' \
  --data '{
  "name": "Mouse",
  "price": 123000,
  "qty": 11
}'
```

##### `GET /products/:id` (Replace with productId you get from the POST /products)
```shell
curl --request GET \
  --url http://localhost:5555/api/products/9dc7a495-c565-4b20-ac7e-84640d5ff63b
```

#### POST /orders/ (Replace with productId you get from the POST /products)
```shell
curl --request POST \
  --url http://localhost:5555/api/orders \
  --header 'content-type: application/json' \
  --data '{
  "productId": "9dc7a495-c565-4b20-ac7e-84640d5ff63b"
}'
```

#### GET /orders/product/:productId (Replace with productId you get from the POST /products)
```shell
curl --request GET \
  --url http://localhost:5555/api/orders/product/9dc7a495-c565-4b20-ac7e-84640d5ff63b
```

