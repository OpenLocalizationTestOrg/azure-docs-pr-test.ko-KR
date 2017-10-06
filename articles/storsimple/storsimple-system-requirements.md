---
title: "aaaStorSimple 시스템 요구 사항 | Microsoft Docs"
description: "Microsoft Azure StorSimple 솔루션에 대한 모범 사례와 소프트웨어, 네트워킹, 고가용성 요구 사항을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>StorSimple 소프트웨어, 높은 가용성 및 네트워킹 요구 사항
## <a name="overview"></a>개요
Azure StorSimple tooMicrosoft를 시작 합니다. 이 문서에서는 중요 한 시스템 요구 사항 및 StorSimple 장치에 대 한 및 hello 장치에 액세스 하는 hello 저장소 클라이언트에 대 한 모범 사례를 설명 합니다. 정보를 검토 하 hello 신중 하 게 배포 및 후속 작동 하는 동안 필요에 따라 tooit 다시 참조할 및 StorSimple 시스템을 배포 하기 전에 것이 좋습니다.

hello 시스템 요구 사항:

* **저장소 클라이언트에 대 한 소프트웨어 요구 사항** -hello 지원 운영 체제 및 해당 운영 체제에 대 한 추가 요구 사항을 설명 합니다.
* **Hello StorSimple 장치의 네트워킹 요구 사항** -iSCSI, 클라우드 또는 관리 트래픽을 방화벽 tooallow에 열려 해당 필요 toobe hello 포트에 대 한 정보를 제공 합니다.
* **StorSimple에 대한 고가용성 요구 사항** - StorSimple 장치 및 호스트 컴퓨터에 대한 고가용성 요구 사항 및 모범 사례를 설명합니다. 

## <a name="software-requirements-for-storage-clients"></a>저장소 클라이언트에 대한 소프트웨어 요구 사항
StorSimple 장치에 액세스 하는 hello 저장소 클라이언트에 대 한 소프트웨어 요구 사항을 준수 하는 hello가 됩니다.

