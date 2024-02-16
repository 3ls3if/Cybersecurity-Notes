# 🐧 Bash

{% embed url="https://linuxhandbook.com/bash/" %}

## Creating a Script

```bash
#! /bin/bash

echo "Hello World!"
```

## Variables

```bash
Name="rohan"

echo $Name

echo ${Name} #same as previous one
```

## User Input

```bash
NAME #variable NAME is declared

read  -p "Enter your name: " NAME #Taking the user input in the NAME variable

echo "Your name is $NAME" #Displaying the user inputed value
```

## If Statement

```bash
#! /bin/bash

NAME="Rohan"

if [ "$NAME" == "Rohan" ]
then
   echo "Your name is $NAME"
fi

```

## If-Else Statement

```bash
#! /bin/bash

NAME="Rohan"

if [ "$NAME" == "Rasdf" ]
then
        echo "Your name is $NAME"
else
        echo "Your name is not $NAME"
fi

```

## Else-If (elif)

```bash
#! /bin/bash

NAME="Rohan"

if [ "$NAME" == "Rasdf" ]
then
        echo "Your name is $NAME"
        
elif [ "$NAME" == "Jack" ]
then
        echo "Your name is Jack"

else
        echo "Your name is not $NAME"
fi


```

## Conditional Operators

| **Operator** | **Description**                                         |
| ------------ | ------------------------------------------------------- |
| -eq          | Returns true if two numbers are equivalent              |
| -lt          | Returns true if a number is less than another number    |
| -gt          | Returns true if a number is greater than another number |
| ==           | Returns true if two strings are equivalent              |
| !=           | Returns true if two strings are not equivalent          |
| !            | Returns true if the expression is false                 |
| -d           | Check the existence of a directory                      |
| -e           | Check the existence of a file                           |
| -r           | Check the existence of a file and read permission       |
| -w           | Check the existence of a file and write permission      |
| -x           | Check the existence of a file and execute permission    |

```bash
#!/bin/bash
echo "Enter a number"
read n
if [ $n -lt 100 ]; then
printf "$n is less than 100\n"
fi
```

## File Operations

* \-e: Returns true value if a file exists.
* \-f: Return true value if a file exists and regular file.
* \-r: Return true value if a file exists and is readable.
* \-w: Return true value if a file exists and is writable.
* \-x: Return true value if a file exists and is executable.
* \-d: Return true value if a file exists and is a directory.

```bash
#!/bin/bash

FILE="test.txt"

if [ -f "$FILE" ]
then
        echo "$FILE is a file"
else
        echo "$FILE is not a file"
fi
```

## CASE Statement

```bash
case EXPRESSION in

  PATTERN_1)
    STATEMENTS
    ;;

  PATTERN_2)
    STATEMENTS
    ;;

  PATTERN_N)
    STATEMENTS
    ;;

  *)
    STATEMENTS
    ;;
esac
```

```bash
#!/bin/bash

read -p "Are you 21 or over? Y/N " ANSWER

case "$ANSWER" in
        [yY] | [yY][eE][sS])
                echo "You can have beer :)"
                ;;
        [nN] | [nN][oO])
                echo "Sorry, no drinking"
                ;;
        *)
                echo "Please enter y/yes or n/no"
                ;;
esac
```

## For Loop                             &#x20;

{% code fullWidth="false" %}
```bash
#!/bin/bash

NAMES="Brad Kevin Alice Mark"

for NAME in $NAMES
        do 
                echo "Hello $NAME"
done

```
{% endcode %}

{% code title="Rename Files" %}
```bash
#!/bin/bash

FILES=$(ls *.txt)

NEW="new"

for FILE in $FILES
        do
                echo "Renaming $FILE to new-$FILE"
                mv $FILE $NEW-$FILE
done


```
{% endcode %}

## While Loop

```bash
while [ condition ];
do
    # statements
    # commands
done
```

```bash
#!/bin/bash

LINE=1

while read -r CUR_LINE
        do
                echo "$LINE: $CUR_LINE"
                ((LINE++))
done < "./new-1.txt"

```

## Functions

```bash
#!/bin/bash

function say_hello() {
        echo "Hello World!"
}

say_hello
```

{% code title="Function with parameters" %}
```bash
#!/bin/bash

function greet()
{
        echo "Hello, I am $1 and I am $2"
}

greet "Rohan" "36"

```
{% endcode %}

