# HAKIM-Angel-Peter_25778
## Assignment: Understanding and Handling OOP/Java Exceptions:
### Objective 
The goal of this assignment is to enhance your understanding of exception handling in Java 
through practical examples. You will write small programs to simulate specific exceptions, 
demonstrate how they occur, and provide appropriate handling mechanisms. 
Each program should: 
- Simulate the exception in a meaningful scenario. 
- Include exception handling using try-catch blocks (and finally if needed). 
- Use comments to explain the code where necessary.

## Checked Exceptions:
### 1. IOException: 
Simulate a scenario like reading a file from disk that might cause an input/output error. 
o Example: Attempt to read a non-existent file.

```
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class IOExceptionExample {
    public static void main(String[] args) {
        String filePath = "non_existent_file.txt";
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("An IOException occurred: " + e.getMessage());
        }
    }
}

```
#### Explanation:

* **Import Statements**: The classes required for file reading and exception handling are imported.

* **File Path**: The path of the file that we will be reading is specified. In this case, it's a non-existent file named non_existent_file.txt.

* **Try Block**: We attempt to open and read the file using BufferedReader and FileReader. The try-with-resources statement ensures that the BufferedReader is closed automatically.

* **Inside the try block**, we read every line from the file and print it to the console.

* **the catch block** handles it by printing an error message to the console.

This program will intentionally throw an IOException because the file non_existent_file.txt does not exist. The thrown exception will be caught and handled in an elegant way with a clear error message.



### 2. FileNotFoundException: 
A specific type of IOException that occurs when a file is not found. 
o Example: Try to open a file that doesn’t exist. 

```
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class FileNotFoundExceptionExample {
    public static void main(String[] args) {
        // The file path to read from
        String filePath = "non_existent_file.txt";

        // Try to open the file
        try {
            File file = new File(filePath);
            Scanner scanner = new Scanner(file);
            // Read and print each line of the file
            while (scanner.hasNextLine()) {
                System.out.println(scanner.nextLine());
            }
            scanner.close();
        } catch (FileNotFoundException e) {
            // Handle the FileNotFoundException
            System.err.println("FileNotFoundException occurred: " + e.getMessage());
        }
    }
}

```
### Explanation:

* **Import Statements**: The classes needed for file handling and exception handling are imported here.

* **File Path**: The path of the file we want to read is provided. In this case, it's a non-existing file called non_existent_file.txt.

* **Try Block**: We try to open the file using the File and Scanner classes.

* **Read and Print**: We read each line in the file and print it into the console inside the try block.

* **Catch Block**: This catches a FileNotFoundException, which may occur if the file does not exist, and prints an error message to the console.

This program will intentionally throw a FileNotFoundException because the file non_existent_file.txt does not exist. The thrown exception is caught and handled with a meaningful error message.

### 3. EOFException: 
Simulate reaching the end of a file unexpectedly. 
o Example: Attempt to read beyond the file's content.

```
import java.io.DataInputStream;
import java.io.EOFException;
import java.io.FileInputStream;
import java.io.IOException;

public class EOFExceptionExample {
    public static void main(String[] args) {
        // The file path to read from
        String filePath = "example_file.dat";

        // Try to read the file
        try (DataInputStream dis = new DataInputStream(new FileInputStream(filePath))) {
            while (true) {
                // Attempt to read an integer from the file
                int data = dis.readInt();
                System.out.println("Read data: " + data);
            }
        } catch (EOFException e) {
            // Handle the EOFException
            System.err.println("Reached the end of the file unexpectedly: " + e.getMessage());
        } catch (IOException e) {
            // Handle other IOExceptions
            System.err.println("An IOException occurred: " + e.getMessage());
        }
    }
}

```
### Explanation:

* **Import Statements**: Here, we import the classes required for file manipulation and exception handling.

* **File Path**: Here, we set the path of the file that we want to read. Here, it is a file named example_file.dat.

* **Try Block**: Under this block, we are trying to open and read the file using DataInputStream and FileInputStream.

* **Read Data**: We will be reading a set of integers from the file inside this try block and print it on the console continuously. This while(true) guarantees we read until an EOFException is thrown.

* **Catch Block for EOFException**: In case of an EOFException being thrown-which will happen, as we reach the end of the file-the catch block catches it and prints some error message on the console.

* **IOException Catch Block**: This block catches any other IOException and handles it by printing an error message to the console.

