
# Inventory Management API

## Project Description

A simple REST API that simulates an inventory system, this project was built as a way for me to solidify my skills in and explore best practice for Python/Flask REST APIs, Docker, and PostgreSQL. The project also includes a SwaggerUI interface that more thoroughly documents individual requests

<br/>

## Requirements and Usage Instructions

Requirements:
- Docker
- An Open Port (Default 5000)


You can install Docker by following the instructions in the link below:

https://docs.docker.com/compose/install/

<br/>

To start the application, run: 

    docker compose up --build



To alter configuration variables passed to the containers you can edit the variables within the included.env file. 
Optionally, you can provide an API Key to recieve weather information at inventory locations from the OpenWeatherAPI. If you do not have an API key you can generate one at https://home.openweathermap.org/users/sign_up.


<br />

### **Usage:**
By default the REST API should be available at http://localhost:5000, you can either call the endpoints directly or use the provided Swagger UI interface.

To use the Swagger UI interface you need to click an endpoint, press the "Try it out" button, insert query parameters, and then press the "Execute" button at the bottom. The response will appear below the "Execute" button.


<br />

## Database Relations and Starting Demo Data

On initialization, the schema is automatically created within the attached PostgreSQL database and some pieces of data are added for demonstration.

Except for item, all of these tables automatically create IDs using Postgres Identities.

[Full Diagram](./DB_Diagram.pdf)




### **Item Table:**
- The central table of this application, holds information about a specific physical item

| Serial Number | Inventory | Product | Condition | Damage Description |
| :---: | :---: | :---:| :---: | :---: |
| 2312412 	| 2 | 1 | Refurbished 	| Like New		|
| 2424444 	| 3 | 2 | Used 			| Weak magnet 	|
| 2142444 	| 1 | 3 | New 			| 				|



### **Product Table:**

- Holds information about a model of item in storage



| Product ID | Product Name | Product Brand | Product Description |
| :---: |:---:| :---:| :--- |
| 1 | Pixel 6                   | Google    | Dual rear camera system: 50 MP wide 12 MP ultra wide 	|
| 2 | Rambler® 30 oz Tumbler    | Yeti      | Iced coffee, sweet tea, lemonade, water, you name it, you’re set. Fits in most cupholders.|
| 3 | Anti-Dust Chalk Sticks    | Crayola   | Crayola Anti-Dust Chalk sticks keep dust to a minimum and are perfect for writing and drawing on blackboards. Available in white.|



### **Inventory Table:**

- Store information on a specific inventory
- Owner could be an organization or individual, potentially a foreign key to a separate table

By not tying a item directly to an address we can provide more granular information on what an item's purpose in storage is and group them together more logically.

| Inventory ID | Address ID | Inventory Name | Owner | Size |
| :---: |:---:| :---:| :---: | :--- |
| 1 | 1 | Backend Storage   | Alex Placeholder  | (Generated) |
| 2 | 2 | Frontend Storage  | Jerry Placeholder | (Generated) |
| 3 | 3 | Vancouver Storage | Linda Placeholder | (Generated) |




### **Address Table:**

- Stores addresses
- Could be used elsewhere in a bigger system (i.e. Employee or Company Address)

| Address ID | Address Country | Address State | Address City | Street Name | House Number | Apt Specifier | Postal Code |
| :---: |:---:| :---:| :---: | :--- | :---: | :---: |:---: |
| 1 | Canada | ON | Ottawa      | O'Connor St       | 151   |       | K2P 2L8 |
| 2 | Canada | ON | Ottawa      | Laurier Ave W     | 234   | #500  | K2P 2L8 |
| 2 | Canada | ON | Vancouver   | Langmuir Street   | 1055  |       | V7X 1L3 |


## Future Work

Some avenues for future development are:

- Automated unit test suites

- Much more inline documentation and help strings

- Request handling and scalable parallel workers through Redis

- A proper networking solution such as uWSGI or Waitress

- More data tables such as "User" or "Company" for inventory / item ownership

- CRUD operations implemented where applicable on all tables

- Proper web interfaces for different use-cases as opposed to just the Swagger UI platform.

- A more sophisticated deployment process using Ansible to instantiate instances remotely