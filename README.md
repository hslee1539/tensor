# tensor
나만의 텐서 패키지

깃허브와 딥러닝 공부용으로 만듬

## 패키지 요약
N차원 텐서를 1차원 배열로 관리하고 연산함.
딥러닝에 필요한 matmul, transpose, element-wise, axis 변환 계산을 하는 코드를 직접 만듬.
이 계산 코드들은 계산과 계산에 필요한 공간 생성을 분리함.
이 계산 코드들은 이 패키지의 computing 패키지에 있고, 이 패키지를 만든 사람의 tensor 클래스와 완전 독립된 모듈들이라 다른 tensor 관리 클래스에 응용 가능함.
또한 tensor 생성과 관련해 정규분포, 일반 랜덤, 값 하나로 초기화 등을 구현해 둠.
사용하는 외부 패키지는 random만 사용
matmul과 element-wise 방법을 별도의 함수를 통해 커스텀 연산을 할 수 있음.

주의점으로, numpy의 연산 결과를 보면서 직접 규칙을 찾아 낸것이라, 이 계산 알고리즘이 맞는지는 더 테스트 해봐야 함.

## 패키지 설치 하는 곳
이 패키지를 사용할 .py가 있는 폴더에 이 패키지 폴더를 복사하거나,
sys.path에 등록된 곳에 이 패키지 폴더를 복사.


## 패키지 사용 방법
이 패키지 폴더 이름으로 import. ( __init__.py가 패키지의 모든 기능을 import함)
Tensor(array, shape)으로 객체를 만들고, array와 shape은 모두 1차원 배열이 와야 함.
연산할 때는 반드시 저장할 곳을 만들어서 연산을 함.

예)
~
import tensor
#2by2
left = tensor.Tensor([1,2,3,4], [2,2]) # array와 shape은 모두 1차원 배열로 저장.
#2by1
right = tensor.Tensor([5,6], [2,1])
#2by1
result = tensor.create_matrix_product( left, right ) # 반드시 연산 결과를 저장할 공간을 만들어야 함. (객체 생성을 명시적으로 하기 위해서)

tensor.matmul(left, right, result) # 내부적으로 계산도 1차원적으로 계산함.
#or
#result = tensor.matmul(left, right, result)
~

만약 C = A + B + 1을 할 때, 반복문이 A + B와 (A + B) + 1를 하면서 2번 반복되는데, 이를 function을 통해 아래의 방법으로 해결 가능함.

예)
~
import tensor
#2by2
left = tensor.Tensor([1,2,3,4], [2,2])
#2
right = tensor.Tensor([5,6], [2])
#2by2
result = tensor.create_element_wise_product( left, right )

# C = A + B를 하면서 같은 루프에 +1까지 같이 하기 위한 코드
def customized_add( left, right ):
	return left + right + 1

# 3번째 인수에 함수를 넘김으로 써, 루프 한번에 계산을 함.
tensor.function_element_wise(left, right, customized_add, result)
~