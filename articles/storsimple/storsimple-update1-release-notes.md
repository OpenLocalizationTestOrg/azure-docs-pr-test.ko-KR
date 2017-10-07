---
title: "aaaStorSimple 8000 시리즈 업데이트 1.2 릴리스 정보 | Microsoft Docs"
description: "StorSimple 8000 시리즈 업데이트 1.2에 대 한 hello 새로운 기능, 문제 및 해결 방법에 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>StorSimple 8000 시리즈 장치의 업데이트 1.2 릴리스 정보

## <a name="overview"></a>개요
hello 다음 릴리스 정보 hello 새로운 기능에 설명 하 고 StorSimple 8000 시리즈 업데이트 1.2에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한 hello StorSimple 소프트웨어, 드라이버 및이 릴리스에 포함 된 디스크 펌웨어 업데이트 목록을 포함 합니다. 

1.2 업데이트 릴리스 (GA), 업데이트 0.1, 0.2, 업데이트 또는 소프트웨어 업데이트 0.3 실행 하는 적용 된 tooany StorSimple 장치를 수 있습니다. 장치가 업데이트 1 또는 업데이트 1.1을 실행하는 경우에는 업데이트 1.2를 사용할 수 없습니다. 장치에서 릴리스 (GA) 실행 중인 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) tooassist는이 업데이트를 설치 합니다.

다음 테이블 목록 hello 장치 소프트웨어 버전 1, 1.1 및 1.2 tooUpdates에 해당 하는 번호입니다.

| 실행 중인 업데이트... | 장치 소프트웨어 버전 |
| --- | --- |
| 업데이트 1.2 |6.3.9600.17584 |
| 업데이트 1.1 |6.3.9600.17521 |
| 업데이트 1.0 |6.3.9600.17491 |

Hello 릴리스 노트 hello를 배포 하기 전에 StorSimple 솔루션의 업데이트에 포함 된 hello 정보를 검토 하십시오. 자세한 내용은 참조 방법을 너무[StorSimple 장치에 업데이트 1.2 설치](storsimple-install-update-1.md)합니다. 

> [!IMPORTANT]
> * 약 5-10 시간 tooinstall이이 업데이트 (hello Windows 업데이트 포함)이 필요 합니다. 
> * 업데이트 1.2에는 소프트웨어, LSI 드라이버 및 디스크 펌웨어 업데이트가 있습니다. tooinstall의 지침에 따라 hello [StorSimple 장치에 업데이트 1.2 설치](storsimple-install-update-1.md)합니다.
> * 새 릴리스를 위한 나타나지 않을 수 있습니다 업데이트 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 곧 사용할 수 있게 되므로 몇 일 후에 업데이트를 스캔합니다.
> 
> 

## <a name="whats-new-in-update-12"></a>업데이트 1.2의 새로운 기능
이러한 기능은 사용자 집합이 처리 된 사용 가능한 tooa 제한 된 업데이트 1과 함께 처음 릴리스 되었습니다. Hello 업데이트 1.2 릴리스에서 대부분의 hello StorSimple 사용자가 새로운 기능과 향상 된 다음 hello를 볼 수 있습니다.:

