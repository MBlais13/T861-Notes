#bash 

## Bash input redirection from variables
* Sometimes you want to redirect standard input from a variable, to do that use <<<

```bash
value="welcome"
cat <<< $value
```

The output of cat will be welcome