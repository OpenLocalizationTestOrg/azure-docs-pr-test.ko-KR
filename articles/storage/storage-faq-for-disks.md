---
title: "Azure IaaS VM 디스크에 대한 질문과 대답(FAQ) | Microsoft Docs"
description: "Azure IaaS VM 디스크 및 프리미엄 디스크(관리 및 관리되지 않는 디스크)에 대한 질문과 대답"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Azure IaaS VM 디스크와 관리 및 관리되지 않는 프리미엄 디스크에 대한 질문과 대답

이 문서에서는 Azure Managed Disks 및 Azure Premium Storage에 대해 몇몇 자주 묻는 질문과 대답을 설명합니다.

## <a name="managed-disks"></a>Managed Disks

**Azure Managed Disks란?**

Managed Disks는 저장소 계정 관리를 처리하여 Azure IaaS VM을 위한 디스크 관리를 간소화하는 기능입니다. 자세한 내용은 참조 hello [관리 하는 디스크 개요](storage-managed-disks-overview.md)합니다.

**80GB인 기존 VHD에서 표준 Managed Disk를 만들 경우 비용은 얼마나 드나요?**

80 GB VHD에서 만든 표준 관리 디스크는 S10 디스크 hello 다음 사용 가능한 표준 디스크 크기로 처리 됩니다. 에 따라 toohello S10 디스크 가격으로 청구 됩니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.

**표준 관리 디스크에 대한 트랜잭션 비용이 있나요?**

예. 각 트랜잭션에 대해 요금이 부과됩니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.

**표준 관리 디스크에 대 한 됩니다 수수료를 지불 합니까 hello 디스크의 사용자를 프로 비전 하는 hello 용량 또는 hello hello hello 디스크 데이터의 실제 크기에 대 한?**

Hello 디스크의 hello 프로 비전 된 용량에 따라 요금이 부과 됩니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.

**프리미엄 Managed Disks의 가격은 관리되지 않는 디스크와 어떻게 다르게 책정되나요?**

관리 되지 않는 프리미엄 디스크와 동일 hello hello 관리 프리미엄 디스크의 가격입니다.

**Hello 저장소 계정 유형 (Standard 또는 Premium) 내 관리 되는 디스크의 변경할 수 있나요?**

예. 관리 되는 디스크의 저장소 계정 유형은 hello hello Azure 포털, PowerShell 또는 Azure CLI hello를 사용 하 여 변경할 수 있습니다.

**방법이 있습니까는를 복사 하거나 관리 되는 디스크 tooa 개인 저장소 계정 내보낼 수 있습니까?**

예. Hello Azure 포털, PowerShell 또는 Azure CLI hello를 사용 하 여 관리 되는 디스크를 내보낼 수 있습니다.

**다른 구독으로 Azure 저장소 계정 toocreate 관리 되는 디스크에에서 VHD 파일을 사용할 수 있습니까?**

아니요.

**다른 지역에 Azure 저장소 계정 toocreate 관리 되는 디스크에에서 VHD 파일을 사용할 수 있습니까?**

아니요.

**고객이 Managed Disks를 사용하는 경우 규모 제한이 있나요?**

관리 되는 디스크 저장소 계정과 연관 된 hello 제한을 제거 합니다. 그러나 hello 수의 구독에 대해 관리 되는 디스크는 제한 too2, 기본적으로 000입니다. 이 숫자 지원 tooincrease를 호출할 수 있습니다.

**관리 디스크의 증분 스냅숏을 가져올 수 있나요?**

아니요. hello 현재 스냅숏 기능이 관리 되는 디스크의 전체 복사본을 만듭니다. 그러나 toosupport 증분 스냅숏 hello 향후에 계획 합니다.

**관리 및 관리되지 않는 디스크를 조합하여 가용성 집합의 VM을 구성할 수 있나요?**

아니요. 가용성 집합에 Vm hello 모든 관리 되는 디스크 또는 모든 관리 되지 않는 디스크 중 하나를 사용 해야 합니다. 디스크의 종류를 선택할 수는 가용성 집합을 만들 때 원하는 toouse 합니다.

**Hello Azure 포털에서에서 관리 하는 디스크 hello 기본 옵션이입니다.**

