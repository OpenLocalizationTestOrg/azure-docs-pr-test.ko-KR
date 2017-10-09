---
title: "StorSimple 가상 배열에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Hello 배포 및 관리 hello StorSimple 가상 배열에 대 한 모범 사례를 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>StorSimple 가상 배열 모범 사례
## <a name="overview"></a>개요
Microsoft Azure StorSimple 가상 배열은 하이퍼바이저 및 Microsoft Azure 클라우드 저장소에서 실행되는 온-프레미스 가상 장치 간의 저장소 작업을 관리하는 통합 저장소 솔루션입니다. StorSimple 가상 배열 효율적이 고 비용 효율적인 대체 toohello 8000 시리즈 실제 배열입니다. hello 가상 배열 기존 하이퍼바이저 인프라에서 실행할 수 있습니다, hello iSCSI 및 hello SMB 프로토콜을 모두 지원 및 원격 본사/지사 시나리오에 적합 합니다. 너무 hello StorSimple 솔루션에 자세한 내용을 보려면 이동[Microsoft Azure StorSimple 개요](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx)합니다.

이 문서에서는 hello 초기 설정, 배포 및 관리의 hello StorSimple 가상 배열 하는 동안 구현 hello 모범 사례를 설명 합니다. 이들 모범 사례는 hello 설정 및 관리 가상 배열에 대 한 유효성이 검사 된 지침을 제공합니다. 이 문서는 위한으로 hello IT 관리자에 게 배포 및 관리 hello 데이터 센터의 가상 배열입니다.

모범 사례 toohelp hello에 대 한 정기적인 검토 toohello 설정 및 작업 흐름 변경 내용이 있을 때 장치가 규정 준수에 여전히 있는지 확인 하는 것이 좋습니다. 가상 배열에 이러한 모범 사례를 구현하는 동안 문제가 발생할 경우 [Microsoft 지원에 문의](storsimple-virtual-array-log-support-ticket.md) 하시기 바랍니다.

## <a name="configuration-best-practices"></a>구성 모범 사례
이들 모범 사례는 hello 가상 배열의 hello 초기 설치 및 배포 하는 동안 다음 toobe 해야 하는 hello 지침을 다룹니다. 이들 모범 사례에는 해당 관련된 toohello 네트워킹, 저장소 계정을 구성 하 고 공유를 만드는 hello 설정 hello 가상 컴퓨터, 그룹 정책 설정, 크기 조정, 프로 비전 하 고 볼륨에 대 한 hello 가상 배열 포함 됩니다. 

