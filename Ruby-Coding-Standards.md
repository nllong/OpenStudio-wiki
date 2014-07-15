> [Wiki](Home) ▸ **Ruby Coding Standards**

### Contents
1. [Introduction](#1-introduction)
2. [Ruby Coding Standards](#2-coding-standards)
    1. [General Guidelines](#21-general-guidelines)
    2. [References](#22-external-references)
    3. [Project Layout](#23-project-layout)
    4. [Naming](#24-naming)
    5. [Files](#25-files)
    6. [Classes](#26-classes)
    7. [Functions](#27-functions)
    8. [General](#28-general)
    10. [Formatting](#210-formatting)

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


### 2.5. Mixins
Use Mixins with caution in order to maintain code readability.

### 2.6. Unit Tests
We assume that C++ portions of OpenStudio are sufficiently tested using the C++ unit tests. Therefore, we do not require that all tests be duplicated for Ruby. However, we do encourage some testing of the Ruby extensions, particularly in areas where Swig does something novel to the exported classes (e.g. changes a name, maps types, etc). Pure Ruby libraries should be tested completely in Ruby. These tests are then ported to C++ unit tests when the functionality is added to the C++ code base.

### 2.7. Indentation and Wrapping
We standardize on the following formatting conventions to improve code readability:

1. Wrap lines at 100 columns. If a line needs to be split, then the split should occur at some functional location (e.g., before/after the operator) and not just after the 100<sup>th</sup> character.
2. Tab character is two spaces

### 2.8. Comments
Documentation is an important part of any source code. Even the most well written code is hard to understand or maintain if it is not properly commented. Comments should be made in RDoc format for documentation generation. The developer is encouraged to insert as many comments as needed to explain the code, not just the minimum required.

#### 2.8.1. Documentation
