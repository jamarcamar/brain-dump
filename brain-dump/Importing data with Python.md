#### Reading a text file
```
filename = 'huck_finn.txt'
file = open(filename, mode='r') # `r` is to read
text = file.read()
file.close()
```

#### Writing a text file
```
filename = 'huck_finn.txt'
file = open(filename, mode='w') # `w` is to write
file.close()
```

#### Context manager with
```
with open('huck_finn.txt', 'r') as file:
	print(file.read())
```