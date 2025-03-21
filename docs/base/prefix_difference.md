## 一维前缀和

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

## 二维前缀和

## 二维差分