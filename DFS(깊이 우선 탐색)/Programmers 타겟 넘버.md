# Programmers [타겟 넘버](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

### 난이도 ★★

---

#### 문제 설명

> n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
>
> ```
> -1+1+1+1+1 = 3
> +1-1+1+1+1 = 3
> +1+1-1+1+1 = 3
> +1+1+1-1+1 = 3
> +1+1+1+1-1 = 3
> ```
>
> 사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

#### 접근 방식

> `DFS`,` BFS` 로 접근할 수 있는 문제입니다.
>
> 간단하게 인덱스 번호를 증가해서 배열에 모든 숫자를 써야 되는 문제이니 배열의 길이와 비교해주고 타겟 넘버랑 같은 지 확인 합니다.

#### 풀이

```java
class Solution {
    static int answer = 0;
    public int solution(int[] numbers, int target) {
        dfs(0, numbers, target, 0);
        return answer;
        // return bfs(numbers, target);
    }
    private static void dfs(int idx, int[] num, int tg, int sum){
        if (idx == num.length){
            if(tg == sum){
                answer++;
            }
            return ;
        }
        dfs(idx+1, num, tg, sum+num[idx]);
        dfs(idx+1, num, tg, sum-num[idx]);
    }
    private static void dfs(int idx, int[] num, int tg, int sum){
        if (idx == num.length){
            if(tg == sum){
                answer++;
            }
            return ;
        }
        dfs(idx+1, num, tg, sum+num[idx]);
        dfs(idx+1, num, tg, sum-num[idx]);
    }
    private static int bfs(int[] num, int tg){
        Queue<Pair> q = new LinkedList<>();
        q.add(new Pair(0, num[0]));
        q.add(new Pair(0, num[0] * -1));
        int result = 0;
        while(!q.isEmpty()){
            Pair p = q.poll();
            if (p.idx == num.length -1){
                if (p.sum == tg){
                    result++;
                }
                continue;
            }
            int newIdx = p.idx +1;
            if(newIdx >= num.length){
                continue;
            }
            q.add(new Pair(newIdx, p.sum + num[newIdx]));
            q.add(new Pair(newIdx, p.sum + num[newIdx] * -1));
        }
        return result;
    }
    private static class Pair{
        int idx;
        int sum;
        public Pair(int idx, int sum){
            this.idx = idx;
            this.sum = sum;
        }
    }
}
```

