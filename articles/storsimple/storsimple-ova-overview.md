---
title: "aaaMicrosoft Azure StorSimple 가상 배열 개요 | Microsoft Docs"
description: "Hello StorSimple 가상 배열에는 온-프레미스 가상 배열 및 Microsoft Azure 클라우드 저장소 간의 저장소 작업을 관리 하는 통합된 저장소 솔루션에 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>소개 toohello StorSimple 가상 배열
## <a name="overview"></a>개요
Microsoft Azure StorSimple 가상 배열 hello는 하이퍼바이저와 Microsoft Azure 클라우드 저장소에서 실행 되는 온-프레미스 가상 배열 간의 저장소 작업을 관리 하는 통합된 저장소 솔루션입니다. hello 가상 배열 효율적이 고, 비용 효율적인 쉽게 관리 되는 파일 서버 또는 대부분의 hello 문제 및 비용에 따른 엔터프라이즈 저장소 및 데이터 보호와 관련 된 iSCSI 서버 솔루션입니다. hello 가상 배열은 원격 본사/지사 사무실 시나리오에 특히 적합 합니다.

이 항목에서는 hello 가상 배열에 대 한 개요를 제공 하-다음은 다른 리소스:

* 모범 사례에 대해서는 [StorSimple 가상 배열 모범 사례](storsimple-ova-best-practices.md)를 참조하세요.
* 간략하게 hello StorSimple 8000 시리즈 장치에 대 한 이동 너무[StorSimple 8000 시리즈: 하이브리드 클라우드 솔루션이](storsimple-overview.md)합니다. 
* Hello StorSimple 5000/7000 시리즈 장치에 대 한 내용은 이동 너무[StorSimple 온라인 도움말](http://onlinehelp.storsimple.com/)합니다.

hello 가상 배열 hello iSCSI 또는 서버 메시지 블록 (SMB) 프로토콜을 지원합니다. 기존 하이퍼바이저 인프라에서 실행 되며 toohello 클라우드 계층화, 클라우드 백업, 신속 하 게 복원, 항목 수준 복구 및 재해 복구 기능을 제공 합니다.

hello 다음 표에 요약 되어 hello hello StorSimple 가상 배열의 중요 한 기능입니다.

| 기능 | StorSimple 가상 배열 |
| --- | --- |
| 설치 요구 사항 |가상화 인프라(Hyper-V 또는 VMware)  사용 |
| Availability |단일 노드 |
| 총 용량(클라우드 포함) |Too64 TB 가상 배열 당 사용 가능한 용량을 증가 |
| 로컬 용량 |가상 배열 (필요 tooprovision 500GB too8 t B 디스크 공간) 당 390 GB too6.4 TB 사용 가능한 용량 |
| 네이티브 프로토콜 |iSCSI 또는 SMB |
| 복구 시간 목표(RTO) |iSCSI: 크기에 관계없이 2분 미만 |
| 복구 지점 목표(RPO) |매일 백업 및 주문형 백업 |
| 저장소 계층화 |사용 하 여 열 매핑을 toodetermine in 또는 out 어떤 데이터 계층이 해야 |
| 지원 |Hello 공급 업체에서 지 원하는 가상화 인프라 |
| 성능 |기본 인프라에 따라 달라짐 |
| 데이터 이동성 |Toohello 복원할 수 동일한 장치 또는 않는 항목 수준 복구 (파일 서버) |
| 저장소 계층 |로컬 하이퍼바이저 저장소 및 클라우드 |
| 공유 크기 |계층화 된:를 too20 TB; 로컬로 고정: too2 TB를 |
| 볼륨 크기 |계층화 된: 500GB too5 TB; 로컬로 고정: GB too500 50GB |
| 볼륨 크기 |계층화 된:를 too5 TB; 로컬로 고정: too500 GB를 |
| 스냅숏 |충돌 일관성 |
| 항목 수준 복구 |예; 사용자가 공유에서 복원 가능 |

## <a name="why-use-storsimple"></a>StorSimple을 사용하는 이유
StorSimple 분 안에 응용 프로그램 수정 하지 않을 사용자와 서버 tooAzure 저장소를 연결합니다.

hello 다음 표에서 설명 hello 주요 이점 중 일부는 hello StorSimple 가상 배열 솔루션을 제공 합니다.

| 기능 | 혜택 |
| --- | --- |
| 투명한 통합 |hello 가상 배열 hello iSCSI 또는 hello SMB 프로토콜을 지원합니다. hello 로컬 계층과 hello 클라우드 계층 간의 데이터 이동을 hello 원활 하 고 투명 한 toohello 사용자입니다. |
| 저장소 비용 감소 |StorSimple와 핫 데이터에 가장 사용 되는 hello에 대 한 충분 한 로컬 저장소 toomeet 현재 수요 프로 비전합니다. 저장소에 대한 수요가 증가하면, StorSimple은 콜드 데이터를 비용 효과적인 클라우드 저장소로 계층화합니다. hello 데이터는 중복 제거 및 압축 된 toohello 클라우드를 보내기 전에 toofurther 저장소 요구 사항 및 비용을 줄입니다. |
| 단순화된 저장소 관리 |StorSimple 여러 장치 hello 클라우드의 toomanage StorSimple 장치 관리자를 사용 하 여 중앙 집중식된 관리를 제공 합니다. |
| 향상된 재해 복구 및 규정 준수 |StorSimple는 hello 메타 데이터를 즉시 복원 및 필요에 따라 hello 데이터를 복원 하 여 더 빠른 재해 복구를 지원 합니다. 즉, 정상 작업 중단을 최소화하면서 계속할 수 있습니다. |
| 데이터 이동성 |데이터 복구 및 마이그레이션 목적으로 다른 사이트에서 계층 구성된 toohello 클라우드를 액세스할 수 있습니다. Note 데이터만 toohello 원래 가상 배열을 복원할 수 있습니다. 그러나 재해 복구 기능 toorestore hello 전체 가상 배열 tooanother 가상 배열을 사용 합니다. |

## <a name="storsimple-workload-summary"></a>StorSimple 워크로드 요약

지원되는 StorSimple 워크로드가 아래 표에 요약되어 있습니다.

|시나리오     |워크로드     |지원됨      |제한               |
|-------------|-------------|---------------|---------------------------|
|ROBO 공동 작업 |파일 공유     |예      |[파일 서버의 최대 제한](storsimple-ova-limits.md)을 참조하세요.<br></br>[지원되는 SMB 버전에 대한 시스템 요구 사항](storsimple-ova-system-requirements.md).| 모든 버전     |

## <a name="workflows"></a>워크플로
StorSimple 가상 배열 hello은 워크플로 수행 하는 hello에 대 한 특히 적합 합니다.

* [클라우드 기반 저장소 관리](#cloud-based-storage-management)
* [위치와 무관한 백업](#location-independent-backup)
* [데이터 보호 및 재해 복구](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>클라우드 기반 저장소 관리
여러 위치에서 여러 장치에 저장 된 데이터를 Azure 포털 toomanage hello에서 실행 되는 hello StorSimple 장치 관리자 서비스를 사용할 수 있습니다. 이것은 분산된 지점 시나리오에 특히 유용합니다. Note hello StorSimple 장치 관리자 서비스 toomanage 가상 배열 및 물리적 StorSimple 장치의 별도 인스턴스를 만들어야 합니다. 또한 이제 해당 hello 가상 배열 hello Azure 클래식 포털 대신 hello 새 Azure 포털을 사용 note 합니다.

![클라우드 기반 저장소 관리](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>위치와 무관한 백업
Hello 가상 배열을 사용 하 여 클라우드 스냅숏은 볼륨 또는 공유의 위치에 관계 없이, 지정 시간 복사본을 제공합니다. 클라우드 스냅숏은 기본적으로 사용하도록 설정되며 사용하지 않도록 설정할 수 없습니다. 모든 볼륨 및 공유를 백업은 동일한 단일 매일 백업 정책을 통해 시간에 hello 및 필요할 때마다 추가 임시 백업을 수행 하기.

### <a name="data-protection-and-disaster-recovery"></a>데이터 보호 및 재해 복구
hello 가상 배열 hello 다음 데이터 보호 및 재해 복구 시나리오를 지원 합니다.

* **볼륨 또는 공유 복원** – hello restore를 사용 하 여 새 워크플로 toorecover 볼륨으로 또는 공유 합니다. 이 접근 방식 toorecover hello 전체 볼륨 또는 공유를 사용 합니다.
* **항목 수준 복구** – 공유 toorecent 백업을 단순화 된 액세스를 허용 합니다. 특별 한에서 개별 파일을 쉽게 복구할 수 있습니다 *.backup* hello 클라우드에서 사용할 수 있는 폴더입니다. 이러한 복원 기능은 사용자를 기반으로 하며 관리자의 개입이 필요하지 않습니다.
* **재해 복구** – 사용 하 여 hello 장애 조치 기능 toorecover 모든 볼륨 또는 공유가 tooa 새 가상 배열입니다. Hello StorSimple 장치 관리자 서비스에 등록 힙이고 hello 원래 가상 배열 장애 조치할 hello 새 가상 배열을 만듭니다. 새 가상 배열 hello hello를 프로 비전 리소스에서는 다음 사용 합니다. 

## <a name="storsimple-virtual-array-components"></a>StorSimple 가상 배열 구성 요소
hello 가상 배열 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

* [가상 배열](#virtual-array) – 가상화된 환경 또는 하이퍼바이저에 프로비전된 가상 컴퓨터를 기반으로 하는 하이브리드 클라우드 저장 장치입니다.  
* [StorSimple 장치 관리자 서비스](#storsimple-device-manager-service) –는 hello 서로 다른 지리적 위치에서 액세스할 수 있는 단일 웹 인터페이스에서 하나 이상의 StorSimple 장치를 관리할 수 있는 Azure 포털의 확장입니다. StorSimple 장치 관리자 서비스 toocreate hello를 사용 하 여 및 서비스 관리, 볼 하 고 장치 및 경보를 관리 있고 볼륨, 공유 및 기존의 스냅숏은 관리 합니다.
* [로컬 웹 사용자 인터페이스](#local-web-user-interface) -웹 기반 UI를 사용 하는 tooconfigure hello 장치 toohello 로컬 네트워크를 연결할 수 있고 다음 hello StorSimple 장치 관리자 서비스와 hello 장치를 등록 합니다. 
* [명령줄 인터페이스](#command-line-interface) – 지원 세션 toostart hello 가상 배열에 사용할 수 있는 Windows PowerShell 인터페이스입니다.
  hello 다음 섹션에서는 이러한 각 구성이 요소를 더 자세히 설명 하 고 hello 솔루션을 데이터 정렬, 저장소, 할당 및 저장소 관리 및 데이터 보호 방법을 설명 합니다.

### <a name="virtual-array"></a>가상 배열
hello 가상 배열이 주 저장소를 제공, 클라우드 저장소와의 통신을 관리 및 tooensure hello 보안과 hello 장치에 저장 되는 모든 데이터의 기밀성을 사용 하면 단일 노드 저장소 솔루션입니다.

hello 가상 배열이 다운로드에 사용할 수 있는 하나의 모델에서 사용할 수 있습니다. hello 가상 배열 최대 용량은 6.4 TB hello 장치 (8TB의 기본 저장소 요구) 및 64TB 포함 하 여 클라우드 저장소에 있습니다. 

hello 가상 배열 hello 같은 기능에 있습니다.

* 비용 효과적입니다. 기존 가상화 인프라를 활용하며 기존 Hyper-V 또는 VMware 하이퍼바이저에 배포될 수 있습니다.
* Hello 데이터 센터에 상주 하 고는 iSCSI 서버 또는 파일 서버에 구성할 수 있습니다. 
* Hello 클라우드와도 통합 되어 있습니다.
* 백업은 재해 복구를 용이 하 게 하 고 항목 수준의 복구 (ILR)를 간소화할 수 있는 hello 클라우드에 저장 됩니다. 
* 물리적 장치 tooa 적용 것 처럼 업데이트 toohello 가상 배열에 적용할 수 있습니다.

> [!NOTE]
> 가상 배열은 확장할 수 없습니다. 따라서 가상 배열 hello를 만들 때 중요 한 tooprovision 적절 한 저장소는 합니다. 
> 
> 

### <a name="storsimple-device-manager-service"></a>StorSimple 장치 관리자 서비스
웹 기반 사용자 인터페이스를 제공 하는 Microsoft Azure StorSimple hello toocentrally 있습니다 수 있도록 StorSimple 장치 관리자 서비스 StorSimple 저장소를 관리 합니다. 작업을 수행 하는 hello StorSimple 장치 관리자 서비스 tooperform hello를 사용할 수 있습니다.

* 단일 서비스에서 다수의 StorSimple 가상 배열을 관리합니다. 
* StorSimple 가상 배열에 대한 보안 설정을 구성하고 관리합니다. (Hello 클라우드에서 암호화는 Microsoft Azure Api에 의존 합니다.)
* 저장소 계정 자격 증명 및 속성을 구성합니다.
* 볼륨 또는 공유를 구성하고 관리합니다.
* 볼륨 또는 공유의 데이터를 백업하고 복원합니다.
* 성능을 모니터링합니다.
* 시스템 설정을 검토하고 발생 가능한 문제를 식별합니다.

관리 사용 하 여 hello StorSimple 장치 관리자 서비스 tooperform 일별 가상 배열입니다.

자세한 내용은 이동 너무[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-virtual-array-manager-service-administration.md)합니다.

### <a name="local-web-user-interface"></a>로컬 웹 사용자 인터페이스
hello 가상 배열 일회성 구성 및 hello StorSimple 장치 관리자 서비스를 사용 하 여 hello 장치를 등록에 사용 되는 웹 기반 UI를 포함 합니다. 있습니다 수 목록 tooshut 사용할 및 가상 배열 hello를 다시 시작, 진단 테스트를 실행, 소프트웨어 업데이트, hello 장치 관리자 암호를 변경, 시스템 로그를 확인 및 Microsoft 기술 지원 서비스 toofile 서비스 요청에 게 문의 하십시오. 

사용 하는 방법에 대 한 정보에 대 한 웹 기반 UI hello, 너무 이동[사용 하 여 hello 웹 기반 UI tooadminister StorSimple 가상 배열](storsimple-ova-web-ui-admin.md)합니다.

### <a name="command-line-interface"></a>명령줄 인터페이스
hello 포함 된 Windows PowerShell 인터페이스 사용 하면 Microsoft 지원에 대 한 지원 세션 tooinitiate 수 있도록 해 가상 배열에서 발생할 수 있는 문제를 해결 하 고 문제를 해결할 수 있도록 합니다.

## <a name="storage-management-technologies"></a>저장소 관리 기술
또한 toohello 가상 배열 및 기타 구성 요소 hello StorSimple 솔루션에서는 같은 소프트웨어 기술을 tooprovide 빠른 액세스 tooimportant 데이터가 hello, 저장소 소비 감소 및 가상 배열에 저장 된 데이터를 보호 합니다.

* [자동 저장소 계층화](#automatic-storage-tiering) 
* [로컬로 고정된 공유 및 볼륨](#locally-pinned-shares-and-volumes)
* [중복 제거와 압축 데이터에 대 한 계층 또는 toohello 클라우드 백업](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [예약된 백업 및 주문형 백업](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>자동 저장소 계층화
hello 가상 배열은 hello 가상 배열 및 hello 클라우드에 새 계층화 메커니즘 toomanage 저장 된 데이터를 사용합니다. 두 개의 계층: hello 지역 가상 배열 및 Azure 클라우드 저장소입니다. StorSimple 가상 배열 hello를 기반으로 현재 사용량, 수명 및 관계 tooother 데이터를 추적 하는 열 지도 hello 계층으로 데이터를 자동으로 정렬 합니다. 대부분 활성 (최신)는 덜 활성 및 비활성 데이터는 자동으로 로컬에 저장 되는 데이터가 마이그레이션 toohello 클라우드입니다. (모든 백업은 클라우드 hello에에서 저장 됩니다.) StorSimple는 데이터와 저장소 할당을 조정하여 사용량 패턴 변경으로 다시 지정합니다. 예를 들어 일부 정보는 시간이 지남에 따라 덜 활성화될 수 있습니다. 점진적으로 빈도가 되면서 아웃 toohello 클라우드 계층화 된 됩니다. 이 데이터를 다시 시작 되 면 toohello 저장소 배열에 계층화 된 됩니다.

계층화된 특정 공유 또는 볼륨에 대한 데이터는 자체 로컬 계층 공간이 보장됩니다. (약 10%의 hello 총 해당 공유 또는 볼륨에 대 한 프로 비전 된 공간)입니다. 이렇게 하면 해당 공유 또는 볼륨에 대 한 hello 가상 배열에 사용 가능한 저장소 hello 줄일 수, 하는 동안 하나의 공유 또는 볼륨에 대 한 계층은 영향을 받지 다른 공유 또는 볼륨의 hello 계층화 요구 사항에 의해 확인 합니다. 따라서 하나의 공유 또는 볼륨에 매우 늘어나면 작업에는 다른 모든 작업 toohello 클라우드를 강제할 수 없습니다. 

![자동 저장소 계층화](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> 로컬과 고정 된 볼륨을 지정할 수 있습니다,이 경우 hello 데이터 hello 가상 배열에 남아 있으며 toohello 클라우드 계층입니다. 자세한 내용은 이동 너무[공유 및 볼륨 로컬로 고정](#locally-pinned-shares-and-volumes)합니다.
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>로컬로 고정된 공유 및 볼륨
적절한 공유 및 볼륨을 로컬로 고정되도록 만들 수 있습니다. 이 기능 하면 중요 한 응용 프로그램에 필요한 데이터가 hello 가상 배열에 남아 있고은 toohello 클라우드 계층입니다. 로컬로 고정 된 공유 및 볼륨 hello 같은 기능을 가집니다. 

* 주체 toocloud 대기 시간 또는 연결 문제 않습니다.
* StorSimple 클라우드 백업 및 재해 복구 기능의 이점이 여전히 존재합니다.

로컬로 고정된 공유 또는 볼륨을 로컬로 고정된 것처럼 계층화된 공유 또는 볼륨으로 복원할 수 있습니다. 

로컬 고정된 볼륨에 대 한 자세한 내용은 이동 너무[hello StorSimple 장치 관리자 서비스 toomanage 볼륨을 사용 하 여](storsimple-virtual-array-manage-volumes.md)합니다.

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>중복 제거와 압축 데이터에 대 한 계층 또는 toohello 클라우드 백업
StorSimple 사용 하 여 중복 제거 및 데이터 압축 toofurther hello 클라우드에서 저장소 요구 사항을 줄입니다. 중복 제거 감소 hello 전반적인 hello 저장 된 데이터 집합에서 중복을 제거 하 여 저장 된 데이터의 양이 합니다. 정보가 변경 StorSimple hello 변경 되지 않은 데이터를 무시 하 고 캡처에만 변경 내용을 hello 합니다. 또한 StorSimple 식별 하 고 중복 된 정보를 제거 하 여 hello 저장 된 데이터 양이 줄어듭니다. 

> [!NOTE]
> Hello 가상 배열에 저장 된 데이터 중복 제거 하지 않거나, 압축 하십시오. 모든 중복 제거 및 압축 hello 데이터가 toohello 클라우드 보내집니다 직전에 발생 합니다.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>예약된 백업 및 주문형 백업
StorSimple 데이터 보호 기능을 사용 하면 toocreate 요청 시 백업을 있습니다. 또한, 기본 백업 일정은 매일 데이터가 백업되도록 보장합니다. 백업은은 hello 클라우드에 저장 되는 증분 스냅숏의 hello 형태로 수행 됩니다. Hello 마지막 백업 이후의 hello 변경 내용만 기록, 스냅숏 생성 하 고 신속 하 게 복원할 수 있습니다. (예: 테이프 백업) 보조 저장소 시스템을 바꾸고 필요한 경우 toorestore 데이터 tooyour 데이터 센터 또는 tooalternate 사이트를 허용 하기 때문에 이러한 스냅숏을 재해 복구 시나리오에서 매우 중요할 수 있습니다.

## <a name="next-steps"></a>다음 단계
너무 방법에 대해 알아봅니다[hello 가상 배열 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md)합니다.

