---
title: Language Features
sidebar_position: 4
---
# Language Features

## General

### 1. Generics
Always specify generic type parameters explicitly. Never use raw types.
```java
List names = new ArrayList<>(); // good

List names = new ArrayList();   // bad — raw type
```

### 2. `var` (Local Variable Type Inference)
`var` is acceptable for local variables when the type is obvious from the right-hand side.
Avoid it when the inferred type would not be immediately clear to a reader.
```java
var users = new ArrayList();         // ok — type is clear

var result = service.process(input); // avoid — type is unclear without checking the method
```

### 3. Enhanced For Loops
Prefer enhanced for loops over index-based loops unless the index is actually needed.
```java
for (String name : names) { // good
  System.out.println(name);
}

for (int i = 0; i < names.size(); i++) { // only if index is needed
  System.out.println(names.get(i));
}
```

### 4. String Templating
Prefer `String.format()` or `formatted()` over string concatenation for readability.
```java
String msg = "Hello, %s!".formatted(name); // good
String msg = "Hello, " + name + "!";       // avoid
```

### 5. Ternary Operator
Ternary is acceptable for simple, readable assignments. Do not nest ternaries.
```java
String label = isActive ? "Active" : "Inactive";                           // good

String label = isActive ? (isPremium ? "Premium" : "Active") : "Inactive"; // bad — nested
```

### 6. Switch Expressions
Prefer switch expressions (arrow syntax) over traditional switch statements for assignments.
```java
// good
String label = switch (status) {
  case ACTIVE -> "Active";
  case PENDING -> "Pending";
  default -> "Unknown";
};

// avoid
String label;
switch (status) {
  case ACTIVE:
    label = "Active";
    break;
  ...
}
```

### 7. Optional
Prefer `Optional<T>` for return values that may be absent instead of returning `null`.
```java
public Optional findUser(String id) { // good
  ...
}

public User findUser(String id) { // avoid — may return null silently
  ...
}
```

Do not use `Optional` as a method parameter or field — only as a return type.
```java
public void process(Optional name) { ... } // bad — use overloads or @Nullable instead
```

### 8. Avoid Magic Numbers
Always extract magic numbers into named constants.
```java
private static final int MAX_RETRIES = 3;

if (retryCount > MAX_RETRIES) { ... } // good

if (retryCount > 3) { ... }           // bad
```

## Typing

### 1. Interfaces Over Concrete Types
Declare variables and parameters using the interface type, not the concrete implementation.
```java
List names = new ArrayList<>();      // good — declared as List
ArrayList names = new ArrayList<>(); // avoid — unnecessarily concrete
```

### 2. `@Nullable` and `@NonNull`
Annotate parameters and return types with `@Nullable` when `null` is a valid value.  
Unannotated types are assumed non-null.
```java
public @Nullable String findName(String id) { ... } // explicitly nullable

public String getName() { ... }                     // assumed non-null
```

### 3. Enums Over Constants
Prefer enums over `static final` string/int constants for sets of related values.
```java
// good
enum Status { PENDING, ACTIVE, CLOSED }

// avoid
static final String STATUS_PENDING = "pending";
static final String STATUS_ACTIVE = "active";
```

### 4. Records (Java 16+)
Use `record` for simple immutable data carriers instead of writing boilerplate POJOs.
```java
// good
public record Point(int x, int y) {}

// avoid — unnecessary boilerplate for pure data
public class Point {
  private final int x;
  private final int y;
  public Point(int x, int y) { this.x = x; this.y = y; }
  public int x() { return x; }
  public int y() { return y; }
}
```