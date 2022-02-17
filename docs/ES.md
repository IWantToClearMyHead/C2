```js
// Use this to give interviewees short questions
```


### [Python]lambda print calculation
```
python3 -c 'x = lambda a, b : a * b; print(x(5,6))'
```

### [Python]dump good view of dict, or dict in dict
```
import json
print(json.dumps(model.instance_infos, sort_keys=False, indent=4))
```

### [Bash]Make 99 Table
```
#!/bin/bash
#print 99 table
for Row in {1..9};do
 for Column in `seq $Row`;do
  echo -ne "${Column}x${Row}=$[$Row*$Column]\t"
 done
 echo
done
```

<a href="index.md">Back to home</a>
