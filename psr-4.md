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

- **class**: The term _class_ refers to PHP classes, interfaces, traits, and
  similar future resource definitions.

- **namespace**: A PHP namespace, as is syntactically valid after the
  [PHP `namespace` keyword](http://www.php.net/manual/en/language.namespaces.definition.php).
  `\` by itself is not an acceptable _namespace_ within this PSR.

- **namespace separator**: The PHP namespace separator symbol `\` (backslash).

- **fully qualified class name**: A full namespace and class name, such as
  `\Acme\Log\Writer\FileWriter`. As defined by
  [PHP's name resolution rules](http://php.net/manual/en/language.namespaces.rules.php),
  the _fully qualified class name_ MUST include the leading namespace
  separator.

- **autoloadable class**: Any class in the library intended for autoloading.  
  (Classes not intended for autoloading are not covered by this term.)

- **autoloadable class name**: The same as the fully qualified class name,
  but without a leading namespace separator.  
  Given a _fully qualified class name_ of `\Acme\Log\Writer\FileWriter`,
  the _autoloadable class name_ is `Acme\Log\Writer\FileWriter`.
  Typically, this is the value sent to the [__autoload()][] function
  and to callbacks registered with [spl_autoload_register()][].

- **terminated namespace name:** A namespace with an appended namespace separator.  
  Example: `Acme\Log\Formatter\` is the terminated namespace name of `Acme\Log\Formatter`.

- **namespace prefix:** Any prefix of an autoloadable class name that is a terminated namespace name.  
  Example: Given an _autoloadable class name_ of `Acme\Log\Writer\FileWriter`,
  the _namespace prefixes_ may be `Acme\`, `Acme\Log\`, and `Acme\Log\Writer\`.

- **class file:** For a given class, a "class file" is a file that, if included by a PHP script, will make this class available.

- **class file path:** For a given class file, this is the path to that file relative to the library root.
  Example: `src/Formatter/LineFormatter.php`

- **directory path:** Given a directory within the library, this is the path to that directory relative to the library root, without a trailing directory separator.

- **terminated directory path:** Directory path, as above, but with a trailing directory separator. Only the library root is specified as an empty string, without a trailing directory separator.  
  Example: `src/Formatter/`.

- **directory prefix:** Any prefix of a file or directory path that is a terminated directory path.

- **relative class name:** For a class and one of its namespace prefixes, the relative class name
  (relative to that namespaceprefix ) is the part of the autoloadable class name that follows
  the namespace prefix.  
  Example: For a class `Acme\Log\Formatter\LineFormatter` and the namespace prefix `Acme\Log\`,
  the relative class name is `Formatter\LineFormatter`.

- **relative file path:** For a file and one of its directory prefixes, the relative file path
  (relative to that directory) is the part of the file path that follows the terminated
  directory path.  
  Example: For a file `src/Formatter/LineFormatter.php` and a directory prefix `src/`,
  the relative file path is `Formatter/LineFormatter.php`.

- **Namespace Depth:** The "depth" of a namespace is the number of namespace separators in the terminated namespace name.  
  Example: The namespace with the terminated name of `Acme\Log\Formatter\` has a depth of 3.


3. Specification
--------------------

1. Every class MUST be in a namespace of at least depth one.

2. Every class SHOULD be in a namespace of at least depth two.

3. A class SHOULD be defined in or made available through a class file.

4. The library MUST specify a relationship that associates terminated namespace names
   with terminated directory paths,  
   OR it MUST make it possible to determine such a relationship.

5. For every class with a class file, the following MUST be true:
   * One of the namespace prefixes of the class is associated with one of the directory prefixes of the class file, via the above relationship.
   * The relative file path (relative to the directory) can be obtained from the relative class name (relative to the namespace), by replacing every namespace separator with a directory separator, and appending the ".php" suffix.



4. Notes
-------------------------------

Needs work!


5. Examples
---------------------------------
