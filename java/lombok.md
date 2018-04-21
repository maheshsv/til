# Lombok

The home page of project Lombok can be found [here](https://projectlombok.org/).

Lombok use annotation to automatically generate boilerplate code such as getter/setter, equals and so on.

### @Data

> **@Data** generates *all* the boilerplate that is normally associated with simple POJOs (Plain Old Java Objects) and beans.

### @Getter/@Setter

Example code from Lombok project.

With Lombok

```java
import lombok.AccessLevel;
import lombok.Getter;
import lombok.Setter;

public class GetterSetterExample {
    @Getter @Setter private int age = 10;
    
    @Setter(AccessLevel.PROTECTED) private String name;
    
    @Override public String toString() {
        return String.format("%s (age: %d)", name, age);
    }
}
```

Vanilla Java

```java
public class GetterSetterExample {
  private int age = 10;

  private String name;
  
  @Override public String toString() {
    return String.format("%s (age: %d)", name, age);
  }
  
  public int getAge() {
    return age;
  }
  
  public void setAge(int age) {
    this.age = age;
  }
  
  protected void setName(String name) {
    this.name = name;
  }
}
```

The complete list of features Lombok supports are [here](https://projectlombok.org/features/all).

