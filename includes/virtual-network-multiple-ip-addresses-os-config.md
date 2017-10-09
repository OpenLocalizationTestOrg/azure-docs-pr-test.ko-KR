## <a name="os-config"></a>IP 주소 tooa VM 운영 체제 추가

연결 하 고 여러 개인 IP 주소를 사용 하 여 만든 로그인 tooa VM입니다. 모든 hello 개인 IP 주소 (주 복제본 hello 포함) 추가한 toohello VM을 수동으로 추가 해야 합니다. Hello VM 운영 체제에 대 한 단계를 완료 합니다.

### <a name="windows"></a>Windows

1. 명령 프롬프트에서 *ipconfig /all*을 입력합니다.  Hello에만 표시 *기본* (DHCP)를 통한 개인 IP 주소입니다.
2. 형식 *ncpa.cpl* hello 명령 프롬프트 tooopen hello에 **네트워크 연결** 창.
3. Hello 적절 한 어댑터에 대 한 hello 속성을 열고: **로컬 영역 연결**합니다.
4. IPv4(인터넷 프로토콜 버전 4)를 두 번 클릭합니다.
5. 선택 **다음 IP 주소 사용 하 여 hello** hello 다음 값을 입력 합니다.

    * **IP 주소**: hello 입력 *기본* 개인 IP 주소
    * **서브넷 마스크**: 서브넷을 기준으로 설정됩니다. 예를 들어 경우 hello 서브넷은 / 24 서브넷 다음 hello 서브넷 마스크는 255.255.255.0입니다.
    * **기본 게이트웨이**: hello hello 서브넷에서 첫 번째 IP 주소입니다. 서브넷 10.0.0.0/24 이면 hello 게이트웨이 IP 주소는 10.0.0.1 합니다.
    * 클릭 **다음 DNS 서버 주소를 사용 하 여 hello** hello 다음 값을 입력 합니다.
        * **기본 설정 DNS 서버**: 자체 DNS 서버를 사용하지 않는 경우 168.63.129.16을 입력합니다.  자체 DNS 서버를 사용 하는 서버에 대 한 hello IP 주소를 입력 합니다.
    * Hello 클릭 **고급** 단추 및 IP 주소를 추가 합니다. 각 hello 보조 개인 IP 주소가 동일한 서브넷 hello 기본 IP 주소에 대해 지정 하는 hello와 8 단계 toohello NIC에에서 나열 된 추가 합니다.
        >[!WARNING] 
        >위의 hello 단계를 올바르게 수행 하지 않는 경우 연결 tooyour VM 손실 될 수 있습니다. 5 단계에 대 한 입력 hello 정보가 진행 하기 전에 정확한 지 확인 합니다.

    * 클릭 **확인** tooclose hello TCP/IP 설정을 차례로 **확인** 다시 tooclose hello 어댑터 설정 합니다. RDP 연결이 다시 설정됩니다.

6. 명령 프롬프트에서 *ipconfig /all*을 입력합니다. 추가한 모든 IP 주소가 표시되고 DHCP는 해제됩니다.


### <a name="validation-windows"></a>유효성 검사(Windows)

tooensure 수 tooconnect toohello 인터넷 hello 올바르게 사용 하 여 추가한 후 공용 IP 연결을 통해 보조 IP 구성에서 위의 프로세스를 hello 다음 명령을 사용 하 여:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>보조 IP 구성에 대 한 hello 구성에 연결 된 공용 IP 주소를 있으면 toohello 인터넷만 ping 할 수 있습니다. 기본 IP 구성에 대 한 공용 IP 주소를 아니며 필요한 tooping toohello 인터넷

### <a name="linux-ubuntu"></a>Linux(Ubuntu)

1. 터미널 창을 엽니다.
2. Hello 루트 사용자 인지 확인 합니다. 가 아닌 경우에 hello 다음 명령을 입력 합니다.

    ```bash
    sudo -i
    ```

