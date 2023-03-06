# Part A

- 20 questions
- 1 mark per qn

## Questions:
 
### 1. Interpreting & explaining exception handling code (syntax, output, flow of control)

   - try: The try block is used to enclose the code that may potentially throw an exception.
   - catch: If an exception is thrown, the catch block is executed to handle the exception.
   - throw: The throw statement is used to explicitly throw an exception when a problem is detected.
   - Example:

     ```
     #include <iostream>
     using namespace std;

     int main() {
       try {
         int age;
         cout << "Enter your age: ";
         cin >> age;
         if (age < 0) {
         throw age;
         }
         cout << "Your age is " << age << endl;
       }
       catch (int age) {
         cerr << "Error: Invalid age entered: " << age << endl;
       }
       return 0;
     }
     ```

### 2. Concepts behind exception handling

   - The basic concept of exception handling is to separate the error handling code from the normal flow of the program.

### 3. Namespace ('using', scope, unnamed, nested, etc)

   - Namespace allows you to group related identifiers (such as variables, functions, and classes) together under a single name.
   - Scope refers to the region of a program where a particular variable/function or object can be accessed.
   - To use identifiers from a namespace, you can either prefix them with the namespace name and the scope resolution operator ::, or you can bring them into the current scope using the 'using' keyword.
   - Examples:

     ```
     namespace my_namespace {
       int my_variable;
       void my_function();
     }

     // Using scope resolution operator
     int x = my_namespace::my_variable;
     my_namespace::my_function();

     // Using 'using' keyword
     using my_namespace::my_variable;
     using my_namespace::my_function;
     
     int y = my_variable;
     my_function();

     // unnamed namespace
     namespace {
       int my_variable;
       void my_function();
     }
     ```

### 4. Function template, concepts, reasons for it, coding it, using it in declaration (explicit specification of type <>)

   - A generic function that can work with different types of data. It is defined using a template keyword followed by a placeholder for the data type
   - The concept is to have the function work with multiple types of data, without the need for creating separate functions for each data type. This helps to write more concise and reusable code.
   - Allows for more flexible and reusable code.
   - Examples on explicit and implicit specified in the function call:

     ```
     template <typename T>
     T add(T x, T y) {
       return x + y;
     }

     int main() {
       int a = 5, b = 10;
       double c = 2.5, d = 3.5;

       // Implicit
       int sum1 = add(a, b);       // sum1 = 15
       double sum2 = add(c, d);    // sum2 = 6.0

       // Explicit
       int sum3 = add<int>(a, b);       // sum3 = 15
       double sum4 = add<double>(c, d); // sum4 = 6.0
     }
     ```

### 5. Difference between class vs struct, in terms of variables access:

   - The default accessibility in a struct is **public**.
   - The default accessibility in a class is **private**. 
   - Both struct and class have the flexibility to make variables public as well if declared.

### 6. Friend function, concept, reasons for it, coding it, how it is combined with insertion/extraction operator overloading

   - Friend is a keyword and is used with **non-member function** to access the private and protected members of a class
   - Example of using friend keyword:

     ```
     class MyClass {
     private:
       int x;
     public:
       friend void myFriendFunction(MyClass obj);
     };

     void myFriendFunction(MyClass obj) {
       obj.x = 10; // myFriendFunction can access private members of MyClass
     }
     ```

   - In this example, myFriendFunction is declared as a friend function of MyClass. Therefore, myFriendFunction has access to the private member _x_ of MyClass and can modify its value.

   - Example of using friend with insertion and extraction operator overloading:

     ```
     class MyClass {
     private:
       int x;
     public:
       MyClass(int num) : x(num) {}

       friend ostream& operator<<(ostream& os, const MyClass& obj);
       friend istream& operator>>(istream& is, MyClass& obj);
     };

     ostream& operator<<(ostream& os, const MyClass& obj) {
       os << obj.x; // Output the private member x
       return os;
     }

     istream& operator>>(istream& is, MyClass& obj) {
       is >> obj.x; // Input the private member x
       return is;
     }

     int main() {
       MyClass obj(5);

       // Output object using insertion operator
       cout << obj << endl; // Output: 5

       // Input object using extraction operator
       cin >> obj;

       // Output modified object using insertion operator
       cout << obj << endl;
       return 0;
     }
     ```

   - In this example, the insertion and extraction operators are overloaded as friend functions of MyClass. Therefore, they have access to the private member x of MyClass and can output or input its value. In the main function, the object obj is first output using the insertion operator. Then, the value of x is modified by inputting a new value using the extraction operator. Finally, the modified object is output again using the insertion operator.

