# calcpw.php

Copyright (c) 2022, Yahe  
All rights reserved.

## usage

```
./calcpw.php [(--dieharder|--modulobias) <password> <information> [<characterset>]]
```

## description

This script implements the calc.pw password calculation algorithm and serves as a reference implementation. The calc.pw password calculation contains a key derivation and key expansion function that is combined with an encoding function to produce pseudorandom but reproducible passwords from a secret password and a service-dependent information.

The password calculation can be modified by prepending trigger flags to the information value:

* `#` : the hash sign triggers the querying of a modified password length, the password must not be longer than 1024 characters, the limit has been introduced as the password calculation is meant to be implemented on a microcontroller later on which will have memory constraints

* `*` : the star sign triggers the querying of a modified character set, the character set defines which characters may occur in the calculated password, the character set consists of one ore more character groups which are split by spaces, character groups are relevant for the enforcement mode, to simplify the definition of the character set it is possible to define ranges from a first character to a last character by using a minus sign (e.g. `0-9` or `A-Z` or `a-z`)

* `!` : the exclamation sign activates the enforcement mode, the enforcement mode makes sure that at least one character from each character group is contained within the calculated password, the password calculation will continue until a valid password has been calculated

When no trigger flag is provided then senseful defaults are used.

## execution

To execute the script you have to call it in the following way:

```
./calcpw.php [(--dieharder|--modulobias) <password> <information> [<characterset>]]
```

* `--dieharder` : (OPTIONAL) to test the strength of the random number generator the script supports a way to output raw pseudorandom data to STDOUT which can then be used by dieharder, when the dieharder mode is used, the parameters `<password>` and `<information>` must be provided as well

* `--modulobias` : (OPTIONAL) the test the resistance of the password encoding against modulo bias the script supports a way to output encoded psuedorandom data to STDOUT which can then be used by a modulo bias test, when the modulo bias mode is used, the parameters `<password>` and `<information>` must be provided as well while the parameter `<characterset>` may be provided as well

* `<password>` : (OPTIONAL) when the dieharder or modulo bias mode is used then the information must be provided

* `<information>` : (OPTIONAL) when the dieharder or modulo bias mode is used then the information must be provided

* `<characterset>` : (OPTIONAL) when the modulo bias mode is used then the character set parameter may be provided

When no parameter is provided then the interactive mode of the script is triggered.