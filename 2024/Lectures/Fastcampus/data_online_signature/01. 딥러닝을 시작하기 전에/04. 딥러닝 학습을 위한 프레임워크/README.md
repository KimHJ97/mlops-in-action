# 파이토치

파이토치(PyTorch)는 딥러닝 및 기계 학습 작업을 위한 오픈 소스 라이브러리입니다.   
 - 텐서 계산: 파이토치는 다차원 배열인 텐서를 위한 강력한 계산 기능을 제공합니다. 이를 통해 데이터를 효율적으로 표현하고, 딥러닝 모델의 계산을 수행할 수 있습니다.
 - 자동 미분(autograd): 파이토치의 자동 미분 기능은 신경망 모델을 훈련시키는 데 중요합니다. 이 기능을 통해 파이토치는 모델의 가중치에 대한 손실 함수의 미분을 자동으로 계산하여 경사 하강법(gradient descent)과 같은 최적화 알고리즘을 사용하여 모델을 업데이트할 수 있습니다.
 - 신경망 모듈: 파이토치는 신경망을 구축하는 데 사용되는 다양한 모듈과 클래스를 제공합니다. 이러한 모듈을 사용하여 다층 퍼셉트론(MLP), 합성곱 신경망(CNN), 순환 신경망(RNN) 등 다양한 유형의 신경망을 구현할 수 있습니다.
 - 모듈화와 유연성: 파이토치는 모듈화가 잘 되어 있어 사용자가 자신만의 모델 구조를 손쉽게 디자인하고 조합할 수 있습니다. 이는 연구나 실제 응용에서 모델을 개발하고 실험하는 데 매우 유용합니다.
 - GPU 지원: 파이토치는 GPU를 사용하여 대규모의 데이터 및 모델을 처리할 수 있습니다. 이는 신경망 모델의 훈련과 추론 속도를 향상시키는 데 도움이 됩니다.

```python
# GPU 사용 여부 체크 예시
# 텐서간의 연산을 수행할 때, 기본적으로 두 텐서가 같은 장치에 있어야 한다.
import torch

data = [
    [1, 2],
    [3, 4]
]

x = torch.tensor(data)
print(x.is_cuda)

x = x.cuda() # GPU로 옮기기
print(x.is_cuda)

x = x.cpu() # CPU로 옮기기
print(x.is_cuda)
```
<br/>

## 파이토치 텐서 소개 및 생성 방법

파이토치에서의 텐서는 다차원 배열로, 텐서는 파이토치에서 데이터를 표현하고 처리하는 데 사용됩니다. 텐서는 Numpy 배열과 유사하며, 다차원 데이터를 저장하고 다양한 수학 연산을 수행할 수 있습니다.  

 - __텐서의 속성__
    - 텐서의 기본 속성으로는 모양(shape), 자료형(data type), 저장된 장치 등이 있다.
```python
tensor = torch.rand(3, 4)

print(tensor)
print(f"Shape: {tensor.shape}")     # torch.Size([3,4])
print(f"Data type: {tensor.dtype}") # torch.float32
print(f"Device: {tensor.device}")   # cpu
```
<br/>

 - __텐서 초기화__
    - 리스트 데이터를 통해 직접 텐서를 초기화할 수 있다.
    - NumPy 배열에서 텐서를 초기화할 수 있다.
    - 다른 텐서의 정보를 토대로 텐서를 초기화할 수도 있다.
```python
# List -> Tensor
data = [
    [1, 2],
    [3, 4]
]
x= torch.tensor(data)

print(x)

# Numpy Array -> Tensor
a = torch.tensor([5])
b = torch.tensor([7])
c = (a + b).numpy()
print(c)
print(type(c)) # numpy.ndarray

result = c * 10
tensor = torch.from_numpy(result)
print(tensor)
print(type(tensor)) # torch.Tensor

# 다른 텐서 정보로 텐서 초기화
x = torch.tensor([
    [5, 7],
    [1, 2]
])

# x와 같은 모양과 자료형을 가지지만, 값이 1인 텐서 생성
x_ones = torch.ones_like(x)
print(x_ones)

# x와 같은 모양을 가지지만, 자료형은 float으로 덮어쓰고, 값은 랜덤으로 채우기
x_rand = torch.rand_like(x, dtype=torch.float32)
print(x_rand)
```
<br/>

## 파이토치 텐서의 형변환 및 차원 조작

 - __텐서의 특정 차원 접근__
```python
tensor = torch.tensor([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
])

print(tensor[0]) # 첫번째 행: [1, 2, 3, 4]
print(tensor[:, 0]) # 첫 번쨰 컬럼: [1, 5, 9]
print(tensor[..., -1]) # 마지막 컬럼: [4, 8, 12]
```
<br/>

 - __텐서 이어붙이기__
    - 두 개의 텐서가 있을 때, 두 텐서를 이어붙여 새로운 텐서를 만들 수 있다.
```python
tensor = torch.tensor([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
])

# dim: 텐서를 이어 붙이기 위한 축
# 0번 축(행)을 기준으로 이어 붙이기
result = torch.cat([tensor, tensor, tensor], dim=0)
print(result)

# 1번 축(열)을 기준으로 이어 붙이기
result = torch.cat([tensor, tensor, tensor], dim=1)
print(result)
```
<br/>

 - __텐서 형변환__
    - 텐서의 자료형을 변환할 수 있다.
