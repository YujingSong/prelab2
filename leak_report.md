# Leak report

The leaking problem is because there is a function called strip(), it has a char array called result with allocating (size-num_spaces+1) characters but are never freed.

But we cannot free result in the function of strip(), because other functions need to use the return value of funtion strip().  Therefore, we free it when other function already used the returned result.

We noticed that function is_clean() is the last function that use the unfreed result, and function is_clean() saved the reasult in a new char array called cleaned.  So when cleaned is not empty, we should free it before return the result.


