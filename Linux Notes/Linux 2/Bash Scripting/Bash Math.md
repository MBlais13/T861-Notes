#bash 

surrounding math inside of `$(())` will evaluate values in bash
```bash
echo $((4+2)) #6  addition
echo $((4-2)) #2  subtraction
echo $((4*2)) #8  multiplication
echo $((4/2)) #2  division
echo $((4%2)) #0  modulo
echo $((4**2)) #16  exponents
```

* To generate a random number in bash you can use $RANDOM , it is a variable that will return a random number

* To specify a range you have to do some arithmetic operations

* `$(($RANDOM%10+1))` a random number between 1 and 10, use modulus division by your range size, and had your minimum value

* `$(($RANDOM%11+10))` a random number between 10 and 20