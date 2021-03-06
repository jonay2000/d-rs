
`d` stands for `data`. `d-rs` is a combination of features from grep, awk
sed, and other unix tools, to easily edit piped data.

## How to use

Let's say a file exists with the following contents:

```
# Hours

x: 3 hours
y: 3.5 hours
z: 15 hours
w: 1.5 hours
```

You can use d to find how many hours there are in total with:

```
cat hours.txt | d f float | d r sum
```
Gives 23.

So what happened here?

d has 4 main subcommands
* filter (or find, it's pretty much the same operation for d)
* map
* reduce
* split

Each of the commands can be abbreviated (by `f`, `m`, `r` or `s` respectively).

So what happened in the example? first we `f`ind all the floats, then we `r`educe
using the `sum` operator.

In general, you can 
* find things using custom or a number of built-in regexes
* map things using custom or a number of built-in regexes, or a python expression (more may come)
* reduce things using the sum, product or join operators (more may come)
* split things based on a single character or word (no regexes supported yet)

## python mapping

using `d m p` (d map python) you can tell d to run a line of python
for every line in the input. Your line will be ran in a context where:
* There is an `i` or `inp` variable available which contains the current line
* There is an `o` or `out` variable which when written to becomes the result of the expression (using `__repr__` to convert it to a string)
* Alternatively, you can print the result of your expression. If you do, the values in `o`/`out` are ignored, to prevent multiple outputs from the expression.

No state is kept between mapping lines.

# TODO list
* more built-in regexes
* finding commonly used units (for example, disk sizes in the format `500KiB`) and automatically convert to their base units (`500Kib` --> `512000`)
* built-in n-to-m base conversion
