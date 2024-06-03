# Intro
This document contains basic coding challenges that the reader is supposed to answer with Python. There is not a single definitive answer to each question but the reader is encouraged (and expected) to apply coding best practices that will result in readable and reusable code.

## Calculating the sum of a list of numbers
You need to calculate the sum of a list of numbers without using the builtin `sum` (or similar methods or functions). You are also not allowed to use loops or list comprehensions. How could you create a function that accepts any sequence of numbers and returns the sum in a generic way?

```python
>>> numbers = [1, 2, 3, 4]
>>> custom_sum(numbers)
10
```

## Using a decorator to time the duration of a function
Let's say you have a (potentially) compute expensive function like the one shown below. You want to measure the time it takes to run this function. On each function invocation you want to print timing statistics to stdout. You want to use a decorator to get this done. How would you do this?

```python
def fibonacci(n):
    """Return the sum for the first `n` numbers in a Fibonacci series"""

    if n == 1:
        return 0
    elif n in (2, 3):
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

## Creating a JSON reader to read properties
You have an application that receives this kind of JSON data on a regular basis. You have written a bit of code that loads this JSON record into a basic Python dictionary.

However instead of accessing the attributes like `record['serial']` you want to create your own class that stores an instance of this dictionary and makes the JSON properties accessible as attributes.

You **cannot** write dedicated methods for each attribute and you are expected to code this into your class using just magic methods (methods like `__init__` and `__getitem__` are examples of magic methods).


```python
>>> record = read_json()  # Assume this reads a single json record into an instance of your class
>>> record.serial  # your class instance should make the properties available as attributes
33457
```

```json
{
    "serial": 33457,
    "name": "Refactoring 101",
    "event_type": "40-minute conference session",

    "time_start": "2014-07-23 11:30:00",
    "time_stop": "2014-07-23 12:10:00",
    "venue_serial": 1449
}
```

### Spotting Antipatterns
Which antipatterns do you spot in the way this class is defined.

```python
class Employee:
	def __init__(self, name, dob, address, job_name):
		self.name = name
		self.dob = dob
		self.address = address
		self.job_name = job_name
		self.connection = Connection(username='npa', password='123')

	def create(self):
		insert_sql = f'''
		INSERT INTO employees VALUES ({self.name}, {self.dob}, {self.address}, {self.job_name})
		'''
		with self.connection.open() as con:
			con.execute(insert_sql)
```
