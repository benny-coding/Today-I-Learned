## EC2 서버에 프로젝트를 배포해 보자
  ### 배포 스크립트 만들기
  - 배포 과정
    - git clone 혹은 git pull을 통해 새 버전의 프로젝트 받음
    - Gradle이나 Maven을 통해 프로젝트 테스트와 빌드
    - EC2 서버에서 해당 프로젝트 실행 및 재실행
  - 배포 때마다 개발자가 하나하나 명령어를 실행하는 불편함이 많다.

  - 쉘 스크립트
    - __REPOSITORY=/home/ec-user/app/step1__
      - 프로젝트 디렉토리 주소는 스크립트 내에서 자주 사용하는 값이기 때문에 변수로 저장합니다.
      - 마찬가지로 PROJECT_NAME=freelec=springboot2-webservice도 동일하게 __변수로__ 저장합니다.
      - 쉘에서는 __타입 없이__ 선언하여 저장합니다.
      - 쉘에서는 $ 변수명으로 변수를 사용할 수 있습니다.
    - __cd $REPOSITORY/$PROJECT_NAME/__
      - 제일 처음 git clone 받았던 디렉토리로 이동합니다.
      - 바로 위의 쉘 변수 설명을 따라 /home/ec2-user/app/step1/freelec-springboot2-webservice 주소로 이동합니다.
    - __git pull__
      - 디렉토리 이동 후, master 브랜치의 최신 내용을 받습니다.
    - __./gradlew build__
      - 프로젝트 내부의 gradlew로 build를 수행합니다.
    - __cp ./build/libs/*.jar $REPOSITORY/__
      - build의 결과물인 jar 파일을 복사해 jar 파일을 모아둔 위치로 복사합니다.
    - __CURRENT_PID=$(pgrep -f springboot-webservice)__
      - 기존에 수행 중이던 스프링 부트 애플리케이션을 종료합니다.
      - pgrep은 process id만 추출하는 명령어입니다.
      - -f 옵션은 프로세스 이름을 찾습니다.
    - __if ~ else ~ fi__
      - 현재 구동 중인 프로세스가 있는지 없는지를 판단해서 기능을 수행합니다.
      - process id 값으 보고 프로세스가 있으면 해당 프로세스를 종료합니다.
    - __JAR_NAME=$(ls -tr $REPOSITORY/ | grep *.jar | tail -n 1)__
      - 새로 실행할 jar 피일명을 찾습니다.
      - 여러 jar 파일이 생기기 때문에 tail -n로 가장 나중의 jar 파일(최신 파일)을 변수에 저장합니다.
    - __nohup java -jar $REPOSITORY/$JAR_NAME 2>&1 &__
      - 찾은 jar 파일명으로 해당 jar 파일을 nohup으로 실행합니다.
      - 스프링 부트의 장점으로 특별히 외장 톰캣을 설치할 필요가 없습니다.
      - 내장 톰캣을 사용해서 jar 파일만 있으면 바로 웹 애플리케이션 서버를 실행할 수 있습니다.
      - 일반적으로 자바를 실행할 때는 java -jar라는 명령어를 사용하지만, 이렇게 하면 사용자가
        터미널 접속을 끊을 때 애플리케이션도 같이 종료됩니다.
      - 애플리케이션 실행자가 터미널을 종료해도 애플리케이션은 계속 구동될 수 있도록
        nohup 명령어를 사용합니다.
    - __-Dspring.config.location__
      - 스프링 설정 파일 위치를 지정합니다.
      - 기본 옵션들을 담고 있는 application.properties과 OAuth 설정들을 담고 있는
        application-oauth.properties의 위치를 지정합니다.
      - classpath가 붙으면 jar 안에 있는 resources 디렉토리를 기준으로 경로가 생성됩니다.
      - application-oauth.properties는 절대경로를 사용합니다.
        외부에 파일이 있기 때문입니다.


