# mac-utm-docker

mac 위의 utm을 설치하여 docker를 실행할 목적으로 생성하였습니다.
utm을 사용하는 이유는 docker는 linux와 함께 개발되어 linux기반에서 docker가 더 좋은 호환성을 보이기때문에 사용하였습니다.
이미지는 chatgpt를 활용하여 aws에서 가장 많이 사용되고 있는 image인 Ubuntu 22.04.5 LTS (Jammy Jellyfish)버전을 사용하였습니다.

## utm download & create iso

utm download link : https://mac.getutm.app/
iso download link : https://releases.ubuntu.com/jammy/



![image](https://github.com/user-attachments/assets/ade15ce0-5cf9-448c-af4d-6c4a10b3202b)

Virtualize : 동일한 CPU만을 사용하여 더 빠른 속도로 사용이 가능하나 HOST SYSTEM과 다른 CPU는 사용이 불가능하다.

Emulate : 다양한 CPU 아키텍처를 실행할 수 있지만 성능이 느릴 수 있다.

#### memory
![image](https://github.com/user-attachments/assets/a867aa93-33cc-4adf-af68-1533543318d6)

#### 디스크
![image](https://github.com/user-attachments/assets/c51944fc-d638-41d9-884b-929afe906651)

메모리의 경우 추후 간단한 ELK와 jenkins를 사용할 것을 고려해 메모리는 8GiB 디스크는 64GiB로 설정하였습니다.

#### 공유폴더
![image](https://github.com/user-attachments/assets/83e34ef9-937f-468c-a445-dfdc33699658)

이미지 하위에 생성되는 디렉토리를 관리하기 위한 설정으로 docker의 volume mount나 bind mount와 비슷한 목적으로 사용되는 것으로 보입니다.

#### iso 잘못된 이미지 
![image](https://github.com/user-attachments/assets/525eada8-d1b9-47e9-bd90-ee37bbb79ab6)
iso의 이미지를 amd 로 선택하여 다음과 같이 실행 중 오류가 발생하였습니다. mac과 호환되는 arm image로 바꿔주면 아래와 같이 정상 실행됩니다.

![image](https://github.com/user-attachments/assets/6fe9a15b-8943-4ff1-abc0-8368ff6e71e5)


## docker 

```bash
sudo apt-get install docker.io
```

version 확인
```bash
usernamegservername:"$ docker --version
Docker version 24.0.7, build
```
권한 부여
```bash
sudo usermod -aG docker $USER
newgrp docker
groups에 docker가 올라가있다면 잘 적용된 것이다.
```

docker pull mysql
![image](https://github.com/user-attachments/assets/c05de8cb-8b13-4d58-a9de-1c9cf31f31a8)

docker run --name mysqldb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql:latest
![image](https://github.com/user-attachments/assets/f4b29fda-713b-46c1-9457-fb16cb50e809)

docker mysql에 진입 성공
![image](https://github.com/user-attachments/assets/873c523d-6fba-4982-b76b-7fdfcef8e398)

