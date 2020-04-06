# 연산자 오버로딩

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    void operator+(Point arg) {
    }
};
void main() {
    Point p1(2, 3), p2(5, 5);

    p1 + p2;  // => p1.operator+( p2 ); 와 같습니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() { cout << x << ',' << y << endl; }
    void operator+(Point arg) {
        cout << "operator+() 함수 호출" << endl;
    }
};
void main() {
    Point p1(2, 3), p2(5, 5);

    p1 + p2;  // => p1.operator+( p2 ); 와 같습니다.
}
```

```cpp
#include <iostream>
using namespace std;
class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    void operator+(const Point& arg) {
        Point pt;
        pt.x = this->x + arg.x;
        pt.y = this->y + arg.y;
    }
};
void main() {
    Point p1(2, 3), p2(5, 5);

    p1 + p2;
}
```

```cpp
#include <iostream>
using namespace std;
class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    const Point operator+(const Point& arg) const {
        Point pt;
        pt.x = this->x + arg.x;
        pt.y = this->y + arg.y;

        return pt;
    }
};
void main() {
    Point p1(2, 3), p2(5, 5);
    Point p3;

    p3 = p1 + p2;  // 컴파일러가 p1.operator+(p2)로 해석해서 호출함!
    p3.Print();
    p3 = p1.operator+(p2);  // 직접 호출함!
    p3.Print();
}
```

## 단항 연산자 오버로딩
```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    void operator++()  // 전위 ++
    {
    }
    void operator++(int)  // 후위 ++
    {
    }
};
void main() {
    Point p1(2, 3), p2(2, 3);

    ++p1;  // p1.operator++(); 와 같습니다.

    p2++;  // p2.operator++(0); 와 같습니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    const Point& operator++()  // 전위 ++
    {
        x++;
        y++;
        return *this;
    }
    const Point operator++(int)  // 후위 ++
    {
        Point pt(x, y);
        ++x;
        ++y;
        return pt;
    }
};
void main() {
    Point p1(2, 3), p2(2, 3);
    Point result;

    result = ++p1;  // p1.operator++(); 와 같습니다.
    p1.Print();
    result.Print();

    result = p2++;  // p2.operator++(0); 와 같습니다.
    p2.Print();
    result.Print();
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    const Point& operator--()  // 전위 --
    {
        x--;
        y--;
        return *this;
    }
    const Point operator--(int)  // 후위 --
    {
        Point pt(x, y);
        --x;
        --y;
        return pt;
    }
};
void main() {
    Point p1(2, 3), p2(2, 3);
    Point result;

    result = --p1;  // p1.operator--(); 와 같습니다.
    p1.Print();
    result.Print();

    result = p2--;  // p2.operator--(0); 와 같습니다.
    p2.Print();
    result.Print();
}

//#include <iostream>
//using namespace std;
//
//class Point
//{
//    int x;
//    int y;
//public:
//    Point(int _x =0 , int _y =0 ):x(_x),y(_y) { }
//    void Print( ) const { cout << x <<',' << y << endl; }
//    bool operator== (const Point& arg) const
//    {
//      return x==arg.x && y==arg.y ? true : false;
//    }
//};
//void main( )
//{
//    Point p1(2,3), p2(5,5), p3(2,3);
//
//    if( p1 == p2 )  // p1.operator== (p2) 와 같습니다.
//      cout << "p1 == p2" << endl;
//    if( p1 == p3 )  // p1.operator== (p3) 와 같습니다.
//      cout << "p1 == p3" << endl;
//}
```

## 이항 연산자 오버로딩
```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    bool operator==(const Point& arg) const {
        return x == arg.x && y == arg.y ? true : false;
    }
};
void main() {
    Point p1(2, 3), p2(5, 5), p3(2, 3);

    if (p1 == p2)  // p1.operator== (p2) 와 같습니다.
        cout << "p1 == p2" << endl;
    if (p1 == p3)  // p1.operator== (p3) 와 같습니다.
        cout << "p1 == p3" << endl;
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    bool operator==(const Point& arg) const {
        return x == arg.x && y == arg.y ? true : false;
    }
    bool operator!=(const Point& arg) const {
        return !(*this == arg);
    }
};
void main() {
    Point p1(2, 3), p2(5, 5), p3(2, 3);

    if (p1 != p2)  // p1.operator!= (p2) 와 같습니다.
        cout << "p1 != p2" << endl;
    if (p1 != p3)  // p1.operator!= (p3) 와 같습니다.
        cout << "p1 != p3" << endl;
}
```

## 전역 함수를 이용한 연산자 오버로딩

### 멤버 함수를 이용한 연산자 오버로딩
```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    int GetX() const { return x; }  // x의 getter
    int GetY() const { return y; }  // y의 getter
    const Point operator-(const Point& arg) const {
        return Point(x - arg.x, y - arg.y);
    }
};
void main() {
    Point p1(2, 3), p2(5, 5);
    Point p3;

    p3 = p1 - p2;

    p3.Print();
}
```

### 전역 함수를 이용한 연산자 오버로딩
```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    int GetX() const { return x; }  // x의 getter
    int GetY() const { return y; }  // y의 getter
    //friend const Point operator- (const Point& argL, const Point& argR);
};
const Point operator-(const Point& argL, const Point& argR) {
    return Point(argL.GetX() - argR.GetX(), argL.GetY() - argR.GetY());
}
//friend 함수를 이용한 방법
//const Point operator- (const Point& argL, const Point& argR)
//{
//    return Point( argL.x-argR.x, argL.y-argR.y );
//}
void main() {
    Point p1(2, 3), p2(5, 5);
    Point p3;

    p3 = p1 - p2;

    p3.Print();
}
```

## STL에 필요한 주요 연산자 오버로딩
```cpp
#include <iostream>
using namespace std;