### 7. Two different operator overloading ways, as **class member function** vs **friend function**, how to interpret, ways to overload binary operators, ways to invoke operators, how to code

   - Overloading as a **Class Member Function**:

     - To overload an operator as a member function, we need to define the function within the class declaration.
     - The overloaded operator function must consists of the **operator** keyword followed by the **symbol** for the operator being overloaded.
     - Here's an example of overloading the "+" operator as a class member function:

       ```
       class MyClass {
       public:
         int num;
         MyClass operator+(const MyClass& other) {
           MyClass result;
           result.num = num + other.num;
           return result;
         }
       };
       ```

   - Overloading as a **Friend Function**:

     - We need to define the operator function outside of the class declaration and declare it as a friend of the class. This allows the operator function to access the private members of the class.
     - Here's an example of overloading the "+" operator as a friend function:

       ```
       class MyClass {
       private:
         int num;
       public:
         // Declaration of operator+ as a friend function
         friend MyClass operator+(const MyClass& lhs, const MyClass& rhs);
       };
       
       friend MyClass operator+(const MyClass& lhs, const MyClass& rhs) {
         MyClass result;
         result.num = lhs.num + rhs.num;
         return result;
       }
       ```

   - Invoking operators:

     ```
     MyClass obj1, obj2, result;
     result = obj1 + obj2;
     ```

### 8. Difference btw acccess modifiers (public/ protected/ private) and its meaning when

   1. Used within a class declaration:

      - When you declare a member as public, protected, or private within a class, you are controlling the visibility and accessibility of that member within the class and its derived classes.
      - Public members are accessible from anywhere in the program, both inside and outside the class.
      - Private members can only be accessed from within the class itself. They are not accessible outside the class, even in derived classes.
      - Protected members are similar to private members, but they can be accessed by derived classes in addition to the base class.

   2. Used in conjunction with specifying super-sub class inheritance (e.g class Derived : private Base)

      - When you specify the type of inheritance (public, protected, or private), you are controlling the accessibility of the members of the base class in the derived class. This determines whether the members are public, protected, or private in the derived class, and thus affects their accessibility and visibility within the derived class and its derived classes.
      - Public inheritance: The public members of the base class become public members of the derived class, the protected members of the base class become protected members of the derived class, and the private members of the base class are not accessible in the derived class.
      - Protected inheritance: The public and protected members of the base class become protected members of the derived class, and the private members of the base class are not accessible in the derived class.
      - Private inheritance: The public and protected members of the base class become private members of the derived class, and the private members of the base class are not accessible in the derived class.

### 9. Difference betw class constructors VS destructors in terms of concepts, when it is being used and how it is declared

   - Constructors are used to initialize objects of a class, while destructors are used to destroy them.
   - Destructors are distinguished by the tilde operator (~).
   - Destructors cannot have any arguments, whereas constructors can.
   - Constructors are called when an object of a class is created, while destructors are called when an object of a class is deleted.
   - Constructors allocate memory for objects of a class, while destructors deallocate the memory.
   - Constructors can be overloaded with multiple versions, but destructors cannot.
   - A class can have multiple constructors, but only one destructor.

     ```
     class MyClass {
     public:
       MyClass();         // default constructor
       MyClass(int x);    // constructor with parameter
       ~MyClass();        // destructor

     private:
       int m_x;
     };

     MyClass::MyClass() {
       // default constructor implementation
       m_x = 0;
     }

     MyClass::MyClass(int x) {
       // constructor with parameter implementation
       m_x = x;
     }

     MyClass::~MyClass() {
       // destructor implementation
     }
     ```

