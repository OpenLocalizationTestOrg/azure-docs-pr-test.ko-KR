---
title: "aaaMicrosoft Azure StorSimple 가상 배열에 대 한 시스템 요구 사항 | Microsoft Docs"
description: "StorSimple 가상 배열 hello 소프트웨어 및 네트워킹 요구 사항"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>StorSimple 가상 배열 시스템 요구 사항
## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure StorSimple 가상 배열 및 hello 배열에 액세스 하는 hello 저장소 클라이언트 hello 중요 한 시스템 요구 사항 설명 합니다. 정보를 검토 하 hello 신중 하 게 배포 및 후속 작동 하는 동안 필요에 따라 tooit 다시 참조할 및 StorSimple 시스템을 배포 하기 전에 것이 좋습니다.

hello 시스템 요구 사항:

* **저장소 클라이언트에 대 한 소프트웨어 요구 사항** -지원 hello 가상화 플랫폼, 웹 브라우저, iSCSI 초기자, SMB 클라이언트, 최소 가상 장치 요구 사항 및 이러한 운영 체제에 대 한 추가 요구 사항이 설명 합니다.
* **Hello StorSimple 장치의 네트워킹 요구 사항** -iSCSI, 클라우드 또는 관리 트래픽을 방화벽 tooallow에 열려 해당 필요 toobe hello 포트에 대 한 정보를 제공 합니다.

hello StorSimple 시스템 요구 사항 정보는이 문서에서 게시 tooStorSimple 가상 배열만 적용 됩니다.

* 8000 시리즈 장치에 대 한 이동 너무[StorSimple 8000 시리즈 장치에 대 한 시스템 요구 사항](storsimple-system-requirements.md)합니다.
* 7000 시리즈 장치에 대 한 이동 너무[StorSimple 5000 7000 시리즈 장치에 대 한 시스템 요구 사항](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements)합니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항
소프트웨어 요구 사항 hello hello 지원 웹 브라우저, SMB 버전, 가상화 플랫폼 및 hello 최소 가상 장치 요구 사항에 hello 정보를 포함 합니다.

### <a name="supported-virtualization-platforms"></a>지원되는 가상화 플랫폼
| **하이퍼바이저** | **버전** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 이상 |
| VMware ESXi |5.5 이상 |

### <a name="virtual-device-requirements"></a>가상 장치 요구 사항
| **구성 요소** | **요구 사항** |
| --- | --- |
| 최소 가상 프로세서(코어) 수 |4 |
| 최소 메모리(RAM) |8GB <br> 파일 서버의 경우 2백만 개 미만의 파일에 대해 8GB, 2-4백만 개 파일에 대해 16GB|
| 디스크 공간<sup>1</sup> |OS 디스크 - 80GB  <br></br>데이터 디스크-500GB too8 TB |
| 최소 네트워크 인터페이스 수 |1 |
| 최소 인터넷 대역폭<sup>2</sup> |5Mbps |

<sup>1</sup> - 씬 프로비전됨

<sup>2</sup> -네트워크 요구 사항 hello 일별 데이터 변경 률에 따라 다를 수 있습니다. 예를 들어 하루 동안 tooback 10GB 또는 많은 변경 사항을 적용 해야 하는 장치, 하는 경우 다음 hello 5 Mbps 연결을 통해 매일 백업 수을 차지 too4.25 시간 (hello 데이터를 압축 하거나 중복 수 없습니다).

### <a name="supported-web-browsers"></a>지원되는 웹 브라우저
| **구성 요소** | **버전** | **추가 요구 사항/메모** |
| --- | --- | --- |
| Microsoft Edge |최신 버전 | |
| Internet Explorer |최신 버전 |Internet Explorer 11로 테스트함 |
| Google Chrome |최신 버전 |Chrome 46으로 테스트함 |

### <a name="supported-storage-clients"></a>지원되는 저장소 클라이언트
StorSimple 가상 배열 (iSCSI 서버로 구성)에 액세스 하는 hello iSCSI 초기자에 대 한 소프트웨어 요구 사항을 준수 하는 hello가 됩니다.

| **지원되는 운영 체제** | **필요한 버전** | **추가 요구 사항/메모** |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2 |StorSimple은 씬 프로비전된 볼륨과 완전히 프로비전된 볼륨을 만들 수 있습니다. 부분적으로 프로비전된 볼륨은 만들 수 없습니다. StorSimple iSCSI 볼륨은 다음에 대해서만 지원합니다:  <ul><li>Windows 기본 디스크의 단순 볼륨.</li><li>볼륨 포맷을 위한 Windows NTFS.</li> |

StorSimple 가상 배열 (파일 서버로 구성)에 액세스 하는 SMB 클라이언트 hello에 대 한 소프트웨어 요구 사항을 준수 하는 hello가 됩니다.

| **SMB 버전** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> 복사 하지 않거나 Windows 파일 시스템 EFS (암호화) toohello StorSimple 가상 배열 파일 서버;에서 보호 되는 파일을 저장 합니다. 그러면 구성이 지원 됩니다. 
> 