* **5000 7000 시리즈 too8000 시리즈 장치에서의 마이그레이션** –이 릴리스에 새로운 기능이 마이그레이션 hello StorSimple 5000 7000 시리즈 어플라이언스 사용자 toomigrate 수 있도록 해당 데이터 tooa StorSimple 8000 시리즈 실제 어플라이언스 또는 가상 기기입니다. hello 마이그레이션 기능에는 두 가지 핵심 가치 제안에 있습니다.                                                                  
  
  * **비즈니스 연속성**, 5000 7000 시리즈 어플라이언스 too8000 시리즈 어플라이언스 때 기존 데이터의 마이그레이션을 사용 하 여 합니다.
  * **기능 제공 hello 8000 시리즈 어플라이언스의 향상 된**, StorSimple Manager 서비스를 통해 여러 어플라이언스의 효율적인 중앙 집중식된 관리, 같은 향상 된 하드웨어 및 펌웨어, 가상 어플라이언스, 데이터 이동성 업데이트 및 향후 로드맵의 hello에 기능을 추가 합니다.
    
    Toohello 참조 [마이그레이션 가이드](http://www.microsoft.com/download/details.aspx?id=47322) 방법에 대 한 자세한 내용은 StorSimple 5000 7000 시리즈 tooan 8000 시리즈 장치 toomigrate 합니다. 
* **Hello Azure Government 포털에서에서 가용성** – 이제 StorSimple를 hello Azure Government 포털에서 사용할 수 있습니다. 너무 어떻게 참조[hello Azure Government 포털에서에서 StorSimple 장치 배포](storsimple-deployment-walkthrough-gov.md)합니다.
* **다른 클라우드 서비스 공급자에 대 한 지원** – hello 지원 되는 다른 클라우드 서비스 공급자는 Amazon S3, RR, HP, OpenStack (베타)와 Amazon S3 합니다.
* **저장소 Api toolatest 업데이트** – StorSimple 되었습니다이 릴리스에서 toohello 최신 Azure 저장소 서비스 Api를 업데이트 합니다. 업데이트 1 이전 소프트웨어 버전을 실행 하는 StorSimple 8000 시리즈 장치 (릴리스, 0.1, 0.2, 및 0.3) hello 2009 년 7 월 17 일 보다 오래 된 Azure 저장소 서비스 Api의 버전을 사용 하는입니다. 업데이트 하는 hello에 명시 된 대로 [저장소 서비스 버전을 제거 하는 방법에 대 한 알림](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), 2016 년 8 월 1 일에서 이러한 Api 지원 되지 것입니다. 적용 하는 hello StorSimple 8000 시리즈 업데이트 1 이전 tooAugust 1, 2016 합니다. 따라서 toodo를 실패할 경우 StorSimple 장치 정상적으로 작동 중지 됩니다.
* **지원에 대 한 영역 중복 저장소 (ZRS)** – 영역 중복 저장소 (ZRS)에 추가 tooLocally 중복 저장소 (LRS) 및 지리적 중복 hello hello 저장소 Api의 최신 버전을 업그레이드 toohello, hello StorSimple 8000 시리즈 지원 됩니다 저장소 (GRS)입니다. Toothis 참조 [Azure 저장소 중복 옵션에는 문서](../storage/common/storage-redundancy.md) ZRS 세부 정보에 대 한 합니다.
* **초기 배포 및 업데이트 환경이 향상** –이 릴리스에서 설치 hello 및 업데이트 프로세스가 향상 되었습니다. hello 설치 마법사를 통해 hello 설치는 hello 네트워크 구성 및 방화벽 설정에 올바르지 않은 경우 향상 된 tooprovide 피드백 toohello 사용자입니다. 추가 진단 cmdlet toohelp 제공 hello 장치의 네트워킹 문제 해결에 있습니다. Hello 참조 [문제 해결 배포 문서](storsimple-troubleshoot-deployment.md) 문제 해결을 위해 사용 되는 hello 새 진단 cmdlet에 대 한 자세한 내용은 합니다.

## <a name="issues-fixed-in-update-12"></a>업데이트 1.2에서 해결된 문제
다음 표에서 hello 1.2, 1.1 및 1 업데이트에서 해결 된 문제에 대 한 요약을 제공 합니다.    

| 아니요. | 기능 | 문제 | 해결된 업데이트 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |StorSimple용 Windows PowerShell |사용자 StorSimple 용 Windows PowerShell을 사용 하 여 hello StorSimple 장치에 원격으로 액세스 되 고 다음 hello 설치 마법사를 시작 하는 경우 충돌이 발생 한 빨리 데이터 0 IP를 입력 했습니다. 이 버그는 이제 업데이트 1에서 해결됩니다. |업데이트 1 |예 |예 |
| 2 |공장 재설정 |경우에 따라 공장 재설정을 수행할 때 hello StorSimple 장치 상태가 된 멈추고이 메시지를 표시 했습니다: **재설정 toofactory가 진행 중인 (8 단계)**합니다. 이러한 hello cmdlet 진행 중인 동안 CTRL + C를 누를 때 발생 합니다. 이 버그는 이제 수정되었습니다. |업데이트 1 |예 |아니요 |
| 3 |공장 재설정 |실패 한 이중 컨트롤러 공장 기본 설정 후 tooproceed 장치 등록을 허용 되었습니다. 이렇게 되면 지원되지않는 시스템 구성이 됩니다. 업데이트 1에는 오류 메시지가 표시되며 공장 재설정에 실패한 장치에서 차단됩니다. |업데이트 1 |예 |아니요 |
| 4 |공장 재설정 |일부 경우에 false positive 불일치 경고가 생성됩니다. 잘못된 불일치 경고는 업데이트 1을 실행 하는 장치에서 더 이상 생성되지 않습니다. |업데이트 1 |예 |아니요 |
| 5 |공장 재설정 |공장 기본 설정으로 중단 된 경우 이전 toocompletion hello 입력 장치 복구 모드,가 수 없습니다 tooaccess Windows PowerShell StorSimple에 대 한 합니다. 이 버그는 이제 수정되었습니다. |업데이트 1 |예 |아니요 |
| 6 |재해 복구 |재해 복구 (DR) 버그 수정 DR hello 검색 hello 대상 장치에서의 백업 중에 실패 하 게 가정해 보십시오. |업데이트 1 |예 |예 |
| 7 |모니터링 LED |경우에, hello 어플라이언스 뒷면에서 모니터링 Led는 올바른 상태를 표시 하지 않았습니다. hello 파란색 LED가 해제 되어 있습니다. 이러한 인터페이스가 구성되지 않더라도 데이터 0 및 데이터 1 LED는 깜박입니다. hello 문제 해결 및 모니터링 Led 이제 hello 올바른 상태를 나타냅니다. |업데이트 1 |예 |아니요 |
| 8 |모니터링 LED |경우에는 경우 업데이트 1을 적용 한 후 hello 활성 컨트롤러에서 파란색 hello light 해제 되어 받으므로 하드 tooidentify hello 활성 컨트롤러 있습니다. 이 문제는 이 패치 릴리스에서 해결되었습니다. |업데이트 1.2 |예 |아니요 |
| 9 |네트워크 인터페이스 |이전 버전에서는 게이트웨이가 라우팅할 수 없는 StorSimple 장치는 오프라인 상태가 될 수 있었습니다. 이 릴리스에서 Data 0에 대 한 라우팅 메트릭이 hello 이루어졌을 hello 가장 낮은; 따라서 경우에 다른 네트워크 인터페이스 클라우드 사용을 통해 Data 0에 hello 장치에서 모든 hello 클라우드 트래픽이 라우팅됩니다. |업데이트 1 |예 |예 |
| 10 |백업 |Hello 패치에 백업을 toofail 24 일 해결 된 후 발생 하는 업데이트 1의 버그 업데이트 1.1을 해제 합니다. |업데이트 1.1 |예 |예 |
| 11 |백업 |이전 버전의 버그로 인해 변경률이 낮은 클라우드 스냅숏에 대한 성능이 저하되었습니다. 이 버그는 이 패치 릴리스에서 수정되었습니다. |업데이트 1.2 |예 |예 |
| 12 |업데이트 |이 패치 릴리스에서 실패 한 업그레이드를 보고 하 고 복구 모드로 hello 컨트롤러 toogo 발생 하는 업데이트 1의 버그가 수정 되었습니다. |업데이트 1.2 |예 |예 |

## <a name="known-issues-in-update-12"></a>업데이트 1.2의 알려진 문제
다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.

| 아니요. | 기능 | 문제 | 주석/해결 방법 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |디스크 쿼럼 |경우에 따라에서 hello 대부분의 디스크 8600 장치의 EBOD 인클로저에 hello 끊어져서 디스크 쿼럼이 없게 하는 경우 다음 hello 저장소 풀이 오프 라인 상태가 됩니다. Hello 디스크가 다시 연결 하는 경우에 오프 라인으로 유지 됩니다. |Tooreboot hello 장치가 필요 합니다. Hello 문제가 지속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |예 |아니요 |
| 2 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 하는 동안 hello 이미지 hello 피어 노드에서 로드 되 면 hello 컨트롤러 ID 수 처음으로 나타나도록 hello 피어 컨트롤러의 id입니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 이 경우 hello 컨트롤러 교체를 완료 한 후 자체적으로 해결 됩니다. |예 |아니요 |
| 3 |저장소 계정 |Hello 저장소 서비스 toodelete hello 저장소 계정을 사용 하는 지원 되지 않는 시나리오입니다. 이렇게 하면 tooa 상황 사용자 데이터를 검색할 수 없습니다. |예 |예 | |
| 4 |장치 장애 조치 |다중에서 동일한 원본 장치 toodifferent 대상 장치는 지원 되지 않습니다 hello는 볼륨 컨테이터의 장애 조치 합니다. 장치 장애 조치 단일 데드 장치 toomultiple 장치에서 먼저 장치 조치할 hello 장치의 hello 볼륨 컨테이너가 데이터 소유권을 잃게 생성 됩니다. 이러한 장애 조치 후 이러한 볼륨 컨테이너 나타나거나 hello Azure 클래식 포털에서에서 볼 때 다르게 동작 합니다. | |예 |아니요 |
| 5 |설치 |SharePoint 용 StorSimple 어댑터를 하는 동안 필요한 tooprovide hello 설치 toofinish 위해에서 장치 IP 성공적으로 합니다. | |예 |아니요 |
| 6 |웹 프록시 |웹 프록시 구성에 있으면 hello로는 HTTPS 프로토콜을 지정 다음 장치를 서비스 통신 영향을 받고 hello 장치는 오프 라인 상태가 유지 됩니다. 지원 패키지도 장치에서 많은 리소스를 소모 hello 프로세스에서 생성 됩니다. |지정한 프로토콜이 hello으로 hello 웹 프록시 URL에 HTTP 있는지 확인 합니다. 자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](storsimple-configure-web-proxy.md)합니다. |예 |아니요 |
| 7 |웹 프록시 |구성 하 고 등록된 된 장치에서 웹 프록시를 사용 하는 경우 장치에서 toorestart hello 활성 컨트롤러가 필요 합니다. | |예 |아니요 |
| 8 |긴 클라우드 대기 시간 및 많은 I/O 작업 |StorSimple 장치 매우 긴 클라우드 대기 시간 (초) 및 높은 수준의 I/O 작업의 조합을 발견 하면 hello 장치 볼륨 상태가 저하 및 hello I/o "장치가 준비 되지 않음" 오류가 발생할 수 있습니다. |Toomanually 재부팅 hello 장치 컨트롤러 필요 하거나이 상황에서 장치 장애 조치 toorecover를 수행 합니다. |예 |아니요 |
| 9 |Azure PowerShell |Hello StorSimple cmdlet을 사용 하는 경우 **Get AzureStorSimpleStorageAccountCredential &#124; Select-object-처음 1-대기** tooselect 새를 만들 수 있도록 첫 번째 개체를 hello **VolumeContainer** 개체 hello cmdlet 모든 hello 개체를 반환 합니다. |다음과 같이 괄호로 hello cmdlet wrap: **(Get Azure StorSimpleStorageAccountCredential) &#124; Select-object-처음 1-대기** |예 |예 |
| 10 |마이그레이션 |여러 볼륨 컨테이너는 마이그레이션에 대 한 전달 되는 경우 최신 백업 에타 hello는 hello 첫 번째 볼륨 컨테이너에 대 한 정확한 합니다. 또한 병렬 마이그레이션 hello hello 첫 번째 볼륨 컨테이너에서 처음 4 백업이 마이그레이션된 후 시작 됩니다. |한번에 하나의 볼륨 컨테이너를 마이그레이션하는 것이 좋습니다. |예 |아니요 |
| 11 |마이그레이션 |Hello 복원 후 볼륨 toohello 백업 정책 또는 hello 가상 디스크 그룹을 추가 되지 않습니다. |Tooadd 이러한 볼륨 tooa 백업 정책 순서 toocreate 백업에 필요 합니다. |예 |예 |
| 12 |마이그레이션 |Hello 5000/7000 시리즈 장치 액세스 하지 않아야 hello 마이그레이션이 완료 되 면 hello 마이그레이션된 데이터 컨테이너입니다. |Hello를 삭제 하는 것이 좋습니다 hello 마이그레이션이 완료 되 고 커밋된 후 데이터 컨테이너를 마이그레이션됩니다. |예 |아니요 |
| 13 |복제 및 DR |업데이트 1을 실행 하는 StorSimple 장치를 복제 하거나 전 업데이트 1 소프트웨어를 실행 하는 tooa 장치 재해 복구를 수행할 수 없습니다. |이러한 작업 tooupdate hello 대상 장치 tooUpdate 1 tooallow 필요 합니다. |예 |예 |
| 14 |마이그레이션 |볼륨 그룹과 연결된 볼륨이 없으면 마이그레이션에 대한 구성 백업은 5000-7000 시리즈 장치에서 실패할 수 있습니다. |연결 된 볼륨이 없으면 인 모든 hello 빈 볼륨 그룹을 삭제 하 고 hello 구성 백업을 다시 시도 하십시오. |예 |아니요 |

