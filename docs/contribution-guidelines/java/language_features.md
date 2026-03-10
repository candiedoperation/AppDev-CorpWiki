---
title: Language Features
sidebar_position: 3
---
# Language Features

## General

### 1. `var` (Local Variable Type Inference)
`var` is acceptable for local variables when the type is obvious from the right-hand side.
Avoid it when the inferred type would not be immediately clear to a reader.
```java
var users = new ArrayList();         // ok — type is clear

var result = service.process(input); // avoid — type is unclear without checking the method
```

### 2. Enhanced For Loops
Prefer enhanced for loops over index-based loops unless the index is actually needed.
```java
for (String name : names) { // good
  System.out.println(name);
}

for (int i = 0; i < names.size(); i++) { // only if index is needed
  System.out.println(names.get(i));
}
```

### 3. String Templating
Prefer `String.format()` or `formatted()` over string concatenation for readability.
```java
String msg = "Hello, %s!".formatted(name); // good
String msg = "Hello, " + name + "!";       // avoid
```

### 4. Ternary Operator
Ternary is acceptable for simple, readable assignments. Do not nest ternaries.
```java
String label = isActive ? "Active" : "Inactive";                           // good

String label = isActive ? (isPremium ? "Premium" : "Active") : "Inactive"; // bad — nested
```

### 5. Switch Expressions
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

### 6. Optional
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

### 7. Avoid Magic Numbers
Always extract magic numbers into named constants.
```java
private static final int MAX_RETRIES = 3;

if (retryCount > MAX_RETRIES) { ... } // good

if (retryCount > 3) { ... }           // bad
```