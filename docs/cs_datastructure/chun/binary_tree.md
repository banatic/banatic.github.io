---
layout: default
title: 이진 검색 트리
nav_order: 1
parent: 자료구조 천인국
grand_parent: 자료구조
use_math: true
last_modified_date: 2020-08-29T07:18:08+0900
---

# 트리

# 이진 트리

자식 노드의 개수가 2이하인 트리

공집합 이거나 루트와 왼쪽 서브트리, 오른쪽 서브트리로 구성된 노드들의 유한 집합, 이진 트리의 서브트리들은 모두 이진 트리여야 한다.

- 이진 트리의 성질
    1. n개의 노드를 가진 이진트리는 n-1개의 간선을 가진다.
    2. 높이가 h인 이진트리의 경우 최소 h개의 노드를 가지며 최대 2^h - 1 개의 노드를 가진다. 

## 포화 이진 트리

단말 노드를 제외한 모든 노드의 자식 노드의 개수가 2인 트리

모든 레벨이 꽉차 있어야 한다.

## 완전 이진 트리

단말 노드가 비어 있을 수 있지만 왼쪽에서 부터 순서대로 있어야 한다. 중간에 빈곳이 없어야 한다.

그외 이진 트리...

노드 i의 부모 노드 인덱스  =  i 

노드 i의 왼쪽 자식 노드 인덱스 = 2 * i

노드 i의 오른쪽 자식 노드 인덱스  = 2 * i  + 1

# 이진트리 순회 (순환적)

전위순회(preorder traversal) : VLR

중위순회(inorder traversal)    : LVR

후위순회(postorder traversal) : LRV

## 레벨 순회

큐를 이용한다. 레벨에 있는 모든 노드를 순회하고 다음 레벨로 넘어간다.

## 이진트리의 높이 구하기

왼쪽과 오른쪽 서브트리의 높이의 최대값을 구하는 방식을 이용, 순환적 풀이

# 스레드 이진트리

이진트리에는 많은 NULL 링크가 존재하게 되는데 이 널 링크에 중위 순회 시에 선행 노드인 중위 선행자 (inorder predecessor) 나 중위 순회 시에 후속 노드인 중위 후속자(inorder successor)를 저장 시켜 놓은 트리가 스레드 이진 트리이다.

# 이진 탐색 트리 (binary search tree)

- 모든 원소의 키는 유일한 키를 가진다.
- 왼쪽 서브 트리 키들은 루트 키보다 작다.
- 오른쪽 서브 트리의 키들은 루트 키보다 크다.
- 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리이다.

## 이진 탐색 트리 노드 탐색

```c
//이진 트리 탐색 함수 순환 사용(recursive)
TreeNode * search(TreeNode * node, int key)
{
	if (node == NULL) return NULL;
	if (key == node->key) return node;
	else if (key < node->key)
			return search(node->left);
	else
			return search(node->right);
```

```c
// 이진 트리 탐색 함수 반복 사용 (iterative)
TreeNode *search(TreeNode * node, int key)
{
	while (node != NULL)
	{
		if (key == node->key) return node;
		if (key < node->key) node  = node->left;
		else node = node->right;	
	}
	return NULL;
}
```

## 이진 탐색 트리의 노드 삽입

- 이진 탐색 트리에 노드를 삽입하기 위해서는 일단 탐색을 해야 한다. 왜냐하면 탐색을 실패하는 곳이 삽입할 곳이기 때문이다.

```c
// 이진 탐색 트리의 노드 삽입 순환적 구현
TreeNode * insert(TreeNode * node, int key)
{
	if (node == NULL) return new_node(key);
	if (key < node->key) node->left = insert(node->left, key);
	else node->right = insert(node->right, key);
	return node;
}
// 새로운 노드를 만드는 유틸리티 함수
TreeNode * new_node(int item)
{
	TreeNode * temp = (TreeNode *)malloc(sizeof(TreeNode));
	temp->key = item;
	temp->left = temp->right = NULL;
	return temp;
}
```

## 이진 탐색 트리의 노드 삭제

- 세가지 경우를 고려해야 한다.
    1. 삭제하려는 경우가 단말 노드인 경우
    2. 삭제하려는 노드가 왼쪽이나 오른쪽 서브 트리 중 하나만 가지고 있는 경우
    3. 삭제하려는 노드가 왼쪽, 오른쪽 서브 트리 두개다 가지고 있는 경우

1. 삭제하려는 경우가 단말 노드인 경우
    - 단말 노드만 간단히 연결을 끊으면된다. (부모의 가리키는 노드를 널로 하고 동적 할당을 해제 한다.)