This program will deliberately throw an EOFException when it reaches the end of the file example_file.dat. The thrown exception is caught and handled gracefully, with a clear error message appearing.

### 4. SQLException: 
Simulate a database error. 
o Example: Attempt to connect to a non-existent database or execute invalid SQL.

```

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class SQLExceptionExample {
    public static void main(String[] args) {
        // Database URL, username, and password
        String url = "jdbc:mysql://localhost:3306/non_existent_db";
        String user = "root";
        String password = "password";

        Connection conn = null;
        Statement stmt = null;

        try {
            // Attempt to establish a connection to the database
            conn = DriverManager.getConnection(url, user, password);
            // Create a statement object to execute SQL queries
            stmt = conn.createStatement();
            // Attempt to execute an invalid SQL query
            String sql = "SELECT * FROM non_existent_table";
            stmt.executeQuery(sql);
        } catch (SQLException e) {
            // Handle the SQLException
            System.err.println("SQLException occurred: " + e.getMessage());
        } finally {
            // Close the resources
            try {
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                System.err.println("Error closing resources: " + e.getMessage());
            }
        }
    }
}

```
### Explanation:

* **Import Statements**: These are the import statements for the classes required, which include database connection and exception handling.

* **Database URL, Username, and Password**: We mention the URL of the database to which we want to connect, along with the username and password. Here, it is for a non-existent database named non_existent_db.

* **Connection and Statement Objects**: Connection and Statement objects are declared to manage the database connection and to execute SQL queries.

* **Try Block**: We try to connect to the database using DriverManager.getConnection(). Then we create a Statement object and try to execute an invalid SQL query.

* **Catch Block for SQLException**: If a SQLException occurs-for example, because the database or table does not exist-the catch block catches it by printing an error message on the console.

* finally Block: We close the Statement and Connection objects regardless of whether an exception occurs, in order to release database resources.

This program will deliberately cause a SQLException to be thrown when it attempts to connect to a nonexistent database and then attempts to execute an invalid SQL query. The exception is caught and handled so that an informative error message is displayed.

### 5. ClassNotFoundException: 
Demonstrate a scenario where a class file is missing at runtime. 

```
public class ClassNotFoundExceptionExample {
    public static void main(String[] args) {
        try {
            // Attempt to load a non-existent class
            Class.forName("com.example.NonExistentClass");
        } catch (ClassNotFoundException e) {
            // Handle the ClassNotFoundException
            System.err.println("ClassNotFoundException occurred: " + e.getMessage());
        }
    }
}

```

### Explanation:

* **Try Block**: We try to load a class called com.example.NonExistentClass using Class.forName(). The class does not exist; hence, it will fire a ClassNotFoundException.

* **Catch for the ClassNotFoundException**: In case there is a ClassNotFoundException-for instance, because the class does not exist-the catch block catches it and prints an error message to the console.

This program will deliberately cause a ClassNotFoundException to be thrown when it attempts to load the non-existent class com.example.NonExistentClass. The exception is caught and handled nicely, providing a meaningful error message.

## Unchecked Exceptions :

### 1. ArithmeticException: 

Simulate an arithmetic operation that fails. 

```
public class ArithmeticExceptionExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.err.println("ArithmeticException occurred: " + e.getMessage());
        }
    }
}
```
### Explanation:

* **Try Block**: We are attempting to perform an arithmetic operation of division of 10 by 0. This will throw an ArithmeticException.

* **Catch Block for ArithmeticException**: In case an ArithmeticException has been thrown-as, for instance, division by zero-the catch block catches and handles the exception by printing the error message to the console.

This program will deliberately throw an ArithmeticException when it tries to divide by zero. The thrown exception is then caught and handled elegantly, giving a good error message.


### 2. NullPointerException: 

Access a null reference.

```
public class NullPointerExceptionExample {
    public static void main(String[] args) {
        String str = null;

        try {
            // Attempt to call a method on a null reference
            int length = str.length();
            System.out.println("Length: " + length);
        } catch (NullPointerException e) {
            // Handle the NullPointerException
            System.err.println("NullPointerException occurred: " + e.getMessage());
        }
    }
}
```

### Explanation:
1. **Try Block**: We try to invoke the `length()` method on a null reference, `str`. This will throw a `NullPointerException`.
2. **Catch Block for NullPointerException**: If a `NullPointerException` occurs-for example, because we are trying to invoke a method on a null reference-the catch block catches it by printing an error message on the console.

