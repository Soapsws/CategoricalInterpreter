This page contains AI-generated sample dummylang code for reference.
I've added brief captions (indicated by //) to explain functionality.

# Example 1: Basic arithmetic

```text
var.dint x = 5;
var.dfloat y = 2.5;

var.dfloat result = x + y;

dout "result";

// dfloat has casting priority over dint, so the result is 7.5
```

# Example 2: Strings

```text
var.dstr first = "Hello, ";
var.dstr second = "world";

var.dstr message = first + second;

dout "message";

// dummylang supports string concatenation with '+', so the message is "Hello, world"
```

# Example 3: Boolean logic

```text
var.dbool a = true;
var.dbool b = false;

var.dbool result = a AND b;

dout "result";

// as per universal logic rules, true AND false returns false
```

# Example 4: Matrix

```text
var.Matrix m = (dint, 3, 3);

m.ins(0, 0, 10);
m.ins(1, 1, 20);

var.dint value = m.get(1, 1);

dout "value";

// Matrices are zero-indexed; the 1-row, 1-column element is 1.
```

# Example 5: Set

```text
var.Set numbers = (dint, 10);

numbers.ins(5);
numbers.ins(8);

var.dbool contains_five = numbers.contains(5);

dout "contains_five";

// contains_five is true, as 5 was inserted to our Set numbers. 
// note that because Sets are resizeable, initializing it with 10 length
// creates 10 indices with value 0. by the end there's 10 0's, a 5, and an 8. 
```

# Example 6: Map

```text
var.Map ages = (dint, 10);

ages.ins("Alice", 20);
ages.ins("Bob", 25);

var.dint alice_age = ages.get("Alice");

dout "alice_age";

// .get() retrieves the value the key maps to. in this case, "Alice" maps to 20.
```

# Example 7: Function

```text
var.Function add = (
    (dint x, dint y)
    (dint)
    (
        return x + y;
    )
);

var.dint result = add.run(4, 7);

dout "result";

// we declare a Function add that takes a dint and a dy - the first parentheses-bound argument
// and returns a dint - the second parentheses-bound argument. result stores the value 4 + 7 = 11.
```

# Example 8: Simple function composition

```text
var.Function double = (
    (dint x)
    (dint)
    (
        return x * 2;
    )
);

var.Function increment = (
    (dint x)
    (dint)
    (
        return x + 1;
    )
);

var.Function transform = increment ^ double;

var.dint result = transform.run(5);

dout "result";

// we declare two Functions - double and increment - which both take a dint and return a dint.
// we declare a container Function transform that composes increment and double.
// it is executed right->left, meaning:
//      the input passed into transform must match the input of double. 
//      the output of double must match the input of increment (given no other fixed arguments are required).
//      the output of increment is the output of transform.
// so transform.run(5) runs double(5) which returns 10, which is passed into increment and 10 + 1 = 11, which is the 
// ultimate output value of transform.run(5) and stored in result
```

# Example 9: Composition with a fixed argument

```text
var.Function lengthen = (
    (dstr text, dint amount)
    (dstr)
    (
        return text + amount * "!";
    )
);

var.Function make_message = (
    (dint x)
    (dstr)
    (
        return "value";
    )
);

var.Function composed = lengthen ^ (make_message, 3);

var.dstr result = composed.run(10);

// it's recommended you look at Example 8 before this, as some intuition will be reused.
// for this composition to hold, the output of each clause must match the input of the clause to its left,
// the input of the rightmost clause is supplied in the function call, and the output of the leftmost clause is the 
// container function's return.
// 
// we notice that the output of the leftmost composed function, make_message, is a dstr,
// whereas the inputs for lengthen require both a dstr and a dint, in that order.
// hence we supply the dint manually by writing the rightmost clause as a tuple of arguments.
// the value 10, supplied by composed.run(10), is automatically matched to make_message, sufficing the pattern
//
// make_message(10) casts it to "10", which is passed alongside 3 to lengthen, which appends "10"
// with three copies of "!", resulting in "10!!!".
//
// if you have multiple functions in the rightmost clause (the one that directly interacts with container function calls),
// values are matched by order of functions listed.
```

# Example 10: Chained composition

```text
var.Function square = (
    (dint x)
    (dint)
    (
        return x * x;
    )
);

var.Function double = (
    (dint x)
    (dint)
    (
        return x * 2;
    )
);

var.Function increment = (
    (dint x)
    (dint)
    (
        return x + 1;
    )
);

var.Function pipeline = increment ^ double ^ square;

var.dint result = pipeline.run(3);

dout "result";

// here our container function, pipeline is composed of three functions.
// their input-output chaining automatically sufficies the rules covered in examples
// 8 and 9, so we don't need additional fixed arguments.
// square is calculated first, the result is passed into double, that result is passed into increment,
// and finally the return of increment is propagated back as the return of pipeline itself.
// 3 is squared into 9, which is doubled into 18, which is incremented into result = 19. 
```
