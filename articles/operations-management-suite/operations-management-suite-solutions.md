---
title: "Operations Management Suite (OMS)에서 aaaSolutions | Microsoft Docs"
description: "패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 솔루션을 고객 tootheir OMS 작업 영역을 추가할 수 있습니다.  이 문서에서는 고객 및 파트너가 사용자 지정 솔루션을 만드는 방법에 대한 세부 정보를 제공합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>OMS(Operations Management Suite)(미리 보기)에서 관리 솔루션 사용
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 관리 솔루션에 대한 예비 설명서입니다.    
> 
> 

패키지에 포함 된 관리 시나리오를 제공 하 여 hello 기능 Operations Management Suite (OMS)을 확장 하는 관리 솔루션을 고객 tootheir 환경에 추가할 수 있습니다.  또한 너무[Microsoft에서 제공 하는 솔루션](../log-analytics/log-analytics-add-solutions.md), 파트너 및 고객 관리 솔루션 toobe 자신의 환경에서 사용 되거나 hello 커뮤니티를 통해 사용할 수 있는 toocustomers 있게 만들 수 있습니다.

## <a name="finding-and-installing-management-solutions"></a>관리 솔루션 찾기 및 설치
찾기 및 hello 다음 섹션에에서 설명 된 대로 관리 솔루션을 설치 하기 위한 여러 메서드가 있습니다.

### <a name="azure-marketplace"></a>Azure 마켓플레이스
Microsoft에서 관리 솔루션을 제공 하 고 신뢰할 수 있는 파트너 hello Azure 포털에서에서 Azure 마켓플레이스 hello에서 설치할 수 있습니다.

1. Azure 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 창에서 선택 **더 많은 서비스**합니다.
3. 너무 아래로 스크롤하여 하나**솔루션** 또는 형식 *솔루션* hello에 **필터** 대화 상자.
4. Hello 클릭 **+ 추가** 단추입니다.
5. 를 찾아 중 하나에 관심이 있는 솔루션에 대 한 검색 hello를 클릭 하면 **필터** 단추 또는 hello에 입력 **검색 칸씩** 상자입니다.
6. 마켓플레이스 항목 tooview 해당 세부 정보를 클릭 합니다.
7. 클릭 **만들기** tooopen hello **솔루션 추가** 창.
8. Hello 같은 증명된 toorequired 정보 됩니다 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account) 또한 매개 변수에 대해 toovalues hello 솔루션입니다.
9. 클릭 **만들기** tooinstall hello 솔루션입니다.

### <a name="oms-portal"></a>OMS 포털
Microsoft에서 제공 하는 관리 솔루션에서 솔루션 갤러리 hello hello OMS 포털에서 설치할 수 있습니다.

1. OMS 포털 toohello에 로그인 합니다.
2. Hello 클릭 **솔루션 갤러리** 바둑판식으로 배열입니다.
3. Hello OMS 솔루션 갤러리 페이지에서 사용 가능한 각 솔루션에 알아봅니다. Tooadd tooOMS hello 솔루션의 hello 이름을 클릭 합니다.
4. 선택한 hello 솔루션에 대 한 hello 페이지 hello 솔루션에 대 한 자세한 정보가 표시 됩니다. **추가**를 클릭합니다.
5. Hello OMS 서비스가 데이터를 처리 한 후 사용을 시작 하 고 hello OMS의 개요 페이지에 표시 추가 hello 솔루션에 대 한 새 타일입니다.

