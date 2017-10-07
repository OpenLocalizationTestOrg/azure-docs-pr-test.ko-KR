---
title: "hello 클라우드에서 대규모 병렬 컴퓨팅 솔루션을 실행 하는 일괄 처리 aaaAzure | Microsoft Docs"
description: "대규모 병렬 및 HPC 워크 로드에 대 한 hello Azure 배치 서비스를 사용 하 여 알아봅니다"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Batch를 사용하여 본질적인 병렬 워크로드 실행

Azure 일괄 처리는 hello 클라우드에서 대규모 병렬 및 고성능 HPC (컴퓨팅) 응용 프로그램을 효율적으로 실행 하기 위한 플랫폼 서비스입니다. Azure 배치 가상 컴퓨터의 관리 되는 컬렉션에서 계산 집약적인 작업 toorun를 예약 하 고 계산할 수 있습니다 자동으로 크기 조정 작업의 리소스 toomeet hello 요구 합니다.

Azure 일괄 처리와 쉽게 및 정의할 수 있습니다 Azure 계산 리소스 tooexecute 응용 프로그램 병렬로 규모에 있습니다. 없는 필요 toomanually는 생성, 구성 및 관리는 HPC 클러스터, 개별 가상 컴퓨터, 가상 네트워크 또는 복잡 한 작업 및 예약 인프라 작업 합니다. Azure 배치는 이러한 태스크를 자동화하거나 단순화합니다.

## <a name="use-cases-for-batch"></a>배치에 대한 사용 사례
배치는 대용량의 비슷한 태스크를 실행하여 원하는 결과를 얻을 수 있는 *배치 처리* 또는 *배치 컴퓨팅*을 위해 관리되는 Azure 서비스입니다. 배치 컴퓨팅은 대량의 데이터를 정기적으로 처리, 변환 및 분석하는 조직에서 가장 일반적으로 사용합니다.

배치는 본질적으로 병렬("처치 곤란 병렬"이라고도 함) 응용 프로그램 및 워크로드에서 잘 작동합니다. 본질적으로 병렬 워크로드는 여러 컴퓨터에서 동시에 작업을 수행하는 여러 태스크로 쉽게 분할됩니다.

![병렬 태스크][1]<br/>

일반적으로 이 기술을 사용하여 처리되는 워크로드의 몇 가지 예는 다음과 같습니다.

* 재무 위험 모델링
* 기후 및 수문학 데이터 분석
* 이미지 렌더링, 분석 및 처리
* 미디어 인코딩 및 트랜스코딩
* 유전자 서열 분석
* 엔지니어링 스트레스 분석
* 소프트웨어 테스트

일괄 처리 reduce 단계가 hello 끝에 있는 병렬 계산을 수행할 수 있고 더 복잡 한 HPC 워크 로드와 같은 실행 [인터페이스 MPI (Message Passing)](batch-mpi.md) 응용 프로그램입니다.

Azure에서 배치 및 다른 HPC 솔루션 간의 비교는 [배치 및 HPC 솔루션](batch-hpc-solutions.md)을 참조하세요.

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>시나리오: 병렬 워크로드 규모 확장
일괄 처리 서비스 hello로 일괄 처리 Api toointeract hello를 사용 하는 일반적인 솔루션 3D 장면-계산 노드가 풀에 대 한 이미지의 hello 렌더링 같은-기본적으로 병렬 작업을 확장 하는 작업이 포함 됩니다. 이 풀의 컴퓨터 노드 "렌더링 팜에" 수 제공 하는 수십, 수백 또는 수천 코어 tooyour 렌더링 작업의 예입니다.

hello 다음 다이어그램은 클라이언트 응용 프로그램 일반적인 일괄 처리 워크플로 보여 줍니다 또는 호스 티 드 서비스를 사용 하 여 일괄 처리 toorun 병렬 작업입니다.

![배치 솔루션 워크플로][2]

이 일반적인 시나리오에서는 응용 프로그램 또는 서비스 hello 다음 단계를 수행 하 여 Azure 일괄 처리에서 계산 작업 부하를 처리 합니다.

