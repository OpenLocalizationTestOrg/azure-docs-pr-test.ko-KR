---
title: "aaaStorSimple 8000 시리즈 솔루션 개요 | Microsoft Docs"
description: "StorSimple 계층화, hello 장치, 가상 장치, 서비스 및 저장소 관리에 설명 하 고 StorSimple에 사용 된 주요 용어를 소개 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션
## <a name="overview"></a>개요
TooMicrosoft Azure StorSimple, 온-프레미스 장치 및 Microsoft Azure 클라우드 저장소 간의 저장소 작업을 관리 하는 통합된 저장소 솔루션을 시작 합니다. StorSimple은 다양 한 hello 문제 및 엔터프라이즈 저장소 및 데이터 보호와 관련 된 비용을 제거 하는 효율적이 고 쉽게 관리할 수 있는, 비용 효율적인 저장소 영역 네트워크 (SAN) 솔루션입니다. StorSimple 8000 시리즈 장치를 소유 하는 hello를 사용 하 여, 클라우드 서비스와 통합 하 고 클라우드 저장소를 포함 하 여 모든 엔터프라이즈 저장소를 원활 하 게 보기에 대 한 관리 도구 집합을 제공 합니다. (hello Microsoft Azure 웹 사이트에 게시 된 StorSimple 배포 정보를 hello tooStorSimple 8000 시리즈 장치에만 적용 하는 데 사용 합니다. StorSimple 5000/7000 시리즈 장치를 사용 하는 경우 너무 이동[StorSimple 도움말](http://onlinehelp.storsimple.com/).)

사용 하 여 StorSimple [저장소 계층화](#automatic-storage-tiering) toomanage 다양 한 저장소 미디어를 통해 데이터를 저장 합니다. hello 현재 작업 집합 저장된 온-프레미스에 반도체 드라이브 (Ssd) 데이터가 덜 자주 사용 되는 하드 디스크 드라이브 (Hdd)에 저장 되어 있고, 않는 아카이브 데이터 toohello 클라우드 푸시됩니다. 또한 StorSimple 중복 제거를 사용 하 고 데이터 hello 저장소 양을 tooreduce hello 압축 사용 합니다. 자세한 내용은 이동 너무[중복 제거와 압축](#deduplication-and-compression)합니다. 정의 다른 주요 용어와 개념 hello StorSimple 8000 시리즈 설명서에 사용 된 경우 이동 너무[StorSimple 용어](#storsimple-terminology) hello이이 문서의 뒷부분에 있습니다.

또한 toostorage 관리 StorSimple 데이터 보호 기능을 사용 하면 toocreate 요청 시 및 예약 된 백업 및 hello에 로컬 또는 클라우드에 해당 하는 다음 저장소. 백업은 증분 스냅숏를 생성 하 고 수 신속 하 게 복원 즉 hello 양식에서 수행 됩니다. 클라우드 스냅숏은 (예: 테이프 백업) 보조 저장소 시스템을 바꾸고 필요한 경우 toorestore 데이터 tooyour 데이터 센터 또는 tooalternate 사이트를 허용 하기 때문에 재해 복구 시나리오에서 매우 중요할 수 있습니다.

![동영상 아이콘](./media/storsimple-overview/video_icon.png) 간략 한 소개 tooMicrosoft Azure StorSimple에 대 한 hello 비디오를 시청 하세요.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>StorSimple을 사용하는 이유
hello 다음 표에 제공 하는 Microsoft Azure StorSimple hello 주요 이점 중 일부 있습니다.

| 기능 | 혜택 |
| --- | --- |
| 투명한 통합 |Hello iSCSI 프로토콜 tooinvisibly 링크 데이터 저장소 기능을 사용합니다. 따라서 hello 클라우드, hello 데이터 센터에에서 저장 된 데이터 또는 원격 서버의 단일 위치에 저장 된 toobe 나타납니다. |
| 저장소 비용 감소 |충분 한 로컬 할당 또는 클라우드 저장소 toomeet 현재 요구 하 고, 필요한 경우에 클라우드 저장소를 확장 합니다. 더욱 감소 저장소 요구 사항 및 비용 hello의 중복 버전을 제거 하 여 동일한 데이터 (중복 제거) 하 고 압축을 사용 하 여 합니다. |
| 단순화된 저장소 관리 |시스템 관리 도구 tooconfigure 제공 하 고 저장 된 데이터를 온-프레미스에 hello 클라우드 및 원격 서버에서 관리 합니다. 또한 Microsoft Management Console(MMC) 스냅인에서 백업 및 복원 기능을 관리할 수 있습니다.|
| 향상된 재해 복구 및 규정 준수 |복구 시간을 확장할 필요가 없습니다. 대신, 필요할 때마다 데이터를 복원합니다. 즉, 정상 작업 중단을 최소화하면서 계속할 수 있습니다. 또한 정책 toospecify 백업 일정 및 데이터 보존을 구성할 수 있습니다. |
| 데이터 이동성 |데이터 업로드 tooMicrosoft Azure 클라우드 서비스 복구 및 마이그레이션 목적으로 다른 사이트에서 액세스할 수 있습니다. 또한 Microsoft Azure에서 실행 중인 가상 컴퓨터 (Vm)에서 StorSimple tooconfigure StorSimple 클라우드 어플라이언스에 사용할 수 있습니다. hello Vm에 대 한 테스트 또는 복구를 위해 가상 장치 tooaccess 저장 된 데이터를 유도할 수 있습니다. |
| 비즈니스 연속성 |StorSimple 5000 7000 시리즈 사용자 toomigrate 데이터 tooa StorSimple 8000 시리즈 장치를 수 있습니다. |
| Hello Azure Government 포털의 가용성 |StorSimple는 hello Azure Government 포털에서에서 제공 됩니다. 자세한 내용은 참조 [hello 정부 포털에서에서 온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-gov-u2.md)합니다. |
| 데이터 보호 및 가용성 |StorSimple 8000 시리즈 hello 영역 중복 저장소 (ZRS), 더하기 tooLocally 중복 저장소 (LRS)에서 및 지역 중복 저장소 (GRS)를 지원합니다. 너무 참조[Azure 저장소 중복 옵션에도 본이 문서](https://azure.microsoft.com/documentation/articles/storage-redundancy/) ZRS 세부 정보에 대 한 합니다. |
| 중요한 응용 프로그램에 대한 지원 |그러면 내용이 중요 한 응용 프로그램에 필요한 데이터를 계층화 된 toohello 없습니다 로컬로 고정 포인터로 적절 한 볼륨을 식별 하는 StorSimple 통해 클라우드 있습니다. 로컬 고정된 볼륨이 주체 toocloud 대기 시간이 이나 연결에 문제가 발생 하지 않습니다. 로컬 고정된 볼륨에 대 한 자세한 내용은 참조 [hello StorSimple 장치 관리자 서비스 toomanage 볼륨을 사용 하 여](storsimple-8000-manage-volumes-u2.md)합니다. |
| 짧은 대기 시간 및 고성능 |Hello 높은 성능, Azure 프리미엄 저장소의 대기 시간이 짧은 기능을 이용 하는 클라우드 어플라이언스에 만들 수 있습니다. StorSimple Premium Cloud Appliance에 대한 자세한 내용은 [Azure에서 StorSimple Cloud Appliance 배포 및 관리](storsimple-8000-cloud-appliance-u2.md)로 이동합니다. |


## <a name="storsimple-components"></a>StorSimple 구성 요소
Microsoft Azure StorSimple 솔루션 hello를 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

* **Microsoft Azure StorSimple 장치** – SSD 및 HDD가 포함된 온-프레미스 하이브리드 저장소 배열로, 중복 컨트롤러 및 자동 장애 조치 기능을 함께 제공합니다. hello 컨트롤러는 저장소 계층화, 현재 사용 되는 (또는 핫) 데이터 배치 (hello 장치 또는 온-프레미스 서버)의 로컬 저장소에 toohello 클라우드 덜 사용 되는 데이터를 이동 하는 동안 관리 합니다.
* **StorSimple 클라우드 어플라이언스에** – 라고도 StorSimple 가상 어플라이언스 hello, 이것이 hello 아키텍처를 복제 하는 hello StorSimple 장치의 소프트웨어 버전 및 대부분의 기능은 hello 물리적 하이브리드 저장 장치입니다. StorSimple 클라우드 어플라이언스에 hello Azure 가상 컴퓨터의 단일 노드에서 실행 됩니다. Azure 프리미엄 저장소를 활용하는 프리미엄 가상 장치는 업데이트 2 이상에서 사용할 수 있습니다.
* **StorSimple 장치 관리자 서비스** –는 hello 단일 웹 인터페이스에서 StorSimple 장치 또는 StorSimple 클라우드 장비를 관리할 수 있는 Azure 포털의 확장입니다. 있습니다 수 StorSimple 장치 관리자 서비스 toocreate hello를 사용 하 여 및 서비스 관리, 및 장치를 관리, 경고 보기의 볼륨 관리 및 보기 및 보기 및 관리 백업 정책 hello 백업 카탈로그.
* **StorSimple 용 Windows PowerShell** – toomanage를 사용할 수 있는 명령줄 인터페이스 hello StorSimple 장치입니다. StorSimple 용 Windows PowerShell에는 StorSimple 장치 tooregister 사용할 수 있는 기능, 장치에서 hello 네트워크 인터페이스 구성, 특정 형식의 업데이트를 설치, hello 지원 세션에 액세스 하 여 장치 문제 해결 및 hello 변경 장치 상태입니다. 연결 toohello 직렬 콘솔 또는 Windows PowerShell 원격을 사용 하 여 StorSimple 용 Windows PowerShell을 액세스할 수 있습니다.
* **Azure PowerShell StorSimple cmdlet** – hello 명령줄에서 tooautomate 서비스 수준 및 마이그레이션 작업을 허용 하는 Windows PowerShell cmdlet 컬렉션입니다. StorSimple 용 hello Azure PowerShell cmdlet에 대 한 자세한 내용을 보려면 이동 toohello [cmdlet 참조](/powershell/module/azure/?view=azuresmps-3.7.0#azure)합니다.
* **StorSimple 스냅숏 관리자** -볼륨 그룹 및 hello Windows 볼륨 섀도 복사본 서비스 toogenerate 응용 프로그램에 일관 된 백업을 사용 하는 MMC 스냅인입니다. StorSimple 스냅숏 관리자 toocreate 백업 일정 및 복제를 사용 하거나 볼륨을 복원할 수 있습니다.
* **SharePoint 용 StorSimple 어댑터** – 투명 하 게 볼 수 있는 및 hello SharePoint 중앙에서에서 관리할 수 있는 StorSimple 저장소를 만드는 동안 Microsoft Azure StorSimple 저장소 및 데이터 보호 tooSharePoint 서버 팜을 확장 하는 도구 관리 포털입니다.

아래 hello 다이어그램은 높은 수준의 hello Microsoft Azure StorSimple 아키텍처 및 구성 요소를 제공합니다.

![StorSimple 아키텍처](./media/storsimple-overview/overview-big-picture.png)

hello 다음 섹션에서는 이러한 각 구성이 요소를 더 자세히 설명 하 고 hello 솔루션을 데이터 정렬, 저장소, 할당 및 저장소 관리 및 데이터 보호 방법을 설명 합니다. hello 마지막 섹션의 hello 중요 한 용어 및 개념 tooStorSimple 관련된 구성 요소와 해당 관리에 대 한 정의 제공합니다.

## <a name="storsimple-device"></a>StorSimple 장치
hello Microsoft Azure StorSimple 장치는 기본 저장소 및 여기에 저장 하는 iSCSI 액세스 toodata 제공 하는 온-프레미스 하이브리드 저장소 배열입니다. 클라우드 저장소와 통신을 관리 하 고 tooensure hello 보안과 hello Microsoft Azure StorSimple 솔루션에 저장 된 모든 데이터의 기밀은 데 도움이 됩니다.

hello StorSimple 장치에는 Ssd 및 Hdd 하드 디스크 드라이브, 뿐 아니라 클러스터링 및 자동 장애 조치에 대 한 지원이 포함 되어 있습니다. 공유 프로세서, 공유 저장소 및 미러링된 컨트롤러 두 개를 포함합니다. 각 컨트롤러 hello 다음을 제공합니다.

* 연결 tooa 호스트 컴퓨터
* Toosix 네트워크 포트 tooconnect toohello 로컬 영역 네트워크 (LAN)를
* 하드웨어 모니터링
* 전원이 중단되는 경우 정보를 유지하는 비휘발성 임의 액세스 메모리(NVRAM)
* 클러스터 인식 hello 업데이트에는 최소한의 있도록 장애 조치 클러스터의 서버에서 toomanage 소프트웨어 업데이트를 업데이트 하거나 서비스 가용성에 영향을 주지 않습니다
* 백엔드 클러스터와 같은 기능의 클러스터 서비스는 고가용성을 제공하며 HDD 또는 SSD가 고장나거나 오프라인으로 전환되는 경우 발생할 수 있는 부정적인 영향을 최소화합니다.

언제든지 컨트롤러 하나만 활성화됩니다. Hello 활성 컨트롤러에 오류가 발생 하는 경우 hello 두 번째 컨트롤러가 자동으로 활성화 됩니다.

자세한 내용은 이동 너무[StorSimple 하드웨어 구성 요소 및 상태](storsimple-8000-monitor-hardware-status.md)합니다.

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
StorSimple toocreate hello 아키텍처와 hello 물리적 하이브리드 저장 장치 기능을 복제 하는 클라우드 어플라이언스에 사용할 수 있습니다. hello StorSimple 클라우드 어플라이언스에 (라고도 hello StorSimple 가상 어플라이언스)는 Azure 가상 컴퓨터의 단일 노드에서 실행 됩니다. (클라우드 어플라이언스는 Azure 가상 컴퓨터에만 만들 수 있습니다. StorSimple 장치 또는 온-프레미스 서버에 만들 수 없습니다.)

hello 클라우드 어플라이언스에 같은 기능 hello에 있습니다.

* 물리적 어플라이언스 처럼 동작 하 고 hello 클라우드에서 인터페이스 toovirtual 컴퓨터는 iSCSI를 제공할 수 있습니다.
* 클라우드 어플라이언스에 개수에 제한 없이 hello 클라우드에서 만들고 필요에 따라 및 해제 하 여 설정할 수 있습니다.
* 재해 복구, 개발 및 테스트 시나리오에서 온-프레미스 환경을 시뮬레이션할 수 있고 백업에서 항목 수준의 검색에 도움이 될 수 있습니다.

StorSimple 클라우드 어플라이언스에 hello는 두 가지 모델에서 사용할 수 있는: hello 8010 장치 (이전의 hello 1100 모델) 및 hello 8020 장치입니다. hello 8010 장치 30TB의 최대 용량을 있습니다. Azure 프리미엄 저장소를 활용 하는 hello 8020 장치를 64TB의 최대 용량을 있습니다. (로컬 계층에서 Azure 프리미엄 저장소는 SSD에 데이터를 저장하는 반면 표준 저장소는 HDD에 데이터를 저장합니다.) 참고 Azure 프리미엄 저장소 계정 toouse 프리미엄 저장소를가지고 있어야 합니다. 프리미엄 저장소에 대 한 자세한 내용은 이동 너무[프리미엄 저장소: Azure 가상 컴퓨터 워크 로드 용 고성능 저장소](../storage/common/storage-premium-storage.md)합니다.

너무 StorSimple 클라우드 어플라이언스에 hello에 대 한 자세한 내용을 보려면 이동[배포 및 관리 azure에서 StorSimple 클라우드 어플라이언스에](storsimple-8000-cloud-appliance-u2.md)합니다.

## <a name="storsimple-device-manager-service"></a>StorSimple 장치 관리자 서비스
Microsoft Azure StorSimple을 사용할 수 있는 웹 기반 사용자 인터페이스 (hello StorSimple 장치 관리자 서비스) 제공 toocentrally 데이터 센터를 관리 하 고 클라우드 저장소입니다. 작업을 수행 하는 hello StorSimple 장치 관리자 서비스 tooperform hello를 사용할 수 있습니다.

* StorSimple 장치에 대한 시스템 설정을 구성합니다.
* StorSimple 장치에 대한 보안 설정을 구성하고 관리합니다.
* 클라우드 자격 증명 및 속성을 구성합니다.
* 서버에서 볼륨을 구성하고 관리합니다.
* 볼륨 그룹을 구성합니다.
* 데이터를 백업하고 복원합니다.
* 성능을 모니터링합니다.
* 시스템 설정을 검토하고 발생 가능한 문제를 식별합니다.

Hello StorSimple 장치 관리자 서비스 tooperform 시스템 중단 초기 설치 및 업데이트의 설치와 같은 시간을 필요로 하는 것을 제외한 모든 관리 태스크를 사용할 수 있습니다.

자세한 내용은 이동 너무[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

## <a name="windows-powershell-for-storsimple"></a>StorSimple용 Windows PowerShell
StorSimple 용 Windows PowerShell 명령줄 인터페이스는 toocreate 사용 및 hello Microsoft Azure StorSimple 서비스를 관리 하 고 설정 및 모니터링할 수 StorSimple 장치를 제공 합니다. StorSimple 장치를 관리하기 위한 전용 cmdlet을 포함하는 Windows PowerShell 기반의 명령줄 인터페이스입니다. StorSimple용 Windows PowerShell에서 다음을 수행할 수 있는 기능이 있습니다.

* 장치를 등록합니다.
* 장치에서 hello 네트워크 인터페이스를 구성 합니다.
* 특정 형식의 업데이트를 설치합니다.
* Hello 지원 세션에 액세스 하 여 장치 문제를 해결 합니다.
* Hello 장치 상태를 변경 합니다.

직렬 콘솔에서 StorSimple 용 Windows PowerShell을 액세스할 수 있습니다 (호스트에 컴퓨터 직접 연결 된 toohello 장치) 또는 Windows PowerShell 원격을 사용 하 여 원격으로 합니다. 일부 Windows PowerShell 초기 장치 등록 등의 StorSimple 작업에 대 한 hello 직렬 콘솔 에서만 수행할 수는 참고 사항

자세한 내용은 이동 너무[tooadminister StorSimple에 대 한 Windows PowerShell을 사용 하 여 장치](storsimple-8000-windows-powershell-administration.md)합니다.

## <a name="azure-powershell-storsimple-cmdlets"></a>Azure PowerShell StorSimple cmdlet
hello Azure PowerShell StorSimple cmdlet은 서비스 수준 tooautomate hello 명령줄에서 마이그레이션 작업을 수행할 수 있는 Windows PowerShell cmdlet 컬렉션입니다. StorSimple 용 hello Azure PowerShell cmdlet에 대 한 자세한 내용을 보려면 이동 toohello [cmdlet 참조](/powershell/module/azure/?view=azuresmps-3.7.0)합니다.

## <a name="storsimple-snapshot-manager"></a>StorSimple 스냅숏 관리자
StorSimple 스냅숏 관리자 toocreate 일관 되 고 지정 시간 백업 복사본 로컬을 사용할 수 있는 관리 MMC (Microsoft Console) 스냅인은 클라우드 데이터입니다. hello 스냅인-> Windows Server 기반 호스트에서 실행 됩니다. StorSimple 스냅숏 관리자를 사용하여 다음을 수행할 수 있습니다.

* 볼륨을 구성, 백업 및 삭제합니다.
* 볼륨 구성 데이터를 백업 하는 그룹 tooensure는 응용 프로그램 일치 합니다.
* 데이터는 미리 결정 된 일정에 따라 백업 및 (로컬 또는 클라우드 hello에서에서) 지정된 된 위치에 저장 되도록 백업 정책을 관리 합니다.
* 볼륨 및 개별 파일을 복원합니다.

백업 스냅숏 hello 마지막 스냅숏 이후에 변경 된 내용만 hello를 기록 하 고 전체 백업 보다 훨씬 적은 저장소가 필요한는 캡처됩니다. 백업 일정을 만들 수도 있고 필요에 따라 즉시 백업할 수 있습니다. 또한 스냅숏 저장 제어 하는 StorSimple 스냅숏 관리자 tooestablish 보존 정책을 사용할 수 있습니다. 이후에 toorestore 데이터를 백업, StorSimple 스냅숏 관리자 사용 하면 필요한 경우 로컬의 hello 카탈로그 또는 클라우드 스냅숏에서 선택 합니다. 

재해가 발생 한 경우 또는 다른 이유로 toorestore 데이터 유지 해야 하는 경우 StorSimple 스냅숏 관리자 복원 증분 방식으로 필요한 것 처럼 됩니다. 데이터 복원 파일을 복원 하거나 장비를 교체, 작업 tooanother 사이트를 이동 하는 동안 전체 시스템 hello 종료 하면 필요 하지 않습니다.

자세한 내용은 이동 너무[StorSimple 스냅숏 관리자 란?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>SharePoint용 StorSimple 어댑터
Microsoft Azure StorSimple SharePoint에서 투명 하 게 확장 StorSimple 저장소 및 데이터 보호 기능 tooSharePoint 서버 팜을 선택적 구성 요소에 대 한 hello StorSimple 어댑터를 포함 합니다. hello 어댑터가 있습니다 toomove Blob tooa 서버 hello Microsoft Azure StorSimple 시스템에 의해 백업 저장소 RBS (Remote Blob) 공급자 및 hello SQL Server RBS 기능을 사용 하 여 작동 합니다. Microsoft Azure StorSimple 다음 hello BLOB 데이터 저장 로컬 또는 hello 클라우드 사용량에 따라 합니다.

SharePoint 용 StorSimple 어댑터 hello hello SharePoint 중앙 관리 포털 내에서 관리 합니다. 따라서 계속 중앙에서 SharePoint 관리 하 고 모든 저장소 hello SharePoint 팜에서 toobe를 나타납니다.

자세한 내용은 이동 너무[SharePoint 용 StorSimple 어댑터](storsimple-adapter-for-sharepoint.md)합니다. 

## <a name="storage-management-technologies"></a>저장소 관리 기술
또한 toohello 전용 StorSimple 장치, 가상 장치 및 기타 구성 요소, Microsoft Azure StorSimple 소프트웨어 기술 tooprovide 빠른 액세스 toodata 및 tooreduce 저장소 소비량 따르는 hello를 사용 하 여:

* [자동 저장소 계층화](#automatic-storage-tiering) 
* [씬 프로비저닝](#thin-provisioning) 
* [중복 제거 및 압축](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>자동 저장소 계층화
Microsoft Azure StorSimple 현재 사용량, 수명 및 관계 tooother 데이터에 따라 논리적 계층의 데이터를 자동으로 정렬 합니다. 대부분 활성 활성 여백을 제외 하는 동안 로컬에 저장 되 고 비활성 데이터는 자동으로 데이터가 마이그레이션 toohello 클라우드입니다. 다음 다이어그램 hello이 저장소 방법을 보여 줍니다.

![StorSimple 저장소 계층](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

tooenable 빠른 액세스 StorSimple 매우 많은 데이터 (핫 데이터)에 저장 Ssd hello StorSimple 장치에서 합니다. 가끔씩 사용 되는 데이터 저장 (웜 데이터) hdd hello 장치에서 또는 서버 hello 데이터 센터에 있습니다. 비활성 데이터, 백업 데이터를 이동 하 고 데이터 유지에 대 한 보관 또는 준수 purposes toohello 클라우드입니다. 

> [!NOTE]
> 업데이트 2 이상에서는 같이 로컬로 고정 된 볼륨을 지정할 수 있습니다, hello 데이터의 hello 로컬 장치에 유지 되며 되지 않습니다는 쿼리에서 toohello 클라우드 계층입니다. 


StorSimple는 데이터와 저장소 할당을 조정하여 사용량 패턴 변경으로 다시 지정합니다. 예를 들어 일부 정보는 시간이 지남에 따라 덜 활성화될 수 있습니다. 덜 활성화 점진적으로 되면서 Ssd tooHDDs 및 toohello 클라우드가 마이그레이션됩니다. 이 데이터를 다시 시작 되 면 경우 마이그레이션된 백 toohello 저장 장치입니다.

hello 저장소 계층화 프로세스는 다음과 같이 발생합니다.

1. 시스템 관리자가 Microsoft Azure 클라우드 저장소 계정을 설정합니다.
2. 관리자에 게 볼륨 및 데이터 보호 정책을 만드는 hello 직렬 콘솔 및 hello StorSimple 장치 관리자 서비스 (실행 hello에 Azure 포털) tooconfigure hello 장치 및 파일 서버를 사용 합니다. 온-프레미스 컴퓨터 (예: 파일 서버)는 hello Internet Small Computer System Interface (iSCSI) tooaccess hello StorSimple 장치를 사용합니다.
3. 처음에 StorSimple hello 장치의 hello 빠른 SSD 계층에서 데이터를 저장합니다.
4. SSD 계층 접근 방식 용량 hello StorSimple deduplicates hello 가장 오래 된 데이터 블록 압축 및 toohello HDD 계층 이동 시킵니다.
5. HDD 계층 접근 방식 용량 hello로 StorSimple hello 가장 오래 된 데이터 블록을 암호화 하 고 보냅니다 안전 하 게 HTTPS 통해 toohello Microsoft Azure 저장소 계정.
6. Microsoft Azure를 만들고 hello 데이터의 여러 복제본의 데이터 센터에서 원격 데이터 센터에 재해가 발생할 경우 hello 데이터를 복구할 수 있는지 확인 합니다.
7. Hello 파일 서버 hello 클라우드에 저장 된 데이터를 요청 하면 StorSimple 원활 하 게 반환 하 고 hello StorSimple 장치의 hello SSD 계층에서 복사본을 저장 합니다.

#### <a name="how-storsimple-manages-cloud-data"></a>StorSimple에서 클라우드 데이터를 관리하는 방법

StorSimple 모든 hello 스냅숏 및 hello 주 데이터 (호스트에 의해 기록 된 데이터)에서 고객 데이터를 deduplicates 합니다. 중복 제거는 저장소 효율성에 대 한 훌륭한, 그렇게 하면 hello 질문은 "hello 클라우드" 복잡해 집니다. hello 계층화 된 주 데이터 및 hello 스냅숏 데이터 서로 중첩 합니다. 단일 청크 hello 클라우드에서 데이터를 계층화 된 주 데이터 경로로 사용 될 수 및 여러 스냅숏을 참조 합니다. 모든 클라우드 스냅숏이 해당 스냅숏을 삭제 될 때까지 모든 hello 지정 시간 데이터의 복사본 hello 클라우드로 잠겨 있는지 확인 합니다.

데이터 참조 toothat 데이터가 없는 경우에 hello 클라우드에서 삭제 됩니다. 예를 들어 hello StorSimple 장치 이므로 다음 일부 기본 데이터를 삭제 하는 모든 hello 데이터의 클라우드 스냅숏을 가져오는 경우 보면 hello _주 데이터_ 즉시 삭제 합니다. hello _클라우드 데이터_ 계층형된 데이터 hello 및 hello 백업을 포함 하는, 유지 되며 hello 동일 합니다. 여전히 hello 클라우드 데이터를 참조 하는 스냅숏이 때문입니다. Hello 클라우드 후 스냅숏이 삭제 됩니다 (및 참조는 다른 모든 스냅숏이 동일한 데이터 hello) 클라우드 소비 감소 합니다. 클라우드 데이터를 제거하기 전에 스냅숏이 해당 데이터를 계속 참조하지 않는지 확인합니다. 이 프로세스 라고 _가비지 수집_ hello 장치에서 실행 되는 백그라운드 서비스입니다. Hello 가비지 컬렉션 서비스 참조를 검사 다른 toothat 데이터 hello 삭제 하기 전에 클라우드 데이터를 제거 직접 실행 하지 않습니다. 가비지 수집의 hello 속도 hello 스냅숏과 hello 총 데이터의 총 수에 따라 달라 집니다. 일반적으로 hello 클라우드 데이터 주 이내에 정리 됩니다.


### <a name="thin-provisioning"></a>씬 프로비저닝
씬 프로비저닝는 사용 가능한 저장소 tooexceed 물리적 리소스를 표시 되는 가상화 기술입니다. 충분 한 저장소를 미리 예약 하는 대신 StorSimple 데 충분 한 공간이 toomeet 현재 요구 씬 프로 비전 tooallocate을 사용 합니다. 클라우드 저장소의 탄력적인 특징 hello StorSimple 거 나 낮출 수 클라우드 저장소 toomeet 변화 하는 요구 하기 때문에이 방법을 지원 합니다.

> [!NOTE]
> 로컬로 고정된 볼륨은 씬 프로비전되지 않습니다. Hello 볼륨을 만들 때 전체에서 tooa 로컬 전용 볼륨에 할당 된 저장소 프로 비전 됩니다.


### <a name="deduplication-and-compression"></a>중복 제거 및 압축
Microsoft Azure StorSimple은 중복 제거와 압축 toofurther 데이터 저장소 요구 사항을 줄이고 합니다.

중복 제거 감소 hello 전반적인 hello 저장 된 데이터 집합에서 중복을 제거 하 여 저장 된 데이터의 양이 합니다. 정보가 변경 StorSimple hello 변경 되지 않은 데이터를 무시 하 고 캡처에만 변경 내용을 hello 합니다. 또한 StorSimple 식별 하 고 불필요 한 정보를 제거 하 여 hello 저장 된 데이터 양이 줄어듭니다. 

> [!NOTE]
> 로컬로 고정된 볼륨의 데이터는 중복 제거되거나 압축되지 않습니다. 그러나 로컬 고정된 볼륨의 백업은 중복 제거되며 압축됩니다.


## <a name="storsimple-workload-summary"></a>StorSimple 워크로드 요약
지원 hello StorSimple 워크 로드의 요약 정보는 아래 표 형식으로 표시 합니다.

| 시나리오 | 워크로드 | 지원됨 | 제한 | 버전 |
| --- | --- | --- | --- | --- |
| 공동 작업 |파일 공유 |예 | |모든 버전 |
| 공동 작업 |분산 파일 공유 |예 | |모든 버전 |
| 공동 작업 |SharePoint |예* |로컬 고정 볼륨에 대해서만 지원됩니다. |업데이트 2 이상 |
| 보관 |단순 파일 보관 |예 | |모든 버전 |
| 가상화 |가상 컴퓨터 |예* |로컬 고정 볼륨에 대해서만 지원됩니다. |업데이트 2 이상 |
| 데이터베이스 |SQL |예* |로컬 고정 볼륨에 대해서만 지원됩니다. |업데이트 2 이상 |
| 비디오 감시 |비디오 감시 |예* |StorSimple 장치에만 전용된 toothis 작업 경우 지원 |업데이트 2 이상 |
| Backup |기본 대상 백업 |예* |StorSimple 장치에만 전용된 toothis 작업 경우 지원 |업데이트 3 이상 |
| Backup |보조 대상 백업 |예* |StorSimple 장치에만 전용된 toothis 작업 경우 지원 |업데이트 3 이상 |

*예&#42; - 솔루션 지침 및 제한 사항이 적용됩니다.*

작업을 수행 하는 hello StorSimple 8000 시리즈 장치에서 지원 되지 않습니다. StorSimple에 배포하는 경우 이러한 워크로드로 인해 지원되지 않는 구성이 형성됩니다.

* 의료 이미지
* Exchange
* VDI
* Oracle
* SAP
* 빅데이터
* 콘텐츠 배포
* SCSI에서 부팅

다음은 목록 hello StorSimple 지원 인프라 구성 요소입니다.

| 시나리오 | 워크로드 | 지원됨 | 제한 | 버전 |
| --- | --- | --- | --- | --- |
| 일반 |Express 경로 |예 | |모든 버전 |
| 일반 |DataCore FC |예* |DataCore SANsymphony 지원 |모든 버전 |
| 일반 |DFSR |예* |로컬 고정 볼륨에 대해서만 지원됩니다. |모든 버전 |
| 일반 |인덱싱 |예* |계층화된 볼륨의 경우 메타데이터만 인덱싱만 지원됩니다(데이터 없음).<br>로컬 고정 볼륨의 경우 전체 인덱싱이 지원됩니다. |모든 버전 |
| 일반 |바이러스 백신 |예* |계층화된 볼륨의 경우 열기 및 닫기 시 검색만 지원됩니다.<br> 로컬 고정 볼륨의 경우 전체 검색이 지원됩니다. |모든 버전 |

*예&#42; - 솔루션 지침 및 제한 사항이 적용됩니다.*

다음은 StorSimple toobuild 솔루션에 사용 되는 다른 소프트웨어의 목록입니다.

| 워크로드 유형 | StorSimple에서 사용되는 소프트웨어 | 지원되는 버전|링크 toosolution 가이드| 
| --- | --- | --- | --- |
| 백업 대상 |Veeam |Veeam v 9 이상 |[Veaam에서 백업 대상인 StorSimple](storsimple-configure-backup-target-veeam.md)|
| 백업 대상 |Veritas Backup Exec |Backup Exec 16 이상 |[Backup Exec에서 백업 대상으로 StorSimple 구성](storsimple-configure-backup-target-using-backup-exec.md)|
| 백업 대상 |Veritas NetBackup |NetBackup 7.7.x 이상  |[NetBackup에서 백업 대상인 StorSimple](storsimple-configure-backuptarget-netbackup.md)|
| 전역 파일 공유 <br></br> 공동 작업 |Talon  |[Talon을 사용하는 StorSimple](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>StorSimple 용어
Microsoft Azure StorSimple 솔루션을 배포 하기 전에 hello 다음을 검토 하는 권장 용어 및 정의 합니다.

### <a name="key-terms-and-definitions"></a>주요 용어 및 정의
| 용어(머리글자어 또는 약어) | 설명 |
| --- | --- |
| 액세스 제어 레코드(ACR) |Tooit를 연결할 수 있는 호스트를 결정 하는 Microsoft Azure StorSimple 장치에서 볼륨과 연결 된 레코드입니다. hello 결정 hello iSCSI 기반 정규화 된 이름 (IQN) tooyour StorSimple 장치를 연결 하는 hello 호스트 (hello ACR에에서 포함). |
| AES-256 |Tooand hello 클라우드에서 이동할 때 데이터 암호화에 256 비트 암호화 표준 AES (고급) 알고리즘입니다. |
| 할당 단위 크기(AUS) |hello 될 수 있는 디스크 공간의 가장 작은 크기에에서 할당 된 toohold 파일을 Windows 파일 시스템입니다. 추가 공간이 사용 되는 toohold hello 파일 이어야 파일 크기는 hello 클러스터 크기의 짝수 배수가 없으면 (toohello를 hello 클러스터 크기의 다음 배수) 공간이 손실된 되 고 hello 하드 디스크의 조각화 합니다. <br>hello는 hello 중복 제거 알고리즘 효과적으로 작동 하기 때문에 Azure StorSimple 볼륨에 대 한 AUS는 64KB 하는 것이 좋습니다. |
| 자동화된 저장소 계층화 |Ssd tooHDDs tooa 계층이 hello 클라우드와 후 중앙 사용자 인터페이스에서 모든 저장소 관리를 사용 하도록 설정 하 고 저 활성 데이터를 자동으로 이동 합니다. |
| 백업 카탈로그 |백업에 사용 된 hello 응용 프로그램 종류 일반적으로 관련 된 컬렉션입니다. 이 컬렉션은 hello StorSimple 장치 관리자 서비스 UI의 백업 카탈로그 블레이드에서 hello에 표시 됩니다. |
| 백업 카탈로그 파일 |StorSimple 스냅숏 관리자의 데이터베이스 백업 hello에에서 현재 저장 되어 있는 사용 가능한 스냅숏의 목록이 포함 된 파일입니다. |
| 백업 정책 |볼륨, 백업 유형 및 시간표 미리 정의 된 일정에 따라 toocreate 백업을 허용 하는 선택할 수 있습니다. |
| Binary Large Object(BLOB) |데이터베이스 관리 시스템에서 단일 엔터티로 저장되는 이진 데이터 컬렉션입니다. 이진 실행 코드가 BLOB으로 저장되는 경우도 있지만 BLOB은 일반적으로 이미지, 오디오 또는 기타 멀티미디어 개체입니다. |
| Challenge Handshake 인증 프로토콜(CHAP) |프로토콜 사용, 암호 또는 암호를 공유 하는 hello 피어에 따라 연결의 tooauthenticate hello 피어가 아닙니다. CHAP는 단방향 또는 상호일 수 있습니다. 단방향 chap hello 대상은 초기자를 인증 합니다. 상호 CHAP hello 대상을 hello 초기자를 인증 하 고 해당 hello 초기자 인증 hello 대상 필요 합니다. |
| 복제 |볼륨의 중복 복사본입니다. |
| Cloud as a Tier(CaaT) |통합 된 클라우드 저장소 hello 저장소 아키텍처 내에 하나의 계층으로 모든 저장소가 하나의 엔터프라이즈 저장소 네트워크의 toobe 일부 표시 되도록 합니다. |
| 클라우드 서비스 공급자(CSP) |클라우드 컴퓨팅 서비스의 공급자입니다. |
| 클라우드 스냅숏 |Hello 클라우드에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. 클라우드 스냅숏은 같습니다 tooa 스냅숏 다른 오프 사이트 저장소 시스템에 복제 합니다. 클라우드 스냅숏은 특히 재해 복구 상황에서 유용합니다. |
| 클라우드 저장소 암호화 키 |암호 또는 장치 toohello 클라우드 전송한 StorSimple 장치 tooaccess hello 암호화 된 데이터에서 사용 하는 키입니다. |
| 클러스터 인식 업데이트 |Hello 업데이트에는 최소한의 있도록 장애 조치 클러스터의 서버에서 소프트웨어 업데이트를 관리 하거나 서비스 가용성에 영향을 주지 않습니다. |
| 데이터 경로 |상호 연결된 데이터 처리 작업을 수행하는 기능 단위 컬렉션입니다. |
| 비활성화 |나누기 hello hello hello StorSimple 장치 사이 연결 하는 영구적인 작업 관련 클라우드 서비스입니다. Hello 장치의 클라우드 스냅숏은이 프로세스를 초과한 후 상태로 복제 또는 재해 복구에 사용할 수 있습니다. |
| 디스크 미러링 |별도 하드에 논리 디스크 볼륨의 복제가 실시간으로 tooensure 지속적인 가용성에서 구동합니다. |
| 동적 디스크 미러링 |동적 디스크에 논리 디스크 볼륨을 복제합니다. |
| 동적 디스크 |디스크 볼륨 형식 및 사용 하 여 관리자 LDM (논리 디스크) toostore hello 여러 실제 디스크에 걸쳐 데이터를 관리 합니다. 동적 디스크 확대 tooprovide 더 많은 여유 공간 일 수 있습니다. |
| EBOD(Extended Bunch of Disks) 엔클로저 |추가 저장소를 위해 여분의 하드 드라이브 디스크를 포함하는 Microsoft Azure StorSimple 장치의 보조 엔클로저입니다. |
| 팻 프로비저닝 |기존 저장소 프로비저닝 저장소 공간을 할당할에 따라 요구를 예상 (대기 이며 대개 hello 현재 초과). *씬 프로비저닝*도 참조하세요. |
| 하드 디스크 드라이브(HDD) |회전 하는 플래터 toostore 데이터를 사용 하는 드라이브입니다. |
| 하이브리드 클라우드 저장소 |클라우드 저장소를 포함하여 로컬 및 오프사이트 리소스를 사용하는 저장소 아키텍처입니다. |
| Internet Small Computer System Interface(iSCSI) |데이터 저장소 장비 또는 시설을 연결하기 위한 IP(인터넷 프로토콜) 기반 저장소 네트워킹 표준입니다. |
| iSCSI 초기자 |Windows tooconnect tooan 외부 iSCSI 기반 저장소 네트워크를 실행 하는 호스트 컴퓨터 수 있도록 하는 소프트웨어 구성 요소입니다. |
| iSCSI 정규화된 이름(IQN) |ISCSI 대상 또는 초기자를 식별하는 고유 이름입니다. |
| iSCSI 대상 |저장소 영역 네트워크에서 중앙 집중화된 iSCSI 디스크 하위 시스템을 제공하는 소프트웨어 구성 요소입니다. |
| 라이브 보관 |아카이브 데이터의 액세스 가능한 모든 hello 시간 (저장 되지 않습니다 오프 사이트 테이프에서 예를 들어) 저장소 접근 합니다. Microsoft Azure StorSimple은 라이브 보관을 사용합니다. |
| 로컬로 고정된 볼륨 |toohello 클라우드 계층화 된 유형에 볼륨을 hello 장치에 상주 하며 되지 않습니다. |
| 로컬 스냅숏 |Hello Microsoft Azure StorSimple 장치에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. |
| Microsoft Azure StorSimple |데이터 센터 저장소 어플라이언스 및 사용 하는 소프트웨어 구성 된 강력한 솔루션 IT 조직은 tooleverage 클라우드 저장소 데이터 센터 저장소 것 처럼 있습니다. StorSimple은 비용을 절감하는 동시에 데이터 보호 및 데이터 관리를 간소화합니다. hello 솔루션 hello 클라우드와 원활한 통합을 통해 주 저장소, 보관, 백업 및 재해 복구 (DR)를 통합합니다. 엔터프라이즈급 플랫폼에서 SAN 저장소 및 클라우드 데이터 관리를 결합함으로써 StorSimple 장치는 모든 저장소 관련 요구에 대해 속도, 단순성 및 안정성을 가능하게 합니다. |
| 전원 및 냉각 모듈(PCM) |따라서 hello 전원 공급 장치 및 냉각 팬, hello로 구성 된 StorSimple 장치의 하드웨어 구성 요소 이름 전원 및 냉각 모듈을 hello 합니다. hello 장치의 기본 인클로저에 hello 반면 hello EBOD 인클로저의 두 개의 580W Pcm에는 두 개의 764W Pcm에 있습니다. |
| 기본 엔클로저 |Hello 응용 프로그램 플랫폼 컨트롤러가 포함 된 StorSimple 장치의 기본 인클로저. |
| 복구 시간 목표(RTO) |비즈니스 프로세스 또는 시스템 전에 사용 되어야 하는 시간의 hello 최대 크기는 재해 발생 후 완전 하 게 복원 됩니다. |
| Serial Attached SCSI(SAS) |HDD(하드 디스크 드라이브)의 한 유형입니다. |
| 서비스 데이터 암호화 키 |키는 hello StorSimple 장치 관리자 서비스에 등록 하는 사용 가능한 tooany 새 StorSimple 장치를 구성 합니다. hello StorSimple 장치 관리자 서비스와 hello 장치 간에 전송 되는 hello 구성 데이터는 공개 키를 사용 하 여 암호화 및 개인 키를 사용 하 여 hello 장치에 대해서만 해독할 수 있습니다. 서비스 데이터 암호화 키를 hello 서비스 tooobtain 암호 해독을 위해이 개인 키를 수 있습니다. |
| 서비스 등록 키 |추가 관리 작업을 위해 Azure 포털 hello에 표시 되도록 StorSimple 장치 관리자 서비스 hello로 hello StorSimple 장치를 등록 하는 데 도움이 되는 키입니다. |
| Small Computer System Interface(SCSI) |컴퓨터를 물리적으로 연결하고 컴퓨터 간에 데이터를 전달하기 위한 표준 집합입니다. |
| 반도체 드라이브(SSD) |움직이는 부분이 없는 디스크(예: 플래시 드라이브)입니다. |
| 저장소 계정 만들기 |특정된 클라우드 서비스 공급자에 대 한 액세스 자격 증명 집합에 tooyour 저장소 계정 연결 되어 있습니다. |
| SharePoint용 StorSimple 어댑터 |투명 하 게 tooSharePoint 서버 팜 StorSimple 저장소 및 데이터 보호를 확장 하는 Microsoft Azure StorSimple 구성 요소입니다. |
| StorSimple 장치 관리자 서비스 |Azure StorSimple 온-프레미스 및 가상 장치의 확장 toomanage 수 있는 Azure 포털을 hello 합니다. |
| StorSimple 스냅숏 관리자 |Microsoft Azure StorSimple에서 백업 및 복원 작업을 관리하기 위한 MMC(Microsoft Management Console) 스냅인입니다. |
| 백업 수행 |Hello 사용자 tootake 볼륨의 대화형 백업을 허용 하는 기능입니다. 것과 반대로 tootaking 정의 된 정책을 통해 자동화 된 백업을 수동 백업 볼륨의 기능적의 대체 방법입니다. |
| 씬 프로비저닝 |사용 가능한 저장 공간을 저장소 시스템에서 사용 하 여 어떤 hello hello 효율성을 최적화 하는 방법. 씬 프로비저닝에서는 지정된 된 시간에 각 사용자가 필요한 hello 최소 공간에 따라 여러 사용자 간에 hello 저장소가 할당 됩니다. *팻 프로비저닝*도 참조하세요. |
| 계층화 |현재 사용량, 수명 및 관계 tooother 데이터에 따라 논리적 그룹의 데이터를 정렬 합니다. StorSimple은 계층에서 데이터를 자동으로 정렬합니다. |
| 볼륨 |드라이브의 hello 형식으로 표시 되는 논리 저장소 영역입니다. StorSimple 볼륨 hello iSCSI 및 StorSimple 장치 사용을 통해 검색 된 것까지 포함 하 여 hello 호스트가 마운트한 toohello 볼륨에 해당 합니다. |
| 볼륨 컨테이너 |볼륨 및 toothem 적용 되는 hello 설정을 그룹화 합니다. StorSimple 장치의 모든 볼륨은 볼륨 컨테이너로 그룹화됩니다. 볼륨 컨테이너 설정으로는 저장소 계정, 데이터에 대 한 암호화 설정을 toocloud hello 클라우드 관련 작업을 사용 하는 대역폭 및 연결 된 암호화 키를 전송 합니다. |
| 볼륨 그룹 |StorSimple 스냅숏 관리자에서 볼륨 그룹은 구성 된 볼륨 toofacilitate 백업 처리의 컬렉션입니다. |
| 볼륨 섀도 복사본 서비스(VSS) |VSS 인식 응용 프로그램 toocoordinate hello 증분 스냅숏 만들기와 통신 하 여 응용 프로그램 일관성을 쉽게 해 주는 Windows Server 운영 체제 서비스입니다. VSS는 스냅숏이 만들어질 때 hello 응용 프로그램이 일시적으로 비활성 없는지 확인 합니다. |
| StorSimple용 Windows PowerShell |Windows PowerShell 기반의 명령줄 인터페이스 toooperate를 사용 하 고 StorSimple 장치를 관리 합니다. Windows PowerShell의 hello 기본 기능 중 일부를 유지 하면서이 인터페이스는 StorSimple 장치 관리에 맞춰진 추가 전용된 cmdlet에 있습니다. |

## <a name="next-steps"></a>다음 단계
[StorSimple 보안](storsimple-8000-security.md)에 대해 알아봅니다.