현재는 향후 hello에 hello 기본 사이트용으로 하지만 합니다.

**내가 빈 관리 디스크를 만들 수 있나요?**

예. 사용자가 빈 디스크를 만들 수 있습니다. 관리 되는 디스크를 만들 수 있습니다는 VM을 독립적으로 예를 들어 tooa VM을 연결 하지 않고도.

**관리 하는 디스크를 사용 하는 가용성 집합에 대 한 지원 hello 장애 도메인 수 란?**

관리 하는 디스크를 사용 하는 hello 가용성 집합 위치한 hello 지역에 따라 지원 hello 장애 도메인 수는 2 또는 3입니다.

**진단 설정에 대 한 표준 저장소 계정이 hello는 어떻게 합니까?**

VM 진단을 위한 개인 저장소 계정을 설정할 수 있습니다. Hello 이후, tooswitch 진단 계획 tooManaged 디스크는 물론 합니다.

**어떤 종류의 역할 기반 액세스 제어 지원을 Managed Disks에 사용할 수 있나요?**

Managed Disks에서는 세 가지 주요 기본 역할을 지원합니다.

* 소유자: 액세스를 포함한 모든 것을 관리할 수 있음
* 참여자: 액세스를 제외한 모든 것을 관리할 수 있음
* 읽기 권한자: 모든 항목을 볼 수 있지만 변경할 수 없음

**방법이 있습니까는를 복사 하거나 관리 되는 디스크 tooa 개인 저장소 계정 내보낼 수 있습니까?**

읽기 전용 공유 액세스 서명을 사용 하 여 관리 하는 hello에 대 한 URI 디스크 toocopy hello 내용을 tooa 개인 저장소 계정 또는 온-프레미스 저장소를 얻을 수 있습니다.

**내 관리 디스크의 복사본을 만들 수 있나요?**

고객 수는 관리 되는 디스크의 스냅숏을 만들고 hello 스냅숏 toocreate 다른 관리 되는 디스크를 사용 합니다.

**관리되지 않는 디스크도 계속 지원되나요?**

예. 관리되지 않는 디스크 및 Managed Disks가 모두 지원됩니다. 새 워크 로드에 대 한 관리 되는 디스크를 사용 하 고 현재 작업 toomanaged 디스크를 마이그레이션하는 것이 좋습니다.


**128 50GB 디스크를 만들고 다음 hello 크기 too130 GB를 늘려, 됩니다 수수료를 지불 합니까 hello 다음 디스크 크기 (512GB)에 대 한?**

예.

**로컬 중복 저장소, 지역 중복 저장소 및 영역 중복 저장소 Managed Disks를 만들 수 있나요?**

Azure Managed Disks에서는 현재 로컬 중복 저장소 Managed Disks만 지원합니다.

**Managed Disks를 축소하거나 크기를 줄일 수 있나요?**

아니요. 이 기능은 현재 지원되지 않습니다. 

**사용 되는 tooprovision VM을는 운영 체제 디스크는 특수화 된 (hello 시스템 준비 도구를 사용 하 여 생성 또는 범용으로 설정) 하는 경우 hello 컴퓨터 이름 속성 변경 합니까?**

아니요. Hello 컴퓨터 이름 속성을 업데이트할 수 없습니다. hello 새 VM 상속 hello 부모가 사용 되는 toocreate hello 운영 체제 디스크는 VM에서 합니다. 

