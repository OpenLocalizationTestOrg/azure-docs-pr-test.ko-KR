---
title: "aaaHigh 가용성의 SAP HANA Azure 가상 컴퓨터 (Vm)에서 | Microsoft Docs"
description: "Azure VM(Virtual Machines)에서 SAP HANA 고가용성을 설정합니다."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Azure VM(Virtual Machines)의 SAP HANA 고가용성

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

온-프레미스에 두 HANA 시스템 복제를 사용 하거나 SAP HANA에 대 한 공유 저장소 tooestablish 고가용성을 사용할 수 있습니다.
현재로서는 Azure에서 HANA 시스템 복제 설정만 지원합니다. SAP HANA 복제는 하나의 마스터 노드와 하나 이상의 슬레이브 노드로 구성됩니다. 변경 내용을 toohello hello 마스터 노드는 데이터는 동기적 또는 비동기적으로 toohello 슬레이브 노드를 복제 합니다.

이 문서에서는 어떻게 toodeploy hello 가상 컴퓨터 hello 가상 컴퓨터 구성, hello 클러스터 프레임 워크를 설치, 설치 및 구성 SAP HANA 시스템 복제 설명 합니다.
Hello 예제 구성에서는 설치 등 인스턴스 번호 03 명령과 HANA 시스템 ID HDB 사용 됩니다.

SAP Note와 문서를 먼저 다음 읽기 hello

* SAP Note [1928533], 다음 항목을 포함합니다.
  * Hello SAP 소프트웨어 배포에 지원 되는 Azure VM 크기의 목록
  * Azure VM 크기에 대한 중요한 용량 정보
  * 지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합
  * Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전
* SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.
* SAP Note [2205917]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 권장되는 OS 설정이 나와 있습니다.
* SAP Note [1944799]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 대한 SAP HANA 지침이 나와 있습니다.
* SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.
* SAP Note [2191498] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Linux에 대 한 합니다.
* SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.
* SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.
* SAP Note [1999351] Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 추가 문제 해결 정보입니다.
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.
* [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]
* [Linux에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]
* [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]
* [SAP HANA SR 성능에 최적화 된 시나리오] [ suse-hana-ha-guide] 온-프레미스 SAP HANA 시스템 복제를 모든 필요한 정보 tooset hello 가이드에 포함 되어 있습니다. 이 가이드를 기준으로 사용합니다.

## <a name="deploying-linux"></a>Linux 배포

SAP HANA에 대 한 hello 리소스 에이전트는 SAP 응용 프로그램에 대 한 SUSE Linux Enterprise Server에 포함 됩니다.
Azure 마켓플레이스 hello BYOS (Bring Your 자신의 구독의) toodeploy 새 가상 컴퓨터를 사용할 수 있는 경우 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다.

### <a name="manual-deployment"></a>수동 배포

1. 리소스 그룹 만들기
1. Virtual Network 만들기
1. 두 개의 저장소 계정 만들기
1. 가용성 집합 만들기  
   최대 업데이트 도메인 설정
1. 부하 분산 장치(내부) 만들기  
   위의 VNET 단계 선택
1. 가상 컴퓨터 1 만들기  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SAP 응용 프로그램 12 SP1용 SLES(BYOS)  
   저장소 계정 1 선택  
   가용성 집합 선택  
1. 가상 컴퓨터 2 만들기  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SAP 응용 프로그램 12 SP1용 SLES(BYOS)  
   저장소 계정 2 선택   
   가용성 집합 선택  
1. 데이터 디스크 추가
1. Hello 부하 분산 장치 구성
    1. 프런트 엔드 IP 풀 만들기
        1. 열기 hello 부하 분산 장치 프런트 엔드 IP 풀을 선택 하 고 추가 클릭
        1. Hello 새 프런트 엔드 IP 풀 (예를 들어 hana-프런트 엔드) hello 이름 입력
       1. 확인 클릭
        1. Hello 새 프런트 엔드 IP 풀을 만든 후 해당 IP 주소를 적어 둡니다
    1. 백 엔드 풀 만들기
        1. 열기 hello 부하 분산 장치 백 엔드 풀을 선택 하 고 추가 클릭
        1. Hello 새 백 엔드 풀 (예를 들어 hana-백 엔드) hello 이름 입력
        1. 가상 컴퓨터 추가 클릭
        1. Hello 앞에서 만든 가용성 집합 선택
        1. Hello SAP HANA 클러스터의 hello 가상 컴퓨터를 선택 합니다.
        1. 확인 클릭
    1. 상태 프로브 만들기
       1. 열기 hello 부하 분산 장치 상태 프로브를 선택 하 고 추가 클릭
        1. Hello 새 상태 프로브 (예: hana-hp) hello 이름 입력
        1. 프로토콜로 TCP를 선택하고 포트 625**03**을 선택한 다음 간격은 5, 비정상 임계값은 2로 유지
        1. 확인 클릭
    1. 부하 분산 규칙 만들기
        1. Hello 부하 분산 장치 부하 분산 규칙 찾아서 추가 클릭
        1. Hello hello 새 부하 분산 장치 규칙 이름 입력 (예: hana-lb-3**03**15)
        1. 선택 hello 프런트 엔드 IP 주소, 백 엔드 풀 및 상태 프로브 하면 이전에 만든 (예를 들어 hana-프런트 엔드)
        1. 프로토콜 TCP를 유지하고 포트 3**03**15 입력
        1. Too30 분 유휴 시간 제한 증가
       1. **Tooenable 있는지를 확인 합니다. 부동 IP**
        1. 확인 클릭
        1. 포트 3에 대 한 위의 hello 단계를 반복**03**17

