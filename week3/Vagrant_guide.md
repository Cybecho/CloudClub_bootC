# Fedora 40 GUI bootC 이미지 빌드 가이드

이 가이드는 Vagrant를 사용하여 GNOME 데스크탑 환경을 가진 Fedora 40 bootC 이미지를 자동으로 빌드하는 환경을 구성합니다. 완성된 이미지에는 Git, Visual Studio Code, Google Chrome이 미리 설치됩니다.

## 자동화된 구성 요소

제공된 Vagrantfile은 다음 작업을 자동으로 수행합니다:

1. **Ubuntu 22.04 LTS 가상머신 생성** (8GB 메모리, 4 CPU 코어)
2. **필수 도구 설치** (podman, git, curl, qemu-utils)
3. **Fedora 40 bootC 기본 이미지 다운로드**
4. **GUI 환경용 Containerfile 자동 생성**
5. **애플리케이션 설치 스크립트 준비**

## 사용 방법

### 1. 환경 준비

Vagrantfile을 새 디렉토리에 저장하고 가상머신을 시작합니다:

```bash
# 새 디렉토리 생성 및 이동
mkdir fedora-bootc-gui && cd fedora-bootc-gui

# Vagrantfile 저장 후
vagrant up
```

### 2. VM에 접속

```bash
vagrant ssh
```

### 3. bootC 이미지 빌드

```bash
cd ~/fedora-bootc-gui
sudo podman build -t fedora-gui-bootc .
```

**주의:** GUI 환경 빌드는 시간이 오래 걸릴 수 있습니다 (30분~1시간).

### 4. 사용자 설정 파일 생성

bootC 이미지를 디스크 이미지로 변환하기 전에 사용자 계정을 설정합니다:

```bash
cat > config.toml << 'EOL'
[[customizations.user]]
name = "fedora"
password = "fedora123"
groups = ["wheel", "sudo"]
shell = "/bin/bash"

[[customizations.user]]
name = "root"
password = "root123"
EOL
```

### 5. bootC 이미지를 디스크 이미지로 변환

QCOW2 형식으로 변환합니다:

```bash
sudo podman run \
  --rm \
  -it \
  --privileged \
  --pull=newer \
  --security-opt label=type:unconfined_t \
  -v ./config.toml:/config.toml:ro \
  -v ./output:/output \
  -v /var/lib/containers/storage:/var/lib/containers/storage \
  quay.io/centos-bootc/bootc-image-builder:latest \
  --type qcow2 \
  --output /output \
  localhost/fedora-gui-bootc
```

### 6. VirtualBox용 VDI 형식으로 변환

```bash
qemu-img convert -f qcow2 -O vdi output/qcow2/disk.qcow2 output/fedora-gui-bootc.vdi
```

### 7. 디스크 이미지를 호스트로 복사

새 터미널에서 Vagrant 디렉토리로 이동하여:

```bash
# vagrant-scp 플러그인 설치 (처음 한 번만)
vagrant plugin install vagrant-scp

# 파일 복사
vagrant scp default:/home/vagrant/fedora-bootc-gui/output/fedora-gui-bootc.vdi ./
```

## 새 VM에서 Fedora GUI 부팅하기

### VirtualBox에서 새 VM 생성

1. **VirtualBox 관리자**에서 "새로 만들기" 클릭
2. **이름**: Fedora-GUI-bootC
3. **종류**: Linux
4. **버전**: Fedora (64-bit)
5. **메모리**: 최소 4GB (권장 8GB)
6. **하드 디스크**: "기존 가상 하드 디스크 파일 사용" 선택
7. 복사한 `fedora-gui-bootc.vdi` 파일 선택

### VM 설정 조정

생성된 VM을 선택하고 "설정" > "디스플레이"에서:
- **비디오 메모리**: 최소 128MB
- **그래픽 컨트롤러**: VMSVGA
- **3D 가속**: 활성화

### 부팅 및 로그인

1. VM 시작
2. 부팅 완료 후 GNOME 로그인 화면에서 다음 계정으로 로그인:
   - **사용자명**: fedora
   - **비밀번호**: fedora123

## 설치된 애플리케이션

부팅 후 다음 애플리케이션들이 사용 가능합니다:

- **GNOME 데스크탑 환경** (전체 GUI)
- **Git** (터미널에서 `git` 명령어)
- **Visual Studio Code** (응용 프로그램 메뉴에서 실행)
- **Google Chrome** (응용 프로그램 메뉴에서 실행)
- **Firefox** (Fedora 기본 브라우저)
- **기본 개발 도구들**

## VM 관리

### Vagrant VM 종료

```bash
# 일시 중지
vagrant suspend

# 완전 종료
vagrant halt

# VM 삭제
vagrant destroy
```

## 문제 해결

### 빌드 시간이 오래 걸리는 경우
- GUI 환경과 애플리케이션 설치로 인해 정상적으로 30분~1시간 소요됩니다.
- 네트워크 상태에 따라 더 오래 걸릴 수 있습니다.

### 메모리 부족 오류
- Vagrant VM의 메모리를 늘려보세요 (Vagrantfile에서 `vb.memory` 값 증가)
- 호스트 시스템에 충분한 메모리가 있는지 확인하세요.

### 그래픽 문제
- VirtualBox에서 3D 가속을 활성화했는지 확인하세요.
- 비디오 메모리를 128MB 이상으로 설정하세요.

## 추가 정보

- **Fedora bootC**: https://docs.fedoraproject.org/en-US/bootc/
- **bootC GitHub**: https://github.com/containers/bootc
- **Fedora Container Images**: https://quay.io/fedora/fedora-bootc