---
title: "aaaStorSimple 8000 시리즈 업데이트 2.2 릴리스 정보 | Microsoft Docs"
description: "StorSimple 8000 시리즈 업데이트 2.2에 대 한 hello 새로운 기능, 문제 및 해결 방법에 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>StorSimple 8000 시리즈 업데이트 2.2 릴리스 정보
## <a name="overview"></a>개요
hello 다음 릴리스 정보 hello 새로운 기능에 설명 하 고 StorSimple 8000 시리즈 업데이트 2.2에 대 한 hello 중요 한 미해결 문제를 식별 합니다. 또한이 릴리스에 포함 된 hello StorSimple 소프트웨어 업데이트의 목록을 포함 합니다. 

2.2 업데이트 적용된 tooany StorSimple 장치 업데이트 2.1을 통해 릴리스 (GA) 또는 업데이트 0.1 실행 수 있습니다. hello 장치 업데이트 2.2와 관련 된 버전이 6.3.9600.17708 합니다.

Hello 릴리스 노트 hello를 배포 하기 전에 StorSimple 솔루션의 업데이트에 포함 된 hello 정보를 검토 하십시오.

> [!IMPORTANT]
> * 업데이트 2.2에는 소프트웨어 전용 업데이트가 포함되어 있습니다. 이 업데이트 약 1.5 ~ 2 시간 tooinstall이 필요합니다. 
> * 업데이트 2.1을 실행하는 경우, 가능한 한 빨리 업데이트 2.2를 적용하는 것이 좋습니다.
> * 새 릴리스를 위한 나타나지 않을 수 있습니다 업데이트 hello 업데이트의 단계별된 공개를 수행 하는 것 때문에 즉시 합니다. 업데이트가 곧 제공될 예정이니 몇 일 후에 업데이트를 다시 검색하세요.
> 
> 

## <a name="whats-new-in-update-22"></a>업데이트 2.2의 새로운 기능
hello 다음 주요 향상 기능이 적용 된 업데이트 2.2에 있습니다.

* **공간 확보 최적화 자동화 된** – 씬 프로 비전 된 볼륨에서 데이터가 삭제 되는 경우 hello 사용 하지 않는 저장소 블록은 있어야 toobe 회수 합니다. 이 릴리스에 고 사용 가능한 더 빠르게 같이 비교 toohello 이전 버전 공간 hello 클라우드에서 사용 하지 않는 hello에 향상 된 hello 공간 회수 프로세스입니다.
* **향상 된 성능을 스냅숏** – 업데이트 2.2 향상 된 hello 시간 tooprocess 클라우드 스냅숏이 포함 큰 볼륨을 사용 하는 고 최소한의 toono 데이터 변동을 특정 시나리오에서 합니다. 이 향상 된이 기능을 활용할 수 있는 시나리오는 hello 보관 볼륨 것입니다.
* **지원 패키지 수집 강화** – hello 지원 패키지 수집 되 고이 릴리스에서 업로드 hello 방식으로 개선 되었습니다. 
* **업데이트 안정성 향상** - 이 릴리스에는 업데이트 안정성을 향상하는 버그 수정이 포함되어 있습니다.

## <a name="issues-fixed-in-update-22"></a>업데이트 2.2에서 해결된 문제
다음 표에서 hello 2.1 및 2.2 업데이트에서 해결 된 문제에 대 한 요약을 제공 합니다.    

