# Acwing 算法基础课

## 第一章 基础算法

### [785. 快速排序](https://www.acwing.com/problem/content/787/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/785-%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F.png)

```cpp
#include <iostream>
using namespace std;
const int N = 1E5 + 10;

int n;
int a[N];

void quick_sort(int l, int r) {
    if(l >= r) return;
    
    int i = l - 1, j = r + 1, x = a[l + r >> 1];
    while(i < j) {
        do i ++; while(a[i] < x);
        do j --; while(a[j] > x);
        if(i < j) swap(a[i], a[j]);
    }
    
    quick_sort(l, j);
    quick_sort(j + 1, r);
}

int main() {
    cin >> n;
    for(int i = 0; i < n; i ++ ) cin >> a[i];
    quick_sort(0, n - 1);
    for(int i = 0; i < n; i ++ ) cout << a[i] << ' ';
    
    return 0;
}
```

### [786. 第k个数](https://www.acwing.com/problem/content/788/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/786-%E7%AC%ACk%E4%B8%AA%E6%95%B0.png)

```cpp
#include <iostream>
using namespace std;
const int N = 1E5 + 10;

int n, k;
int a[N];

int quick_sort(int l, int r, int k) {
    if(l >= r) return a[l];
    
    int i = l - 1, j = r + 1, x = a[l + r >> 1];
    while(i < j) {
        do i ++; while(a[i] < x);
        do j --; while(a[j] > x);
        if(i < j) swap(a[i], a[j]);
    }
    
    if(k <= j - l + 1) return quick_sort(l, j, k);
    else return quick_sort(j + 1, r, k - (j - l + 1));
}

int main() {
    cin >> n >> k;
    for(int i = 0; i < n; i ++ ) cin >> a[i];
    cout << quick_sort(0, n - 1, k);
    
    return 0;
}
```

### [787. 归并排序](https://www.acwing.com/problem/content/789/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/787-%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F.png)

```cpp
#include <iostream>
using namespace std;

const int N = 1E5 + 10;

int n;
int a[N], t[N];

void merge_sort(int l, int r) {
    if(l >= r) return;
    
    int mid = l + r >> 1;
    merge_sort(l, mid);
    merge_sort(mid + 1, r);
    
    int k = 0, i = l, j = mid + 1;
    while(i <= mid and j <= r)
        a[i] < a[j] ? t[k ++ ] = a[i ++ ] : t[k ++ ] = a[j ++ ];
    while(i <= mid) t[k ++ ] = a[i ++ ];
    while(j <= r) t[k ++ ] = a[j ++ ];
    for(int i = l, j = 0; i <= r; i ++, j ++ )
        a[i] = t[j];
}

int main() {
    cin >> n;
    for(int i = 0; i < n; i ++ ) cin >> a[i];
    merge_sort(0, n - 1);
    for(int i = 0; i < n; i ++ ) cout << a[i] << ' ';
    
    return 0;
}
```

### [788. 逆序对的数量](https://www.acwing.com/problem/content/790/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/788-%E9%80%86%E5%BA%8F%E5%AF%B9%E7%9A%84%E6%95%B0%E9%87%8F.png)

```cpp
#include <iostream>
using namespace std;

const int N = 1E5 + 10;

int n;
int a[N], t[N];

long long merge_sort(int l, int r) {
    if(l >= r) return 0ll;
    
    long long res = 0;
    int mid = l + r >> 1;
    res += merge_sort(l, mid);
    res += merge_sort(mid + 1, r);
    
    int k = 0, i = l, j = mid + 1;
    while(i <= mid and j <= r)
        a[i] <= a[j] ? t[k ++ ] = a[i ++ ] : (res += mid - i + 1, t[k ++ ] = a[j ++ ]);
    while(i <= mid) t[k ++ ] = a[i ++ ];
    while(j <= r) t[k ++ ] = a[j ++ ];
    for(int i = l, j = 0; i <= r; i ++, j ++ )
        a[i] = t[j];
    return res;
}

int main() {
    cin >> n;
    for(int i = 0; i < n; i ++ ) cin >> a[i];
    cout << merge_sort(0, n - 1);
    
    return 0;
}
```

