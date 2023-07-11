# Java Objects to JSON Conversion

1. Problem Summary
  - (1) Convert Java objects into JSON representation object (2) Convert JSON object into string output
  - For more details, see 'JsonExercise.txt' file

2. Observations
  - JSON standard (https://www.json.org/json-en.html)
    - Two structures: 
      - Objects ('string:value' pairs, unordered, can be nested)
      - Arrays (list of values, ordered, can be nested).
    - Value types
      - string (double quotes)
      - number
      - true
      - false
      - null
      - Another object or an array
  - Java 
    - 8 Primitive types:
		  - byte
		  - char
		  - short
		  - int
		  - float
		  - long
		  - double
		  - boolean
    - Objects/reference types:
      - 'String' handling
        - In Java, a 'string' is an immutable class object. i.e. its state does not change.
        - String values are stored in a 'string constant pool'. Implication:
        ```
            String s3 = "hi";
            String s4 = "hi"; 
            // s4 ref is the same as s3; 
            // JVM checks string constant pool to see if object with this value exists; if so, then that object ref is assigned to s4.
        ```
      - Arrays/collections framework: They are just objects.
      - Null
        - Arises when a variable does not have a value assigned to it. (Hence why it is called NullPointerException; the variable is not pointing to any object in the heap.)
        - Null represents absence of a value. It is not the same as an empty string or an empty array.
  - My proposed Java implementation of JSON standard:
    - The following points outline my observations of equivalence between Java and JSON standard.
    - Representing values:
      - Java Object 'attribute name:attribute value' can represent JSON 'name:value' pairs.
    - Representing structures:
      - Depends on (1) the position of the object within the object graph (2) the number of attributes the object possesses. See 'Classification' section below for more details.
    - Possible structural combinations:
    ```
      { }

      [ ] / [ primitive/structure, primitive/structure etc ]
      
      { string: primitive }

      { string: structure }
    ```
    
    - Data type equivalence (Java attribute type(s): JSON type)
      	- byte, short, int, float, long, double: number
        - char: string
		    - boolean: true, false
        - Non-initialised attribute/attribute that is only declared: null
        - String: string
        - Java Object: See 'Classification' section below for more details.
    - Array ordering
      - If Java Object is array/collection: Preserve index order.
      - If Java Object attributes are all primitive types: JSON array index order goes from first declared attribute to last.

3. Implementation
  - The following concepts are used:
    - Generic tree (arbitrary number of children)

    - Pointers

    - Recursion

  - Classification:
    - If root node object consist of none or one attribute, it is an array [].
    - If root node object consist of more than one attribute, it is an object {}.
    - If child node object consist of no attributes, it is a null value and a leaf node.
    - If child node object consist of one attribute, AND the attribute type is a primitive or null, it is a value and a leaf node.
    - If child node object consist of one attribute, AND the attribute type is an object, it is an array [].
    - If child node object consist of more than one attribute, AND all attribute types are primitives or null, it is an an array [] and a leaf node.
    - If child node object consist of more than one attribute, BUT NOT all attribute types are primitives or null, it is an object {}.

4. Evaluation
  - JSON edge cases
    - Array of arrays
    - Null values
    - Empty object
    - Empty array
    - Repeated key
  - Alternative ways to classification
  - Alternative to tree representation

5. Resources
  - JSON linting: https://jsonlint.com/
  - JSON standard: https://www.json.org/json-en.html
