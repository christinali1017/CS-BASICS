###Grep
---

Grep finding phone numbers in files

```
grep '\(([0-9]\{3\})\|[0-9]\{3\}\)[ -]\?[0-9]\{3\}[ -]\?[0-9]\{4\}' file
```
http://stackoverflow.com/questions/2269586/grep-with-regex-for-phone-number






###awk
---
See the following simple example:

```
$ awk '{print}' /etc/passwd
```

When we called awk, we specified /etc/passwd as our input file. When we executed awk, it evaluated the print command for each line in /etc/passwd, in order.All output is sent to stdout, and we get a result identical to catting /etc/passwd. Now, for an explanation of the { print } code block. In awk, curly braces are used to group blocks of code together, similar to C. Inside our block of code, we have a single print command. In awk, when a print command appears by itself, the full contents of the current line are printed.


http://www.ibm.com/developerworks/library/l-awk1/

###What is the difference between (cp f1.txt f2.txt) & (less f1.txt > f2.txt)
---

The difference is that cp is far clearer to humans. That is one of the first things you should be optimizing for.

Using less in this way is so obscure, it's not really obvious that it works unless you try it out. The other answer points out that it doesn't work - if your file contains certain characters, and you expect the command to work without user interaction, e.g. as part of a script. This limitation is also obscure (at least I didn't think of it, despite having seen this behavior plenty of times).

less happens to be slower, one reason is it transfers data in smaller chunks. Run them under strace, I see less chunks 1023 bytes (1KiB - 1); cp chunks 64KiB.

- **less happens to be slower**



http://unix.stackexchange.com/questions/189347/what-is-the-difference-between-cp-f1-txt-f2-txt-less-f1-txt-f2-txt



