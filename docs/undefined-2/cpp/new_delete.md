# new\_delete

```cpp
#include <iostream>


int main() {

	//C 언어에서 배열을 생성하고 메모리를 할당하는 방법
	// int arr[5]; // 스택 영역에 배열 생성
	// 정수 5개를 저장할 수 있는 배열을 생성하고 메모리를 할당하는 방법
	int* arr = (int*)malloc(sizeof(int) * 5); // 동적 메모리 할당

	free(arr);

	int* ptr = new int;// new 연산자를 이용해서 동적 메모리 할당 해당 정수 변수의 메모리 주소값이 반환되어 ptr에 저장된다.
	*ptr = 10; // ptr이 가리키는 메모리 공간에 10을 저장한다.

	delete ptr; // new 연산자를 이용해서 동적 메모리 할당한 메모리를 해제한다.

    /*	int a = 5;
	delete& a;*/
	// 스텍 메모리 영역에 존재하는 변수 a의 주소값을 delete 연산자를 이용해서 해제하려하면 런타임 에러 발생함

	int arr_size;
	std::cout << "arr_size: ";
	std::cin >> arr_size;

	// new 연산자를 이용해서 동적 메모리 할당
	int* list = new int[arr_size];

	for (int i = 0; i < arr_size; i++) {
		std::cin >> list[i];
	}
	
	for (int i = 0; i < arr_size; i++) {
		std::cout << "list[" << i << "]: " << list[i] << std::endl;
	}

	delete[] list;// new 연산자를 이용해서 동적 메모리 할당한 배열을 해제할 때는 delete[] 연산자를 사용해야 한다.
	


}
```
