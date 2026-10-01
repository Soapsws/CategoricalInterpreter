Data Types / Objects
    // using 'd' as prefix to not be confused with Haskell primitive types
    dint
    dfloat
    dbool
    dstr
    Matrix
    Set
    Map
    Function

Operators
    = : assignment operator
    == : comparison operator, compares by value
    + : performs calculations between numerical types (automatic conversion to the stronger type if necessary)
        appends strings 
    -, *, / : performs calculations between numerical types (automatic conversion to the stronger type if necessary) 
    OR, AND : compares booleans
    ^ : composes functions

Variables
    defined using var.{type} {name} = {initial value};
    for example, var.dint my_integer = 5;

Special Lexical Tokens
    ; : end of line 
    ( ) : priority delimiter

Initialization Syntax for Objects
    // default values are initialized to 0 (for dint, dfloat), false (for dbool), "" (for dstr), Do Nothing (for Function), Matrix,
    // Set, Map are composed of primitive types
    Matrix: var.Matrix {name} = ({primitive_type}, {length}, {width}) | Fixed Size
    Set: var.Set {name} = ({primitive_type}, {initial size}) | Dynamic Size
    Map: var.Map {name} = ({primitive_type}, {initial size}) | Dynamic Size
    Function: var.Function {name} = (
        ({parameter1 type} {parameter1 name}, {parameter2 type parameter2 name}, ...)
        ( {return type {}})
        ( {body} ) // must include "return" keyword
    )

Object Functionality

    // for now, Matrices, Sets, and Maps can only contain primitive types.
    // as I further explore the composable nature of Haskell and its inspiration in category theory,
    // I might make objects composable amongst each other

    Matrix : assume we have a Matrix m
        m.ins({row}, {column}, {value})
        primitive_type m.get({row}, {column})

    Set : assume we have a Set s
        dbool s.ins({value})
        dbool s.contains({value})
        dbool s.rem({value})
    
    Map : assume we have a Map m
        dbool m.ins({key}, {value}) // overwrites value if pre-existing
        dbool m.contains({key})
        dbool m.rem({key})
        primitive_type m.get({key})

    Function : assume we have a Function fn
        primitive_type fn.run({arguments});
        // edit cannot modify parameters or return type
        dbool fn.edit(
            {body}
        )


Input/Output
    din {file}: inputs file
    dout {string}: outputs value of dstr variable

