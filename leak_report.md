# Leak report

There are two types of error you (as the grader) are likely to see.  The first arises from the original C file when valgrind is run on the executable

** add error messages** (I'll let you add these Sophia since I am lazy **and** have already generated the solution... thanks)

Fixing that requires `freeing` the allcoated memory (I did it outside of the function `strip`.  The pointer *cleaned refers to this "problem area", and this is what should be cleaned using `free(cleaneed)`.  However... that alone will not remove all errors.  The program will also generate an error for an invalid `free`.  This is because if the function `strip` encounters a string purely of whitepace, then it will return an empty string whose memory was **not reserved using calloc**.  Instead, as is the C-way, any constant strings are pre-allocated.  Trying to free such a memory address does not generate an error during execution, but does raise a red-flag when valgrind is run correctly... That's why the `free(cleaned);` line should be in an `if` statment that checks the size of string cleaned.