### 10. Difference betw 2 ways in which 'virtual' keyword is used
   - To declare virtual/pure virutal functions
   
      - When a member function is declared as **virtual** in a base class, it can be overridden in a derived class.
      - When a member function is declared as **pure virtual** in a base class, it **must be overridden** in any derived class that is not also an abstract class.
      - Virtual functions allow dynamic binding, which means that the correct function to call is determined at runtime based on the type of the object being pointed to or referenced.
      - Pure virtual functions are declared using the = 0 syntax and have no implementation in the base class.

      ```
      class Shape {
      public:
          virtual void draw() = 0;  // pure virtual function
          virtual void move(int x, int y);  // virtual function
      };

      class Circle : public Shape {
      public:
          void draw() override;  // override pure virtual function
          void move(int x, int y) override;  // override virtual function
      };
      ```

   - To prevent "diamond of death" (multiple inheritance)
   
      - It can occur when a class inherits from two or more classes that have a common base class. This can lead to multiple inheritance paths, and if the base class has any non-virtual functions, there can be ambiguity about which implementation to use.
      - To prevent it, you can use the virtual keyword when inheriting from the base class. This creates a "virtual base class", which means that only one instance of the base class is created, even if it appears multiple times in the inheritance hierarchy.

      ```
      class A {
      public:
        int x;
      };

      class B : virtual public A {
      public:
        int y;
      };

      class C : virtual public A {
      public:
        int z;
      };

      class D : public B, public C {
      public:
        void setX(int value) { x = value; }  // x is now unambiguous
      };
      ```

      - In this example, B and C both inherit from A as a virtual base class, and D inherits from both B and C. This ensures that there is only one instance of A in the inheritance hierarchy, and that `x` is unambiguous in D.

### 11. Valid ways to declare iterators for a container like vector (eg. const, non-const, foward, reverse)

   - Const and non-const iterators

     - Vector provides two types of iterators: iterator and const_iterator.
     - Iterator is used to iterate over a non-const vector, while const_iterator is used to iterate over a const vector.
     - A regular or non const_iterator points to an element inside the container and **can be used to modify** the element to which it is pointing
     - A const iterator points to an element of constant type which means the element which is being pointed to by a const_iterator **can’t be modified.**
     - Example of using iterator and const_iterator to iterate over a non-const/const vector:

        ```
        vector<int> vec = {1, 2, 3, 4};
        for (vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
          *it += 1;              // Able to update elements of vector
          cout << *it << endl;
        }

        const vector<int> cvec = {1, 2, 3, 4};
        for (vector<int>::const_iterator cit = cvec.begin(); cit != cvec.end(); ++cit) {
          cout << *cit << endl;
        }
        ```

   - Reverse iterators

     - Vector also provides two types of iterators for iterating in reverse: reverse_iterator and const_reverse_iterator.
     - Reverse_iterator is used to iterate over a non-const vector in reverse, while
     - Const_reverse_iterator is used to iterate over a const vector in reverse.
     - An example of using a reverse_iterator and const_reverse_iterator to iterate over a non-const/const vector in reverse:

      ```
      vector<int> vec = {1, 2, 3, 4};
      for (vector<int>::reverse_iterator it = vec.rbegin(); it != vec.rend(); ++it) {
        *it += 1;              // Able to update elements of vector
        cout << *it << endl;
      }

      const vector<int> cvec = {1, 2, 3, 4};
      for (vector<int>::const_reverse_iterator cit = cvec.rbegin(); cit != cvec.rend(); ++cit) {
        cout << *cit << endl;
      }
      ```

   - Constness of the container does not affect whether you can use forward or reverse iterators, but it affects whether you can use const or non-const iterators. In general, you should use const iterators whenever possible to avoid unintentionally modifying a container.

     - An example of using a const_reverse_iterator to iterate over a const vector in reverse:
        ```
        const vector<int> vec = {1, 2, 3, 4};
        for (vector<int>::const_reverse_iterator it = vec.rbegin(); it != vec.rend(); ++it) {
          cout << *it << endl;
        }
        ```

