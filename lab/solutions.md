
* Using the new/save syntax, create a student, first and last name and an age

```
first = Student.new
first.first_name = "Jack"
first.last_name = "Ma"
first.age = 50
```

* Save the student to the database

```    
first.save
``` 
    
* Using the find/set/save syntax update the student's first name to taco

```
user = Student.find(1)
user.first_name = "taco"
user.save
```

* Delete the student (where first_name is taco)

```
user.destroy
```
 
* Validate that every Student's last name is unique

```
class Student < ActiveRecord::Base
	validates :last_name, :presence => true, 
		:uniqueness => true
end
```

* Validate that every Student has a first and last name that is longer than 4 characters

```
class Student < ActiveRecord::Base
	validates :first_name, :presence => true, 
		:length => {:minimum => 5}
	validates :last_name, :presence => true, 
		:length => {:minimum => 5}
end		
```

* Validate that every first and last name cannot be empty
  
```
class Student < ActiveRecord::Base
	validates_presence_of :first_name
	validates_presence_of :last_name
end
		
```

  
* Combine all of these individual validations into one validation (using validate and a hash)

```
class Student < ActiveRecord::Base
	validates :last_name, :presence => true,
		:uniqueness => true,
		:length => {:minimum => 5}
	validates :first_name, :presence => true,
		:length => {:minimum => 5}		
end

```

* Using the create syntax create a student named John Doe who is 33 years old


```
user = Student.create(:first_name => "John", :last_name => "Doe", :age => 33)
```

*    Show if this new student entry is valid

```
user.valid?

```

*    Show the number of errors for this student instance


```
user.errors.messages.name.length
user.errors.size

```

*    In one command, Change John Doe's name to Jonathan Doesmith


```
user.update_attributes(:first_name => "Jonathan", :last_name => "Doesmith")

```

*    Clear the errors array


```
user.errors.clear

```

*    Save Jonathan Doesmith


```
user.save

```

*    Find all of the Students


```
all = Students.all

```

*    Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error


```
Student.find_by_id(128)

```

*    Find the first student in the table


```
Student.first
```

 *   Find the last student in the table


```
Student.last
```

 *  Find the student with the last name of Doesmith


```
Student.where(:last_name => "Doesmith")
```

  *  Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order


```
Student.limit(5).offset(1).order(last_name::asc)

```

   * Delete Jonathan Doesmith


```
Student.where(:last_name => "Doesmith").destroy

```


*    Use the validates_format_of and regex to only validate names that consist of letters (no numbers or symbols) and start with a capital letter

```
validates :cammelCase? 

def cammelCase?

validates_format_of :first_name => /^[A-Z][a-z][A-Za-z]*$/

validates_format_of :last_name => /^[A-Z][a-z][A-Za-z]*$/

end


```

*    Write a custom validation to ensure that no one named Delmer Reed, Tim Licata, Anil Bridgpal or Elie Schoppik is included in the students table

```
FORBIDDEN_USERNAMES = ["Delmer Reed", "Tim Licata", "Anil Bridgpal", "Elie Schoppik"]
validate :username_is_allowed

Student.username = student.first_name + " " + student.last_name

username = user.username
def username_is_allowed
    if FORBIDDEN_USERNAMES.include?(username)
        errors.add(:username, "this is a restricted username")
    end
end
```