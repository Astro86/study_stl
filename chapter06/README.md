# vector 컨테이너

## 생성자

| 생성자           | 설명                                                 |
| :------------ | :------------------------------------------------- |
| vector v      | 빈 컨테이너를 생성한다.                                      |
| vector v(n)   | vector v는 기본값으로 초기화된 n개의 원소를 갖는다.                  |
| vector v(n,x) | vector v는 x값으로 초기화된 n개의 원소를 갖는다.                   |
| vector v(v2)  | vector v는 vector v2 컨테이너의 복사본이다.(복사 생성자 호출)        |
| vector v(b,e) | 이터레이터를 이용해 vector v를 생성한다.(특정 구간을 복사하려고 할 때 사용한다.) |

## 멤버 함수

| 멤버함수            | 설명                                              |
| :-------------- | :---------------------------------------------- |
| v.assign(n,x)   | vector v에 x값으로 n개의 원소를 할당한다.                    |
| v.assign(b,e)   | 이터레이터를 이용해 vector v를 만든다.                       |
| v.at(i)         | vector v의 i번째 원소를 참조한다.                         |
| v.back()        | vector v의 마지막 원소를 참조한다.                         |
| v.clear()       | vector v의 모든 원소를 제거한다.                          |
| v.empty()       | vector v가 비었는지 조사한다.                            |
| v.front()       | vector v의 첫 번째 원소를 참조한다.                        |
| v.insert(p,n,x) | p가 가르키는 위치에 n개의 x값을 삽입한다.                       |
| v.pop_back()    | vector v의 마지막 원소를 제거한다.                         |
| v.push_back(x)  | vector v의 끝에 x를 추가한다.                           |
| v.reserve(n)    | n개의 원소를 저장할 공간을 예약한다.                           |
| v.resize(n)     | vector v의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화한다. |
| v.size()        | vector v의 원소의 개수                                |
| v.swap(v2)      | vector v와 vector v2를 swap한다.                    |

## 반환 값이 있는 멤버 함수

|                   |                                    |
| :---------------- | :--------------------------------- |
| p = v.begin()     | vector v의 시작 이터레이터를 반환한다.          |
| p = v.end()       | vector v의 마지막 이터레이터를 반환한다.         |
| p = v.rbegin()    | vector v를 역순으로 시작하는 위치를 반환한다       |
| p = v.rend()      | vector v를 역순으로 끝나는 위치를 반환한다.       |
| q = v.erase(p)    | p가 가르키는 원소를 제거하고 현재 위치를 반환한다.      |
| q = v.erase(b,e)  | [b, e)구간의 원소를 전부 제거한다.             |
| q = v.insert(p,x) | p가 가르키는 위치에 x값을 삽입하고 해당 위치를 반환한다.  |
| x = v.capacity()  | vector v에 할당된 공간의 크기를 반환한다.        |
| x = v.max_size()  | vector v가 담을 수 있는 최대 원소의 개수를 반환한다. |