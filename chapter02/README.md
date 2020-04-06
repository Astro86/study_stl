# 함수 포인터

```cpp
#include <iostream>
using namespace std;

void main() {
    int n = 10;
    int *pn = &n;
}
```

```cpp
#include <iostream>
using namespace std;

void Print(int n) {
    cout << "정수: " << n << endl;
}
void main() {
    // void Print(int n)의 함수 포인터 선언
    void (*pf)(int);
    // 함수의 이름은 함수의 시작 주소
    pf = Print;

    Print(10);  //1. 함수 호출
    pf(10);     //2. 포인터를 이용한 함수 호출, 첫 번째 방법
    (*pf)(10);  //3. 포인터를 이용한 함수 호출, 두 번째 방법

    cout << endl;
    cout << Print << endl;
    cout << pf << endl;
    cout << *pf << endl;
}
```

```cpp
#include <iostream>
using namespace std;

void Print() {
    cout << "정적 함수 Print()" << endl;
}
class Point {
   public:
    void Print() {
        cout << "멤버 함수 Print()" << endl;
    }
};
void main() {
    Point pt;
    Point* p = &pt;

    Print();     // 첫째, 정적 함수 호출
    pt.Print();  // 둘째, 객체로 멤버함수 호출
    p->Print();  // 셋째, 주소로 멤버함수 호출
}
```

```cpp
#include <iostream>
using namespace std;

void Print(int n) {
    cout << "전역 함수: " << n << endl;
}
namespace A {
void Print(int n) {
    cout << "namespace A 전역 함수: " << n << endl;
}
}  // namespace A
class Point {
   public:
    static void Print(int n) {
        cout << "Point 클래스의 정적 멤버 함수: " << n << endl;
    }
};
void main() {
    void (*pf)(int);

    Print(10);         // 1. namespace 없는 전역 함수 호출
    A::Print(10);      // 2, namespace A의 전역 함수 호출
    Point::Print(10);  // 3, Point 클래스의 정적 멤버 함수 호출
    cout << endl;

    pf = Print;
    pf(10);  // 1. 함수 포인터로 namespace 없는 전역 함수 호출
    pf = A::Print;
    pf(10);  // 2. 함수 포인터로 namespace A의 전역 함수 호출
    pf = Point::Print;
    pf(10);  // 3. 함수 포인터로 Point 클래스의 정적 멤버 함수 호출
}
```

```cpp
#include <iostream>
using namespace std;

//////// 서버 /////////////
void PrintHello() {
    cout << "Hello!" << endl;
}
/////// 클라이언트 /////////
void main() {
    PrintHello();
}
```

```cpp
#include <iostream>
using namespace std;
void Client();

//////// 서버 /////////////
void PrintHello() {
    cout << "Hello!" << endl;
    Client();  //서버에서 클라이언트 코드 호출
}
/////// 클라이언트 /////////
void Client() {
    cout << "난 client" << endl;
}
void main() {
    PrintHello();  //서버 코드 호출
}
```

```cpp
#include <iostream>
using namespace std;

//////// 서버 /////////////
// 배열의 모든 원소에 반복적인 작업을 하도록 추상화되어 있음(구체적인 작업은 없음)
void For_each(int *begin, int *end, void (*pf)(int)) {
    while (begin != end) {
        pf(*begin++);  // 클라이언트 함수 호출(콜백)
    }
}
/////// 클라이언트 /////////
void Print1(int n)  // 공백을 이용하여 원소를 출력
{
    cout << n << ' ';
}
void Print2(int n)  // 각 원소를 제곱하여 출력
{
    cout << n * n << " ";
}
void Print3(int n)  // 문자열과 endl을 이용하여 원소를 출력
{
    cout << "정수 : " << n << endl;
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};

    For_each(arr, arr + 5, Print1);  // Print1() 콜백 함수의 주소를 전달
    cout << endl
         << endl;
    For_each(arr, arr + 5, Print2);  // Print2() 콜백 함수의 주소를 전달
    cout << endl
         << endl;
    For_each(arr, arr + 5, Print3);  // Print3() 콜백 함수의 주소를 전달
}
```

```cpp
#include <algorithm>  // for_each() 알고리즘(서버)을 사용하기 위한 헤더
#include <iostream>
using namespace std;
/////// 클라이언트 /////////
void Print1(int n)  // 공백을 이용하여 원소를 출력
{
    cout << n << ' ';
}
void Print2(int n)  // 각 원소를 제곱하여 출력
{
    cout << n * n << " ";
}
void Print3(int n)  // 문자열과 endl을 이용하여 원소를 출력
{
    cout << "정수 : " << n << endl;
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};

    for_each(arr, arr + 5, Print1);  // Print1() 콜백 함수의 주소를 전달
    cout << endl
         << endl;
    for_each(arr, arr + 5, Print2);  // Print2() 콜백 함수의 주소를 전달
    cout << endl
         << endl;
    for_each(arr, arr + 5, Print3);  // Print3() 콜백 함수의 주소를 전달
}
```