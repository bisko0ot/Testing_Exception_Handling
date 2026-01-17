# Testing_Exception_Handling
step 1:

validation
package validation;

public class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
package validation;

public class InvalidDepartmentException extends Exception {
    public InvalidDepartmentException(String message) {
        super(message);
    }
}
step 2:
user.validation
module user.validation {
    exports validation;
}
package validation;

public class Validator {

    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18 || age > 60) {
            throw new InvalidAgeException("Age must be between 18 and 60");
        }
    }

    public static void validateDepartment(String dept) throws InvalidDepartmentException {
        if (!(dept.equalsIgnoreCase("ICT") ||
              dept.equalsIgnoreCase("CSE") ||
              dept.equalsIgnoreCase("EEE"))) {
            throw new InvalidDepartmentException("Invalid Department");
        }
    }
}
step 3;
test
package test;

import validation.Validator;
import validation.InvalidAgeException;
import validation.InvalidDepartmentException;

public class MainApp {
    public static void main(String[] args) {

        try {
            int age = 16;
            String dept = "BBA";

            Validator.validateAge(age);
            Validator.validateDepartment(dept);

            System.out.println("Validation Successful");

        } catch (InvalidAgeException e) {
            System.out.println("Age Error: " + e.getMessage());
        } catch (InvalidDepartmentException e) {
            System.out.println("Department Error: " + e.getMessage());
        } finally {
            System.out.println("Validation Process Completed");
        }
    }
}

