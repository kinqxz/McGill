# COMP 206 — Lecture 5

**Course:** Introduction to Software Systems  
**Date:** September 15th 2026
**Topic:** Vim and Permissions

---

## Vim
- Powerful text editor designed to efficiently write text from a terminal
- Preinstalled on most Linux distributions
- Modal editor
  - Keys have different functions depending on current mode
  - (compare to editors like Notepad where typing always inserts text)

## Vim modes
- Instead of a menu system, Vim uses modes
The most important modes are:
- Insert mode:
  - To edit your text
  - Can press any keyboard characters
- Normal mode (also known as command mode):
  - Enter editor commands
    - Move around in the file, change modes, copy, undo, etc.
- Command-line mode:
  - Save, load, quit, search, etc.
- Visual mode:
  - Like normal modes, but movement keys highlight lines to apply editor commands on all of them

## Important commands
To get help for a command, :help command

- Insert mode:
  - To get in insert mod, any of the following: i, I, a, A, o, O
    - i - insert text before the cursor | I - insert at start of line before first non-blank
    - a - append text after the cursor | A - append text at the end of the line
    - o - begin a new line below the cursor and insert text | O - same but above cursor

- Normal mode:
  - To get to normal mode: Esc key
  - To move:
    - h, j, k, l to move left, down, up, right
    - gg - go to first line | G - go to last line
  - To delete: dd, D, x, r
    - dd - deleted a line | D - delete the rest of the line
    - x - delete a character | r - replace a character
  - To copy (yank) and paste a line:
    - yy or Y (equivalent) - yank | p - paste before cursor | P - paste after cursor
  - To undo and redo:
    - u (undo) and ctrl+r (redo)

- Command-line mode:
  - w, q, wq, q!, line number, e filename
    - :w - save file | :q - quit current window | :wq save and quit | :q! quit and discard changes
    - :number - go to a specific line number (For example, :14)
    - :e filename - Edit a file
  - To search: / (forward), ? (backwards)
    - Once you press enter, press n and N to get next/previous result

## More on vim
- Commands can be preceded by a number to repeat them a number of times, for example 5dd wwould deleted the next 5 lines. (In the help doc, this is described as [count])
- You can learn about basic vim commands by typing vimtutor in your Unix command-line. This is a program that comes with every vim installation

## Permissions
- All files are owned by a user and a group
  - Usually, this owner is the user that created the file.
- Permissions on files exists at three level (classes)
  - user, group, and others.
- Three types of rights can be given:
  - read, write and execute.
- Any combination of these rights must be given to these three levels.

Symbolic notation

Ex: -rw-r--r-- 1

- File type: -
- User permissions: rw-
- Group permissions: r--
- Other permissions: r--

- The symbolic notation for permissions is displayed as a string of 9 characters (10 if including file type)
  - (0th: indicates if the file is a directory.)
  - 1st: indicates if the user that owns the file has read access to the file
  - 2nd: indicates if the user that owns the file has write access to the file
  - 3rd: indicates if the user that owns the file has execute access to the file
  - 4th, 5th, 6th: indicates if the group owner has read, write, or execute.
  - 7th, 8th, 9th: indicates if all other users have read, write or execute.

## Order of precedence for permissions
- The order of precedence for permissions is:
  - User
  - Group
  - Others
- If a user is in multiple classes, the highest one applies

**chmod** command
- Change mode: Change file permissions
  - Can be used by owner or superuser (root)
- Who:
  - u: The user who owns the file (this means "you")
  - g: The group the file belongs to
  - o: The other users
  - a: all of the above
- Permission:
  - r: Permission to read the file
  - w: Permission to write (or delete) the file
  - x: Permission to execute the file (for directories, this is needed to enter them)
- Changes to:
  - =: become
  - +: add
  - -: remove

chmod command examples
- The syntax of the command is as follows:
  - chmod who=permission files
Here are a few examples of the chmod command:
- Give read permission to group:
  - chmod g+r file.txt
- Give write/execute permission to you (user):
  - chmod u+wx file2.txt
- Remove all permissions from others
  - chmod o= file3.txt
- Give read/write permission only to user and group
  - chmod ug=rw file4.* file2.txt
- Give read only to user and execute only to group
  - chmod u=r,g=x file4.* file2.txt (no space after the comma)

## Binary representation of permissions
- Given a 9 character permissions string:
rwx --- rw-
- We can equivalent represent it in binary
111 000 110
- Where 1 means "on" and 0 means "off"

## Octal representation of permissions
- Given the binary representation of permissions we can convert it to octal (base 8) by converting each group of 3 bits to its corresponding digit as follows:

Binary | Octal
000 - 0
001 - 1
010 - 2
011 - 3
100 - 4
101 - 5
110 - 6
111 - 7

Ex: 111 000 110 in octal is 706

chmod and octal representation
- chmod supports octal representation
  - Often used when wnat to set up all permissions at the same time
- Ex:
  - chmod 400 filename
    - Give user permission to read and no permissions to group and others

