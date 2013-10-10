Definitions
===========

**Library:** A collection of PHP files (and possibly other files) in a directory structure. 
Note: A larger project composed of multiple libraries may again be regarded as a library by itself.

**Class:** The term "class" refers to PHP classes, interfaces, and traits.  
Note: We assume that every such class has a valid PHP class name.

**Fully Qualified Class Name:** The full namespace and class name of a class, without a leading namespace separator.
Example: `Acme\Log\Formatter\LineFormatter`.

**Root namespace:** The PHP namespace that is the parent of all other PHP namespaces, and that in PHP is specified by `\` (a single namespace separator).

**Terminated Namespace Name:** The string representing a full PHP namespace, without a leading namespace separator, but with a trailing namespace separator. Only the root namespace is specified as an empty string, without a trailing namespace separator.  
Example 1: `Acme\Log\Formatter\` is the terminated namespace name of `Acme\Log\Formatter`.

**Class File:** For a given class, a "class file" is a file that, if included by a PHP script, will make this class available.

**Class File path:** For a given class file, this is the path to that file relative to the library root.
Example: `src/Formatter/LineFormatter.php`

**Directory Path:** Given a directory within the library, this is the path to that directory relative to the library root, without a trailing directory separator.

**Terminated Directory Path:** Directory path, as above, but with a trailing directory separator. Only the library root is specified as an empty string, without a trailing directory separator.  
Example: `src/Formatter/`.

**"under" a namespace:** A class or namespace is "under" another namespace, if it has the terminated namespace name of that other namespace as a prefix.  
A namespace is NOT "under" _itself_.  
Note: In other words, the other namespace as a direct or indirect "parent".  
Note: Every namespace is under the root namespace, except for the root namespace itself.

**"under" a directory:** A file or directory is "under" another directory, if it has the terminated directory path of that other directory as a prefix.
A directory is NOT "under" _itself_.  
Note: In other words, the other directory as a direct or indirect "parent".  
Note: Every library directory is "under" the library root, except the library root itself.

**namespace depth:** The depth of a namespace is the number of parent namespaces it is "under".  
Example: The depth of namespace `Acme\Log\Formatter\` is three.


Specification
=============

1. A class MUST be "under" a namespace with a depth of one.

2. A class SHOULD be "under" a namespace with a depth of two.

3. A class SHOULD be defined in or made available through a class file.

4. The library MUST specify a relationship that associates PHP namespaces with directory paths.
  * It is recommended, but not required, that this be a 1:1 relationship.
  * It is recommended, but not required, to specify the relationship in a machine-readable and commonly-understood format.

5. For every class that is made available through a class file, there MUST be a namespace associated with a library directory, where:
  * The terminated namespace name is a prefix of the fully qualified class name.
  * The terminated directory path is a prefix of the class file path.
  * The remaining part of the class file path can be obtained from the remaining part of the fully qualified class name, by replacing every namespace separator with a directory separator, and appending the ".php" suffix.

