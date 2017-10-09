---
title: "Azure 로그 분석 작업 영역 aaaGet 시작 | Microsoft Docs"
description: "Log Analytics의 작업 영역은 몇 분 안에 시작하고 실행할 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Log Analytics 작업 영역 시작
Azure Log Analytics를 신속하게 시작하고 실행할 수 있으며 IT 인프라에서 수집된 운영 인텔리전스를 평가하는 데 도움이 됩니다. 이 문서를 사용하면 *무료로* 수집한 데이터에 대한 탐색 및 분석을 손쉽게 시작하고 조치를 취할 수 있습니다.

이 문서 역할을 소개 tooLog 간략 한 자습서 toowalk를 사용 하 여 분석 하면 Azure에서 최소한의 배포를 통해 hello 서비스를 사용 하 여 시작할 수 있도록 합니다. Azure에서 관리 데이터가 저장 된 hello 논리적 컨테이너 작업 영역을 이라고 합니다. 이 정보를 검토 자신의 평가 완료 한 후에 hello 평가 작업 영역을 제거할 수 있습니다. 이 문서는 자습서이기 때문에 비즈니스 요구 사항, 계획 또는 아키텍처 지침이 언급되지 않습니다.

>[!NOTE]
>Microsoft Azure Government 클라우드 hello를 사용 하는 경우 사용 하 여 [Azure Government 모니터링 + 관리 설명서](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) 대신 합니다.

시작 하는 hello 사용 되는 프로세스 tooget 개요는 다음과 같습니다.

