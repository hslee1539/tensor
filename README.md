# tensor
������ �ټ� ��Ű��

������ ������ ���ο����� ����

## ��Ű�� ���
N���� �ټ��� 1���� �迭�� �����ϰ� ������.
�����׿� �ʿ��� matmul, transpose, element-wise, axis ��ȯ ����� �ϴ� �ڵ带 ���� ����.
�� ��� �ڵ���� ���� ��꿡 �ʿ��� ���� ������ �и���.
�� ��� �ڵ���� �� ��Ű���� computing ��Ű���� �ְ�, �� ��Ű���� ���� ����� tensor Ŭ������ ���� ������ �����̶� �ٸ� tensor ���� Ŭ������ ���� ������.
���� tensor ������ ������ ���Ժ���, �Ϲ� ����, �� �ϳ��� �ʱ�ȭ ���� ������ ��.
����ϴ� �ܺ� ��Ű���� random�� ���
matmul�� element-wise ����� ������ �Լ��� ���� Ŀ���� ������ �� �� ����.

����������, numpy�� ���� ����� ���鼭 ���� ��Ģ�� ã�� �����̶�, �� ��� �˰����� �´����� �� �׽�Ʈ �غ��� ��.

## ��Ű�� ��ġ �ϴ� ��
�� ��Ű���� ����� .py�� �ִ� ������ �� ��Ű�� ������ �����ϰų�,
sys.path�� ��ϵ� ���� �� ��Ű�� ������ ����.


## ��Ű�� ��� ���
�� ��Ű�� ���� �̸����� import. ( __init__.py�� ��Ű���� ��� ����� import��)
Tensor(array, shape)���� ��ü�� �����, array�� shape�� ��� 1���� �迭�� �;� ��.
������ ���� �ݵ�� ������ ���� ���� ������ ��.

��)
~
import tensor
#2by2
left = tensor.Tensor([1,2,3,4], [2,2]) # array�� shape�� ��� 1���� �迭�� ����.
#2by1
right = tensor.Tensor([5,6], [2,1])
#2by1
result = tensor.create_matrix_product( left, right ) # �ݵ�� ���� ����� ������ ������ ������ ��. (��ü ������ ��������� �ϱ� ���ؼ�)

tensor.matmul(left, right, result) # ���������� ��굵 1���������� �����.
#or
#result = tensor.matmul(left, right, result)
~

���� C = A + B + 1�� �� ��, �ݺ����� A + B�� (A + B) + 1�� �ϸ鼭 2�� �ݺ��Ǵµ�, �̸� function�� ���� �Ʒ��� ������� �ذ� ������.

��)
~
import tensor
#2by2
left = tensor.Tensor([1,2,3,4], [2,2])
#2
right = tensor.Tensor([5,6], [2])
#2by2
result = tensor.create_element_wise_product( left, right )

# C = A + B�� �ϸ鼭 ���� ������ +1���� ���� �ϱ� ���� �ڵ�
def customized_add( left, right ):
	return left + right + 1

# 3��° �μ��� �Լ��� �ѱ����� ��, ���� �ѹ��� ����� ��.
tensor.function_element_wise(left, right, customized_add, result)
~