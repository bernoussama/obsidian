### `awk`
--- 
```bash
awk '{print $1}' input.txt           # print the first field of each line
awk '{print NF}' input.txt           # print the number of fields in each line
awk '{print $1,$3}' input.txt        # print the first and third fields of each line
awk '{if ($1 > 10) print $2}' input.txt   # print the second field of lines where the first field is greater than 10
awk '/pattern/ {print $0}' input.txt      # print the entire line that contains the pattern
awk '{sum += $1} END {print sum}' input.txt  # calculate the sum of the first field in the file and print it at the end

```
- 
`find . -name "[aFj]*p?" -exec ls -l {} \;`