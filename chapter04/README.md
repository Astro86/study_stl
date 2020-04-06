# 템플릿

```cpp
#include <iostream>
using namespace std;

void Print(int a, int b) {
    cout << a << ", " << b << endl;
}
void main() {
    Print(10, 20);
}
```

```cpp
#include <iostream>
using namespace std;

template <typename T>
void Print(T a, T b) {
    cout << a << ", " << b << endl;
}
void main() {
    Print(10, 20);          // 정수 출력
    Print(0.123, 1.123);    // 실수 출력
    Print("ABC", "abcde");  // 문자열 출력
}
```

```cpp
#include <iostream>
using namespace std;

void Print(int a, int b) {
    cout << a << ", " << b << endl;
}
void Print(double a, double b) {
    cout << a << ", " << b << endl;
}
void Print(const char* a, const char* b) {
    cout << a << ", " << b << endl;
}
void main() {
    Print(10, 20);          // 정수 출력
    Print(0.123, 1.123);    // 실수 출력
    Print("ABC", "abcde");  // 문자열 출력
}
```

```cpp
#include <iostream>
using namespace std;

template <typename T>
void Print(T a, T b) {
    cout << a << ", " << b << endl;
}
void main() {
    Print<int>(10, 20);                  // 정수 출력
    Print<double>(0.123, 1.123);         // 실수 출력
    Print<const char*>("ABC", "abcde");  // 문자열 출력
}
```

```cpp
#include <iostream>
using namespace std;

template <typename T1, typename T2>
void Print(T1 a, T2 b) {
    cout << a << ", " << b << endl;
}
void main() {
    Print(10, 1.5);        // 정수, 실수 출력
    Print("Hello!", 100);  // 문자열, 정수 출력
    Print(1.5, "Hello!");  // 실수, 문자열 출력
}
```

```cpp
#include <iostream>
using namespace std;

template <typename T>
void Swap(T &a, T &b) {
    T temp = a;
    a = b;
    b = temp;
}
void main() {
    int n1 = 10, n2 = 20;
    double d1 = 1.1, d2 = 2.2;

    cout << n1 << ", " << n2 << endl;
    Swap(n1, n2);
    cout << n1 << ", " << n2 << endl;
    cout << endl;

    cout << d1 << ", " << d2 << endl;
    Swap(d1, d2);
    cout << d1 << ", " << d2 << endl;
}
```

```cpp
#include <iostream>
using namespace std;

template <typename T, int size>
void PrintArray(T* arr) {
    for (int i = 0; i < size; ++i) {
        cout << "[" << i << "]: " << arr[i] << endl;
    }
    cout << endl;
}
void main() {
    int arr1[5] = {10, 20, 30, 40, 50};
    PrintArray<int, 5>(arr1);  // 명시적 호출

    double arr2[3] = {1.1, 2.2, 3.3};
    PrintArray<double, 3>(arr2);  // 명시적 호출
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    explicit Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};

template <typename T>
void Print(T a) {
    cout << a << endl;
}
void main() {
    int n = 10;
    double d = 2.5;
    Point pt(2, 3);

    Print(n);
    Print(d);
    Print(pt);  //에러! cout << pt; 연산이 불가능하므로
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    explicit Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};
// 일반화 함수 템플릿
template <typename T>
void Print(T a) {
    cout << a << endl;
}
// 특수화 함수 템플릿
template <>
void Print(Point a)  // 명시적인 코드: void Print<Point>(Point a)
{
    cout << "Print 특수화 버전: ";
    a.Print();
}
void main() {
    int n = 10;
    double d = 2.5;
    Point pt(2, 3);

    Print(n);   // Print<int>( n )    일반화 버전 호출
    Print(d);   // Print<double>( d ) 일반화 버전 호출
    Print(pt);  // Print<Point>( pt ) 특수화 버전 호출
}
```

```cpp
#include <iostream>
using namespace std;

class Array {
    int *buf;
    int size;      // 원소의 개수
    int capacity;  // 저장 가능한 메모리 크기
   public:
    explicit Array(int cap = 100) : buf(0), size(0), capacity(cap) {
        buf = new int[capacity];
    }
    ~Array() { delete[] buf; }
    void Add(int data) {
        buf[size++] = data;
    }
    int operator[](int idx) const {
        return buf[idx];
    }
    int GetSize() const {
        return size;
    }
    // 나머지 인터페이스 생략...
};

void main() {
    Array arr;

    arr.Add(10);
    arr.Add(20);
    arr.Add(30);

    for (int i = 0; i < arr.GetSize(); ++i)
        cout << arr[i] << endl;
}
```

