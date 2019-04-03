
## 미션

- NAND 게이트 동작을 함수로 구현합니다.
- 함수의 매개변수는 BOOL 타입을 갖는 두 개를 갖고, 결과값은 BOOL 타입으로 리턴합니다.
- paramA 와 paramB 가 모두 true 일 때만 결과가 false 가 되고, 나머지 다른 경우는 모두 true가 됩니다

## NAND (NOT AND)

NAND | 0 | 1
:---------:  | :-----------: | :-----------:
0	| 1 | 1
1	| 1 | 0

```python
def nand(paramA:bool, paramB:bool)-> bool:
    return not (paramA and paramB)

print(nand(True, True)) # => False
print(nand(True, False)) # => True
print(nand(False, True)) # => True
print(nand(False, False)) # => True
```