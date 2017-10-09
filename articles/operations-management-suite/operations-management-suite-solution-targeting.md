---
title: "OMS의 대상으로 aaaSolution | Microsoft Docs"
description: "솔루션 Targeting는에 OMS Operations Management Suite () toolimit 관리 솔루션 tooa 특정 에이전트 집합을 허용 하는 기능입니다.  이 문서에서는 설명 방법을 toocreate 범위 구성 tooa 솔루션을 적용 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Operations Management Suite (OMS)에서 tooscope 관리 솔루션 toospecific 에이전트 (미리 보기)를 대상으로 하는 솔루션을 사용 하 여
솔루션 tooOMS를 추가 하면 기본 tooall Windows 및 Linux 에이전트 연결된 tooyour 로그 분석 작업 영역에 의해 자동으로 배포 됩니다.  Tooa 특정 에이전트 집합을 제한 하 여 솔루션에 대 한 toomanage 프로그램 비용 및 제한 hello 양의 데이터 수집을 할 수 있습니다.  이 문서에서는 설명 방법을 toouse **솔루션을 대상으로** tooapply 범위를 허용 하는 OMS 기능 되 tooyour 솔루션입니다.

## <a name="how-tootarget-a-solution"></a>어떻게 tootarget 솔루션
있는 경우 3 단계 tootargeting 솔루션 hello 다음 섹션에에서 설명 된 대로  Note 다른 단계에 대 한 hello OMS 포털 및 hello Azure 포털 둘 다 필요 합니다.


### <a name="1-create-a-computer-group"></a>1. 컴퓨터 그룹 만들기
Hello 컴퓨터를 만들어 범위에서 tooinclude 한다는 것을 지정 된 [컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md) 로그 분석에서 합니다.  hello 컴퓨터 그룹을 로그 검색에 따라 또는 Active Directory 또는 WSUS 그룹 등의 다른 원본에서 가져올 수 있습니다. 으로 [아래에 설명 된](#solutions-and-agents-that-cant-be-targeted)직접 컴퓨터 연결 tooLog 분석 hello 범위에 포함 될 것만 필요 합니다.

Hello 컴퓨터 그룹 작업 영역에서 만든를 만든 후 다음 수에 포함 하 적용된 tooone 또는 많은 해결 될 수 있는 범위 구성 합니다.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. 범위 구성 만들기
 A **범위 구성** 하나 이상의 컴퓨터 그룹을 포함 하며 적용된 tooone 또는 많은 해결 될 수 있습니다. 
 
 다음 프로세스를 수행 하는 hello를 사용 하 여 범위 구성을 만듭니다.  

 1. Hello Azure 포털에서 탐색 너무**로그 분석** 작업 영역을 선택 합니다.
 2. Hello 작업 영역에 대 한 hello 속성에서 **작업 영역 데이터 원본** 선택 **범위 구성을**합니다.
 3. 클릭 **추가** toocreate 새 범위 구성 합니다.
 4. 입력 **이름** hello 범위 구성에 대 한 합니다.
 5. **컴퓨터 그룹 선택**을 클릭합니다.
 6. 만든 hello 컴퓨터 그룹 및 필요에 따라 다른 그룹 tooadd toohello 구성을 선택 합니다.  **선택**을 클릭합니다.  
 6. 클릭 **확인** toocreate hello 범위 구성 합니다. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Hello 범위 구성 tooa 솔루션을 적용 합니다.
있으면 범위 구성을 tooone 또는 많은 해결 적용할 수 있습니다.  단일 범위 구성을 여러 솔루션에서 사용할 수 있지만, 각 솔루션은 범위 구성을 하나만 사용할 수 있습니다.

다음 프로세스를 수행 하는 hello를 사용 하 여 범위 구성을 적용 합니다.  

 1. Hello Azure 포털에서 탐색 너무**로그 분석** 작업 영역을 선택 합니다.
 2. Hello 작업 영역에 대 한 hello 속성에서 선택 **솔루션**합니다.
 3. 클릭 tooscope hello 솔루션에서 원하는 합니다.
 4. Hello 솔루션에 대 한 hello 속성의 **작업 영역 데이터 원본** 선택 **솔루션을 대상으로**합니다.  Hello 옵션을 사용할 수 없는 경우 다음 [이 솔루션을 대상으로 지정할 수](#solutions-and-agents-that-cant-be-targeted)합니다.
 5. **범위 구성 추가**를 클릭합니다.  적용 된 구성을 toothis 솔루션이 이미 있는 경우 다음이 옵션은 사용할 수 없습니다.  추가 하기 전에 다른 hello 기존 구성을 제거 해야 합니다.
 6. 만든 hello 범위 구성을 클릭 합니다.
 7. 조사식 hello **상태** 표시 hello 구성 tooensure의 **Succeeded**합니다.  Hello 구성 및 선택의 hello 타원 toohello 오른쪽 클릭 hello 상태 오류가 나타나면 **편집 범위 구성** toomake 변경 합니다.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>대상으로 지정할 수 없는 솔루션 및 에이전트
다음은 에이전트와 솔루션을 대상으로 함께 사용할 수 없는 솔루션에 대 한 hello 기준입니다.

- 솔루션을 대상으로 tooagents 배포 toosolutions만 적용 됩니다.
- 솔루션을 대상으로 Microsoft에서 제공 하는 toosolutions만 적용 됩니다.  Toosolutions는 적용 되지 않습니다 [직접 만들거나 파트너 만든](operations-management-suite-solutions-creating.md)합니다.
- TooLog 분석에 직접 연결 하는 에이전트만 필터링 할 수 있습니다.  솔루션에서 자동으로 범위 구성에 포함 하는 지 여부는 연결 된 Operations Manager 관리 그룹의 일부인 tooany 에이전트를 배포 해야 합니다.

### <a name="exceptions"></a>예외
Hello로 솔루션을 대상으로 사용할 수 없습니다 명시 된 조건을 hello에 맞을 경우에 솔루션을 수행 합니다.

- 에이전트 상태 평가

## <a name="next-steps"></a>다음 단계
- 사용자 환경에서 사용할 수 있는 tooinstall 않는 hello 솔루션을 비롯 한 관리 솔루션에 대 한 자세한 [추가 Azure 로그 분석 관리 솔루션 tooyour 작업 영역](../log-analytics/log-analytics-add-solutions.md)합니다.
- [Log Analytics 로그 검색의 컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md)에서 컴퓨터 그룹 생성에 대해 자세히 알아보세요.