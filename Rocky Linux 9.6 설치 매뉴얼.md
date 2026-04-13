# 1. RAID 구성 확인
Dell PowerEdge 시리즈의 경우 보통 PERC가 설치되어 있어 실행 화면에서 Ctrl + R을 계속 연타하고 있으면, PERC BIOS Utility로 넘어가 RAID 상태를 확인할 수 있습니다.

![](./Attached%20files/KakaoTalk_20260409_161451506.jpg)

Dell PowerEdge 시리즈의 경우 보통 PERC가 설치되어 있어 실행 화면에서 Ctrl + R을 계속 연타하고 있으면, PERC BIOS Utility로 넘어가 RAID 상태를 확인할 수 있습니다.

![](./Attached%20files/KakaoTalk_20260409_161447229.jpg)

견적서에 따로 RAID 구성을 언급하지 않은 경우 F2(Operations) -> Delete VD를 통해 Virtual Disk를 모두 지워주고 새로 Disk Group 하나를 만들어 모든 하드 디스크를 포함시키면 됩니다.

![](./Attached%20files/KakaoTalk_20260409_161452875.jpg)

기본은 RAID-0입니다. 데이터 백업을 위한 어떤 기능도 쓰지 않습니다. 일반 PC와 같은 설정입니다. 왼쪽 하단에서 선택할 수 있는 모든 하드 디스크를 선택하고 Advanced Settings에서 Initialize를 선택합니다. 하드 디스크에 있는 정보를 초기화시키는 기능입니다. RAID-0로 설치할 때는 넘겨도 상관없으나, RAID-1으로 설치할 때는 하드 디스크에 남아있는 데이터가 OS 설치를 방해하는 경우가 종종 있습니다.

## 견적서에 디스크 그룹을 유지해달라는 경우
이 경우 첫 화면에서 디스크 그룹을 선택하신 후 F2(Operations)에서 Fast Init을 찾아 디스크 내 데이터 초기화만 진행하시면 됩니다.

# 2. 설치 시작
## 2-1. USB 부팅
Ctrl + Alt + Delete로 재시작을 하신 후 F11을 눌러 Boot Manager 화면으로 진입합니다. 그곳에서 Hard Disk -> USB(또는 Front USB)를 선택하시면 OS 설치가 시작됩니다. 설치 화면에서 Install Rocky Linux를 선택하시면 됩니다.

## 2-2. 언어 선택
![](./Attached%20files/KakaoTalk_20260409_161453972.jpg)

견적서에 있는 언어를 선택하시면 됩니다. 보통 위와 같이 영어를 선택합니다.

# 3. 설치 설정
![](./Attached%20files/KakaoTalk_20260409_161455323.jpg)

설치 메인 화면입니다. 여기서 필요한 곳으로 들어가 설정을 진행합니다.

## 3-1. 시간 설정
![](./Attached%20files/KakaoTalk_20260409_161456436.jpg)

Time & Date 메뉴로 들어가 시간을 설정합니다. 지도에서 클릭하면 가까운 기준 시로 값이 변경됩니다. 시간대는 견적서에 맞게 하시면 됩니다. 견적서에 빠져 있다면 Rigion: Asia, City: Seoul로 설정하시면 됩니다.

## 3-2. 네트워크 설정
![](./Attached%20files/KakaoTalk_20260409_161457535.jpg)

Network & Host Name 메뉴로 들어갑니다. 여러 NIC(Network Interface Card)가 보이는데, 가장 작은 숫자를 가진 포트를 선택합니다. 위 사진에선 eno1입니다.

![](./Attached%20files/KakaoTalk_20260409_161458669.jpg)

NIC 내부 값을 변경합니다. 값은 보통 견적서에 나와있으며, 밑은 예시입니다.
IPADDR = 14.0.87.74 -> Address에 입력
NETMASK = 255.255.255.192 -> Netmask에 입력
GATEWAY = 14.0.87.65 -> Gateway에 입력
DNS1 = 210.220.163.82 -> DNS servers에 입력
DNS2 = 164.124.101.2 -> Search domains에 입력

## 3-3. 디스크 선택 및 파티션 구성
![](./Attached%20files/KakaoTalk_20260409_161459838.jpg)

Installation Destination 메뉴로 들어갑니다. 설치 대상 디스크를 선택해야 합니다. USB에 해당하는 Flash Disk를 제외하고 모두 선택합니다. Storage Configuration은 Custom으로 선택합니다.

![](./Attached%20files/KakaoTalk_20260409_161501998.jpg)

Standard Partition을 선택하고 Click here to create them automatically를 눌러 다음으로 넘어갑니다. 예시의 OS 버전은 minimal 구성이 강제된 버전이라 따로 더 선택할 수 있는 구성이 없습니다. 견적서에 minimal install로 해달라 할 경우 여기서 minimal을 고르면 됩니다.

![](./Attached%20files/KakaoTalk_20260409_161504109.jpg)

견적서 대로 만들면 됩니다. 기본 세팅으로 최소로 만들어 달라하면 위 화면에서 값만 적절히 조정합니다.

