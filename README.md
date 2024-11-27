# Java-with-SQL-

java-mysql-project/
├── src/
│   ├── DBConnection.java
│   └── Main.java
├── lib/
│   └── mysql-connector-java-8.0.29.jar  (if not using Maven)
├── pom.xml  (if using Maven)
├── README.md
└── .gitignore


Set Up MySQL Database
Install MySQL: If you haven't already, install MySQL on your system. During installation, remember the root password and MySQL port.
Create a Database: Open MySQL Workbench and log in to MySQL. Run the following SQL query to create a new database:
CREATE DATABASE RegistrationDetails;
Create a Table: Now, create a table inside RegistrationDetails database. You can use the following SQL command to create a users table:
use RegistrationDetails;
CREATE TABLE RegistrationDetails_table (
    id int,
    Name VARCHAR(100),
    Email VARCHAR(100),
    DateOfBirth DATE,
    PhoneNumber VARCHAR(15)
);
Insert Sample Data: Insert some sample data into the users table:
INSERT INTO users (name, email, age) VALUES ('John Doe', 'john@example.com', 30);
INSERT INTO users (name, email, age) VALUES ('Jane Smith', 'jane@example.com', 25);

Configure MySQL Connection in Java
In your Java project, configure the connection to the MySQL database.

JDBC Driver: Ensure the MySQL JDBC driver (mysql-connector-java) is available. If you're using Maven, add the following dependency to your pom.xml
If you're not using Maven, download the JDBC driver from MySQL official site and add it to your project's lib directory.

Database Connection Code: Inside your Java code, you will need to establish a connection to the MySQL database using the JDBC URL, username, and password. Below is an example DBConnection.java:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DBConnection {
    public static Connection getConnection() {
        String url = "jdbc:mysql://localhost:3306/java_mysql_db";
        String username = "root";
        String password = "your_mysql_password"; // Replace with your MySQL password
        Connection conn = null;

        try {
            conn = DriverManager.getConnection(url, username, password);
            System.out.println("Connection successful!");
        } catch (SQLException e) {
            e.printStackTrace();
            System.out.println("Connection failed!");
        }

        return conn;
    }
}
Test the CRUD Operations: The application will connect to the MySQL database and perform CRUD operations. Below is a simple example of performing a SELECT operation to fetch users from the users table.
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class UserDAO {
    public static void getAllUsers() {
        String query = "SELECT * FROM users";
        try (Connection conn = DBConnection.getConnection();
             PreparedStatement stmt = conn.prepareStatement(query);
             ResultSet rs = stmt.executeQuery()) {

            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("id"));
                System.out.println("Name: " + rs.getString("name"));
                System.out.println("Email: " + rs.getString("email"));
                System.out.println("Age: " + rs.getInt("age"));
                System.out.println("------------");
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
Run the Application: Run your Java application to see the data being fetched from the MySQL database.