```cpp
#include <iostream>
#include <string>  //문자열 string 클래스 헤더
using namespace std;

class IntArray  //정수 Array
{
    int *buf;
    int size;
    int capacity;

   public:
    explicit IntArray(int cap = 100) : buf(0), size(0), capacity(cap) { buf = new int[capacity]; }
    ~IntArray() { delete[] buf; }
    void Add(int data) { buf[size++] = data; }
    int operator[](int idx) const { return buf[idx]; }
    int GetSize() const { return size; }
};
class DoubleArray  //실수 Array
{
    double *buf;
    int size;
    int capacity;

   public:
    explicit DoubleArray(int cap = 100) : buf(0), size(0), capacity(cap) { buf = new double[capacity]; }
    ~DoubleArray() { delete[] buf; }
    void Add(double data) { buf[size++] = data; }
    double operator[](int idx) const { return buf[idx]; }
    int GetSize() const { return size; }
};
class StringArray  //문자열 Array
{
    string *buf;
    int size;
    int capacity;

   public:
    explicit StringArray(int cap = 100) : buf(0), size(0), capacity(cap) { buf = new string[capacity]; }
    ~StringArray() { delete[] buf; }
    void Add(string data) { buf[size++] = data; }
    string operator[](int idx) const { return buf[idx]; }
    int GetSize() const { return size; }
};
void main() {
    IntArray iarr;  // 정수 Array 객체
    iarr.Add(10);
    iarr.Add(20);
    iarr.Add(30);

    for (int i = 0; i < iarr.GetSize(); ++i)
        cout << iarr[i] << " ";
    cout << endl;

    DoubleArray darr;  // 실수 Array 객체
    darr.Add(10.12);
    darr.Add(20.12);
    darr.Add(30.12);

    for (int i = 0; i < darr.GetSize(); ++i)
        cout << darr[i] << " ";
    cout << endl;

    StringArray sarr;  // 문자열 Array 객체
    sarr.Add("abc");
    sarr.Add("ABC");
    sarr.Add("Hello!");

    for (int i = 0; i < sarr.GetSize(); ++i)
        cout << sarr[i] << " ";
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>  //문자열 string 클래스 헤더
using namespace std;

template <typename T>  // 클래스 템플릿 Array 정의
class Array {
    T *buf;
    int size;
    int capacity;

   public:
    explicit Array(int cap = 100) : buf(0), size(0), capacity(cap) {
        buf = new T[capacity];
    }
    ~Array() { delete[] buf; }
    void Add(T data) {
        buf[size++] = data;
    }
    T operator[](int idx) const {
        return buf[idx];
    }
    int GetSize() const {
        return size;
    }
};
void main() {
    Array<int> iarr;  //정수(클라이언트가 T 타입 결정) Array 객체
    iarr.Add(10);
    iarr.Add(20);
    iarr.Add(30);

    for (int i = 0; i < iarr.GetSize(); ++i)
        cout << iarr[i] << " ";
    cout << endl;

    Array<double> darr;  //실수(클라이언트가 T 타입 결정) Array 객체
    darr.Add(10.12);
    darr.Add(20.12);
    darr.Add(30.12);

    for (int i = 0; i < darr.GetSize(); ++i)
        cout << darr[i] << " ";
    cout << endl;

    Array<string> sarr;  //문자열(클라이언트가 T 타입 결정) Array 객체
    sarr.Add("abc");
    sarr.Add("ABC");
    sarr.Add("Hello!");

    for (int i = 0; i < sarr.GetSize(); ++i)
        cout << sarr[i] << " ";
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T = int, int capT = 100>  // int, 100 디폴트 매개 변수 값 지정
class Array {
    T *buf;
    int size;
    int capacity;

   public:
    explicit Array(int cap = capT) : buf(0), size(0), capacity(cap) {
        buf = new T[capacity];
    }
    ~Array() { delete[] buf; }
    void Add(T data) {
        buf[size++] = data;
    }
    T operator[](int idx) const {
        return buf[idx];
    }
    int GetSize() const {
        return size;
    }
};
void main() {
    Array<> iarr;  // 디폴트 매개 변수 값 int, 100 사용
    iarr.Add(10);
    iarr.Add(20);
    iarr.Add(30);

    for (int i = 0; i < iarr.GetSize(); ++i)
        cout << iarr[i] << " ";
    cout << endl;

    Array<double> darr;  // 디폴트 매개 변수 값 100 사용
    darr.Add(10.12);
    darr.Add(20.12);
    darr.Add(30.12);

    for (int i = 0; i < darr.GetSize(); ++i)
        cout << darr[i] << " ";
    cout << endl;

    Array<string, 10> sarr;  // 디폴트 매개 변수 값 사용하지 않음
    sarr.Add("abc");
    sarr.Add("ABC");
    sarr.Add("Hello!");

    for (int i = 0; i < sarr.GetSize(); ++i)
        cout << sarr[i] << " ";
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T>
class ObjectInfo {
    T data;

   public:
    ObjectInfo(const T& d) : data(d) {}
    void Print() {
        cout << "타입 : " << typeid(data).name() << endl;
        cout << "크기 : " << sizeof(data) << endl;
        cout << "값 : " << data << endl;
        cout << endl;
    }
};
void main() {
    ObjectInfo<int> d1(10);
    d1.Print();  // 객체 정보 출력

    ObjectInfo<double> d2(5.5);
    d2.Print();  // 객체 정보 출력

    ObjectInfo<string> d3("Hello!");
    d3.Print();  // 객체 정보 출력
}
```