| 아니요 | 기능 | 문제 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- |
| 1 |호스트 성능 |Hello에 이전 해제, 호스트 쪽 성능 문제 hello 로컬 고정된 볼륨 생성 중에 관찰 된 고정 된 볼륨을 계층화 된 볼륨 tooa 로컬로의 hello 변환 하는 동안 합니다. 그 결과로 hello 볼륨 만들기 및 변환 절차 중 hello 호스트 성능 향상이 릴리스에서 이러한 문제가 해결 되었습니다. |예 |아니요 |
| 2 |로컬로 고정된 볼륨 |경우에 따라에서 hello 시스템 로컬로 고정 된 볼륨을 만들 때 충돌 합니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 3 |계층화 |Hello 메타 데이터 (8010 및 8020) StorSimple 클라우드 어플라이언스에 hello 계층에 대 한 클라우드 hello 너무 자주 끊기면 충돌 했습니다. 이 문제는 이 릴리스에서 해결되었습니다. |아니요 |예 |
| 4 |스냅숏 만들기 |큰 볼륨 및 데이터 변동의 최소 toono 있는 경우에 증분 스냅숏 관련된 toohello 만들기 문제가 있었습니다. 이러한 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 5 |Openstack 인증 |Openstack hello 클라우드 서비스 공급자를 사용할 때으로 드문 경우 버그 관련된 toohello 인증 hello 사용자 실행 됩니다 충돌에서 hello JSON 파서 결과입니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 6 |호스트 쪽 복사 |이전 버전의 소프트웨어 드문 경우 버그를 하나의 볼륨 tooanother 볼륨에서 hello 데이터를 복사할 때 toohello ODX 타이밍 였던 관련 있습니다. 이 컨트롤러 장애 조치 발생 하 고 hello 시스템 복구 모드로 전환 될 수 없습니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 7 |WMI(Windows Management Instrumentation) |이전 버전의 소프트웨어 hello 여러 개 hello 예외를 사용 하 여 웹 프록시 오류 않았습니다 "<ManagementException> 공급자를 로드 하지 못했습니다". 이 버그 특성 사용된 tooa WMI 메모리 누수가 발생 였으며 고정 됩니다. |예 |아니요 |
| 8 |업데이트 |이전 버전의 소프트웨어를 hello에 특정 경우에 따라에서 hello 사용자 tooscan 또는 설치 업데이트를 시도할 때 "CisPowershellHcsscripterror"를 받았습니다. 이 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 9 |지원 패키지 |이 릴리스에서 있었는지 개선 toohello 방식으로 hello 지원 패키지 수집 되 고 업로드 합니다. |예 |예 |

## <a name="known-issues-in-update-22"></a>업데이트 2.2의 알려진 문제
다음 표에서 hello이이 릴리스의 알려진된 문제에에서 대 한 요약을 제공 합니다.

