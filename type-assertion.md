# Type Assertion
Type assertion is used to extract the real (concrete) type from an interface{} value.

```bash
var x interface{} = "Hello"
value, ok := x.(string)
```
**x** can hold any type, but Go doesn't know what it is exactly.

So we use type assertion to say: “I believe this is a string — give it to me as a string.”

- If **x** contains a string: **value** will store that string and **ok** will store **true**

- If **x** is NOT a string (or nil): **value** will store **empty string -> ""** and **ok** will store **false**

#### Other examples: 
```bash
num, ok := x.(int)
```

```bash
value, ok := x.(bool)
```