```cpp
#include <iostream>
using namespace std;
void For_each(int *begin, int *end, void (*pf)(int)) {
    while (begin != end) {
        pf(*begin++);
    }
}
void PrintInt(int n) {
    cout << n << " ";
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};
    For_each(arr, arr + 5, PrintInt);  // 정수 출력
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename IterT, typename Func>
void For_each(IterT begin, IterT end, Func pf) {
    while (begin != end) {
        pf(*begin++);
    }
}
void PrintInt(int data) {
    cout << data << " ";
}
void PrintString(string data) {
    cout << data << " ";
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};
    For_each(arr, arr + 5, PrintInt);  // 정수 출력
    cout << endl;

    string sarr[3] = {"abc", "ABCDE", "Hello!"};
    For_each(sarr, sarr + 3, PrintString);  // 문자열 출력
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename IterT, typename Func>
void For_each(IterT begin, IterT end, Func pf) {
    while (begin != end) {
        pf(*begin++);
    }
}
void PrintInt(int data) {
    cout << data << " ";
}
void PrintString(string data) {
    cout << data << " ";
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};
    For_each<int*, void (*)(int)>(arr, arr + 5, PrintInt);  // 정수 출력
    cout << endl;

    string sarr[3] = {"abc", "ABCDE", "Hello!"};
    For_each<string*, void (*)(string)>(sarr, sarr + 3, PrintString);  // 문자열 출력
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename IterT, typename Func>
void For_each(IterT begin, IterT end, Func pf) {
    while (begin != end) {
        pf(*begin++);
    }
}
template <typename T>
void Print(T data) {
    cout << data << " ";
}
void main() {
    int arr[5] = {10, 20, 30, 40, 50};
    For_each(arr, arr + 5, Print<int>);  // 정수 출력
    cout << endl;

    string sarr[3] = {"abc", "ABCDE", "Hello!"};
    For_each(sarr, sarr + 3, Print<string>);  // 문자열 출력
    cout << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename IterT, typename Func>
void For_each(IterT begin, IterT end, Func pf) {
    while (begin != end) {
        pf(*begin++);
    }
}
template <typename T>
struct PrintFunctor {
    string sep;  // 출력 구분자 정보
   public:
    explicit PrintFunctor(const string& s = " ") : sep(s) {}
    void operator()(T data) const {
        cout << data << sep;
    }
};
void main() {
    int arr[5] = {10, 20, 30, 40, 50};
    For_each(arr, arr + 5, PrintFunctor<int>());
    cout << endl;

    string sarr[3] = {"abc", "ABCDE", "Hello!"};
    For_each(sarr, sarr + 3, PrintFunctor<string>("*\n"));
    cout << endl;
}
```

```cpp
#include <functional>  // STL greater와 less 헤더
#include <iostream>
using namespace std;

template <typename T>
struct Less {
    bool operator()(T a, T b) {
        return a < b;
    }
};
template <typename T>
struct Greater {
    bool operator()(T a, T b) {
        return a > b;
    }
};
void main() {
    cout << Less<int>()(10, 20) << endl;  //사용자 Less, Greater 사용
    cout << Less<int>()(20, 10) << endl;
    cout << Greater<int>()(10, 20) << endl;
    cout << Greater<int>()(20, 10) << endl;
    cout << endl;
    cout << less<int>()(10, 20) << endl;  //STL의 less, greater 사용
    cout << less<int>()(20, 10) << endl;
    cout << greater<int>()(10, 20) << endl;
    cout << greater<int>()(20, 10) << endl;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename RetType, typename ArgType>
class Functor {
   public:
    RetType operator()(ArgType data) {
        cout << data << endl;
        return RetType();
    }
};
void main() {
    Functor<void, int> functor1;
    functor1(10);
    Functor<bool, string> functor2;
    functor2("Hello!");
}
```

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

template <typename T1, typename T2>
struct Pair {
    T1 first;
    T2 second;
    Pair(const T1& ft, const T2& sd) : first(ft), second(sd) {}
};
void main() {
    Pair<int, int> p1(10, 20);
    cout << p1.first << ',' << p1.second << endl;
    Pair<int, string> p2(1, "one");
    cout << p2.first << ',' << p2.second << endl;
    cout << endl;

    pair<int, int> p3(10, 20);  //STL의 pair
    cout << p3.first << ',' << p3.second << endl;
    pair<int, string> p4(1, "one");  //STL의 pair
    cout << p4.first << ',' << p4.second << endl;
    vector<int> v;
}
```