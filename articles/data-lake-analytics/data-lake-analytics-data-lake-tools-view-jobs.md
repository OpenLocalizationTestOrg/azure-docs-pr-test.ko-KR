---
title: "aaaUse 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Azure Data Lake Analytics 작업용 작업 브라우저 및 작업 보기 사용
hello Azure Data Lake 분석 서비스 아카이브 제출한 작업에는 [쿼리 저장소](#query-store)합니다. 이 문서에서는 toouse 작업 브라우저와 Visual Studio toofind hello 기록에 대 한 Azure 데이터 레이크 Tools의 작업 보기 정보 작업 방법을 배웁니다. 

기본적으로 hello Data Lake 분석 서비스는 hello 작업 30 일 동안 보관합니다. 사용자 지정 하는 hello 만료 정책을 구성 하 여 hello Azure 포털에서에서 hello 만료 기간을 구성할 수 있습니다. 만료 된 후 수 tooaccess hello 작업 정보 되지 않습니다. 

## <a name="prerequisites"></a>필수 조건
[Data Lake Tools for Visual Studio 필수 구성 요소](data-lake-analytics-data-lake-tools-get-started.md#prerequisites)를 참조하세요.

## <a name="open-hello-job-browser"></a>Hello 작업 브라우저를 열으십시오
액세스를 통해 작업 브라우저 hello **서버 탐색기 > Azure > Data Lake 분석 > 작업** Visual Studio에서.  Hello 작업 브라우저를 사용 하 여 hello 쿼리 저장소는 Data Lake 분석 계정에 액세스할 수 있습니다. 작업 브라우저 쿼리 저장소에서 표시 hello, 기본 작업 정보를 표시 하 고 자세한 작업 정보에 hello 오른쪽 보여 주는 작업 보기.

## <a name="job-view"></a>작업 보기
작업 보기를 보여 줍니다 hello 작업의 세부 정보입니다. 작업을 tooopen hello 작업 브라우저에서에서 작업을 두 번 클릭 하거나 작업 보기를 클릭 하 여 hello 데이터 레이크 메뉴에서 열 수 있습니다. Hello 작업 URL로 채워진 대화 상자가 표시 됩니다.

![Data Lake Tools Visual Studio 작업 브라우저](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

작업 보기에 포함된 내용은 다음과 같습니다.

* 작업 요약
  
    Hello 작업 보기를 새로 고침 toosee hello 실행 중인 작업의 정보를 보다 최신입니다.
  
  * 작업 그래프(그래프):
    
      작업 상태는 hello 작업 단계를 설명합니다.
    
      ![Azure Data Lake Analytics 작업 단계 상태](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * 준비: 스크립트 toohello 클라우드, 컴파일 및 최적화 hello 컴파일 서비스를 사용 하 여 hello 스크립트를 업로드 합니다.
    * 큐에 넣은: 작업은 충분 한 리소스에 대 한 대기 중인 큐에 대기 중인된 whey 또는 hello 작업 계정 제한 당 최대 동시 작업 hello를 초과 합니다. hello 우선 순위 설정은 대기 중인된 작업-낮은 hello 수치로 hello hello hello 커지게의 hello 순서를 결정합니다.
    * 실행 중: hello 작업은 실제로 Data Lake 분석 계정에서 실행 됩니다.
    * 완료 하는 중: hello 작업 (예: hello 파일을 완료 하는 중) 완료 됩니다.
      
      hello 작업은 모든 단계에서 실패할 수 있습니다. 예를 들어, 컴파일 오류 hello 준비 단계, hello 큐 대기 단계에서 시간 초과 오류 및 등 hello 실행 단계에서 실행 오류가 발생 합니다.
  * 기본 정보
    
      hello 기본 작업 정보 hello hello 작업 요약 패널의 아래쪽에 표시 됩니다.
    
      ![Azure Data Lake Analytics 작업 단계 상태](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * 작업 결과: 성공 또는 실패입니다. 모든 단계 hello 작업이 실패할 수 있습니다.
    * 총 기간: 제출 시간과 종료 시간 간 벽시계 시간(기간)입니다.
    * 계산 시간 총: hello 총 모든 꼭 짓 점 실행 시간을 고려할 수 있습니다 hello 시간 hello 작업으로 실행 되 하나만 꼭 짓 점. TooTotal 꼭지점 toofind 정점에 대 한 자세한 내용은 참조 하십시오.
    * 전송/시작/종료 시간: hello 시간 hello Data Lake 분석 서비스 작업 제출/시작 toorun hello를 받을 때 작업/끝 hello 작업 성공 여부에 있습니다.
    * 실행 중 컴파일/대기 /: hello 준비/대기 중/실행 단계 중에 소요 된 벽 시계 시간입니다.
    * 계정: hello Data Lake 분석 계정 hello 작업 실행에 사용 됩니다.
    * 작성자: hello 제출한 사용자의 hello 작업 실제 사용자 계정 또는 시스템 계정일 수 있습니다.
    * 우선 순위: hello hello 작업의 우선 순위입니다. hello 낮은 hello 수치로 hello hello 우선 순위가 높습니다. Hello 큐에 있는 hello 작업 hello 순서를만 영향을 줍니다. 높은 우선 순위를 설정할 경우 실행 중인 작업을 선취하는 것은 아닙니다.
    * 병렬 처리 수준: hello 동시 Azure 데이터 레이크 분석 단위 (ADLAUs) 즉, 꼭 짓 점의 최대 수를 요청 했습니다. 현재 한 꼭 짓 점에 같은 tooone VM 2 대 가상 코어와 6 개의 g B RAM으로,이 업그레이드 될 수 있지만 나중에 데이터 레이크 분석 업데이트 합니다.
    * Toobe hello 작업이 완료 될 때까지 처리 필요로 하는 바이트: 남아 있는 바이트입니다.
    * 읽기/쓰기 바이트: 읽기/쓰기 이후 되었다면 hello 작업 실행을 시작 하는 바이트입니다.
    * 꼭 짓 점을 총: hello 작업은 대부분의 작업 들 나뉘어져, 각 작업에는 꼭 짓 점 라고 합니다. 이 값은 작업 단위 hello 작업으로 구성 합니다. 꼭짓점은 기본 처리 단위, 즉, ADLAU(Azure Data Lake Analytics Unit)와 같으며 꼭짓점은 병렬로 실행할 수 있습니다. 
    * 완료 된/실행/실패: hello 꼭지점 완료/실행/실패의 수입니다. 꼭 짓 점을 tooboth 사용자 코드 및 시스템 오류 인해 실패할 수 있습니다 하지만 hello 시스템 재시도가 여러 번 자동으로 꼭지점 실패 했습니다. Hello 꼭지점은 여전히 다시 시도한 후 실패 한 경우 hello 전체 작업이 실패 합니다.
* 작업 그래프
  
    U-SQL 스크립트 입력된 데이터 toooutput 데이터 변환의 hello 논리를 나타냅니다. hello 스크립트 컴파일되고 hello 준비 단계에서 tooa 실제 실행 계획을 최적화 합니다. 작업 그래프는 tooshow hello 실제 실행 계획 합니다.  다음 다이어그램 hello hello 프로세스를 보여줍니다.
  
    ![Azure Data Lake Analytics 작업 단계 상태](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    작업(Job)은 여러 작업(Work)으로 세분화됩니다. 각 작업(Work)을 꼭짓점이라고 합니다. hello 꼭 짓 점은 꼭 짓 점 슈퍼 (즉, 단계)로 그룹화 되 고 작업 그래프도 시각화 합니다. hello 작업 그래프에서 hello 녹색 단계 placards hello 단계를 보여 줍니다.
  
    Hello를 수행 하는 단계에서 모든 꼭 동일한 종류의 동일 하 게 작동 hello의 다양 한 요소와 데이터입니다. 예를 들어 한 TB 데이터에 파일이 있고 여기에서 읽은 꼭짓점이 수백 개 있을 경우 각 꼭짓점은 청크를 읽습니다. Hello 그룹화 되는 해당 꼭 짓 동일한 단계와 동일 수행 동일한 입력된 파일의 여러 부분에 대해 작동 합니다.
  
  * <a name="state-information"></a>단계 정보
    
      특정 단계에서 일부 숫자 hello 게시에 표시 됩니다.
    
      ![Azure Data Lake Analytics 작업 그래프 단계](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 추출: hello 이름 수와 hello 작업 방법으로 명명 된 단계입니다.
    * 84 꼭지점:이 단계에서 꼭 짓 점의 총 개수를 hello 합니다. hello 그림의 작업 수가 들이이 단계에서 나누어져 보여 줍니다.
    * 12.90 s/꼭 짓 점:이 단계에 대 한 평균 꼭 짓 점 실행 시간 hello 합니다. 이 수치는 SUM(전체 꼭짓점 실행 시간)을 (전체 꼭짓점 수)로 나누어 계산합니다. 즉, 12.90에 hello 전체 단계 완료 병렬 처리 수준에서 실행 되는 모든 hello 꼭지점 할당 수, 하는 경우 s입니다. 또한 모든 hello에서 작업 하는 경우이 단계를 순차적으로 수행 됩니다, hello 비용 #vertices 것 의미 * 평균 시간입니다.
    * 850,895개 행 기록: 이 단계에서 기록한 총 행 수입니다.
    * R/W: 이 단계에서 읽거나 쓴 총 데이터의 양입니다(바이트).
    * Colors: 색 hello 단계 tooindicate 다른 꼭 짓 점 상태에 사용 됩니다.
      
      * 녹색은 hello 꼭 짓 점 성공 했는지를 나타냅니다.
      * 주황색은 hello 꼭지점을 다시 시도 나타냅니다. 다시 시도 하는 hello 꼭지점에 실패 했습니다 자동으로 다시 시도 있고 성공적으로 hello 시스템과 hello 전체 단계 성공적으로 완료 된 합니다. Hello 꼭 짓 점 아직 못했습니다 다시 시도 표시 되지만 hello 색 빨간색과 hello 전체 작업 실패를 설정 합니다.
      * 빨간색 실패를 나타냅니다. 즉, 특정 꼭 짓 점 되었습니다 hello 시스템에서 몇 번 다시 시도 수 있었지만 여전히 실패 합니다. 이 시나리오에는 전체 작업 toofail hello 하면 됩니다.
      * 파란색은 특정 꼭짓점이 실행 중임을 의미합니다.
      * 흰색 나타냅니다 hello 꼭 짓 점 대기 중입니다. hello 꼭 짓 점 대기 toobe는 ADLAU를 사용할 수 있게 하거나 입력된 데이터 준비 되어 있지 있으므로 입력에 대 한 대기 중일 수 있습니다 예약 될 수 있습니다.
      
      하나의 상태에서 마우스 커서를 이동 하 여 hello 단계에 대 한 자세한 정보를 얻을 수 있습니다.
      
      ![Azure Data Lake Analytics 작업 그래프 단계 세부 정보](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * 꼭 짓 점을: 예를 들면 개수 꼭지점 합계, 개수 꼭지점 완료 되 면에 실패 했거나 실행/대기 중, 등 여전히은 hello 꼭지점 세부 정보를 설명 합니다.
  * 포드 전체/내부 포드에서 읽은 데이터: 파일과 데이터가 분산된 파일 시스템의 여러 포드에 저장됩니다. 여기에서 값 hello pod 같거나 pod 교차 hello의 읽을 데이터의 양을 설명 합니다.
  * 계산 시간 총: hello 합계 hello 단계에서 모든 꼭 짓 점 실행 시간을 고려할 수 있는 것 hello 시간 hello 단계도 작동 하는 경우 수행 되는 것이 하나의 꼭지점에 실행 될 때입니다.
  * 데이터 및 행 작성/read: 얼마나 데이터 또는 행 읽기/쓰기 낮거나 toobe 필요 나타냅니다 읽기입니다.
  * 꼭짓점 읽기 실패 수: 데이터를 읽는 중 실패한 꼭짓점의 수에 대해 설명합니다.
  * 중복 된 꼭 짓 점 무시: hello 시스템 여러 꼭 짓 점을 꼭 짓 점 성능을 향상 시키는, 하는 경우 예약 될 수 있습니다 toorun hello 동일한 작업입니다. Reductant 꼭지점 hello 꼭 짓 점 중 하나를 성공적으로 완료 되 면 삭제 됩니다. 꼭 짓 점 중복 레코드 hello 수의 중복으로 hello 단계에서 삭제 되는 꼭 삭제 합니다.
  * 꼭 짓 점 해지: hello 꼭 짓 점이 성공 했지만 가져오기 toosome 이유로 인해 나중에 다시 실행 합니다. 예를 들어 중간 입력된 데이터를 손실 하는 다운스트림 꼭 짓 점, hello 업스트림 꼭 짓 점 toorerun을 라는 나타납니다.
  * 꼭 짓 점 일정 실행: hello 꼭지점 예정 된 hello 총 시간입니다.
  * 읽을 최대/최소/평균 꼭 짓 점 데이터: hello 최소/평균/최대 모든 꼭 짓 점 데이터를 읽습니다.
  * 기간: hello 벽 시계 시간 단계를 사용 하면 tooload 프로필 toosee이이 값이 필요 합니다.
  * 작업 재생
    
      Data Lake 분석 작업을 실행 하 고 아카이브 hello hello 꼭지점 시작 되는 때와 같은 hello 작업의 정보를 실행 하는 꼭 짓 점을 중지 실패 했으며 다시 어떻게 등입니다. Hello 쿼리 저장소에 기록 되 고 해당 작업 프로필에 저장 된 자동으로 모든 hello 정보입니다. 작업 보기에서 "부하 프로필"을 통해 작업 프로필 hello를 다운로드할 수 있습니다 및 hello 작업 프로필을 다운로드 한 후 작업 재생 hello를 볼 수 있습니다.
    
      작업 재생은 epitome 시각화 hello 클러스터에서 발생 한 일입니다. 작업 실행 진행률을 보고 매우 짧은 시간(일반적으로 30초 미만) 동안의 성능 이상과 병목 현상을 시각적으로 감지할 수 있습니다.
  * 작업 열 지도 표시 
    
      작업 그래프에서 hello 디스플레이 드롭다운을 통해 작업 열 지도 선택할 수 있습니다. 
    
      ![Azure Data Lake Analytics 작업 그래프 열 지도 표시](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      작업을 통해 hello 작업 대부분 hello의 자주 사용 되는 작업의 한 I/O 경계 작업 인지 또는 찾아 수 등의 hello I/O, 시간 및 처리량 열 지도 표시 합니다.
    
      ![Azure Data Lake Analytics 작업 그래프 열 지도 예](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * 진행률: 작업 실행 진행률 hello에 대 한 정보를 참조 하십시오 [정보 단계](#stage-information)합니다.
    * 읽기/쓰기 데이터: 각 단계에서 읽기/쓰기 총 데이터의 열 지도 hello 합니다.
    * 계산 시간: SUM (꼭지점 실행 시간 마다)의 hello 열 지도 고려할 수 있는이 걸리는 시간 1 꼭 짓 점으로 hello 단계에서 모든 작업을 실행 하는 방식입니다.
    * 노드당 평균 실행 시간: SUM (꼭지점 실행 시간 마다)의 hello 열 지도 / (꼭 짓 점 수)입니다. 즉, 전체 단계 hello 병렬 처리 수준에서 실행 되는 모든 hello 꼭지점 할당 수, 하는 경우이 시간 내에 수행 됩니다.
    * 입/출력 처리: hello 열 지도의 각 단계 입/출력 처리량의 경우 사용자 작업은이 통해 I/O 바운드 작업 하는 경우을 확인할 수 있습니다.
* 메타데이터 작업
  
    U-SQL 스크립트에서 데이터베이스 만들기, 테이블 삭제 등의 일부 메타데이터 작업을 수행할 수 있습니다. 이러한 작업은 컴파일 후 메타데이터 작업에 표시됩니다. 여기에서 어설션을 찾고 엔터티를 만들거나 삭제할 수 있습니다.
  
    ![Azure Data Lake Analytics 작업 보기 메타데이터 작업](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* 상태 기록
  
    작업 요약에서 hello 상태 기록 표시도 있지만 여기에서 자세한 내용을 확인할 수 있습니다. 자세한 hello를 찾을 수 있습니다 hello 작업을 준비 하는 경우 같은 정보가 큐에 대기 실행이 시작, 종료 되었습니다. 또한 hello 작업이 컴파일 실패 한 횟수를 찾을 수 있습니다 (CcsAttempts hello: 1)은 때 실제로 hello 작업 디스패치 된 toohello 클러스터 (hello 세부 정보: 디스패치 작업 toocluster) 등입니다.
  
    ![Azure Data Lake Analytics 작업 보기 상태 기록](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* 진단
  
    hello 도구 작업 실행을 자동으로 진단합니다. 작업에 오류 또는 성능 문제가 있으면 경고가 표시됩니다. Toodownload 프로필 tooget 전체 정보 여기 해야 note 하십시오. 
  
    ![Azure Data Lake Analytics 작업 보기 진단](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * 경고: 여기에 컴파일러 경고와 함께 경고가 표시됩니다. Hello 경고가 표시 되 면 자세한 내용을 보려면 "x 문제" 링크 toohave을 클릭할 수 있습니다.
  * 꼭짓점이 너무 오래 실행됨: 꼭짓점 시간이 부족할 경우(예: 5시간) 여기에서 문제를 확인할 수 있습니다.
  * 리소스 사용: 필요한 것보다 많거나 적은 병렬 처리를 할당한 경우 여기에서 문제를 확인할 수 있습니다. 리소스 사용 현황 toosee 자세히를 클릭 하 고 가상 시나리오 toofind 더 나은 리소스 할당을 수행할 수 또한 (자세한 내용은이 가이드 참조).
  * 메모리 검사: 5GB 이상의 메모리를 사용하는 꼭짓점이 있을 경우 여기에서 문제를 확인할 수 있습니다. 작업 실행이 시스템 한계보다 많은 메모리를 사용할 경우 시스템에 의해 중단될 수 있습니다.

## <a name="job-detail"></a>작업 세부 정보
작업 세부 정보 표시 hello, 스크립트, 리소스 및 꼭 짓 점 실행 보기를 포함 하 여 hello 작업의 자세한 정보.

![Azure Data Lake Analytics 작업 세부 정보](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* 스크립트
  
    hello hello 작업의 U-SQL 스크립트 hello 쿼리 저장소에 저장 됩니다. Hello 원래 U-SQL 스크립트를 볼 수 있으며 필요한 경우 다시 제출할 수 있습니다.
* 리소스
  
    리소스를 통해 hello 쿼리 저장소에 저장 된 hello 작업 컴파일 출력을 찾을 수 있습니다. 예를 들어, "algebra.xml"는 사용 되는 tooshow hello 등록 hello 어셈블리 등 여기 작업 그래프는 찾을 수 있습니다.
* Vertex 실행 보기
  
    꼭짓점 실행에 대한 세부 정보가 표시됩니다. 작업 프로필 hello 읽기/쓰기, 런타임, 상태 등 총 데이터와 같은 모든 꼭 짓 점 실행 로그를 보관 합니다. 이 보기를 통해 작업이 실행되는 방식에 대한 세부 정보를 확인할 수 있습니다. 자세한 내용은 참조 [꼭 짓 점 실행 보기 데이터 레이크 Tools for Visual Studio에서에서 사용 하 여 hello](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)합니다.

## <a name="next-steps"></a>다음 단계
* toolog 진단 정보 참조 [Azure Data Lake 분석에 대 한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)
* toosee 복잡 한 쿼리를 참조 [분석 웹 사이트 Azure 데이터 레이크 분석을 사용 하 여 로그](data-lake-analytics-analyze-weblogs.md)합니다.
* toouse 꼭 짓 점 실행 보기 참조 [사용 하 여 hello 데이터 레이크 Tools for Visual Studio에서에서 꼭 짓 점 실행 보기](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