3. Hello 네트워크 인터페이스 ('t h 0' 가정)의 hello 구성 파일을 업데이트 합니다.

    * Dhcp에 대 한 hello 기존 행 항목을 유지 합니다. 이전에 hello 기본 IP 주소 구성 된 유지 됩니다.
    * 명령 다음 hello로 추가 정적 IP 주소에 대 한 구성을 추가 합니다.

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    .cfg 파일이 표시됩니다.
4. 열기 hello 파일입니다. 위의 hello hello 파일 끝에 삼각형 hello를 표시 되어야 합니다.

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. 이 파일에 존재 하는 hello 줄 다음에 오는 줄을 다음 hello를 추가 합니다.

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Hello 다음 명령을 사용 하 여 hello 파일을 저장 합니다.

    ```bash
    :wq
    ```

7. 다음 명령을 hello로 hello 네트워크 인터페이스를 다시 설정 하십시오.

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > 원격 연결을 사용 하는 경우 라인 동일 hello에서 ifdown와 ifup 모두를 실행 합니다.
    >

8. Hello IP 주소는 다음 명령을 hello로 toohello 네트워크 인터페이스를 추가 하는 것을 확인 합니다.

    ```bash
    ip addr list eth0
    ```

    Hello IP 주소 hello 목록의 일부로 추가한 표시 되어야 합니다.

### <a name="linux-redhat-centos-and-others"></a>Linux(Redhat, CentOS 및 기타)

1. 터미널 창을 엽니다.
2. Hello 루트 사용자 인지 확인 합니다. 가 아닌 경우에 hello 다음 명령을 입력 합니다.

    ```bash
    sudo -i
    ```

3. 암호를 입력하고 화면 지시를 따릅니다. Hello 루트 사용자 인 경우 되 면 다음 명령을 hello로 toohello 네트워크 스크립트 폴더를 이동 합니다.

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. 목록 hello 관련 hello 다음 명령을 사용 하 여 ifcfg 파일:

    ```bash
    ls ifcfg-*
    ```

    표시 되어야 *ifcfg eth0* hello 파일 중 하 나와 있습니다.

5. 아래와 같이 tooadd IP 주소에 대 한 구성 파일을 만듭니다. 각 IP 구성에 대해 하나의 파일을 만들어야 합니다.

    ```bash
    touch ifcfg-eth0:0
    ```

6. 열기 hello *ifcfg-eth0:0* 다음 명령을 hello로 파일:

    ```bash
    vi ifcfg-eth0:0
    ```

7. 콘텐츠 toohello 파일을 추가 *eth0:0* 이 경우 hello 다음 명령을 사용 합니다. 있는지 tooupdate 정보 IP 주소에 기반 합니다.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. 다음 명령을 hello로 hello 파일을 저장 합니다.

    ```bash
    :wq
    ```

9. Hello 네트워크 서비스를 다시 시작 하 고 hello 다음 명령을 실행 하 여 hello 변경 사항이 정상적으로 수행 되었는지 확인 합니다.

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Hello IP 주소를 추가, 표시 되어야 *eth0:0*, 반환 되는 hello 목록에 있습니다.

### <a name="validation-linux"></a>유효성 검사(Linux)

다음 명령을 hello를 사용 하 여과 것 tooensure 수 tooconnect toohello는 hello 공용 IP 통해 보조 IP 구성에서 인터넷 연결:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>보조 IP 구성에 대 한 hello 구성에 연결 된 공용 IP 주소를 있으면 toohello 인터넷만 ping 할 수 있습니다. 기본 IP 구성에 대 한 공용 IP 주소를 아니며 필요한 tooping toohello 인터넷

Linux vm의 경우 보조 NIC에서 toovalidate 아웃 바운드 연결을 시도할 때, tooadd 적절 한 경로 할 수 있습니다. 가지가 여러 방법으로 toodo이 있습니다. Linux 배포에 대한 적절한 설명서를 참조하세요. hello 다음 하나의 메서드 tooaccomplish 이것은:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- 있는지 tooreplace 수 있습니다:
    - **10.0.0.5** hello 개인 ip 주소는 공용 IP가 있는 주소 관련된 tooit
    - **10.0.0.1** tooyour 기본 게이트웨이
    - **eth2** 보조 NIC의 toohello 이름
