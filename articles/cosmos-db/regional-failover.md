---
title: "Azure Cosmos DB에서 장애 조치 aaaRegional | Microsoft Docs"
description: "Azure Cosmos DB에서 수동 및 자동 장애 조치(failover)가 작동하는 방식에 대해 알아봅니다."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>비즈니스 연속성을 위한 Azure Cosmos DB의 자동 지역별 장애 조치(failover)
Azure Cosmos DB hello 글로벌 데이터 배포를 제공 하 여 단순화 완전히 관리 [다중 지역 데이터베이스 계정](distribute-data-globally.md) 일관성, 가용성 및 성능에 해당 하는 포함 된 모든 간 지우기 균형을 제공 하는 보장합니다. Cosmos DB 계정을 제공 고가용성을 단일 숫자 ms 대기 시간, [잘 정의 된 일관성 수준이](consistency-levels.md), 멀티 호 밍 Api hello 기능 tooelastically 배율 처리량 및 저장소 지역 투명 한 장애 조치 hello 전세계 합니다. 

Cosmos DB 명시적 모두 지원, 정책 기반 장애 조치 하는 수 toocontrol hello 종단 간 시스템 동작은 실패의 hello 이벤트에서. 이 문서에서 다음을 살펴봅니다.

* 수동 장애 조치(failover)가 Cosmos DB에서 작동하는 방식
* Cosmos DB에서 자동 장애 조치(failover)가 작동하는 방식 및 데이터 센터가 다운될 때 발생하는 결과
* 응용 프로그램 아키텍처에서 수동 장애 조치를 사용하는 방법

Scott Hanselman과 수석 엔지니어링 관리자 Karthik Raman이 진행하는 이 Azure Friday 비디오를 통해 지역 장애 조치에 대해서도 자세히 알아 볼 수 있습니다.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>다중 지역 응용 프로그램 구성
장애 조치 모드에 들어가기 전에 다중 지역 가용성의 응용 프로그램 tootake 장점은 구성 국가별 장애 조치의 hello 면에서 복원 하는 방법을 살펴봅니다.

* 먼저 여러 지역에 응용 프로그램을 배포합니다.
* 응용 프로그램을 배포한 모든 지역에서 대기 시간이 짧은 액세스 tooensure hello에 해당 구성 [기본 지역 목록](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) hello 중 하나를 통해 각 지역의 지원 되는 Sdk에 있습니다.

조각과 방법을 따르는 hello tooinitialize 다중 지역 응용 프로그램입니다. 여기에서는 Azure Cosmos DB 계정 hello `contoso.documents.azure.com` 두 영역-유럽 북부 및 미국 서 부로 구성 되어 있습니다. 

* hello 응용 프로그램 (예: Azure 응용 프로그램 서비스 사용) hello 미국 서 부 지역에 배포 되어 
* 구성 된 `West US` hello 짧은 대기 시간에 대 한 첫 번째 기본 영역으로 읽기
* 구성 된 `North Europe` hello (국가별 실패 하는 동안 고가용성)에 대 한 두 번째 기본 영역으로

DocumentDB API hello,이 구성은 다음 코드 조각 hello 같습니다.

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

hello 응용 프로그램은도 hello 순서를 반대로 하는 기본 지역에 hello 유럽 북부 지역에 배포 됩니다. 즉, 짧은 대기 시간 읽기에 대 한 hello 북부 유럽 지역의 먼저 지정 됩니다. 그런 다음 hello 미국 서 부 지역 국가별 실패 하는 동안 고가용성을 위해 두 번째 기본 영역은 hello로 지정 됩니다.

hello 다음 아키텍처 다이어그램은 다중 지역 응용 프로그램 배포를 있는 보여 줍니다 Cosmos DB 및 hello 응용 프로그램 구성된 toobe Azure 4 개의 지리적 지역에서 사용할 수 있습니다.  

![Azure Cosmos DB를 통해 전역으로 분산된 응용 프로그램 배포](./media/regional-failover/app-deployment.png)

이제 hello Cosmos DB 서비스에서 자동 장애 조치를 통해 지역 오류를 처리 하는 방법을 살펴보겠습니다. 

