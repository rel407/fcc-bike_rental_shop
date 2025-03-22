# Bike Rental Shop

This is a simple bike rental shop system built using PostgreSQL and a Bash script to interact with the database. The system allows customers to rent and return bikes, tracking the availability of bikes and customer information.

## Features

- **Bike Rental**: Rent available bikes.
- **Bike Return**: Return rented bikes.
- **Database**: Uses PostgreSQL to store customer and rental data.
- **Bash Script Interface**: Interactive command-line interface to manage rentals.

## Database Structure

The system uses the following tables in the `bikes` database:

### 1. Bikes Table
| Column      | Type      | Description                          |
|-------------|-----------|--------------------------------------|
| bike_id     | SERIAL    | Primary key, unique ID for each bike |
| type        | TEXT      | Type of the bike (e.g., Mountain, Road, etc.) |
| size        | INTEGER   | Size of the bike (in inches)         |
| available   | BOOLEAN   | Availability status of the bike (true/false) |

### 2. Customers Table
| Column      | Type      | Description                          |
|-------------|-----------|--------------------------------------|
| customer_id | SERIAL    | Primary key, unique ID for each customer |
| name        | TEXT      | Name of the customer                 |
| phone       | TEXT      | Phone number of the customer (used for identification) |

### 3. Rentals Table
| Column         | Type      | Description                              |
|----------------|-----------|------------------------------------------|
| rental_id      | SERIAL    | Primary key, unique ID for each rental   |
| customer_id    | INTEGER   | Foreign key referencing `customers` table |
| bike_id        | INTEGER   | Foreign key referencing `bikes` table    |
| date_rented    | TIMESTAMP | The date when the bike was rented       |
| date_returned  | TIMESTAMP | The date when the bike was returned (nullable) |

## Setup Instructions

1. **Install PostgreSQL**:
   - Ensure you have PostgreSQL installed. You can download it from the [official website](https://www.postgresql.org/download/).

2. **Create the Database**:
   - Run the following command in the PostgreSQL shell to create the `bikes` database:
     ```sql
     CREATE DATABASE bikes;
     ```

3. **Create the Tables**:
   - After creating the database, use the following SQL to create the necessary tables:
     ```sql
     CREATE TABLE bikes (
         bike_id SERIAL PRIMARY KEY,
         type VARCHAR(15) NOT NULL,
         size INTEGER NOT NULL,
         available BOOLEAN NOT NULL
     );

     CREATE TABLE customers (
         customer_id SERIAL PRIMARY KEY,
         name VARCHAR(40) NOT NULL,
         phone VARCHAR(15) NOT NULL
     );

     CREATE TABLE rentals (
         rental_id SERIAL PRIMARY KEY,
         customer_id INTEGER REFERENCES customers(customer_id),
         bike_id INTEGER REFERENCES bikes(bike_id),
         date_rented TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
         date_returned TIMESTAMP
     );
     ```

4. **Clone the Repository**:
   - Clone this repository to your local machine:
     ```bash
     git clone https://github.com/yourusername/bike-rental-shop.git
     cd bike-rental-shop
     ```

5. **Edit the Script**:
   - Make sure the script (`bike_rental.sh`) is executable:
     ```bash
     chmod +x bike_rental.sh
     ```

6. **Run the Script**:
   - Execute the script to start the bike rental system:
     ```bash
     ./bike_rental.sh
     ```

## Usage

1. **Rent a Bike**:
   - From the main menu, select option `1` to rent a bike. The system will display available bikes and prompt for a selection. You will need to provide your phone number (and name if you are a new customer).

2. **Return a Bike**:
   - Select option `2` to return a bike. The system will display your current rentals and prompt you to return the rented bike.

3. **Exit**:
   - Select option `3` to exit the system.

## Example Workflow

- **Rent a Bike**:
  ```bash
   How may I help you?
   1. Rent a bike
   2. Return a bike
   3. Exit

   Which one would you like to rent?
  ```

  After entering your phone number and choosing a bike, the system will update the database with the rental information.

### Return a Bike:

```bash
How may I help you?
1. Rent a bike
2. Return a bike
3. Exit

Here are your rentals:
1) 26" Road Bike

Which one would you like to return?
```
## Contributing

Feel free to fork the project, make improvements, and submit pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
