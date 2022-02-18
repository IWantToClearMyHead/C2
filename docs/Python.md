### try in a loop, print ok only

```
def a_function():
    return 1/0;
def b_function():
    return 1;
def c_function():
    return ["a" + 1];

functions = [a_function, b_function, c_function]
for f in functions:
    try:
        if f():
            print(f.__name__, "\033[95m{}\033[00m".format("is ok"))
    except Exception as exception:
        #print(f.__name__, "\033[91m{}\033[00m".format(exception))
        pass
```

### license to continue, here is "geek"
```
for _ in range(3):
  
    user_input = input(" Please enter your lucky word or type 'END' to terminate loop: ")
      
    if user_input == "geek":
        print("You are really a geek")
        break
  
    elif user_input == "END":
        break
  
    else:
        print("Try Again")
```

### break a list loop
```
functions = [-1,0,1,2,3]
for f in functions:
    try:
        if f == 1:
            print(f, "\033[95m{}\033[00m".format("is ok"))
            break
    except Exception as exception:
        #print(f.__name__, "\033[91m{}\033[00m".format(exception))
        pass
```

### break a generator
```
def fl(n):
    for x in range(n):
        yield x

for f in fl(10):
    try:
        if f == 5:
            print(f, "\033[95m{}\033[00m".format("is ok"))
            break
        else:
            print(f, "\033[91m{}\033[00m".format("is not ok"))
    except Exception as exception:
        print(f, "\033[92m{}\033[00m".format(exception))
```

### go over the generator to show only the ok
```
def fl(n):
    for x in range(n):
        yield x

for f in fl(10):
    try:
        if f == 5:
            print(f, "\033[95m{}\033[00m".format("is ok"))
        else:
            print(f, "\033[91m{}\033[00m".format("is not ok"))
    except Exception as exception:
        print(f, "\033[92m{}\033[00m".format(exception))
```
<a href="#top">Back to top</a>
