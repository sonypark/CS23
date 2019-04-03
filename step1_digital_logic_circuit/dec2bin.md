## 미션1
- 0부터 256 미만의 Int 정수형 10진수를 [Bool] 2진수 배열로 변환하는 dex2bin 함수를 구현한다.

- 사칙연산만으로 변환하는 방식을 구현한다.
- 만들어지는 비트 순서는 낮은 자리가 배열의 앞쪽에 오도록 표현한다. 
- 배열의 순서대로 보면 이진수가 뒤집혀 있는 것처럼 보인다고 가정한다.
- `이진수 1100 = [ 0, 0, 1, 1 ]` `이진수 0101 = [ 1, 0, 1, 0 ]`

```python
# decimal to binary (10진수 -> 2진수)
def dec2bin(decimal):
    binary = []
    while decimal > 0:
        remainder = decimal % 2
        binary.append(remainder)
        decimal = decimal // 2
    return binary
print('dec2bin:', dec2bin(173))
```

```python
# binary to decimal (2진수 -> 10진수)
def bin2dec(binary):
    decimal = 0
    p = 1
    for i in range(len(binary)):
        value = binary[i] * p
        decimal += value
        p *= 2
    return decimal

s = [0,1,1,1]
s2 = [1,1,1,1,0,1,0,1]
print('bin2dec:', bin2dec(s2))
```

---------
## 정리
> 앞서 만들었던 이진 덧셈기에 입력과 출력에 연결해서 10진수 덧셈이 동작하는지 여부를 확인한다.

```python
def halfAdder(bitA:bool, bitB:bool):
    sum = bitA ^ bitB  # ^ is logical xor in python
    carry = bitA and bitB
    return [carry, sum]

def fullAdder(bitA:bool, bitB:bool, carry_in:bool):
    carry1, sum1 = halfAdder(carry_in, bitA)
    carry2, sum2 = halfAdder(sum1, bitB)
    carry3 = carry1 or carry2

    return [carry3, sum2]
```

```python
# 8 bit = 1 byte
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

byteA = [ 1, 1, 0, 0, 1, 0, 1, 0 ]
byteB = [ 1, 1, 0, 1, 1, 0, 0, 1 ]
print(byteAdder(byteA, byteB))
```


```python
## byteAdder 계산기에서도 잘 동작한다.
print(bin2dec(byteAdder(dec2bin(10), dec2bin(10))))
```