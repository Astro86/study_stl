# set 컨테이너

## 생성자

|             |                              |
| :---------- | :--------------------------- |
| set s       | 비어있는 set 컨테이너를 생성한다.         |
| set s(s2)   | 복사생성자를 이용해 s2의 복사본인 s를 생성한다. |
| set s(b, e) | 이터레이터를 이용해서 set을 생성한다.       |

## 멤버 함수

|                |                         |
| :------------- | :---------------------- |
| s.clear()      | set s의 모든 원소를 지운다.      |
| s.empty()      | set s가 비었는지 조사한다.       |
| s.insert(b, e) | 이터레이터를 이용해 s에 값을 추가한다.  |
| s.size()       | set s의 크기를 반환한다.        |
| s.swap(s2)     | set s와 set s2를  swap한다. |

## 반환값이 있는 멤버 함수

|                       |                                                                                       |
| :-------------------- | :------------------------------------------------------------------------------------ |
| p = s.begin()         | set s의 시작 이터레이터를 반환한다.                                                                |
| p = s.end()           | set s의 종료 이터레이터를 반환한다.                                                                |
| p = s.rbegin()        | set s의 역순으로 시작하는 이터레이터를 반환한다.                                                         |
| p = s.rend()          | set s의 역순으로 끝나는 이터레이터를 반환한다.                                                          |
| n = s.count(k)        | set s에 원소 k의 개수를 반환한다.                                                                |
| q = s.erase(p)        | set s에 p가 가르키는 원소를 제거한다.                                                              |
| q = s.erase(b, e)     | 이터레이터를 이용해 set s에서 [b, e)범위를 삭제한다.                                                    |
| n = s.erase(k)        | set s에서 k 원소를 삭제한다.                                                                   |
| p = s.find(k)         | set s에서 원소 k가 있는지 확인한 후 이터레이터를 반환한다. 없으면 s.end()를 반환한다.                               |
| pr = s.insert(k)      | set s에 원소 k를 삽입한다. (반환 값은 pair : first는 원소 k의 이터레이터, second는 성공여부)                    |
| q = s.insert(p, k)    | 이터레이터 p가 가르키는 위치부터 시작해 k를 삽입한다.                                                       |
| pr = s.equal_range(k) | set s에 원소 k와 같은 값을 같는 범위를 반환한다.(반환 값은 pair : first는 lower_bound, second는 upper_bound) |
| p = s.lower_bound(k)  | k의 시작 구간을 가르키는 이터레이터를 반환한다.                                                           |
| p = s.upper_bound(k)  | k의 끝 구간을 가르키는 이터레이터를 반환한다.                                                            |
| n = s.max_size()      | set s에 넣을 수 있는 최대의 원소의 갯수를 반환한다.                                                      |
| pred = s.key_comp()   | s의 정렬 기준을 반환한다.                                                                       |
| pred = s.value_comp() | set s의 value 정렬기준을 반환한다.                                                              |

# map 컨테이너

|             |                              |
| :---------- | :--------------------------- |
| map m       | 비어있는 set 컨테이너를 생성한다.         |
| map m(s2)   | 복사생성자를 이용해 s2의 복사본인 s를 생성한다. |
| map m(b, e) | 이터레이터를 이용해서 set을 생성한다.       |

## 멤버 함수

|                |                         |
| :------------- | :---------------------- |
| m.clear()      | map m의 모든 원소를 지운다.      |
| m.empty()      | map m가 비었는지 조사한다.       |
| m.insert(b, e) | 이터레이터를 이용해 m에 값을 추가한다.  |
| m.size()       | map m의 크기를 반환한다.        |
| m.swap(m2)     | map m와 map m2를  swap한다. |

## 반환값이 있는 멤버 함수

|                       |                                                                                            |
| :-------------------- | :----------------------------------------------------------------------------------------- |
| p = m.begin()         | map m의 시작 이터레이터를 반환한다.                                                                     |
| p = m.end()           | map m의 종료 이터레이터를 반환한다.                                                                     |
| p = m.rbegin()        | map m의 역순으로 시작하는 이터레이터를 반환한다.                                                              |
| p = m.rend()          | map m의 역순으로 끝나는 이터레이터를 반환한다.                                                               |
| n = m.count(k)        | map m에 원소 k의 개수를 반환한다.                                                                     |
| q = m.erase(p)        | map m에 p가 가르키는 원소를 제거한다.                                                                   |
| q = m.erase(b, e)     | 이터레이터를 이용해 map m에서 [b, e)범위를 삭제한다.                                                         |
| n = m.erase(k)        | map m에서 k 원소를 삭제한다.                                                                        |
| p = m.find(k)         | map m에서 원소 k가 있는지 확인한 후 이터레이터를 반환한다. 없으면 m.end()를 반환한다.                                    |
| pr = m.insert(k)      | map m에 원소 k를 삽입한다. (반환 값은 pair : first는 원소 k의 이터레이터, second는 성공여부)                         |
| q = m.insert(p, k)    | 이터레이터 p가 가르키는 위치부터 시작해 k를 삽입한다.                                                            |
| pr = m.equal_range(k) | map m에 원소 k와 같은 (key)값을 같는 범위를 반환한다.(반환 값은 pair : first는 lower_bound, second는 upper_bound) |
| p = m.lower_bound(k)  | (key) k의 시작 구간을 가르키는 이터레이터를 반환한다.                                                          |
| p = m.upper_bound(k)  | (key) k의 끝 구간을 가르키는 이터레이터를 반환한다.                                                           |
| n = m.max_size()      | map m에 넣을 수 있는 최대의 원소의 갯수를 반환한다.                                                           |
| pred = m.key_comp()   | s의 정렬 기준을 반환한다.                                                                            |
| pred = m.value_comp() | map m의 value 정렬기준을 반환한다.                                                                   |