### [789. 数的范围](https://www.acwing.com/problem/content/791/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/789-%E6%95%B0%E7%9A%84%E8%8C%83%E5%9B%B4.png)

```cpp
#include <iostream>
using namespace std;

const int N = 1E5 + 10;

int n, m, x;
int a[N];

int main() {
    cin >> n >> m;
    for(int i = 0; i < n; i ++ ) cin >> a[i];
    while(m -- ) {
        cin >> x;
        int l = 0, r = n - 1;
        
        while(l < r) {
            int mid = l + r >> 1;
            if(a[mid] >= x) r = mid;
            else l = mid + 1;
        }
        
        if(a[l] != x) {
            cout << "-1 -1\n";
            continue;
        } 
        cout << l << ' ';
        
        l = 0, r = n - 1;
        while(l < r) {
            int mid = l + r + 1 >> 1;
            if(a[mid] <= x) l = mid;
            else r = mid - 1;
        }
        cout << l << endl;
    }
    
    return 0;
}
```

### [790. 数的三次方根](https://www.acwing.com/problem/content/792/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/790-%E6%95%B0%E7%9A%84%E4%B8%89%E6%AC%A1%E6%96%B9%E6%A0%B9.png)

```cpp
#include <iostream>
using namespace std;

const double eps = 1E-8;

double n;

int main() {
    cin >> n;
    double l = -100, r = 100; 
    
    while(r - l >= eps) {
        double mid = (l + r) / 2;
        if(mid * mid * mid >= n) r = mid;
        else l = mid;
    }
    
    printf("%.6f", l);
    
    return 0;
}
```

### [791. 高精度加法](https://www.acwing.com/problem/content/793/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/791-%E9%AB%98%E7%B2%BE%E5%BA%A6%E5%8A%A0%E6%B3%95.png)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<int> ADD(vector<int> &A, vector<int> &B) {
    vector<int> C;
    int t = 0;
    for(int i = 0; i < A.size() or i < B.size() or t; i ++ ) {
        if(i < A.size()) t += A[i];
        if(i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());
    
    vector<int> A, B;
    for(int i = 0; i < a.size(); i ++ ) A.push_back(a[i] - '0');
    for(int i = 0; i < b.size(); i ++ ) B.push_back(b[i] - '0');

    vector<int> C = ADD(A, B);
    for(int i = C.size() - 1; i >= 0; i -- ) cout << C[i];
    return 0;
}
```

### [792. 高精度减法](https://www.acwing.com/problem/content/794/)

![](https://raw.githubusercontent.com/qqcykbz001/acwing/main/792-%E9%AB%98%E7%B2%BE%E5%BA%A6%E5%87%8F%E6%B3%95.png)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

vector<int> SUB(vector<int> &A, vector<int> &B) {
    vector<int> C;
    int t = 0;
    for(int i = 0; i < A.size(); i ++ ) {
        t = A[i] - t;
        if(i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if(t < 0) t = 1;
        else t = 0;
    }
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}

bool operator< (string &a, string &b) {
    if(a.size() != b.size()) return a.size() < b.size();
    for(int i = 0; i < a.size(); i ++ ) 
        if(a[i] != b[i])
            return a[i] < b[i];
    return false;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    if(a < b) {
        cout << "-";
        swap(a, b);
    }
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());
    vector<int> A, B;
    for(int i = 0; i < a.size(); i ++ ) A.push_back(a[i] - '0');
    for(int i = 0; i < b.size(); i ++ ) B.push_back(b[i] - '0');

    vector<int> C = SUB(A, B);
    for(int i = C.size() - 1; i >= 0; i -- ) cout << C[i];
    return 0;
}
```