| 아니요. | 기능 | 문제 | 주석/해결 방법 | Toophysical 장치를 적용 됩니다. | Toovirtual 장치를 적용 됩니다. |
| --- | --- | --- | --- | --- | --- |
| 1 |디스크 쿼럼 |경우에 따라에서 hello 대부분의 디스크 8600 장치의 EBOD 인클로저에 hello 끊어져서 디스크 쿼럼이 없게 하는 경우 다음 hello 저장소 풀은 오프 라인 상태가 됩니다. Hello 디스크가 다시 연결 하는 경우에 오프 라인으로 유지 됩니다. |Tooreboot hello 장치가 필요 합니다. Hello 문제가 지속 되 면 Microsoft 지원에 다음 단계에 문의 하세요. |예 |아니요 |
| 2 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 하는 동안 hello 이미지 hello 피어 노드에서 로드 되 면 hello 컨트롤러 ID 수 처음으로 나타나도록 hello 피어 컨트롤러의 id입니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |별도의 작업이 필요하지 않습니다. 이 경우 hello 컨트롤러 교체를 완료 한 후 자체적으로 해결 됩니다. |예 |아니요 |
| 3 |저장소 계정 |Hello 저장소 서비스 toodelete hello 저장소 계정을 사용 하는 지원 되지 않는 시나리오입니다. 이렇게 하면 tooa 상황 사용자 데이터를 검색할 수 없습니다. | |예 |예 |
| 4 |장치 장애 조치 |다중에서 동일한 원본 장치 toodifferent 대상 장치는 지원 되지 않습니다 hello는 볼륨 컨테이터의 장애 조치 합니다. 단일 데드 장치 toomultiple 장치에서 장애 조치에는 먼저 장애 장치 조치 hello 장치의 hello 볼륨 컨테이너가 데이터 소유권을 잃게 생성 됩니다. 이러한 장애 조치 후 이러한 볼륨 컨테이너 나타나거나 hello Azure 클래식 포털에서에서 볼 때 다르게 동작 합니다. | |예 |아니요 |
| 5 |설치 |SharePoint 용 StorSimple 어댑터를 하는 동안 필요한 tooprovide hello 설치 toofinish 위해에서 장치 IP 성공적으로 합니다. | |예 |아니요 |
| 6 |웹 프록시 |웹 프록시 구성에 있으면 hello로는 HTTPS 프로토콜을 지정 다음 장치를 서비스 통신 영향을 받고 hello 장치는 오프 라인 상태가 유지 됩니다. 지원 패키지도 장치에서 많은 리소스를 소모 hello 프로세스에서 생성 됩니다. |지정한 프로토콜이 hello으로 hello 웹 프록시 URL에 HTTP 있는지 확인 합니다. 자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](storsimple-configure-web-proxy.md)합니다. |예 |아니요 |
| 7 |웹 프록시 |구성 하 고 등록된 된 장치에서 웹 프록시를 사용 하는 경우 장치에서 toorestart hello 활성 컨트롤러가 필요 합니다. | |예 |아니요 |
| 8 |긴 클라우드 대기 시간 및 많은 I/O 작업 |StorSimple 장치 매우 긴 클라우드 대기 시간 (초) 및 높은 수준의 I/O 작업의 조합을 발견 하면 hello 장치 볼륨 상태가 저하 및 hello I/o "장치가 준비 되지 않음" 오류가 발생할 수 있습니다. |Toomanually 재부팅 hello 장치 컨트롤러 필요 하거나이 상황에서 장치 장애 조치 toorecover를 수행 합니다. |예 |아니요 |
| 9 |Azure PowerShell |Hello StorSimple cmdlet을 사용 하는 경우 **Get AzureStorSimpleStorageAccountCredential &#124; Select-object-처음 1-대기** tooselect 새를 만들 수 있도록 첫 번째 개체를 hello **VolumeContainer** 개체 hello cmdlet 모든 hello 개체를 반환 합니다. |다음과 같이 괄호로 hello cmdlet wrap: **(Get Azure StorSimpleStorageAccountCredential) &#124; Select-object-처음 1-대기** |예 |예 |
| 10 |마이그레이션 |여러 볼륨 컨테이너는 마이그레이션에 대 한 전달 되는 경우 최신 백업 에타 hello는 hello 첫 번째 볼륨 컨테이너에 대 한 정확한 합니다. 또한 병렬 마이그레이션 hello hello 첫 번째 볼륨 컨테이너에서 처음 4 백업이 마이그레이션된 후 시작 됩니다. |한번에 하나의 볼륨 컨테이너를 마이그레이션하는 것이 좋습니다. |예 |아니요 |
| 11 |마이그레이션 |Hello 복원 후 볼륨 toohello 백업 정책 또는 hello 가상 디스크 그룹을 추가 되지 않습니다. |Tooadd 이러한 볼륨 tooa 백업 정책 순서 toocreate 백업에 필요 합니다. |예 |예 |
| 12 |마이그레이션 |Hello 5000/7000 시리즈 장치 액세스 하지 않아야 hello 마이그레이션이 완료 되 면 hello 마이그레이션된 데이터 컨테이너입니다. |Hello를 삭제 하는 것이 좋습니다 hello 마이그레이션이 완료 되 고 커밋된 후 데이터 컨테이너를 마이그레이션됩니다. |예 |아니요 |
| 13 |복제 및 DR |업데이트 1을 실행 하는 StorSimple 장치 복제 하거나 재해 복구 tooa 장치 전 업데이트 1 소프트웨어 실행을 수행할 수 없습니다. |이러한 작업 tooupdate hello 대상 장치 tooUpdate 1 tooallow 필요 합니다. |예 |예 |
| 14 |마이그레이션 |볼륨 그룹과 연결된 볼륨이 없으면 마이그레이션에 대한 구성 백업은 5000-7000 시리즈 장치에서 실패할 수 있습니다. |연결 된 볼륨이 없으면 인 모든 hello 빈 볼륨 그룹을 삭제 하 고 hello 구성 백업을 다시 시도 하십시오. |예 |아니요 |
| 15 |Azure PowerShell cmdlet 및 로컬에 고정된 볼륨 |Azure PowerShell cmdlet을 통해 로컬에 고정된 볼륨을 만들 수 없습니다. (Azure PowerShell을 통해 만드는 모든 볼륨은 계층화됩니다.) |항상 hello StorSimple 관리자 서비스 tooconfigure 로컬로 고정 된 볼륨을 사용 합니다. |예 |아니요 |
| 16 |로컬에 고정된 볼륨에 사용 가능한 공간 |로컬로 고정 된 볼륨을 삭제 하면 hello 공간 새 볼륨에 사용할 수 있는 즉시 업데이트 되지 않을 수 있습니다. hello StorSimple 관리자 서비스에 업데이트 사용 가능한 로컬 공간을 약 1 시간 마다 hello 합니다. |Toocreate hello 새 볼륨을 시도 하기 전에 한 시간까지 기다립니다. |예 |아니요 |
| 17 |로컬로 고정된 볼륨 |복원 작업을 hello 임시 스냅숏 백업이 백업 카탈로그 hello 있지만 hello 복원 작업의 hello 기간에만 표시합니다. 또한 접두사가 포함 된 가상 디스크 그룹을 노출 **tmpCollection** hello에 **백업 정책** 페이지, 있지만 hello hello 기간에 대 한 복원 작업입니다. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 계층화 된 볼륨에만 있는 hello 복원 작업의 경우,이 문제가 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 18 |로컬로 고정된 볼륨 |복원 작업을 취소 하 고 hello 복원 작업이 표시 됩니다는 그 후에 즉시 컨트롤러 장애 조치가 발생 하는 경우 **실패** 대신 **Canceled**합니다. 복원 작업이 실패 하 고 hello 복원 작업이 표시 됩니다는 그 후에 즉시 컨트롤러 장애 조치가 발생 하는 경우 **Canceled** 대신 **실패**합니다. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 계층화 된 볼륨에만 있는 hello 복원 작업의 경우,이 문제가 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 19 |로컬로 고정된 볼륨 |복원 작업을 취소 하거나 복원 실패 하 고 컨트롤러 장애 조치가 발생 한 다음, 하는 경우 추가 복원 작업 hello에 나타납니다 경우 **작업** 페이지. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 계층화 된 볼륨에만 있는 hello 복원 작업의 경우,이 문제가 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 20 |로컬로 고정된 볼륨 |Tooconvert 계층화 된 볼륨 (생성 및 업데이트를 통한 복제 또는 이전)를 시도 하면 tooa 로컬 고정 볼륨 공간이 부족 합니다. 장치에서 실행 중인 또는 클라우드 가동이 중지 힙이고 hello clone(s) 손상 될 수 있습니다. |이 문제는 업데이트 2.1 이전 소프트웨어로 만들어지고 복제된 볼륨을 사용하는 경우에만 발생합니다. 자주 발생하지 않는 시나리오여야 합니다. | | |
| 21 |볼륨 변환 |볼륨 변환 진행 중인 동안 hello Acr tooa 연결 된 볼륨을 업데이트 하지 않으면 (계층화 된 toolocally 고정 또는 그 반대로). Hello Acr를 업데이트 합니다. 데이터가 손상 될 수 있습니다. |필요한 경우 업데이트 hello Acr 이전 toohello 볼륨으로의 변환 고 없도록 더 이상 ACR 업데이트 hello 변환이 진행 중인 동안 합니다. | | |

## <a name="controller-and-firmware-updates-in-update-22"></a>업데이트 2.2의 컨트롤러 및 펌웨어 업데이트
이 릴리스에는 소프트웨어 전용 업데이트가 포함되어 있습니다. 그러나 버전 이전 tooUpdate 2에서에서 업데이트 하는 경우 tooinstall 드라이버를 Storport, Spaceport, 해야 합니다 (경우에 따라) 하 고 디스크 장치에 펌웨어 업데이트 합니다.

Tooinstall hello 드라이버, Storport, Spaceport, 및 디스크 펌웨어 업데이트를 참조 하는 방법에 대 한 자세한 내용은 [업데이트 2.2를 설치](storsimple-install-update-21.md) StorSimple 장치에 있습니다.

## <a name="virtual-device-updates-in-update-22"></a>업데이트 2.2의 가상 장치 업데이트
이 업데이트는 적용 된 toohello 가상 장치 수 없습니다. 새 가상 장치 생성 toobe가 필요 합니다. 

## <a name="next-step"></a>다음 단계
너무 방법에 대해 알아봅니다[업데이트 2.2를 설치](storsimple-install-update-21.md) StorSimple 장치에 있습니다.