struct FuncObject {
   public:
    void operator()(int arg) const {
        cout << "정수 : " << arg << endl;
    }
};
void Print1(int arg) {
    cout << "정수 : " << arg << endl;
}
void main() {
    void (*Print2)(int) = Print1;
    FuncObject Print3;

    Print1(10);  // 첫째, 함수 호출
    Print2(10);  // 둘째, 함수 호출
    Print3(10);  // 첫째, 함수 호출 Print3.operator(10)을 호출
}
```

```cpp
#include <iostream>
using namespace std;

struct FuncObject {
   public:
    void operator()(int arg) const {
        cout << "정수 : " << arg << endl;
    }
    void operator()(int arg1, int arg2) const {
        cout << "정수 : " << arg1 << ',' << arg2 << endl;
    }
    void operator()(int arg1, int arg2, int arg3) const {
        cout << "정수 : " << arg1 << ',' << arg2 << ',' << arg3 << endl;
    }
};

void main() {
    FuncObject print;
    print(10);  //객체 생성 후 호출(암시적)
    print(10, 20);
    print(10, 20, 30);
    cout << endl;

    print.operator()(10);  //객체 생성 후 호출(명시적)
    print.operator()(10, 20);
    print.operator()(10, 20, 30);
    cout << endl;

    FuncObject()(10);  //임시 객체로 호출(암시적)
    FuncObject()(10, 20);
    FuncObject()(10, 20, 30);
    cout << endl;

    FuncObject().operator()(10);  //객체 생성 후 호출(명시적)
    FuncObject().operator()(10, 20);
    FuncObject().operator()(10, 20, 30);
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
    int operator[](int idx) const {
        if (idx == 0)
            return x;
        else if (idx == 1)
            return y;
        else
            throw "이럴 수는 없는 거야!";
    }
};
void main() {
    Point pt(1, 2);

    pt.Print();

    cout << pt[0] << ','    // pt.operator[](0) 호출
         << pt[1] << endl;  // pt.operator[](1) 호출
}
```

```cpp
#include <iostream>
using namespace std;

class Array {
    int *arr;
    int size;
    int capacity;

   public:
    Array(int cap = 100) : arr(0), size(0), capacity(cap) {
        arr = new int[capacity];
    }
    ~Array() {
        delete[] arr;
    }
    void Add(int data) {
        if (size < capacity)
            arr[size++] = data;
    }
    int Size() const {
        return size;
    }
    int operator[](int idx) const {
        return arr[idx];
    }
};

void main() {
    Array ar(10);

    ar.Add(10);
    ar.Add(20);
    ar.Add(30);
    for (int i = 0; i < ar.Size(); i++)
        cout << ar[i] << endl;  // ar.operator[](i) 와 같습니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Array {
    int* arr;
    int size;
    int capacity;
    // 복사 함수 생략(복사 생성자,복사 대입 연산자)
   public:
    Array(int cap = 100) : arr(0), size(0), capacity(cap) {
        arr = new int[capacity];
    }
    ~Array() {
        delete[] arr;
    }
    void Add(int data) {
        if (size < capacity)
            arr[size++] = data;
    }
    int Size() const {
        return size;
    }
    int operator[](int idx) const {
        return arr[idx];
    }
    int& operator[](int idx) {
        return arr[idx];
    }
};

