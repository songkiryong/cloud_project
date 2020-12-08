# CloudComputing Project

## 목표 : AWS Ec2와 Ubuntu 가상서버를 이용하여 코딩테스트 프로그램 & 웹 구현 
### [Ubuntu 가상서버] - 코딩 테스트 웹 구현
### 1. docker 설치 & 컨테이너 구동
- sudo su - 

	`// root로 이동 ( docker는 root권한이 있어야 실행 O )`

- curl -fsSL https://get.docker.com/ | sudo sh
- docker version 

	`// 설치 여부 확인`

![alt text](version.PNG)

- Nginx 이미지로 컨테이너 실행

	`// docker image pull nginx`

	`// docker container run -d -p 12345:80 nginx`

- docker container ls 

	`// 컨테이너 상태 확인`
![alt text](12345.PNG)

- mkdir /home/sp~/workspace_docker/www/ 
- index.html 작성
- host pc 웹 페이지 저장 디렉토리 
<-> Nginx 디렉토리 

	`// docker container run -v $PWD:/usr/share/nginx/html -d -p 54323:80 nginx`

	![alt text](54323.PNG)

### 2. <.html> 코드 작성
#### 웹 구현 html
- index.html
![alt text](index.PNG)
- about.html
![alt text](a.PNG)
- how.html
![alt text](h1.PNG)
![alt text](h2.PNG)
- code.html
![alt text](c1.PNG)
![alt text](c2.PNG)
![alt text](c3.PNG)

#### 프로그래밍 문제 시각화 html
- `C` 
#### - c_easy
![alt text](c_e.PNG)
#### - c_normal
![alt text](c_n.PNG)
#### - c_hard
![alt text](c_h1.PNG)
![alt text](c_h2.PNG)

- `JAVA` 
#### - java_easy
![alt text](j_e.PNG)
#### - java_normal
![alt text](j_n.PNG)
#### - java_hard
![alt text](j_h1.PNG)
![alt text](j_h2.PNG)
![alt text](j_h3.PNG)

- `PYTHON` 
#### - python_easy
![alt text](p_e.PNG)
#### - python_normal
![alt text](p_n.PNG)
#### - python_hard
![alt text](p_h.PNG)

### 3. 웹 구현 결과물 
#### PC
![alt text](home.PNG)
![alt text](about.PNG)
![alt text](how.PNG)
![alt text](code.PNG)
- easy -> 문제 초록색 표시
![alt text](easy.PNG)
- normal -> 문제 파란색 표시
![alt text](normal.PNG)
- hard -> 문제 빨간색 표시
![alt text](hard.PNG)
#### Phone 
![alt text](ph1.jpg)
![alt text](ph2.jpg)
![alt text](ph3.jpg)
![alt text](ph4.jpg)



### [AWS EC2] - 코딩 테스트 정답 확인 프로그램 구현
### 1. AWS 인스턴스 생성
![alt text](instance.png)

***
### 2. putty -> SSH연결
#### - 프라이빗 키 설정
- .pem -> .ppk 
	
	`//puttygen 이용`
#### - 패키지 설치
- gcc

	`//  apt-get update`

	`// apt-get install gcc`

***
### 3. 코딩 테스트 정답 확인 프로그램 구현
#### - cloud_p.c
#### `code`
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

int option_mode() {
        int opt;


        printf("=====Select mode=====\n");
        printf("1.easy\n");
        printf("2.normal\n");
        printf("3.hard\n");
        printf("4.이전으로\n");
        printf("입력 : ");

        scanf("%d", &opt);
        return opt;
}


int option_language() {
        int opt;

        printf("====Select language====\n");
        printf("1. C\n");
        printf("2. Python\n");
        printf("3. Java\n");
        printf("4. quit\n");
        printf("입력 : ");
        scanf("%d",&opt);

        return opt;
}


void result_file(char *result){
        char str[256];
        struct tm *st,*et;
        time_t start,end;
        unsigned int hour;
        unsigned int min;
        int sec;
start=time(NULL);//문제시작할때 시간
        printf("warning : 정답을 입력할 때는 띄어쓰기를 하지 마세요.\n");
        printf("< 정답 입력 > : ");
        scanf("%s" , str);
        end=time(NULL);//답변제출할때 시간
        sec=end-start;
        hour=(sec)/3600;
        min=((sec)-(hour*3600))/60;
        sec=sec-((hour*3600)+(min*60));


        if(strcmp(result,str)==0){
                printf("정답입니다.\n");
                printf("소요된 시간 : %d:%d:%d\n",hour,min,sec);

         }
        else{
                printf("\t오답입니다.\n");
                printf("\t(정답) %s\n", result);
                printf("소요된 시간 : %d:%d:%d\n",hour,min,sec);

         }

}



void c() {

        int opt;
        opt=option_mode();
        switch(opt) {
                case 1:
                        //easy
                        result_file("10");
                break;
                case 2:
                        //normal
                        result_file("a|c=0x%x=%d");
                break;

                case 3:
                        //hard
	result_file("add함수의주소:%x");
                case 4:
                        option_language();

                break;


        }

}

void java() {

        int opt;
        opt=option_mode();

        switch(opt) {
                case 1:
                        //easy
                        result_file("sc.nextInt()");
                break;
                case 2:
                        //normal
                        result_file("i++<=n");
                break;
                case 3:
                        //hard
                        result_file("Cal().start()");
                case 4:
                        option_language();
                break;
        }
}

void python() {
        int opt;
        opt=option_mode();
        switch(opt) {
                case 1:
                        //easy
                        result_file("len");

                break;

case 2:
                        //normal
                        result_file("x:0");

                break;
                case 3:
                        //hard
                        result_file("(set(range(1,5000))");

                case 4:
                        option_language();


                break;
        }
}

int main(void) {
        int opt;
        opt=option_language();
while(1) {
        switch(opt) {
                case 1:
                c();
                break;

                case 2:
                python();
                break;

                case 3:
                java();
                break;

                case 4:
                printf("------QUIT PROGRAM--------\n");
                exit(1);
        }
}
}
```

#### - 컴파일

	 gcc -o cloud_p cloud_p.c

#### - 파일 실행

	 ./cloud_p

#### - 실행 result
` -> 걸린시간 , 정답 / 오답 출력`

![alt text](result.png)