This program will deliberately throw a `NullPointerException` when it tries to invoke a method on a null reference. The exception is caught and handled nicely, providing a clear error message.

### 3. ArrayIndexOutOfBoundsException: 
Access an invalid array index. 

```
public class ArrayIndexOutOfBoundsExceptionExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};

        try {
            // Attempt to access an invalid array index
            int invalidIndexValue = numbers[10];
            System.out.println("Value at index 10: " + invalidIndexValue);
        } catch (ArrayIndexOutOfBoundsException e) {
            // Handle the ArrayIndexOutOfBoundsException
            System.err.println("ArrayIndexOutOfBoundsException occurred: " + e.getMessage());
        }
    }
}


```
### Explanation:

* **Try Block**: We try to access the element at index 10 in an array of size 5. This will trigger an ArrayIndexOutOfBoundsException.

* **Catch Block for ArrayIndexOutOfBoundsException**: If there is an ArrayIndexOutOfBoundsException, say for trying to access an index out of bounds, it gets handled in the catch block by printing an error message to the console.

The program will intentionally throw an ArrayIndexOutOfBoundsException when it accesses an invalid index of an array. An appropriate error message is given out when the exception is handled.


### 4. ClassCastException: 
Demonstrate an invalid type cast. 

```
public class ClassCastExceptionExample {
    public static void main(String[] args) {
        Object obj = "This is a string";

        try {
            // Attempt to cast the object to an incompatible type (Integer)
            Integer num = (Integer) obj;
            System.out.println("Number: " + num);
        } catch (ClassCastException e) {
            // Handle the ClassCastException
            System.err.println("ClassCastException occurred: " + e.getMessage());
        }
    }
}
```
### Explanation:

* **Try Block**: We are trying to cast an object of String type into Integer. It will obviously cause a ClassCastException because such types cannot be cast. 

* **Catch Block for ClassCastException**: If the ClassCastException is thrown- for instance, we are trying to cast an object on an object of an incompatible type-the catch block handles it by printing an error message in the console.

This program will intentionally cause a ClassCastException when trying to cast an object into an incompatible type. The subsequent exception is caught and handled to provide a clean error message.

### 5. IllegalArgumentException: 
Pass an invalid argument to a method. 

```
public class IllegalArgumentExceptionExample {
    public static void main(String[] args) {
        try {
            // Attempt to set a negative age
            setAge(-5);
        } catch (IllegalArgumentException e) {
            // Handle the IllegalArgumentException
            System.err.println("IllegalArgumentException occurred: " + e.getMessage());
        }
    }

    // Method to set age with validation
    public static void setAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age must be non-negative.");
        }
        System.out.println("Age is set to: " + age);
    }
}

```
### Explanation:

* **Try Block**: We try calling the setAge method with a negative value (-5). An IllegalArgumentException will be thrown here.

* **Catch for IllegalArgumentException**: In case an IllegalArgumentException is thrown-say, since we are passing an invalid argument-the catch block catches that and prints the error to the console.

* **setAge() method** : This method verifies the age parameter. It throws an IllegalArgumentException if age is negative.

This program will deliberately throw an IllegalArgumentException when it attempts to set a negative age. The thrown exception is caught and handled with a meaningful error message.


### 6. NumberFormatException: 

Attempt to convert a string to a number when the format is invalid.

```
public class NumberFormatExceptionExample {
    public static void main(String[] args) {
        String invalidNumber = "123abc";

        try {
            // Attempt to convert the invalid string to an integer
            int number = Integer.parseInt(invalidNumber);
            System.out.println("Number: " + number);
        } catch (NumberFormatException e) {
            // Handle the NumberFormatException
            System.err.println("NumberFormatException occurred: " + e.getMessage());
        }
    }
}
```
### Explanation:

* **Try Block**: We attempt to convert the string invalidNumber ("123abc") to an integer using Integer.parseInt(). This will throw a NumberFormatException because there are non-numeric characters in the string.

* **Catch Block for NumberFormatException**: In case of a NumberFormatException-a situation that arises when the format of the string is incorrect, for instance-the catch block catches it and prints out an error message on the console.

The code will deliberately raise a NumberFormatException when it attempts to turn a string that cannot be processed into a number. A more elegant handling of the exception provides a proper error message for the user.










