| 지원되는 운영 체제 | 필요한 버전 | 추가 요구 사항/메모 |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2, 2016 |StorSimple iSCSI 볼륨에서 Windows 디스크 유형에 따라 hello만 사용 하기 위해 지원 됩니다.<ul><li>기본 디스크의 단순 볼륨</li><li>동적 디스크의 단순 및 미러 볼륨</li></ul>Hello 소프트웨어 iSCSI 초기자만 hello 운영 체제에 기본적으로 사용할 수 있습니다. 하드웨어 iSCSI 초기자는 지원되지 않습니다.<br></br>Windows Server 2012 및 2016 씬 프로비전 및 ODX 기능은 StorSimple iSCSI 볼륨을 사용하는 경우에 지원됩니다.<br><br>StorSimple은 씬 프로비전된 볼륨과 완전히 프로비전된 볼륨을 만들 수 있습니다. 부분적으로 프로비전된 볼륨은 만들 수 없습니다.<br><br>씬 프로비전된 볼륨을 다시 포맷하는 데에는 시간이 오래 걸릴 수 있습니다. Hello 볼륨을 삭제 한 다음 다시 포맷 하는 대신 한 새를 만드는 것이 좋습니다. 그러나 여전히 선호 tooreformat 볼륨:<ul><li>Hello 다음 hello 다시 포맷 tooavoid 공간 재사용에 따른 지연 하기 전에 명령을 실행 합니다. <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>완료 되 면 hello 서식을 사용 하 여 hello 다음 명령 toore 사용 공간 확보 수 있습니다.<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>에 설명 된 대로 hello Windows Server 2012 핫픽스를 적용 [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour Windows Server 컴퓨터.</li></ul></li></ul></ul> SharePoint 용 StorSimple 스냅숏 관리자 또는 StorSimple 어댑터 구성 됩니다, 경우 너무 이동[선택적 구성 요소에 대 한 소프트웨어 요구 사항](#software-requirements-for-optional-components)합니다. |
| VMWare ESX |5.5 및 6.0 |iSCSI 클라이언트로 VMWare vSphere와 함께 지원됩니다. VAAI 블록 기능은 StorSimple 장치에서 VMware vSphere와 함께 지원됩니다. |
| Linux RHEL/CentOS |5, 6 및 7 |Open iSCSI 초기자 버전 5, 6 및 7과 함께 Linux iSCSI 클라이언트를 지원합니다. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX는 현재 StorSimple에 지원되지 않습니다.
> 
> 

## <a name="software-requirements-for-optional-components"></a>선택적 구성 요소에 대한 소프트웨어 요구 사항
소프트웨어 요구 사항을 준수 하는 hello hello 선택적 StorSimple 구성 요소 (StorSimple 스냅숏 관리자 및 SharePoint 용 StorSimple 어댑터) 됩니다.

| 구성 요소 | 호스트 플랫폼 | 추가 요구 사항/메모 |
| --- | --- | --- |
| StorSimple 스냅숏 관리자 |Windows Server 2008R2 SP1, 2012, 2012R2 |Windows Server에서 StorSimple 스냅숏 관리자 사용은 미러링한 동적 디스크의 백업/복원에 필요하며 응용 프로그램에 일관된 백업에 필요합니다.<br> StorSimple Snapshot Manager는 Windows Server 2008 R2 SP1(64비트), Windows 2012 R2 및 Windows Server 2012에서만 지원됩니다.<ul><li>Window Server 2012를 사용하는 경우 StorSimple Snapshot Manager를 설치하기 전에 .NET 3.5–4.5를 설치해야 합니다.</li><li>Windows Server 2008 R2 SP1을 사용하는 경우 StorSimple Snapshot Manager를 설치하기 전에 Windows Management Framework 3.0을 설치해야 합니다.</li></ul> |
| SharePoint용 StorSimple 어댑터 |Windows Server 2008R2 SP1, 2012, 2012R2 |<ul><li>SharePoint용 StorSimple 어댑터는 SharePoint 2010 및 SharePoint 2013에서만 지원됩니다.</li><li>RBS는 SQL Server Enterprise Edition 2008 R2 또는 2012 버전이 필요합니다.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>StorSimple 장치에 대한 네트워킹 요구 사항
StorSimple 장치는 잠긴 장치입니다. 그러나 포트 필요 toobe iSCSI, 클라우드 및 관리 트래픽에 대 한 방화벽 tooallow 프로그램에서 열립니다. hello 다음 표 toobe 방화벽에서 열 필요로 하는 hello 포트입니다. 이 표에 *에* 또는 *인바운드* toohello 방향에서 들어오는 클라이언트 요청 액세스할 수 있는 장치를 참조 합니다. *Out* 또는 *아웃 바운드* 는 StorSimple 장치 hello 배포를 벗어나 외부로 데이터를 전송 toohello 방향 참조: 인터넷 아웃 바운드 toohello 예를 들어 있습니다.

| 포트 번호 <sup>1, 2</sup> | 인 또는 아웃 | 포트 범위 | 필수 | 참고 사항 |
| --- | --- | --- | --- | --- |
| TCP 80(HTTP)<sup>3</sup> |아웃 |WAN |아니요 |<ul><li>아웃 바운드 포트는 인터넷 액세스 tooretrieve 업데이트에 사용 됩니다.</li><li>hello 아웃 바운드 웹 프록시는 사용자가 구성할 수 있습니다.</li><li>tooallow 시스템 업데이트를이 포트도 열려 있어야 hello 컨트롤러 고정 Ip에 대 한 합니다.</li></ul> |
| TCP 443(HTTPS)<sup>3</sup> |아웃 |WAN |예 |<ul><li>아웃 바운드 포트는 hello 클라우드에서 데이터에 액세스 하기 위해 사용 됩니다.</li><li>hello 아웃 바운드 웹 프록시는 사용자가 구성할 수 있습니다.</li><li>tooallow 시스템 업데이트를이 포트도 열려 있어야 hello 컨트롤러 고정 Ip에 대 한 합니다.</li><li>이 포트도 가비지 수집에 대 한 hello 컨트롤러 모두에서 사용 됩니다.</li></ul> |
| UDP 53(DNS) |아웃 |WAN |일부 경우에는 메모를 참조하십시오. |이 포트는 인터넷 기반 DNS 서버로 사용하는 경우에만 필요합니다. |
| UDP 123(NTP) |아웃 |WAN |일부 경우에는 메모를 참조하십시오. |이 포트는 인터넷 기반 NTP 서버로 사용하는 경우에만 필요합니다. |
| TCP 9354 |아웃 |WAN |예 |StorSimple Manager 서비스 hello로 StorSimple 장치 toocommunicate hello에서 hello 아웃 바운드 포트를 사용 합니다. |
| 3260(iSCSI) |내용 |LAN |아니요 |이 포트는 iSCSI를 통해 사용 되는 tooaccess 데이터는입니다. |
| 5985 |내용 |LAN |아니요 |인바운드 포트는 hello StorSimple 장치와 StorSimple 스냅숏 관리자 toocommunicate에서 사용 됩니다.<br>이 포트는 원격으로 연결할 때 tooWindows PowerShell StorSimple에 대 한 HTTP를 통한에 사용 됩니다. |
| 5986 |내용 |LAN |아니요 |이 포트는 원격으로 연결할 때 tooWindows PowerShell StorSimple에 대 한 HTTPS를 통해 사용 됩니다. |

<sup>1</sup> 인바운드 포트가 없습니다 필요 toobe에서 연 공용 인터넷 hello 합니다.

<sup>2</sup> 여러 포트에서 게이트웨이 구성을 제공, hello 아웃 바운드 라우팅된 트래픽 순서 결정 됩니다에 설명 된 hello 포트 라우팅 순서에 따라 [포트 라우팅은](#routing-metric)아래, 합니다.

<sup>3</sup> 수 tooconnect toohello 인터넷 직접 또는 hello를 통해 구성 된 웹 프록시 및 hello 컨트롤러 StorSimple 장치에서 고정 Ip가 라우팅 가능 해야 합니다. hello 고정 IP 주소는 hello 업데이트 toohello 장치를 서비스에 사용 됩니다. Hello 장치 컨트롤러 toohello hello 통해 인터넷 고정 Ip를 연결할 수 없는 경우 됩니다 수 tooupdate StorSimple 장치입니다.

> [!IMPORTANT]
> Hello 방화벽을 수정 하거나 hello StorSimple 장치와 Azure 간의 SSL 트래픽을 암호를 해독 하지 않습니다 확인 합니다.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>방화벽 규칙에 대한 URL 패턴
네트워크 관리자는 hello URL 패턴 toofilter hello에 따라 규칙 인바운드 및 아웃 바운드 트래픽을 hello 고급 방화벽을 구성할 종종 있습니다. StorSimple 장치 및 hello StorSimple Manager 서비스는 Azure 서비스 버스, Azure Active Directory 액세스 제어, 저장소 계정 및 Microsoft 업데이트 서버와 같은 다른 Microsoft 응용 프로그램에 따라 달라 집니다. 이러한 응용 프로그램과 관련 된 hello URL 패턴에 사용 되는 tooconfigure 방화벽 규칙 될 수 있습니다. 이러한 응용 프로그램과 관련 된 hello URL 패턴을 변경할 수 있는 중요 한 toounderstand 것 합니다. 이 차례로 및 필요 합니다. 네트워크 관리자 toomonitor hello로 StorSimple에 대 한 고 필요한 경우 방화벽 규칙을 업데이트 합니다.

StorSimple 고정 IP 주소에 따라 대부분의 경우에서 자유롭게 아웃바운드 트래픽에 대한 방화벽 규칙을 설정하는 것이 좋습니다. 그러나 고급 방화벽 규칙을 필요한 toocreate 보안 환경 tooset 아래 hello 정보를 사용할 수 있습니다.

> [!NOTE]
> 항상 hello 장치 (원본) Ip tooall hello 사용 네트워크 인터페이스 설정 되어야 합니다. hello 대상 Ip 너무 설정할지[Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653)합니다.
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Azure 포털의 URL 패턴
| URL 패턴 | 구성 요소/기능 | 장치 IP |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple 관리자 서비스<br>액세스 제어 서비스<br>Azure 서비스 버스 |클라우드 사용 네트워크 인터페이스 |
| `https://*.backup.windowsazure.com` |장치 등록 |데이터 0만 해당 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |인증서 해지 |클라우드 사용 네트워크 인터페이스 |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 저장소 계정 및 모니터링 |클라우드 사용 네트워크 인터페이스 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft 업데이트 서버<br> |컨트롤러 고정 IP만 |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |컨트롤러 고정 IP만 |
| `https://*.partners.extranet.microsoft.com/*` |지원 패키지 |클라우드 사용 네트워크 인터페이스 |

#### <a name="url-patterns-for-azure-government-portal"></a>Azure Government 포털의 URL 패턴
| URL 패턴 | 구성 요소/기능 | 장치 IP |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |StorSimple 관리자 서비스<br>액세스 제어 서비스<br>Azure 서비스 버스 |클라우드 사용 네트워크 인터페이스 |
| `https://*.backup.windowsazure.us` |장치 등록 |데이터 0만 해당 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |인증서 해지 |클라우드 사용 네트워크 인터페이스 |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 저장소 계정 및 모니터링 |클라우드 사용 네트워크 인터페이스 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft 업데이트 서버<br> |컨트롤러 고정 IP만 |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |컨트롤러 고정 IP만 |
| `https://*.partners.extranet.microsoft.com/*` |지원 패키지 |클라우드 사용 네트워크 인터페이스 |

### <a name="routing-metric"></a>라우팅 메트릭
라우팅 메트릭이 hello 데이터 toohello 지정한 라우팅합니다 hello 게이트웨이 및 hello 인터페이스와 연결 된 네트워크입니다. 경로가 여러 개일 toohello 파악 하는 경우 라우팅 메트릭이 hello 라우팅 프로토콜 toocalculate hello 최상의 경로 tooa 대상으로 지정 된 사용한 동일한 대상이 있습니다. hello 낮은 hello 라우팅 메트릭, hello hello 우선 순위가 높은 합니다.

Hello StorSimple, 여러 네트워크 인터페이스와 게이트웨이의 컨텍스트 구성 toochannel 트래픽, hello 라우팅 메트릭 재생 toodetermine hello 상대 순서는 hello 인터페이스 사용 가져오기에 옵니다. hello 라우팅 메트릭 hello 사용자가 변경할 수 없습니다. 그러나 hello를 사용할 수 있습니다 `Get-HcsRoutingTable` cmdlet tooprint StorSimple 장치에 hello 라우팅 테이블 (및 메트릭). Get-HcsRoutingTable cmdlet에 대한 자세한 내용은 [StorSimple 배포 문제 해결](storsimple-troubleshoot-deployment.md)을 참조하세요.

메트릭 알고리즘 라우팅 hello StorSimple 장치에서 실행 되는 hello 소프트웨어 버전에 따라 달라 집니다.

**이전 tooUpdate 1를 해제합니다.**

여기에 소프트웨어 버전 이전 tooUpdate 1 같은 hello GA, 0.1, 0.2, 또는 0.3 릴리스를 포함 됩니다. 라우팅 메트릭을 기반으로 하는 hello 순서는 다음과 같습니다.

   *마지막으로 구성된 10GbE 네트워크 인터페이스 > 기타 10GbE 네트워크 인터페이스 > 마지막으로 구성된 1GbE 네트워크 인터페이스 > 기타 1GbE 네트워크 인터페이스*

**릴리스 업데이트 1과 이전 tooUpdate 2에서 시작**

여기에는 1, 1.1, 또는 1.2 같은 소프트웨어 버전이 포함됩니다. 라우팅 메트릭을 기반으로 하는 hello 순서는 다음과 같이 결정 됩니다.

   *데이터 0 > 마지막으로 구성된 10GbE 네트워크 인터페이스 > 기타 10GbE 네트워크 인터페이스 > 마지막으로 구성된 1GbE 네트워크 인터페이스 > 기타 1GbE 네트워크 인터페이스*

   업데이트 1의 DATA 0의 라우팅 메트릭이 hello 이루어집니다 hello 가장 낮은; 따라서 모든 hello 클라우드 트래픽은 DATA 0 통해 라우팅됩니다. StorSimple 장치에 둘 이상의 클라우드 지원 네트워크 인터페이스가 있는 경우 이를 기록해 둡니다.

**업데이트 2 이후 릴리스**

업데이트 2의 몇 가지 향상 된 네트워킹 관련 기능 및 hello 라우팅 메트릭을 변경 되었습니다. hello 동작을 다음과 같이 설명 될 수 있습니다.

* 미리 결정 된 값 집합이 toonetwork 인터페이스 할당 되었습니다.     
* 아래 표시 된 값이 지정 되어 toohello와 다양 한 네트워크 인터페이스 클라우드 사용 하거나 때 클라우드-사용 안 함 하지만 구성 된 게이트웨이 사용 하는 예제 테이블을 고려 합니다. 여기에 할당 된 참고 hello 값은 예제 값만입니다.

    | 네트워크 인터페이스 | 클라우드 사용 | 클라우드 미사용(게이트웨이 구성됨) |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Data 1  | 2            | 20                       |
    | Data 2  | 3            | 30                       |
    | Data 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Data 5  | 6            | 60                       |


* hello 네트워크 인터페이스를 통해 hello 클라우드 트래픽을 라우팅할 수 hello 순서는.
  
    *Data 0 > Data 1 > Date 2 > Data 3 > Data 4 > Data 5*
  
    이 다음 예제는 hello로 설명 될 수 있습니다.
  
    클라우드 사용 네트워크 인터페이스가 두 개(Data 0과 Data 5)인 StorSimple 장치가 있다고 가정합니다. Data 1에서 Data 4까지는 클라우드를 사용하지 않지만 구성된 게이트웨이가 있습니다. 이 장치에 대 한 트래픽을 라우팅할 수 hello 순서가 됩니다.
  
    *Data 0(1) > Data 5(6) > Data 1(20) > Data 2(30) > Data 3(40) > Data 4(50)*
  
    *여기서 괄호로 hello 숫자 hello 개별 라우팅 메트릭에 나타냅니다.*
  
    Data 0에 실패 하면 hello 클라우드 트래픽은 Data 5를 통해 라우팅됩니다. 데이터 0 및 Data 5 toofail 경우 다른 모든 네트워크에는 게이트웨이가 구성 되어 있다고 가정 hello 클라우드 트래픽은 Data 1 진행 합니다.
* 클라우드 지원 네트워크 인터페이스에 실패 하면 30 두 번째 지연 tooconnect toohello 인터페이스와 함께 3 회는 합니다. 모든 hello 다시 시도가 실패 하는 경우 hello 트래픽은 라우트된 toohello 다음 사용 가능한 클라우드 지원 인터페이스 hello 라우팅 테이블을 기준으로입니다. 클라우드 사용 hello 모든 네트워크 인터페이스가 실패 경우 hello 장치는 toohello 장애 조치할 다른 컨트롤러 (이 경우 다시 부팅 없음).
* iSCSI 사용 네트워크 인터페이스에 VIP 오류가 있으면, 2초 지연 후에 재시도가 3회 실행됩니다. 이 동작은 높게 유지 되었음을 hello 이전 릴리스에서 hello 동일 합니다. 모든 hello iSCSI 네트워크 인터페이스는 실패 하는 경우 컨트롤러 장애 조치 (다시 부팅 하면 동봉) 발생 합니다.
* VIP 오류가 있으면 StorSimple 장치에 경고가 생성됩니다. 자세한 내용은 이동 너무[경고 빠른 참조](storsimple-manage-alerts.md)합니다.
* 재시도에 있어서 iSCSI는 클라우드에 우선합니다.
  
    다음 예제는 hello 고려: A StorSimple 장치에 사용 하도록 설정 하는 두 개의 네트워크 인터페이스, Data 0 및 Data 1입니다. Data 0은 클라우드를 사용하지만 Data 1은 클라우드와 iSCSI 모두를 사용합니다. 이 장치에서 클라우드 또는 iSCSI에 사용하도록 설정된 다른 네트워크 인터페이스는 없습니다.
  
    지정한 데이터 1 실패 hello 마지막 iSCSI 네트워크 인터페이스 이면 이렇게 하면 컨트롤러 장애 조치 tooData 1 on hello 다른 컨트롤러입니다.

### <a name="networking-best-practices"></a>네트워킹 모범 사례
또한 위의 네트워킹 요구 사항이 hello StorSimple 솔루션의 최적의 성능 위해서는 toohello toohello 최선의 구현 방법을 준수 하세요.

* StorSimple 장치에서 항상 전용 40Mbps 대역폭(이상)을 사용할 수 있어야 합니다. 이 대역폭을 공유 되지 않아야 합니다 (또는 hello QoS 정책 사용 하 여 할당을 보장 해야) 다른 응용 프로그램과 합니다.
* 네트워크 연결 toohello 인터넷은 항상 사용할 수 있는지 확인 합니다. 불안정 하거나 자주 끊기면 인터넷 연결 toohello 등의 장치 없이 인터넷 연결 되지 않은 구성이 지원된 됩니다.
* 전용 iSCSI 및 클라우드 액세스에 대 한 장치에서 네트워크 인터페이스를 포함 하 여 hello iSCSI 및 클라우드 트래픽을 격리 합니다. 어떻게 너무 자세한 내용은 참조[네트워크 인터페이스 수정](storsimple-modify-device-config.md#modify-network-interfaces) StorSimple 장치에 있습니다.
* 네트워크 인터페이스에 대한 링크 집합 제어 프로토콜(LACP) 구성을 사용하지 마십시오. 지원되지 않는 구성입니다.

## <a name="high-availability-requirements-for-storsimple"></a>StorSimple에 대한 고가용성 요구 사항
hello 하드웨어 플랫폼 hello StorSimple 솔루션에 포함 되어 있는 데이터 센터에서 내결함성 / 고가용성 저장소 인프라에 대 한 기초를 제공 하는 가용성 및 안정성 기능을 갖추고 있습니다. 그러나 요구 사항은 없으며 toohelp 준수 해야 하는 모범 사례는 StorSimple 솔루션의 hello 가용성을 보장 합니다. StorSimple을 배포 하기 전에 신중 하 게 hello 요구 사항 및 hello StorSimple 장치에 대 한 모범 사례를 따르고 연결 된 호스트 컴퓨터를 검토 합니다.

모니터링 및 StorSimple 장치의 hello 하드웨어 구성 요소를 유지 관리 하는 방법에 대 한 자세한 내용은 이동 너무[hello StorSimple 관리자 서비스 toomonitor 하드웨어 구성 요소 및 상태를 사용 하 여](storsimple-monitor-hardware-status.md) 및 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>StorSimple 장치에 대한 고가용성 요구 사항 및 절차
다음 정보를 주의 깊게 검토 hello tooensure hello 고가용성 StorSimple 장치의 합니다.

#### <a name="pcms"></a>PCM
StorSimple 장치에는 운영 중 스왑 가능한 중복 전원 및 냉각 모듈(PCM)이 포함됩니다. 각 PCM에 충분 한 용량 tooprovide hello 전체 섀시에 서비스를 있습니다. tooensure 고가용성을 두 Pcm에 모두 설치 되어야 합니다.

* 전원이 공급 되지 않는 경우에 Pcm toodifferent 전원 소스 tooprovide 가용성을 연결 합니다.
* PCM에 문제가 있으면 즉시 교체를 요청합니다.
* Hello 교체품을 받아 tooinstall 준비 되 면 오류가 발생 한 PCM 제거 것입니다.
* 두 PCM을 동시에 제거하지 마십시오. hello PCM 모듈 hello 백업 배터리 모듈을 포함 합니다. 모두 제거 hello의 Pcm를 배터리 보호 없이 종료 되 고 hello 장치 상태 저장 되지 않습니다. 너무 hello 배터리에 대 한 자세한 내용을 보려면 이동[유지 hello 백업 배터리 모듈](storsimple-battery-replacement.md#maintain-the-backup-battery-module)합니다.

#### <a name="controller-modules"></a>컨트롤러 모듈
StorSimple 장치에는 운영 중 스왑 가능한 중복 컨트롤러 모듈이 포함됩니다. hello 두 컨트롤러 모듈이 활성/수동 방식으로 작동합니다. 지정된 된 시간에 컨트롤러 모듈 하나가 활성 상태 이며 서비스를 제공 하는, hello 하는 동안 다른 컨트롤러 모듈은 수동입니다. hello 수동 컨트롤러 모듈이 켜지 고 작동 hello 활성 컨트롤러 모듈에 오류가 발생 하거나 제거 합니다. 각 컨트롤러 모듈에 충분 한 용량 tooprovide hello 전체 섀시에 서비스를 합니다. 두 컨트롤러 모듈에는 설치 된 tooensure 고가용성 이어야 합니다.

* 항상 두 컨트롤러 모듈이 모두 설치되었는지 확인합니다.
* 컨트롤러 모듈에 문제가 있으면 즉시 교체를 요청합니다.
* Hello 교체품을 받아 준비 tooinstall 되는 경우에 오류가 발생 한 컨트롤러 모듈을 제거 하기. 오랫동안 모듈을 제거 hello 공기 흐름이 영향 되 고 따라서 hello 시스템의 냉각이 hello 됩니다.
* Hello 네트워크 연결 tooboth 컨트롤러 모듈은 동일 하며 hello 연결 된 네트워크 인터페이스 지 네트워크 구성이 동일한 있는지 확인 합니다.
* 컨트롤러 모듈에 장애가 발생 하거나 교체 하십시오 해야 해당 hello hello 오류가 발생 한 컨트롤러 모듈을 교체 하기 전에 다른 컨트롤러 모듈이 활성 상태입니다. 컨트롤러가 활성 상태임 tooverify 너무 이동[식별 hello 장치에서 활성 컨트롤러](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)합니다.
* Hello에서 두 컨트롤러 모듈을 제거 하지 마십시오 동시 합니다. 컨트롤러 장애 조치가 진행 중이면 hello 대기 컨트롤러 모듈을 종료 하지 않거나 hello 섀시에서 제거 합니다.
* 컨트롤러 장애 조치 후 컨트롤러 모듈을 제거하기 전에 5분 이상 기다립니다.

#### <a name="network-interfaces"></a>네트워크 인터페이스
StorSimple 장치 컨트롤러 모듈마다 1기가비트 4개 및 10기가비트 2개의 이더넷 네트워크 인터페이스가 있습니다.

* Hello 네트워크 연결 tooboth 컨트롤러 모듈은 동일 하며 hello 네트워크 인터페이스 hello 컨트롤러 모듈 인터페이스가 연결 된 toohave 네트워크 구성이 동일한 지 확인 합니다.
* 가능 하면 네트워크 장치 오류의 hello 이벤트에서 서로 다른 스위치 tooensure 서비스 가용성에서 네트워크 연결을 배포 합니다.
* 분리만 hello 또는 hello 마지막 남은 iSCSI 사용 인터페이스 (Ip 할당), hello 인터페이스를 먼저 사용 하지 않도록 설정 하 고 hello 케이블을 분리 합니다. Hello 인터페이스 연결 되지 않은 경우 먼저, 다음 발생 합니다 hello 활성 컨트롤러 toofail toohello 수동 컨트롤러를 통해. Hello 수동 컨트롤러의 해당 인터페이스도 분리가, 두 hello 컨트롤러 한 컨트롤러를 결정 하기 전까지 여러 번을 재부팅 됩니다.
* 각 컨트롤러 모듈에서 두 개 이상의 데이터 인터페이스 toohello 네트워크를 연결 합니다.
* 두 개의 10 hello 10gbe 인터페이스를 사용 하는 경우 배포 서로 다른 스위치에 해당 합니다.
* 가능한 경우 링크, 네트워크 또는 인터페이스 오류 hello 서버 허용할 수 있는 서버 tooensure에서 MPIO를 사용 합니다.

너무 높은 가용성과 성능을 위해 장치 네트워킹에 대 한 자세한 내용을 보려면 이동[StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) 또는 [8600 StorSimple 장치 설치](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)합니다.

#### <a name="ssds-and-hdds"></a>SSD 및 HDD
StorSimple 장치에는 미러링된 공간을 사용하여 보호되는 SSD(Solid State Disk) 및 HDD(Hard Disk Drive)가 포함됩니다. 미러링된 공간을 사용 하면 해당 hello 장치는 하나 이상의 Ssd 또는 Hdd 수 tootolerate hello 실패 합니다.

* 모든 SSD 및 HDD 모듈이 설치되었는지 확인합니다.
* SSD 또는 HDD 문제가 있으면 즉시 교체를 요청합니다.
* SSD 또는 HDD에 오류가 발생 하거나 교체가 필요한, 경우에 SSD 또는 HDD 교체 해야 하는 hello만 제거 하는 있는지 확인 합니다.
* 제거 하지 마십시오 둘 이상의 SSD 또는 HDD 언제 든 지 hello 시스템에서 시간.
  특정 유형의 2개 이상의 디스크(HDD, SDD) 오류 또는 단시간 프레임 내의 연속된 오류는 시스템 오작동 및 잠재적 데이터 손실을 야기할 수 있습니다. 이 경우 지원을 위해 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 합니다.
* 교체 하는 동안 모니터링 hello **하드웨어 상태** hello에 **유지 관리** hello hello Ssd 및 Hdd의 드라이브 페이지입니다. 녹색 확인 나타나지만 hello 디스크 정상 인지 확인, 빨간색 느낌표 하지만 실패 한 SSD 또는 HDD를 나타냅니다.
* 시스템 오류 시 tooprotect 해야 하는 모든 볼륨에 대해 클라우드 스냅숏을 구성 하는 것이 좋습니다.

#### <a name="ebod-enclosure"></a>EBOD 인클로저
StorSimple 장치 모델 8600의 디스크 EBOD (Extended Bunch) 인클로저 더하기 toohello 기본 인클로저를 포함합니다. EBOD에는 미러링된 공간을 사용하여 보호되는 EBOD 컨트롤러 및 HDD(하드 디스크 드라이브)가 포함됩니다. 미러링된 공간을 사용 하면 해당 hello 장치는 하나 이상의 Hdd 수 tootolerate hello 실패 합니다. hello EBOD 인클로저는 중복 SAS 케이블 연결된 toohello 기본 인클로저 합니다.

* 다음 사항을 확인 두 EBOD 인클로저 컨트롤러 모듈, 두 SAS 케이블 및 모든 hello 하드 디스크 드라이브가 항상 설치 됩니다.
* EBOD 인클로저 컨트롤러 모듈에 오류가 있는 경우 즉시 교체를 요청합니다.
* EBOD 인클로저 컨트롤러 모듈에 오류가 발생 하면 해야 해당 hello hello 실패 한 모듈을 교체 하기 전에 다른 컨트롤러 모듈이 활성화 되어 있습니다. 컨트롤러가 활성 상태임 tooverify 너무 이동[식별 hello 장치에서 활성 컨트롤러](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)합니다.
* EBOD 컨트롤러 모듈 교체 하는 동안 지속적으로 상태를 모니터링 hello hello # hello StorSimple Manager 서비스에서에서 구성 요소에 액세스 하 여 **유지 관리** > **하드웨어 상태**합니다.
* SAS 케이블에 실패 하거나 (Microsoft 기술 지원 관련된 toomake 이러한 결정을 이어야 함) 교체 해야 있을 경우 교체 해야 하는 hello SAS 케이블만 제거 하는 있는지 확인 합니다.
* 동시에에서 제거 하지 마십시오 두 SAS 케이블 언제 든 지 hello 시스템 시간에서입니다.

### <a name="high-availability-recommendations-for-your-host-computers"></a>호스트 컴퓨터에 대한 고가용성 권장 사항
이러한 모범 사례 tooensure hello의 고가용성 호스트 연결 된 tooyour StorSimple 장치를 주의 깊게 검토 합니다.

* [2-노드 파일 서버 클러스터 구성][1]으로 StorSimple을 구성합니다. 단일 지점 오류 및 중복성 hello 호스트 측에서 빌드를 제거 하 여 hello 전체 솔루션 항상 사용할 수 있습니다.
* Hello 저장소 컨트롤러의 장애 조치 중 고가용성을 위해 Windows Server 2012 (SMB 3.0)와 함께 사용할 수 있는 지속적으로 사용 가능한 (CA) 공유를 사용 합니다. Windows Server 2012를 사용 하 여 파일 서버 클러스터와 지속적으로 사용 가능한 공유를 구성 하는 것에 대 한 자세한 내용은 참조 toothis [비디오 데모](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares)합니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 시스템 제한에 대해 자세히 알아봅니다](storsimple-limits.md).
* [자세한 내용은 방법 toodeploy StorSimple 솔루션](storsimple-deployment-walkthrough-u2.md)합니다.

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