## <a id="AutomaticFailovers"></a>자동 장애 조치
Azure 지역 가동 중단 또는 데이터 센터 중단의 hello 드문 이벤트에서 Cosmos DB 영향을 받는 hello 지역에 있으면 모든 Cosmos DB 계정의 장애 조치를 자동으로 트리거됩니다. 

**읽기 지역에 가동 중단이 발생하면 어떻게 됩니까?**

Cosmos DB 계정은 hello 영향을 받는 영역 중 하나에 있는 읽기 영역으로는 자동으로 해당 쓰기 지역에서 연결이 끊어지고 오프 라인으로 표시 됩니다. hello Cosmos DB Sdk 구현 tooautomatically 수 있게 해 주는 국가별 검색 프로토콜 영역에 사용할 수 있고 리디렉션 호출 toohello 다음 사용 가능한 지역 hello 기본 지역 목록에서 읽기를 검색 합니다. Hello의 hello 영역 중 우선 지역 목록을 사용할 수 있는, 호출 자동으로 대체할 toohello 현재 쓰기 지역. 응용 프로그램 코드 toohandle 국가별 장애 변경 없이 사용 해야 합니다. 이 전체 프로세스 동안 일관성 보증이 toobe Cosmos DB에 의해 적용을 계속 합니다.

![Azure Cosmos DB의 읽기 지역 장애](./media/regional-failover/read-region-failures.png)

Hello 영향을 받는 영역 hello 중단에서 복구 되 면 hello 지역에 있는 모든 영향을 받는 hello Cosmos DB 계정은 hello 서비스에 의해 자동으로 복구 됩니다. Cosmos DB 계정 hello 영향을 받는 영역에 읽기 영역을 보유 한 다음 자동으로 현재 쓰기 지역와 동기화 하 고 온라인 설정 합니다. hello Cosmos DB Sdk hello 가용성 hello 새 영역을 찾아 hello 현재 읽기 영역 hello 응용 프로그램에서 구성한 hello 기본 영역 목록을 기반으로 hello 영역을 선택 해야 하는지 여부를 평가 합니다. 후속 읽기는 변경 내용을 tooyour 응용 프로그램 코드를 사용할 필요 없이 리디렉션된 toohello 복구 된 지역입니다.

**쓰기 지역에 가동 중단이 발생하면 어떻게 됩니까?**

지정한 Cosmos DB 계정에 대 한 현재 쓰기 영역 hello hello 영향을 받은 영역을 사용 하는 경우 다음 hello 지역 자동으로 표시될지 오프 라인으로 합니다. 그런 다음 대체 지역은 hello 영향을 받는 각 Cosmos DB 계정 영역을 작성할 때 수준이 올려집니다. Hello Azure 포털을 통해 프로그램 Cosmos DB 계정에 대 한 hello 지역 선택 순서를 완벽 하 게 제어할 수 있습니다 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)합니다. 

![Azure Cosmos DB의 장애 조치(failover) 우선 순위](./media/regional-failover/failover-priorities.png)

자동 장애 조치 하는 동안 Cosmos DB 자동으로 선택 hello 다음 쓰기 영역 지정한 Cosmos DB에 대 한 계정 hello에 따라 우선 순위 순서를 지정 합니다. 

![Azure Cosmos DB의 쓰기 지역 장애](./media/regional-failover/write-region-failures.png)

Hello 영향을 받는 영역 hello 중단에서 복구 되 면 hello 지역에 있는 모든 영향을 받는 hello Cosmos DB 계정은 hello 서비스에 의해 자동으로 복구 됩니다. 

* 해당 이전 쓰기 지역 hello 영향을 받는 영역에 있는 DB cosmos 계정 hello 영역의 hello 복구 후에 오프 라인 모드에서 읽기 가용성은 유지 됩니다. 
* 쿼리할 수 있습니다이 지역 toocompute 복제 되지 않은 한 쓰기가 hello 비활성 동안 hello hello 현재 쓰기 지역에서 사용할 수 있는 데이터와 비교 하 여 합니다. 응용 프로그램의 hello 요구에 따라, 병합 및/또는 충돌 해결을 수행 하 고 hello 최종 집합 변경 내용 다시 toohello 현재 쓰기 영역을 작성할 수 있습니다. 
* 병합 변경 내용을 마친 후 있습니다 수 hello 영향을 받는 영역 다시 온라인 상태로 전환 제거 하 고 hello 지역 tooyour Cosmos DB 계정에 다시 추가 중입니다. Hello 영역 다시 추가 되 면 구성할 수 있습니다 hello 쓰기 지역 변수로 다시 hello Azure 포털을 통해 수동 장애 조치를 수행 하 여 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)합니다.

