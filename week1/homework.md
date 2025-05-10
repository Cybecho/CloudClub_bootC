# Link
[퍼플렉시티 리서치](https://www.perplexity.ai/search/prompttemplate-task-bootable-c-hSTv7a0HSOu7YaiN9vUc9Q)

[제미나이 리서치](https://docs.google.com/document/d/1VkxKrGcOpzJ5D83kf8CUFzlOyNrIuXLVJ4GVOsc_2bg/edit?usp=sharing)

# boot C

## A. 도대체 무엇일까?
- 이미지 자체를 
- bootC 이미지는 일반 컨테이너 이미지와 달리, "부팅 가능한 컨테이너(bootable container)"로 설계되어 있습니다.
- 이 이미지를 bootc install 명령어로 시스템에 설치하면, 기존 OS 대신 해당 이미지를 기반으로 시스템이 부팅됩니다.
- 이때 실제로 OS의 루트 파일 시스템(/usr, /etc, /var 등)이 bootC 이미지로 대체되고, 커널 파라미터, 서비스 설정 등도 이미지에 정의된 대로 적용됩니다.
- 설치 후 시스템을 재부팅하면, 내가 만든 bootC 이미지가 OS로 동작하는지 직접 확인할 수 있습니다. 예를 들어, 이미지에 포함한 패키지나 파일, 서비스가 정상적으로 동작하는지 체크할 수 있습니다.

## B. 그래서 왜 쓰는가?
- 이거 이미지 자체를 버전별로 관리하려고 쓰기 좋음.
- 원자성이 보장됨. 이것이 무엇을 의미하냐? 해당 OS는 그 OS자체만으로 역할을 수행할 수 있다는것임.
    - 운영자는 그냥 이미지만 바꿔끼워두면 해당 OS의 동작은 머 그냥 다 알아서 함. 내부 들어가서 만질 필요가 없음.

### B-1. 구체적으로, 어디에 쓰일 수 있을까?

### B-2. 현재 내 환경에서는 어디에 적용될수 있을까?

## C. boot C 대신에 사용할 수 있는 기술들에 대한 레퍼런스

### C-1. 왜 굳이 bootC일까? docker/ansible 기반 자동화로는 안될까?? cloud init쓰면 안돼?

## D. 그래서, boot C는 어떻게 사용하는가?

### D-1. 놀랍게도, bootC의 문법은 Dockerfile과 유사하다.
- bootC 이미지는 놀랍게도 우리가 이미 익숙한 방식으로 만들어진다. 
- 바로 표준 Containerfile (Dockerfile과 거의 같다) 문법과 Podman, Docker, Buildah 같은 도구들을 사용해서 빌드된다.
- 즉, bootC용 베이스 이미지에서 시작해 필요한 요소를 추가하면 나만의 이미지가 된다.
- 패키지 설치, 설정 추가, 애플리케이션 내장 등 다양한 커스터마이징이 가능하며, Docker 이미지 만드는 방식과 유사하다.

### D-2. 예제 코드
아래는 위의 간단한 bootC Containerfile을 빌드하고, 이미지를 확인하며, 실제로 bootc로 실행(테스트)하는 방법을 안내합니다.

#### 1. Containerfile 작성

아래 코드를 `Containerfile`이라는 이름으로 저장하세요.

```Dockerfile
# CentOS Stream bootC 베이스 이미지 사용
FROM quay.io/centos-bootc/centos-bootc:stream9

# vim 패키지 설치 (필요한 패키지만 최소로 설치)
RUN dnf -y install vim

# 간단한 텍스트 파일 추가
RUN echo "안녕하세요, bootC 간단 예제입니다." > /root/hello.txt
```

#### 2. 빌드 및 실행

```Dockerfile
# 1. Containerfile이 있는 디렉터리로 이동
cd /path/to/your/containerfile

# 2. 이미지를 빌드합니다. (my-bootc-test라는 이름으로 태그)
podman build -t my-bootc-test .

# 3. 빌드된 이미지를 확인합니다.
podman images

# 4. (선택) bootc로 이미지를 테스트 설치합니다.
sudo bootc install --image localhost/my-bootc-test

# 또는 podman-bootc로 컨테이너 기반 부팅 테스트를 할 수 있습니다.
# podman-bootc가 설치되어 있어야 합니다.
podman bootc install --image localhost/my-bootc-test

# 5. (테스트 후) /root/hello.txt 파일이 잘 생성되었는지 확인합니다.
cat /root/hello.txt

```