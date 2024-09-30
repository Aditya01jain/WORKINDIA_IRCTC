
---

# WORKINDIA_IRCTC

This project is a full-fledged **Railway Management System** built with **Node.js**, **Express.js**, and **MySQL**. It provides APIs for users to check train availability, book seats, and manage bookings. Additionally, it features an **admin interface** for train management.

By utilizing **transactions** and **row-level locking**, the system ensures that only one user can book available seats at any given time, effectively handling race conditions.

## Features

- **User Registration & Authentication**: Secure user management with JWT and password encryption.
- **Admin Train Management**: Admins can create and manage trains.
- **Train Availability**: Users can check train availability between any source and destination.
- **Seat Booking**: Users can book seats on available trains, with conflict prevention via row-level locking.
- **View Bookings**: Users can view their booking details.

## Technologies Used

- **Node.js**
- **Express.js**
- **MySQL**
- **JWT (JSON Web Tokens)**
- **bcrypt.js** (For password encryption)

## Installation Guide

1. **Clone the repository**:
   ```bash
   git clone https://github.com/aniket-24/WorkIndia-IRCTC.git
   ```
   
2. **Navigate to the project directory**:
   ```bash
   cd WorkInda-IRCTC
   ```

3. **Install the required dependencies**:
   ```bash
   npm install
   ```

4. **Configure environment variables**:
   Create a `.env` file and set the following variables:
   ```plaintext
   HOST=<your_mysql_host>
   USER=<your_mysql_user>
   PASSWORD=<your_mysql_password>
   NAME=<your_mysql_database_name>
   JWT_SECRET=<your_jwt_secret_key>
   ADMIN_KEY=<admin_key_for_protected_routes>
   ```

5. **Set up the MySQL database**:
   - Execute the SQL scripts located in the `database` directory to create the necessary tables.

6. **Run the application**:
   ```bash
   npm start
   ```

## API Documentation

### Authentication

- **Register a New User**  
  `POST /auth/register`  
  Body:
  ```json
  {
    "username": "example",
    "email": "example@mail.com",
    "password": "your_password"
  }
  ```

- **Login and Obtain JWT**  
  `POST /auth/login`  
  Body:
  ```json
  {
    "email": "example@mail.com",
    "password": "your_password"
  }
  ```

### Trains (Admin Only)

- **Create a New Train**  
  `POST /trains/create`  
  Body:
  ```json
  {
    "trainName": "Train A",
    "source": "City A",
    "destination": "City B",
    "departureTime": "10:00",
    "arrivalTime": "18:00",
    "seats": 120
  }
  ```

### Bookings

- **Check Train Availability**  
  `GET /trains/availability?source=<source>&destination=<destination>`  
  Example URL:
  ```
  http://localhost:3000/trains/availability?source=xyzCityA&destination=xyzCityB
  ```

- **Book Seats on a Train**  
  `POST /bookings/book`  
  Body:
  ```json
  {
    "trainId": 1,
    "seats": 2
  }
  ```

- **View Booking Details for a Specific Train**  
  `GET /bookings/details?trainId=<trainId>`  
  Example URL:
  ```
  /bookings/details?trainId=1
  ```

### Users

- **Get User Details**  
  `GET /users/me` (requires authentication)  

## Handling Race Conditions

- The system ensures race conditions are handled during booking using **transactions** and **row-level locking**. This guarantees that no two users can book the same seat simultaneously.

---

## Postman Collection

You can test the API easily using **Postman**.  
[Click here to access the Postman collection](https://www.postman.com/aditya0306/workindia/collection/lhpb5k1/workindia-irctc-aditya?action=share&creator=37893550).


---

### Developed by **Aditya Jain**.

---