### 12. List major components of STL (e.g containers, generic algorithms adapter, etc) and briefly explain its purpose

   - CONTAINERS
      A container is a holder object that stores a collection of other objects. It manages the storage space for its elements and provides member funcitons to access them, either directly or through iterators

   - ITERATORS
      Iterators are used to point at the memory address of STL containers. They are primarily used in sequence of numbers, characters, etc. They reduce the complexity and execution time of program.

   - GENERIC ALGO
      Algorithm are applied to containers through the iterators that are available to traverse containers. It is a description of a procedure that terminates with a result.

   - FUNCTION OBJECTS
      Objects that are instances of classes that have an overloaded operator(), the functin call operator, are considered to be function objects. it provides two main advantages over a straight function call. The first is that a function object can contain state. The second is that a function object is a type and therefore can be used as a template parameter.

   - ADAPTERS
      The adapter acts as a wrapper between two objects. It catches calls for one object and transforms them to format and interface recognizable by the second object.

   - ALLOCATORS
      They are objects responsible for encapsulating memory management. It is used when you want to separate allocation and do construction in two steps. It is also used when separate destruction and deallocation is done in two steps. The default allocator simply uses the operators new and delete to obtain and release memory.

### 13. How to prevent inheritance in C++ 11

   - We prevent inheritance by declaring a class as **final**. The final keyword indicates that the class cannot be used as a base class, i.e., it cannot be inherited by other classes.
   - An example:

      ```
      class Base final {
        // Class implementation here
      };

      class Derived : public Base { // Error: 'Base' is marked as 'final'
        // Class implementation here
      };
      ```

### 14. Difference betw method overloading VS overridding

   - The **number** or **types** of parameters may differ in method overloading, but they must be the same for method overriding.
   - Method overriding can only happen when the base class has the function declared as **virtual**, only then can the derived class override the function. But method overloading does not require any specific keywords.
   - Method overriding is accomplished during **run-time** and method overloading is accomplished during **compile-time**.
   - The destructor for a class cannot be overloaded in any way, neither through method overloading nor method overriding.

### 15. Meaning of * and -> when used in conjunction with 'this' keyword (eg. (*this).someVariable or this->someVariable or \*this->someVariable , etc)

   - To access the current object from within a member function, you can use the **this** pointer.
   - For example, suppose you have a class called MyClass with a member variable called myVariable:

      ```
      class MyClass {
      public:
        void myMethod() {
          int x = (*this).myVariable;
          int y = this->myVariable;
          int z = *this->myVariable;
        }

      private:
        int myVariable;
      };
      ```

   - When you use \*this, you are dereferencing the this pointer, which gives you a reference to the current object. You can then access the member variables and member functions of the object using the dot (.) operator. For example, (\*this).someVariable would access the someVariable member variable of the current object.
   - When you use this->, you are using the arrow (->) operator to access the member variables and member functions of the current object directly. This is equivalent to using (\*this). to access the member variables and member functions. For example, this->someVariable would access the someVariable member variable of the current object.
   - It is also possible to use *this-> to dereference the this pointer and then access a member variable or member function of the current object using the arrow (->) operator. For example, *this->someVariable would access the value of the someVariable member variable of the current object.

### 16. What does it mean to have an abstract class, and how to declare it?

   - An abstract class is a class that cannot be instantiated, meaning you cannot create objects of an abstract class.
   - Contains at least one pure virtual function.
   - You declare a pure virtual function by using a pure specifier ( = 0 ) in the declaration of a virtual member function in the class declaration.
   - Example:
      ```
      class Shape {
      public:
        virtual double area() const = 0; // pure virtual function
      };
      ```

### 17. What does it mean to provide .h and .o file to a "client", and why would we do this? Explain how the .h and .o files are related

   - Providing .h and .o files to a client means giving them the header file and compiled object file of a program or library. We do this to allow the client to use the functions and classes defined in the program/library without having access to the source code. The .h file contains function and class declarations, while the .o file contains compiled machine code for those functions and classes. They are related in that the .h file tells the client what functions and classes are available and how to use them, while the .o file provides the actual code to execute those functions and classes.

# Part B

- 6-9 questions
- varying marks per qns

## Questions:

### 1. Writing Declaration & implementation for structs

   - Struct delcaration ends with a semicolon
   - Example:

     ```
     // Struct declaration
     struct Person {
         std::string name;
         int age;
         float height;

         // Constructor declaration
         Person(std::string name, int age, float height);

         // Method declaration
         void sayHello();
     };

     // Constructor implementation
     Person::Person(std::string name, int age, float height) {
         this->name = name;
         this->age = age;
         this->height = height;
     }

     // Method implementation
     void Person::sayHello() {
         std::cout << "Hello, my name is " << name << " and I'm " << age << " years old." << std::endl;
     }
     ```

