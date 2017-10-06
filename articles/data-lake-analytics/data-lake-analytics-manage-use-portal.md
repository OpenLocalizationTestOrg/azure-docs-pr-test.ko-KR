---
title: "사용 하 여 Azure Data Lake 분석 aaaManage hello Azure 포털 | Microsoft Docs"
description: "자세한 내용은 toomanage Data Lake 분석 계정, 데이터 원본, 사용자와 작업 하는 방법입니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Azure 포털 hello를 사용 하 여 Azure 데이터 레이크 분석 관리
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

어떻게 toomanage Azure Data Lake 분석 계정, 데이터 소스 계정, 사용자 및 사용 하 여 작업 hello Azure 포털에 알아봅니다. 다른 도구를 사용 하는 방법에 대 한 관리 항목 toosee hello hello 페이지 위쪽에 있는 탭을 클릭 합니다.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Data Lake Analytics 계정 관리

### <a name="create-an-account"></a>계정 만들기

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기** > **인텔리전스 + 분석** > **Data Lake Analytics**를 클릭합니다.
3. 다음 항목 hello에 대 한 값을 선택 합니다. 
   1. **이름**: hello 이름 hello Data Lake 분석 계정입니다.
   2. **구독**: hello hello 계정에 사용 되는 Azure 구독.
   3. **리소스 그룹**: toocreate hello 계정에 hello Azure 리소스 그룹입니다. 
   4. **위치**: hello hello Data Lake 분석 계정에 대 한 Azure 데이터 센터입니다. 
   5. **데이터 레이크 저장소**: hello Data Lake 분석 계정에 사용 되는 기본 저장소 toobe hello 합니다. hello Azure 데이터 레이크 저장소 계정 및 hello Data Lake 분석 계정에 있어야 합니다. 동일한 위치를 hello 합니다.
4. **만들기**를 클릭합니다. 

### <a name="delete-a-data-lake-analytics-account"></a>Data Lake Analytics 계정 삭제

Data Lake Analytics 계정을 삭제하기 전에 먼저 해당 기본 Data Lake Store 계정을 삭제합니다.

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **삭제**를 클릭합니다.
3. 형식 hello 계정 이름입니다.
4. **삭제**를 클릭합니다.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>데이터 원본 관리

Data Lake 분석 데이터 원본 hello를 지원 합니다.

* 데이터 레이크 저장소
* Azure 저장소

데이터 탐색기 toobrowse 데이터 원본을 사용 하 고 기본 파일 관리 작업을 수행할 수 있습니다. 

### <a name="add-a-data-source"></a>데이터 원본 추가

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **데이터 원본**을 클릭합니다.
3. **데이터 원본 추가**를 클릭합니다.
    
   * 데이터 레이크 저장소 계정 tooadd 해야 hello 계정 이름과 액세스 toohello toobe 수 tooquery 계정 것입니다.
   * Azure Blob 저장소 tooadd hello 저장소 계정 및 계정 키 hello 해야합니다. toofind hello 포털에서 저장소 계정의 toohello 이동 합니다.

## <a name="set-up-firewall-rules"></a>방화벽 규칙 설정

데이터 레이크 분석 toofurther 잠금 액세스 tooyour Data Lake 분석 계정 hello 네트워크 수준에서 사용할 수 있습니다. 방화벽을 사용하도록 설정하고 IP 주소를 지정하거나 신뢰할 수 있는 클라이언트에 대한 IP 주소 범위를 정의할 수 있습니다. 이러한 측정값을 사용 하도록 설정 하면 범위에 정의 된 hello hello IP 주소를가지고 있는 클라이언트만 toohello 저장소를 연결할 수 있습니다.

다른 Azure 서비스에서 Azure 데이터 팩터리 또는 Vm을 toohello Data Lake 분석 계정에 연결 되어 있는지 확인 **Azure 서비스 허용** 꺼져 **에**합니다. 

### <a name="set-up-a-firewall-rule"></a>방화벽 규칙 설정

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. Hello hello 왼쪽 메뉴에서 클릭 **방화벽**합니다.

## <a name="add-a-new-user"></a>새 사용자 추가

