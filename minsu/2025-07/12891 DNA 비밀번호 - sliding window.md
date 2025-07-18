# 12891 DNA 비밀번호 - sliding window

[](https://www.acmicpc.net/problem/12891)

## 문제 조건

- (1 ≤ |P| ≤ |S| ≤ 1,000,000)

## 풀이 과정

문자열 중 연속되는 부분 문자열을 구하는 문제라 전체 문자열에서 부분 문자열을 한 칸씩 이동하며 조건을 만족하는지 확인하는 방식을 사용했습니다. 문제 조건에서 (1 ≤ |P| ≤ |S| ≤ 1,000,000)이라 했기 떄문에 시간 복잡도는 O(n)인 알고리즘을 사용해도 무방합니다.

## 코드

```java
/**
 * 12891 DNA 비밀번호
 *
 * s(문자열 길이), p(부분문자열 길이), line(문자열), mDna(최소 기준 배열), dna(각 문자 개수 배열), count(조건을 만족하는 dna 개수)
 * for(s만큼 반복) {
 *     문자열 받기
 * }
 * needs(mDna) 받기
 *
 * for(0~p까지 반복) {
 *     첫 부분 문자열 받기
 *     dna 배열에 문자열의 각 문자 개수 저장하기
 * }
 * if ( 최소 개수 이상일때 ) count 증가
 * 
 * for(i -> 1~s-p까지 반복) {
 *     line[i-1] 제거 및 C 갱신
 *     line[i+p-1] 추가 및 C 갱신
 *
 *     if ( 최소 개수 이상일때 ) count 증가
 * }
 */
class Main
{
    static int[] dna;
    static int[] mDna;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        int s = Integer.parseInt(st.nextToken());
        int p = Integer.parseInt(st.nextToken());
        int count = 0;

        String line = br.readLine();

        dna = new int[4];
        mDna = new int[4];

        st = new StringTokenizer(br.readLine());
        for(int i=0; i<4; i++) {
            mDna[i] = Integer.parseInt(st.nextToken());
        }

        for(int i=0; i<p; i++) {
            char c = line.charAt(i);
            add(c);
        }

        if ( isCheck() ) {
            count++;
        }

        for(int i=0; i<s-p; i++) {
            remove(line.charAt(i));
            add(line.charAt(i+p));
            if ( isCheck() ) {
                count++;
            }
        }

        System.out.println(count);
    }
    public static void add(char ch) {
        if ( ch == 'A' ) {
            dna[0]++;
        } else if ( ch == 'C' ) {
            dna[1]++;
        } else if ( ch == 'G' ) {
            dna[2]++;
        } else if ( ch == 'T' ) {
            dna[3]++;
        }
    }
    public static void remove(char ch) {
        if ( ch == 'A' ) {
            dna[0]--;
        } else if ( ch == 'C' ) {
            dna[1]--;
        } else if ( ch == 'G' ) {
            dna[2]--;
        } else if ( ch == 'T' ) {
            dna[3]--;
        }
    }
    public static boolean isCheck() {
        for(int i=0; i<4; i++) {
            if ( mDna[i] > dna[i] ) {
                return false;
            }
        }
        return true;
    }
}
```