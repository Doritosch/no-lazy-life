# 1655 가운데를 말해요 - Priority Queue

[](https://www.acmicpc.net/problem/1655)

## 문제 조건

- 시간 제한 - 0.1 초
- N은 1보다 크거나 같고, 100,000보다 작거나 같은 자연수이다.
- 정수는 -10,000보다 크거나 같고, 10,000보다 작거나 같다.
- 정수를 하나씩 입력할때마다 입력받은 정수들 중에서 중간값을 출력해야한다.

## 풀이 과정

정수를 입력할때마다 중간값을 찾고 갱신하는 방식은 시간 제한 0.1 초를 만족시키지 못할 것 같아서 삽입과 갱신의 시간복잡도가 O(logN)인 우선순위 큐를 사용하여 문제를 해결하려 했습니다.

최대 힙과 최소 힙을 두어 정수를 균형있게 삽입한 뒤, 각 힙의 root 부분을 비교하여 최대 힙에 중간 값 중 작은 값이 들어가게 처리해주었습니다.

```java
class Main
{
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((o1, o2) -> o2-o1);
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for(int i=0; i<n; i++) {
            int num = Integer.parseInt(br.readLine());

            if ( maxHeap.size() == minHeap.size() ) {
                maxHeap.add(num);
            } else {
                minHeap.add(num);
            }

            if ( !maxHeap.isEmpty() && !minHeap.isEmpty() ) {
                if ( maxHeap.peek() > minHeap.peek() ) {
                    int temp = maxHeap.poll();
                    maxHeap.add(minHeap.poll());
                    minHeap.add(temp);
                }
            }
            System.out.println(maxHeap.peek());
        }
    }
}
```