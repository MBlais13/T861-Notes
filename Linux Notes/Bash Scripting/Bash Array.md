#bash 


## Arrays
* ${var:start:length} – get a substring  
* ${var/match/replace} – replace the first occurrence of match with replace
* ${var//match/replace} – replace all instances of match with replace

* Recall arrays are lists of values  
* To declare and array from a list use:
     * `declare -a arrayName=(item1 item2 item3)`
     * `arrayName=(item1 item2 item3)`
     * `arrayName[0]=item1`
     * `arrayName[1]=item2`


---
## Create Array
```

```

## Arrays cont.
* To access elements of an array you can use the following syntax
	* `${arrayName[0]} `= first element
	* `${arrayName[1]}` = second elements
	
* To access all elements we can use:
	* `${arrayName[@]}` = array expansion into list
	* Note in this case if this is quoted "`${arrayName[@]}`" then each array element will be quoted when creating a list

```bash
"${array[@]}" # “One Item” “Two Item” - 2 Items (Usually the desired result)
${array[@]} # One Item Two Item – 4 Items
```