Hello를 사용할 수 있습니다 **사용자 추가 마법사** tooeasily 새 데이터 레이크 사용자를 프로 비전 합니다.

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. 왼쪽 아래에서 hello에 **시작**, 클릭 **사용자 추가 마법사**합니다.
3. 사용자를 선택한 다음 **선택**을 클릭합니다.
4. 역할을 선택한 다음 **선택**을 클릭합니다. 새 개발자 toouse 선택 hello Azure 데이터 레이크를 tooset **데이터 레이크 분석 개발자** 역할입니다.
5. Hello U SQL 데이터베이스에 대 한 hello 액세스 제어 목록 (Acl)을 선택 합니다. 선택 사항에 만족하면 **선택**을 클릭합니다.
6. 파일에 대 한 hello Acl을 선택 합니다. Hello 기본 저장소에 대 한 hello 루트 폴더에 대 한 hello Acl를 변경 하지 않는 "/" 및 hello/시스템 폴더에 대 한 합니다. **선택**을 클릭합니다.
7. 선택한 변경 내용을 모두 검토한 다음 **실행**을 클릭합니다.
8. Hello 마법사가 완료 되 면 클릭 **수행**합니다.

## <a name="manage-role-based-access-control"></a>역할 기반 액세스 제어 관리

다른 Azure 서비스와 마찬가지로 사용자가 어떻게 상호 작용 하는 역할 기반 액세스 제어 (RBAC) toocontrol hello 서비스와 함께 사용할 수 있습니다.

hello 표준 RBAC 역할 기능을 수행 하는 hello를 갖습니다.
* **소유자**: 수 작업 제출, 작업을 모니터링, 모든 사용자의 작업을 취소 하 고 hello 계정을 구성 합니다.
* **참가자**: 수 작업 제출, 작업을 모니터링, 모든 사용자의 작업을 취소 하 고 hello 계정을 구성 합니다.
* **독자**: 작업을 모니터링할 수 있습니다.

Hello 데이터 레이크 분석 개발자 역할 tooenable U-SQL 개발자 toouse hello Data Lake 분석 서비스를 사용 합니다. Hello 데이터 레이크 분석 개발자 역할을 사용할 수 있습니다.
* 작업을 제출합니다.
* 모든 사용자가 제출한 작업의 작업 상태 및 hello 진행률을 모니터링 합니다.
* 모든 사용자가 제출 하는 작업에서 hello U-SQL 스크립트를 참조 하십시오.
* 자신의 작업만을 취소합니다.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>사용자 또는 보안 그룹 tooa Data Lake 분석 계정 추가

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **액세스 제어(IAM)** > **추가**를 클릭합니다.
3. 원하는 역할을 선택합니다.
4. 사용자를 추가합니다.
5. **확인**을 클릭합니다.

>[!NOTE]
>사용자 또는 보안 그룹 toosubmit 작업을 필요한 경우 hello 저장소 계정에 대 한 권한이 해야 합니다. 자세한 내용은 [Data Lake Store에 저장된 데이터 보호](../data-lake-store/data-lake-store-secure-data.md)를 참조하세요.
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>작업 관리

### <a name="submit-a-job"></a>작업 제출

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.

2. **새 작업**을 클릭합니다. 각 작업에 대해 다음을 구성합니다.

    1. **작업 이름**: hello 작업의 hello 이름입니다.
    2. **우선 순위**: 숫자가 낮을수록 우선 순위가 높습니다. 두 개의 작업이 대기 중인 경우 hello 하나 더 낮은 우선 순위 값을 먼저 실행 됩니다.
    3. **병렬 처리 수준**:이 작업에 대 한 tooreserve를 처리 하는 hello 최대 수를 계산 합니다.

3. **작업 제출**을 클릭합니다.

### <a name="monitor-jobs"></a>작업 모니터링

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **모든 작업 보기**를 클릭합니다. Hello 계정에서 모든 hello 활성 상태이 고 최근에 완료 된 작업의 목록이 표시 됩니다.
3. 필요에 따라 **필터** 하 여 hello 작업을 찾을 toohelp **시간 범위**, **작업 이름**, 및 **작성자** 값입니다. 

### <a name="monitoring-pipeline-jobs"></a>파이프라인 작업 모니터링
파이프라인의 일부인 작업도 tooaccomplish 특정 시나리오 함께, 일반적으로 순차적으로 작동 합니다. 예를 들어, 고객 정보의 사용을 정리, 추출, 변환, 집계하는 파이프라인을 사용할 수 있습니다. 파이프라인 작업이 hello 작업이 제출 된 경우 hello "파이프라인" 속성을 사용 하 여 식별 됩니다. ADF V2를 사용하여 예약된 작업에는 이 속성이 자동으로 포함됩니다. 

파이프라인의 일부인 U-SQL 작업 목록이 tooview: 

