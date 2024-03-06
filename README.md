# Documentation Tests - Pytest
## Description
Tests are an important step in software development.  
Pytest is a Python testing library.

## Sommaire
1. [General testing best practices](#General-testing-best-practices)
2. [Unit tests](#Unit-tests)  
    a. [Technically - Assert](#Assert)  
    b. [Techniquement - Fixtures](#Fixtures)  
    c. [Techniquement - Parametrize](#Parametrize)  
    d. [Techniquement - Mark](#Mark)
3. [Useful commands](#Useful-commands)  
4. [Test output](#Test-output)

## General Testing Best Practices
It is important to follow the testing pyramid in terms of creating tests and their significance in software development.  
For example, one can refer to testing methodologies such as AAA or GWT for unit tests (Arrange, Act, Assert or Given When Then, respectively).  
Developing a unit test means being precise and isolated. When working with data such as pandas data, it is important to only include the necessary columns for the test to function.  

## Unit Tests
Unit tests are tests that allow for a detailed examination of the code.  
They are generally used to test a function.  
Compared to other tests, it is important to have many unit tests.  
Unit tests should be created during development (before production code) in order to test and improve the code continuously (CI/CD perspective).  
Unit tests should be fast (in execution), independent (of other tests or functions), and precise (testing only one functionality).  

### Technically
What are the technical aspects of pytest? How do you create a unit test with pytest?

#### Assert
Pytest works with the "assert" keyword, which allows for the verification of equality between the function's execution in the test and the expected result.  
This is the most important element of any unit test. A unit test in pytest is valid as long as a condition is verified in this way.  
Example of a test with an assert in the AAA format:
```
# Arrange
un = 1
deux = 2
resultat_attendu = 3

# Act
resultat_test = ma_fonction_somme(un, deux)

# Assert
assert resultat_test == resultat_attendu
```
##### Spécification pandas
Ne pas faire de assert mais plutôt ```pd.testing.assert_frames_equal```.  


#### Fixtures
To go further, there are fixtures in pytest.  
Fixtures in pytest are Python decorators that allow for the initialization of parts of code that can be isolated and reused.  
Written in the following format:
```
import pytest

class Student:
    def __init__(self):
        self.grades = []

@pytest.fixture
def student():
    return Student()

def test_create_student_grades(student):
    assert student.grades == []
```

#### Parametrize
Allows for the definition of parameters for the test.  
Written in the following format:
```
@pytest.mark.parametrize("grade_1,grade_2, grade_3, average",  [(12, 10, 8, 10), (20, 18, 16, 18), (3,9,9,7)])

# application dans la fonction
def test_average(grade_1, grade_2, grade_3, average):
  student = Student()
  student = Student()
  student.grades = [] #Set an empty list of grades each time the test runs
  student.add_grade(grade_1)
  student.add_grade(grade_2)
  student.add_grade(grade_3)
  assert student.academic_average == average
```

See : https://docs.pytest.org/en/7.1.x/example/parametrize.html

#### Mark
Allows for the launching of only certain types of test functions.  
Written in the following way:
```
@pytest.mark.slow
def test_slow_function():
    # Test code here
    pass

@pytest.mark.fast
def test_fast_function():
    # Test code here
    pass
```

See : https://docs.pytest.org/en/7.1.x/example/markers.html

## Useful Commands
General pytest :  
* In an entire folder, the command ```pytest``` will run all files starting with "test_".
* ```pytest <test_file_name.py>``` runs only the selected test file.
* ```pytest -vv``` provides more details in the test output.  

Marks :  
* And executed in the following way: ```pytest -v -m fast```.  
* You can also exclude them in this way: ```pytest -v -m "not slow"```.  

## Test output
Explanation of the outputs.