## <a name="physical-device-updates-in-update-12"></a>업데이트 1.2의 물리적 장치 업데이트
패치 업데이트가 1.2 적용된 tooa 물리적 장치 (버전 이전 tooUpdate 1 실행) 인 경우 hello 소프트웨어 버전 too6.3.9600.17584를 변경 됩니다.

## <a name="controller-and-firmware-updates-in-update-12"></a>업데이트 1.2의 컨트롤러 및 펌웨어 업데이트
이 릴리스는 hello 드라이버 및 장치에서 hello 디스크 펌웨어를 업데이트합니다.

* Hello SAS 컨트롤러 업데이트에 대 한 자세한 내용은 참조 [업데이트 1이 Microsoft Azure StorSimple 어플라이언스의 LSI SAS 컨트롤러용](https://support.microsoft.com/kb/3043005)합니다. 
* Hello 디스크 펌웨어 업데이트에 대 한 자세한 내용은 참조 [디스크 펌웨어 업데이트 1이 Microsoft Azure StorSimple 어플라이언스 용](https://support.microsoft.com/kb/3063416)합니다.

## <a name="virtual-device-updates-in-update-12"></a>업데이트 1.2의 가상 장치 업데이트
이 업데이트는 적용 된 toohello 가상 장치 수 없습니다. 새 가상 장치 생성 toobe가 필요 합니다. 

## <a name="next-steps"></a>다음 단계
* [장치에 업데이트 1.2를 설치합니다](storsimple-install-update-1.md).

