---
title: "aaaUse 사례-고객 프로 파일링"
description: "Azure 데이터 팩터리는 사용 되는 toocreate 데이터 기반 워크플로 (파이프라인) tooprofile 게임 고객 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>사용 사례 - 고객 프로파일링
Azure Data Factory에는 많은 사용 되는 서비스 tooimplement hello Cortana Intelligence solution accelerator 제품군 중 하나입니다.  Cortana Intelligence에 대한 자세한 내용은 [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics)를 참조하세요. 이 문서에서는 간단한 사용 사례 toohelp 설명 시작에 대 한 Azure Data Factory 수 일반적인 분석 문제를 해결 하는 방법을 이해 하는 데 있습니다.

## <a name="scenario"></a>시나리오
Contoso는 게임 콘솔, 핸드헬드 장치, PC(개인용 컴퓨터) 등 다양한 플랫폼용 게임을 만드는 게임 회사입니다. 플레이어가 게임, 대로 사용 패턴, 게임 스타일 및 hello 사용자의 기본 설정을 추적 hello를 큰 볼륨의 로그 데이터가 생성 됩니다.  인구 통계, 국가 함께 사용 하면 제품 데이터를 Contoso 분석 tooguide tooenhance 플레이어 발생 하 고 업그레이드를 위한 대상으로 지정 하는 방법에 고 게임을 수행할 수 있습니다 및 구입 합니다. 

Contoso의 목표는 플레이어의 hello 게임 기록에 근거 tooidentify 상향 판매/교차 판매 기회의 뛰어난 기능 toodrive 비즈니스 성장 추가 및 보다 나은 경험 toocustomers 제공 합니다. 이 사용 사례의 경우 비즈니스의 예로 게임 회사를 사용합니다. hello 회사 toooptimize 플레이어의 동작에 따라 해당 게임을 원합니다. 이러한 원칙 tooengage가 원하는 tooany 비즈니스 해당 고객의 제품 및 서비스에 게 적용 하 고 고객 경험을 향상 시킵니다.

이 솔루션에서는 Contoso 최근에 시작 된 마케팅 캠페인의 tooevaluate hello 효과 하려고 합니다. 에서는 시작 hello 원시 게임 로그, 프로세스 및 지리적 위치 데이터와 함께를 보강, 광고의 참조 데이터와 조인 하며 마지막으로 Azure SQL 데이터베이스 tooanalyze hello 캠페인의 영향에 복사 합니다.

## <a name="deploy-solution"></a>솔루션 배포
모든 필요한 tooaccess 이며이 간단한 사용 사례 아웃 시도 [Azure 구독](https://azure.microsoft.com/pricing/free-trial/), [Azure Blob 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account), 및 [Azure SQL 데이터베이스](../sql-database/sql-database-get-started.md)합니다. Hello에서 파이프라인을 프로 파일링 하는 hello 고객 배포 **샘플 파이프라인** 데이터 팩터리의 hello 홈 페이지에 바둑판식으로 배열 합니다.

1. 데이터 팩터리를 만들거나 기존 데이터 팩터리를 엽니다. 참조 [Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계 toocreate 데이터 팩터리에 대 한 합니다.
2. Hello에 **DATA FACTORY** 블레이드 hello 데이터 팩토리에 대 한 클릭 hello **샘플 파이프라인** 바둑판식으로 배열입니다.

    ![샘플 파이프라인 타일](./media/data-factory-samples/SamplePipelinesTile.png)
3. Hello에 **샘플 파이프라인** 블레이드에서 hello 클릭 **프로 파일링 하는 고객** toodeploy 되도록 합니다.

    ![샘플 파이프라인 블레이드](./media/data-factory-samples/SampleTile.png)
4. Hello 샘플에 대 한 구성 설정을 지정 합니다. 예를 들어 Azure Storage 계정 이름과 키, Azure SQL Server 이름, 데이터베이스, 사용자 ID, 암호 등입니다.

    ![샘플 블레이드](./media/data-factory-samples/SampleBlade.png)
5. Hello 구성 설정을 지정 하 여 완료 한 후 클릭 **만들기** 샘플 파이프라인 및 hello 파이프라인에서 사용 되는 연결 된 서비스/테이블 hello toocreate/배포 합니다.
6. 이전 hello 클릭 hello 샘플 타일에서 배포의 hello 상태를 확인할 **샘플 파이프라인** 블레이드입니다.

    ![배포 상태](./media/data-factory-samples/DeploymentStatus.png)
7. Hello 표시 되 면 **배포 성공** hello 타일 hello 샘플을 닫기 hello 메시지 **샘플 파이프라인** 블레이드입니다.  
8. **DATA FACTORY** 블레이드에 표시 연결 된 서비스, 데이터 집합 및 파이프라인 tooyour 데이터 팩터리 추가 됩니다.  

    ![데이터 팩터리 블레이드](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>솔루션 개요
이 간단한 사용 사례는 Azure 데이터 팩터리 tooingest를 사용 하 여, 준비, 변환, 분석 하는 방법을 데이터 게시의 한 예로 사용할 수 있습니다.

![종단 간 워크플로](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

이 그림에서는 hello 데이터 파이프라인에서에서 어떻게 나타나는지 hello Azure 포털 배포 된 후에 대해 설명 합니다.

1. hello **PartitionGameLogsPipeline** hello 원시 게임 이벤트를 읽은 다음 blob 저장소에서 연도, 월 및 일을 기반으로 파티션을 만듭니다.
2. hello **EnrichGameLogsPipeline** 분할된 게임 이벤트와 지역 코드 참조 데이터를 조인 하 고 IP 주소 toohello 해당 지리적 위치에 매핑하여 hello 데이터를 강화 합니다.
3. hello **AnalyzeMarketingCampaignPipeline** 파이프라인 hello 보강 한 데이터를 사용 하 고 데이터 toocreate hello 최종 출력 마케팅 캠페인 효과 포함 하는 광고 hello를 사용 하 여 처리 합니다.

이 예제에서는 데이터 팩터리의 입력된 데이터, 변환 및 프로세스 hello 데이터를 복사 하 고 hello 최종 데이터 tooan Azure SQL 데이터베이스를 출력 하는 사용 되는 tooorchestrate 활동 이지만  데이터 파이프라인의 hello 네트워크를 시각화 하 고, 관리 다음 hello UI에서에서 해당 상태를 모니터링 수도 있습니다.

## <a name="benefits"></a>이점
해당 사용자 프로필 분석을 최적화 하 고 비즈니스 목표에 맞추어를 게임 회사 수 tooquickly 수집 사용 패턴은 하 고 해당 마케팅 캠페인의 hello 효과 분석 합니다.