### <a name="deploy-with-template"></a>템플릿을 사용하여 배포
사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스. hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.

1. 열기 hello [데이터베이스 템플릿을] [ template-multisid-db] 또는 hello [템플릿 수렴] [ template-converged] hello Azure 포털에 hello 데이터베이스 템플릿은 만듭니다 hello 데이터베이스에 대 한 부하 분산 규칙 hello 수렴 형된 템플릿도 만듭니다. 반면 hello 부하 분산 규칙 ASCS/SCS 및 호출자 (Linux에만 해당) 인스턴스에 대 한 합니다. Tooinstall SAP NetWeaver 기반 시스템을 계획 하 고 싶다면 tooinstall hello ASCS/SCS 인스턴스에 경우 hello에 동일한 컴퓨터를 사용 하 여 hello [템플릿 수렴 형][template-converged]합니다.
1. Hello 매개 변수 뒤에 입력
    1. SAP 시스템 ID -  
       Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 Id를 입력 합니다. hello Id는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
    1. 스택 형식 (hello 수렴 형된 서식 파일을 사용 하는 경우에 해당)  
       Hello SAP NetWeaver 스택 유형 선택
    1. OS 종류 -  
       Hello Linux 배포 사항 중 하나를 선택 합니다. 이 예에서는 SLES 12 BYOS 선택
    1. Db 형식  
       HANA 선택
    1. SAP 시스템 크기 -  
       hello 양을 SAPS hello 새 시스템을 제공 합니다. SAP 기술 파트너 나 시스템 통합 업체에 문의 개수 SAPS hello 시스템 내용의 확실 하지 않은 경우
    1. 시스템 가용성 -  
       HA를 선택합니다.
    1. 관리자 사용자 이름 및 관리자 암호 -  
       새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.
    1. 기존 또는 새 서브넷 -  
       새 가상 네트워크와 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다. 가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 기존 선택 합니다.
    1. 서브넷 ID -  
    hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다. VPN 또는 Express 경로 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다. hello ID는 일반적으로 /subscriptions/ 처럼 보이는`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Linux HA 설정

다음 항목 hello에 대 한 접두사로 사용 하거나 [A]-[1]-1 또는 [2]에 적용할 수 toonode-에 적용할 수 toonode 2, 해당 tooall 노드 됩니다.

1. [A] SLES SAP BYOS 전용-등록 SLES toobe 수 toouse hello 저장소에 대 한
1. [A] SLES for SAP BYOS 전용 - 공개 클라우드 모듈 추가
1. [A] SLES 업데이트
    ```bash
    sudo zypper update

    ```

1. [1] ssh 액세스 사용
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] ssh 액세스 사용
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] ssh 액세스 사용
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] HA 확장 설치
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] 설치 디스크 레이아웃
    1. LVM  
    일반적으로 로그 파일 및 데이터를 저장 하는 볼륨에 대 한 LVM toouse를 좋습니다. 아래 예제에서는 hello 하려면 네 개의 연결 된 데이터 디스크 두 개의 볼륨을 사용 하는 toocreate 되어야 하는 hello 가상 컴퓨터에 있어야 합니다.
        * Toouse 되도록 하는 모든 디스크에 대 한 실제 볼륨을 만듭니다.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Hello 데이터 파일에 대 한 볼륨 그룹, hello 로그 파일에 대 한 하나의 볼륨 그룹 및 SAP HANA의 hello 공유 디렉터리에 대 한 만들기
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Hello 논리 볼륨을 만듭니다.
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Hello 탑재 디렉터리를 만들고 hello 모든 논리 볼륨의 UUID를 복사 합니다.
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * 논리 볼륨이 3 개씩 hello에 대 한 fstab 항목 만들기
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    이 줄 너무/등/fstab 삽입
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Hello 새 볼륨을 탑재
    <pre><code>
    sudo mount -a
    </code></pre>
    1. 일반 디스크  
       소규모 또는 데모 시스템용으로 한 디스크에 HANA 데이터와 로그 파일을 둘 수 있습니다. hello 다음 /dev/sdc에 파티션을 만들고 명령과 xfs로 포맷 합니다.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>/dev/sdc1의 hello id 기록
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] 모든 호스트의 호스트 이름 확인 설정  
    DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다. 이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.
   Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기
    ```bash
    sudo vi /etc/hosts
    ```
    다음 줄 너무/등/호스트 hello를 삽입 합니다. IP 주소 및 호스트 이름 toomatch hello 환경 변경    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] 클러스터 설치
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] toocluster 노드를 추가 합니다.
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] 변경 hacluster 암호 toohello 동일한 암호
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] corosync toouse 다른 전송을 구성 하 고 nodelist를 추가 합니다. 그렇지 않으면 클러스터가 작동하지 않습니다.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    Hello 다음 콘텐츠 toohello 굵게 표시 된 파일을 추가 합니다.
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    다음 hello corosync 서비스 다시 시작

    ```bash
    sudo service corosync restart
    
    ```

1. [A] HANA HA 패키지 설치  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>SAP HANA 설치

장을 참조 4의 hello [SAP HANA SR 성능에 최적화 된 시나리오 가이드] [ suse-hana-ha-guide] tooinstall SAP HANA 시스템 복제 합니다.

1. [A] hello HANA DVD에서에서 hdblcm을 실행 합니다.
    * 설치 선택 -> 1
    * 설치할 추가 구성 요소 선택 -> 1
    * 설치 경로 [/hana/shared] 입력: -> ENTER
    * 로컬 호스트 이름 입력 [..]: -> ENTER
    * Tooadd 추가 호스트 toohello 시스템 하 시겠습니까? (y/n) [n]: -> ENTER
    * SAP HANA 시스템 ID 입력: <SID of HANA e.g. HDB>
    * 인스턴스 번호 [00] 입력:   
  HANA 인스턴스 번호입니다. 위의 hello 예제 뒤 또는 hello Azure 템플릿을 사용한 경우 03를 사용 하 여
    * 데이터베이스 모드 선택 / 인덱스 [1] 입력: -> ENTER
    * 시스템 사용량 선택 / 인덱스 [4] 입력:  
  Hello 시스템 사용을 선택 합니다.
    * 데이터 볼륨의 위치 [/hana/data/HDB] 입력: -> ENTER
    * 로그 볼륨의 위치 [/hana/log/HDB] 입력: -> ENTER
    * 최대 메모리 할당 제한? [n]: -> ENTER
    * '...' 호스트에 대 한 인증서 호스트 이름 입력 [...]: ENTER->
    * SAP 호스트 에이전트 사용자(sapadm) 암호 입력:
    * SAP 호스트 에이전트 사용자(sapadm) 암호 확인:
    * 시스템 관리자(hdbadm) 암호 입력:
    * 시스템 관리자(hdbadm) 암호 확인:
    * 시스템 관리자 홈 디렉터리 [/usr/sap/HDB/home] 입력: -> ENTER
    * 시스템 관리자 로그인 셸 [/bin/sh] 입력: -> ENTER
    * 시스템 관리자 사용자 ID [1001] 입력: -> ENTER
    * 사용자 그룹 ID(sapsys) [79] 입력: -> ENTER
    * 데이터베이스 사용자(SYSTEM) 암호 입력:
    * 데이터베이스 사용자(SYSTEM) 암호 확인:
    * 컴퓨터를 다시 부팅한 다음 시스템 다시 시작? [n]: -> ENTER
    * Toocontinue 하 시겠습니까? (y/n):  
  Hello 요약의 유효성을 검사 하 고 y toocontinue 입력
1. [A] SAP 호스트 에이전트 업그레이드  
  Hello에서 hello 최신 SAP 호스트 에이전트 아카이브 다운로드 [SAP Softwarecenter] [ sap-swcenter] 하 고 실행할 hello 명령 tooupgrade hello 에이전트 다음 합니다. Hello 경로 toohello 보관 toopoint toohello 다운로드 한 파일을 대체 합니다.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] 루트로 HANA 복제 만들기  
    Hello 다음 명령을 실행 합니다. SAP HANA 설치의 hello 값을 사용 하 여 있는지 tooreplace 굵게 표시 된 문자열 (HANA 시스템 ID HDB 및 인스턴스 번호 03)를 확인 합니다.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] 루트로 키 저장소 항목 만들기
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] 루트로 데이터베이스 백업
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] toohello sapsid 사용자 (예: hdbadm) 전환 하 고 hello 기본 사이트를 만듭니다.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] toohello sapsid 사용자 (예: hdbadm) 전환한 hello 보조 사이트를 만듭니다.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>클러스터 프레임워크 구성

Hello 기본 설정 변경

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>이제 hello 파일 toohello 클러스터 로드
sudo crm configure load update crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>STONITH 장치 만들기

hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다. 이러한 단계 toocreate 서비스 사용자를 수행 하십시오.

1. 너무 이동<https://portal.azure.com>
1. Azure Active Directory 블레이드 열기 hello  
   TooProperties 이동한 적어 둡니다 hello 디렉터리 id입니다. 이 hello **테 넌 트 id**합니다.
1. 앱 등록 클릭
1. 추가를 클릭합니다.
1. 이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭
1. hello 로그온 URL은 사용 되지 않으며 유효한 URL이 될 수 있습니다.
1. 선택 hello 새 앱 hello 설정 탭의 키 클릭
1. 새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭
1. Hello 값 적어 둡니다. Hello로 사용 **암호** hello 서비스 사용자에 대 한
1. 적어 둡니다 hello 응용 프로그램 id입니다. Hello 사용자 이름으로 사용 됩니다 (**로그인 id** hello 단계 아래에) hello 서비스 사용자의

hello 서비스 사용자에 없는 사용 권한을 tooaccess Azure 리소스 기본적으로 합니다. Toogive hello 서비스 보안 주체 사용 권한 toostart 필요 하 고 중지 (할당 취소) hello 클러스터의 모든 가상 컴퓨터.

1. Toohttps://portal.azure.com 이동
1. 모든 리소스 블레이드를 hello 열기
1. Hello 가상 컴퓨터를 선택 합니다.
1. 액세스 제어(IAM) 클릭
1. 추가를 클릭합니다.
1. Hello 역할 소유자를 선택 합니다.
1. 위에서 만든 hello 응용 프로그램의 hello 이름 입력
1. 확인 클릭

Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>이제 hello 파일 toohello 클러스터 로드
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>SAP HANA 리소스 만들기

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>이제 hello 파일 toohello 클러스터 로드
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>이제 hello 파일 toohello 클러스터 로드
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>클러스터 설정 테스트
hello 장 다음 설치 프로그램을 테스트 하는 방법을 설명 합니다. 모든 테스트 루트는 hello SAP HANA 마스터 hello 가상 컴퓨터 saphanavm1에서 실행 되 고 가정 합니다.

#### <a name="fencing-test"></a>펜싱 테스트

네트워크 인터페이스 노드 saphanavm1에 hello를 사용 하지 않도록 설정 하 여 hello 펜스 에이전트의 hello 설치 프로그램을 테스트할 수 있습니다.

<pre><code>
sudo ifdown eth0
</code></pre>

hello 가상 컴퓨터 가져오기 지금 다시 시작 하거나 클러스터 구성에 따라 중지 해야 합니다.
Hello stonith 작업 toooff로 설정 하면 hello 가상 컴퓨터가 중지 되 고 hello 리소스는 가상 컴퓨터를 실행 하는 마이그레이션된 toohello 합니다.

Hello 가상 컴퓨터를 다시 시작 되 면 hello SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다. 이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>수동 장애 조치 테스트

수동 장애 조치 노드 saphanavm1에 hello pacemaker 서비스를 중지 하 여 테스트할 수 있습니다.
<pre><code>
service pacemaker stop
</code></pre>

Hello 장애 조치 후 hello 서비스를 다시 시작할 수 있습니다. hello saphanavm1에 SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다. 이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>마이그레이션 테스트

Hello 다음 명령을 실행 하 여 hello SAP HANA 마스터 노드를 마이그레이션할 수 있습니다.
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Hello SAP HANA 마스터 노드 및 가상 IP 주소 toosaphanavm2 hello를 포함 하는 hello 그룹 마이그레이션해야 합니다.
hello saphanavm1에 SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다. 이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

hello 마이그레이션은 toobe 다시 삭제 해야 하는 위치 제약 조건을 만듭니다.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

또한 hello 보조 노드에 리소스의 toocleanup hello 상태 해야

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>다음 단계
* [SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]
* [SAP용 Azure Virtual Machines 배포][deployment-guide]
* [SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]
* tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다. 
