> [Wiki](Home) ▸ **Ruby Coding Standards**

### Contents
1. [Introduction](#1-introduction)
2. [Coding Standards](#2-coding-standards)
    1. [General Guidelines](#21-general-guidelines)
    2. [External References](#22-external-references)
        1. [References](#221-references)
        2. [Links](#222-links)
    3. [Project Layout](#23-project-layout)
        1. [Project Files](#231-project-files)
        2. [Source Files](#232-source-files)
        3. [External Dependencies](#233-external-dependencies)
    4. [Naming](#24-naming)
        1. [Namespaces](#241-namespaces)
        2. [Other Naming Conventions](#242-other-naming-conventions)
        3. [Naming Descriptiveness](#243-naming-descriptiveness)
    5. [Files](#25-files)
        1. [Include Statements](#251-include-statements)
        2. [Using Statements and Namespace Aliases](#252-using-statements-and-namespace-aliases)
    6. [Classes](#26-classes)
        1. [Object Oriented Design](#261-object-oriented-design)
        2. [Class Header Files](#262-class-header-files)
        3. [Class Source Files](#263-class-source-files)
        4. [Class Definitions](#264-class-definitions)
        5. [Code Definitions in Header Files](#265-code-definitions-in-header-files)
        6. [Inheritance and Virtual Functions](#266-inheritance-and-virtual-functions)
        7. [Friends](#267-friends)
        8. [Nested Classes](#268-nested-classes)
    7. [Functions](#27-functions)
        1. [Inline](#271-inline)
        2. [Function Overloading](#272-function-overloading)
        3. [Passing Arguments](#273-passing-arguments)
        4. [Return Values](#274-return-values)
        5. [Const-Correctness](#275-const-correctness)
    8. [General](#28-general)
        1. [Strings](#281-strings)
        2. [Paths](#282-paths)
        3. [Typedefs](#283-typedefs)
        4. [Memory Management](#284-memory-management)
        5. [Avoid Code Duplication](#285-avoid-code-duplication)
        6. [Flow Control](#286-flow-control)
        7. [Serialization](#287-serialization)
        8. [SWIG Support](#288-swig-support)
    9. [Code Portability](#29-code-portability)
        1. [Compiler Warnings](#291-compiler-warnings)
        2. [Exceptions](#292-exceptions)
        3. [Logging](#293-logging)
        4. [Unit Tests](#294-unit-tests)
    10. [Formatting](#210-formatting)
        1. [Indentation and Wrapping](#2101-indentation-and-wrapping)
        2. [Comments](#2102-comments)
        3. [Old Code and Commented-out Code](#2103-old-code-and-commented-out-code)
        4. [Temporary Code](#2104-temporary-code)
3. [Ruby Coding Standards](#3-ruby-coding-standards)
    1. [Project Layout](#31-project-layout)
    2. [Naming](#32-naming)
    3. [Unit Tests](#33-unit-tests)
    4. [Indentation and Wrapping](#34-ndentation-and-wrapping)
    5. [Comments](#35-comments)

## 1. Introduction
The Ruby bindings to OpenStudio include a mix of compiled Swig generated extensions, pure Ruby libraries, unit tests of both the extensions and Ruby libraries, and example scripts to help users get started. These elements are packaged together and included in the OpenStudio installer. Centralizing all OpenStudio functionality to a single install location allows user scripts to reference the OpenStudio API in a standard way across computers and projects. Users reference the OpenStudio API from project specific scripts that are out of the scope of the OpenStudio project. However, as user scripts become more developed and mature we encourage them to be added back into the official OpenStudio distribution either as example scripts (low complexity) or pure Ruby libraries (higher complexity). Ruby-only functionality that is widely used will be ported to C++ so it can be available in bindings to other languages as well as the core C++ tools. The Ruby coding standards generally follow the C++ standards. In this chapter we only describe points of departure or clarify places where the C++ coding standards conflict with normal Ruby conventions.

## 2. Ruby Coding Standards

### 2.1. General Guidelines
These guidelines are not hard and fast rules, but rather general suggestions to keep in mind when making
design decisions.

- Keep the code as DRY (Do not repeat yourself) as possible
- Balance between Ruby magic and readable code
- Use the [Rubocop](https://github.com/bbatsov/rubocop) static code analyzer to inspect your code

### 2.2. References
Most of these standards are based on the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide)

### 2.3. Project Layout
The following name conventions are in place for Ruby files:

To limit complexity of Ruby include paths, all Ruby tests and scripts are assumed to be part of the OpenStudio library, that the `lib` directory is in the user's Ruby path, and that all required shared libraries are in the system's path (this is achieved during the `require 'openstudio'` call). Therefore, all Ruby scripts and libraries should refer to each other relative to the `lib` directory.


#### 2.3.1. Directory Structure
Ruby is full of conventions and these should be respected in order to enable other Ruby based tools when possible. The directory structure of a Ruby project should have the following conventions

1. bin - Any executables
1. test - Unit test directory
1. spec - RSpec test directory
1. lib - Library directory containing subdirectories of the modules and source files
1. ext - Native extensions

The name of the directories shall be the [snake cased](http://en.wikipedia.org/wiki/Snake_case) version of the Module or Class name

File names shall be snake cased, typically conforming to the sname cased version of the Module or Class name.

#### 2.3.2. Source Files
The following are common files used in Ruby and the expected extensions (case sensitive)

1. Rakefile - Rakefile
1. Gemfile - Gemfile
1. Ruby Files - .rb
1. Embedded Ruby Files - .rb.erb
1. Test Files - *_test.rb
1. Spec Files - *_spec.rb

#### 2.4. Naming
The top level module for OpenStudio code is `OpenStudio`. Sub modules are also used and follow the C++ namespaces for Swig extensions. Other conventions are:
- Classes are upper camel case, e.g. `DetailedGeometry`
- OpenStudio Member functions and local variables are lower camel case, e.g. `addVertex` and `timeOfDay`
- Ruby based member functions and local variables are snake cased, e.g. `add_vertex_ruby` and `time_of_day_ruby`
- Do not start the name of the function with `get_`
- Enumerations are snake cased and symbolized, e.g. `enum items{:small_items, :big_items}`
- Unit test cases are upper camel case and post-fixed with `_test`, individual tests are upper camel cased and prefixed by `test_`. The idea is that test cases be easily recognizable in standard output when running a large number of tests, use `_` to indicate spaces for greater readability.


#### 2.5. Mix-ins
Use Mix-ins with caution in order to maintain code readability.

#### 2.6. Unit Tests
We assume that C++ portions of OpenStudio are sufficiently tested using the C++ unit tests. Therefore, we do not require that all tests be duplicated for Ruby. However, we do encourage some testing of the Ruby extensions, particularly in areas where Swig does something novel to the exported classes (e.g. changes a name, maps types, etc). Pure Ruby libraries should be tested completely in Ruby. These tests are then ported to C++ unit tests when the functionality is added to the C++ code base.

#### 2.7. Indentation and Wrapping
We standardize on the following formatting conventions to improve code readability:

1. Wrap lines at 100 columns. If a line needs to be split, then the split should occur at some functional location (e.g., before/after the operator) and not just after the 100<sup>th</sup> character.
2. Tab character is two spaces

### 3. Comments
Documentation is an important part of any source code. Even the most well written code is hard to understand or maintain if it is not properly commented. Comments should be made in RDoc format for documentation generation. The developer is encouraged to insert as many comments as needed to explain the code, not just the minimum required.

#### 3.1. Documentation
