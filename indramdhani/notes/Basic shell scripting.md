### Creating the file

```bash
nano filename.sh
chmod +x filename.sh
```

### Hello world

```bash
#!/bin/bash

echo "Hello world"
```

### Show current time

```bash
#!/bin/bash

date
```

### Show file

```bash
#!/bin/bash

ls -alh
```

### Show current path

```bash
#!/bin/bash

pwd
```

### Zip files

```bash
#!/bin/bash

zip zipname.zip *
```

### Variables

```bash
#!/bin/bash

GREETING="Welcome"
USER=$(whoami)
DAY=$(date)

echo "$GREETING back $USER! Today is $DAY, which is the best day of the entire week!"
echo "Your Bash shell version is: $BASH_VERSION. Enjoy!"
```

### Functions

```bash
#!/bin/bash

function user {
	echo "Username: $(whoami)"
	echo "Home Directory: $HOME"
}

function get_date {
	echo "Date: $(date)"
}

user
get_date
```

### Functions with Parameter

```bash
#!/bin/bash

USER="indra"

function user {
	echo "Username: $1"
}

user $USER

```

### File with parameter

```bash
#!/bin/bash

USER=$1

function user {
	echo "Username: $1"
}

user $USER
```

### File with parameter

```bash
#!/bin/bash

echo $1 $2 $3 $4
echo $#
echo $*
```

### Comparison

[Untitled](https://www.notion.so/e9f13080370d4daa968b379ad9e6f9ea)

```bash
#!/bin/bash

string_a="UNIX"
string_b="GNU"
echo "$string_a and $string_b"
[ $string_a = $string_b ]
echo $?

num_a=100
num_b=100
num_c=50

echo "$num_a"
echo "$num_b"
echo "$num_c"

echo "$num_a and $num_b"
[ $num_a -eq $num_b ]
echo $?

echo "$num_a and $num_c"
[ $num_a -gt $num_c ]
echo $?
```

### Conditional Statement

```bash
#!/bin/bash

num_a=100
num_b=200

echo "$num_a"
echo "$num_b"

if [ $num_a -lt $num_b ]; then
	echo "$num_a is less than $num_b"
fi

if [ $num_a -gt $num_b ]; then
	echo "condition correct"
else 
	echo "condition not correct"
fi

```

### Switch

```bash
#!/bin/bash
input_number=$1

case $input_number in 
100)
echo "100";;
200)
echo "200";;
300)
echo "300";;
*)
echo "$input_number not defined";;
esac

```

### For Looping

```bash
#!/bin/bash

for i in 1 2 3; do
	echo $i
done
```

### While Looping

```bash
#!/bin/bash

counter=0
while [ $counter -lt 3 ]; do
	let counter+=1
	echo $counter
done
```

### Until Looping

```bash
#!/bin/bash

counter=6
until [ $counter -lt 3 ]; do
	let counter-=1
	echo $counter
done
```

---

[](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)[https://linuxconfig.org/bash-scripting-tutorial-for-beginners](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)

[](https://linuxhint.com/30_bash_script_examples/)[https://linuxhint.com/30\_bash\_script\_examples/](https://linuxhint.com/30_bash_script_examples/)

[](https://devhints.io/bash)[https://devhints.io/bash](https://devhints.io/bash)

#server #bash #shell 