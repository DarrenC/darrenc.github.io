# Scripting - bash etc

- [Scripting - bash etc](#scripting---bash-etc)
  - [Books, articles etc](#books-articles-etc)
    - [Books](#books)
    - [Tutorials](#tutorials)
  - [Bash script elements](#bash-script-elements)
    - [Bash built-in variables](#bash-built-in-variables)
    - [Loops](#loops)
    - [Arrays](#arrays)
    - [SED](#sed)
    - [Shell Parameter Expansions](#shell-parameter-expansions)
  - [Bash script snippets](#bash-script-snippets)
    - [Checking logged in user](#checking-logged-in-user)
    - [Here docs - ssh and then run commands from a script](#here-docs---ssh-and-then-run-commands-from-a-script)
      - [Example of running a here doc with the ssh command to launch commands remotely](#example-of-running-a-here-doc-with-the-ssh-command-to-launch-commands-remotely)
    - [Source vs ./](#source-vs-)
  - [Stuff for the reporting script](#stuff-for-the-reporting-script)
    - [Reporting](#reporting)
    - [Proposing a list of simulations to choose from](#proposing-a-list-of-simulations-to-choose-from)

## Books, articles etc

### Books

- <https://linuxcommand.org/index.php> and the pdf version <https://netcologne.dl.sourceforge.net/project/linuxcommand/TLCL/19.01/TLCL-19.01.pdf>

### Tutorials

- <https://arachnoid.com/linux/shell_programming.html>
- SED/AWK intro - <https://www.makeuseof.com/tag/sed-awk-learn/>
  - Difference between them (with some nice examples) - <https://stackoverflow.com/questions/1632113/what-is-the-difference-between-sed-and-awk>
- Mad SED scripts - <http://sed.sourceforge.net/#scripts>
- GNU SED manual - <https://www.gnu.org/software/sed/manual/sed.html>
- Shell Parameter Expansions (see examples below) - <http://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html>

## Bash script elements

### Bash built-in variables

- <https://coderwall.com/p/85jnpq/bash-built-in-variables>

```bash
#! /bin/sh
echo '$#' $#
echo '$@' $@
echo '$?' $?

# If you run the above script as:
# > ./test.sh 1 2 3
# You get output:
$# 3
$@ 1 2 3
$? 0

# You passed 3 parameters to your script.

$# = number of arguments. Answer is 3
$@ = what parameters were passed. Answer is 1 2 3
$? = was last command successful. Answer is 0 which means 'yes'
```

### Loops

```bash
# Listing files in a directory
for f in *; do
  echo "file name is: $f"
done
```

Also some nice tutorials about different kinds of loops/situations

- <https://linuxize.com/post/bash-for-loop/>

```bash
# Example of looping over array values
values=(John Harry Jake Scott Philis)
for value in ${values[@]}; do
  echo "Current array value: ${value}"
done
```

### Arrays

- OLD BASH - Getting the last entry in the array
  - First get the size of the array as a number
  - Subtract one to get the last index
  - Get the value using []
- <https://stackoverflow.com/questions/36977855/get-last-element-in-bash-array/36978740>

```bash
  echo ${#arr[@]}
  echo ${arr[${#arr[@]}-1]}
```

- Newer BASH (~4.1) - <https://unix.stackexchange.com/questions/198787/is-there-a-way-of-reading-the-last-element-of-an-array-with-bash>

- Assigning value to an array element

```bash
# NB - no spaces around "=" :)
array[$i]="abc"
```

### SED

Streaming editor suited to modifying a per-line stream of text from a file or input string.
[GNU SED Manual](https://www.gnu.org/software/sed/manual/sed.html)

```bash
# pipe the string into the sed command (nb - works in ksh, bash or other shells)
# (could also use sed ... <<< "some string" but only in BASH)
# Remove the string foggy from the original string
echo 'foggy light' | sed 's/foggy//g'

# Simple example of replacing , by ;
sed 's/,/;/g' <<< "A,B,C"
sed 's/,/;/g' somefile.txt

# If you want to remove all the blocks of " -macro <WORD> "

$ sed 's/\s-macro \S*//g' <<< "cf foo -J 12345 -z -macro TEST_IFDEFINE -macro THIS -macro THIS1 -macro THIS2"  | cat -vet -
cf foo -J 12345 -z$

# \s-macro \S* matches space + -macro + space + a word.
# sed 's/something//g' removes this something as many times as it occurs in the string.

# Find numbers in form -123.45 and convert to (123.45)
sed 's/-\([0-9.]\+\)/(\1)/g' inputfile

# Find a number preceeded by a , followed by ,null] and delete it from the string (//g)
no_nulls=$(echo "$original_string" | sed 's/\(,[0-9]\+,null]\)//g' )

# Editing the line after the matching one - find a line containing FIXME and then on the next line (n;) add a prefix blah__ to the first character found.
sed -i '/FIXME.*/{n;s/\([a-z,A-Z]\)/blah__\0/;}' myfile.txt


# https://stackoverflow.com/questions/26568952/how-to-replace-multiple-patterns-at-once-with-sed
# Here what's interesting is more the "&" to output the captured match which helped where \1 wasn't good.
# This example adds a \n before each match of AND, GROUP BY etc.
sed -e 's:AND:\n&:g' -e 's:GROUP BY:\n&:g' -e 's:UNION:\n&:g' -e 's:FROM:\n&:g' file

```

### Shell Parameter Expansions

Can be used as an alternative to calling out to sed/awk

- <http://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html>

```bash
# Remove the delimeter $del from the original_string to the end (based on the * for the pattern match)
"${original_string%%"$del"*}"
```

## Bash script snippets

### Checking logged in user

```bash
# could also check $USER variable
if [ "$(whoami)" != "username" ]; then
    echo "Script must be run as user: username"
    exit -1
fi
```

### Here docs - ssh and then run commands from a script

- <http://www.tldp.org/LDP/abs/html/here-docs.html>

#### Example of running a here doc with the ssh command to launch commands remotely

```bash
ssh ${connection_string} <<'ENDSSH'
 cd \~
 ls -la ENDSSH
```

### Source vs ./

When running a script can do either "source" or ./

In most cases this is completely the same (source is a synonym of .) but there are some differences relating to source reusing the existing shell and ./ starting a sub-shell. This could have a side-effect for example if you "cd " inside the script being executed.

- [Documentation of source here](https://ss64.com/bash/source.html)

## Stuff for the reporting script

### Reporting

- Check for results directory -
    <https://www.cyberciti.biz/faq/howto-check-if-a-directory-exists-in-a-bash-shellscript/>

### Proposing a list of simulations to choose from

- List the contents of the jar file to get simulations
  - <https://stackoverflow.com/questions/7770183/list-contents-of-multiple-jar-files>
  - jar tvf to list contents -
        <https://www.google.com/search?client=ubuntu&channel=fs&q=jar+tvf&ie=utf-8&oe=utf-8>
  - example of this in a gist -
        <https://gist.github.com/nivag/5881687>
  - Xargs in case there are multiple commands -
        <http://man7.org/linux/man-pages/man1/xargs.1.html>
- Then will need to add all classes to an array and display it with a
    choice of value
- then launch the simulation based on the choice
- In case there needs to be a script for input and a script to
    launch -
    <https://unix.stackexchange.com/questions/535225/run-script-with-user-input-and-then-disconnect-job-and-run-in-background>
