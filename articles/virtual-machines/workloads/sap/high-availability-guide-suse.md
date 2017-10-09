---
title: "가상 컴퓨터에 대 한 고가용성 SUSE Linux Enterprise Server에서의 SAP NetWeaver SAP 응용 프로그램에 대 한 aaaAzure | Microsoft Docs"
description: "SAP 응용 프로그램용 SUSE Linux Enterprise Server의 SAP NetWeaver에 대한 고가용성 가이드"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>SAP 응용 프로그램용 SUSE Linux Enterprise Server의 Azure VM에 있는 SAP NetWeaver에 대한 고가용성

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

이 문서 toodeploy hello 가상 컴퓨터를 hello 가상 컴퓨터 구성, hello 클러스터 프레임 워크를 설치 및 항상 사용 가능한 SAP NetWeaver 7.50 시스템 설치 방법을 설명 합니다.
Hello 예제 구성에서는 설치 명령이 등입니다. 여기서는 ASCS 인스턴스 번호 00, ERS 인스턴스 번호 02 및 SAP 시스템 ID NWS를 사용합니다. hello hello 예제에서 hello 리소스 (예: 가상 컴퓨터, 가상 네트워크) 이름을 가정 hello를 사용한 [템플릿 수렴] [ template-converged] SAP 시스템 ID NWS toocreate hello 리소스와 합니다.

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
* [SAP HANA SR 성능 최적화된 시나리오][suse-hana-ha-guide]  
  hello 가이드에서는 온-프레미스 SAP HANA 시스템 복제를 모든 필요한 정보 tooset 합니다. 이 가이드를 기준으로 사용합니다.
* [DRBD Pacemaker와 항상 사용 가능한 NFS 저장소] [ suse-drbd-guide] hello 가이드 모든 필요한 정보 tooset 항상 사용 가능한 NFS 서버를 포함 합니다. 이 가이드를 기준으로 사용합니다.


## <a name="overview"></a>개요

tooachieve 높은 가용성, SAP NetWeaver NFS 서버가 필요합니다. NFS 서버 hello 별도 클러스터에 구성 되 고 여러 SAP 시스템에서 사용할 수 있습니다.

![SAP NetWeaver 고가용성 개요](./media/high-availability-guide-suse/img_001.png)

SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver 호출자 및 SAP HANA 데이터베이스 hello NFS 서버 hello 가상 호스트 이름 및 가상 IP 주소를 사용 합니다. Azure 부하 분산 장치는 필요한 toouse 가상 IP 주소입니다. hello 다음 목록은 hello hello 부하 분산 장치 구성입니다.

### <a name="nfs-server"></a>NFS 서버
* 프런트 엔드 구성
  * IP 주소 10.0.0.4
* 백 엔드 구성
  * Hello NFS 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 네트워크 인터페이스 tooprimary 연결
* 프로브 포트
  * 포트 61000
* 부하 분산 규칙
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A)SCS
* 프런트 엔드 구성
  * IP 주소 10.0.0.10
* 백 엔드 구성
  * Hello (A) SCS/호출자 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 연결 된 tooprimary 네트워크 인터페이스
* 프로브 포트
  * 포트 620**&lt;nr&gt;**
* 부하 분산 규칙
  * 32**&lt;nr&gt;** TCP
  * 36**&lt;nr&gt;** TCP
  * 39**&lt;nr&gt;** TCP
  * 81**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="ers"></a>ERS
* 프런트 엔드 구성
  * IP 주소 10.0.0.11
* 백 엔드 구성
  * Hello (A) SCS/호출자 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 연결 된 tooprimary 네트워크 인터페이스
* 프로브 포트
  * 포트 621**&lt;nr&gt;**
* 부하 분산 규칙
  * 33**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* 프런트 엔드 구성
  * IP 주소 10.0.0.12
* 백 엔드 구성
  * Hello HANA 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 네트워크 인터페이스 tooprimary 연결
* 프로브 포트
  * 포트 625**&lt;nr&gt;**
* 부하 분산 규칙
  * 3**&lt;nr&gt;**15 TCP
  * 3**&lt;nr&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>고가용성 NFS 서버 설정

