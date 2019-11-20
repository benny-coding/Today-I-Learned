## Docker로 Elastic Stack 설치하기
  * Docker 설치하기  
    * https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html 
      위 링크에 subicura님께서 잘 설명해주시고 계신다 그대로만 따라하면 될 것이다.   
  * `Docker`를 실행한다.
  * `elasticStack`을 `docker`에서 빠르게 세팅하기 위해서는 https://github.com/deviantony/docker-elk
    깃허브에 들어가서 로컬에 git clone을 한다.
  * 로컬에서 `git clone`을 한 폴더 (docker-compose.yml)이 있는 폴더에 터미널로 들어가서 `docker-compose up` 명령어를 실행한다.
  * 처음에 세팅되는데 시간이 꽤 걸릴 것이다. 다 세팅이 되면 `http://localhost:5601/` 여기에 접속해보자
  * 위에 경로는 데이터를 시각화하여 볼 수 있는 Kibana의 로컬 세팅 경로이다.
  * 기본 로그인 정보는 `Username : elastic` , `Password : changeme` 이다.
    