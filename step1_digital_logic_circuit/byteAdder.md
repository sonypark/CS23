
## 미션1

- 덧셈은 숫자 연산에서 가장 기본이 되는 동작입니다.
- BOOL 타입으로 동작하는 이진 덧셈기를 논리 게이트 동작만으로 구현해봅니다.

#### 합(sum)
> 합을 구하는 내부 함수를 구현합니다.

```python
def XOR(bitA:bool, bitB:bool):
    return bitA != bitB
```

#### 자리올림(carry)
> 자리올림 비트를 구하는 내부 함수를 구현합니다.

```python
def AND(bitA:bool, bitB:bool):
    return bitA and bitB
```

#### 반쪽덧셈(halfadder)
> 입력을 두 개 받아서, 합(sum)과 자리올림(carry)를 배열로 리턴하는 함수를 구현합니다.
```python
def halfAdder(bitA:bool, bitB:bool):
    sum = bitA ^ bitB  # ^ is logical xor in python
    carry = bitA and bitB
    return [carry, sum]

print('halfAdder: ', halfAdder(1,1))
print('halfAdder: ', halfAdder(1,0))
```

#### 전체덧셈(fulladder)

> 입력을 두 개와 자리올림 비트를 입력으로 받아서, 합(sum)과 자리올림(carry)를 배열로 리턴하는 함수를 구현합니다.

```python
def fullAdder(bitA:bool, bitB:bool, carry_in:bool):
    carry1, sum1 = halfAdder(carry_in, bitA)
    carry2, sum2 = halfAdder(sum1, bitB)
    carry3 = carry1 or carry2

    return [carry3, sum2]

print('fullAdder: ', fullAdder(1,1,1))
print('fullAdder: ', fullAdder(1,0,1))
```


## 미션2
- 앞에서 만든 이진 덧셈기를 이용해서 BOOL 타입으로 동작하는 8비트 덧셈기를 구현한다.

- 바이트 덧셈(byteadder) : 8비트를 BOOL타입 배열로 2개를 입력 받는다.
- 자리올림(carry) + 전체 합(sum)을 순서대로 배열로 담아서 리턴하는 함수를 구현한다.
- 입력으로 들어오는 byteA, byteB 배열의 길이는 같다고 가정한다.
- 입력으로 들어오는 byteA 비트 순서는 낮은 자리가 배열의 앞쪽에 오도록 표현한다. 
- 배열의 순서대로 보면 이진수가 뒤집혀 있는 것처럼 보인다고 가정한다.


> 8 bit = 1 byte
```python
def byteAdder(byteA, byteB):
    answer = []
    for i in range(len(byteA)):
        if i == 0:
            carry, sum = halfAdder(byteA[0], byteB[0])
            answer.append(sum)
        else:
            carry2, sum2 = fullAdder(byteA[i], byteB[i], carry)
            answer.append(sum2)
            carry = carry2
    answer.append(carry)
    return answer


# byteA = [1, 1, 0, 1, 1, 0, 1, 0]
# byteB = [1, 0, 1, 1, 0, 0, 1, 1]
byteA = [ 1, 1, 0, 0, 1, 0, 1, 0 ]
byteB = [ 1, 1, 0, 1, 1, 0, 0, 1 ]
print(byteAdder(byteA, byteB))
```