### <a name="supported-storage-format"></a>지원되는 저장소 형식
Hello Azure 블록 blob 저장소만 지원 됩니다. 페이지 Blob은 지원되지 않습니다. [블록 Blob 및 페이지 Blob에 대한](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 자세한 내용입니다.

## <a name="networking-requirements"></a>네트워킹 요구 사항
hello 다음 표 toobe iSCSI, SMB, 클라우드 또는 관리 트래픽을 대 한 방화벽 tooallow 프로그램에서 열 필요로 하는 hello 포트입니다. 이 표에 *에* 또는 *인바운드* toohello 방향에서 들어오는 클라이언트 요청 액세스할 수 있는 장치를 참조 합니다. *Out* 또는 *아웃 바운드* 는 StorSimple 장치 hello 배포를 벗어나 외부로 데이터를 전송 toohello 방향 참조: 인터넷 아웃 바운드 toohello 예를 들어 있습니다.

| **포트 번호<sup>1</sup>** | **인 또는 아웃** | **포트 범위** | **필수** | **참고 사항** |
| --- | --- | --- | --- | --- |
| TCP 80(HTTP) |아웃 |WAN |아니요 |아웃 바운드 포트는 인터넷 액세스 tooretrieve 업데이트에 사용 됩니다. <br></br>hello 아웃 바운드 웹 프록시는 사용자가 구성할 수 있습니다. |
| TCP 443(HTTPS) |아웃 |WAN |예 |아웃 바운드 포트는 hello 클라우드에서 데이터에 액세스 하기 위해 사용 됩니다. <br></br>hello 아웃 바운드 웹 프록시는 사용자가 구성할 수 있습니다. |
| UDP 53(DNS) |아웃 |WAN |일부 경우에는 메모를 참조하십시오. |이 포트는 인터넷 기반 DNS 서버로 사용하는 경우에만 필요합니다. <br></br> 파일 서버를 배포하는 경우에는 로컬 DNS 서버를 사용하는 것이 좋습니다. |
| UDP 123(NTP) |아웃 |WAN |일부 경우에는 메모를 참조하십시오. |이 포트는 인터넷 기반 NTP 서버로 사용하는 경우에만 필요합니다.<br></br> 파일 서버를 배포하는 경우 Active Directory 도메인 컨트롤러와 시간을 동기화하는 것이 좋습니다. |
| TCP 80(HTTP) |그런 다음 |LAN |예 |로컬 관리에 대 한 hello StorSimple 장치에 로컬 UI에 대 한 인바운드 포트를 hello은이 있습니다. <br></br> HTTP를 통해 로컬 UI hello에 액세스 하는 참고 tooHTTPS 자동 리디렉션됩니다. |
| TCP 443(HTTPS) |그런 다음 |LAN |예 |로컬 관리에 대 한 hello StorSimple 장치에 로컬 UI에 대 한 인바운드 포트를 hello은이 있습니다. |
| TCP 3260(iSCSI) |그런 다음 |LAN |아니요 |이 포트는 iSCSI를 통해 사용 되는 tooaccess 데이터는입니다. |

<sup>1</sup> 인바운드 포트가 없습니다 필요 toobe에서 연 공용 인터넷 hello 합니다.

> [!IMPORTANT]
> Hello 방화벽을 수정 하거나 hello StorSimple 장치와 Azure 간의 SSL 트래픽을 암호를 해독 하지 않습니다 확인 합니다.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>방화벽 규칙에 대한 URL 패턴
네트워크 관리자는 hello URL 패턴 toofilter hello에 따라 규칙 인바운드 및 아웃 바운드 트래픽을 hello 고급 방화벽을 구성할 종종 있습니다. 가상 배열 및 hello StorSimple 장치 관리자 서비스는 Azure 서비스 버스, Azure Active Directory 액세스 제어, 저장소 계정 및 Microsoft 업데이트 서버와 같은 다른 Microsoft 응용 프로그램에 따라 달라 집니다. 이러한 응용 프로그램과 관련 된 hello URL 패턴에 사용 되는 tooconfigure 방화벽 규칙 될 수 있습니다. 이러한 응용 프로그램과 관련 된 hello URL 패턴을 변경할 수 있는 중요 한 toounderstand 것 합니다. 이 차례로 및 필요 합니다. 네트워크 관리자 toomonitor hello로 StorSimple에 대 한 고 필요한 경우 방화벽 규칙을 업데이트 합니다. 

StorSimple 고정 IP 주소에 따라 대부분의 경우에서 자유롭게 아웃바운드 트래픽에 대한 방화벽 규칙을 설정하는 것이 좋습니다. 그러나 고급 방화벽 규칙을 필요한 toocreate 보안 환경 tooset 아래 hello 정보를 사용할 수 있습니다.

> [!NOTE]
> 
> * 항상 hello 장치 (원본) Ip tooall hello 클라우드 지원 네트워크 인터페이스 설정 되어야 합니다. 
> * hello 대상 Ip 너무 설정할지[Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653)합니다.
> 
> 

| URL 패턴 | 구성 요소/기능 |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple 장치 관리자 서비스<br>액세스 제어 서비스<br>Azure 서비스 버스 |
| `http://*.backup.windowsazure.com` |장치 등록 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |인증서 해지 |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 저장소 계정 및 모니터링 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft 업데이트 서버<br> |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |
| `https://*.partners.extranet.microsoft.com/*` |지원 패키지 |
| `http://*.data.microsoft.com ` |Windows에서 원격 분석 서비스 참조 hello [customer experience 및 진단 원격 분석에 대 한 업데이트](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>다음 단계
* [StorSimple 가상 배열 hello 포털 toodeploy 준비](storsimple-virtual-array-deploy1-portal-prep.md)