void main() {
    Array ar(10);
    ar.Add(10);
    ar.Add(20);
    ar.Add(30);

    cout << ar[0] << endl;  // ar.operator[](int) 를 호출합니다.
    cout << endl;

    const Array& ar2 = ar;
    cout << ar2[0] << endl;  // ar.operator[](int) const 를 호출합니다.
    cout << endl;

    ar[0] = 100;  // ar.operator[](int) 를 호출합니다.
    //ar[1] = 100; 에러! 상수 객체(값)를 리턴하므로 대입할 수 없습니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};
void main() {
    Point *p1 = new Point(2, 3);  //메모리 할당
    Point *p2 = new Point(5, 5);  //메모리 할당

    p1->Print();  //p1의 멤버 함수 호출(서비스 사용)
    p2->Print();  //p2의 멤버 함수 호출(서비스 사용)

    delete p1;  //메모리 제거
    delete p2;  //메모리 제거
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};
class PointPtr {
    Point *ptr;

   public:
    PointPtr(Point *p) : ptr(p) {}
    ~PointPtr() {
        delete ptr;
    }
};
void main() {
    PointPtr p1 = new Point(2, 3);  //메모리 할당
    PointPtr p2 = new Point(5, 5);  //메모리 할당

    //p1->Print(); // 아직 서비스 사용 못함!
    //p2->Print(); // 아직 서비스 사용 못함!

    //p1의 소멸자에서 Point 동적 객체를 자동 메모리 제거합니다.
    //p2의 소멸자에서 Point 동적 객체를 자동 메모리 제거합니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};
class PointPtr {
    Point *ptr;

   public:
    PointPtr(Point *p) : ptr(p) {}
    ~PointPtr() {
        delete ptr;
    }
    Point *operator->() const {
        return ptr;
    }
};
void main() {
    PointPtr p1 = new Point(2, 3);  //메모리 할당
    PointPtr p2 = new Point(5, 5);  //메모리 할당

    p1->Print();  //p1.operator->()->Print() 호출 (서비스 사용)
    p2->Print();  //p2.operator->()->Print() 호출 (서비스 사용)
    //p1의 소멸자에서 Point 동적 객체를 자동 메모리 제거합니다.
    //p2의 소멸자에서 Point 동적 객체를 자동 메모리 제거합니다.
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};
class PointPtr {
    Point* ptr;

   public:
    PointPtr(Point* p) : ptr(p) {}
    ~PointPtr() {
        delete ptr;
    }
    Point* operator->() const {
        return ptr;
    }
    Point& operator*() const {
        return *ptr;
    }
};
void main() {
    Point* p1 = new Point(2, 3);    //일반 포인터
    PointPtr p2 = new Point(5, 5);  //스마트 포인터

    p1->Print();  //p1->Print() 호출
    p2->Print();  //p2.operator->()->Print() 호출
    cout << endl;

    (*p1).Print();  //(*p1).Print() 호출
    (*p2).Print();  //p1.operator*().Print() 호출

    delete p1;
    //p2의 소멸자에서 Point 동적 객체를 자동 메모리 제거합니다.
}
```

## 타입 변환 연산자 오버로딩

### 생성자를 이용한 타입 변환
```cpp
#include <iostream>
using namespace std;

class A {
};
class B {
   public:
    B() { cout << "B() 생성자" << endl; }
    B(A& _a) { cout << "B(A _a) 생성자" << endl; }
    B(int n) { cout << "B(int n) 생성자" << endl; }
    B(double d) { cout << "B(double d) 생성자" << endl; }
};
void main() {
    A a;
    int n = 10;
    double d = 5.5;

    B b;    // B() 생성자 호출
    b = a;  // b = B(a) 암시적 생성자 호출 후 대입
    b = n;  // b = B(n) 암시적 생성자 호출 후 대입
    b = d;  // b = B(d) 암시적 생성자 호출 후 대입
}
```

```cpp
#include <iostream>
using namespace std;

class Point {
    int x;
    int y;

   public:
    Point(int _x = 0, int _y = 0) : x(_x), y(_y) {}
    void Print() const { cout << x << ',' << y << endl; }
};

void main() {
    Point pt;
    pt.Print();

    pt = 10;  // Point(10,0) 암시적 생성자 호출
    pt.Print();
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

void main() {
    Point pt;
    pt.Print();

    //pt = 10; // 에러! 암시적 생성자 호출이 불가능!
    pt = Point(10);  // 이렇게 명시적 생성자 호출만 가능!
    pt.Print();
}
```

### 타입 변환 연산자 오버로딩을 이용한 타입 변환
```cpp
#include <iostream>
using namespace std;

class A {
};
class B {
   public:
    operator A() {
        cout << "operator A() 호출" << endl;
        return A();
    }
    operator int() {
        cout << "operator int() 호출" << endl;
        return 10;
    }
    operator double() {
        cout << "operator double() 호출" << endl;
        return 5.5;
    }
};
void main() {
    A a;
    int n;
    double d;

    B b;
    a = b;  //b.operator A() 암시적 호출
    n = b;  //b.operator int() 암시적 호출
    d = b;  //b.operator double() 암시적 호출

    cout << endl;
    a = b.operator A();       // 명시적 호출
    n = b.operator int();     // 명시적 호출
    d = b.operator double();  // 명시적 호출
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
    operator int() const {
        return x;
    }
};
void main() {
    int n = 10;

    Point pt(2, 3);
    n = pt;  // pt.operator int() 암시적 호출
    cout << n << endl;
}
```