### <a name="provisioning"></a>프로비전
StorSimple 가상 배열 (Hyper-v 또는 VMware) hello 하이퍼바이저에서 사용자를 프로 비전 하는 가상 컴퓨터 (VM)를 호스트 서버입니다. Hello 가상 컴퓨터를 프로 비전 할 때에 호스트 수 toodedicate 충분 한 리소스 인지 확인 합니다. 자세한 내용은 이동 너무[최소 리소스 요구 사항](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision 배열입니다.

가상 배열 hello를 프로 비전 할 때 모범 사례를 따르는 hello를 구현 합니다.

|  | Hyper-V | VMware |
| --- | --- | --- |
| **가상 컴퓨터 유형** |**2세대** 이미지와 함께 사용할 *2세대* VM. <br></br> **1세대** 이미지와 함께 사용할 *1세대* VM. |*.vmdk* 이미지를 사용할 경우에는 가상 컴퓨터 버전 8 - 11을 사용합니다. |
| **메모리 유형** |**정적 메모리**로 구성합니다. <br></br> Hello를 사용 하지 마십시오 **동적 메모리** 옵션입니다. | |
| **데이터 디스크 유형** |**동적 확장**으로 프로비전합니다.<br></br> **고정 크기** 는 시간이 오래 걸립니다. <br></br> Hello를 사용 하지 마십시오 **차이점 보관용** 옵션입니다. |사용 하 여 hello **씬 프로 비전** 옵션입니다. |
| **데이터 디스크 수정** |확장 또는 축소는 허용되지 않습니다. 시도 toodo hello 장치에서 모든 hello 로컬 데이터 손실을 발생 합니다. |확장 또는 축소는 허용되지 않습니다. 시도 toodo hello 장치에서 모든 hello 로컬 데이터 손실을 발생 합니다. |

### <a name="sizing"></a>크기 조정
StorSimple 가상 배열 크기를 조정할 때 hello 다음 요인을 고려 합니다.

* 볼륨 또는 공유에 사용할 로컬 예약. Hello 공간의 약 %12 각 프로 비전 된 계층화 된 볼륨 또는 공유에 대 한 hello 로컬 계층에서 예약 됩니다. 대략 hello 공간이 10% 남았을 파일 시스템에 대 한 로컬 고정된 볼륨에 대 한 예약 됩니다.
* 스냅숏 오버헤드. 약 15% 공간 hello 로컬 계층에서 스냅숏을 예약 되어 있습니다.
* 복원이 필요합니다. 새 작업으로 복원을 수행 하, 크기 조정 복원에 필요한 hello 공간을 고려해 야 합니다. Tooa 공유 또는 볼륨의 hello 복원이 완료 된 크기가 동일 합니다.
* 예기치 않은 증가를 대비하여 버퍼를 약간 할당해야 합니다.

Hello 요소 앞에 따라, 용량 요구 사항을 hello 수식은 다음 hello로 나타낼 수 있습니다.

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

hello 다음 예제는 설명 수 크기를 정하는 것 요구 사항을 기반으로 하는 가상 배열입니다.

#### <a name="example-1"></a>예제 1:
가상 배열에서 원하는 toobe 수

* 2TB 계층화 볼륨 또는 공유 프로비전.
* 1TB 계층화 볼륨 또는 공유 프로비전.
* 로컬로 고정된 300GB 볼륨 또는 공유 프로비전.

Hello에 대 한 이전 볼륨 또는 공유에 응 hello hello 로컬 계층에 필요한 공간을 계산 합니다.

먼저, 각 계층화 된 볼륨/공유에 대 한 로컬 예약 hello 볼륨/공유 크기의 같은 too12% 것입니다. 로컬로 고정 hello 볼륨/공유에 대 한 로컬 예약은 10%의 hello 로컬 고정 볼륨/공유 크기 (또한 toohello 비전 크기)입니다. 이 예제에는 다음 사항이 필요합니다.

* 240GB 로컬 예약(2TB 계층화 볼륨/공유의 경우)
* 120GB 로컬 예약(1TB 계층화 볼륨/공유의 경우)
* 로컬로 고정 된 볼륨 또는 공유 (추가 로컬 예약 toohello 300GB 프로 비전 된 크기의 10%)에 대 한 330 GB

hello 지금까지 hello 로컬 계층에서 필요한 전체 공간은: 240 GB + 120GB + 330 = 690 g B입니다.

둘째, hello 로컬 계층의 공간 크기 이상으로 hello 가장 큰 단일 예약 해야합니다. 이 추가 금액 클라우드 스냅숏에서 toorestore 필요한 경우에 사용 됩니다. 이 예에서 hello 가장 큰 로컬 예약 330 GB (파일 시스템에 대 한 예약이 포함)는 해당 toohello 추가 되므로 690 GB: 690 GB + 330 GB = 1020 GB입니다.
후속 추가 복원이 수행 했습니다 hello 이전 복원 작업에서 hello 공간을 확보할 항상 수 있습니다 했습니다.

총 로컬의 15% 필요 셋째, 간격을 지금까지 toostore 로컬 스냅숏의 85%를 사용할 수 있도록 합니다. 이 예에서는 약 1020GB = 0.85&ast;프로비전된 데이터 디스크(TB)입니다. 따라서 hello 프로 비전 된 데이터 디스크는 것 (1020&ast;(1/0.85)) = 1200 GB = 1.20 TB ~ 1.25 TB (toonearest 사분 위 수 반올림 함)

예기치 않은 증가 및 새로운 복원 작업을 대비하여 약 1.25-1.5TB의 로컬 디스크를 프로비전해야 합니다.

> [!NOTE]
> Hello 로컬 디스크는 씬 프로 비전 하는 것이 좋습니다. 이 권장 사항은 되므로 hello 복원 공간은 5 일 보다 오래 된 toorestore 데이터에 필요 합니다. 항목 수준 복구에서는 있습니다 toorestore 데이터 hello에 대 한 마지막 5 일 필요 없이 복원 위한 추가 공간이 hello 합니다.


#### <a name="example-2"></a>예 2:
가상 배열에서 원하는 toobe 수

* 2TB 계층화 볼륨 프로비전
* 로컬로 고정된 300GB 볼륨 프로비전

계층화 볼륨/공유에 필요한 로컬 공간 예약의 12% 및 로컬로 고정된 볼륨/공유의 10%를 기반으로 필요한 공간을 계산해 보면 다음과 같습니다.

* 240GB 로컬 예약(2TB 계층화 볼륨/공유의 경우)
* 로컬로 고정 된 볼륨 또는 공유 (추가 로컬 예약 toohello 프로 비전 300GB 공간의 10%)에 대 한 330 GB

Hello 로컬 계층에 필요한 총 공간은: 240 GB + 330 = 570 g B

hello 최소 로컬 복원에 필요한 공간은 330 GB입니다.

총 디스크의 15%만 0.85를 사용할 수 있도록 사용 되는 toostore 스냅숏을 합니다. 따라서는 hello 디스크 크기 (900&ast;(1/0.85)) = 1.06 TB ~ 1.25 TB (toonearest 사분 위 수 반올림 함)

예기치 않은 증가를 고려하여 1.25-1.5TB 로컬 디스크를 프로비전할 수 있습니다.

### <a name="group-policy"></a>그룹 정책
그룹 정책은 사용자 및 컴퓨터에 대 한 특정 구성을 tooimplement을 수 있는 인프라입니다. 그룹 정책 설정은 연결 된 toohello는 그룹 정책 개체 (Gpo)에 포함 된 Active Directory 도메인 서비스 (AD DS) 컨테이너를 다음: 사이트, 도메인 또는 조직 구성 단위 (Ou). 

가상 배열 도메인에 가입 된 경우 Gpo에 적용 된 tooit 될 수 있습니다. 이러한 Gpo는 hello StorSimple 가상 배열의 hello 작동에 부정적인 영향을 줄 수 있는 바이러스 백신 소프트웨어 등의 응용 프로그램을 설치할 수 있습니다.

따라서 다음 작업을 수행하는 것이 좋습니다.

* 가상 배열이 Active Directory용 자체 OU(조직 구성 단위)에 있는지 확인합니다.
* 그룹 정책 개체 (Gpo)에 없는 적용된 tooyour 가상 배열 인지 확인 합니다. 상속을 차단할 수 있습니다 (자식 노드)의 가상 배열 hello tooensure Gpo hello 부모에서 자동으로 상속 되지 않습니다. 자세한 내용은 이동 너무[상속을 차단](https://technet.microsoft.com/library/cc731076.aspx)합니다.

### <a name="networking"></a>네트워킹
가상 배열에 대 한 네트워크 구성은 hello hello 로컬 웹 UI 통해 수행 됩니다. 가상 네트워크 인터페이스는 hello 가상 배열 프로 비전 된 hello 하이퍼바이저를 통해 사용 됩니다. 사용 하 여 hello [네트워크 설정을](storsimple-virtual-array-deploy3-fs-setup.md) tooconfigure hello 가상 네트워크 인터페이스 IP 주소, 서브넷 및 게이트웨이 페이지입니다.  장치에 대 한 hello 기본 및 보조 DNS 서버, 시간 설정 및 선택적으로 프록시 설정을 구성할 수 있습니다. 대부분의 네트워크 구성은 hello 일회성 설정입니다. 검토 hello [네트워킹 요구 사항이 StorSimple](storsimple-ova-system-requirements.md#networking-requirements) 이전 toodeploying hello 가상 배열입니다.

가상 배열을 배포할 때에는 다음과 같은 모범 사례를 따르는 것이 좋습니다.

* 가상 배열 항상 배포는 hello에 해당 hello 네트워크에 hello 용량 toodedicate 5 Mbps 인터넷 대역폭 (이상) 확인 하십시오.
  
  * 인터넷 대역폭 요구 작업 특성 및 hello 데이터 변경 률에 따라 달라 집니다.
  * 처리 될 수 있는 hello 데이터 변경에 정비례 tooyour 인터넷 대역폭입니다. 예를 들어 백업을 수행할 때 5Mbps 대역폭은 8시간에 약 18GB의 데이터를 변경할 수 있습니다. 대역폭이 4배 증가하면(20Mbps) 4배 더 많은 데이터 변경(72GB)을 처리할 수 있습니다.
* 인터넷 연결 toohello를 항상 사용할 수 있는지 확인 합니다. 불안정 하거나 자주 끊기면 인터넷 연결 toohello 장치 hello 클라우드에서 액세스 toodata 손실 될 수 있습니다 및 구성이 지원 될 수 있습니다.
* Toodeploy iSCSI 서버와 장치를 계획 하는 경우:
  
  * Hello를 사용 하지 않도록 설정 하는 것이 좋습니다 **IP 주소를 자동으로 가져오기** 옵션 (DHCP).
  * 고정 IP 주소를 구성합니다. 기본 및 보조 DNS 서버를 구성해야 합니다.
  * 첫 번째 네트워크 인터페이스 hello만 가상 배열에서 여러 네트워크 인터페이스를 정의 하는 경우 (기본적으로이 인터페이스는 **이더넷**) hello 클라우드를 연결할 수 있습니다. toocontrol hello 종류의 트래픽을 가상 배열 (iSCSI 서버로 구성)에 여러 가상 네트워크 인터페이스를 만들 고 이러한 인터페이스 toodifferent 서브넷을 연결할 수 있습니다.
* toothrottle hello 클라우드 대역폭만 (hello 가상 배열에 사용) hello 라우터 또는 방화벽 hello에 대 한 제한을 구성 합니다. 프로그램 하이퍼바이저 제한을 정의 하는 경우 방금 hello 클라우드 대역폭 대신 iSCSI 및 SMB를 비롯 한 모든 hello 프로토콜을 제한 됩니다.
* 하이퍼바이저에 대한 시간 동기화를 확인합니다. Hyper-v를 사용 하 여 가상 배열 hello Hyper-v 관리자를 선택 하는 경우 너무 이동**설정 &gt; Integration Services**, 해당 hello 확인 **시간 동기화** 을 선택 합니다.

### <a name="storage-accounts"></a>저장소 계정
StorSimple 가상 배열은 단일 저장소 계정과 연결할 수 있습니다. 이 저장소 계정을 자동으로 생성된 된 저장소 계정, hello에 계정이 수 hello 서비스 또는 저장소 계정으로 동일한 구독 관련 tooanother 구독 합니다. 자세한 내용은 참조 방법을 너무[가상 배열에 대 한 저장소 계정을 관리](storsimple-virtual-array-manage-storage-accounts.md)합니다.

사용 하 여 hello 가상 배열와 연결 된 저장소 계정에 대 한 권장 사항을 따르면 합니다.

* Hello 최대 용량 (64TB) 가상 배열 및 저장소 계정에 대 한 hello 최대 크기 (500 테라바이트)에 대 한 단일 저장소 계정 사용 하 여 여러 가상 배열, 링크할 때 고려해 야 합니다. 이 해당 저장소 계정 tooabout 7 연관 될 수 있는 전체 크기가 가상 배열 hello 수를 제한 합니다.
* 새 저장소 계정을 만드는 경우
  
  * Hello 지역 가장 가까운 toohello 원격 본사/지사 사무실에 StorSimple 가상 배열 인 배포 된 toominimize 대기 시간이 만드는 것이 좋습니다.
  * 지역 간에 저장소 계정을 이동할 수 없다는 점을 염두에 두어야 합니다. 또한 구독 간에 서비스를 이동할 수 없습니다.
  * Hello 데이터 센터 간의 중복성을 구현 하는 저장소 계정을 사용 합니다. GRS(지역 중복 저장소), ZRS(영역 중복 저장소) 및 LRS(로컬 중복 저장소)는 모두 가상 배열에 사용할 수 있습니다. 저장소 계정의 hello 서로 다른 형식에 대 한 자세한 내용은 이동 너무[Azure 저장소 복제](../storage/common/storage-redundancy.md)합니다.

### <a name="shares-and-volumes"></a>공유 및 볼륨
StorSimple 가상 배열이 파일 서버로 구성되면 공유를 프로비전할 수 있고, iSCSI 서버로 구성되면 볼륨을 프로비전할 수 있습니다. 공유 및 볼륨 만들기에 대 한 유용한 hello toohello 크기와 hello 형식이 구성 관련 되어 있습니다.

#### <a name="volumeshare-size"></a>볼륨/공유 크기
가상 배열이 파일 서버로 구성되면 공유를 프로비전할 수 있고, iSCSI 서버로 구성되면 볼륨을 프로비전할 수 있습니다. 공유 및 볼륨 만들기에 대 한 유용한 hello toohello 크기 관련 되는 및 hello 구성 된 유형입니다. 

공유 또는 가상 장치에서 볼륨을 프로 비전 할 때 모범 사례를 따르는 유의 hello에 보관 합니다.

* hello 계층화 된 공유의 파일 크기를 프로 비전 하는 상대 toohello 크기 hello 계층화 성능에 영향을 줄 수 있습니다. 큰 파일로 작업하면 계층화가 매우 느려질 수 있습니다. 큰 파일을 사용 하는 경우에 hello이 가장 큰 파일은 hello 공유 크기의 3% 보다 작은 것이 좋습니다.
* Hello 가상 배열에는 최대 16 볼륨/공유를 만들 수 있습니다. 에 대 한 hello의 hello 크기 제한을 로컬로 고정 된 볼륨/공유 계층을 항상 toohello 참조 [StorSimple 가상 배열 제한](storsimple-ova-limits.md)합니다.
* 볼륨을 만들 때의 향후 데이터 증가 예상 하는 hello 데이터 소비에 고려해 야 합니다. hello 볼륨은 나중에 확장할 수 없습니다.
* Hello 볼륨을 만든 후 hello StorSimple에 hello 볼륨 크기를 축소할 수 없습니다.
* Tooa 작성 hello 볼륨 데이터 (상대 toohello 로컬 공간 hello 볼륨에 대 한 예약) 특정 임계값에 도달 하면 볼륨을 StorSimple, 계층, hello IO 제한 되었습니다. Toowrite toothis 볼륨 계속 천천히 hello IO 현저 하 게 합니다. Tooa를 쓸 수는 없지만 볼륨 (म 중지 하지 않고 적극적으로 hello 프로 비전 된 용량 이상 쓰이지 않도록에서 hello 사용자) 프로 비전 된 용량 이상 계층의 초과 구독 될 있어야 하는 경고 알림 toohello 효과 참조 하십시오. Hello 볼륨 데이터를 삭제 하는 등 수정 조치를 취하는 명령적 되었을 hello 경고가 표시 되 면 (볼륨 확장은 현재 지원 되지 않음).
* 재해 복구 사용 사례에 대 한 hello 수가 허용 가능한 공유/볼륨은 16 이며 최대 hello 병렬로 처리할 수 있는 공유/볼륨의 수는 또한 16, 공유/볼륨 수가 hello RPO 및 Rto에 영향이 없습니다.

#### <a name="volumeshare-type"></a>볼륨/공유 유형
StorSimple 지원 hello 사용에 따라 두 볼륨/공유 형식: 로컬로 고정 된 한 계층입니다. 로컬 고정된 볼륨/공유 hello 계층화 된 볼륨/공유는 씬 프로 비전 하는 반면 씩 프로 비전 됩니다. 로컬 고정된 볼륨/공유 tootiered 변환할 수 없습니다 또는 *반대의* 한 번 생성 합니다.

StorSimple 볼륨/공유를 구성할 때 모범 사례를 따르는 hello를 구현 하는 것이 좋습니다.

* Hello 작업 볼륨을 만들기 전에 toodeploy를 만들려는 경우에 따라 hello 볼륨 형식을 확인 하십시오. 데이터 로컬 보증이 필요하고(클라우드가 중단되더라도) 클라우드 대기 시간이 낮아야 하는 워크로드에는 로컬로 고정된 볼륨을 사용합니다. 로컬로 고정 된 tootiered에서 hello 볼륨 종류를 변경할 수 없습니다 가상 배열에 볼륨을 만든 후 또는 *반대로*합니다. 예를 들어 SQL 워크로드 또는 VM(가상 컴퓨터)을 호스팅하는 워크로드를 배포할 때에는 파일 공유 워크로드를 위한 계층화 볼륨을 사용합니다.
* 큰 파일 크기를 처리할 때 자주 사용 되는 하지 않는 아카이브 데이터에 대 한 hello 옵션을 선택 합니다. 이 옵션을 사용 하는 경우 512kb 보다 큰 중복 제거 청크 크기가 사용 되는 tooexpedite hello 데이터 toohello 클라우드를 전송 합니다.

#### <a name="volume-format"></a>볼륨 형식
Tooinitialize, 탑재, 및 형식 hello 필요한 iSCSI 서버에서 StorSimple 볼륨을 만든 후 볼륨입니다. Hello 연결 호스트 tooyour StorSimple 장치에서이 작업을 수행 합니다. 탑재 및 hello StorSimple 호스트의 볼륨을 포맷할 때 다음과 같은 최상의 방법은 사용 하는 것이 좋습니다.

* 모든 StorSimple 볼륨에서 빠른 포맷을 수행합니다.
* StorSimple 볼륨을 포맷할 때에는 할당 단위 크기(AUS) 64KB(기본값은 4KB)를 사용합니다. hello 64 KB AUS 기반으로 일반적인 StorSimple 작업 및 기타 작업에 대 한 내부에서 수행 된 테스트 합니다.
* ISCSI 서버로 구성 하는 StorSimple 가상 배열 hello를 사용 하 여 사용 하지 마십시오 스팬된 볼륨 또는 동적 디스크는 이러한 볼륨 또는 디스크 StorSimple에서 지원 되지 않는 경우.

#### <a name="share-access"></a>공유 액세스
가상 배열 파일 서버에 공유를 만들 때에는 다음 지침을 따르세요.

* 공유를 만들 때 사용자 그룹을 단일 사용자 대신 공유 관리자로 할당합니다.
* Windows 탐색기를 통해 hello 공유를 편집 하 여 hello 공유를 만든 후 hello NTFS 사용 권한을 관리할 수 있습니다.

#### <a name="volume-access"></a>볼륨 액세스
StorSimple 가상 배열에 hello iSCSI 볼륨을 구성할 때 중요 한 toocontrol 액세스는 필요할 때마다 다시 설명 합니다. toodetermine 서버를 호스트 하는 볼륨을 액세스할 수, 작성 및 액세스 제어 레코드 (Acr) StorSimple 볼륨을 연결 합니다.

StorSimple 볼륨에 대 한 Acr를 구성할 때 모범 사례를 따르는 hello를 사용 합니다.

* 볼륨 하나에 반드시 하나 이상의 ACR을 연결합니다.

* 둘 이상의 ACR tooa 볼륨을 할당할 때 hello 볼륨에 액세스할 수 있습니다 동시에 둘 이상의 클러스터 되지 않은 호스트에 의해 방식으로 노출 되지 않도록 확인 합니다. 여러 Acr tooa 볼륨에 할당 한 경우 경고 메시지가 팝업 tooreview 있습니다에 대 한 구성 됩니다.

### <a name="data-security-and-encryption"></a>데이터 보안 및 암호화
StorSimple 가상 배열에 데이터의 hello 기밀성과 무결성을 보장 하는 데이터 보안 및 암호화 기능이 있습니다. 이러한 기능을 사용할 때에는 다음과 같은 모범 사례를 따르는 것이 좋습니다. 

* 가상 배열 toohello 클라우드에서 hello 데이터를 보내기 전에 클라우드 저장소 암호화 키 toogenerate aes-256 암호화를 정의 합니다. 데이터가 암호화 된 toobegin 된 경우이 키는 필요 하지 않습니다. hello 키 생성 및 수와 같은 키 관리 시스템을 사용 하 여 안전 하 게 보호 유지 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md)합니다.
* Hello SSL 모드 toocreate 사용 하도록 설정 되었는지 확인 hello StorSimple Manager 서비스를 통해 hello 저장소 계정을 구성 하면 StorSimple 장치와 hello 사이의 네트워크 통신을 위한 보안 채널 클라우드입니다.
* 주기적으로 (hello Azure 저장소 서비스에 액세스)에서 저장소 계정에 대 한 키를 다시 생성 hello에 대 한 tooaccount tooaccess 관리자 변경 hello 목록에 따라를 변경 합니다.
* 가상 배열에는 데이터 압축 되며 tooAzure 전송 하기 전에 중복 됩니다. Windows Server 호스트에 hello 데이터 중복 제거 역할 서비스를 사용 하지 않는 것이 좋습니다.

## <a name="operational-best-practices"></a>운영 모범 사례
hello operational 모범 사례는 hello 일상적인 관리 또는 hello 가상 배열의 작업 중 수행 해야 할 합니다. 이러한 사용 약관 백업, 백업 세트, 장애 조치 수행, 비활성화 및 삭제 hello 배열, 시스템 사용량 모니터링 및에서 상태를 복원 하는 것 등의 특정 관리 작업을 포함 하 고 가상 배열에서 검색 바이러스를 실행 합니다.

### <a name="backups"></a>백업
hello 데이터가 가상 배열에서 두 가지 방법으로 toohello 클라우드 백업, 기본 자동 매일 백업을 22 시 30 또는 수동 요청 시 백업을 통해 hello 전체 장치를 시작 합니다. 기본적으로 hello 장치에 상주 하는 모든 hello 데이터의 일별 클라우드 스냅숏이 자동으로 만듭니다. 자세한 내용은 이동 너무[StorSimple 가상 배열을 백업](storsimple-virtual-array-backup.md)합니다.

hello 빈도 보존 hello 기본 백업과와 관련 된 변경할 수 없지만 hello 일별 백업이 매일 시작는 hello 시간을 구성할 수 있습니다. 자동화 된 백업을, hello에 대 한 hello 시작 시간을 구성 하는 경우 것을 권장 합니다.

* 사용량이 적은 시간에 백업을 예약합니다. 백업 시작 시간에 수많은 호스트 IO가 발생하지 않아야 합니다.
* 장치 장애 조치 나 가상 배열에서 tooprotect hello 데이터 유지 관리 기간 이전 toohello tooperform를 계획할 때 수동 요청 시 백업을 시작 합니다.

### <a name="restore"></a>복원
두 가지 방법으로 설정 하는 백업에서 복원할 수 있습니다: tooanother 볼륨 또는 공유를 복원 하거나 항목 수준의 복구 (파일 서버를 구성 하는 가상 배열에 대해서만 사용 가능)를 수행 합니다. 항목 수준 복구 hello StorSimple 장치에서 toodo 모든 hello 공유의 클라우드 백업에서 파일 및 폴더의 세분화 된 복구를 허용 합니다. 자세한 내용은 이동 너무[백업에서 복원](storsimple-virtual-array-clone.md)합니다.

복원을 수행할 때 유의 해야 하는 지침을 따르는 hello에 유의 하십시오.

* StorSimple 가상 배열은 바로 복원을 지원하지 않습니다. 그러나 수 쉽게 낼 수는 두 단계로: 배열 하 고 다음 tooanother 볼륨/공유 복원 가상 hello에 공간을 만들 합니다.
* 로컬 볼륨을 복원할 때 유의 hello 복원에 장기 실행 작업이 됩니다. Hello 볼륨 더 신속 하 게 온라인 상태가 되지만 hello 데이터 toobe 하이드레이션 hello 백그라운드에서 계속 됩니다.
* hello 볼륨 유형 남아 hello 복원 과정 동안 동일 hello 합니다. 계층화 된 볼륨이 복원 된 볼륨 및 로컬 고정된 볼륨 tooanother 로컬로 고정 볼륨 tooanother 계층입니다.
* Hello 복원 작업이 실패 하면 볼륨 또는 백업 세트에서 공유 toorestore 시도, 대상 볼륨 또는 공유의 여전히 있습니다 때 hello 포털에서 만들 수 있습니다. 이 사용 되지 않는 대상 볼륨을 삭제 하거나이 요소에서 발생 하는 모든 향후 문제 hello 포털 toominimize에서 공유 하는 것입니다.

### <a name="failover-and-disaster-recovery"></a>장애 조치(Failover) 및 재해 복구
장치 장애 조치 하면 toomigrate에서 데이터는 *소스* hello 데이터 센터 tooanother에서 장치 *대상* 동일 하거나 서로 다른 지리적 위치 장치 hello에 있습니다. 장치 장애 조치 hello hello 전체 장치입니다. 장애 조치 중 hello 소스 장치에 대 한 클라우드 데이터 hello hello 대상 장치의 소유권 toothat을 변경합니다.

장애 조치 tooanother 가상 배열에서 관리 하는 hello 동일만 수 StorSimple 가상 배열에 대 한 StorSimple Manager 서비스입니다. 장애 조치 tooan 8000 시리즈 장치 또는 hello 하나 hello 소스 장치에 대 한) (보다 다른 StorSimple Manager 서비스에서 관리 하는 배열을 허용 되지 않습니다. hello 장애 조치 고려 사항에 대해 자세히 toolearn 너무 이동[hello 장치 장애 조치에 대 한 필수 구성 요소](storsimple-virtual-array-failover-dr.md)합니다.

오류를 통해 가상 배열를 수행할 때는 hello 다음 염두에서에 둬야 합니다.

* 계획된 된 장애 조치는 권장된 모범 사례 tootake 모든 hello 볼륨/공유 오프 라인 이전 tooinitiating hello 장애 조치입니다. Tootake hello 볼륨/공유 오프 라인으로 hello에서 먼저 호스트 알아본 후 된 오프 라인 가상 장치에서 hello 운영 체제 관련 지침을 따릅니다.
* 에서는 파일 서버 장애 복구 (DR)에 대 한 공유 권한을 hello 하는 hello 소스와 동일한 도메인에 자동으로 해결 되었는지 hello 대상 장치 toohello 참가 하는 것이 좋습니다. 만 hello 장애 조치 tooa 대상 장치에 hello 동일한 도메인은이 버전에서 지원 됩니다.
* Hello DR 성공적으로 완료 되 면 hello 소스 장치가 자동으로 삭제 됩니다. Hello 장치를 더 이상 사용할 수 있지만 hello 호스트 시스템에서 프로 비전 하는 hello 가상 컴퓨터는 여전히 리소스를 소비 합니다. 에서 삭제 하는이 가상 컴퓨터 호스트 시스템 tooprevent 비용이에서 발생 하는 것이 좋습니다.
* 마십시오 유의 hello 장애 조치가 성공적으로 하는 경우에 **hello 데이터는 항상 안전 hello 클라우드**합니다. 다음 세 가지 시나리오는 hello에 장애 조치 완료 되지 않았습니다 hello를 고려 합니다.
  
  * Hello hello DR 사전 검사를 수행 하는 경우 같은 hello 장애 조치의 초기 단계에서 오류가 발생 했습니다. 이 경우 대상 장치를 여전히 사용할 수 있습니다. Hello에 hello 장애 조치를 다시 시도할 수 동일한 대상 장치입니다.
  * Hello 실제 장애 조치 프로세스 중에 오류가 발생 했습니다. 이 경우 hello 대상 장치를 사용할 수 없게 표시 되어 있습니다. 다른 대상 가상 배열을 프로비전 및 구성한 후 장애 조치(Failover)에 사용해야 합니다.
  * hello 장애 조치는 hello 원본 장치가 삭제 된 다음 완료 된 하지만 hello 대상 장치 문제가 고 모든 데이터에 액세스할 수 없습니다. hello 데이터 여전히 안전 hello 클라우드에서 이며 다른 가상 배열 생성 및 다음 hello DR 위한 대상 장치로 사용 하 여 쉽게 검색할 수 있습니다.

### <a name="deactivate"></a>비활성화
StorSimple 가상 배열을 비활성화 하면 hello 장치와 StorSimple Manager 서비스를 해당 하는 hello hello 연결 서버. 비활성화는 **영구** 작업이며 실행 취소할 수 없습니다. 비활성화 된 장치 hello StorSimple Manager 서비스에 다시 등록할 수 없습니다. 자세한 내용은 이동 너무[비활성화 및 삭제 StorSimple 가상 배열](storsimple-virtual-array-deactivate-and-delete-device.md)합니다.

Hello 가상 배열 비활성화 하는 경우에 유용한 정보를 다음에 유의 하십시오.

* 모든 hello 데이터 사전 toodeactivating 가상 장치의 클라우드 스냅숏을 만듭니다. 가상 배열 비활성화 하면 모든 hello 로컬 장치 데이터가 손실 됩니다. 클라우드 스냅숏을 만드는 하면 toorecover 데이터 이후 단계에서 있습니다.
* StorSimple 가상 배열 비활성화 하기 전에 toostop 있는지 확인 하거나 클라이언트와 해당 장치에 종속 된 호스트를 삭제 합니다.
* 비용이 발생하지 않도록 장치를 더 이상 사용하지 않으려면 장치를 비활성화합니다.

### <a name="monitoring"></a>모니터링
연속 정상 상태에 있는 StorSimple 가상 배열 tooensure toomonitor 필요한 배열 hello 및 경고를 포함 하 여 hello 시스템에서 정보를 수신 하는지 확인 합니다. toomonitor hello hello 가상 배열에 최선의 구현 방법을 구현 hello의 전반적인 상태:

* Hello OS 디스크 물론 가상 배열 데이터 디스크의 tootrack hello 디스크 사용량 모니터링을 구성 합니다. Hyper-v를 실행 하는 경우 가상화 호스트에 SCVMM System Center Virtual Machine Manager () 및 System Center Operations Manager (SCOM) toomonitor의 조합을 사용할 수 있습니다.
* 특정 사용량 수준에서 가상 배열 toosend 경고의 전자 메일 알림을 구성 합니다.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>인덱스 검색 및 바이러스 스캔 응용 프로그램
StorSimple 가상 배열 hello 로컬 계층 toohello Microsoft Azure 클라우드에에서 데이터 계층 자동으로 구성할 수 있습니다. StorSimple에 저장 된 hello 데이터를 사용 하는 tooscan 인덱스 검색 또는 바이러스 검사와 같은 응용 프로그램을 사용 하는 경우는 hello 클라우드 데이터 고 되지 않는 가져올 액세스 toohello 로컬 계층을 다시 가져온 tootake 주의 해야 합니다.

가상 배열에서 인덱스 검색 또는 바이러스 검색 hello를 구성할 때 모범 사례를 따르는 hello를 구현 하는 것이 좋습니다.

* 자동으로 구성된 모든 전체 스캔 작업을 사용하지 않도록 설정합니다.
* 계층화 된 볼륨에 대 한 hello 인덱스 검색 또는 바이러스 검사 응용 프로그램 tooperform 증분 검색을 구성 합니다. 이만 hello 새 데이터 가능성이 있는 hello 로컬 계층에서 검색 합니다. 증분 작업 중 hello 데이터 계층 구성된 toohello 클라우드를 액세스할 수 없습니다.
* 올바른 검색 필터 hello 및 설정이 구성 되어 파일의 의도 한 hello 형식만 검사할지 있어를 확인 합니다. 예를 들어 이미지 파일 (JPEG, GIF 및 TIFF) 및 드로잉 엔지니어링 하지을 스캔 해야 하는지 hello 증분 또는 전체 인덱스 다시 작성 중입니다.

Windows 인덱싱 프로세스를 사용하는 경우 다음 지침을 따르세요.

* Hello 인덱스 toobe 자주 다시 작성 해야 하는 경우는 많은 양의 데이터 (TBs) hello 클라우드에서 회수 하는 대로 계층화 된 볼륨에 대 한 인덱서 Windows hello를 사용 하지 마십시오. Hello 인덱스를 다시 작성 검색 모든 파일 형식을 tooindex 콘텐츠 않습니다.
* Hello Windows hello 로컬 계층 toobuild hello 인덱스 (hello 클라우드 데이터에 액세스할 수 없습니다)에 대해 데이터에만 액세스는이 처럼 인덱싱 로컬 고정된 볼륨에 대 한 프로세스를 사용 합니다.

### <a name="byte-range-locking"></a>바이트 범위 잠금
응용 프로그램 hello 파일 내에서 지정 된 바이트 범위를 잠글 수 있습니다. 바이트 범위 잠금 하십시오 tooyour StorSimple을 작성 하는 하는 hello 응용 프로그램에서 사용 하는 경우 다음 계층화 해도 가상 배열에서 작동 하지 않습니다. Hello 계층화 toowork에 대 한 액세스 hello 파일의 모든 영역 잠금 되어야 합니다. 가상 배열의 가상화 볼륨에는 바이트 범위 잠금이 지원되지 않습니다.

권장 되는 측정값 포함 tooalleviate 바이트 범위 잠금:

* 응용 프로그램 논리에서 바이트 범위 잠금을 해제합니다.
* 사용 하 여 로컬 고정 볼륨 (대신 계층형)이 응용이 프로그램과 관련 된 hello 데이터에 대 한 합니다. 로컬로 고정 된 볼륨 hello 클라우드로 계층 하지 않습니다.
* 사용 하 여 로컬로 고정 된 볼륨 바이트 범위 잠금 사용 하도록 설정 된 경우 hello 복원이 완료 된 hello 볼륨 온라인 가져올 수 있습니다. 이러한 경우에 hello 복원 toobe 완료 대기 해야 합니다.

## <a name="multiple-arrays"></a>다중 배열
여러 가상 배열 인해 hello 장치의 hello 성능이 떨어지게 hello 클라우드에 spill 수 있는 데이터의 증가 작업 집합 배포 toobe tooaccount이 필요할 수 있습니다. 이러한 경우에 증가 하는 hello 작업 집합 되 최상의 tooscale 장치입니다. 이렇게 하려면 하나 이상의 장치 toobe hello 온-프레미스 데이터 센터에 추가 합니다. Hello 장치를 추가할 때 할 수 없습니다.

* 분할 hello 현재 데이터의 집합입니다.
* 새 작업 toonew 장치를 배포 합니다.
* 부하 분산에서 권장 하는 여러 가상 배열을 배포 하는 경우 관점에서 다른 하이퍼바이저 호스트 hello 배열 분산 합니다.
* 다중 가상 배열(파일 서버 또는 iSCSI 서버로 구성된 경우)을 분산 파일 시스템 네임스페이스에 배포할 수 있습니다. 자세한 단계에 대 한 이동 너무[하이브리드 클라우드 저장소 배포 지침과 파일 시스템 Namespace 솔루션 Distributed](https://www.microsoft.com/download/details.aspx?id=45507)합니다. 분산된 파일 시스템 복제는 현재 바람직하지 hello 가상 배열 사용. 

## <a name="see-also"></a>참고 항목
너무 방법에 대해 알아봅니다[StorSimple 가상 배열 관리](storsimple-virtual-array-manager-service-administration.md) hello StorSimple Manager 서비스를 통해 합니다.