![프로세스 다이어그램](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Azure 계정 만들기 및 로그인

Azure 계정이 없는 경우 toocreate 하나 toouse 로그 분석 해야 합니다. 모든 Azure 서비스에 액세스할 수 있는 30일간 유효한 [무료 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate 무료 계정 및 로그인
1. Hello 지침에 따라 [무료 Azure 계정 만들기](https://azure.microsoft.com/free/)합니다.
2. Toohello 이동 [Azure 포털](https://portal.azure.com) 에 로그인 합니다.

## <a name="2-create-a-workspace"></a>2 작업 영역 만들기

hello 다음 단계는 toocreate 작업 영역입니다.

1. Hello Azure 포털에서에서 hello hello 마켓플레이스 서비스 목록이 검색에 대 한 *로그 분석*를 선택한 후 **로그 분석**합니다.  
    ![Azure 포털](./media/log-analytics-get-started/log-analytics-portal.png)
2. 클릭 **만들기**, hello 다음 항목에 대 한 선택 옵션을 선택 합니다.
   * **OMS 작업 영역** - 작업 영역의 이름을 입력합니다.
   * **구독** -hello 원하는 tooassociate hello 새 작업 영역이 하나를 선택 하는 여러 구독이 있는 경우.
   * **리소스 그룹**
   * **위치**:
   * **가격 책정 계층**  
       ![빠른 생성](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. 클릭 **확인** toosee 작업 영역 목록이 있습니다.
4. Hello Azure 포털에서에서 작업 영역 toosee 세부 정보를 선택 합니다.       
    ![작업 영역 정보](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>업그레이드 작업 영역을 3 toonew 로그 검색
릴리스되는 새로운 로그 분석 쿼리 언어는 및에서 그 순서 tootake 혜택 필요 tooconvert 작업 영역.  작업 영역에서 호스팅되는 hello 지역 업그레이드 되 면 hello 위쪽 tooconvert 초대 작업 영역에 걸쳐 자주색 배너를 표시 됩니다. hello 업그레이드가 자발적 참여 하 고 로그 분석 및 추가한 모든 솔루션과 함께 작업에 영향을 주지 않습니다.  

추가적인 내용은 toounderstand hello 성능 고려 사항 및 프로세스 tooupgrade [Azure 로그 분석 업그레이드 toonew 로그 검색](log-analytics-log-search-upgrade.md)합니다.  

## <a name="4-add-solutions-and-solution-offerings"></a>4 솔루션 및 솔루션 제품 추가

다음으로 관리 솔루션 및 솔루션 제품을 추가합니다. 관리 솔루션은 특정 문제 영역을 중심으로 피벗된 메트릭을 제공하는 논리, 시각화 및 데이터 취득 규칙의 컬렉션입니다. 솔루션 제품은 관리 솔루션의 모음입니다.

솔루션 tooyour 작업 영역 추가 다양 한 종류의 데이터는 에이전트를 사용 하 여 연결 된 tooyour 작업 하는 컴퓨터에서 로그 분석 toocollect 수 있습니다. 등록할 에이전트는 나중에 설명하겠습니다.

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd 솔루션과 솔루션 제공

1. Azure 포털에서 클릭 **새로** hello에서 **hello 마켓플레이스** 상자에 입력 합니다 **활동 로그 분석** 한 다음 ENTER 키를 누릅니다.
2. 모든 hello 블레이드를 **활동 로그 분석** 클릭 하 고 **만들기**합니다.  
    ![활동 로그 분석](./media/log-analytics-get-started/activity-log-analytics.png)  
3. Hello에 *관리 솔루션 이름* 블레이드에서 원하는 tooassociate hello 관리 솔루션으로 작업 영역을 선택 합니다.
4. **만들기**를 클릭합니다.  
    ![솔루션 작업 영역](./media/log-analytics-get-started/solution-workspace.png)  
5. Tooadd 1-4 단계를 반복 합니다.
    - hello **보안 및 규정 준수** 서비스 hello 맬웨어 방지 평가 하 고 보안 및 감사 솔루션으로 제공 합니다.
    - hello **자동화 및 제어** 서비스 hello 자동화 Hybrid Worker, 변경 내용 추적 및 시스템 업데이트 평가 (업데이트 관리) 솔루션으로 제공 합니다. Hello 솔루션 제공을 추가 하는 경우 자동화 계정을 만들어야 합니다.  
        ![Automation 계정](./media/log-analytics-get-started/automation-account.png)  
6. 너무 이동 하 여 tooyour 작업 영역을 추가 하는 hello 관리 솔루션을 볼 수 있습니다**로그 분석** > **구독** > ***작업영역이름***  >  **개요**합니다. 사용자가 추가한 hello 관리 솔루션에 대 한 타일 표시 됩니다.  
    >[!NOTE]
    >에이전트 toohello 작업 영역 연결 되어 있지 म 추가한 hello 솔루션에 대 한 데이터 표시 되지 않습니다.  

    ![데이터가 없는 솔루션 타일](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 VM 만들기 및 에이전트 등록

다음으로 Azure에서 간단한 가상 컴퓨터를 만듭니다. 온보드 hello OMS 에이전트 tooenable VM을 만든 후 것입니다. 사용할 수 있도록 hello 에이전트 hello VM에서에서 데이터 수집을 시작 하 고 데이터 tooLog 분석을 보냅니다.

### <a name="toocreate-a-virtual-machine"></a>toocreate 가상 컴퓨터

- Hello 지침에 따라 [hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터를 만들](../virtual-machines/virtual-machines-windows-hero-tutorial.md) hello 새 가상 컴퓨터를 시작 합니다.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>가상 컴퓨터 tooLog hello 분석 연결

- Hello 지침에 따라 [연결 Azure 가상 컴퓨터 tooLog 분석](log-analytics-azure-vm-extension.md) Azure 포털 hello tooconnect hello tooLog 분석 사용 하 여 VM입니다.

## <a name="6-view-and-act-on-data"></a>6 데이터 보기 및 작업

이전에 hello 활동 로그 분석 솔루션 및 hello 보안 및 규정 준수, 자동화 및 제어 서비스 제공 활성화 합니다. 다음으로 솔루션에 의해 수집된 데이터와 로그 검색의 결과를 살펴보겠습니다.

toostart, 솔루션 내에서 표시 되는 데이터를 살펴봅니다. 그런 다음 로그 검색을 통해 액세스한 로그 검색을 살펴봅니다. 로그 검색 toocombine 사용 하면 사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결 하 고 있습니다. 자세한 내용은 참조 [로그 분석 검색 로그인](log-analytics-log-searches.md) 작업 영역 toohello 새 쿼리 언어를 변환한 경우 참조 또는 [로그 분석에서 이해 로그 검색](log-analytics-log-search-new.md)합니다. 

### <a name="tooview-antimalware-data"></a>tooview 맬웨어 방지 프로그램 데이터

1. Hello Azure 포털에서 탐색 너무**로그 분석** > ***작업 영역***합니다.
2. 작업 영역에 대 한 hello 블레이드에서 아래 **일반**, 클릭 **개요**합니다.  
    ![개요](./media/log-analytics-get-started/overview.png)
3. Hello 클릭 **맬웨어 방지 평가** 바둑판식으로 배열입니다. 이 예제의 경우 Windows Defender가 컴퓨터에 설치되어 있지만 서명이 만료된 것을 볼 수 있습니다.  
    ![맬웨어 방지](./media/log-analytics-get-started/solution-antimalware.png)
4. 예를 들어 아래 **보호 상태**, 클릭 **서명 만료 됨** 만료는 시그니처가 있는 hello 컴퓨터에 대 한 tooopen 로그 검색 및 보기 세부 정보입니다. 이 예제에서는 해당 hello 컴퓨터 이름은 참고 *getstarted*합니다. 만료 된 서명 사용 하 여 둘 이상의 컴퓨터 인 경우 모두에 나타나는 hello 로그 검색 결과.  
    ![맬웨어 방지 만료](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview 보안 및 감사 데이터

1. 작업 영역에 대 한 hello 블레이드에서 아래 **일반**, 클릭 **개요**합니다.  
2. Hello 클릭 **보안 및 감사** 바둑판식으로 배열입니다. 이 예제에서 두 가지 주목할만한 문제를 볼 수 있습니다. 중요 업데이트가 누락된 컴퓨터가 하나 있고 보호가 충분하지 않은 컴퓨터가 하나 있습니다.  
    ![보안 및 감사](./media/log-analytics-get-started/security-audit.png)
3. 예를 들어 아래 **주목할 만한 문제**, 클릭 **중요 업데이트가 누락 된 컴퓨터** 중요 업데이트가 누락 된 컴퓨터에 대 한 tooopen 로그 검색 및 보기 세부 정보입니다. 이 예제의 경우 누락된 중요 업데이트가 하나 있고 누락된 다른 업데이트가 63개 있습니다.  
    ![보안 및 감사 로그 검색](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>시스템 업데이트 데이터에 대 한 중심을 tooview

1. 작업 영역에 대 한 hello 블레이드에서 아래 **일반**, 클릭 **개요**합니다.  
2. Hello 클릭 **시스템 업데이트 평가** 바둑판식으로 배열입니다. 이 예제의 경우 중요 업데이트가 필요한 *getstarted*라는 Windows 컴퓨터 하나와 정의 파일 업데이트가 필요한 컴퓨터가 하나 있는 것을 볼 수 있습니다.  
    ![시스템 업데이트](./media/log-analytics-get-started/system-updates.png)
3. 예를 들어 아래 **누락 된 업데이트**, 클릭 **중요 업데이트** 중요 업데이트가 누락 된 컴퓨터에 대 한 tooopen 로그 검색 및 보기 세부 정보입니다. 이 예제의 경우 누락된 업데이트가 하나 있고 필수 업데이트가 하나 있습니다.  
    ![시스템 업데이트 로그 검색](./media/log-analytics-get-started/system-updates-log-search.png)
4. Toohello 이동 [Operations Management Suite](http://microsoft.com/oms) 웹 사이트와 Azure 계정으로 로그인 합니다. 로그인 한 상태에서 표시 hello 솔루션 정보 비슷한 toowhat hello Azure 포털에에서 표시 됩니다.  
    ![OMS 포털](./media/log-analytics-get-started/oms-portal.png)
5. Hello 클릭 **업데이트 관리** 바둑판식으로 배열입니다.
6. Hello 업데이트 관리 대시보드에서 hello 시스템 업데이트 정보 정보가 포함 되어 알 비슷한 toohello 시스템 업데이트 hello Azure 포털에에서 나와 있는 것입니다. 그러나 hello **업데이트 배포 관리** 타일은 새 합니다. Hello 클릭 **업데이트 배포 관리** 바둑판식으로 배열입니다.  
    ![업데이트 관리 타일](./media/log-analytics-get-started/update-management.png)
7. Hello에 **배포 업데이트** 페이지 **추가** toocreate는 *업데이트 실행*합니다.  
    ![업데이트 배포](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  Hello에 **새 업데이트 배포** 페이지을 hello 업데이트 배포에 대 한 이름을 입력 한 다음 컴퓨터 tooupdate 선택 (이 예제에서는 *getstarted*) 일정을 선택한 후 클릭 **저장**.  
    ![새 배포](./media/log-analytics-get-started/new-deployment.png)  
    예약 된 hello hello 업데이트 배포를 저장 한 후 표시를 업데이트 합니다.  
    ![예약된 업데이트](./media/log-analytics-get-started/scheduled-update.png)  
    Hello 업데이트 실행이 완료 되 면 hello 상태 표시 **마침**합니다.
    ![완료된 업데이트](./media/log-analytics-get-started/completed-update.png)
9. Hello 업데이트 실행이 완료 되 면 hello 실행 성공 여부를 적용 하는 경우 업데이트 하는 항목에 대 한 정보를 볼 수 있는지 여부를 볼 수 있습니다.

## <a name="after-evaluation"></a>평가를 마친 후

이 자습서에서 가상 컴퓨터에 에이전트를 설치하고 신속하게 시작했습니다. 수행한 hello 단계 빠르고 간편한 했습니다. 하지만 대부분의 대규모 조직 및 엔터프라이즈는 온-프레미스 IT 인프라가 복잡합니다. 따라서 이러한 복잡 한 환경에서 데이터 수집 추가 계획 및 노력이 보다 차지 hello 자습서 않습니다. Hello 링크 toohelpful 아티클에 대해 다음 단계 섹션 뒤의 hello 정보를 검토 합니다.

필요에 따라이 자습서를 사용 하 여 만든 hello 작업 영역을 제거할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 연결에 대 한 자세한 내용은 [Windows 에이전트](log-analytics-windows-agents.md) tooLog 분석 합니다.
* 연결에 대 한 자세한 내용은 [Operations Manager 에이전트](log-analytics-om-agents.md) tooLog 분석 합니다.
* [로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.
* 익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview 솔루션에서 수집 된 정보를 자세히 설명 합니다.
