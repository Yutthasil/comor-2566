# Basic of Shell Script
### Create file Shell script
```
touch hello_world.sh
```

### Find the path to your bash shell.
```
which bash
```
In my case, the path is ` /usr/bin/bash ` and I will include this in the shebang.

### Write the command.
```
echo "Hello World"
```
Edit the file hello_world.sh using a text editor of your choice and add the above lines in it.

### Provide execution rights to your user.
```
chmod u+x hello_world.sh
```
`chmod` modifies the existing rights of a file for a particular user. We are adding `+x` to user u.

### Run the script.
You can run the script in the following ways:
```
./hello_world.sh
bash hello_world.sh
```

## The Basic Syntax of Bash Scripting
Just like any other programming language, bash scripting follows a set of rules to create programs understandable by the computer. In this section, we will study the syntax of bash scripting.

### How to define variables
We can define a variable by using the syntax `variable_name=value`. To get the value of the variable, add `$` before the variable.
```
greeting=Hello
name=Tux
echo $greeting $name
```

### Arithmetic Expressions
Below are the operators supported by bash for mathematical calculations:

|OPERATOR | USAGE 
|-------- | ------
|+        | addition
|-        | subtruction
| *	       | multiplication
| /	       | division
| **       |	exponentiation
| %	      | modulus

<b>Examples >>> </b>
```
expr 10 + 10000
expr 30 / 2
```
Numerical expressions can also be calculated and stored in a variable using the syntax below:
```
var=$((expression))
```
<b>Example >>> </b>
```
var=$((3+9))
echo $var
```
Fractions are not correctly calculated using the above methods and truncated. <br>
For decimal calculations, we can use bc command to get the output to a particular number of decimal places. bc (Bash Calculator) is a command line calculator that supports calculation up to a certain number of decimal points. 
```
echo "scale=2;22/7" | bc
```
Where `scale` defines the number of decimal places required in the output.

### How to read user input
Sometimes you'll need to gather user input and perform relevant operations. <br>
In bash, we can take user input using the `read` command.
```
read variable_name
```
To prompt the user with a custom message, use the `-p` flag.
<b>Example >>> </b>
```
echo "Enter a numner"
read a

echo "Enter a numner"
read b

var=$((a+b))
echo $var
```

### Numeric Comparison logical operators
Comparison is used to check if statements evaluate to `true` or `false`. We can use the below shown operators to compare two statements:

OPERATION |	SYNTAX |	EXPLANATION
--------- | ------ | --------------
Equality |	num1 -eq num2	| is num1 equal to num2
Greater than equal to |	num1 -ge num2	| is num1 greater than equal to num2
Greater than|	num1 -gt num2 |	is num1 greater than num2
Less than equal to |	num1 -le num2 |	is num1 less than equal to num2
Less than |	num1 -lt num2 |	is num1 less than num2
Not Equal to |	num1 -ne num2 |	is num1 not equal to num2

#### Syntax:
```
if [ conditions ]
    then
         commands
fi
```
<b>Example >>> </b>
```
read x
read y

if [ $x -gt $y ]
then
echo X is greater than Y
elif [ $x -lt $y ]
then
echo X is less than Y
elif [ $x -eq $y ]
then
echo X is equal to Y
fi
```

## Conditional Statements (Decision Making)
Conditions are expressions that evaluate to a boolean expression (true or false). To check conditions, we can use if, if-else, if-elif-else and nested conditionals.

The structure of conditional statements is as follows: <br>

* `if...then...fi` statements
* `if...then...else...fi` statements
* `if..elif..else..fi`
* `if..then..else..if..then..fi..fi..` (Nested Conditionals)

Syntax: <br>

```
if [[ condition ]]
then
	statement
elif [[ condition ]]; then
	statement 
else
	do this by default
fi
```

To create meaningful comparisons, we can use AND `-a` and OR `-o` as well.

The below statement translates to: If `a` is greater than 40 and b is less than 6. <br>
`if [ $a -gt 40 -a $b -lt 6 ]` <br>

<b>Example >>> </b>
```
read a
read b
read c

if [ $a == $b -a $b == $c -a $a == $c ]
then
echo EQUILATERAL

elif [ $a == $b -o $b == $c -o $a == $c ]
then 
echo ISOSCELES
else
echo SCALENE

fi
```
## Looping and skipping ##
For loops allow you to execute statements a specific number of times.

### Looping with numbers: ###
In the example below, the loop will iterate 5 times.

```
for i in {1..5}
do
    echo $i
done
```
### Looping with strings:
We can loop through strings as well.
```
for X in cyan magenta yellow  
do
	echo $X
done
```

### While loop
While loops check for a condition and loop until the condition remains `true`. We need to provide a counter statement that increments the counter to control loop execution. <br>

In the example below, (( i += 1 )) is the counter statement that increments the value of i.

<b>Example >>> </b>
```
i=1
while [[ $i -le 10 ]] ; do
   echo "$i"
  (( i += 1 ))
done
```

## Reading files
Suppose we have a file `sample_file.txt` as shown below:

![alt text](https://github.com/Chinjuku/Code-Development-1/blob/main/image/commandscripting.png)

```
LINE=1

while read -r CURRENT_LINE
	do
		echo "$LINE: $CURRENT_LINE"
    ((LINE++))
done < "sample_file.txt"
```

![alt text](https://github.com/Chinjuku/Code-Development-1/blob/main/image/commandscriptoutput.png)

### How to execute commands with back ticks
If you need to include the output of a complex command in your script, you can write the statement inside back ticks.

Syntax:
``` var= `commands` ```

Example: Suppose we want to get the output of a list of mountpoints with `tmpfs` in their name. We can craft a statement like this: `df -h | grep tmpfs`.

```
var=`df -h | grep tmpfs`
echo $var
```

### How to get arguments for scripts from the command line
It is possible to give arguments to the script on execution.
`$@` represents the position of the parameters, starting from one.

```
for x in $@
do
    echo "Entered arg is $x"
done
```
Run it like this:
`./script arg1 arg2`

### How to Automate Scripts by Scheduling via cron Jobs

Cron is a job scheduling utility present in Unix like systems. You can schedule jobs to execute daily, weekly, monthly or in a specific time of the day. Automation in Linux heavily relies on cron jobs. <br>

Below is the syntax to schedule crons:
```
# Cron job example
* * * * * sh /path/to/script.sh
```
Here, `*` in code represents minute(s) hour(s) day(s) month(s) weekday(s), respectively. <br>

Below are some examples of scheduling cron jobs.

SCHEDULE | SCHEDULED VALUE
-------- | ---------------
5 0 * 8 * |	At 00:05 in August.
5 4 * * 6 |	At 04:05 on Saturday.
0 22 * * 1-5 |	At 22:00 on every day-of-week from Monday through Friday.

You can learn about cron in detail in this <u> blog </u> post.

## How to Check Existing Scripts in a System

### Using crontab
`crontab -l` lists the already scheduled scripts for a particular user.

![alt text](https://github.com/Chinjuku/Code-Development-1/blob/main/image/crontab.png)

### Using the find command
The `find` command helps to locate files based on certain patterns. As most of the scripts end with `.sh`, we can use the `find` script like this:

```
find . -type f -name "*.sh"
```

Where,

* `.` represents the current directory. You can change the path accordingly.
* `-type f` indicates that the file type we are looking for is a text based file.
* `*.sh` tells to match all files ending with `.sh`.

![alt text](https://github.com/Chinjuku/Code-Development-1/blob/main/image/shcommand.png)