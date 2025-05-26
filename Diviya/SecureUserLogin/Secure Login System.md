### Simple Java Login System with BCrypt: Secure User Signup, Login, and Logout
### **Introduction***
In the world of software development, **user authentication** is one of the most important features to get right. Whether you're building a web app, mobile app, or desktop application, you must allow users to **sign up**, **log in securely**, and **log out** when needed.

In this blog, we'll walk through a **Java console-based authentication system** that supports:

- Secure Signup
    
-  Secure Login using **BCrypt**
    
- Safe Logout
    
- Managing one active user at a time

```

package org.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import org.mindrot.jbcrypt.BCrypt;

public class AuthApp {

    private static Map<String, String> userDB = new HashMap<>();
    private static String currentUser = null;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("\n=== Menu ===");
            System.out.println("1. Signup");
            System.out.println("2. Login");
            System.out.println("3. Logout");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");

            int option = 0;
            try {
                option = Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Please enter a valid number.");
                continue;
            }

            switch (option) {
                case 1: signup(scanner); break;
                case 2: login(scanner); break;
                case 3: logout(scanner); break;
                case 4:
                    System.out.println("Exiting. Bye!");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid option.");
            }
        }
    }

    private static void signup(Scanner scanner) {
        if (currentUser != null) {
            System.out.println("You are already logged in as " + currentUser + ". Please logout to signup a new user.");
            return;
        }

        System.out.print("Enter email: ");
        String email = scanner.nextLine().trim();
        if (!isValidEmail(email)) {
            System.out.println("Invalid email format. Must contain '@'.");
            return;
        }
        if (userDB.containsKey(email)) {
            System.out.println("Email already registered.");
            return;
        }
        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        if (!isValidPassword(password)) {
            System.out.println("Password must contain at least 3 letters (one uppercase), 3 digits, and 2 special characters.");
            return;
        }

        String hashedPassword = BCrypt.hashpw(password, BCrypt.gensalt());
        userDB.put(email, hashedPassword);
        System.out.println("Signup successful. Please login to continue.");
    }

    private static void login(Scanner scanner) {
        if (currentUser != null) {
            System.out.println("Already logged in as " + currentUser);
            System.out.print("Do you want to logout and login as a different user? (yes/no): ");
            String choice = scanner.nextLine().trim().toLowerCase();

            if (choice.equals("yes")) {
                currentUser = null;
            } else {
                System.out.println("Login cancelled.");
                return;
            }
        }

        System.out.print("Enter email: ");
        String email = scanner.nextLine().trim();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        if (userDB.containsKey(email)) {
            String storedHash = userDB.get(email);
            if (BCrypt.checkpw(password, storedHash)) {
                currentUser = email;
                System.out.println("Login successful. Welcome " + currentUser + "!");
            } else {
                System.out.println("Invalid credentials.");
            }
        } else {
            System.out.println("User not found.");
        }
    }

    private static void logout(Scanner scanner) {
        if (currentUser == null) {
            System.out.println("No user is currently logged in.");
        } else {
            System.out.print("Enter your email to confirm logout: ");
            String email = scanner.nextLine().trim();
            if (email.equals(currentUser)) {
                System.out.println("User " + currentUser + " logged out successfully.");
                currentUser = null;
            } else {
                System.out.println("Email does not match the logged-in user. Logout aborted.");
            }
        }
    }

    private static boolean isValidEmail(String email) {
        return email.contains("@");
    }

    private static boolean isValidPassword(String password) {
        int letterCount = 0, digitCount = 0, specialCount = 0;
        boolean hasUpper = false, hasLower = false;

        for (char ch : password.toCharArray()) {
            if (Character.isUpperCase(ch)) hasUpper = true;
            else if (Character.isLowerCase(ch)) hasLower = true;
            if (Character.isLetter(ch)) letterCount++;
            else if (Character.isDigit(ch)) digitCount++;
            else if (!Character.isLetterOrDigit(ch)) specialCount++;
        }

        return password.length() >= 8 &&
               hasUpper && hasLower &&
               digitCount >= 2 && specialCount >= 2;
    }
}

```

```
pom.xml
<dependencies>  
    <dependency>        
    <groupId>org.mindrot</groupId>  
        <artifactId>jbcrypt</artifactId>  
        <version>0.4</version>  
    </dependency>
    </dependencies>
```
### How the System Works
### 1.Signup (Register a New User)

- Prompts the user to enter a valid **email**.
    
    - It must contain `@`
        
- Prompts for a **strong password**:
    
    - Minimum **3 letters**
        
    - Minimum **3 digits**
        
    - Minimum **2 special characters**

- **Password is hashed with `BCrypt.hashpw()` and stored
    
- Duplicate emails are not allowed
    

---

###  2. Login

- User enters email and password.
    
- First, it checks if a user is already logged in:
    
    - If yes, prompts to logout before logging in with another account
    
- Validates password using `BCrypt.checkpw(plain, hash)`
    
- If matched, logs in the user
        

---

### 3️.Logout

- Asks the logged-in user to confirm by entering their email
    
- Only logs out if email matches `currentUser`
---

### 4️.One User at a Time

- The system is designed to allow **only one active user session at a time**.
    
    
---

## Security: Why Use BCrypt?

### What is BCrypt?

BCrypt is a hashing algorithm specifically designed for securely storing passwords.

### ⚙ How it works:

- - Adds **salt** (random data) automatically
    
- Creates **unique hashes** for the same password
    
- Is **one-way** — you can't reverse it
    
- Protects against **brute force and rainbow table attacks**
####  Example:

`Password: MySecret123! BCrypt Hash: $2a$10$g1xTcQdJKVwvn08gMzZ5mO4tOS2YfBz5trfEP3J1ZToJ9YoYnpOCC`

---

## Library Used: jBCrypt

This project adds the **jBCrypt** library dependency.

- Simple and easy to integrate
    
- Lightweight library
    
-  Used widely in the Java community for password hashing
## Conclusion

This simple Java console application teaches the **core principles** of authentication:

- Input validation
    
- Password hashing with BCrypt
    
- Session control (single active user)