### <a name="deploying-linux"></a>Linux 배포

Azure 마켓플레이스 hello toodeploy 새 가상 컴퓨터를 사용할 수 있는 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다.
사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스. hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.

1. 열기 hello [SAP 파일 서버 템플릿] [ template-file-server] hello Azure 포털에서   
1. Hello 매개 변수 뒤에 입력
   1. 리소스 접두사 -  
      원하는 toouse hello 접두사를 입력 합니다. hello 값은 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
   2. OS 종류 -  
      Hello Linux 배포 사항 중 하나를 선택 합니다. 이 예제에서는 SLES 12를 선택합니다.
   3. 관리자 사용자 이름 및 관리자 암호 -  
      새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.
   4. 서브넷 ID -  
      hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다. 원하는 toocreate 새 가상 네트워크 또는 VPN 또는 Express 경로 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 hello 서브넷을 선택 하는 경우 비워 둡니다. hello ID는 일반적으로 /subscriptions/ 처럼 보이는**&lt;구독 id&gt;**/resourceGroups/**&lt;리소스 그룹 이름은&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름입니다.&gt;**

### <a name="installation"></a>설치

hello 다음 항목은 접두사가 사용 하 여 **[A]** -해당 tooall 노드 **[1]** -해당 toonode 1 또는 **[2]** -해당 toonode 2입니다.

1. **[A]** SLES 업데이트

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** ssh 액세스 사용

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** ssh 액세스 사용

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** ssh 액세스 사용

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** HA 확장 설치
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** 호스트 이름 확인 설정   

   DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다. 이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.
   Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   다음 줄 너무/등/호스트 hello를 삽입 합니다. IP 주소 및 호스트 이름 toomatch hello 환경 변경   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** 클러스터 설치
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Toocluster 노드 추가
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  변경 hacluster 암호 toohello 동일한 암호

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  다른 전송을 corosync toouse를 구성 하 고 nodelist를 추가 합니다. 그렇지 않으면 클러스터가 작동하지 않습니다.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   다음 hello corosync 서비스 다시 시작

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** drbd 구성 요소 설치

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Hello drbd 장치에 대 한 파티션을 만들려면

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** LVM 구성 만들기

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Hello NFS drbd 장치 만들기

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hello drbd 장치 만들기 및 시작

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** 초기 동기화 건너뛰기

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  집합 hello 주 노드

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Hello 새 drbd 장치가 동기화 될 때까지 대기

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Drbd 장치 hello에 파일 시스템을 만들

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>클러스터 프레임워크 구성

1. **[1]**  Hello 기본 설정 변경

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  추가 hello NFS drbd 장치 toohello 클러스터 구성

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  만들기 hello NFS 서버

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS 파일 시스템 리소스 만들기

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS 내보내기 만들기

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a>STONITH 장치 만들기

hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다. 이러한 단계 toocreate 서비스 사용자를 따릅니다.

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH 장치 만들기

Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  STONITH 장치 hello 사용 하도록 설정

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>(A)SCS 설정

### <a name="deploying-linux"></a>Linux 배포

Azure 마켓플레이스 hello toodeploy 새 가상 컴퓨터를 사용할 수 있는 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다. hello 마켓플레이스 이미지는 SAP NetWeaver 용 hello 리소스 에이전트를 포함합니다.

사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스. hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.

1. 열기 hello [ASCS/SCS 다중 SID 템플릿] [ template-multisid-xscs] 또는 hello [템플릿 수렴] [ template-converged] hello Azure 포털 hello ASCS/SCS 서식 파일에만 만듭니다 (예: Microsoft SQL Server 또는 SAP HANA) 데이터베이스에 대 한 부하 분산 규칙 hello hello 수렴 형된 템플릿 반면 SAP NetWeaver ASCS/SCS hello 및 호출자 (Linux에만 해당) 인스턴스에 대 한 hello 부하 분산 규칙을 만듭니다. Tooinstall SAP NetWeaver 기반 시스템을 계획 하 고 싶다면 tooinstall hello 데이터베이스 경우 같은 컴퓨터 hello, hello를 사용 하 여 [템플릿 수렴][template-converged]합니다.
1. Hello 매개 변수 뒤에 입력
   1. 리소스 접두사(ASCS/SCS 다중 SID 템플릿에만 해당)  
      원하는 toouse hello 접두사를 입력 합니다. hello 값은 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
   3. SAP 시스템 ID(수렴형 템플릿에만 해당)  
      Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 Id를 입력 합니다. hello Id는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.
   4. 스택 유형 -  
      Hello SAP NetWeaver 스택 유형 선택
   5. OS 종류 -  
      Hello Linux 배포 사항 중 하나를 선택 합니다. 이 예에서는 SLES 12 BYOS 선택
   6. Db 형식  
      HANA 선택
   7. SAP 시스템 크기 -  
      hello 양을 SAPS hello 새 시스템을 제공합니다. SAP 기술 파트너 나 시스템 통합 업체에 문의 개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우
   8. 시스템 가용성 -  
      HA를 선택합니다.
   9. 관리자 사용자 이름 및 관리자 암호 -  
      새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.
   10. 서브넷 ID -  
   hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다.  선택 사용 하거나 hello NFS 서버 배포의 일부로 만든 동일한 서브넷 hello 또는 toocreate 새 가상 네트워크를 예약할 경우 비워 둡니다. hello ID는 일반적으로 /subscriptions/ 처럼 보이는**&lt;구독 id&gt;**/resourceGroups/**&lt;리소스 그룹 이름은&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름입니다.&gt;**

### <a name="installation"></a>설치

hello 다음 항목은 접두사가 사용 하 여 **[A]** -해당 tooall 노드 **[1]** -해당 toonode 1 또는 **[2]** -해당 toonode 2입니다.

1. **[A]** SLES 업데이트

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** ssh 액세스 사용

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** ssh 액세스 사용

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** ssh 액세스 사용

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** HA 확장 설치
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** SAP 리소스 에이전트 업데이트  
   
   Hello 리소스 에이전트 패키지에 대 한 패치는 필요한 toouse hello 새 구성,이 문서에 설명 되어 있는 합니다. 다음 명령을 hello로 hello 패치를 이미 설치한 경우 확인할 수 있습니다.

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   hello 출력와 유사 해야 합니다.

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   에 나열 된 tooinstall hello 패치 hello grep 명령 hello IS_ERS 매개 변수를 찾지 못하면 경우 해야 [hello SUSE 다운로드 페이지](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** 호스트 이름 확인 설정   

   DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다. 이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.
   Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   다음 줄 너무/등/호스트 hello를 삽입 합니다. IP 주소 및 호스트 이름 toomatch hello 환경 변경   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** 클러스터 설치
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Toocluster 노드 추가
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  변경 hacluster 암호 toohello 동일한 암호

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  다른 전송을 corosync toouse를 구성 하 고 nodelist를 추가 합니다. 그렇지 않으면 클러스터가 작동하지 않습니다.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   다음 hello corosync 서비스 다시 시작

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** drbd 구성 요소 설치

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Hello drbd 장치에 대 한 파티션을 만들려면

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** LVM 구성 만들기

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Hello SCS drbd 장치 만들기

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hello drbd 장치 만들기 및 시작

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Hello 호출자 drbd 장치 만들기

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hello drbd 장치 만들기 및 시작

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** 초기 동기화 건너뛰기

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  집합 hello 주 노드

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Hello 새 drbd 장치가 동기화 될 때까지 대기

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Drbd 장치 hello에 파일 시스템을 만들

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>클러스터 프레임워크 구성

**[1]**  Hello 기본 설정 변경

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>SAP NetWeaver 설치 준비

1. **[A]**  만들기 hello 공유 디렉터리

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** autofs 구성
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   아래 코드를 사용하여 파일을 만듭니다.

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Autofs toomount hello 새 공유를 다시 시작

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]** 스왑 파일 구성
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Hello 에이전트 tooactivate hello 변경 다시 시작

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>SAP NetWeaver ASCS/ERS 설치

1. **[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다. 노드 hello 리소스의 실행에 중요 하지 않습니다.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** SAP NetWeaver ASCS 설치  

   예를 들어 hello ASCS hello에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하는 hello 첫 번째 노드에서 루트로 SAP NetWeaver ASCS 설치 <b>nws ascs</b>, <b>10.0.0.10</b>hello 부하 분산 장치 프로브 hello에 대 한 예를 사용 하는 인스턴스 번호를 hello <b>00</b>합니다.

   Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다. 노드 hello 리소스의 실행에 중요 하지 않습니다.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** SAP NetWeaver ERS 설치  

   예를 들어 hello hello 호출자에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하 여 hello 두 번째 노드는 루트로 SAP NetWeaver 호출자 설치 <b>nws 호출자</b>, <b>10.0.0.11</b> 예를 들어 hello 부하 분산 장치 프로브 hello에 대 한 사용 하는 인스턴스 번호를 hello <b>02</b>합니다.

   Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > SWPM SP 20 PL 05 이상을 사용하세요. 더 낮은 버전 hello 사용 권한을 올바르게 설정 하지 않으면 및 hello 설치가 실패 합니다.
   > 

1. **[1]**  Hello ASCS/SCS 및 호출자 인스턴스 프로필 적용
 
   * ASCS/SCS 프로필

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * ERS 프로필

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]** 연결 유지 구성

   hello SAP NetWeaver 응용 프로그램 서버와 hello ASCS/SCS 간의 hello 통신 소프트웨어 부하 분산 장치를 통해 라우팅됩니다. hello 부하 분산 장치 구성 가능한 시간 초과 이후 비활성 연결을 끊습니다. tooprevent이 tooset hello SAP NetWeaver ASCS/SCS 프로필의에서 매개 변수를 필요 하 고 hello Linux 시스템 설정을 변경 합니다. 자세한 내용은 [SAP Note 1410736][1410736]을 참조하세요.
   
   hello ASCS/SCS 프로필 매개 변수 큐에 넣지/encni/set_so_keepalive hello 마지막 단계에서 이미 추가 되었습니다.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Hello SAP 사용자 hello 설치 후 구성
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Hello ASCS 및 호출자 SAP 서비스 toohello sapservice 파일 추가

   Hello ASCS 서비스 항목 toohello 두 번째 노드 및 복사 hello 호출자 서비스 항목 toohello 첫 번째 노드를 추가 합니다.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Hello SAP 클러스터 리소스 만들기

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다. 노드 hello 리소스의 실행에 중요 하지 않습니다.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a>STONITH 장치 만들기

hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다. 이러한 단계 toocreate 서비스 사용자를 따릅니다.

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH 장치 만들기

Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  STONITH 장치 hello 사용 하도록 설정

Hello STONITH 장치를 사용 하도록 설정

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>데이터베이스 설치

이 예제에서 SAP HANA System Replication을 설치 및 구성합니다. SAP HANA hello hello SAP NetWeaver ASCS/SCS와 호출자와 동일한 클러스터에서 실행 됩니다. 전용 클러스터에 SAP HANA를 설치할 수도 있습니다. 자세한 내용은 [Azure VM(Virtual Machines)의 SAP HANA 고가용성][sap-hana-ha]을 참조하세요.

### <a name="prepare-for-sap-hana-installation"></a>SAP HANA 설치 준비

일반적으로는 데이터와 로그 파일을 저장하는 볼륨의 LVM을 사용하는 것이 좋습니다. 테스트를 위해 toostore 일반 디스크에 직접 데이터 및 로그 파일 hello를 선택할 수 있습니다.

1. **[A]** LVM  
   아래 예제에서는 hello 하려면 네 개의 연결 된 데이터 디스크 두 개의 볼륨을 사용 하는 toocreate 되어야 하는 hello 가상 컴퓨터에 있어야 합니다.
   
   Toouse 되도록 하는 모든 디스크에 대 한 실제 볼륨을 만듭니다.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Hello 데이터 파일에 대 한 볼륨 그룹, hello 로그 파일에 대 한 하나의 볼륨 그룹 및 SAP HANA의 hello 공유 디렉터리에 대 한 만들기
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Hello 논리 볼륨을 만듭니다.
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Hello 탑재 디렉터리를 만들고 hello 모든 논리 볼륨의 UUID를 복사 합니다.
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   논리 볼륨이 3 개씩 hello에 대 한 autofs 항목 만들기
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   이 줄 toosudo vi /etc/auto.direct 삽입
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Hello 새 볼륨을 탑재
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** 일반 디스크  

   소규모 또는 데모 시스템용으로 한 디스크에 HANA 데이터와 로그 파일을 둘 수 있습니다. hello 다음 /dev/sdc에 파티션을 만들고 명령과 xfs로 포맷 합니다.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   이 줄 too/etc/auto.direct 삽입
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Hello 대상 디렉터리를 만들고 hello 디스크를 탑재 합니다.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>SAP HANA 설치

hello 다음 단계에 기반 hello의 4 장을 [SAP HANA SR 성능에 최적화 된 시나리오 가이드] [ suse-hana-ha-guide] tooinstall SAP HANA 시스템 복제 합니다. 읽어 보십시오 hello 설치를 계속 하기 전에.

1. **[A]**  Hdblcm hello HANA DVD에서에서 실행
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** SAP 호스트 에이전트 업그레이드

   Hello에서 hello 최신 SAP 호스트 에이전트 아카이브 다운로드 [SAP Softwarecenter] [ sap-swcenter] 하 고 실행할 hello 명령 tooupgrade hello 에이전트 다음 합니다. Hello 경로 toohello 보관 toopoint toohello 다운로드 한 파일을 대체 합니다.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** 루트로 HANA 복제 만들기  

   Hello 다음 명령을 실행 합니다. SAP HANA 설치의 hello 값을 사용 하 여 있는지 tooreplace 굵게 표시 된 문자열 (HANA 시스템 ID HDB 및 인스턴스 번호 03)를 확인 합니다.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** 루트로 키 저장소 항목 만들기

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** 루트로 데이터베이스 백업

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Toohello HANA sapsid 사용자를 전환 하 고 hello 주 사이트를 만듭니다.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Toohello HANA sapsid 사용자를 전환 하 고 hello 보조 사이트를 만듭니다.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** SAP HANA 클러스터 리소스 만들기

   먼저 hello 토폴로지를 만듭니다.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   다음으로 hello을 HANA 리소스 만들기
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다. 노드 hello 리소스의 실행에 중요 하지 않습니다.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  설치 hello SAP NetWeaver 데이터베이스 인스턴스

   예를 들어 hello hello 데이터베이스에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하 여 루트로 설치 hello SAP NetWeaver 데이터베이스 인스턴스 <b>nws db</b> 및 <b>10.0.0.12</b>.

   Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>SAP NetWeaver 응용 프로그램 서버 설치

이러한 단계 tooinstall SAP 응용 프로그램 서버를 따릅니다. hello 단계 아래 hello ASCS/SCS와에서 다른 서버에 응용 프로그램 서버 hello 및 HANA 서버 설치 한다고 가정 합니다. 그렇지 않은 경우 (예: 호스트 이름 확인 구성)는 다음 hello 단계 중 일부는 필요 하지 않습니다.

1. 호스트 이름 확인 설정    
   DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다. 이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.
   Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기
   ```bash
   sudo vi /etc/hosts
   ```
   다음 줄 너무/등/호스트 hello를 삽입 합니다. IP 주소 및 호스트 이름 toomatch hello 환경 변경    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Hello sapmnt 디렉터리 만들기

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. autofs를 구성합니다.
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   다음 코드를 사용하여 새 파일을 만듭니다.

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Autofs toomount hello 새 공유를 다시 시작

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. 스왑 파일을 구성합니다.
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Hello 에이전트 tooactivate hello 변경 다시 시작

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. SAP NetWeaver 응용 프로그램 서버 설치

   기본 또는 추가 SAP NetWeaver 응용 프로그램 서버를 설치합니다.

   Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. SAP HANA 보안 저장소 업데이트

   SAP HANA 보안 업데이트 hello toopoint toohello hello SAP HANA 시스템 복제 설치 프로그램의 가상 이름을 저장 합니다.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>다음 단계
* [SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]
* [SAP용 Azure Virtual Machines 배포][deployment-guide]
* [SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]
* tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.
* tooestablish 고가용성 및 Azure Vm에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA의 높은 가용성 Azure 가상 컴퓨터 (Vm)에서][sap-hana-ha]
