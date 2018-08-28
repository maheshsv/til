# Builder Pattern

> Consider a builder when faced with many constructor parameters.

A manual implementation of builder pattern is like:

```java
public class Person {
    private final String name;
    private final String gender;
    private final int age;
    private final int salary;
    private final String phoneNumber;
    private final String address;

    public static class Builder {
        // Required parameters
        private final String name;
        private final String gender;

        // Optional parameters
        private int age = 0;
        private int salary = 0;
        private String phoneNumber = null;
        private String address = null;

        public Builder(String name, String gender) {
            this.name = name;
            this.gender = gender;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Builder salary(int salary) {
            this.salary = salary;
            return this;
        }

        public Builder phoneNumber(String phoneNumber) {
            this.phoneNumber = phoneNumber;
            return this;
        }

        public Builder address(String address) {
            this.address = address;
            return this;
        }

        public Person build() {
            return new Person(this);
        }
    }

    private Person(Builder builder) {
        name = builder.name;
        gender = builder.gender;
        age = builder.age;
        salary = builder.salary;
        phoneNumber = builder.phoneNumber;
        address = builder.address;
    }

    @Override
    public String toString() {
        return "Name: " + name + " Gender: " + gender + " Age: " + age +
                " Salary: " + salary + " Phone Number: " + phoneNumber +
                " Address: " + address;
    }
}

Person person = new Person.Builder("ZhangSan", "Male")
    .age(28)
    .address("SF")
    .phoneNumber("123-456-7890")
    .salary(1)
    .build();
```

