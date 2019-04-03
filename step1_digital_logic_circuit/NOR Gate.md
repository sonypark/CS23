
## 미션

- NOR게이트 동작을 구현합니다.
- 함수의 매개변수는 BOOL 타입을 갖는 두 개를 갖고, 결과값은 BOOL 타입으로 리턴합니다.
- paramA 와 paramB 가 모두 false 일 때만 결과가 true 가 되고, 나머지 다른 경우는 모두 false가 됩니다.


## NOR (NOT OR)

NOR | 0 | 1
:---------:  | :-----------: | :-----------:
0	| 1 | 0
1	| 0 | 0


```python
def nor(paramA:bool, paramB:bool)->bool:
    return not (paramA or paramB)

print(nand(True, True)) # => False
print(nand(True, False)) # => False
print(nand(False, True)) # => False
print(nand(False, False)) # => True
```