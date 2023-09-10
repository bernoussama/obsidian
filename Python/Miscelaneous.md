## Lambda function
```python
# Recommended:
def f(x): return 3*x


# Not recommended:
f = lambda x: 3*x
```

## Handling files
### Read and write binary files
```python
from os import strerror

data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 + i

try:
    bf = open('file.bin', 'wb')
    bf.write(data)
    bf.close()
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))

# Your code that reads bytes from the stream should go here.
try:
    bf = open('file.bin', 'rb')
    bf.readinto(data)
    bf.close
    print([bin(b) for b in data])
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```

- Read binary File
```python
from os import strerror

try:
    bf = open('file.bin', 'rb')
    data = bytearray(bf.read())
    bf.close()

    for b in data:
        print(hex(b), end=' ')

except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```
- **Be careful** - don't use this kind of read if you're not sure that the file's contents will fit the available memory.

- Read specific number of bytes
```python
try:
    bf = open('file.bin', 'rb')
    data = bytearray(bf.read(5)) # reads 5 bytes from the file stream
    bf.close()

    for b in data:
        print(hex(b), end=' ')

except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```
