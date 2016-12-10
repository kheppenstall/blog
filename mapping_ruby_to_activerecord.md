# Mapping Ruby Enumerables to ActiveRecord Methods

## Introduction

In any web application, using Ruby to parse data after querying your database is extremely slow. I learned that the hard way. That is not what Ruby was built for. Instead we use ActiveRecord. But that means learning a whole new set of methods. This document is to help you learn the ActiveRecord equivalent of Ruby enumerables.

[Ruby Enumerables Documentation](https://ruby-doc.org/core-2.2.3/Enumerable.html)

[ActiveRecord Documentation](http://api.rubyonrails.org/classes/ActiveRecord/QueryMethods.html)

## Example Context
Let's consider students, classes, and teachers. Students can be enrolled in many classes. Teachers can teach many classes. Classes can have many students but only one teacher.


And here are our example relationships:

* Many students to many classes
* 1 teacher to many classes

#### Models
```ruby
class Teacher 
  has_many :classes
end

class Student 
  has_many :classes
end

class Class 
  belongs_to :teacher
  belongs_to :student 
end
```

And here are the attributes of each model.

Students have a `first_name`, `last_name`, and `id`.

Teachers have a `first_name`, `last_name`, and `id`.

Classes have a `name`, `enrollment` (integer), `id`.


## Example Maps

* #### `find_all` / `select` (Ruby) to `where` (ActiveRecord)

  `# Find all students with the first name John`

  Ruby

  ```ruby
  Student.all.find_all {|student| student.first_name == 'John'}
  ```

  ActiveRecord

  ```ruby
  Student.where(name: 'John')
  ```

* #### `sort_by` (Ruby) to `order` (ActiveRecord) with one argument

  `# Sort students by last name`

  Ruby

  ```ruby
  Student.all.sort_by {|student| [student.last_name}
  ```

  ActiveRecord

  ```ruby
  Student.order(:last_name)
  ```

* #### `sort_by` (Ruby) to `order` (ActiveRecord) with multiple arguments

  `# Sort students by last name, then first name`

  Ruby

  ```ruby
  Student.all.sort_by {|student| [student.last_name, student.first_name]}
  ```

  ActiveRecord

  ```ruby
  Student.order(:last_name, :first_name)
  ```

* #### `map` (Ruby) to `pluck` (ActiveRecord)

  `# List of first names of all students`

  Ruby

  ```ruby
  Student.all.map {|student| student.first_name}
  ```

  ActiveRecord

  ```ruby
  Student.pluck(:first_name)
  ```

* #### `reduce` (Ruby) to `sum` (ActiveRecord)

  `# The sum of enrollments over all classes.`

  Ruby

  ```ruby
  Class.all.reduce(0) {|sum, class| sum += class.enrollment}
  ```

  ActiveRecord

  ```ruby
  Class.sum(:enrollment)
  ```



