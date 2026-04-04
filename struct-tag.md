# Go Struct Tags – Comprehensive Guide

Struct tags in Go provide metadata about struct fields, allowing control over how fields are serialized, validated, or handled by external packages. This guide explains struct tags, their uses, and practical examples.

---

## 1. What is a Struct Tag?

A **struct tag** is a string literal attached to a struct field using backticks `` ` ``. It provides additional instructions for Go tools and libraries.

```go
type Response struct {
    Message string `json:"message"`
}
```

* `Message` → Go field name
* `string` → type of field
* `` `json:"message"` `` → struct tag for JSON encoding

---

## 2. Why Use Struct Tags?

Struct tags are used to:

1. Control **JSON/XML encoding**
2. Handle **database mapping**
3. Validate struct fields
4. Customize ORM behavior
5. Provide metadata for frameworks

---

## 3. JSON Struct Tag

### Basic Usage

```go
type Response struct {
    Message string `json:"message"`
}
```

**Effect:**

* Field `Message` becomes `message` in JSON
* Standard practice for APIs

### Output Example

```json
{
  "message": "Hello, World"
}
```

### Common Options

| Option      | Description                                                      |
| ----------- | ---------------------------------------------------------------- |
| `omitempty` | Skip the field if it is zero value (empty string, 0, false, nil) |
| `-`         | Ignore field when encoding/decoding                              |

**Example:**

```go
type User struct {
    Name  string `json:"name"`
    Email string `json:"email,omitempty"`
    Age   int    `json:"-"`
}
```

* `Email` will be omitted if empty
* `Age` will never appear in JSON

---

## 4. XML Struct Tag

```go
type Response struct {
    Message string `xml:"message"`
}
```

* Works similar to JSON but for XML serialization

---

## 5. Database / ORM Tags

Used to map struct fields to database columns:

```go
type User struct {
    ID    int    `db:"id"`
    Name  string `db:"name"`
    Email string `db:"email"`
}
```

* Libraries: `sqlx`, `gorm`
* Helps ORM map struct fields to table columns

**GORM Example:**

```go
type User struct {
    ID    uint   `gorm:"primaryKey"`
    Name  string `gorm:"size:100;not null"`
}
```

* `primaryKey`, `size`, `not null` → GORM-specific instructions

---

## 6. Validation Tags

Used with libraries like `go-playground/validator`:

```go
import "github.com/go-playground/validator/v10"

type User struct {
    Name  string `validate:"required,min=3,max=32"`
    Email string `validate:"required,email"`
}
```

* `required` → field must be non-empty
* `min=3,max=32` → string length constraints
* `email` → must be valid email

**Validation Example:**

```go
v := validator.New()
err := v.Struct(user)
```

---

## 7. Multiple Tags on One Field

You can combine multiple tags using **space separation**:

```go
type User struct {
    Name string `json:"name" db:"user_name" validate:"required,min=3"`
}
```

* JSON: `name`
* DB column: `user_name`
* Validation: required and min length 3

---

## 8. Omitting Fields in JSON/XML

```go
type Response struct {
    Password string `json:"-"`
}
```

* Field `Password` will never appear in JSON/XML output

---

## 9. Most Commonly Used Struct Tags

| Tag                | Usage                                                          |
| ------------------ | -------------------------------------------------------------- |
| `json:"fieldName"` | Map struct field to JSON key, with optional `omitempty` or `-` |
| `xml:"fieldName"`  | Map struct field to XML tag                                    |
| `db:"columnName"`  | Map struct field to database column (sqlx)                     |
| `gorm:"options"`   | GORM-specific database instructions                            |
| `validate:"rules"` | Field validation rules (go-playground/validator)               |
| `form:"field"`     | Bind form or query parameters                                  |
| `yaml:"fieldName"` | Map field for YAML serialization                               |

---

## 10. Summary / Best Practices

1. Use **JSON tags** for APIs
2. Use **db/gorm tags** for database mapping
3. Use **validate tags** for input validation
4. Combine multiple tags carefully: space-separated
5. Use `omitempty` to keep JSON responses clean
6. Use `-` to ignore sensitive fields

---

Struct tags make your Go code **clean, consistent, and compatible with frameworks**.
They are extremely useful for building **APIs, databases and validations**.

---

