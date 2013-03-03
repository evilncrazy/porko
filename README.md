Porko
=====

Porko is a markup language to create mock SQL databases. Designed to be terse and readable. 
Useful for fixtures or testing queries.

# Example

```php
# Create a person table
person id, name, age:
  # Insert some people. Porko can infer the type of the columns from the data.
  1, "Alice", 24
  2, "Bob", 26
  3, "Charlie", 30

# Create a pizza table
pizza name, cost, vegetarian (defaults_to no):
  # Add a vegetarian pizza
  Vegetarian, 6.00, yes # strings don't need to be quoted
  
  # Make more some pizzas
  name, cost (defaults_to 7.00):
    Supreme, Italian, Meat Lovers, Hawaiian # insert lots of entries on one line
    
# Create a likes table to represent who likes what pizzas
likes person_id, pizza_name:
  1, Supreme # Alice likes supreme
  1, Italian 
  2, Vegetarian # Bob likes vegetarian
```

# Data Types
* __String__: Single/Double quotes can be used, but are optional
* __Integer__
* __Decimal__: Must begin with a digit (e.g. 0.14)
* __Boolean__: Can be in the forms: true, false, yes, no

# Syntax Elements
## Lists
A list is just a bunch of comma separated values. Trailing commas are fine.

__Example:__ ```"Hello", 3.14, true``` or ```"Coffee", "Soup",``` or ```"single-list", ```

## Attribute Tuple
An attribute tuple is a comma separated tuple of key-value pairs.
It looks something like this: ```(attribute1 value1, attribute2 value2, ...)```

Values are optional.

__Example:__ ```(key, nullable, defaults_to null)```

# Syntax
## Creating a Database
By convention, the name of the database is the name of the Porko file without the .po extension.

__Example:__ ```pizzeria.po``` will use pizzeria as its database name

## Creating a table
Write the table name followed by a __list__ of column names. Each column name can be followed by an __attribute tuple__.

__Example:__ ```pizzeria id (primary_key), name (string, max_length 100), address ```

## Inserting rows
Standard way of inserting rows looks like this:
```
table-name column1, column2, column3: # need the colon at the end
  value1, value2, value3 # indented block
  value4, value5, value6 # insert corrosponding values for each column
```

However, you can also specific which columns you want to specify values for, using default values for the rest:
```
  # ... in a table insert block
  specific-column1 (optional attribute tuple), specific-column2 (optional attribute tuple):
    value1, value2 # indented block
    value3, value4
```

# Contribute
Feel free to contribute to the spec. Just send a pull request with your changes.
Parsers written in any language are welcome.