1. Azure 포털 hello tooyour Data Lake 분석 계정 이동 합니다.
2. **작업 정보**를 클릭합니다. "모든 작업이" 탭 기본값은 실행 중, 목록을 보여 주는 hello 큐에 대기 하 고 작업을 종료 합니다.
3. Hello 클릭 **파이프라인 작업** 탭 합니다. 파이프라인 작업 목록에 각 파이프라인에 대해 집계된 통계가 함께 표시됩니다.

### <a name="monitoring-recurring-jobs"></a>되풀이 작업 모니터링
Hello 된 되풀이 작업은 동일한 비즈니스 논리는 하지만 서로 다른 입력된 데이터를 사용 될 때마다 실행 됩니다. 이상적으로 되풀이 작업 항상 성공 하 고 실행 시간이 상대적으로 안정적인; 이러한 동작은 모니터링 hello 작업은 정상 상태를 확인 하는 데 도움이 됩니다. 되풀이 작업 hello "Recurrence" 속성을 사용 하 여 식별 됩니다. ADF V2를 사용하여 예약된 작업에는 이 속성이 자동으로 포함됩니다.

tooview U-SQL 작업 되풀이 되는 목록: 

1. Azure 포털 hello tooyour Data Lake 분석 계정 이동 합니다.
2. **작업 정보**를 클릭합니다. "모든 작업이" 탭 기본값은 실행 중, 목록을 보여 주는 hello 큐에 대기 하 고 작업을 종료 합니다.
3. Hello 클릭 **되풀이 작업** 탭 합니다. 되풀이 작업 목록에 각 되풀이 작업에 대해 집계된 통계가 함께 표시됩니다.

## <a name="manage-policies"></a>정책 관리

### <a name="account-level-policies"></a>계정 수준 정책

이러한 정책은 tooall 작업 Data Lake 분석 계정에 적용 됩니다.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Data Lake Analytics 계정의 최대 AU 수
정책은 hello Data Lake 분석 계정 צ ְ ײ 분석 단위 (AUs)의 총 수를 제어 합니다. 기본적으로 hello 값 too250을 설정 됩니다. 예를 들어이 값은 too250 AUs 설정, 있습니다 있으면 250 할당 AUs tooit를 실행 하는 하나의 작업 또는 25와 실행 중인 10 작업 AUs 각 합니다. 전송 된 작업을 추가로 hello 실행 중인 작업이 완료 될 때까지 대기 합니다. Hello 높아질 AUs 실행 중인 작업이 완료 되 면 작업 toorun 큐에 대기 합니다.

toochange hello 수 AUs Data Lake 분석 계정에 대 한:

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **속성**을 클릭합니다.
3. 아래 **최대 AUs**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다. 
4. **Save**를 클릭합니다.

> [!NOTE]
> 기본 (250) hello 하지 더 필요한 경우 AUs, hello 포털에서을 클릭 **도움말 + 지원** toosubmit 지원 요청. Data Lake 분석 계정에 사용할 수 있는 AUs hello 수를 늘릴 수 있습니다.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>동시에 실행될 수 있는 최대 작업 수
정책에서 제어 하는 작업 수 hello에 실행할 수 있습니다 동시 합니다. 기본적으로이 값 too20을 설정 됩니다. 데이터 레이크 분석 AUs 사용할 수 있으면 hello 실행 중인 작업의 총 수에는이 정책의 hello 값에 도달할 때까지 즉시 새 작업에 예약 된 toorun은입니다. Hello 동시에 실행할 수 있는 작업의 최대 수에 도달 하면 후속 작업 (AU 가용성)에 따라 하나 이상의 실행 중인 작업이 완료 될 때까지 우선 순위에 따라 대기 됩니다.

동시에 실행할 수 있습니다. 있는 작업 toochange hello 수:

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **속성**을 클릭합니다.
3. 아래 **실행 작업의 최대 수**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다. 
4. **Save**를 클릭합니다.

