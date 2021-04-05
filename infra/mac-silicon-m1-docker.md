# MAC Silicon\(M1\)에 Docker 설치하기

### Docker 란?

> 컨테이너 기반의 가상화 플랫폼 오픈소스

### 설치 방법

~~사전 환경 : Homebrew 먼저 설치~~

```bash
# brew로 docker search
brew search docker

# brew로 docker insatll
brew install docker

# docker 구동 확인
docker -v
```

## \[2021-04-01\] Docker Desktop RC 3

{% embed url="https://docs.docker.com/docker-for-mac/apple-m1/" %}

```bash
# Darwin / AMD64 아키텍처 기반의 구동이 여전히 필요하기 때문에, 로제타2가 반드시 설치되어 있어야 한다.
# 터미널에서 아래 명령줄을 실행한다.
softwareupdate --install-rosetta
```