## <a id="ManualFailovers"></a>수동 장애 조치

또한 현재 hello tooautomatic 장애 조치 지정한 Cosmos DB 계정의 지역 수동으로 동적 변경할 수 hello 기존 읽기 영역의 tooone을 작성 합니다. Hello Azure 포털을 통해 수동 장애 조치를 시작할 수 있습니다 또는 [프로그래밍 방식으로](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)합니다. 

수동 장애 조치 되도록 **데이터 손실을 0** 및 **가용성 0** 손실 되 고 정상적으로 이전 hello에서 전송 쓰기 상태 쓰기 지역 toohello 새 hello 지정한 Cosmos DB 계정에 대 한 합니다. 자동 장애 조치 Cosmos DB SDK를 자동으로 hello와 같은 지역 수동 장애 조치 중에 변경 및 호출을 자동으로 리디렉션된 toohello 새 쓰기 영역 핸들 작성 합니다. 응용 프로그램 toomanage 장애 코드 또는 구성 변경 내용이 없습니다 사용 해야 합니다. 

![Azure Cosmos DB에서의 수동 장애 조치(failover)](./media/regional-failover/manual-failovers.png)

수동 장애 조치 유용할 수 있습니다 hello 일반적인 시나리오는 다음과 같습니다.

**Hello 클록 모델**: 응용 프로그램 hello hello 시간에 따라 예측 가능한 트래픽 패턴을 있으면 hello 쓰기 상태 toohello 가장 활동적인 지리적 지역 hello 하루 중 시간에 따라 주기적으로 변경할 수 있습니다.

**서비스 업데이트**: 특정 전 세계적으로 분산된 응용 프로그램 배포의 계획 된 서비스 업데이트 하는 동안 트래픽 관리자를 통해 트래픽을 toodifferent 영역 경로 재정의 해야 할 수도 있습니다. 이제 이러한 응용 프로그램 배포에 있는 되기 toobe 활성 트래픽 hello 서비스 업데이트 기간 동안 수동 장애 조치 tookeep hello 쓰기 상태 toohello 영역을 사용할 수 있습니다.

**BCDR(비즈니스 연속성 및 재해 복구) 및 HADR(고가용성 및 재해 복구) 절차** - 대부분의 엔터프라이즈 응용 프로그램에는 개발 및 릴리스 프로세스의 일부로 비즈니스 연속성 테스트가 포함됩니다. BCDR 및 HADR 테스트 종종는 규정 준수 인증의 중요 한 단계 및 지역 가동 중단의 hello 경우에서 서비스 가용성을 보장 합니다. Cosmos DB 계정의 수동 장애 조치를 트리거하 및/또는 추가 및 영역을 동적으로 제거 하 여 저장소에 대 한 Cosmos DB를 사용 하는 응용 프로그램의 hello BCDR 준비 상태를 테스트할 수 있습니다.

이 문서에서는 Cosmos DB에서 어떻게 수동 및 자동 장애 조치 작업 및 사용자 Cosmos DB 계정 및 응용 프로그램 toobe 전체적으로 사용 가능한 구성 하는 방법을 살펴보았습니다. Cosmos DB의 전체 복제 지원을 사용 하 여 종단 간 대기 시간을 향상 시킬 수 있으며 지역 오류의 hello 이벤트에도 항상 사용 가능한 되는지 확인 하십시오. 

## <a id="NextSteps"></a>다음 단계
* Cosmos DB에서 [글로벌 배포](distribute-data-globally.md)를 지원하는 방법에 대한 자세한 정보
* [Azure Cosmos DB를 통한 전역 일관성](consistency-levels.md)에 대한 자세한 정보
* Azure Cosmos DB의 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)를 사용하여 여러 지역으로 개발
* 자세한 내용은 방법 toobuild [다중 지역 기록기 아키텍처](multi-region-writers.md) Azure documentdb

