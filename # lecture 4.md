# # lecture 4

## 1.Designing Functions

**Design Tips**: 

Give each functions exactly one job

> Don't let functions to do multiple jobs,like the Swiss knife

Don't repeat yourself,just duplicate it

> Don't make functions iterate themselves

Define functions generally

> Let the functions to do general job,not a  specific condition

## 2.Higher-Order Functions

- **assert**

  ```python
  assert boolean_value,statement
  """when the boolean_value is false,then execute the statement"""
  ```

- **generalization**

  general those similar steps into one functions,don't repeat a step in different functions

## 3.functions as  return values

we could let a function to be the return value

```python
def make_adder(n):
    """
    >>> add_three=make_adder(3)
    >>> add_three(4)
    7    
    """
    def adder(k):
        return k+n
    return adder
```

## 4.lambda Expressions

- ```python
  square=lambda:x*x
  """
  square now is bound to a function called 'lambda',which returns the value of x*x 
  >>> square(4)
  16
  
  """
  ```

- **Difference Between Def & Lambda**

  only the def gives the function an *intrinsic* name

  ```python
  square=lambda:x*x
  """ 
  >>>square
  function <lambda>
  """
  
  def square(x):
      return x*x
  """ 
  >>>square
  function <square>
  """
  ```

  > *intrinsic* means the function has its own name,while using the Lambda Expressions only gives the name called 'Lambda'



​	



