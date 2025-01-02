# R Questions

## Question 1
Predict the output of the following code:

```R
numbers <- 1:5
squared_numbers <- numbers^2
cat("Length of squared_numbers:", length(squared_numbers), "\n")
print(squared_numbers)
```

## Question 2
You are provided the following R code for some analysis involving simple matrix multiplication:
```R
print(class(matrix_data))
print(length(matrix_data))
print(class(matrix_data[[1]]))

weights = c(1.23, 2.34, 5.43, 0.98)

results = sapply(1:length(matrix_data), function(x) {
	sum(matrix_data[[x]] * weights[[x]])
})
print(results)
```
You run the above code and get the following output
```R
[1] "list"
[1] 4
[1] "matrix"
[1]        NA -3.780217        NA  3.046643
```

You were told by your colleague that `matrix_data` is a list of 4 matrices and these needs to be multiplied by specific sets of weight values, provided as the `weights` variable. Checking the class and length of `matrix_data` shows that it is as your colleague described.
But you get some `NA` values in your results when you expected 4 .

- What steps would you take to troubleshoot this issue?
- What could be the reason some of the outputs are returning `NA` values?


## Question 3
You encounter the following directory structure:

```bash
# .
# ├── mypackage/
# │   ├── R/
# │   │   └── functions.R
# │   ├── DESCRIPTION
# │   ├── NAMESPACE
```

What is the purpose of the DESCRIPTION file in an R package?
What would you include in the NAMESPACE file to export a function named `my_function` from `functions.R`?

## Question 4
You are provided the following `data.table`:
```R
dt <- data.table(group = c("A", "A", "B", "B"), value = c(10, 20, 30, 40))
print(dt)
```

```less
    group value
   <char> <num>
1:      A    10
2:      A    20
3:      B    30
4:      B    40
```
You are tasked to create a new column which has the value of a running cumulative `value` by `group`.  
Essentially, you are to a create the following `data.table`:

```less
    group value running_total
   <char> <num>         <num>
1:      A    10            10
2:      A    20            30
3:      B    30            30
4:      B    40            70
```

How can you achieve with as little code as possible?