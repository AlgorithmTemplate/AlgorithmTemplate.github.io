## 一维前缀和

一维前缀和可以通过 $O(n)$ 的预处理，在 $O(1)$ 的时间内求出数组中一段区间的和。

#### 模版题

[蓝桥OJ：一维前缀和](https://www.lanqiao.cn/problems/18437/learning/)

#### 代码模版
???+ example "参考实现"
    === "C++"
        ```c++
        #include <iostream>
        using namespace std;
        int a[100010];
        int s[100010];
        int main()
        {
            int n,q;
            scanf("%d %d",&n,&q);
            for(int i=1;i<=n;i++){
                scanf("%d",&a[i]);
                s[i]=a[i]+s[i-1];
            }
            for(int i=1;i<=q;i++){
                int l,r;
                scanf("%d%d",&l,&r);
                printf("%d\n",s[r]-s[l-1]);
            }
            return 0;
        }
        ```
    === "Java"
        ```java
        import java.util.Scanner;

        public class Main {
            public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                int n = sc.nextInt();
                int q = sc.nextInt();
                int[] a = new int[n + 1];
                int[] s = new int[n + 1];

                for (int i = 1; i <= n; i++) {
                    a[i] = sc.nextInt();
                    s[i] = a[i] + s[i - 1];
                }

                for (int i = 1; i <= q; i++) {
                    int l = sc.nextInt();
                    int r = sc.nextInt();
                    System.out.println(s[r] - s[l - 1]);
                }
            }
        }
        ```
    === "Python"
        ```python
        n, q = map(int, input().split())
        a = list(map(int, input().split()))
        s = [0] * (n + 1)

        for i in range(1, n + 1):
            s[i] = a[i - 1] + s[i - 1]

        for _ in range(q):
            l, r = map(int, input().split())
            print(s[r] - s[l - 1])
        ```

## 一维差分

一维差分可以通过 $O(n)$ 的预处理，在 $O(1)$ 的时间内对数组中一段区间的数进行加减。

#### 模版题

[蓝桥OJ：一维差分](https://www.lanqiao.cn/problems/18438/learning/)

#### 代码模版
???+ example "参考实现"
    === "C++"
        ```c++
        #include<bits/stdc++.h>
        using namespace std;
        const int N=2e5+10;
        int a[N],b[N];
        int n,m;
        int main(){
            scanf("%d%d",&n,&m);
            for(int i=1;i<=n;i++){
                scanf("%d",&a[i]);
                b[i]=a[i]-a[i-1];
            }
            for(int i=1;i<=m;i++){
                int l,r,d;
                scanf("%d%d%d",&l,&r,&d);
                b[l]+=d;
                b[r+1]-=d;
            }
            for(int i=1;i<=n;i++){
                b[i]=b[i-1]+b[i];
                printf("%d ",b[i]);
            }
        } 
        ```
    === "Java"
        ```java
        import java.util.Scanner;

        public class Main {
            public static void main(String[] args) {
                Scanner in = new Scanner(System.in);
                int n = in.nextInt();
                int m = in.nextInt();
                long[] a = new long[n + 1];
                long[] b = new long[n + 2];

                for (int i = 1; i <= n; i++) {
                    a[i] = in.nextLong(); // 输入序列
                    b[i] = a[i] - a[i - 1];
                }

                while (m-- > 0) {
                    int l = in.nextInt();
                    int r = in.nextInt();
                    int d = in.nextInt();
                    b[l] += d;
                    b[r + 1] -= d;
                }

                for (int i = 1; i <= n; i++) {
                    b[i] = b[i - 1] + b[i];
                    System.out.print(b[i] + " ");
                }
                System.out.println();
            }
        }
        ```
    === "Python"
        ```python
        import os
        import sys
        n,m=map(int,input().split())
        a=[0]+list(map(int,input().split()))+[0]#len=n+2
        b=[0]*(n+2)
        for i in range(1,n+1):
            b[i]=a[i]-a[i-1]#差分方程

        for i in  range(0,m):
            l,r,d=map(int,input().split())
            b[l]+=d
            b[r+1]-=d

        for i in range(1,n+1):
            b[i]=b[i]+b[i-1]
            print(b[i],end=" ")
        ```

## 二维前缀和
二维前缀和可以通过 $O(n\times m)$ 的预处理，在 $O(1)$ 的时间内求出一个子矩阵的和。
### 模板题
[蓝桥OJ:二维前缀和](https://www.lanqiao.cn/problems/18439/learning)
### 代码模板
???+ example "参考实现"
    === "C++"
        ```c++
        #include <iostream>
        using namespace std;
        int a[1010][1010];
        int s[1010][1010];
        int main()
        {
            int n,m,q;
            scanf("%d %d %d",&n,&m,&q);
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    scanf("%d",&a[i][j]); 
                } 
            } 
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    s[i][j]=a[i][j]+s[i-1][j]+s[i][j-1]-s[i-1][j-1];
                } 
            }
            for(int i=1;i<=q;i++){
                int x1,y1,x2,y2;
                scanf("%d %d %d %d",&x1,&y1,&x2,&y2)
                printf("%d\n",s[x2][y2]-s[x1-1][y2]-s[x2][y1-1]+s[x1-1][y1-1]); 
            }
        }
        ```
    === "Java"
        ```java
        import java.util.Scanner;

        public class Main {
            public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                int n = sc.nextInt();
                int m = sc.nextInt(); 
                int q = sc.nextInt();
                int[][] a = new int[n + 1][m + 1];
                int[][] s = new int[n + 1][m + 1];

                for (int i = 1; i <= n; i++) {
                    for (int j = 1; j <= m; j++) {
                        a[i][j] = sc.nextInt();  
                    }  
                }
                for (int i = 1; i <= n; i++) {
                    for (int j = 1; j <= m; j++) {
                        s[i][j] = a[i][j] + s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1];
                    } 
                }
                for (int i = 1; i <= q; i++) {
                    int x1 = sc.nextInt();
                    int y1 = sc.nextInt();
                    int x2 = sc.nextInt();
                    int y2 = sc.nextInt();
                    System.out.println(s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1] 
                }
            }  
        }
        ```
    === "Python"
        ```python
        n, m, q = map(int, input().split())
        a = [[0] * (m + 1) for _ in range(n + 1)]
        s = [[0] * (m + 1) for _ in range(n + 1)]

        for i in range(1, n + 1):
            row = list(map(int, input().split()))
            for j in range(1, m + 1):
                a[i][j] = row[j - 1]
                s[i][j] = a[i][j] + s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1]

        for _ in range(q):
            x1, y1, x2, y2 = map(int, input().split())
            result = s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1]
            print(result)
        ```
## 二维差分
二维差分可以通过 $O(n\times m)$ 的预处理，在 $O(1)$ 的时间内对一个子矩阵的数进行加减。
### 模板题
[蓝桥OJ:二维差分](https://www.lanqiao.cn/problems/18440/learning)
### 代码模板
???+ example "参考实现"
    === "C++"
        ```c++
        #include <iostream>
        using namespace std;
        int a[1010][1010];
        int b[1010][1010];
        int main()
        {
            int n,m,q;
            scanf("%d %d %d",&n,&m,&q);
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    scanf("%d",&a[i][j]);
                }
            }
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    b[i][j]=a[i][j]-a[i-1][j]-a[i][j-1]+a[i-1][j-1];
                }
            }
            for(int i=1;i<=q;i++){
                int x1,y1,x2,y2,d;
                scanf("%d %d %d %d %d",&x1,&y1,&x2,&y2,&d);
                b[x1][y1]+=d;
                b[x2+1][y1]-=d;
                b[x1][y2+1]-=d;
                b[x2+1][y2+1]+=d; 
            }
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    b[i][j]=b[i][j]+b[i-1][j]+b[i][j-1]-b[i-1][j-1];
                    printf("%d ",b[i][j]);
                }
                printf("\n"); 
            } 
        }
        ```
    === "Java"
        ```java
        import java.util.Scanner;

        public class Main {
            public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                int n = sc.nextInt();
                int m = sc.nextInt();
                int q = sc.nextInt();
                int[][] a = new int[n + 1][m + 1];
                int[][] b = new int[n + 1][m + 1];

                for (int i = 1; i <= n; i++) {
                    for (int j = 1; j <= m; j++) {
                        a[i][j] = sc.nextInt();
                    }
                }

                for (int i = 1; i <= n; i++) {
                    for (int j = 1; j <= m; j++) {
                        b[i][j] = a[i][j] - a[i - 1][j] - a[i][j - 1] + a[i - 1][j - 1];
                    }
                }

                for (int i = 1; i <= q; i++) {
                    int x1 = sc.nextInt();
                    int y1 = sc.nextInt();
                    int x2 = sc.nextInt();
                    int y2 = sc.nextInt();
                    int d = sc.nextInt();
                    b[x1][y1] += d;
                    b[x2 + 1][y1] -= d;
                    b[x1][y2 + 1] -= d;
                    b[x2 + 1][y2 + 1] += d;
                } 
                for (int i = 1; i <= n; i++) {
                    for (int j = 1; j <= m; j++) {
                        b[i][j] = b[i][j] + b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];
                        System.out.print(b[i][j] + " "); 
                    } 
                    System.out.println();
                }
            }  
        }
        ```
    === "Python"
        ```python
        n, m, q = map(int, input().split())
        a = [[0] * (m + 1) for _ in range(n + 1)]
        b = [[0] * (m + 1) for _ in range(n + 1)]

        for i in range(1, n + 1):
            row = list(map(int, input().split()))
            for j in range(1, m + 1):
                a[i][j] = row[j - 1]
                b[i][j] = a[i][j] - a[i - 1][j] - a[i][j - 1] + a[i - 1][j - 1]

        for _ in range(q):
            x1, y1, x2, y2, d = map(int, input().split())
            b[x1][y1] += d
            b[x2 + 1][y1] -= d
            b[x1][y2 + 1] -= d
            b[x2 + 1][y2 + 1] += d

        for i in range(1, n + 1):
            for j in range(1, m + 1):
                b[i][j] = b[i][j] + b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1]
                print(b[i][j], end=" ")
            print()
        ```