### 2. Implementating functions that uses / access

   - struct variables example:

     ```
     #include <iostream>
     using namespace std;

     // Struct declaration
     struct Person {
       string name;
       int age;
     };

     // Function that uses/accesses a struct variable
     void printPersonInfo(Person p) {
       cout << "Name: " << p.name << endl;
       cout << "Age: " << p.age << endl;
     }

     int main() {
       // Struct variable initialization
       Person john;
       john.name = "John";
       john.age = 30;

       // Function call that uses/accesses a struct variable
       printPersonInfo(john);

       return 0;
     }
     ```

   - array of struct example:

     ```
     #include <iostream>
       using namespace std;

       // Struct declaration
       struct Person {
         string name;
         int age;
       };

       // Function that uses/accesses an array of struct
       void printPersonArray(Person people[], int n) {
         for (int i = 0; i < n; i++) {
           cout << "Name: " << people[i].name << endl;
           cout << "Age: " << people[i].age << endl;
         }
       }

       int main() {
         // Array of struct initialization
         Person people[3] = {
           {"John", 30},
           {"Mary", 25},
           {"Bob", 40}
         };

         // Function call that uses/accesses an array of struct
         printPersonArray(people, 3);

         return 0;
       }
     ```

### 3. Exception Handling : basic concepts - Try, Throw, Catch, writing Exception Class, throwing Exception objects, etc

   - Try block: A try block contains the code that may throw an exception. If an exception is thrown in the try block, the program jumps to the corresponding catch block.
   - Throw statement: A throw statement is used to explicitly throw an exception. It can throw an object of any type.
   - Catch block: A catch block catches an exception thrown by a try block. It contains code that handles the exception. A catch block can handle one or more types of exceptions
   - Exception class: An exception class is a user-defined class that represents an exception. It can be thrown as an object of that class.
   - Example:

     ```
     #include <iostream>

     class MyException : public std::exception {
     private:
         std::string message;
     public:
         MyException(std::string msg) : message(msg) {}
         std::string getMessage() const { return message; }
     };

     void divide(int x, int y) {
         if (y == 0) {
             throw MyException("Division by zero");
         }
         std::cout << x / y << std::endl;
     }

     int main() {
         try {
             divide(10, 2);
             divide(10, 0);
         } catch (const MyException& e) {
             std::cout << "Exception caught: " << e.getMessage() << std::endl;
         }
         return 0;
     }
     ```

### 4. Operator overloading:

   - A function that overloads =, (), [] or -> for a class must be a member function of this class. (no need use friend)
   - Relatonal (==, <, >, <=, >=, and !=)

     - They are used to **compare** objects of a class and can be overloaded to define the meaning of comparison for a particular class.
     - Example using without friend

       ```
        class Person {
        private:
            string name;
            int age;
        public:
            Person(string n, int a) : name(n), age(a) {}

            // Overload the less than operator
            bool operator<(const Person& other) const {
                return age < other.age;
            }
        };

        int main() {
            Person p1("John", 25);
            Person p2("Emily", 30);

            if (p1 < p2) {
                cout << p1.getName() << " is younger than " << p2.getName() << endl;
            } else {
                cout << p1.getName() << " is older than " << p2.getName() << endl;
            }

            return 0;
        }
       ```

     - Example using with friend

       ```
        #include <iostream>
        using namespace std;

        class Complex {
        private:
            double real;
            double imag;

        public:
            Complex(double r = 0, double i = 0) : real(r), imag(i) {}

            // Binary operator overloading using friend function
            friend Complex operator+(const Complex &c1, const Complex &c2);

            void display() {
                cout << real << " + i" << imag << endl;
            }
        };

        // Friend function definition
        Complex operator+(const Complex &c1, const Complex &c2) {
            return Complex(c1.real + c2.real, c1.imag + c2.imag);
        }

        int main() {
            Complex c1(2.0, 3.0), c2(4.0, 5.0), c3;
            c3 = c1 + c2; // Using the overloaded binary operator
            c3.display();

            return 0;
        }
       ```

   - Binary (+, -, \*, /, %, and &)

     - They are used to **perform arithmetic or logical operations** on objects of a class and can be overloaded to define the behavior of the operator for a particular class.
     - Example

       ```
       class MyNumber {
       private:
          int value;
       public:
          MyNumber(int v) : value(v) {}
          MyNumber operator+(const MyNumber& other) const {
              return MyNumber(value + other.value);
          }
          // other member functions and data members...
       };


        int main() {
        MyNumber a(5);
        MyNumber b(10);
        MyNumber c = a + b; // calls operator+ overload
        std::cout << c.getValue() << std::endl; // prints 15
        return 0;
        }

       ```

   - Io operators (<<, >>)

     - They are used to **perform input/output operations** on objects of a class and can be overloaded to define how the object should be represented when printed to the console or read from input.
     - Example for <<

     ```
      #include <iostream>
      #include <string>

      class Person {
      public:
          Person(std::string n, int a) : name(n), age(a) {}
          std::string getName() const { return name; }
          int getAge() const { return age; }
      private:
          std::string name;
          int age;
      };

      std::ostream& operator<<(std::ostream& os, const Person& p) {
          os << "Name: " << p.getName() << ", Age: " << p.getAge();
          return os;
      }

      int main() {
          Person john("John", 30);
          std::cout << john << std::endl;
          return 0;
      }
     ```

