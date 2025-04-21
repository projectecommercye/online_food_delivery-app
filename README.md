A Java-based web application that allows users to explore restaurants, order food online, and manage their orders.



✨ Features
      ✔️ User Authentication: Sign-up, sign-in, and sign-out functionality.
      ✔️ Home Page: Displays a list of different restaurants.
      ✔️ Menu Page: View food items of a selected restaurant.
      ✔️ Add to Cart: Users can add items to their cart.
      ✔️ Checkout & Order Confirmation: Proceed to checkout and confirm the order.
      ✔️ Order History: Users can view past orders with all details.
      ✔️ Profile Management: Users can edit their profile information.

🔧 Technologies Used
Frontend: JSP, CSS
Backend: Java (Servlets, JDBC)
Database: MySQL
Server: Apache Tomcat
📝 Project Structure
FoodDeliveryApplication/
├── src/main/java/
│   ├── com.tap.model/           # Model classes (User, Order, Restaurant, etc.)
│   ├── com.tap.dao/             # DAO interfaces
│   ├── com.tap.daoImplementation/  # DAO implementation classes
│   ├── com.tap.utility/         # Database connection utility
│   ├── com.tap.servlets/        # Servlets handling requests
│
├── webapp/
│   ├── assets/                  # Images, animation video, sound files
│   ├── jspFiles/                # All JSP pages
│   ├── styles/                  # CSS files
│   ├── WEB-INF/
│   │   ├── lib/                 # MySQL Connector JAR
│   │   ├── web.xml              # Deployment descriptor
⚡ How to Run the Project
Follow these steps to set up and run the project on your system:

🛠 Prerequisites
Install Java JDK (11 or higher)
Install Apache Tomcat (9 or higher)
Install MySQL Server
Install Eclipse IDE (or any other IDE that supports Java Web Development)
Add MySQL Connector JAR to the lib/ folder
📝 Step 1: Clone the Repository
git clone https://github.com/mamatha833/FoodDeliveryApplication.git
🔧 Step 2: Set Up the MySQL Database
Open MySQL Workbench or any MySQL client.
Create a new database:
CREATE DATABASE FoodDeliveryDB;
Switch to the new database:
USE FoodDeliveryDB;
Create the required tables:
CREATE TABLE user (
    userId INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    username VARCHAR(100),
    password VARCHAR(255),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15),
    address VARCHAR(200),
    role 
    enum('admin','customer','restaurantOwner','deliveryPartner'),
    createdDate  TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    lastLoginDate  TIMESTAMP
);

CREATE TABLE restaurant (
    restaurantId INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    address VARCHAR(255),
    phone varchar(10),
    rating  float,
    cusineType varchar(45),
    isActive tinyint,
    eta varchar(45),
    adminUserId int,
    imagePath varchar(200),
    FOREIGN KEY (adminUserId) REFERENCES user(userId)

);

CREATE TABLE menu (
    menuId INT AUTO_INCREMENT PRIMARY KEY,
    restaurantId INT,
    itemName VARCHAR(100),
    description varchar(200),
    price float,
    ratings float,
    isAvailable tinyint,
    imagePath varchar(200),
    FOREIGN KEY (restaurantId) REFERENCES restaurant(restaurantId)
);

CREATE TABLE `order` (
    orderId INT AUTO_INCREMENT PRIMARY KEY,
    userId INT,
    restaurantId int,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    totalAmount float,
    status enum('placed','shipped','delivered','cancelled') 
    DEFAULT "placed",
    address varchar(500),
    phone varchar(20),
    paymentMode  enum('upi','cod','card') DEFAULT "cod",
    FOREIGN KEY (userId) REFERENCES user(userId),
    FOREIGN KEY (restaurantId) REFERENCES restaurant(restaurantId)
);


 CREATE TABLE `orderitem` (
    orderItemId INT AUTO_INCREMENT PRIMARY KEY,
    orderId INT,
    menuId int,
    quantity int,
    totalPrice float,
    FOREIGN KEY (orderId) REFERENCES `order`(orderId),
    FOREIGN KEY (menuId) REFERENCES menu(menuId)
);
🛠 Step 3: Import the Project in Eclipse
Open Eclipse IDE.
Click File → Import → Existing Projects into Workspace.
Select the FoodDeliveryApplication folder.
Click Finish.
🌐 Step 4: Configure Tomcat Server
In Eclipse, go to Window → Show View → Servers.
Right-click and Add New Server → Select Apache Tomcat.
Set the Tomcat installation directory.
Click Finish.
🚀 Step 5: Run the Application
Right-click the project → Run As → Run on Server.
Choose Apache Tomcat and click Finish.
Open your browser and visit:
http://localhost:8080/FoodDeliveryApplication/
💡 Additional Notes
Make sure MySQL is running before launching the project.
Update DatabaseConnection.java in com.tap.utility with your MySQL credentials:
String url = "jdbc:mysql://localhost:3306/FoodDeliveryDB";
String user = "root";
String password = "your_password";
If you face any errors, check the Tomcat logs in Eclipse.
💼 Contributing
Pull requests are welcome! If you find any issues, feel free to open an issue.

💌 Contact
For any queries, reach out at yallamamatha5@gmail.com.
