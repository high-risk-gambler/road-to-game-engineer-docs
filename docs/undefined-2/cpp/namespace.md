---
description: C++ namespace 에 대한 간략한 설명
---

# namespace

```

#include <iostream>
#include "header1.h"
#include "header2.h"

using header1::foo; //using 문을 사용해서 명시적으로 header1의 foo()를 사용하도록 지정

namespace { // 익명 네임스페이스를 사용하여 이 파일에서만 접근 가능한 함수와 변수를 정의
    int only_in_this_file = 0;

    int OnlyInThisFile() {return only_in_this_file;}
}

int main()
{
    std::cout << "Hello World!" << std::endl;

    foo(); // using 문을 사용해서 같은 이름을 가진 header1의 foo()을 기본적으로 사용하게 됨 현재 header1 과 header2 에 모두 같은 함수가 선언되어 있음

    OnlyInThisFile(); // 익명 네임스페이스 안에 정의된 함수는 이 파일에서만 접근 가능
    only_in_this_file = 3;  //  익명 네임스페이스 안에 정의된 변수도 이 파일에서만 접근 가능

    return 0;
}



```

네임스페이스 : C++ 코드가 정의된 공간의 이름 정도

header1::foo  이런식으로 해당 namespace::functionName  함수 참조 가능&#x20;

using 문을 사용해서 현재 파일에서 명시적으로 어떤 네임스페이스 내부에 있는 함수를 사용할건지 선택가능함 따라서 우선순위로 사용됨&#x20;

익명 네임스페이스 : 같은 파일 내부에 이름 없는 네임스페이스를 정의한다 위 코드에 `namespace {}` 로 되는것 익명이 아니라면 `namespace 네임스페이스의이름 {}` 같은 형식이 되어야함



\>> 연산자 : 양쪽의 변수가 정수이면 비트 연산 수행 근데 한쪽의 연산자가 스트림이면 스트림내의 오른쪽에 있는 변수 혹은 문자열의 값을 스트림에 추가하는 연산자임

