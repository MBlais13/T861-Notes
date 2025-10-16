#bash 

## Text Color
example:
```bash
echo -e "\033[1m Test"
# output would be Test in bold.
```

```bash
echo -e "\033[32m"
# outputs terminal color to green
```

To revert use:
```bash
echo -e "\033[0m"
# reverts back to normal
```

```bash
echo -e "\033[32mthis is green\033[0mback to normal"
# outputs terminal color to green and back to normal
```
##### *References*
https://misc.flogisoft.com/bash/tip_colors_and_formatting

## Brace String Manipulation

- `${string:start:length}` - get a substring
- `echo ${string:5}` - Gets the first 
- `echo ${string:5:5}`
- `echo ${string:0:-3}`
- `var//match//replace`

```bash
string="why has it been sooooo COLD!"
echo ${string:5}
echo ${string:5:5}
echo ${string:0:-3}
```
