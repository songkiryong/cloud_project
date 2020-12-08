# CloudComputing Project

## 목표 : AWS Ec2와 Ubuntu 가상서버를 이용하여 코딩테스트 프로그램 & 웹 구현 
### [Ubuntu 가상서버] - 코딩 테스트 웹 구현
### 1. docker 설치 & 컨테이너 구동
- sudo su - // root로 이동 ( docker는 root권한이 있어야 실행 O )
- curl -fsSL https://get.docker.com/ | sudo sh
- docker version // 설치 여부 확인
![alt text](version.PNG)
- Nginx 이미지로 컨테이너 실행

	// docker image pull nginx

	// docker container run -d -p 12345:80 nginx

- docker container ls // 컨테이너 상태 확인
![alt text](12345.PNG)

- mkdir /home/sp~/workspace_docker/www/ 
- index.html 작성
- host pc 웹 페이지 저장 디렉토리 
<-> Nginx 디렉토리 

	// docker container run -v $PWD:/usr/share/nginx/html -d -p 54323:80 nginx
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
- C 
#### - c_easy
![alt text](c_e.PNG)
#### - c_normal
![alt text](c_n.PNG)
#### - c_hard
![alt text](c_h1.PNG)
![alt text](c_h2.PNG)

- JAVA 
#### - java_easy
![alt text](j_e.PNG)
#### - java_normal
![alt text](j_n.PNG)
#### - java_hard
![alt text](j_h1.PNG)
![alt text](j_h2.PNG)
![alt text](j_h3.PNG)

- PYTHON 
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
![alt text](ph2.PNG)
![alt text](ph3.PNG)
![alt text](ph4.PNG)


### [AWS EC2] - 코딩 테스트 정답 확인 프로그램 구현
### 1. AWS 인스턴스 생성
#### - http포트 규칙 추가

![alt text](addport.PNG)


***
### 2. putty -> SSH연결
#### - 패키지 설치
- gcc
- //  apt-get update
- // apt-get install gcc

***
### 3. 코딩 테스트 정답 확인 프로그램 구현
#### - cloud.c
#### `code`
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int option_mode() {
	int opt;


	printf("=====Select mode=====\n");
	printf("1.easy\n");
	printf("2.normal\n");
	printf("3.hard\n");
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
	printf("입력 : ");
	scanf("%d",&opt);

	return opt;
}

void read_file(char* file) {
	char buffer[BUFSIZ];
	int size;
	int count;
	

	FILE *fp=fopen(file,"r");
	fseek(fp,0,SEEK_END);
	size=ftell(fp);
	fseek(fp,0,SEEK_SET);
	fread(buffer,size,1,fp);
	printf("%s",buffer);
	fclose(fp);
}


void c() {

	int opt;
        opt=option_mode();
        char file[BUFSIZ];
	switch(opt) {
		case 1:
			//easy file open
			strcpy(file,"c_easy.txt");
			read_file(file);
		break;
		case 2:
			//normal file open
		break;
		case 3:
			//hard file open
		break;

		
	}
      
}

void java() {

	int opt;
        opt=option_mode();

	switch(opt) {
		case 1:
			//easy file open
		break;
		case 2:
			//normal file open
		break;
		case 3:
			//hard file open
		break;
	}
}

void python() {

	int opt;
        opt=option_mode();

	switch(opt) {
		case 1:
			//easy file open
		break;
		case 2:
			//normal file open
		break;
		case 3:
			//hard file open
		break;
	}
}

int main(void) {
	int opt;
	
	opt=option_language();

	switch(opt) {
		case 1:
		c();
		break;

		case 2:
		java();
		break;

		case 3:
		python();
		break;
	}
}

```