### 5. Please refer to all examples with << insertion and >> extraction operators, how it is associated with a class, how it is implemented

   - Example for >>

     ```
     #include <iostream>
     #include <string>

     class Person {
     public:
         std::string name;
         int age;
         Person(std::string name = "", int age = 0) : name(name), age(age) {}
     };

     std::istream& operator>>(std::istream& is, Person& person) {
         is >> person.name >> person.age;
         return is;
     }

     int main() {
         Person p;
         std::cout << "Enter name and age: ";
         std::cin >> p;
         std::cout << "Name: " << p.name << ", Age: " << p.age << std::endl;
         return 0;
     }
     ```

### 6. Writing Declaration & Implementation for classes, in relation to the following concepts:

   - Encapsulation:

     - Process of hiding the implementation details of a class from the outside world and providing a well-defined interface for interacting with the class.
     - File level: using _.h and _.cpp for each class, together with #ifndef, #define, #endif header guards
       - To prevent multiple inclusion of the same header file, #ifndef, #define, and #endif preprocessor directives are often used to create header guards. These guards ensure that the contents of the header file are only included once in a single translation unit, preventing duplicate symbol definitions and reducing compile time.
     - Variable level : using private / protected / public when necessary
     - Example

       ```
        // Point2D.h

        #ifndef POINT2D_H
        #define POINT2D_H

        class Point2D {
        private:
            double x;
            double y;

        public:
            Point2D();
            Point2D(double x, double y);

            double getX() const;
            void setX(double x);

            double getY() const;
            void setY(double y);
        };

        #endif

        // Point2D.cpp
        #include "Point2D.h"

        Point2D::Point2D() : x(0), y(0) {}

        Point2D::Point2D(double x, double y) : x(x), y(y) {}

        double Point2D::getX() const {
            return x;
        }

        void Point2D::setX(double x) {
            this->x = x;
        }

        double Point2D::getY() const {
            return y;
        }

        void Point2D::setY(double y) {
            this->y = y;
        }
       ```

   - Inheritance:

     - Creating a new class by extending an existing class
     - how to specify super-sub classes, what files to #include
     - Example

     ```
        #ifndef SAVINGS_ACCOUNT_H
       #define SAVINGS_ACCOUNT_H

       #include "BankAccount.h"

       class SavingsAccount : public BankAccount {
       private:
           double interestRate;

       public:
           SavingsAccount(std::string accountNumber, double balance, double interestRate);

           void addInterest();
       };

       #endif
     ```

   - Polymorphism:

     - Ability of an object to take on many forms
     - Using **virtual functions** and **method overriding**
     - Virtual function is a function in the base class that is declared with the virtual keyword and is intended to be overridden in the subclasses
     - Method overriding is the process of providing a new implementation for a virtual function in a subclass.
     - When a pointer to a base class is used to access a derived class object, the correct virtual function is called based on the actual type of the object, rather than the type of the pointer. This is known as **dynamic binding**, as the function call is determined at **runtime**, whereas **static binding** is determined at **compiled time**.
     - Here is an example of implementing method overriding and dynamic binding in C++:

       ```
       class Shape {
       public:
           virtual double getArea() {
               return 0.0;
           }
       };

       class Circle : public Shape {
       private:
           double radius;
       public:
           Circle(double r) {
               radius = r;
           }
           double getArea() {
               return 3.14 * radius * radius;
           }
       };

       class Rectangle : public Shape {
       private:
           double length;
           double width;
       public:
           Rectangle(double l, double w) {
               length = l;
               width = w;
           }
           double getArea() {
               return length * width;
           }
       };

       int main() {
           Shape* shape1 = new Circle(5.0);
           Shape* shape2 = new Rectangle(3.0, 4.0);
           cout << "Circle area: " << shape1->getArea() << endl;       // Circle area: 78.5
           cout << "Rectangle area: " << shape2->getArea() << endl;    // Rectangle area: 12
           return 0;
       }
       ```

