
# 🚀 Python Concepts And FastAPI CRUD Operations


# 1. Python Concepts

## 1.1 Generators

- **Generators**: Generators are a special type of iterable in Python, designed to generate values one at a time and only when requested—making them exceptionally efficient for handling large data and infinite sequences. Unlike lists,
which store all items in memory, generators yield values on demand and thus save memory and processing time

- **Key Features**
  - Processing large files: Read data line by line instead of loading the entire file.
  - Lazy computations: Evaluate data only when needed, ideal for streams or real-time data.
  - Infinite sequences: Generate endless data.

### Example
```bash
def count_up_to(n):
    count = 1
    while count <= n:
        yield count
        count += 1
 
for num in count_up_to(5):
    print(num)
```


---

## 1.2 Decorators

- **Decorators**: A decorator in Python is a function that allows you to modify or extend the behavior of other functions or methods without changing their actual code. Decorators "wrap" another function and let you execute code before and after the wrapped function runs, making them a powerful tool for code reuse and separation of concerns

- **Key Features**
  - Logging
  - Authentication and access control
  - Timing and profiling functions.

### Example
```bash
def my_decorator(func):
    def wrapper():
        print("Before the function call")
        func()
        print("After the function call")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()

```
### Handling Arguments
```bash
def decorator_name(func):
    def wrapper(*args, **kwargs):
        # Add functionality before the original function call
        result = func(*args, **kwargs)
        # Add functionality after the original function call
        return result
    return wrapper

@decorator_name
def function_to_decorate():
    # Original function code
    pass
```

### Class-Based Decorators
```bash
class CallCounter:
    def __init__(self, func):
        self.func = func
        self.count = 0
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Called {self.count} times")
        return self.func(*args, **kwargs)

@CallCounter
def greet():
    print("Hello!")

```

## 1.3 Lamda Function
- **Lamda**: Python Lambda Functions are anonymous functions means that the function is without a name. As we already know the def keyword is used to define a normal function in Python. Similarly, the lambda keyword is used to define an anonymous function
  - *arguments* : one or more parameters, just like a regular function.
  - *expression* : a single expression whose result will be returned automatically.

### Syntax
``` bash
lambda arguments: expression
```
- **Key Features**
  - Used when simple functionality is required
  - Lambda functions are commonly used as arguments to other functions


### Example
```bash
add = lambda x, y: x + y
print(add(3, 4))  # Output: 7

```
### Lamda function as an Argument
``` bash
numbers = [1,2,3]
map(lambda x: x**2, numbers)

```
## 1.4 Dictionary
- **Dictionary**: A dictionary in Python is a built-in data type used to store data in key-value pairs. Keys must be unique and immutable (such as strings, integers, or tuples), while values can be of any type and may be duplicated. Dictionaries are mutable, so you can add, modify, or remove items after creation.
### Syntax
```bash
dict = {
          "key1":"value1",
          "key2":"value2",
          "key3":"value3"
       }
```
- **Key Features**
  - Highly efficient for retrieval using keys
  - Commonly used for representing structured data (like JSON), fast lookups, and flexible data storage.
  - Methods include .get(), .update(), .keys(), .values(), .items(), etc.

### Example
```bash
person = {
    "name": "Vamsi",
    "age": 25,
    "city": "Hyderabad"
}
```
### Accessing and Modifying Values
- To access a value
  - **Syntax**

  ```bash
   dictionary_name["key"]
  ````
  - **Example**

  ```bash
    person["name"]
  ```
- To remove a key-value pair
  - **Example**
  ```bash
    del person["name"]
  ```
- To add or update a value:
  - **Example**
  ```bash
   person["state"] = "telangana"
  ```
## 1.5 List
- **List**: A list in Python is a built-in, mutable data structure designed to store an ordered collection of items, which can be of any type (numbers, strings, objects, even other lists). Lists are extremely versatile and are among the most commonly used data types in Python for managing collections of data
### Syntax
  - **Creating list**
  ```bash
  list_name = ["value1","value2","value3"]
  ```
  - **Creating list with list() constructor**
  ```bash
  empty = list()
  from_tuple = list((1, 2, 3))
  ```
- **Key Features**
  - Ordered: Elements retain the order in which they are added; order is preserved when you iterate over the list
  - Mutable: You can modify, add, or remove elements after creation.
  - Methods include .get(), .update(), .keys(), .values(), .items(), etc.

### Example
```bash
fruits = ["apple", "cherry", "orange", "banana"]
```
### Accessing and Modifying Values
- To access a value
  - **Syntax**

  ```bash
   list_name[index]
  ````
  - **Example**

  ```bash
    fruits[0]
  ```
- To remove a key-value pair
  - **Example**
  ```bash
    fruits.remove("banana")  # Removes first Occurence of banana
    fruits.pop()   # Removes last item
    fruits.clear() # Removes all items
  ```
- To add a value:
  - **Example**
  ```bash
   fruits.append("orange")   # Adds to end
   fruits.insert(1, "kiwi")  # Inserts at index 1
   fruits.extend(["pear", "melon"])  # Appends multiple items
  ```
- To Update a value:
  - **Example**
  ```bash
    fruits[0] = "grape"
  ```
- To Slice LIst:
  - **Example**
  ```bash
    print(fruits[1:3])       # Returns a sublist with elements at index 1 and 2
  ```
---

# 2. CRUD Operations With FastAPI

## 2.1 FastAPI
- **FastAPI**: FastAPI is a modern and high-performance Python web framework used to build APIs quickly and efficiently. Designed with simplicity it allows developers to create RESTful APIs using Python's type hints which also enable automatic validation and error handling

## 2.2 Setup and Install
- To Include FastAPI library in your project install fastapi
  ```bash
     pip install fastapi
  ```
## 2.3 To run fastapi apps install uvicorn

```bash
pip install uvicorn
```
## 2.4 CRUD operations in Fastapi
- CRUD refers to the basic operations that can be performed on data in a database. It stands for Create, Read, Update, and Delete, and it represents the fundamental functionalities that are essential for managing data in most applications.
  - CREATE: It involves adding new data to the database. In FastAPI, we can create data by sending a POST request to the appropriate endpoint.
  - READ: It involves retrieving existing data from the database. In FastAPI, we can perform Read operations using GET requests.
  - UPDATE: It involves updating existing data in the database. In FastAPI we can perform an Update operation using PUT/PATCH, PUT allows us to update the entire database whereas PATCH allows us to modify specific fields in the database.
  - DELETE: It involves deleting existing data from the database. In FastAPI we can perform a Delete Operation using DELETE requests.

## 2.5 Operation Mapping
- Create: POST /items/
- Read (List): GET /items/
- Read (Single): GET /items/{item_id}
- Update: PUT /items/{item_id}
- Delete: DELETE /items/{item_id}

## Conclusion
- In this article you learned about python basics and implementation of CRUD with fastapi