/boot : 최소는 1024 MB이고 회사에서 받은 설치 가이드에선 2048 MB가 권장 값입니다.

swap : 메모리에 따라 달라집니다. 서버 메모리가 8 ~ 64G일 경우 권장 값이 8GB입니다. 회사에서 받은 설치 가이드에선 4GB로 되어있는데, 공간이 적어 문제가 될 수 있어서 개인적으로 8GB로 설정합니다. swap은 OS가 메모리 공간이 부족할 때 잠깐 보관하는 창고로 생각하시면 됩니다. 평소엔 문제가 없으나 메모리 피크 시에는 OS가 메모리 확보를 위해 메모리 회수를 강하게 하면서 문제가 발생할 수 있습니다.

나머지는 보통 기본값으로 진행합니다.

### RAID 0 + RAID 5 구성
이 경우 RAID 0 디스크 그룹에는 OS 정보를 저장하고, RAID 5에는 중요한 데이터를 저장하려는 의도입니다. OS는 언제든 교체될 수 있고, 복구도 쉽기 때문에 중요도가 떨어집니다. 그래서 따로 데이터를 분산 저장할 필요 없어 RAID 0 디스크 그룹에 설치합니다.

/data는 RAID 5(보통 용량이 큰 디스크 그룹) 전체를 쓰도록 하고, 나머지는 모두 RAID 0에 해당하는 디스크 그룹에 설치되도록 설정합니다. Modify...를 통해 변경할 수 있습니다.

## 3-4 계정 설정
![](./Attached%20files/KakaoTalk_20260409_161506142.jpg)

Root Password 메뉴에서 root 비밀번호를 설정합니다. 견적서에 나와있는 비밀번호로 설정하시면 됩니다. 그리고 보통 고객사에서 root 로그인을 이용하므로 Allow root SSH login with password를 체크합니다.

![](./Attached%20files/KakaoTalk_20260409_161507376.jpg)

User Creation 메뉴에서 운영용 계정을 만듭니다. 견적서에 나와있는 아이디와 비밀번호로 설정합니다.

# 4. 설치 후 설정(선택)
## 4-1 방화벽 비활성화
![](./Attached%20files/KakaoTalk_20260409_161508221.jpg)

systemctl stop firewalld : 방화벽 끄는 명령어
systemctl disable firewalld : 재부팅해도 방화벽 비활성화되도록 하는 명령어
systemctl status firewalld : 방화벽 현재 상태 확인

firewalld.service : disabled가 보이면 비활성화 된 것입니다.

## 4-2 crypto policy 변경
구형 클라이언트 호환성 때문에 LEGACY 정책이 필요한 경우가 있습니다. 구형 클라이언트는 최신 버전보다 낮은 수준의 암호화 알고리즘을 사용하기 때문에 정책을 바꾸지 않으면 접근이 차단될 수 있습니다.

![](./Attached%20files/KakaoTalk_20260409_161509135.jpg)

update-crypto-policies --set LEGACY : crypto policy를 LEGACY로 바꾸는 명령어
update-crypto-policies --show : 현재 crypto policy 정책을 보여주는 명령어. LEGACY가 나오면 올바르게 변경된 것입니다.

## 4-3 SELinux 비활성화
![](./Attached%20files/KakaoTalk_20260409_161510798.jpg)

grubby --update-kernel ALL --args selinux=0 : selinux 값을 disabled로 바꾸는 명령어. 다른 방법으로 /etc/selinux/config에서 SELINUX=disabled로 바꿔서 처리할 수도 있습니다. 두 가지 방법 모두 리부팅을 해야 적용됩니다.

setenforce 0: selinux 값을 임시로 비활성화 합니다. getenforce로 값을 보면 disabled가 아니라 다른 값이 들어가 있는 것을 볼 수 있습니다. 완전히 비활성화할 경우엔 필요없는 명령어 입니다.

getenforce : selinux 값을 확인하는 명령어입니다. 리부팅 후 Disabled가 출력되면 완전히 비활성화 된 것입니다.

## 4-4 SSH 포트 변경
방화벽, SElinux가 켜져있다면 두 곳에서도 포트를 열어야 정상 작동합니다. 꺼져 있다면 상관없습니다.

![](./Attached%20files/KakaoTalk_20260409_161509942.jpg)

vi /etc/ssh/sshd_config로 들어가면 위와 같은 화면이 나옵니다. 보통 설정값 앞에 샾이 붙어있는데, 그 설정값을 주석 처리해서 비활성화하는 목적으로 사용됩니다. 실제로 값을 적용하려면 앞의 샾을 지워줘야 합니다.

Port 값을 요구하는 값으로 변경 후 저장한 후 다음 명령을 순서대로 실행합니다.

sshd -t : 설정한 sshd 문서의 문법이 맞는지 확인하는 명령어
systemctl restart sshd : 설정 반영해서 재시작하는 명령어

systemctl status sshd : 서비스가 정상적으로 살아났는지 확인
ss -tulpn | grep <포트번호> : 원하는 포트에서 실제로 리스닝 중인지 확인

## 4-5 디스크 정보 확인
df -h
cat /etc/fstab