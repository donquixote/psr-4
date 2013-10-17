PSR-4: Organization of class files.
====================================

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).


1. Overview
--------------------

The following describes how to organize PHP class files in a directory structure ("library").

The benefit of following these requirements are:
* Making it easy for a (human) reader to find where a specific class is defined.
* Making the classes easy to load with a compliant autoloader.


2. Definitions
--------------------

- **Library:** The subject that this specification should apply to:
  * A collection of PHP files (and possibly other files) in a directory structure, or a subset of these files.
  * The PHP classes that are defined in or provided by this library, or those of these PHP classes that should be subject to this spec.
  * Optionally, documentation and meta information that belongs to the library, but might not be part of the directory structure.
  
  Note: A larger project composed of multiple libraries may again be regarded as a library by itself, and be subject to this spec.

- **Class:** The term "class" refers to PHP classes, interfaces, and traits.  
  Note: We assume that every such class has a valid PHP class name.

- **Fully Qualified Class Name:** The full namespace and class name of a class, without a leading namespace separator.
  Example: `Acme\Log\Formatter\LineFormatter`.

- **Root namespace:** The PHP namespace that is the parent of all other PHP namespaces, and that in PHP is specified by `\` (a single namespace separator).

- **Terminated Namespace Name:** The string representing a full PHP namespace, without a leading namespace separator, but with a trailing namespace separator. Only the root namespace is specified as an empty string, without a trailing namespace separator.  
  Example 1: `Acme\Log\Formatter\` is the terminated namespace name of `Acme\Log\Formatter`.

- **Class File:** For a given class, a "class file" is a file that, if included by a PHP script, will make this class available.

- **Class File path:** For a given class file, this is the path to that file relative to the library root.
  Example: `src/Formatter/LineFormatter.php`

- **Directory Path:** Given a directory within the library, this is the path to that directory relative to the library root, without a trailing directory separator.

- **Terminated Directory Path:** Directory path, as above, but with a trailing directory separator. Only the library root is specified as an empty string, without a trailing directory separator.  
  Example: `src/Formatter/`.

- **"under" a namespace:** A class or namespace is "under" another namespace, if it has the terminated namespace name of that other namespace as a prefix.  
  A namespace is NOT "under" _itself_.  
  Note: In other words, the other namespace is a direct or indirect "parent".  
  Note: Every namespace is "under" the root namespace, except for the root namespace itself.

- **"under" a directory:** A file or directory is "under" another directory, if it has the terminated directory path of that other directory as a prefix.
  A directory is NOT "under" _itself_.  
  Note: In other words, the other directory is a direct or indirect "parent".  
  Note: Every library directory is "under" the library root, except the library root itself.

- **Relative Class Name:** For a class that is "under" a namespace, the relative class name (relative to that namespace) is the part of the fully qualified class name that follows the terminated namespace name.  
  Example: For a class `Acme\Log\Formatter\LineFormatter` being "under" the namespace `Acme\Log\`, the relative class name is `Formatter\LineFormatter`.

- **Relative File Path:** For a file that is "under" a directory, the relative file path (relative to that directory) is the part of the file path that follows the terminated directory path.  
  Example: For a file `src/Formatter/LineFormatter.php` being "under" the directory `src/`, the relative file path is `Formatter/LineFormatter.php`.

- **Namespace Depth:** The "depth" of a namespace is the number of parent namespaces it is "under".  
  Example: The namespace `Acme\Log\Formatter\` has a depth of 3.


3. Specification
--------------------

1. A class MUST be "under" a namespace with a depth of one (or more).

2. A class SHOULD be "under" a namespace with a depth of two (or more).

3. A class SHOULD be defined in or made available through a class file.

4. The library MUST specify a relationship that associates PHP namespaces with directory paths,  
  OR it MUST make it possible to determine such a relationship.

5. A class file for a class may exist ONLY IF
  * One of the namespaces the class is "under" is associated with one of the directories the class file is "under", via the above relationship.
  * The relative file path (relative to the directory) can be obtained from the relative class name (relative to the namespace), by replacing every namespace separator with a directory separator, and appending the ".php" suffix.

