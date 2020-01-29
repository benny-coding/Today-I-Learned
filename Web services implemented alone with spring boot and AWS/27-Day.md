## 코드가 푸시되면 자동으로 배포해 보자 - Travis CI 배포 자동화
  ### Travis CI와 AWS S3 연동하기
  - __before_deploy__
    - deploy 명령어가 실행되기 전에 수행됩니다.
    - CodeDeploy는 Jar 파일은 인식하지 못하므로 Jar+기타 설정 파일들을 모아 압축(zip)합니다.
  - __zip -r freelec-springboot-webservice__
    - 현재 위치의 모든 파일을 freelec-springboot2-webservice 이름으로 압축(zip)합니다.
    - 명령어의 마지막 위치는 본인의 프로젝트 이름이어야 합니다.
  - __mkdir -p deploy__
    - deploy라는 디렉토리를 Travis CI가 실행 중인 위치에서 생성합니다.
  - __mv freelec-springboot2-webservice.zip deploy/freelec-springboot2-webservice.zip__
    - freelec-springboot2-webservice.zip 파일을 deploy/freelec-springboot2-webservice.zip으로 이동시킵니다.
  - __deploy__
    - S3로 파일 업로드 혹은 CodeDeploy로 배포 등 외부 서비스와 연동될 행위들을 선언합니다.
  - __local_dir:deploy__
    - 앞에서 생성한 deploy 디렉토리를 지정합니다.
    - 해당 위치의 파일들만 S3로 전송합니다.
 
  - IAM에서 역활과 사용자
    - 역할
      - AWS 서비스에만 할당할 수 있는 권한
      - EC2, CodeDeploy, SQS 등
    - 사용자
      - AWS 서비스 외에 사용할 수 있는 권한
      - 로컬 PC,IDC 서버 등