1. Hello 업로드 **입력 파일** 및 hello **응용 프로그램** 을 Azure 저장소 계정에 해당 파일 tooyour 처리할 합니다. hello 입력된 파일 예: 재무 모델링 데이터 또는 비디오 파일 toobe 코드 변환 된 응용 프로그램에서 처리 하는 모든 데이터를 수 있습니다. hello 응용 프로그램 파일에는 3 차원 렌더링 응용 프로그램 또는 미디어 코드 변환기와 같은 hello 데이터 처리에 사용 되는 모든 응용 프로그램 수 있습니다.
2. 일괄 처리 만들기 **풀** -일괄 처리 계정에 대 한 계산 노드의 이러한 노드는 hello 가상 컴퓨터에서 실행할 작업입니다. Hello 같은 속성을 지정할 [노드 크기](../cloud-services/cloud-services-sizes-specs.md)등의 운영 체제 및 hello 응용 프로그램 tooinstall hello 노드 hello 풀 (hello 응용 프로그램 1 단계에서 업로드)를 연결 하는 경우의 Azure 저장소의 hello 위치입니다. 구성할 수도 있습니다 hello 풀 너무[배율을 자동으로 조정](batch-automatic-scaling.md) 작업에서 생성 된 응답 toohello 작업에서 합니다. 자동 크기 조정 동적으로 hello hello 풀의 계산 노드 수를 조정 합니다.
3. 일괄 처리 만들기 **작업** toorun hello 작업의 계산 노드 hello 풀에 있습니다. 작업을 만들 때 배치 풀과 연결합니다.
4. 추가 **작업** toohello 작업 합니다. 작업 tooa 작업을 추가 하는 경우 hello 일괄 처리 서비스는 자동으로 hello hello 풀의 hello 계산 노드에서 실행 태스크를 예약 합니다. 각 작업 tooprocess hello 입력된 파일을 업로드 하는 hello 응용 프로그램을 사용 합니다.
   
   * 4a. 작업이 실행 되기 전에 hello 데이터 (hello 입력된 파일)에 할당 된 tooprocess toohello 계산 노드를 다운로드할 수 있습니다. 경우 hello 응용 프로그램에 아직 설치 하지 hello 노드 (2 단계 참조)을 다운로드할 수 있습니다 여기 대신 합니다. Hello 다운로드 완료 되 면 자신의 할당 된 노드에서 hello 작업을 실행 합니다.
5. 실행 하는 hello 작업와 hello 작업 및 작업의 일괄 처리 toomonitor hello 진행률을 쿼리할 수 있습니다. 클라이언트 응용 프로그램 또는 서비스는 HTTPS를 통해 hello 일괄 처리 서비스와 통신합니다. 수천 대에서 수천 개의 계산 노드가 실행 되는 작업 모니터링 하 고 수, 때문에 반드시 너무[hello 일괄 처리 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md)합니다.
6. Hello 작업을 완료의 결과 데이터 tooAzure 저장소에 업로드할 수 있습니다. 또한 계산 노드에 대해 hello 파일 시스템에서 직접 파일을 검색할 수 있습니다.
7. 모니터링 프로그램을 감지 하면 작업 hello 작업이 완료 되었을 클라이언트 응용 프로그램이 나 서비스에 추가 처리 또는 평가 대 한 hello 출력 데이터를 다운로드할 수 있습니다.

보관이 한 가지 방법은 toouse 일괄 처리에 주의 하 고이 시나리오는 사용 가능한 기능 중 일부에 설명 합니다. 예를 들어 실행할 수 있습니다 [동시에 여러 작업](batch-parallel-node-tasks.md) 각 노드를 계산 하 고 사용할 수 있습니다 [준비 및 완료 작업을 작업](batch-job-prep-release.md) tooprepare hello 노드 작업을 위한 다음 나중에 정리 합니다.

## <a name="next-steps"></a>다음 단계
시간 toodig 깊은 toolearn hello 일괄 처리 서비스에 대 한 고급 개요를가지고 있기 수 사용법 tooprocess 계산 집약적인 병렬 작업입니다.

* 읽기 hello [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), toouse 일괄 처리를 준비 하 고 모든 사용자에 대 한 필수 정보입니다. hello 문서 풀, 노드, 작업 및 작업, 및 hello와 같은 일괄 처리 서비스 리소스에 대 한 자세한 내용은 일괄 처리 응용 프로그램을 작성 하는 동안 사용할 수 있는 많은 API 기능을 포함 합니다.
* Hello에 대 한 자세한 내용은 [일괄 처리 Api와 도구](batch-apis-tools.md) 일괄 처리 솔루션을 만드는 데 사용할 수 있습니다.
* [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md) toolearn 어떻게 toouse C# hello 일괄 처리.NET 라이브러리 tooexecute 단순 작업 일반 일괄 처리 워크플로 사용 하 고 있습니다. 이 문서를 사용 하면 첫 번째 중단할 toouse 일괄 처리 서비스 hello 하는 방법을 학습 하는 동안 중 하나 여야 합니다. 또한 한 [Python 버전](batch-python-tutorial.md) hello 자습서입니다.
* Hello 다운로드 [코드 샘플 GitHub에서] [ github_samples] toosee C# 및 Python 일괄 처리 tooschedule 및 프로세스 샘플 작업 부하와 상호 작용할 수 있는 방법입니다.
* 체크 아웃 hello [일괄 학습 경로] [ learning_path] 일괄 처리와 toowork tooget hello 때 사용할 수 있는 tooyou 리소스의 개념에 알아봅니다.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
