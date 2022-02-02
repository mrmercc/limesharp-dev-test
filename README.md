# Limesharp Developer Test

Hi, 
As mentioned in main-repo (https://github.com/limesharp/Developer-Test) I've completed the tests 
both in JavaScript and PHP. Below you will see tasks and solutions in both languages.

### **Task 1** 
Make this work (repeat 3 times the contents of an array):

    repeat([1,2,3]) //[1,2,3,1,2,3,1,2,3]

**Solution**

**Explanation:** I wrote a function that takes iteration count as parameter (3 by default as requested in the task). First I check variable type and show error in console if something else is passed as variable rather than array. In modern solution I flatten the array first and then create new array that fills array in arguments and flatten it again. 

In pre-es6 solution, I've created an empty array first and then pushed passed array in argument in for loop. After that I called `concat` function to merge arrays and returned it.

#####  Javascript (*Modern Way*)
```javascript
let testArray1 = ['a', 'b', 'c', 'x', 'u'];
let testArray2 = [1, 2, 3, 4, 5, 6];

function repeat(items, iterationCount = 3) {
   if (!Array.isArray(items)) throw new Error('Please provide an array!');
   items = items.flat();
   return Array(iterationCount).fill(items).flat();
}

// Tests

console.log(repeat(testArray1)); // output --> ["a", "b", "c", "x", "u", "a", "b", "c", "x", "u", "a", "b", "c", "x", "u"]
console.log(repeat(testArray2, 4)); // output -> [1, 2, 3, 4, 5, 6, 1, 2, 3, 4, 5, 6, 1, 2, 3, 4, 5, 6]
```
#####  Javascript (*Pre-ES Way*)

```javascript
let testArray1 = ['a', 'b', 'c', 'x', 'u'];
let testArray2 = [1, 2, 3, 4, 5, 6];

function repeatItems(items, iterationCount = 3) {
   if (!Array.isArray(items)) throw new Error('please provide an array!');
   var repeat = [];
   for (let i = 0; i < iterationCount; i++) {
      repeat.push(items);
   }
   return (repeat = [].concat.apply([], repeat));
 }
 
 // Tests

console.log(repeat(testArray1)); // output --> ["a", "b", "c", "x", "u", "a", "b", "c", "x", "u", "a", "b", "c", "x", "u"]
console.log(repeat(testArray2, 4)); // output -> [1, 2, 3, 4, 5, 6, 1, 2, 3, 4, 5, 6, 1, 2, 3, 4, 5, 6]
```
#### PHP

```php
$testArray1 = [1,2,3];
$testArray2 = ['x', 'y', 'z'];

function repeat($items, $iterationCount = 3) {
   if( !is_array($items) ) throw new Exception('Please provide an array!');
   $repeat = [];
   for( $i=0; $i < $iterationCount; $i++ ) {
      array_push($repeat, $items);
   }
   return array_merge(...$repeat);
}

// tests
print_r(repeatArrayItems($testArray1)) ;

/* Output;
(
    [0] => 1
    [1] => 2
    [2] => 3
    [3] => 1
    [4] => 2
    [5] => 3
    [6] => 1
    [7] => 2
    [8] => 3
)
*/
```


------------

### **Task 2** 

Make this work (no vowels, lowercase except the first letter):


    reformat("liMeSHArp DeveLoper TEST")
	

"If we type in our console your function and reformat("liMeSHArp DeveLoper TEST") then the result should be Lmshrp dvlpr tst"


**Solution**

**Explanation:** In this function, after type checking first, I wrote RegEx (Regular Expression) to match all vowels in sentence whether it's uppercase or not, and replaced them with empty string and returned lowercase version of given sentence. I sliced first character and joined rest of the sentence with slice function. The `charAt(0)` function returns only given character so I've used it to take first char of the sentence. And then I got rest of the sentence with `slice(1)` function and merged whatever returned from `charAt(0)` and `slice(1)` and returned that in the function. This function works both in modern and old browsers.


#####  Javascript

```javascript
let testString = 'liMeSHArp DeveLoper TEST';
let anotherString = 'In the SEARCH OF INcreDIBle';

function reformat(word) {
   if (typeof word !== 'string') throw new Error('Please enter valid string');
   let pattern = /[aeiou]/gi // g: for all matches, i: case-insensitive
   word = word.replace(pattern, '').toLowerCase();
   word = word.charAt(0).toUpperCase() + word.slice(1);
   return word;
}

// tests 

console.log(reformat(testString));		 // output --> Lmshrp dvlpr tst
console.log(reformat(anotherString));  // output --> N th srch f ncrdbl

```

#####  PHP

```php

$testString = 'liMeSHArp DeveLoper TEST';
$anotherTestString = 'In the SEARCH OF INcreDIBle';

function reformat($sentence) {
   $pattern = "/[aeiou]/i";
   $replace = '';
   return ucfirst(strtolower(preg_replace($pattern, $replace, $sentence)));
}

// tests

echo reformat($testString); // output --> Lmshrp dvlpr tst
echo reformat($anotherTestString); // output --> N th srch f ncrdbl
```