**관리 되는 디스크와 Azure 리소스 관리자 템플릿 toocreate Vm을 샘플은 어디서 찾을 수 있습니까?**
* [Managed Disks를 사용하는 템플릿 목록](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Managed Disks 및 Storage 서비스 암호화 

**Managed Disk를 만들 경우 Azure Storage 서비스 암호화를 기본적으로 사용하나요?**

예.

**Hello 암호화 키를 관리 하는 사람?**

Microsoft은 hello 암호화 키를 관리합니다.

**내 Managed Disks에 Storage 서비스 암호화를 비활성화할 수 있나요?**

아니요.

**Storage 서비스 암호화는 특정 지역에서만 사용할 수 있나요?**

아니요. 것은 관리 하는 디스크를 사용할 수 있는 모든 hello 지역에서 사용할 수 있습니다. 모든 공용 지역 및 독일에서 Managed Disks를 사용할 수 있습니다.

**내 Managed Disk가 암호화되었는지 어떻게 확인할 수 있나요?**

Hello 시간 hello Azure 포털, Azure CLI hello 및 PowerShell에서 관리 되는 디스크를 만들 때 확인할 수 있습니다. Hello 시간은 2017 년 6 월 9 후 디스크에 암호화 되어 있습니다. 

**2017년 6월 10일 이전에 만들어진 내 기존 디스크를 어떻게 암호화할 수 있나요?**

2017 년 6 월 10부터 tooexisting 관리 되는 디스크에 기록 하는 새 데이터 자동으로 암호화 됩니다. 기존 데이터 용량의 tooencrypt 예정도 및 hello 암호화 hello 백그라운드에서 비동기적으로 수행 됩니다. 이제 기존 데이터를 암호화해야 하는 경우 디스크의 복사본을 만듭니다. 새 디스크가 암호화됩니다.

* [Hello Azure CLI를 사용 하 여 관리 하는 디스크 복사](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [PowerShell을 사용하여 Managed Disks 복사](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**관리되는 스냅숏 및 이미지가 암호화되나요?**

예. 2017년 6월 9일 이후에 만든 모든 관리되는 스냅숏 및 이미지는 자동으로 암호화됩니다. 

**추가 되거나 이전에 암호화 된 toomanaged 디스크인 저장소 계정에 있는 관리 되지 않는 디스크가 있는 Vm을 변환할 수 있습니까?**

예

**Managed Disk 또는 스냅숏에서 내보낸 VHD도 암호화되나요?**

아니요. VHD tooan 내보낼 경우 수는 스냅숏, 또는 암호화 된 관리 되는 디스크에서 저장소 계정 암호화 한 다음 암호화 합니다. 

## <a name="premium-disks-managed-and-unmanaged"></a>프리미엄 디스크: 관리 및 관리되지 않는 디스크

**VM에서 DSv2와 같이 Premium Storage를 지원하는 크기를 사용하는 경우 프리미엄 및 표준 데이터 디스크를 모두 연결할 수 있나요?** 

예.

**Premium 및 D, Dv2, G 또는 F 계열과 같이 프리미엄 저장소를 지원 하지 않는 표준 데이터 디스크 tooa 크기 계열 둘 다에 연결할 수 있나요?**

아니요. 만 표준 데이터 디스크 tooVMs 지 프리미엄 저장소를 원하는 크기 시리즈를 사용 하지 않는 연결할 수 있습니다.

**80GB인 기존 VHD로 프리미엄 데이터 디스크를 만들 경우 비용은 얼마가 드나요?**

프리미엄 데이터 디스크를 80 GB VHD에서 만든 P10 디스크 hello 다음 사용 가능한 프리미엄 디스크 크기로 처리 됩니다. 에 따라 toohello P10 디스크 가격으로 청구 됩니다.

**프리미엄 저장소 트랜잭션 비용 toouse 있습니까?**

특정 한도의 IOPS 및 처리량이 프로비전되는 디스크 크기마다 고정 비용이 있습니다. hello 기타 비용은 아웃 바운드 대역폭 및 스냅숏 용량을 해당 하는 경우입니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage)합니다.

**I hello 디스크 캐시에서 얻을 수 있는 처리량 및 IOPS에 대 한 hello 제한 사항은 무엇입니까?**

캐시에 대 한 결합 된 제한을 hello 및 DS 시리즈에 대 한 로컬 SSD는 4, 000 IOPS 코어 수 및 코어당 초당 33MB 합니다. hello GS 시리즈 코어당 5,000 IOPS 및 초당 코어당 라이선스 모델을 제공합니다.

**로컬 SSD 디스크 관리 되는 VM에 대해 지원 되는 hello?**

hello 로컬 SSD는 임시 저장소 디스크 관리 되는 VM에 포함 되어 있는 합니다. 이 임시 저장소에 대한 추가 비용은 없습니다. 사용 하지 않는 로컬 SSD toostore이 응용 프로그램 데이터 Azure Blob 저장소에 지속 되지 않으므로 하는 것이 좋습니다.

**모든 영향 hello에 대 한 사용 TRIM의 프리미엄 디스크에?**

사용 되지 않지만 단점은 toohello TRIM Azure 디스크를 프리미엄 또는 표준 디스크에 있습니다.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>새 디스크 크기: 관리 및 관리되지 않는 디스크

**Hello 운영 체제 및 데이터 디스크에 대해 지원 되는 가장 큰 디스크 크기는 무엇입니까?**

운영 체제 디스크에 대 한 Azure 지원 hello 파티션 유형은 hello 마스터 부트 레코드 (MBR)입니다. hello MBR 형식은 too2 TB 디스크 크기를 지원합니다. 운영 체제 디스크에 대 한 Azure 지원 있는 hello 최대 크기는 2TB입니다. Azure는 데이터 디스크에 대 한 too4 TB를 지원합니다. 

**Hello 가장 큰 페이지 blob 크기 지원 되는 무엇입니까?**

hello 가장 큰 페이지 blob 크기는 Azure 지원은 8TB (8,191 GB)입니다. 데이터 또는 운영 체제 디스크 4TB (4, 095mb GB) 연결 된 tooa VM 보다 큰 페이지 blob 지원 되지 않습니다.

**필요한 toouse 새 버전의 Azure tools toocreate 연결, 크기 조정 및 1TB 보다 큰 디스크를 업로드?**

기존 Azure tools toocreate 프로그램 tooupgrade 필요 하지 않습니다, 연결, 또는 1TB 보다 큰 디스크의 크기를 조정 합니다. 파일을 VHD tooupload 온-프레미스 직접 tooAzure 페이지 blob 또는 관리 되지 않는 디스크, toouse hello 최신 도구 집합을 필요:

|Azure 도구      | 지원되는 버전                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | 버전 번호 4.1.0: 2017년 6월 릴리스 이상|
|Azure CLI v1     | 버전 번호 0.10.13: 2017년 5월 릴리스 이상|
|AzCopy           | 버전 번호 6.1.0: 2017년 6월 릴리스 이상|

Azure CLI v2 및 Azure 저장소 탐색기에 대 한 hello 지원이 곧 제공 됩니다. 

**P4 및 P6 디스크 크기가 관리되지 않는 디스크 또는 페이지 Blob에 지원되나요?**

아니요. P4(32GB) 및 P6(64GB) 디스크 크기는 Managed Disks에만 지원됩니다. 관리되지 않는 디스크 및 페이지 Blob에도 곧 지원됩니다.

**관리 되는 기존 내 프리미엄 디스크 64GB hello 작은 디스크 (주위 2017 년 6 월 15) 사용 하기 전에 만들어진 보다 작은 경우 어떻게 것 청구?**

64 GB 보다 작은 기존 작은 프리미엄 디스크에 따라 요금이 청구 toobe toohello P10 가격 책정 계층을 계속합니다. 

**P10 tooP4 또는 P6에서 64GB 미만인 작은 프리미엄 디스크의 디스크 계층 hello를 전환 하려면 어떻게 해야 합니까?**

작은 디스크의 스냅숏을 하 고 가격 계층 tooP4는 디스크 tooautomatically 스위치 hello를 만들 수 있습니다 또는 사용자를 프로 비전 하는 hello 크기에 따라 P6 합니다. 


## <a name="what-if-my-question-isnt-answered-here"></a>여기서 내 질문에 대답하지 않으면 어떻게 하나요?

질문하려는 내용이 아래 목록에 나와 있지 않으면 알려 주세요. 대답을 확인하는 방법을 알려 드리겠습니다. Hello 주석에서이 문서의 끝 hello에 질문을 게시할 수 있습니다. tooengage hello Azure 저장소 팀 및 다른 커뮤니티 구성원 들이 문서에 대 한 MSDN hello를 사용 하 여 [Azure 저장소 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)합니다.

toorequest 기능 요청 및 아이디어 toohello 제출 [Azure 저장소 피드백 포럼](https://feedback.azure.com/forums/217298-storage)합니다.