2. 삭제하는 노드가 왼쪽이나 오른쪽 서브 트리 중 하나만 가지고 있는 경우
    - 자기 노드는 삭제하고 왼쪽이나 오른쪽 노드를 붙여주면 된다.
3. 삭제하려는 노드가 왼쪽, 오른쪽 서브 트리 두 개 다 가지고 있는 경우
    - 삭제하는 노드와 가장 가까운 후계자를 선택한다. 왼쪽 서브트리에서 제일 큰 노드를 선택해도 되고 오른쪽 서브트리에서 제일 작은 노드를 선택해도 된다. 제일 큰 노드는 트리를 중위 순회했을 때 삭제할 노드의 선행 노드와 후속 노드에 해당한다.

    ```c
    // 이진 탐색 트리와 키가 주어지면 키가 저장된 노드를 삭제하고 새로운 루트 노드를 반환한다.
    TreeNode * delete(TreeNode * node, int key)
    {
        if (node == NULL) return NULL;
        
        // 만약 키가 루트보다 작다면 왼쪽 서브트리에 있는 것이다
        if (key < node->data) node->left = delete(node->left, key);
        // 키가 루트보다 크다면 오른쪽 서브트리에 있는 것이다.
        else if (key > node->key) node->right = delete(node->right, key);
        // 같으면 이 노드 삭제
        else 
        {
            // 첫번째나 두번째 경우
            if (node->left == NULL)
            {
                TreeNode * temp = node->right;
                free(node);
                return temp;
            }
            else if (node->right == NULL)
            {
                TreeNode * temp = node->left;
                free(node);
                return temp;
            }
            // 세번째 경우
            TreeNode * temp = min_value(node->right);
            
            // 중위 순회시 후계 노드를 복사한다.
            node->key = temp->key;
            // 중위 순회시 후계노드를 삭제한다.
            node->right = delete(node->right, temp->key);
        }
        return node;
    }

    // 주어진 탐색트리에서 최소 키값을 갖는 노드를 찾아서 반환
    TreeNode * min_value(TreeNode * node)
    {
       TreeNode * current = node;
       // 오른쪽 트리중 최소 단말 노드 찾으러 내려김
       while (current != NULL)
            current = current->left;
       return current;
    }
    ```

# 균형 이진 탐색 트리

## AVL 트리

- 각 노드의 왼쪽 서브 트리의 높이와 오른쪽 서브트리의 높이 차이가 1 이하인 이진 탐색 트리
- 비균형 상태가 되면 노드를 재배치 하여 균형을 맞춘다.
- 모든 연산이 로그에 끝난다.
- 균형인수 (balance factor) : (왼쪽 서브트리 높이 - 오른쪽 서브트리 높이)
- 모든 노드의 균형 인수가 -1, 0, 1 이면 AVL 트리이다.
- 균형을 이루는 AVL 트리의 균형이 깨질때는 삽입, 삭제 연산을 수행할 때 이다.

### AVL 트리의 탐색

- 이진 탐색 트리와 동일하다.

### AVL 트리의 삽입

- 삽입되는 위치에서 루트까지의 경로에 있는 조상 노드들의 균형인수에 영향을 준다.
- 새로운 노드가 삽입되고 불균형 상태로 변한 가장 가까운 조상 노드의 서브트리에 대해서 다시 균형을 잡아야 한다.

불균형 경우에 따라 LL RR RL LR 로 나뉜다. 

각 경우에 따라 로테이트 하는 방식이 다르다 

오른쪽 로테이트와 왼쪽 로테이트가 있다 이 둘을 잘 혼합하여 균형을 맞춘다. 

오른쪽 회전 함수

```c
// right rotate function 
AVLnode * right_rotate(AVLnode * parent)
{
    AVLnode * child = parent->left;
    parent->left = child->right;
    // ^ child의 양쪽 노드가 생기니까 원래 있던 child의 오른쪽 서브트리를 옮겨줘야 하는데
    // 오른쪽 서브트리를 옮기기 적당한 곳은 이제 막 왼쪽 노드를 잃어서 왼쪽이 비어있고 
    // child 키보다 큰 녀석들이지만 parent 보다는 작기 때문에 parent->left 에 이어준다.
    child->right = parent;
    return child;
}
```

왼쪽 회전 함수

```c
AVLnode * left_rotate(AVLnode * parent)
{
    AVLnode * child = parent->right;
    parent->right = child->left;
    // 위의 오른쪽 회전 함수의 이유와 같음
    child->left = parent;
    return child;
}
```