```python
a = torch.tensor([2], dtype=torch.int)
b = torch.tensor([5.0])

print(a.dtype) # torch.int32
print(b.dtype) # torch.float32

# 텐서 a는 자동으로 float32형으로 형변환 처리
print(a + b)

# 텐서 b를 int32형으로 형변환하여 덧셈 수행
print(a + b.type(torch.int32))
```
<br/>

 - __텐서의 모양 변경__
    - view() 메서드로 텐서의 모양을 변경할 수 있다.
    - view()를 이용하면 주소값이 공유된다. 떄문에, 원본값이 그대로 변경된다.
```python
a = torch.tensor([1, 2, 3, 4, 5, 6, 7, 8])
b = a.view(4, 2)
print(b)

# a의 값을 변경하면 b도 변경
a[0] = 7
print(b)

# a의 값을 복사(copy)한 뒤에 변경
c = a.clone().view(4, 2)
a[0] = 9
print(c)
```
<br/>

 - __텐서의 차원 교환__
    - 하나의 텐서에서 특정한 차원끼리 순서를 교체할 수 있다.
```python
a = torch.rand((64, 32, 3))
print(a.shape) # torch.Size([64, 32, 3])

b = a.permute(2, 1, 0) # 차원 자체를 교환
print(b.shape) # torch.Size([3, 32, 64])
```
<br/>

## 파이토치 텐서의 연산과 함수

 - __텐서의 연산__
    - 텐서는 사칙연산 등 기본적인 연산을 제공한다.
```python
a = torch.tensor([
    [1, 2],
    [3, 4]
])
b = torch.tensor([
    [5, 6],
    [7, 8]
])

print(a + b)
print(a - b)
print(a * b)
print(a / b)

# 행렬 곱 수행
print(a.matmul(b))
print(torch.matmul(a, b))

# 평균 계산
a = torch.Tensor([
    [1, 2, 3, 4],
    [5, 6, 7, 8]
])
print(a)
print(a.mean()) # 전체 원소에 평균
print(a.mean(dim=0)) # 각 열에 대해서 평균 계산
print(a.mean(dim=1)) # 각 행에 대해서 평균 계산

# 합계 계산
print(a)
print(a.sum()) # 전체 원소에 대한 합계
print(a.sum(dim=0)) # 각 열에 대해서 합계 계산
print(a.sum(dim=1)) # 각 행에 대해서 합계 계산

# 최대 함수
# max(): 원소의 최댓값 반환
# argmax(): 가장 큰 원소(최댓값)의 인덱스 반환
a = torch.Tensor([
    [1, 2, 3, 4],
    [5, 6, 7, 8]
])
print(a)
print(a.max()) # 전체 원소에 대한 최댓값
print(a.max(dim=0)) # 각 열에 대해서 최댓값
print(a.max(dim=1)) # 각 행에 대해서 최댓값
print(a.argmax()) # 전체 원소에 대한 최댓값의 인덱스
print(a.argmax(dim=0)) # 각 열에 대한 최댓값의 인덱스
print(a.argmax(dim=1)) # 각 행에 대한 최댓값의 인덱스
```
<br/>

 - __텐서의 차원 줄이기&늘리기__
    - unsqueeze(): 크기가 1인 차원을 추가
    - squeeze(): 크기가 1인 차원 제거
```python
a = torch.Tensor([
    [1, 2, 3, 4],
    [5, 6, 7, 8]
])
print(a.shape) # torch.Size([2, 4])

# 첫 번쨰 축에 차원 추가
a = a.unsqueeze(0)
print(a)
print(a.shape) # torch.Size([1, 2, 4])

# 네 번쨰 축에 차원 추가
a = a.unsqueeze(3)
print(a)
print(a.shape) # torch.Size([1, 2, 4, 1])

# 크기가 1인 차원 제거
a = a.squeeze()
print(a)
print(a.shape) # torch.Size([2, 4])
```
<br/>

## 자동 미분과 기울기

 - PyTorch에서는 연산에 대하여 자동 미분을 수행할 수 있다.
    - 일반적으로 모델을 학습할 때는 기울기를 추적한다.
    - 하지만, 학습된 모델을 사용할 때는 파라미터를 업데이트하지 않으므로, 기울기를 추적하지 않는 것이 일반적이다.
```python
import torch

# requires_grad를 설정할 떄만 기울기 추적
x = torch.tensor([3.0, 4.0], requires_grad=True)
y = torch.tensor([1.0, 2.0], requires_grad=True)
z = x + y

print(z) # [4.0, 6.0]
print(z.grad_fn) # 더하기(add)

out = z.mean()
print(out) # 5.0
print(out.grad_fn) # 평균(mean)

out.backward() # scalar에 대하여 가능
print(x.grad)
print(y.grad)
print(z.grad) # leaf variable에 대해서만 gradient 추적이 가능하다. 따라서 None.

temp = torch.tensor([3.0, 4.0], requires_grad=True)
print(temp.requires_grad)
print((temp ** 2).requires_grad)

# 기울기를 추적하지 않기 때문에 계산 속도가 더 빠르다.
with torch.no_grad():
    temp = torch.tensor([3.0, 4.0], requires_grad=True)
    print(temp.requires_grad)
    print((temp ** 2).requires_grad)
```

