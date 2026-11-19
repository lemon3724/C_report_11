1. scanf 및 보안   
```C   
#define CRT_SECURE_NO_WARNINGS //C에서 발생하는 모든 경고 무시
#include <stdio.h>
#include <string.h>

int main(void)
{
  char s[100];

  printf("문장 입력: ");
  scanf_s("%[^\n]", s); //\n이 입력으로 들어오기 전 까지 문자를 입력 받음

  //문자열을 반대로 출력 (s-1부터 시작해서 0까지 이므로)
  for(int i = (int)strlen(s)-1; i >= 0; i--)
  {
    printf("%c", str[i]);
  }

  return 0;
}
```

2. 함수의 포인터   
```C
#include <stdio.h>

int add(int a, int b)
{
  return a+b;
}

int main(void)
{
  int a = 11, b = 22;
  int (*sum)(int, int) = add; //포인터를 활용해 add라는 함수를 sum으로 선언
  printf("%d", sum(a, b)); //선언한 sum으로 add를 호출

  return 0;
}
```

3. 2차원 배열
```C
#include <stdio.h>

int main(void)
{
  int a[3][4] = {1, 2, 3, 4,
                  5, 6, 7, 8,
                  9, 10, 11, 12}; //3열 4행의 2차원 배열 선언 (직관적인 이해를 위해 이런 형태로 선언함)
  int s;
  for(int i = 0; i < 3; i++)
  {
    for(int j = 0; j < 4; j++)
    {
      s += a[i][j]; //i번째 열 j번째 행에 있는 숫자를 덧셈
    }
  }

  printf("%d", s);

  return 0;
}
```

4. 구조체로 2명의 3과목 성적을 생성해서 binary형태로 my.bin에 저장
```C
#define CRT_SECURE_NO_WARNINGS
#include <stdio.h>

struct s{
  int k, e, m;
}; //int 변수 3개를 가진 구조체 선언

int main(void)
{
  struct s a[2] = {{80, 90, 85}, {70, 75, 95}}; //각 배열에 있는 구조체에 값 지정
  FILE *p = fopen("my.bin", "wb"); //my.bin 이라는 파일을 쓰기(write)+binary 모드로 열기
  fwrite(a, sizeof(struct s), 2, p); //a의 시작 주소, 구조체 s만큼 할당, s 안에서 2개 선택, 파일 포인터 p를 가져와 데이터를 작성
  fclose(p); //파일 닫기

  return 0;
}
```

5. 파일을 읽고 개인 평균 및 과목 평균 출력
```C
#define CRT_SECURE_NO_WARNINGS
#include <stdio.h>

struct s{
  int k, e, m;
};

int main(void)
{
  struct s a[2];
  FILE *p fopen("my.bin", "rb"); //my.bin 이라는 파일을 읽기(read)+binary 모드로 열기
  fread(a, sizeof(struct s), 2, p); //a의 시작 주소, 구조체 s만큼 할당, s 안에서 2개 선택, 파일 포인터 p를 가져와 데이터를 읽어옴
  fclose(p); //파일 닫기

  printf("개인 1: %.2f, 개인 2: %.2f\n", (a[0].k + a[0].e + a[0].m) / 3.0, (a[1].k + a[1].e + a[1].m) / 3.0);
  printf("과목 1: %.2f, 과목 2: %.2f, 과목 3: %.2f\n", (a[0].k + a[1].k) / 2.0, (a[0].e + a[1].e) / 2.0, (a[0].e + a[1].e) / 2.0);

  return 0;
}
```

6. 버블 정렬
```C
#include <stdio.h>

int main(void)
{
  int a[] = {2, 4, 1, 5, 3}; //정렬되어 있지 않은 배열

  for(int i = 0; i < 4; i++)
  {
    for(int j = 0; j < 4-i; j++)
    {
      if(a[j] > a[j+1]) //만약 뒤에 앞에 있는 값이 뒤에 있는 값보다 크다면 정렬 진행
      {
        int t = a[j];
        a[j] = a[j+1];
        a[j+1] = t;
      }
    }
  }
  //정렬 완료 (시간복잡도 O(n^2))

  for(int i = 0; i < 5; i++)
  {
    printf("%d ", a[i]);
  }

  return 0;
}
```

7. 정수형 변수 저장 후 합을 계산 후 출력
```C
#include <stdio.h>

int main(void)
{
  int a = 22, b = 33;
  printf("%d", a+b);

  return 0;
}
```

8. 명령행 인자로 두 정수를 입력 받아 합을 출력
```C
#include <stdio.h>

int main(int argc, char *argv[])
{
  //입력 받은 명령 인자가 2개일 경우 2개를 출력
  if(argc == 2)
  {
    printf("%d %d", argv[1], argv[2]);
  }

  return 0;
}
```

9. 반복문을 사용해 5~10까지 정수를 더한 값 출력
```C
#include <stdio.h>

int main(void)
{
  int a = 0;
  for(int i = 5; i <= 10; i++)
  {
    a += i;
  }
  printf("%d", a);

  return 0;
}
```

10. 동적 메모리 할당을 활용해 정수 3개를 할당 받은 후 합을 출력
```C
#include <stdio.h>
#include <strlib.h>

int main(void)
{
  int *a = (int*)malloc(sizeof(int)*3); //포인터 변수 a에 int 크기 만큼 3개를 할당
  *(a+0) = 11; //포인터 변수를 배열처럼 활용
  *(a+1) = 33;
  *(a+2) = 55;
  printf("%d", *(a+0)+*(a+1)+*(a+2));

  return 0;
}
```

11. 3명의 성적(kr, en)을 구조체로 초기화하고 개인별 평균 구하기 (대상: JCShim, GDHong, JYKo)
```C
#include <stdio.h>

//student 라는 이름의 구조체 선언
typedef struct student{
  char name[10];
  int kr, en;
};

int main(void)
{
  //구조체를 s라는 이름으로 3개의 배열 형태로 저장
  student s[3] = {("JCShim", 100, 85), ("GDHong", 95, 80), ("JYKo", 90, 75)};

  for(int i = 0; i < 3; i++)
  {
    //구조체 내부 자료형인 int를 float로 형변환 후 계산하여 출력
    printf("%s 평균: %.2f\n", s[i].name, ((float)s[i].kr + (float)s[i].en) / 2.0);
  }

  return 0;
}
```
