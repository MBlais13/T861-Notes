#bash 

Heredoc Syntax

Heredoc syntax allows us to send multiple lines of input to a command similar to redirecting from a file but without creating a file

to use heredoc syntax we use <<{end of input indicator}, ex. `EOF`

```bash
sftp user@server.com <<EOF
    put file.txt

dir EOF
```