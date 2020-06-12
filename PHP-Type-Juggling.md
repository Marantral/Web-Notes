# PHP Type Juggling

## Equal vs Identical
In php there is a big difference between "==" (Equal or called "Loose Comparison")  and "===" (Identical or called "Strict Comparisons"). Equal will check to see if the  variables are equal to each other after type juggling occurs. Where Identical checks to see if the variables are equal and are the same type.
#### Example of Loose Comparison
   php > var_dump('0' == 0); </br>
   bool(true) </br> 
   Notes: This is true because type juggling changed the string 0 to the integer of zero and they are equal.

#### Example of Strict Comparison
   php > var_dump('0' === 0); </br>
   bool(false) </br>
   Notes: This is false because they have two different types. One being a string and one being an  integer. That means it will not be identical or it is false. 

## Types
#### String 
Any string of characters, specified by single quotes, double quotes, heredoc syntax, or nowdoc syntax. 
 - single quote: </br>
    $string = 'This is the string' </br>
 - double quote: </br>
    $string = "This is the string" </br>
 - heredoc syntax: </br>
    $string = <<<EOT </br>
    This is the string </br>
    EOT; </br>
 - nowdoc syntax: </br>
    $string = <<<'EOT' </br>
    This is the string </br>
    EOT;</br>
 
 #### Integer
 An integer is a number on the number line (-2, -1, 0, 1, 2,). They can be decimal, octal, hexadecimal, binary, or _ decimal (as of PHP 7.4.0) numbers.
     
 ##### Float 
 Floats or "real numbers" are numbers with the below syn taxes </br> 
        $a = 1.234; </br>
        $b = 1.2e3; </br>
        $c = 7E-10; </br>
        $d = 1_234.567; // as of PHP 7.4.0 </br>

## PHP Type Juggling 
PHP does not support explicit type definition in variable declarations. This means that type is decided based on the context in which the variable is used. 
    
       $foo = "1";  // $foo is string (ASCII 49)
       $foo *= 2;   // $foo is now an integer (2)
       $foo = $foo * 1.3;  // $foo is now a float (2.6)
       $foo = 5 * "10 Little Piggies"; // $foo is integer (50)
       $foo = 5 * "10 Small Pigs";     // $foo is integer (50)
  
## Magic Hash -- 
"e" is a numerical constant and it equals 2.71828. when you have a hash like 1e1 this would equal 10 or 1 and 1 zero. likewise if you had a 5e10 it would be a 5 and 10 zeros.

   php > var_dump(5e10 == 50000000000); </br>
   bool(true)   </br>
   Notes: with type juggling we are assuming that the hash or string is represented as a string, however in php the type is determined by the context in which the variable is used.

   php > var_dump('5e10qwe' == 50000000000);  </br>
   bool(true)  </br>
   php > var_dump('5e10qwe' == '50000000000');  </br>
   bool(false)  </br>
   
   As we can see when the string is compared with an integer the string is treated like an integer. 
   This means that if a hash has 0e123 it will = 0   </br>
   Note: This will more likely happen in MD5 and SHA1 hash values


## What does all of this mean for us?
If they are using Equals in PHP and we have access to the comparison variables then we could potentially subvert the intended operations.