> [!NOTE]
> Toorun hello hello 포털에서 작업의 기본 (20) 번호 보다 클릭 더 필요한 경우 **도움말 + 지원** toosubmit 지원 요청. hello Data Lake 분석 계정에 동시에 실행할 수 있는 작업 수를 늘릴 수 있습니다.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>시간 tookeep 작업 메타 데이터 및 리소스 
U-SQL 작업을 실행 하는 사용자가 hello Data Lake 분석 서비스에 관련 된 모든 파일은 유지 합니다. 관련된 파일 hello U-SQL 스크립트를 hello U-SQL 스크립트, 컴파일된 리소스 및 통계에서 참조 하는 hello DLL 파일을 포함 합니다. hello 파일이 hello 기본 Azure 데이터 레이크 저장소 계정의 hello /system/ 폴더에 있습니다. 이 정책은 이러한 리소스를 자동으로 삭제 되기 전에 저장 되는 기간을 제어 (hello 기본값은 30 일)입니다. 디버깅을 위해 및 hello 향후에 다시 실행할 수 있는 작업의 성능 튜닝에 이러한 파일을 사용할 수 있습니다.

toochange 시간 tookeep 작업 메타 데이터 및 리소스:

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **속성**을 클릭합니다.
3. 아래 **일 tooRetain 작업 쿼리**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다.  
4. **Save**를 클릭합니다.

### <a name="job-level-policies"></a>작업 수준 정책
작업 수준 정책을 사용 하 여 제어할 수 있습니다 최대 AUs hello 및 hello 개별 사용자 (또는 특정 보안 그룹의 구성원) 전송 하는 작업에 설정할 수 있는 최대 우선 순위입니다. 사용자가 발생 하는 hello 비용을 제어할 수이 있습니다. 수도 있습니다 우선 순위가 높은 예약 된 작업을 제어 hello 효과 미칠 수에서 실행 되는 프로덕션 작업 hello 동일한 Data Lake 분석 계정.

Data Lake 분석 hello 작업 수준에서 설정할 수 있는 두 가지 정책에 있습니다.

* **작업당 AU 제한**: 사용자가 AUs toothis 수를 가진 작업을 제출할 수 있습니다. 기본적으로이 한도 hello AU 상한 hello 계정에 대 한 동일한 hello 됩니다.
* **우선 순위**: 사용자가 우선 순위 보다 낮거나 toothis 값을 가진 작업을 제출할 수 있습니다. 숫자가 높을수록 우선 순위가 낮습니다. 기본적으로이 설정은 too1, hello 가능한 우선 순위가 가장 높은 인 합니다.

모든 계정에는 설정된 기본 정책이 있습니다. hello 기본 정책은 hello 계정의 tooall 사용자가 적용 됩니다. 특정 사용자 및 그룹에 대한 추가 정책을 설정할 수 있습니다. 

> [!NOTE]
> 계정 수준 정책 및 작업 수준 정책은 동시에 적용됩니다.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>특정 사용자 또는 그룹에 대한 정책 추가

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **속성**을 클릭합니다.
3. 아래 **작업 제출 제한**, hello 클릭 **정책 추가** 단추입니다. 그런 다음 선택 하거나 hello 설정을 다음을 입력 합니다.
    1. **정책 이름 계산**: tooremind 정책 이름을 입력 하면 hello 정책의 hello 목적입니다.
    2. **사용자 또는 그룹 선택**: hello 사용자 또는이 정책이 적용 되는 그룹을 선택 합니다.
    3. **Hello 작업 AU 제한 설정**: toohello 적용 되는 hello AU 제한 설정 사용자 또는 그룹을 선택 합니다.
    4. **우선 순위 제한 hello 설정**: hello 우선 순위 제한 설정 toohello 적용 되는 사용자 또는 그룹 선택 합니다.

4. **Ok**를 클릭합니다.

5. 새 정책 hello hello에 나열 된 **기본** 정책 테이블 **작업 제출 제한**합니다. 

#### <a name="delete-or-edit-an-existing-policy"></a>기존 정책 삭제 또는 편집

1. Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.
2. **속성**을 클릭합니다.
3. 아래 **작업 제출 제한**, tooedit 원하는 찾기 hello 정책입니다.
4.  toosee hello **삭제** 및 **편집** hello hello 테이블의 맨 오른쪽 열에 해당 하는 옵션을 클릭 **중...** .

### <a name="additional-resources-for-job-policies"></a>정책 작업에 대한 추가 리소스
* [Policy overview blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)(정책 개요 블로그 게시물)
* [Account-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)(계정 수준 정책 블로그 게시물)
* [Job-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)(작업 수준 정책 블로그 게시물)

## <a name="next-steps"></a>다음 단계

* [Azure Data Lake Analytics 개요](data-lake-analytics-overview.md)
* [데이터 레이크 분석 hello Azure 포털을 사용 하 여 시작](data-lake-analytics-get-started-portal.md)
* [Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-powershell.md)

