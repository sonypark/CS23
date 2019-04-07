## 미션

- XOR 함수를 구현합니다.
- XOR = Exclusive OR
- A,B 둘 중 하나만 True 일 경우 True 리턴


## XOR (Exclusive OR)

XOR | 0 | 1
:---------:  | :-----------: | :-----------:
0	| 0 | 1
1	| 1 | 0


```python
def xor(paramA:bool, paramB:bool)->bool:
    return paramA != paramB

print(xor(True, True)) # => False
print(xor(True, False)) # => True
print(xor(False, True)) # => True
print(xor(False, False)) # => False
```