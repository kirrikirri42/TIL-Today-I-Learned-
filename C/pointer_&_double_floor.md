TIL-Today-I-Learned 20200515(Fri)

Output is a two-dimensional string array and I received the address of output[i] in another function.

`void    inputmalloc(char **output, char *str)`
The `output` input is `&output[i]` in another function.
In this inputmalloc function I wrote as follows `*output[i]` at first.
But I realized that it should be `(*output)[i]`
because what I'm looking at is the ith element of what output is pointing at.
Not what the ith element of output is pointing at.


---

The and operator in c can be represented either by `&&` or `&`. Both works fine.

---

`0.` means `0.0` showing that it's a double, not an integer.
When I printed it with `%lf` and `%f`, I got 0.000000 in both cases.
Not sure yet though.

---

floor(x) means the largest integer smaller or equal to x.

