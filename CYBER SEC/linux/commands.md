<!-- @format -->

### Ubuntu CLI Commands

You can use the cp command to copy the contents of one file to another on Ubuntu.

```bash
cp /home/user/documents/file1.txt /tmp/file2.txt
```

Move a file to a different directory:

```bash
mv file.txt /path/to/destination/

```

Move and rename a file:

```bash
mv oldfile.txt newfile.txt

```

Move a file to a parent directory:

```bash
mv file.txt ../

```

Move multiple files to a directory:

```bash
mv file1.txt file2.txt /path/to/destination/

```

Location of a particular thing / package (mostly source files)

```bash
whereis package_name
```

Tells you what something does

```bash
whatis package_name
```

Move and rename a file:

```bash
mv oldfile.txt newfile.txt

```

Command to Add/Create user

```bash
sudo adduser user_name

```

Switch user

```bash
su username

```

Delete User

```bash
sudo deluser username

```

To exit user

```bash
exit
```

### Grep

Certainly! grep is a powerful command-line tool for searching and manipulating text in Linux and Ubuntu. Here are some common grep commands along with important flags:

Basic Text Search:

The most basic usage of grep is for searching for a specific word or pattern in a file or a stream of text.

```bash
grep "pattern" filename
```

`-i` (ignore case): Perform a case-insensitive search.

`-v` (invert match): Display lines that do not contain the specified pattern.

`-l` (list filenames): Show only the filenames that contain the pattern (useful with multiple files).

Recursive Search:

To search for a pattern in all files within a directory and its subdirectories, you can use the -r flag.

```bash
grep -r "pattern" directory/

```

Regular Expressions:

`grep` supports regular expressions for more complex pattern matching.

```bash
grep -E "regex_pattern" filename

```

`-o` (only matching): Display only the matched part of the line.

`-P` (Perl-compatible regex): Use Perl-compatible regular expressions.

Count Matches:

To count the number of matches instead of displaying the lines, use the `-c` flag.

```bash
grep -c "pattern" filename

```

Display Line Numbers:

To show line numbers along with matching lines, use the `-n` flag.

```bash
grep -n "pattern" filename

```

Recursive Directory Search with Line Numbers:

A combination of flags to recursively search directories, show line numbers, and display the filenames containing matches.

```bash
grep -rnl directory/ -e "pattern"

```

Search for Whole Words:

Use the `-w` flag to match whole words, not substrings.

```bash
grep -w "word" filename

```

Exclude Files or Directories:

You can exclude specific files or directories from the search using the `--exclude` and `--exclude-dir` flags.

```bash
grep "pattern" --exclude="exclude_file" --exclude-dir="exclude_dir" directory/

```

Using `find` with `grep`:

You can combine `find` and `grep` to search for files matching a pattern in a specific directory and its subdirectories.

```bash
find directory/ -type f -exec grep -H "pattern" {} \;

```

Check running processes:

```bash
ps

```

Make/Change user Password

```bash
sudo passwd name-of-users

```

Change Name of User

```bash
sudo usermod -l <new-name> <old-name>

```

To see all groups

```bash
cat /etc/group

```

To see the groups a user belongs in:

```bash
groups name-of-user

```

To see the members of a group:

```bash
getent group name-of-group

```

To create a new group:

```bash
sudo addgroup name-of-group

```

```bash
sudo groupadd name-of-group

```

To add a user to a group:

```bash
sudo usermod -a -G name-of-group name-of-user

```

To delete a group:

```bash
sudo delgroup name-of-group

```

```bash
sudo groupdel name-of-group

```

To remove a user from a group:

```bash
deluser name-of-user name-of-group

```

Changing permissions:

```bash
sudo chmod <owner-permissions group-permissions all-permissions> file/ folder -R

```

Changing owner:

```bash
sudo chown -R name-ofuser name-of-folder/file

```

Changing group:

```bash
sudo chgrp -R name-of-group name-of-folder/file

```

Checking file/folder permissions

```bash
stat file_name/folder_name

```

Checking file/folder permissions for hidden files

```bash
ls -la file_name/folder_name

```
