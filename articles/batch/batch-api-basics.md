---
title: "개발자를 위한 Azure 일괄 처리의 aaaOverview | Microsoft Docs"
description: "Hello 일괄 처리 서비스와 해당 Api 개발 측면에서는 hello 기능에 알아봅니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Batch를 사용하여 대규모 병렬 계산 솔루션 개발

Hello Azure 배치 서비스의 hello 핵심 구성 요소인이 개요에서는 hello 기본 서비스 기능을 설명할 및 리소스 배치 개발자의 toobuild 대규모 병렬 사용 하 여 솔루션을 계산 합니다.

분산된 컴퓨팅 응용 프로그램을 개발 하는 또는 서비스에 직접 발급 [REST API] [ batch_rest_api] hello 중 하나를 호출 하거나 사용 중인 [일괄 처리 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development)를 사용 하 여 대부분의 hello 리소스와이 문서에서 설명 하는 기능.

> [!TIP]
> 더 높은 수준의 소개 toohello 일괄 처리 서비스를 참조 하십시오. [Azure 배치 기본 사항](batch-technical-overview.md)합니다.
>
>

## <a name="batch-service-workflow"></a>Batch 서비스 워크플로
hello 다음과 같은 개략적인 워크플로 거의 모든 응용 프로그램 및 병렬 작업을 처리 하기 위한 hello 일괄 처리 서비스를 사용 하는 서비스의 일반적인.