### 7. Class template

   - how to declare a simple class template
   - writing implementation code for class template
   - (refer to 1st 5-6 slides on 'class templating' lecture notes)

### 8. How to declare and correctly use

   - STL containers (eg. vector)
   - Designed to hold and organize collections of elements
     - #include &lt;vector&gt;
     - #include &lt;deque&gt;
     - #include &lt;list&gt;
     - #include &lt;forward_list&gt;
     - #include &lt;set&gt;
     - #include &lt;map&gt;
     - #include &lt;unordered_set&gt;
     - #include &lt;unordered_map&gt;
   - Sequence containers:
     - vector: dynamic array
     - deque: double-ended queue
     - list: linked list
     - forward_list: singly linked list
   - Associative containers:
     - set: sorted set of unique elements
     - multiset: sorted set of non-unique elements
     - map: sorted key-value pairs of unique keys
     - multimap: sorted key-value pairs of non-unique keys
   - Unordered containers:
     - unordered_set: unordered set of unique elements
     - unordered_multiset: unordered set of non-unique elements
     - unordered_map: unordered key-value pairs of unique keys
     - unordered_multimap: unordered key-value pairs of non-unique keys

- Generic Algorithim (eg. find)

  - Functions that can be used with different types of containers
  - #include &lt;algorithim&gt;
  - Some commonly used generic algorithms in C++ include:
    - find(): This algorithm is used to find the first occurrence of a value in a container. It returns an iterator to the found element, or an iterator to the end of the container if the value is not found
    - sort(): This algorithm is used to sort the elements of a container in ascending order. It takes two iterators as arguments, representing the beginning and end of the range to be sorted
    - reverse(): This algorithm is used to reverse the order of the elements in a container. It takes two iterators as arguments, representing the beginning and end of the range to be reversed
    - count(): This algorithm is used to count the number of occurrences of a value in a container. It takes two iterators as arguments, representing the beginning and end of the range to be searched
    - accumulate(): This algorithm is used to compute the sum of the elements in a container. It takes two iterators as arguments, representing the beginning and end of the range to be accumulated, as well as an initial value

- Iterators (eg. foward/ reverse iterators for vector)

  - Iterators are objects that are used to traverse and access the elements of a container
  - Example

    ```
    #include <vector>
    using namespace std;

    vector<int> myVector = {5, 10, 15, 20};

    // Forward Iterator
    for (vector<int>::iterator it = myVector.begin(); it != myVector.end(); ++it) {
        cout << *it << endl;
    }

    // Reverse Iterator
    for (vector<int>::reverse_iterator rit = myVector.rbegin(); rit != myVector.rend(); ++rit) {
        cout << *rit << endl;
    }
    ```

- Default Random Engine (within #include<random>)

  - The default random engine is a pseudorandom number generator that is part of the C++ standard library
  - Example

    ```
    #include <iostream>
    #include <random>

    int main() {
        // Create a default random engine
        std::default_random_engine engine;

        // Generate a random number between 0 and 9
        std::uniform_int_distribution<int> distribution(0, 9);
        int random_number = distribution(engine);

        std::cout << "Random number: " << random_number << std::endl;

        return 0;
    }
    ```