### <a name="azure-quickstart-templates"></a>Azure 빠른 시작 템플릿
Hello 커뮤니티의 회원과 관리 솔루션 tooAzure 퀵 스타트 서식 파일을 전송할 수 있습니다.  이후 설치에 대 한 이러한 서식 파일을 다운로드 하거나 검사 toolearn 어떻게 너무[사용자 고유의 솔루션을 만들](#creating-a-solution)합니다.

1. 에 설명 된 hello 프로세스에 따라 [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account) toolink 작업 영역 및 계정.
2. 너무 이동[Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.  
3. 관심 있는 솔루션을 검색합니다.
4. 세부 정보에서 hello 결과 tooview hello 솔루션을 선택 합니다.
5. Hello 클릭 **tooAzure 배포** 단추입니다.
6. Hello 리소스 그룹 및 hello 솔루션의 모든 매개 변수에 대 한 추가 toovalues의 위치와 같은 증명된 tooprovide 정보 됩니다.
7. 클릭 **구매** tooinstall hello 솔루션입니다.

### <a name="deploy-azure-resource-manager-template"></a>Azure Resource Manager 템플릿 배포
Hello 커뮤니티 하거나에서 얻을 수 있는 솔루션 [사용자가 직접 만든](#creating-a-solution) 리소스 관리자 템플릿으로 구현 hello에 대 한 표준 방법 중 하나를 사용할 수 있습니다 [서식 파일 배포](../azure-resource-manager/resource-group-template-deploy-portal.md)합니다.  참고는 hello 솔루션을 설치 하기 전에 해야을 만든 다음 연결 hello [OMS 작업 영역 및 자동화 계정](#oms-workspace-and-automation-account)합니다.

## <a name="oms-workspace-and-automation-account"></a>OMS 작업 영역 및 Automation 계정
대부분의 관리 솔루션에 필요한는 [OMS 작업 영역](../log-analytics/log-analytics-manage-access.md) toocontain 뷰 및 [자동화 계정](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook 및 관련 리소스입니다. 작업 영역을 hello 및 계정은 hello 요구 사항을 준수를 충족 해야 합니다.

* 솔루션은 하나의 OMS 작업 영역과 하나의 자동화 계정만 사용할 수 있습니다.  
* hello OMS 작업 영역 및 솔루션에서 사용 되는 자동화 계정 해야 tooone 연결 된 다른 합니다. OMS 작업 영역 연결된 tooone 자동화 계정에만 사용할 수 있습니다 및 자동화 계정을 연결 된 tooone OMS 작업 영역 수만 있습니다.
* 자동화 계정에 있어야 합니다. 리소스 그룹 및 지역이 동일한 hello 되었으며 toobe hello OMS 작업 영역 연결 합니다.  hello 예외는 미국 동부 지역에 OMS 작업 영역 및 및 미국 동부 2의에서 자동화 계정입니다.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>OMS 작업 영역 및 자동화 계정 간의 링크 만들기
어떻게 hello OMS 작업 영역을 지정 하 고 자동화 계정 솔루션에 대 한 hello 설치 방법에 따라 달라 집니다.

* Hello OMS 포털을 통해 Microsoft 솔루션을 설치 하면 hello 현재 OMS 작업 영역에 설치 되며 자동화 계정이 필요 합니다.
* Hello Azure 마켓플레이스를 통해 솔루션을 설치 하면 OMS 작업 영역 및 자동화 계정에 대 한 메시지가 표시 되 및 서로 hello 링크 만들어집니다.  
* Hello Azure 마켓플레이스에서 외부에서 솔루션을 OMS 작업 영역 hello 및 자동화 계정 hello 솔루션을 설치 하기 전에 연결 해야 합니다.  Hello Azure Marketplace에서에서 모든 솔루션을 선택 하 고 hello OMS 작업 영역 및 자동화 계정을 선택 하 여이 수행할 수 있습니다.  Tooactually hello OMS 작업 영역 및 자동화 계정을 선택 하는 즉시 hello 링크를 만들 수는 없으므로 hello 솔루션을 설치할 필요는 없습니다.  Hello 링크를 만든 후 사용할 수 있습니다 OMS 작업 영역 및 자동화 계정을 하는 모든 솔루션에 대 한 합니다. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>OMS 작업 영역 및 자동화 계정 간의 hello 링크를 확인 하는 중
OMS 작업 영역 및 절차를 수행 하는 hello를 사용 하 여 자동화 계정 간의 hello 링크를 확인할 수 있습니다.

1. Hello Azure 포털에서에서 hello 자동화 계정을 선택 합니다.
2. Hello toohello 맨 아래로 스크롤 **설정을** 창.
3. 섹션이 없는 경우 **OMS 리소스** hello에 **설정을** 창에서이 계정을 연결 된 tooan OMS 작업 영역입니다.
4. 선택 **작업 영역** hello OMS 작업 영역의 tooview hello 세부 정보 toothis 자동화 계정을 연결 합니다.

## <a name="listing-management-solutions"></a>목록 관리 솔루션
Hello 다음 hello 작업 공간 연결 된 Azure 구독 tooyour 프로시저 tootooview hello 관리 솔루션을 사용 합니다.

1. Azure 포털 toohello에 로그인 합니다.
2. Hello 왼쪽된 창에서 선택 **더 많은 서비스**합니다.
3. 너무 아래로 스크롤하여 하나**솔루션** 또는 형식 *솔루션* hello에 **필터** 대화 상자.
4. 모든 작업 영역에 설치된 솔루션이 나열됩니다.

Note hello OMS 포털을 사용 하 여 hello 현재 작업 영역에 설치 된 유일한 hello Microsoft 솔루션을 볼 수 있습니다.

## <a name="removing-a-management-solution"></a>관리 솔루션 제거
관리 솔루션 제거 되 면 hello 솔루션의 모든 리소스 제거 됩니다.  

1. Hello Azure의에서 hello 솔루션을 찾아의 hello 절차를 사용 하 여 포털 [솔루션 나열](#listing-solutions)합니다.
2. Tooremove hello 솔루션을 선택 합니다.
3. Hello 클릭 **삭제** 단추입니다.

## <a name="creating-a-management-solution"></a>관리 솔루션 만들기
관리 솔루션 만들기에 대한 전체 지침은 [OMS(Operations Management Suite)](operations-management-suite-solutions-creating.md)에서 확인할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
* [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates)에서 다양한 Resource Manager 템플릿 샘플을 검색합니다.
* 자신만의 [관리 솔루션](operations-management-suite-solutions-creating.md)을 만듭니다.

