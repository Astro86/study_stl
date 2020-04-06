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