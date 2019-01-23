# Java Enums

Java Enums learning notes from [here](http://tutorials.jenkov.com/java/enums.html).

```java
// A simple example
public enum Level {
    HIGH,
    MEDIUM,
    LOW
}

// Enum Iteration: Enum values()
for(Level level : Level.values()) {
    System.out.println(level);
}

// Enum valueOf()
Level level = Level.valueOf("HIGH");

// Enum Fields and Methods
public enum Level {
    HIGH(3),
    MEDIUM(2),
    LOW(1);

    private final int levelCode;

    private Level(int levelCode) {
        this.levelCode = levelCode;
    }

    // getter for levelCode
    public int getLevelCode() {
        return this.levelCode;
    }
}

// Enum abstract methods
public enum Level {
    HIGH {
        @Override
        public String asLowerCase() {
            return HIGH.toString().toLowerCase();
        }
    },
    MEDIUM {
        @Override
        public String asLowerCase() {
            return MEDIUM.toString().toLowerCase();
        }
    },
    LOW {
        @Override
        public String asLowerCase() {
            return LOW.toString().toLowerCase();
        }
    };

    public abstract String asLowerCase();
}

// Enum implement interface, sounds easy, right?

// EnumSet
EnumSet<Level> enumSet = EnumSet.of(Level.HIGH, Level.LOW);

// EnumMap
EnumMap<Level, String> enumMap = new EnumMap<>(Level.class);
enumMap.put(Level.HIGH  , "high level");
enumMap.put(Level.MEDIUM, "medium level");
enumMap.put(Level.LOW   , "low level");

```

And there is also a good read on [implementing simple state machine with Java Enums](https://www.baeldung.com/java-enum-simple-state-machine).