1. Hello 업로드 **데이터 파일** tooprocess tooan 원하는 [Azure 저장소] [ azure_storage] 계정. 일괄 처리에서는 Azure Blob 저장소에 액세스 하기 위해 기본적으로 지원 하 고 작업 너무 이러한 파일을 다운로드할 수[계산 노드](#compute-node) hello는 태스크는 실행 합니다.
2. Hello 업로드 **응용 프로그램 파일** 하 여 작업을 실행 합니다. 이러한 파일 이진 또는 스크립트와 해당 종속성 수 있으며 작업의 hello 작업으로 실행 됩니다. 작업 저장소 계정에서 이러한 파일을 다운로드할 수 있습니다 또는 hello를 사용할 수 있습니다 [응용 프로그램 패키지](#application-packages) 응용 프로그램 관리 및 배포에 대 한 일괄 처리의 기능입니다.
3. 계산 노드 [풀](#pool)을 만듭니다. 풀을 만들 때 hello hello 풀, 크기 및 hello 운영 체제에 대 한 계산 노드 수를 지정 합니다. 작업에서 각 태스크를 실행 하는 경우 할당 된 풀의 hello 노드 중 하나에서 tooexecute 합니다.
4. [작업](#job)을 만듭니다. 작업에서는 태스크의 컬렉션을 관리합니다. 해당 작업의 작업을 실행 하는 여기서 각 작업 tooa 특정 풀을 연결 합니다.
5. 추가 [작업](#task) toohello 작업 합니다. 각 작업 hello 응용 프로그램 또는 저장소 계정에서 다운로드 tooprocess hello 데이터 파일을 업로드 하는 스크립트를 실행 합니다. 각 작업이 완료 되는 대로 해당 출력 tooAzure 저장소 업로드할 수 있습니다.
6. 작업 진행 상황을 모니터링 하 고 Azure 저장소에서 hello 작업 출력을 검색 합니다.

hello 다음 섹션에서는 대해 고 hello 분산된 컴퓨팅 시나리오를 사용할 수 있는 일괄 처리의 다른 리소스.

> [!NOTE]
> 필요한는 [일괄 처리 계정을](#account) toouse hello 일괄 처리 서비스. 대부분의 Batch 솔루션에서는 파일 저장 및 검색을 위해 [Azure Storage][azure_storage] 계정을 사용합니다. 현재 일괄 처리를 지원만 hello **범용** 의 5 단계에서 설명 된 대로 저장소 계정 유형을 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 에 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.
>
>

## <a name="batch-service-resources"></a>Batch 서비스 리소스
Hello 리소스--계정, 다음 중 일부는 hello 일괄 처리 서비스를 사용 하는 모든 솔루션에 필요한 노드, 풀, 작업 및 작업을 계산 합니다. 작업 일정, 응용 프로그램 패키지 등의 기타 리소스는 유용하기는 하지만 선택적 기능입니다.

* [계정](#account)
* [Compute 노드](#compute-node)
* [풀](#pool)
* [작업](#job)

  * [작업 일정](#scheduled-jobs)
* [Task](#task)

  * [시작 태스크](#start-task)
  * [작업 관리자 태스크](#job-manager-task)
  * [작업 준비 및 해제 태스크](#job-preparation-and-release-tasks)
  * [MPI(다중 인스턴스 태스크)](#multi-instance-tasks)
  * [작업 종속성](#task-dependencies)
* [응용 프로그램 패키지](#application-packages)

## <a name="account"></a>계정
일괄 처리 계정은 hello 일괄 처리 서비스 내에서 고유 하 게 식별 된 엔터티입니다. 모든 처리는 Batch 계정과 연결됩니다.

Hello를 사용 하 여 Azure 배치 계정을 만들 수 있습니다 [Azure 포털](batch-account-create-portal.md) 또는 프로그래밍 방식으로와 같이 hello로 [Batch Management.NET 라이브러리](batch-management-dotnet.md)합니다. Hello 계정을 만들 때 Azure 저장소 계정을 연결할 수 있습니다.

### <a name="pool-allocation-mode"></a>풀 할당 모드

Batch 계정을 만들 때 계산 노드의 [풀](#pool)이 할당되는 방식을 지정할 수 있습니다. Azure 일괄 처리에 의해 관리 되는 구독에서 계산 노드 tooallocate 풀을 선택할 수 있습니다 또는 사용자의 구독에 할당할 수 있습니다. hello *풀 할당 모드* hello 계정에 대 한 속성 풀 할당 되는 위치를 결정 합니다. 

toodecide 할당 모드 toouse 풀 있는 시나리오에 가장 잘 맞는 고려해 야 합니다.

* **서비스 배치**: 일괄 처리 서비스는 hello 기본 풀 할당 모드는 풀 hello 백그라운드 Azure에서 관리 하는 구독에 할당 됩니다. Hello 일괄 처리 서비스가 풀 할당 모드에 대 한 핵심 이러한 사항에 유의 하십시오.

    - hello 일괄 처리 서비스가 풀 할당 모드는 클라우드 서비스와 가상 컴퓨터를 모두 풀을 지원합니다.
    - hello 일괄 처리 서비스가 풀 할당 모드는 지원 모두 공유 키 인증 또는 [Azure Active Directory 인증](batch-aad-auth.md) (Azure AD). 
    - Hello 일괄 처리 서비스가 풀 할당 모드를 사용 하 여 할당 된 풀의 전용 또는 우선 순위가 낮은 계산 노드 중 하나를 사용할 수 있습니다.
    - 사용자 지정 VM 이미지에서 Azure 가상 컴퓨터 풀을 toocreate 계획 이거나 toouse 가상 네트워크를 계획 하는 경우에 hello 일괄 처리 서비스가 풀 할당 모드를 사용 하지 마십시오. 대신 hello 사용자 구독 풀 할당 모드 계정을 만듭니다.
    - Hello 일괄 처리 서비스가 풀 할당 모드를 사용 하 여 만든 계정에서 사용자를 프로 비전 하는 가상 컴퓨터 풀에서 작성 해야 [Azure 가상 컴퓨터 마켓플레이스] [ vm_marketplace] 이미지입니다.

* **사용자 구독**: hello 사용자 구독 풀 할당 모드에서 일괄 처리 풀 hello hello 계정이 생성 되는 Azure 구독에에서 할당 됩니다. Hello 사용자 구독 풀 할당 모드에 대 한 핵심 이러한 사항에 유의 하십시오.
     
    - hello 사용자 구독 풀 할당 모드에는 가상 컴퓨터 풀만 지원합니다. Cloud Services 풀은 지원하지 않습니다.
    - 사용자 지정 VM 이미지 또는 toouse 가상 네트워크에서 가상 컴퓨터 풀 toocreate을 가상 컴퓨터 풀과, hello 사용자 구독 풀 할당 모드를 사용 해야 합니다.  
    - 사용 해야 [Azure Active Directory 인증](batch-aad-auth.md) hello 사용자 구독에 할당 되는 풀과 합니다. 
    - Hello 풀 할당 모드가 tooUser 구독 설정 된 경우에 일괄 처리 계정에는 Azure 키 자격 증명 모음을 설정 해야 합니다. 
    - Hello 사용자 구독 풀 할당 모드를 사용 하 여 만든 계정에서 풀에만 전용된 계산 노드를 사용할 수 있습니다. 우선 순위가 낮은 노드는 지원되지 않습니다.
    - 들어오거나 hello 사용자 구독 풀 할당 모드를 가진 계정에서 사용자를 프로 비전 하는 가상 컴퓨터 풀을 만들 수 있습니다 [Azure 가상 컴퓨터 마켓플레이스] [ vm_marketplace] 이미지, 또는 이미지를 사용자 지정 이 옵션을 제공 합니다.

다음 표에서 hello hello 일괄 처리 서비스 및 사용자 구독 풀 할당 모드를 비교 합니다.

| **풀 할당 모드**                 | **Batch 서비스**                                                                                       | **사용자 구독**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **다음에 풀이 할당됨**               | Azure에서 관리하는 구독                                                                           | hello 사용자 구독 계정을 만든 일괄 처리는 hello에                        |
| **지원되는 구성**             | <ul><li>클라우드 서비스 구성</li><li>가상 컴퓨터 구성(Linux 및 Windows)</li></ul> | <ul><li>가상 컴퓨터 구성(Linux 및 Windows)</li></ul>                |
| **지원되는 VM 이미지**                  | <ul><li>Azure Marketplace 이미지</li></ul>                                                              | <ul><li>Azure Marketplace 이미지</li><li>사용자 지정 이미지</li></ul>                   |
| **지원되는 계산 노드 형식**         | <ul><li>전용 노드</li><li>우선 순위가 낮은 노드</li></ul>                                            | <ul><li>전용 노드</li></ul>                                                  |
| **지원되는 인증**             | <ul><li>공유 키</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault 필요**             | 아니요                                                                                                      | 예                                                                                |
| **코어 할당량**                           | Batch 코어 할당량에 의해 결정됨                                                                          | 구독 코어 할당량에 의해 결정됨                                              |
| **Azure Vnet(Virtual Network) 지원** | 클라우드 서비스 구성 hello를 사용 하 여 만든 풀                                                      | 가상 컴퓨터 구성 hello를 사용 하 여 만든 풀                               |
| **Vnet 배포 모델 지원됨**      | 클래식 배포 모델을 사용하여 만든 Vnet                                                             | Hello 클래식 배포 모델 또는 Azure 리소스 관리자를 사용 하 여 만든 Vnet |

## <a name="azure-storage-account"></a>Azure Storage 계정

대부분의 Batch 솔루션은 리소스 파일 및 출력 파일을 저장하기 위해 Azure Storage를 사용합니다.  

5 단계에서 설명 된 대로 현재 일괄 처리만 hello 범용 저장소 계정 유형은 지원 [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md#create-a-storage-account) 에 [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다. Batch 태스크(표준 태스크, 시작 태스크, 작업 준비 태스크 및 작업 릴리스 태스크 포함)은 범용 저장소 계정에서 상주하는 리소스 파일을 지정해야 합니다.


## <a name="compute-node"></a>Compute 노드
계산 노드는 Azure 가상 컴퓨터 (VM) 또는 클라우드 서비스 VM 전용된 tooprocessing 응용 프로그램의 작업 부하의 일부입니다. 노드의 hello 크기 hello CPU 코어 수, 메모리 용량 및 toohello 노드에 할당 되는 로컬 파일 시스템 크기를 결정 합니다. Azure 클라우드 서비스를 hello에서 이미지를 사용 하 여 Windows 또는 Linux 노드 풀을 만들 수 있습니다 [Azure 가상 컴퓨터 마켓플레이스][vm_marketplace], 또는 사용자 지정 이미지를 준비 합니다. Hello 다음을 참조 [풀](#pool) 이러한 옵션에 대 한 자세한 내용은 섹션.

노드 실행 파일 또는 hello 노드의 hello 운영 체제 환경에서 지원 되는 스크립트를 실행할 수 있습니다. 여기에 Windows용 \*.exe, \*.cmd, \*.bat 및 PowerShell 스크립트, Linux용 이진 파일, 셸 및 Python 스크립트를 포함합니다.

Batch의 모든 계산 노드는 다음 사항도 포함합니다.

* 태스크에서 참조로 사용할 수 있는 표준 [폴더 구조](#files-and-directories) 및 연결된 [환경 변수](#environment-settings-for-tasks)
* **방화벽** 된 설정을 toocontrol 액세스를 구성 합니다.
* [원격 액세스](#connecting-to-compute-nodes) tooboth (프로토콜 RDP (원격 데스크톱)) Windows 및 Linux (SSH (보안 셸)) 노드.

## <a name="pool"></a>풀
풀은 응용 프로그램이 실행되는 노드 컬렉션입니다. hello 풀 만들 수 있습니다 수동으로 또는 자동으로 일괄 처리 서비스 hello가, 수행 하는 hello 작업 toobe를 지정 하는 경우. 만들 수 있으며 응용 프로그램의 hello 리소스 요구 사항을 충족 하는 풀 관리. 생성 된 hello 일괄 처리 계정에 의해서만 풀을 사용할 수 있습니다. 하나의 Batch 계정에는 둘 이상의 풀이 있을 수 있습니다.

Azure 배치 풀 기반 hello 핵심 Azure 계산 플랫폼을 활용 합니다. 대규모 할당, 응용 프로그램 설치, 데이터 분산, 상태 모니터링 및 유연한 조정 hello 풀 내에서 계산 노드 수를 제공 ([배율](#scaling-compute-resources)).

Tooa 풀 추가 된 모든 노드에 고유 이름 및 IP 주소 할당 됩니다. 노드는 풀에서 제거 되 면 toohello 운영 체제 또는 파일이 적용 된 모든 변경 내용이 손실, 하 고 이름 및 IP 주소는 나중에 사용할 해제 됩니다. 노드가 풀에서 제거되면 수명이 끝납니다.

풀을 만들 때 hello 다음 특성을 지정할 수 있습니다. Hello 일괄 처리의 hello 풀 할당 모드에 따라 일부 설정이 다르면 [계정](#account):

- Compute 노드 운영 체제 및 버전
- Compute 노드 유형 및 대상 노드 수
- Hello 계산 노드의 크기
- 크기 조정 정책
- 태스크 예약 정책
- 계산 노드의 통신 상태
- 계산 노드의 시작 태스크
- 응용 프로그램 패키지
- 네트워크 구성

이러한 각 설정의 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.

> [!IMPORTANT]
> Hello 일괄 처리 서비스가 풀 할당 모드를 사용 하 여 만든 일괄 처리 계정 hello 일괄 처리 계정에는 코어 수를 제한 하는 기본 할당량이 있어야 합니다. 코어 수가 hello toohello 계산 노드 수를 해당합니다. 찾을 수 있습니다 hello 기본 할당량 및 지침은 방법 너무[는 할당량을 늘리세요](batch-quota-limit.md#increase-a-quota) 에 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다. 풀의 대상 노드 수가 달성은, hello 코어 할당량 hello 이유를 수 있습니다.
>
>일괄 처리 계정 hello 사용자 구독 풀 할당 모드를 사용 하 여 만든 hello 일괄 처리 서비스 할당량을 지원 하지 않습니다. Hello에 공유 대신 코어 할당량 hello에 대 한 구독을 지정 합니다. 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 [Virtual Machines 제한](../azure-subscription-service-limits.md#virtual-machines-limits)을 참조하세요.
>
>

### <a name="compute-node-operating-system-and-version"></a>Compute 노드 운영 체제 및 버전

일괄 처리 풀을 만들 때 hello Azure 가상 컴퓨터 구성 및 운영 체제 hello 풀의 각 계산 노드에서 toorun 원하는의 hello 유형을 지정할 수 있습니다. hello 두 일괄 처리에서 사용할 수 있는 구성 유형은 다음과 같습니다.

- hello **가상 컴퓨터 구성**, 해당 hello 풀을 지정 하는 Azure 가상 컴퓨터 구성 됩니다. 이러한 VM은 Linux 또는 Windows 이미지에서 만들 수 있습니다. 

    Hello 가상 컴퓨터 구성에 따라 풀을 만들 때 지정 해야 hello 사용 되는 이미지 toocreate의 hello 원본과 hello 노드의 hello 크기 뿐만 아니라, 뿐만 아니라 hello **가상 컴퓨터 이미지 참조** 및 hello 일괄 처리 **노드 에이전트 SKU** toobe hello 노드에 설치 합니다. 이러한 풀 속성에 대한 자세한 내용은 [Azure Batch 풀에서 Linux 계산 노드 프로비전](batch-linux-nodes.md)을 참조하세요.

- hello **클라우드 서비스 구성**, 해당 hello 풀을 지정 하는 Azure 클라우드 서비스 노드 구성 됩니다. Cloud Services는 Windows 계산 노드*만* 제공합니다.

    클라우드 서비스 구성 풀에 대 한 사용 가능한 운영 체제 hello에 나열 된 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](../cloud-services/cloud-services-guestos-update-matrix.md)합니다. Toospecify hello 노드 크기 해야 클라우드 서비스 노드를 포함 하는 풀을 만들 때와 해당 *OS 제품군*합니다. 클라우드 서비스는 Windows를 실행 중인 가상 컴퓨터 보다 신속 하 게 배포 된 tooAzure는. Windows 계산 노드 풀을 원하는 경우 배포 시간 측면에서 Cloud Services가 성능 상의 이점을 제공할 수 있습니다.

    * hello *OS 제품군* 또한 hello OS로 설치 된.net 버전을 결정 합니다.
    * 클라우드 서비스 내에서 작업자 역할로 지정할 수는 *OS 버전* (작업자 역할에 대 한 자세한 내용은 참조 hello [사람에 게 클라우드 서비스에 대 한](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) hello에 대 한 섹션 [클라우드 서비스 개요](../cloud-services/cloud-services-choose-me.md)).
    * 작업자 역할을 갖는 지정 하는 권장 한 대로 `*` hello에 대 한 *OS 버전* hello 노드는 자동으로 업그레이드 하 고 없는 필요한 작업 toocater toonewly 릴리스된 버전은 있도록 합니다. 특정 운영 체제 버전을 선택 하기 위한 기본 사용 사례 hello 이전 버전과 호환성 테스트 toobe hello 버전 toobe 업데이트를 허용 하기 전에 수행할 수 있는 tooensure 응용 프로그램 호환성입니다. 유효성 검사 후 hello *OS 버전* 실행 중인 모든 작업이 중단 되며 다시 대기 hello 새 OS 이미지를 설치할 수 있습니다-및 hello 풀을 업데이트할 수 있습니다.

풀을 만들 때 필요한 tooselect hello 적절 한 **nodeAgentSkuId**hello 기본 VHD 이미지의 OS hello에 따라 합니다. Hello를 호출 하 여 OS 이미지 참조를 사용할 수 있는 노드 에이전트 SKU ID tootheir의 매핑을 얻을 수 [목록 지원 노드 에이전트 Sku](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) 작업 합니다.

Hello 참조 [계정](#account) 일괄 처리 계정을 만들 때 hello 풀 할당 모드 설정에 대 한 내용은 섹션입니다.

#### <a name="custom-images-for-virtual-machine-pools"></a>가상 컴퓨터 풀에 대한 사용자 지정 이미지

toouse 사용자 지정 이미지 tooprovision 가상 컴퓨터 풀 hello 사용자 구독 풀 할당 모드 일괄 처리 계정을 만듭니다. 이 모드에서 일괄 처리 풀 hello 계정이 있는 hello 구독에 할당 됩니다. Hello 참조 [계정](#account) 일괄 처리 계정을 만들 때 hello 풀 할당 모드 설정에 대 한 내용은 섹션입니다.

사용자 지정 이미지 toouse 간에 일반화 하 여 tooprepare hello 이미지가 필요 합니다. Azure Vm에서 사용자 지정 Linux 이미지를 준비 하는 방법에 대 한 정보를 참조 하십시오. [템플릿으로 Azure Linux VM toouse 캡처](../virtual-machines/linux/capture-image-nodejs.md)합니다. Azure VM에서 사용자 지정 Windows 이미지 준비에 대한 자세한 내용은 [Azure PowerShell을 사용하여 사용자 지정 VM 이미지 만들기](../virtual-machines/windows/tutorial-custom-images.md)를 참조하세요. 

> [!IMPORTANT]
> 사용자 지정 이미지를 준비할 때는 유의 hello 다음에 유의 하십시오.
> - 일괄 처리 풀 않습니다 tooprovision를 사용 하 여 해당 hello 기본 OS 이미지를 확인 하지는 모든 사전 설치 된 hello 사용자 지정 스크립트 확장 등의 Azure 확장입니다. 사전 설치 된 확장을 포함 하는 hello 이미지를 Azure hello VM을 배포 하는 문제가 발생할 수 있습니다.
> - 제공한 사용 하 여 기본 임시 드라이브 hello hello 배치 노드 에이전트 현재에서는 hello 기본 임시 드라이브 처럼 해당 hello 기본 OS 이미지를 확인 합니다.
>
>

사용자 지정 이미지를 사용 하 여 가상 컴퓨터 구성 풀 toocreate 해야 하나 이상의 표준 Azure 저장소 계정 toostore 사용자 지정 VHD 이미지 하거나. 사용자 지정 이미지는 Blob으로 저장됩니다. hello hello에 대 한 hello 사용자 지정 이미지 VHD blob의 Uri를 지정 하는 풀을 만들 때 사용자 지정 이미지 tooreference [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) hello 속성 [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) 속성.

저장소 계정 hello 다음 조건을 충족 하는지 확인 합니다.   

- hello 저장소 계정을 포함 하는 hello 사용자 지정 이미지 VHD blob에서 toobe 필요한 일괄 처리 계정 (hello 사용자 구독) hello으로 동일한 구독을 hello 합니다.
- hello hello에 toobe 해야 하는 저장소 계정이 지정 된 일괄 처리 계정 hello와 동일한 영역입니다.
- 현재 표준 범용 저장소 계정만 지원됩니다. Azure 프리미엄 저장소는 hello 나중에 지원 됩니다.
- 사용자 지정 VHD Blob이 여러 개 있는 단일 저장소 계정을 지정하거나 Blob 하나만 있는 저장소 계정을 여러 개 지정할 수 있습니다. Toouse 권장 여러 저장소 계정 tooget 성능이 향상 됩니다.
- 고유한 사용자 지정 이미지 VHD blob 하나 too40 Linux VM 인스턴스 또는 Windows VM 인스턴스를 20 개를 지원할 수 있습니다. 많은 수의 Vm 인 hello VHD blob toocreate 풀의 toocreate 복사본이 필요 합니다. 예를 들어, 200 Windows Vm을 사용 하 여 풀 필요 hello에 대 한 지정 된 10 개의 고유한 VHD blob **osDisk** 속성입니다.

toocreate hello Azure 포털을 사용 하 여 사용자 지정 이미지에서 풀:

1. Hello Azure 포털에서에서 tooyour 일괄 처리 계정을 이동 합니다.
2. Hello에 **설정** 블레이드, 선택 hello **풀** 메뉴 항목입니다.
3. Hello에 **풀** 블레이드, 선택 hello **추가** 명령; hello **풀 추가** 블레이드를 표시 됩니다.
4. 선택 **사용자 지정 이미지 (Linux/Windows)** hello에서 **이미지 유형** 드롭다운입니다. hello를 표시 하는 hello 포털 **사용자 지정 이미지** 선택 합니다. Hello에서 하나 이상의 Vhd를 선택 합니다. 동일한 컨테이너와 클릭 hello **선택** 단추입니다. 
    Hello 나중에 다른 저장소 계정 및 다른 컨테이너에서 여러 Vhd에 대 한 지원이 추가 됩니다.
5. 올바른 선택 hello **게시자/제품/Sku** hello 원하는 사용자 지정 Vhd를 선택 **캐싱** 모드에서는 다음 모든 페이지에서 채우기 hello hello 풀에 대 한 다른 매개 변수입니다.
6. toocheck 풀을 기반으로 이미지를 사용자 지정 하는 경우 참조 hello **운영 체제** hello의 hello 리소스 요약 섹션에서 속성 **풀** 블레이드입니다. 이 속성의 hello 값은 **사용자 지정 VM 이미지**합니다.
7. 풀에 연결 된 모든 사용자 지정 Vhd hello 풀에 표시 되는 **속성** 블레이드입니다.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Compute 노드 유형 및 대상 노드 수

풀을 만들 때 어떤 유형의 계산 노드 및 대상 수를 각각에 대해 hello를 지정할 수 있습니다. hello 두 계산 노드 유형은 다음과 같습니다.

- **전용 계산 노드.** 전용 계산 노드는 사용자 워크로드용으로 예약되어 있습니다. 보다 우선 순위가 낮은 노드는 하지만 보장 됩니다 toonever 선점 될 합니다.

- **우선 순위가 낮은 계산 노드.** 우선 순위가 낮은 노드 과도 한 용량에서에서 활용 Azure toorun 일괄 처리 작업 합니다. 우선 순위가 낮은 노드는 전용 노드보다 시간당 비용이 더 적게 들며, 많은 계산 성능이 필요한 워크로드를 사용할 수 있습니다. 자세한 내용은 [Batch에서 우선 순위가 낮은 VM 사용](batch-low-pri-vms.md)을 참조하세요.

    Azure에 여유 용량이 부족하면 우선 순위가 낮은 계산 노드는 선취될 수 있습니다. 노드는 작업을 실행 하는 동안 우선 되 면 hello 작업 다시 대기 되며 계산 노드를 다시 사용할 수 있게 되 면 다시 실행 됩니다. 우선 순위가 낮은 노드는 작업은 유연 hello 작업 완료 시간 및 hello 작업은 여러 노드에 분산에 적합 한 옵션입니다. 시나리오에 맞는 toouse 우선 순위가 낮은 노드를 결정 하기 전에 모든 작업 인해 분실 하 있는지 확인 toopreemption 최소이 고 쉬운 toorecreate 됩니다.

    도 hello 풀 할당 모드를 사용 하 여 만든 일괄 처리 계정에 대해서만 사용할 수 있는 우선 순위가 낮은 계산 노드가**일괄 처리 서비스**합니다.

Hello에 모두 우선 순위가 낮은 토폴로지와 전용 계산 노드를 가질 수 동일한 풀입니다. 각 유형의 노드에 &mdash; 우선 순위가 낮은 토폴로지와 전용 &mdash; 가 필요한 hello 노드 수를 지정할 수는 자체 대상 설정 합니다. 
    
hello 계산 노드 수는 참조 된 tooas는 *대상* 하므로 하면 풀에 따라서는 hello 필요한 노드 수에 도달 하지 수도 있습니다. 예를 들어, 풀을 얻지 못할 수도 hello 대상 hello에 도달한 경우 [코어 할당량](batch-quota-limit.md) 먼저 일괄 처리 계정. 자동 크기 조정 적용 한 경우 hello 풀 hello 대상을 얻지 못할 수도 또는 hello 최대 노드 수를 제한 하는 수식 toohello 풀입니다.

우선 순위가 낮은 계산 노드 및 전용 계산 노드에 대한 가격 정보는 [Batch 가격 책정](https://azure.microsoft.com/pricing/details/batch/)을 참조하세요.

### <a name="size-of-hello-compute-nodes"></a>Hello 계산 노드의 크기

**Cloud Services 구성** 계산 노드 크기는 [Cloud Services 크기](../cloud-services/cloud-services-sizes-specs.md)에 나열됩니다. Batch는 `ExtraSmall`, `STANDARD_A1_V2` 및 `STANDARD_A2_V2`를 제외한 모든 Cloud Services 크기를 지원합니다.

**가상 컴퓨터 구성** 계산 노드 크기는 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/linux/sizes.md)(Linux) 및 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/windows/sizes.md)(Windows)에 나열되어 있습니다. Batch는 `STANDARD_A0`및 프리미엄 저장소(`STANDARD_GS`, `STANDARD_DS` 및 `STANDARD_DSV2` 시리즈) 크기를 제외한 모든 Azure VM 크기를 지원합니다.

계산 노드 크기를 선택할 때는 hello 특징 및 hello 노드에서 실행 하는 hello 응용 프로그램의 요구 사항을 고려 합니다. Hello 응용 프로그램은 다중 스레드 및 메모리 소비 양을 도와 같은 측면 hello 가장 적합 하 고 비용 효율적인 노드 크기를 결정 합니다. 것이 일반적인 tooselect 하나 이상의 태스크를 가정 합니다. 노드 크기는 한 번에 한 노드에서 실행 됩니다. 그러나 가능한 toohave는 여러 작업 (및 따라서 여러 응용 프로그램 인스턴스가) [병렬로 실행](batch-parallel-node-tasks.md) 작업 실행 중에 계산 노드. 이 경우 일반적인 toochoose 큰 노드 크기 tooaccommodate hello 증가 요청을 병렬 작업 실행 됩니다. 자세한 내용은 [태스크 일정 정책](#task-scheduling-policy)을 참조하세요.

풀의 hello 노드 모두에 동일한 hello 크기입니다. 시스템 요구 사항이 서로 다른 toorun 응용 프로그램 의도 및/또는 한다고 로드 수준, 하는 경우에 별도 풀을 사용 하는 것이 좋습니다.

### <a name="scaling-policy"></a>크기 조정 정책

동적 작업에 대 한 작성 및 적용할 수 있습니다는 [자동 크기 조정 수식](#scaling-compute-resources) tooa 풀입니다. hello 일괄 처리 서비스는 주기적으로 수식이 평가 하 고 hello 다양 한 풀, 작업 및 지정할 수 있는 작업 매개 변수를 기반으로 하는 hello 풀 내의 노드 수를 조정 합니다.

### <a name="task-scheduling-policy"></a>태스크 예약 정책

hello [작업 노드당 최대](batch-parallel-node-tasks.md) 구성 옵션 hello hello 풀 내에서 각 계산 노드에서 동시에 실행할 수 있는 작업의 최대 개수를 결정 합니다.

hello 기본 구성, 노드에서 실행 되는 한 번에 한 작업씩 하지만 시나리오가 toohave 도움이 되는 노드에 동시에 실행 하는 두 개 이상의 작업을 지정 합니다. Hello 참조 [예제 시나리오](batch-parallel-node-tasks.md#example-scenario) hello에 [동시 노드 작업](batch-parallel-node-tasks.md) 문서 toosee 어떻게 노드당 여러 작업을 얻을 수 있습니다.

지정할 수 있습니다는 *채우기 유형* 는 일괄 처리는 풀의 모든 노드에서 hello 작업을 균등 하 게 분산 작업 tooanother 노드를 할당 하기 전에 hello 최대 작업 수와 각 노드를 압축 하는지 여부를 결정 합니다.

### <a name="communication-status-for-compute-nodes"></a>계산 노드의 통신 상태

대부분의 시나리오에서 작업 독립적으로 작동 하 고 서로 toocommunicate 필요는 없습니다. 하지만 [MPI 시나리오](batch-mpi.md)와 같이 태스크가 통신해야 하는 응용 프로그램이 있습니다.

풀 tooallow를 구성할 수 있습니다 **노드 간 통신**, 런타임에 풀 내에서 노드 통신할 수 있도록 합니다. 노드 간 통신 기능을 사용하는 경우 Cloud Services 구성 풀의 노드는 1100보다 큰 포트에서 서로 통신할 수 있고 가상 컴퓨터 구성 풀은 모든 포트에서 트래픽을 제한하지 않습니다.

Note는 노드 간 통신을 사용 하도록 설정도 클러스터 내에서 hello 노드의 hello 배치에 영향을 줍니다 및 배포 제한 사항으로 인해 hello 최대는 풀의 노드 수를 제한할 수 있습니다. 응용 프로그램 노드 간 통신에 필요 하지 않습니다 hello 일괄 처리 서비스 수 잠재적으로 많은 수의 노드가 toohello 풀 서로 다른 여러 클러스터의 할당과 데이터 센터 tooenable 병렬 처리 능력을 증가 합니다.

### <a name="start-tasks-for-compute-nodes"></a>계산 노드의 시작 태스크

선택적 hello *시작 작업* hello 풀을 연결 하는 해당 노드의 및 때마다 노드를 다시 시작 하거나 이미지로 다시 설치 하는 같은 방식으로 각 노드에서 실행 합니다. hello 시작 태스크가 hello hello 계산 노드에서 작업을 실행 하는 hello 응용 프로그램을 설치 하는 등의 작업 실행에 대 한 계산 노드를 준비 하기 위한 특히 유용 합니다.

### <a name="application-packages"></a>응용 프로그램 패키지

지정할 수 있습니다 [응용 프로그램 패키지](#application-packages) toodeploy toohello hello 풀의 노드를 계산 합니다. 응용 프로그램 패키지는 간소화 된 배포 및 작업을 실행 하는 hello 응용 프로그램의 버전 관리를 제공 합니다. 풀에 지정할 응용 프로그램 패키지는 해당 풀에 조인되거나 다시 부팅 또는 이미지로 다시 설치되는 모든 노드에 설치됩니다.

> [!NOTE]
> 응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다. 클라우드 서비스 구성을 사용 하 여 hello 풀이 작성 되었습니다. 경우에 10 2016 년 3 월 사이의 5 년 7 월 2017 생성 되는 일괄 처리 풀에서 사용할 수 있습니다. 2016 년 3 월 이전 too10를 생성 하는 일괄 처리 풀에서 응용 프로그램 패키지를 지원 하지 않습니다. 응용 프로그램 tooyour 일괄 처리 노드 toodeploy 패키지 하는 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 참조 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.
>
>

### <a name="network-configuration"></a>네트워크 구성

Azure의 hello 서브넷을 지정할 수 있습니다 [가상 네트워크 (VNet)](../virtual-network/virtual-networks-overview.md) 는 hello 풀 계산 노드는 만들어야 합니다. Hello 참조 [풀 네트워크 구성](#pool-network-configuration) 한 자세 합니다.


## <a name="job"></a>작업
작업은 태스크의 컬렉션입니다. 풀의 hello 계산 노드에서 해당 작업에 의해 계산 수행 되는 방법을 관리 합니다.

* hello 작업 지정 hello **풀** 는 hello 작업은 toobe 실행 합니다. 각 작업에 새 풀을 만들거나 많은 작업에 하나의 풀을 사용할 수 있습니다. 작업 일정과 연결된 각 작업 또는 작업 일정과 연결된 모든 작업에 풀을 만들 수 있습니다.
* 선택적 **작업 우선 순위**를 지정할 수 있습니다. 작업이 현재 진행 중인 작업 보다 높은 우선 순위로 전송 되 면 hello 우선 순위가 높은 작업에 대 한 hello 작업 hello 우선 순위가 낮은 작업에 대 한 작업 보다 먼저 hello 큐에 삽입 됩니다. 이미 실행 중인 우선 순위가 낮은 작업의 태스크는 선취되지 않습니다.
* 작업을 사용할 수 있습니다 **제약 조건을** toospecify 작업에 대 한 일정 한 제한:

    설정할 수 있습니다는 **최대 wallclock 시간**에 hello 작업 및 작업의 모든 작업은 지정 된 hello 최대 wallclock 시간 보다 오래 실행을 하는 경우 종료 됩니다.

    Batch는 실패한 태스크를 검색하고 다시 시도할 수 있습니다. Hello를 지정할 수 있습니다 **태스크 다시 시도의 최대 수** 작업이 인지 여부를 포함 하는 제약 조건으로 *항상* 또는 *되지* 다시 시도 합니다. 해당 hello 작업은 다시 실행 하는 다시 대기 toobe 의미는 작업을 다시 시도 합니다.
* 클라이언트 응용 프로그램 작업 tooa 작업을 추가 하거나 지정할 수 있습니다는 [작업 관리자 태스크가](#job-manager-task)합니다. 작업 관리자 태스크는 작업에 대 한 필요한 toocreate hello 필요한 작업 사용 되는 hello 정보를 포함 하, hello 중 하나에서 실행 되 고 hello 작업 관리자 태스크와 hello 풀의 노드를 계산 합니다. hello 작업 관리자 태스크는 처리-일괄 처리 전용으로 메시지가 대기 되는 즉시 hello 작업 작성 되 고 실패 한 경우 다시 시작 됩니다. 작업 관리자 태스크는 *필요한* 하 여 만든 작업에 대 한 한 [작업 일정](#scheduled-jobs) hello 작업 인스턴스화되기 전에 hello 유일한 방법은 toodefine hello 작업 이기 때문에 있습니다.
* 기본적으로 작업 hello 작업 내에서 모든 작업이 완료 되 면 hello 활성 상태로 남아 있습니다. Hello 작업이 자동으로 종료 된 hello 작업의 모든 태스크가 완료 되 면 되도록이 동작을 변경할 수 있습니다. 세트 hello 작업 **onAllTasksComplete** 속성 ([OnAllTasksComplete] [ net_onalltaskscomplete] 일괄 처리.net에서) 너무*terminatejob* tooautomatically hello 완료 상태에 해당 작업 모두 있을 때 hello 작업을 종료 합니다.

    Hello 일괄 처리 서비스에서 작업으로 간주 참고 *없는* 작업 toohave 해당 작업 모두 수행 합니다. 따라서 이 옵션은 [작업 관리자 태스크](#job-manager-task)와 함께 가장 일반적으로 사용됩니다. 새 작업을 처음부터 설정 해야 작업 관리자 없이 toouse 작업 자동 종료 하려는 경우 **onAllTasksComplete** 속성 너무*noaction*, 너무 설정한 다음*terminatejob* 작업 toohello 작업 추가 완료 한 후에 합니다.

### <a name="job-priority"></a>작업 우선 순위
일괄 처리에서 만드는 우선 순위 toojobs를 할당할 수 있습니다. hello 일괄 처리 서비스는 계정 내에서 작업 일정의 hello 작업 toodetermine hello 순서 hello 우선 순위 값을 사용 (이 혼동된 toobe는 [예약 된 작업](#scheduled-jobs)). hello 우선 순위 값의 범위는-1000 too1000에서,-1000으로 hello 가장 낮은 우선 순위가 고 1000 hello 최고 합니다. 작업을 호출 hello의 tooupdate hello 우선 순위 [hello는 작업의 속성 업데이트] [ rest_update_job] 작업 (일괄 처리 REST) 또는 hello 수정 [CloudJob.Priority] [ net_cloudjob_priority] 속성 (일괄 처리.NET).

Hello 내에서 동일한 계정으로 우선 순위가 높은 작업에는 우선 순위가 낮은 작업 보다 우선 순위를 예약 합니다. 하나의 계정에서 우선 순위가 더 높은 작업이 다른 계정에서 우선 순위가 더 낮은 다른 작업보다 먼저 예약되는 것은 아닙니다.

풀 간의 예약 작업은 서로 별개입니다. 다양한 풀 사이에서, 연결된 풀에 유휴 노드가 부족한 경우 우선 순위가 높은 작업이 먼저 예약된다고 보장할 수 없습니다. Hello에 동일한 풀 작업 hello로 동일한 우선 순위 수준을 예약 된의 수 있는 같은 기회를 갖게 됩니다.

### <a name="scheduled-jobs"></a>Scheduled jobs
[작업 일정] [ rest_job_schedules] toocreate hello 일괄 처리 서비스 내에서 되풀이 작업을 사용 합니다. 작업 일정 toorun 작업 하 고 hello 작업 toobe 실행에 대 한 hello 사양을 포함 하는 시기를 지정 합니다. 기간 hello 일정-의 hello 기간을 지정할 수 있습니다 및 때 hello 일정-이 고 기간을 예약 된 작업 hello 하는 동안 만들어지는 빈도.

## <a name="task"></a>작업
태스크는 작업과 연결되는 계산의 단위입니다. 노드에서 실행됩니다. 작업 실행을 위한 tooa 노드 할당 되거나 노드에 사용할 수 있게 될 때까지 큐에 대기 됩니다. 간단히 말해서, 작업에서 실행 됩니다 하나 이상의 프로그램 또는 스크립트는 계산 노드 tooperform hello 수행 해야 작업.

태스크를 만들 때 다음을 지정할 수 있습니다.

* hello **명령줄** hello 작업에 대 한 합니다. 이것이 hello 계산 노드에서 응용 프로그램 또는 스크립트를 실행 하는 hello 명령줄입니다.

    명령줄 hello toonote 실제로 shell에서 실행 되지 않도록 유용 합니다. 따라서와 같은 셸 기능을 기본적으로 사용할 수 없습니다 [환경 변수](#environment-settings-for-tasks) 확장 (여기에 hello `PATH`). tootake 이점은 이러한 기능을 호출 해야 hello 명령줄에서 hello 셀에 등을 시작 하 여 `cmd.exe` Windows 노드에서 또는 `/bin/sh` Linux에서:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    응용 프로그램 또는 스크립트에 속하지 않은 노드 hello 작업 필요 toorun `PATH` 환경 변수를 참조 하거나, hello 셸 hello 작업 명령줄에서 명시적으로 호출 합니다.
* **리소스 파일** hello 데이터 toobe 처리를 포함 하는 합니다. 이러한 파일 된 hello 작업의 명령줄 실행 되기 전에 범용 Azure 저장소 계정에서 Blob 저장소에서 자동으로 복사 된 toohello 노드입니다. 자세한 내용은 hello 섹션을 참조 하십시오. [시작 태스크](#start-task) 및 [파일 및 디렉터리](#files-and-directories)합니다.
* hello **환경 변수** 응용 프로그램에 필요 합니다. 자세한 내용은 참조 hello [작업에 대 한 환경 설정을](#environment-settings-for-tasks) 섹션.
* hello **제약 조건** 는 hello 아래의 작업을 실행 해야 합니다. 제약 조건 hello 최대 시간을 포함 하는 예를 들어 hello 작업 toorun, hello 최대 횟수 실패 한 작업을 재시도할 수 있으며 hello 최대 시간 hello 작업의 작업 디렉터리에 파일이 유지 되도록 합니다.
* **응용 프로그램 패키지** toodeploy toohello 계산 노드는 hello 작업은 예약 된 toorun 합니다. [응용 프로그램 패키지](#application-packages) 간소화 된 배포 및 작업을 실행 하는 hello 응용 프로그램의 버전 관리를 제공 합니다. 작업 수준 응용 프로그램 패키지는 다른 작업 한 풀에서 실행 되 고 작업이 완료 되 면 hello 풀 삭제 되지 않습니다 공유 풀 환경에 특히 유용 합니다. 작업에 hello 풀 노드 보다 적은 작업 인 작업 응용 프로그램 패키지 응용 프로그램 작업을 실행 하는 배포 된 유일한 toohello 노드 이므로 데이터 전송을 최소화할 수 있습니다.

또한 tootasks tooperform 계산 노드에서 정의 특별 한 작업을 수행 하는 hello도 제공 hello 일괄 처리 서비스에서:

* [시작 태스크](#start-task)
* [작업 관리자 태스크](#job-manager-task)
* [작업 준비 및 해제 태스크](#job-preparation-and-release-tasks)
* [MPI(다중 인스턴스 태스크)](#multi-instance-tasks)
* [작업 종속성](#task-dependencies)

### <a name="start-task"></a>시작 태스크
연결 하 여 한 **시작 작업** 풀을 사용 하 여 hello 운영 환경 노드를 준비할 수 있습니다. 예를 들어 작업을 실행 하는 hello 응용 프로그램을 설치 하거나 백그라운드 프로세스를 시작 하는 등의 작업을 수행할 수 있습니다. hello 시작 태스크-hello 풀에 남아 있는 기간과 같습니다 toohello 풀 및 다시 시작 하거나 이미지로 다시 설치할 때 추가 먼저 hello 노드는 때를 포함 하 여에 대 한 노드 시작 될 때마다 실행 됩니다.

Hello 시작 작업의 기본 이점은 필요한 tooconfigure 되 hello 정보의 모든 계산 노드를 포함 하 고 작업 실행에 필요한 hello 응용 프로그램을 설치할 수는 있습니다. 따라서 hello 풀의 노드 수를 늘리면 하기만 하면 hello 새 대상 노드 수를 지정 하는 합니다. hello 시작 태스크가 필요한 tooconfigure hello 새 노드를 사용 하도록 준비 작업을 허용 하기 위해 hello 일괄 처리 서비스 hello 정보를 제공 합니다.

모든 Azure 일괄 처리 작업과 목록을 지정할 수와 **리소스 파일** 에 [Azure 저장소][azure_storage], 또한 tooa **명령줄** toobe 실행 됩니다. hello 일괄 처리 서비스 먼저 hello 리소스 파일 toohello 노드 Azure 저장소에서 복사한 다음 hello 명령줄을 실행 합니다. 풀 시작 작업에 대 한 hello 파일 목록 hello 작업 응용 프로그램과 해당 종속성에 일반적으로 포함 됩니다.

그러나 hello 시작 태스크가 hello 계산 노드에서 실행 중인 모든 태스크에서 사용 하는 참조 데이터 toobe를 포함 될 수 있습니다. 예를 들어 시작 작업의 명령줄을 수행할 수는 `robocopy` 작업 toocopy 응용 프로그램 파일 (리소스 파일로 지정 된 및 toohello 노드 다운로드) hello에서 시작 작업의 [작업 디렉터리](#files-and-directories) toohello [공유 폴더](#files-and-directories), 후 MSI를 실행 또는 `setup.exe`합니다.

시작 작업 toocomplete hello에 대 한 일괄 처리 서비스 toowait hello에 대 한 일반적으로 바람직한 hello 노드 준비 toobe 할당 된 작업으로 간주 되기 전에 있지만이 구성할 수 있습니다.

계산 노드에서 시작 태스크가 실패 하면 다음 hello hello 노드의 상태는 업데이트 된 tooreflect hello 실패 및 hello 노드 작업 할당 되지 않았습니다. 시작 태스크의 명령줄에서 실행 된 hello 프로세스 0이 아닌 종료 코드를 반환 하는 경우 또는 저장소에서 해당 리소스 파일을 복사 하는 문제가 있는 경우에 실패할 수 있습니다.

를 추가 하거나 기존 풀에 대 한 hello 시작 작업을 업데이트 하는 경우에 hello 시작 작업 적용 toobe toohello 노드는 계산 노드를 다시 부팅 해야 합니다.

>[!NOTE]
> hello 시작 태스크의 총 크기 해야 보다 작거나 같은 too32768 문자를 리소스 파일 및 환경 변수를 포함 한 합니다. tooensure 시작 작업에이 요구 사항을 충족 하는지, 두 가지 방법 중 하나를 사용할 수 있습니다.
>
> 1. 일괄 처리 풀의 각 노드에서 응용 프로그램 패키지 toodistribute 응용 프로그램이 나 데이터를 사용할 수 있습니다. 응용 프로그램 패키지에 대 한 자세한 내용은 참조 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.
> 2. 응용 프로그램 파일이 포함된 압축 보관 파일을 수동으로 만들 수 있습니다. 압축 된 보관 tooAzure 저장소에 blob으로 업로드 합니다. 시작 작업에 대 한 리소스 파일로 압축 하는 hello 보관 파일을 지정 합니다. 시작 작업에 대 한 hello 명령줄을 실행 하기 전에 hello 명령줄에서 hello 보관을 압축을 풉니다. 
>
>    toounzip hello 보관 hello 보관 선택한 도구를 사용할 수 있습니다. Toounzip hello 아카이브를 사용 하 여 hello 시작 작업에 대 한 리소스 파일로 tooinclude hello 도구가 필요 합니다.
>
>

### <a name="job-manager-task"></a>작업 관리자 태스크
일반적으로 사용 된 **작업 관리자 태스크가** toocontrol 및/또는 모니터 실행--예를 들어 toocreate 작업 및 작업에 대 한 hello 작업 제출, 추가 작업 toorun 확인 및 작업 완료 되는 시점을 결정 합니다. 그러나 작업 관리자 태스크가 제한 toothese 활동 아닙니다. 된 hello 작업에 필요한 모든 작업을 수행할 수 있는 완전 한 작업입니다. 예를 들어 작업 관리자 태스크 수 매개 변수로 지정 된 파일을 다운로드, 그 파일의 hello 내용을 분석 및 해당 내용에 따라 추가 작업을 제출 합니다.

작업 관리자 태스크는 다른 모든 작업이 시작되기 전에 시작됩니다. Hello를 같은 기능을 제공 합니다.

* 자동으로 변수로 제출 된 작업 일괄 처리 서비스 hello 하 여 hello 작업이 만들어질 때.
* 것은 예약 된 tooexecute hello 하기 전에 작업의 다른 작업이 있습니다.
* 연결 된 해당 노드는 hello 마지막 toobe hello 풀 downsized 되는 경우 풀에서 제거 합니다.
* 해당 종료 hello 작업의 모든 작업의 제한은 toohello 종료 될 수 있습니다.
* 작업 관리자 태스크가 toobe 다시 시작 해야 하는 경우 우선 순위가 가장 높은 hello 제공 됩니다. 유휴 노드를 사용할 수 없는 경우 hello 일괄 처리 서비스 종료 될 수 있습니다 하나 hello 작업 관리자 태스크 toorun hello에 대 한 hello 풀 toomake 공간에서 실행 중인 다른 작업입니다.
* 다른 작업의 hello 작업을 통해 하나의 작업에서 작업 관리자 태스크 우선 순위를 않아도 됩니다. 작업 간에는 작업 수준 우선 순위만 준수됩니다.

### <a name="job-preparation-and-release-tasks"></a>작업 준비 및 해제 태스크
Batch는 사전 작업 실행 설치를 위한 작업 준비 태스크를 제공합니다. 작업 릴리스 태스크는 사후 작업 유지 관리 또는 정리를 위한 작업입니다.

* **태스크를 준비 하는 작업**: toorun 예약 된 작업 인 모든 계산 노드에서 작업 준비 작업 실행, 이전 hello에 다른 작업 실행 태스크가 실행 됩니다. 모든 작업에서 공유 하지만 예를 들어 고유 toohello 작업은 작업 준비 작업 toocopy 데이터를 사용할 수 있습니다.
* **작업 그룹 작업**: 작업이 완료 되 면 작업 릴리스 작업이 하나 이상의 작업을 실행 하는 hello 풀의 각 노드에서 실행 되는 것입니다. 예를 들어 hello 작업 준비 작업으로 복사 하는 작업 릴리스 작업 toodelete 데이터 또는 toocompress 및 업로드 진단 로그 데이터를을 사용할 수 있습니다.

준비 작업 둘 다, 릴리스 작업 수 toospecify 명령줄 toorun hello 작업을 호출 하는 경우. 파일 다운로드, 상승된 권한 실행, 사용자 지정 환경 변수, 최대 실행 기간, 재시도 횟수 및 파일 보존 시간 등의 기능을 제공합니다.

작업 준비 및 해제 태스크에 대한 자세한 내용은 [Azure Batch 계산 노드에서 작업 준비 및 완료 태스크 실행](batch-job-prep-release.md)을 참조하세요.

### <a name="multi-instance-task"></a>다중 인스턴스 태스크
A [다중 인스턴스 작업](batch-mpi.md) 동시에 둘 이상의 계산 노드에 대해 구성 된 toorun 되는 작업입니다. 다중 인스턴스 작업을 성능 우선을 사용할 수 있습니다는 계산 노드 그룹을 필요로 하는 컴퓨팅 시나리오 함께 할당 tooprocess 단일 작업 (같은 인터페이스 MPI (Message Passing)).

에 대 한 자세한 내용은 hello 일괄 처리.NET 라이브러리를 사용 하 여 MPI 작업 일괄 처리의 실행을 체크 아웃 [toorun 인터페이스 MPI (Message Passing) 응용 프로그램을 Azure 일괄 처리의 작업을 사용 하 여 다중 인스턴스](batch-mpi.md)합니다.

### <a name="task-dependencies"></a>작업 종속성
[작업 종속성](batch-task-dependencies.md), 이름에서 알 수 hello로, 작업을 실행 하기 전에 다른 작업의 hello 완료에 따라 달라 지는 toospecify를 허용 합니다. 이 기능은 "다운스트림" 태스크는 업스트림 작업 다운스트림 태스크에 필요한 일부 초기화를 수행 하는 경우 또는 "업스트림" 작업-의 hello 출력을 사용 하는 상황에 대 한 지원을 제공 합니다. toouse 일괄 작업에서 첫 번째 사용 작업 종속성을 해야이 기능을 합니다. 다른 종속 된 각 작업에 대 한 다음 (또는 다른 많은), 해당 작업에 따라 달라 지는 hello 작업을 지정 합니다.

작업 종속성이 있는 hello 다음과 같은 시나리오를 구성할 수 있습니다.

* *taskB*가 *taskA*에 종속됨(*taskB*는 *taskA*가 완료될 때까지 실행을 시작하지 않음)
* *taskC*는 *taskA* 및 *taskB*에 종속됨
* *taskD*는 실행하기 전에 태스크 범위(예: 태스크 *1*~*10*)에 종속됨

체크 아웃 [Azure 배치의 종속성 작업](batch-task-dependencies.md) 및 hello [TaskDependencies] [ github_sample_taskdeps] hello에 대 한 코드 샘플 [azure 일괄 처리-샘플] [ github_samples] 깊이 있는 자세한 정보도이 기능에 대 한 GitHub 리포지토리 합니다.

## <a name="environment-settings-for-tasks"></a>태스크에 대한 환경 설정
일괄 처리 서비스 hello로 실행 된 각 작업에는 계산 노드에서 설정 하는 액세스 tooenvironment 변수가 있습니다. 여기에 hello 일괄 처리 서비스에 정의 된 환경 변수 ([서비스 정의][msdn_env_vars]) 및 사용자 정의 환경 변수를 작업에 대해 정의할 수 있습니다. hello 응용 프로그램 및 작업을 실행 하는 스크립트 실행 하는 동안 toothese 환경 변수 액세스 있어야 합니다.

Hello 채워 hello 태스크 또는 작업 수준에서 사용자 정의 환경 변수를 설정할 수 *환경 설정* 이러한 엔터티에 대 한 속성. 예를 들어 hello 참조 [작업 tooa 작업에 추가할] [ rest_add_task] 작업 (배치 REST API) 또는 hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] 및 [ CloudJob.CommonEnvironmentSettings] [ net_job_env] 일괄 처리.net에서 속성입니다.

클라이언트 응용 프로그램 또는 서비스 hello를 사용 하 여 서비스 정의 및 사용자 지정 작업의 환경 변수를 가져올 수 [작업에 대 한 정보를 가져올] [ rest_get_task_info] 작업 (일괄 처리 REST) 또는 액세스 하 여 hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] 속성 (일괄 처리.NET). 이러한 계산 노드에서 실행 중인 프로세스에 액세스할 수 있으며 hello 노드에 대 한 다른 환경 변수를 사용 하 여 hello 친숙 한 `%VARIABLE_NAME%` (Windows) 또는 `$VARIABLE_NAME` (Linux) 구문입니다.

[Compute 노드 환경 변수][msdn_env_vars]에서 모든 서비스 정의 환경 변수의 전체 목록을 찾을 수 있습니다.

## <a name="files-and-directories"></a>파일 및 디렉터리
각 태스크에는 *작업 디렉터리*가 있으며 여기서 0개 이상의 파일 및 디렉터리를 만듭니다. 작업 디렉터리가 hello 작업을 처리 하는 hello 데이터에서 실행 되는 hello 프로그램을 저장 하는 데 사용할 수 및 hello 출력 hello 처리를 수행 합니다. 모든 파일 및 디렉터리 작업의 hello 작업 사용자가 소유 합니다.

hello 일괄 처리 서비스는 hello와 노드에 hello 파일 시스템의 일부를 노출 *루트 디렉터리*합니다. 작업 hello를 참조 하 여 hello 루트 디렉터리에 액세스할 수 `AZ_BATCH_NODE_ROOT_DIR` 환경 변수입니다. 환경 변수 사용에 대한 자세한 내용은 [태스크에 대한 환경 설정](#environment-settings-for-tasks)을 참조하세요.

hello 루트 디렉터리에 디렉터리 구조를 다음 hello를 포함 되어 있습니다.

![Compute 노드 디렉터리 구조][1]

* **공유**:이 디렉터리에서 읽기/쓰기 액세스를 너무 제공*모든* 노드에서 실행 하는 작업입니다. Hello 노드에서 실행 되는 모든 작업 수 만들기, 읽기, 업데이트, 및이 디렉터리의 파일을 삭제 합니다. 작업 hello를 참조 하 여이 디렉터리에 액세스할 수 `AZ_BATCH_NODE_SHARED_DIR` 환경 변수입니다.
* **startup**: 이 디렉터리는 시작 태스크에서 작업 디렉터리로 사용됩니다. 모든 hello 파일을 다운로드 한 toohello 노드 hello 시작 작업은 여기에 저장 됩니다. hello 시작 태스크 수 만들기, 읽기, 업데이트, 및이 디렉터리에 파일을 삭제 합니다. 작업 hello를 참조 하 여이 디렉터리에 액세스할 수 `AZ_BATCH_NODE_STARTUP_DIR` 환경 변수입니다.
* **작업**: hello 노드에서 실행 되는 각 작업에 대 한 디렉터리가 만들어집니다. Hello를 참조 하 여 액세스 하는 것 `AZ_BATCH_TASK_DIR` 환경 변수입니다.

    각 작업 디렉터리 내에서 hello 일괄 처리 서비스는 작업 디렉터리를 만듭니다 (`wd`) hello에 의해 지정 된 해당 고유 경로 `AZ_BATCH_TASK_WORKING_DIR` 환경 변수입니다. 이 디렉터리는 읽기/쓰기 액세스 toohello 작업을 제공합니다. hello 작업 수 만들기, 읽기, 업데이트, 및이 디렉터리에 파일을 삭제 합니다. 이 디렉터리는 hello에 따라 유지 되는 *RetentionTime* hello 작업에 대해 지정 된 제약 조건입니다.

    `stdout.txt`및 `stderr.txt`: 이러한 파일 중 hello 태스크의 실행 hello toohello 작업 폴더에 기록 합니다.

> [!IMPORTANT]
> 노드 hello 풀에서 제거 되 면 *모든* hello의 hello 노드에 저장 된 파일을 제거 됩니다.
>
>

## <a name="application-packages"></a>응용 프로그램 패키지
hello [응용 프로그램 패키지](batch-application-packages.md) 기능을 쉽게 관리 및 응용 프로그램의 배포 toohello 계산 노드가 제공 풀에 있습니다. 업로드 하 고 및가 이진 파일을 포함 하 여 작업을 하 여 여러 버전의 응용 프로그램을 실행 하는 hello 관리 하 고, 지원 파일 수입니다. 다음 자동으로 배포할 수 있습니다 또는 이러한 응용 프로그램 toohello 중 풀의 노드를 계산 합니다.

Hello 풀 및 작업 수준에서 응용 프로그램 패키지를 지정할 수 있습니다. 풀의 응용 프로그램 패키지를 지정 하면 hello 응용 프로그램은 hello 풀에서 배포 된 tooevery 노드입니다. 작업 응용 프로그램 패키지를 지정 하면 hello 응용 프로그램은 배포 된 유일한 toonodes hello 수행 하는 작업의 예약 된 toorun 하나 이상 있는, hello 하기 바로 전에 태스크의 명령줄이 실행 됩니다.

일괄 처리 핸들 hello Azure 저장소 toostore 응용 프로그램 패키지 작업의 세부 정보 및 사용자 코드 및 관리 오버 헤드를 간소화할 수 있도록 toocompute 노드를 배포 합니다.

toofind hello 응용 프로그램 패키지 기능에 대 한 자세한 내용을 확인해 보세요 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.

> [!NOTE]
> 응용 프로그램 패키지 tooan 풀을 추가 하는 경우 *기존* 풀 hello 응용 프로그램 패키지 배포 toobe toohello 노드는 계산 노드를 다시 부팅 해야 합니다.
>
>

## <a name="pool-and-compute-node-lifetime"></a>풀 및 계산 노드 수명
Azure 일괄 처리 솔루션을 디자인할 때 한 toomake 방법에 대 한 디자인을 결정 하며 풀 생성 된 해당 풀 내의 노드 수 있는 상태로 유지 된 시간 계산 됩니다.

Hello 스펙트럼의 한쪽 끝에 제출 하면 각 작업에 대 한 풀을 만들고 작업 실행이 완료 되는 즉시 hello 풀을 삭제 합니다. 이 hello 노드 필요 하 고 자신이 유휴 상태가 되는 즉시 종료 될 때만 할당 되기 때문에 사용률을 최대화 합니다. 즉, hello 작업 기다린 hello 노드 toobe 할당에 대 한 중요 한 toonote 작업 노드를 개별적으로 사용할 수 있는 할당 되는 즉시 실행을 예약 및 hello 하는 동안에 시작 작업이 완료 되었습니다. 일괄 처리는 *하지* toohello 노드 작업을 할당 하기 전에 사용할 수 있는 풀 내 모든 노드가 될 때까지 기다립니다. 이렇게 하면 사용 가능한 모든 노드의 최대 사용률을 보장합니다.

Hello에 hello 스펙트럼의 다른 쪽 끝 즉시 시작 하는 작업은 우선 순위가 가장 높은 hello 경우 미리 풀을 만들 있고 작업 제출 하려면 먼저 해당 노드를 사용할 수 있도록 합니다. 이 시나리오에서는 작업을 즉시 시작 되지만 노드 수 유휴을 기다리는 동안 toobe 할당 합니다.

통합 접근 방식은 일반적으로 가변적이지만 지속적인 부하를 처리하는 데 사용됩니다. 여러 작업에 제출 되어 있지만 toohello 작업 부하에 따라 위아래로 hello 노드 수를 확장할 수는 풀을 사용할 수 있습니다 (참조 [배율 계산 리소스](#scaling-compute-resources) hello 섹션 다음에). 이는 현재 부하에 따라 사후 대응적으로 수행하거나 부하를 예측할 수 있는 경우 사전 대응적으로 수행할 수 있습니다.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>VNet(가상 네트워크) 및 방화벽 구성 

Azure 일괄 처리의 계산 노드는 풀의 프로 비전 할 때 hello 풀을 Azure의 서브넷과 연결할 수 있습니다 [가상 네트워크 (VNet)](../virtual-network/virtual-networks-overview.md)합니다. 서브넷을 사용 하 여 VNet 만들기에 대해 자세히 toolearn 참조 [Azure 가상 네트워크 서브넷 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다. 

 * 풀에 연결 된 VNet hello 해야 합니다.

   * 동일한 Azure hello **지역** hello Azure 배치 계정으로 합니다.
   * 동일한 hello **구독** hello Azure 배치 계정으로 합니다.

* hello 유형의 VNet 지원 hello 일괄 처리 계정에 대 한 풀 할당 방법에 따라 달라 집니다.

    - 일괄 처리 계정에 대 한 hello 풀 할당 모드가 tooBatch 서비스를 설정 된 경우 hello를 사용 하 여 만든 VNet 유일한 toopools를 할당할 수 있습니다 **클라우드 서비스 구성**합니다. 또한 hello 지정 VNet hello 클래식 배포 모델을 만들어야 합니다. Vnet hello Azure 리소스 관리자 배포 모델을 사용 하 여 만든 지원 되지 않습니다.
 
    - 배치 계정에 대 한 hello 풀 할당 모드 tooUser 구독을 설정 되어 있으면 hello를 사용 하 여 만든 VNet 유일한 toopools를 할당할 수 있습니다 **가상 컴퓨터 구성**합니다. Hello를 사용 하 여 만든 풀 **클라우드 서비스 구성** 지원 되지 않습니다. hello hello Azure 리소스 관리자 배포 모델 또는 hello 클래식 배포 모델와 연결 된 VNet을 만들 수 있습니다.

    VNet 지원을 요약 테이블에 대 한 hello 참조 toopool 할당 모드에 따라 [풀 할당 모드](#pool-allocation-mode) 섹션.

* TooBatch 서비스에서 일괄 처리 계정에 대 한 hello 풀 할당 모드가 설정 된 경우 일괄 처리 서비스 보안 주체 tooaccess hello에 대 한 권한을 hello VNet 제공 해야 합니다. hello VNet hello를 할당 해야 [Classic Virtual Machine Contributor Role-Based 액세스 제어 (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) toohello 일괄 처리 서비스 사용자 역할입니다. Hello 지정 RBAC 역할 제공 되지 않는 경우 hello 일괄 처리 서비스는 400 (잘못 된 요청)을 반환 합니다. hello Azure 포털의에서 tooadd hello 역할:

    1. 선택 hello **VNet**, 다음 **액세스 제어 (IAM)** > **역할** > **가상 컴퓨터 참가자**  >  **추가**합니다.
    2. Hello에 **사용 권한을 추가** 블레이드, 선택 hello **가상 컴퓨터 참가자** 역할입니다.
    3. Hello에 **사용 권한을 추가** 블레이드, 일괄 처리 API hello에 대 한 검색 합니다. 검색 이러한 문자열에 대 한 다시 hello API를 찾을 때까지:
        1. **MicrosoftAzureBatch**
        2. **Microsoft Azure Batch** - 최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello 일괄 처리 API에 대 한 hello id입니다. 
    3. Hello API 일괄 처리 서비스 사용자를 선택 합니다. 
    4. **Save**를 클릭합니다.

        ![VM 참가자 역할 tooBatch 서비스 사용자를 할당 합니다.](./media/batch-api-basics/iam-add-role.png)


* hello 서브넷 충분 한 있어야 지정 무료 **IP 주소** tooaccommodate hello 대상 노드의 총 수, 즉, hello의 합계를 hello `targetDedicatedNodes` 및 `targetLowPriorityNodes` hello 풀의 속성입니다. Hello 서브넷 없는 경우 충분 한 사용 가능한 IP 주소, 일괄 처리 서비스 hello 부분적으로 hello 계산 노드 hello 풀에 할당 및이 크기 조정 오류를 반환 합니다.

* hello는 서브넷에 허용 해야 hello 일괄 처리 서비스 toobe에서 통신 작업 수 tooschedule hello 계산 노드를 지정 합니다. 계산 노드 통신 toohello 경우 의해 거부 되는 **보안 그룹 NSG (네트워크)** 다음 일괄 처리 서비스 hello 너무 hello 계산 노드의 hello 상태를 설정 하는 VNet hello와 관련 된**사용할 수 없는**합니다.

* Hello VNet에 연결 된 지정 된 경우 **(Nsg) 네트워크 보안 그룹** 및/또는 **방화벽**, 인바운드 통신에 대 한 몇 개의 예약 된 시스템 포트를 사용 해야 합니다.

- 가상 컴퓨터 구성을 사용하여 만든 풀의 경우 포트 29876 및 29877을 사용하도록 설정하고 , Linux의 경우 포트 22, Windows의 경우 포트 3389를 사용하도록 설정합니다. 
- 클라우드 서비스 구성을 사용하여 만든 풀의 경우 포트 10100, 20100 및 30100을 사용하도록 설정합니다. 
- 아웃 바운드 연결 tooAzure 포트 443에서 저장소를 사용 하도록 설정 합니다. 또한 VNET을 제공하는 모든 사용자 지정 DNS 서버에서 Azure Storage 끝점을 확인할 수 있어야 합니다. Hello 양식의 URL 특히 `<account>.table.core.windows.net` 확인할 수 있어야 합니다.

    hello 다음 표에서 hello 인바운드 tooenable hello 가상 컴퓨터 구성을 사용 하 여 만든 풀에 필요한 포트:

    |    대상 포트    |    원본 IP 주소      |    Batch가 NSG를 추가합니까?    |    사용 가능한 VM toobe에 대 한 필요 합니까?    |    사용자의 작업   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>가상 컴퓨터 구성 hello 사용 하 여 만든 풀에 대 한: 29876, 29877</li><li>클라우드 서비스 구성 hello 사용 하 여 만든 풀에 대 한: 10100, 20100, 30100</li></ul>         |    Batch 서비스 역할 IP 주소만 |    예. 일괄 처리의 네트워크 인터페이스 (NIC) 연결 된 tooVMs hello 수준에서 Nsg를 추가합니다. 이러한 NSG는 Batch 서비스 역할 IP 주소의 트래픽만 허용합니다. 전체 웹 hello에 대 한 이러한 포트를 여는 경우에 hello 트래픽 hello NIC.에서 차단 됩니다. |    예  |  일괄 처리는 일괄 처리 IP 주소에만 허용 하기 때문에 NSG를 toospecify를 않아도 됩니다. <br /><br /> 하지만 NSG를 지정하는 경우에는 이러한 포트에 인바운드 트래픽을 허용하세요. <br /><br /> 지정 하는 경우 * 프로그램 NSG의 원본 IP hello, 일괄 처리 여전히 추가 Nsg 연결 된 NIC tooVMs의 hello 수준에 있습니다. |
    |    3389, 22               |    사용자 컴퓨터를 VM hello를 원격으로 액세스할 수 있도록 디버깅을 위해 사용 합니다.    |    아니요                                    |    아니요                     |    원격 액세스 (RDP/SSH) toohello toopermit VM을 원하는 경우 Nsg를 추가 합니다.   |                 

    다음 표에서 hello tooenable toopermit 액세스 tooAzure 저장 해야 하는 hello 아웃 바운드 포트를 설명 합니다.

    |    아웃바운드 포트    |    대상    |    Batch가 NSG를 추가합니까?    |    사용 가능한 VM toobe에 대 한 필요 합니까?    |    사용자의 작업    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    아니요    |    예    |    모든 Nsg를 추가한 경우이 포트가 열려 toooutbound 트래픽의 임을 확인 합니다.    |


## <a name="scaling-compute-resources"></a>계산 리소스 크기 조정
와 [자동 크기 조정을](batch-automatic-scaling.md), hello toohello 현재 작업 및 자원 배정 현황을 계산 시나리오에 따라 풀의 계산 노드 수를 동적으로 조정 하는 hello 일괄 처리 서비스를 사용할 수 있습니다. 이렇게 하면 toolower hello 필요한 리소스에만 hello를 사용 하 여 응용 프로그램 실행의 전반적인 비용, 한 필요로 하지 않는 것을 해제 합니다.

[자동 크기 조정 수식](batch-automatic-scaling.md#automatic-scaling-formulas)을 작성하고 해당 수식의 풀과 연결하여 자동 크기 조정을 사용하도록 설정합니다. hello 일괄 처리 서비스는 hello 다음 크기 조정 간격 (구성할 수 있는 간격)에 대 한 hello 풀의 노드 hello 수식 toodetermine hello 대상 수를 사용 합니다. 나중에 풀에 배율을 사용 하도록 설정 또는 만들 때 hello는 풀에 대 한 자동 크기 조정 설정을 지정할 수 있습니다. 또한 hello 배율에서 크기 조정을 사용 하는 풀에서 설정을 업데이트할 수 있습니다.

예를 들어 아마도 작업이 필요 매우 많은 작업 toobe 실행을 제출 합니다. Hello hello 현재 대기 중인된 작업 수 및 hello 작업의 hello 작업의 hello 완료 비율에 따른 hello 풀의 노드 수를 조정 하는 크기 조정 수식 toohello 풀을 할당할 수 있습니다. 주기적으로 hello 일괄 처리 서비스는 hello 수식을 계산 하 고 hello 풀, 작업 및 다른 수식 설정을 기반으로 크기를 조정 합니다. hello 서비스 큐에 대기 중인된 작업 수가 많은 경우 필요에 따라 노드를 추가 하 고 큐에 대기 중이거나 실행 중인 작업이 없는 경우 노드를 제거 합니다.

크기 조정 수식을 기반으로 다음 메트릭을 hello:

* **시간 메트릭으로** 지정 hello에 5 분 마다 수집 된 통계를 기반으로 하는 시간 수입니다.
* **리소스 메트릭**은 CPU 사용량, 대역폭 사용량, 메모리 사용량 및 노드 수를 기반으로 합니다.
* **태스크 메트릭**은 *활성*(큐에 대기), *실행* 또는 *완료* 등 태스크 상태에 따라 다릅니다.

자동 크기 조정을 hello 풀의 계산 노드 수가 줄어들면 toohandle 작업 hello hello 시간에 실행 하는 작업을 감소 하는 방법을 고려해 야 합니다. tooaccommodate이, 일괄이 처리를 제공는 *노드 할당 취소 옵션* 수식에 포함할 수 있는 합니다. 예를 들어,를 실행 중인 작업을 즉시 중지, 즉시 중지 하 고 다음 다른 노드에서 실행을 위해 다시 대기 하거나 hello 노드 hello 풀에서 제거 되기 전에 toofinish 허용을 지정할 수 있습니다.

자동으로 응용 프로그램 크기를 조정하는 방법에 대한 자세한 내용은 [Azure Batch 풀에서 자동으로 계산 노드 크기 조정](batch-automatic-scaling.md)을 참조하세요.

> [!TIP]
> toomaximize는 리소스 사용률을 계산 하 고, 작업의 hello 끝에서 노드 toozero hello 대상 수를 설정 하지만 실행 중인 작업 toofinish 허용 합니다.
>
>

## <a name="security-with-certificates"></a>인증서를 사용한 보안
암호화 또는 암호에 대 한 hello 키 등의 작업에 대 한 중요 한 정보를 해독 하는 경우 일반적으로 toouse 인증서가 필요는 [Azure 저장소 계정][azure_storage]합니다. toosupport이 노드에서 인증서를 설치할 수 있습니다. 암호화 된 암호는 tootasks 명령줄 매개 변수를 통해 또는 hello 작업 리소스 중 하나에 포함 하 고 설치 하는 hello 인증서 toodecrypt 사용된 될 수 있습니다 이러한.

Hello를 사용 하 여 [인증서 추가] [ rest_add_cert] 작업 (일괄 처리 REST) 또는 [CertificateOperations.CreateCertificate] [ net_create_cert] 메서드 (일괄 처리.NET) tooadd 인증서 tooa 일괄 처리 계정입니다. 그런 다음 새로운 또는 기존 풀과 hello 인증서를 연결할 수 있습니다. 인증서와 풀과 연결 된 일괄 처리 서비스 hello hello 풀의 각 노드에서 hello 인증서를 설치 합니다. hello 일괄 처리 서비스는 hello 노드 시작 되 면, 모든 작업 (hello 시작 작업 및 작업 관리자 태스크가 포함)를 실행 하기 전에 hello 적절 한 인증서를 설치 합니다.

인증서 tooan를 추가 하는 경우 *기존* 풀 hello 적용 toobe toohello 노드 인증서에 해당 계산 노드를 다시 부팅 해야 합니다.

## <a name="error-handling"></a>오류 처리
필요한 toohandle를 찾을 수 있습니다 일괄 처리 솔루션 내에서 작업 및 응용 프로그램 오류가 발생 했습니다.

### <a name="task-failure-handling"></a>태스크 오류 처리
태스크 오류는 다음 범주로 분류됩니다.

* **사전 처리 실패**

    작업 실패 toostart 전처리 오류 hello 작업에 대 한 설정 됩니다.  

    미리 처리 오류가 발생할 수 없습니다 hello 작업의 리소스 파일을 이동, hello 저장소 계정이 더 이상를 사용할 수 없거나 다른 문제가 발생 했습니다는 금지 hello 성공의 파일을 복사 toohello 노드.

* **파일 업로드 오류**

    어떤 이유로 든 실패 하면 작업에 대해 지정 된 파일을 업로드 하는 경우에 파일 업로드 오류 hello 작업에 대 한 설정 됩니다.

    파일 업로드가 hello 유효 하지 않거나 없으면 hello 저장소 계정이 더 이상를 쓰기 권한을 제공 하지 않습니다 Azure 저장소에 액세스 하거나 다른 문제가 있는 경우 제공 된 SAS 발견 하지 못한 경우 파일에서의 성공적인 복사 hello 오류가 발생할 수 없습니다 hello 노드입니다.    

* **응용 프로그램 오류**

    hello 작업의 명령줄에서 지정 된 hello 프로세스도 실패할 수 있습니다. hello 프로세스 하다 고 판단 되 toohave hello 작업에서 실행 되는 hello 프로세스에 의해 0이 아닌 종료 코드를 반환 하는 경우 실패 (참조 *작업 종료 코드* hello 다음 섹션에서).

    응용 프로그램 오류에 대 한 일괄 처리를 구성할 수 있습니다를 tooa tooautomatically 다시 시도 hello 태스크 횟수를 지정 합니다.

* **제약 조건 오류**

    지정 하는 작업 또는 작업에 대 한 최대 실행 시간과 hello hello 제약 조건을 설정할 수 있습니다 *maxWallClockTime*합니다. 이 tooprogress 실패 하는 작업을 종료 하기 위해 유용할 수 있습니다.

    Hello 최대 수명을 초과 되 면 hello 작업으로 표시 됩니다 *완료*, hello 종료 코드가 너무 설정 되어 있지만`0xC000013A` 및 hello *schedulingError* 필드가로 표시 되 `{ category:"ServerError", code="TaskEnded"}`합니다.

### <a name="debugging-application-failures"></a>응용 프로그램 오류 디버그
* `stderr` 및 `stdout`

    실행 하는 동안 응용 프로그램 tootroubleshoot 문제를 사용할 수 있는 진단 출력을 생성할 수 있습니다. Hello에 설명 된 대로 이전 섹션 [파일 및 디렉터리](#files-and-directories), 표준 출력과 표준 오류 출력 너무 hello 일괄 처리 서비스에서 기록`stdout.txt` 및 `stderr.txt` hello hello 작업 디렉터리의 파일이 계산 노드. 이 파일 hello Azure 포털 또는 hello 일괄 처리 Sdk toodownload 중 하나를 사용할 수 있습니다. 예를 들어 이러한 파일 및 사용 하 여 문제 해결을 위해 다른 파일을 검색할 수 있습니다 [ComputeNode.GetNodeFile] [ net_getfile_node] 및 [CloudTask.GetNodeFile] [ net_getfile_task] hello 일괄 처리.NET 라이브러리에 있습니다.

* **태스크 종료 코드**

    앞서 언급 했 듯이 작업 hello 프로세스 hello 작업에서 실행 되는 0이 아닌 종료 코드를 반환 하는 경우 hello 일괄 처리 서비스에서 실패 한 것으로 표시 됩니다. 프로세스를 실행 하는 작업을 하는 경우 일괄 처리 hello로 hello 작업의 종료 코드 속성을 채우는 *hello 프로세스의 코드를 반환*합니다. 작업의 종료 코드는 중요 한 toonote는 **하지** hello 일괄 처리 서비스에 의해 결정 됩니다. 작업의 종료 코드는 hello 프로세스 자체 또는 hello 운영 체제에서 실행 되는 hello 프로세스에 의해 결정 됩니다.

### <a name="accounting-for-task-failures-or-interruptions"></a>태스크 실패 또는 중단에 대한 조정
간혹 태스크가 실패하거나 중단될 수 있습니다. hello 작업 응용 프로그램 자체 실패할 수 있습니다, 작업이 실행 되는 hello에 hello 노드 다시 부팅 될 수 있습니다 또는 hello 노드에서에서 제거 될 수 hello 풀 크기 조정 작업 중 이면 hello 풀의 할당 취소 정책까지 기다리지 않고 즉시 tooremove 노드 집합 작업 toofinish 합니다. Hello 작업 모든 경우 일괄 처리에 의해 다른 노드에서 실행을 위해 자동으로 요청할 수 수 있습니다.

또한 일시적인 문제 toocause 작업 toohang에 대 한 가능한 또는 tooexecute 너무 길어서 수행 됩니다. 작업에 대 한 hello 최대 실행 간격을 설정할 수 있습니다. Hello 최대 실행 간격을 초과할 경우 hello 일괄 처리 서비스는 hello 작업 응용 프로그램을 중단 합니다.

### <a name="connecting-toocompute-nodes"></a>Toocompute 노드를 연결
추가 디버깅 및 tooa 계산 노드를 원격으로 로그인 하 여 문제 해결을 수행할 수 있습니다. Windows 노드에 대해 hello Azure 포털 toodownload 프로토콜 RDP (원격 데스크톱) 파일을 사용 하 고 Linux 노드에 대 한 SSH (보안 셸) 연결 정보를 얻을 수 있습니다. 예를 들어 일괄 처리 Api-hello를 함께 사용 하 여 이름을 수행할 수도 있습니다 [일괄 처리.NET] [ net_rdpfile] 또는 [일괄 처리 Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh)합니다.

> [!IMPORTANT]
> RDP 또는 SSH를 통해 tooconnect tooa 노드를 먼저 만들어야 합니다 사용자 hello 노드에서 합니다. toodo이 hello Azure 포털을 사용할 수 있습니다 [사용자 계정 tooa 노드 추가] [ rest_create_user] hello 배치 REST API를 사용 하 여 hello 호출 [ComputeNode.CreateComputeNodeUser] [ net_create_user] 메서드 일괄 처리.NET 또는 호출 hello [add_user] [ py_add_user] hello 일괄 처리 Python 모듈에서 메서드.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>문제가 있는 계산 노드 문제 해결
실패 하는 일부 작업의 경우 일괄 처리 클라이언트 응용 프로그램 또는 서비스 실패 hello 작업 tooidentify 오동작 노드의 hello 메타 데이터를 검사할 수 있습니다. 풀의 각 노드에 고유 ID를 지정 하 고 hello 노드는 작업이 실행 되는 hello 작업 메타 데이터에 포함 됩니다. 문제 노드를 식별하면 다음과 같은 몇 가지 작업을 수행할 수 있습니다.

* **Hello 노드를 다시 부팅** ([REST][rest_reboot] | [.NET][net_reboot])

    재시작 hello 노드 걸린 또는 손상 프로세스와 같은 잠재적인 문제를 지울 경우에 따라 수 있습니다. 시작 태스크를 사용 하는 경우 풀 또는 작업 준비 태스크 작업에 사용 하는 경우 실행할 hello 노드 다시 시작 될 때 note 합니다.
* **Hello 노드를 이미지로 다시 설치할** ([REST][rest_reimage] | [.NET][net_reimage])

    Hello 운영 체제 hello 노드를 다시 설치 합니다. 노드를 다시 부팅 한와 마찬가지로 작업을 시작 하 고 작업 준비 작업 hello 노드를 이미지로 다시 설치 된 후 다시 실행 하십시오.
* **Hello 풀에서 hello 노드 제거** ([REST][rest_remove] | [.NET][net_remove])

    때때로 필요한 toocompletely hello 노드 hello 풀에서 제거 됩니다.
* **Hello 노드에서 작업 예약 사용 안 함** ([REST][rest_offline] | [.NET][net_offline])

    이 효과적으로 hello 노드가 오프 라인 더 이상 작업이 tooit를 할당 하지만 hello 노드 tooremain 실행을 가능 하 고 있는 hello 풀에 있습니다. 이렇게 하면 hello 오류의 hello 발생 tooperform 추가 조사 hello 실패 한 작업 데이터의 손실 없이 및 hello 노드 추가 작업 실패를 유발 하지 않고 있습니다. 작업 일정 hello 노드에 대 한 다음 비활성화할 수는 예를 들어 [에 원격으로 로그인](#connecting-to-compute-nodes) tooexamine hello 노드의 이벤트 로그 또는 기타 문제 해결을 수행 합니다. 작업 일정을 사용 하 여 hello 노드를 다시 온라인을 상태로 되돌릴 수 조사를 완료 한 후 ([REST][rest_online] | [.NET] [ net_online]), 또는 다른 작업 이전에 설명한 hello 중 하나를 수행 합니다.

> [!IMPORTANT]
> Hello 동작을 수행할 때 hello 노드에서 현재 실행 중인 작업의 처리 방법을 수 toospecify은 이미지로 다시 설치, 제거 및 작업 일정 사용 안 함-,-이 섹션에 설명 되어 있는 각 작업을 다시 부팅 합니다. 예를 들어 해제할 경우 작업을 지정할 수 있습니다 hello 일괄 처리.NET 클라이언트 라이브러리를 사용 하 여 노드에서 예약 된 [DisableComputeNodeSchedulingOption] [ net_offline_option] enum 값 toospecify 여부 너무**Terminate** 작업 실행, **큐에 다시 넣고** 할 다른 노드에서 예약에 대 한 hello 동작을 수행 하기 전에 실행 중인 작업 toocomplete를 허용 하거나 (**TaskCompletion**).
>
>

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 내용은 [일괄 처리 Api와 도구](batch-apis-tools.md) 일괄 처리 솔루션을 만드는 데 사용할 수 있습니다.
* 일괄 처리 응용 프로그램에 대 한 단계별 안내 [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md)합니다. 또한 한 [Python 버전](batch-python-tutorial.md) Linux에서 작업을 실행 하는 hello 자습서의 계산 노드.
* 다운로드 하 고 hello 빌드 [일괄 처리 탐색기] [ github_batchexplorer] 일괄 처리 솔루션을 개발 하는 동안 사용 하기 위해 샘플 프로젝트입니다. 일괄 처리 탐색기 hello를 사용 하 여 hello 다음 등을 수행할 수 있습니다.

  * Batch 계정 내에서 풀, 작업 및 태스크 모니터링 및 조작
  * 노드에서 `stdout.txt`, `stderr.txt` 및 기타 파일 다운로드
  * 노드에서 사용자를 만들고 원격 로그인을 위한 RDP 파일 다운로드
* 너무 방법에 대해 알아봅니다[Linux 계산 노드는 풀을 만들](batch-linux-nodes.md)합니다.
* Hello 방문 [Azure 배치 포럼] [ batch_forum] msdn 합니다. hello 포럼은 좋은 배우는 하는지 여부는 일괄 처리를 사용 하 여 전문 tooask 질문을 배치 합니다.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
