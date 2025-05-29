In Bash, you can get the length of an array using the syntax `${#array_name[@]}`. Here’s how you can do it:

1. First, define your array.
2. Then, use the length syntax to get the number of elements in the array.

Here’s an example:

```bash
# Define an array
my_array=(apple banana cherry)

# Get the length of the array
length=${#my_array[@]}

# Print the length
echo "The length of the array is: $length"
```

In this example, the output will be:

```
The length of the array is: 3
``` 

This method works for both indexed and associative arrays in Bash.