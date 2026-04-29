# 카카오 클라우드 전환 시 확인할 것

1.  **Source/Dest. Check:** NAT 역할을 하는 Bastion 인스턴스의 '소스/대상 확인'을 반드시 **비활성화**
2.  **Security Groups:** Bastion에서는 모든 대역에서의 SSH(22) 허용, Private 노드에서 오는 모든 트래픽 허용, Private VM에서는 Public VM에서 오는 모든 트래픽 허용, Private 노드 간 모든 트래픽 허용 
3.  **SSH Key:** SSH 키를 맞게 GitHub Actions Secrets의 SSH_PRIVATE_KEY 값 변경
4.  **BASTION_HOST:** Bastion VM의 퍼블릭 IP에 맞게 BASTION_HOST 값 변경
5.  **BASTION_USER:** Bastion VM에 접속했을 때 뜨는 user명에 맞게 BASTION_USER 값 변경
6.  **네트워크 인터페이스 명칭 확인** : Bastion VM 터미널에 접속해서 "ip addr" 명령어를 입력해서 뜨는 네트워크 인터페이스 이름 (ens5, eth0 등)에 맞게 setup_nat.yml 변경
7.  **inventory.ini:** : 변경된 IP에 맞게 인벤토리 IP 대역 변경
8.  **라우팅 테이블** : 프라이빗 서브넷 라우팅 테이블 수정 (Bastion 추가)

### 테스트 환경
-   AWS
-   Ubuntu 22.04
-   Kubespray 2.31 (master 브랜치)
-   쿠버네티스 버전 1.35.4
-   파이썬 버전 3.11
-   앤서블 버전 11.x
-   앤서블 엔진 버전 2.18.x

### 마지막 설정
컨트롤 플레인에 접속해서 아래 명령어 입력

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
