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

- less happens to be slower
- 


http://unix.stackexchange.com/questions/189347/what-is-the-difference-between-cp-f1-txt-f2-txt-less-f1-txt-f2-txt



