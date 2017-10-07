---
title: "로그 분석에서 aaaComputer 그룹 로그 검색 | Microsoft Docs"
description: "로그 분석에서 컴퓨터 그룹을 사용 하면 tooscope 로그 검색 tooa 특정 컴퓨터 집합이 있습니다.  이 문서에서는 toocreate 컴퓨터 그룹 및 toouse 로그에서 해당 검색 방법에서는 hello 다양 한 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Log Analytics 로그 검색의 컴퓨터 그룹 

>[!NOTE]
> 이 문서에는 hello 현재 로그 Anayltics 쿼리 언어를 사용 하 여 컴퓨터 그룹의 hello 사용 방법을 설명 합니다.    작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 컴퓨터 그룹 다르게 작동 합니다.  메모는 hello 새로운 쿼리 언어에 대 한 hello 서로 다른 구문 및 동작이 함께이 문서에 제공 됩니다.  


로그 분석에서 컴퓨터 그룹 허용 tooscope [검색 로그](log-analytics-log-searches.md) tooa 특정 컴퓨터 집합이 있습니다.  각 그룹에는 사용자가 정의를 사용하거나 여러 원본에서 그룹을 가져와 컴퓨터가 채워집니다.  Hello 그룹 로그 검색에 포함 되어 있으면, hello 결과가 hello 그룹의 hello 컴퓨터와 일치 하는 제한 된 toorecords 됩니다.

## <a name="creating-a-computer-group"></a>컴퓨터 그룹 만들기
다음 표에 hello hello 방법 중 하나를 사용 하는 로그 분석에서 컴퓨터 그룹을 만들 수 있습니다.  각 방법에 대 한 내용은 아래 hello 섹션에 제공 됩니다. 

| 메서드 | 설명 |
|:--- |:--- |
| 로그 검색 |컴퓨터의 목록을 반환 하는 로그 검색을 만들고 컴퓨터 그룹으로 hello 결과 저장 합니다. |
| 로그 검색 API |사용 하 여 hello 로그 검색 API tooprogrammatically hello 로그 검색 결과에 따른 컴퓨터 그룹을 만듭니다. |
| Active Directory |Active Directory 도메인의 멤버 이며 각 보안 그룹에 대 한 로그 분석에서 그룹을 만듭니다는 모든 에이전트 컴퓨터의 hello 그룹 구성원 자격을 자동으로 검색 합니다. |
| WSUS |대상 그룹에 대해 자동으로 WSUS 서버나 클라이언트를 검색하고 각각에 대해 Log Analytics에 그룹을 만듭니다. |

### <a name="log-search"></a>로그 검색
로그 검색에서 생성 하는 컴퓨터 그룹에 모두 정의 하는 검색 쿼리에서 반환 하는 hello 컴퓨터 포함 합니다.  이 쿼리는 hello 그룹이 만들어진 후 변경 내용을 반영 되도록 hello 컴퓨터 그룹을 사용할 때마다 실행 됩니다.

로그 검색에서 프로시저 toocreate 컴퓨터 그룹을 다음 hello를 사용 합니다.

1. 컴퓨터 목록을 반환하는 [로그 검색 만듭니다](log-analytics-log-searches.md).  hello 검색 집합만 반환 해야 합니다는 고유한 컴퓨터와 같은 수준의 암호화를 사용 하 여 **고유 컴퓨터** 또는 **컴퓨터별 개수 () 측정** hello 쿼리에서 합니다.  
2. Hello 클릭 **저장** hello hello 화면 위쪽에 단추입니다.
3. 선택 **예** 너무**컴퓨터 그룹으로이 쿼리를 저장 합니다.**합니다.
4. 에 입력 한 **이름** 및 **범주** hello 그룹에 대 한 합니다.  있는 경우 이미 사용 하 여 검색 hello 동일한 이름 및 범주를 다시 입력 정보 요청된 toooverwrite 수는 것입니다.  다양 한 범주의 이름과 같은 이름을 hello로 여러 개의 검색을 할 수 있습니다. 

다음은 컴퓨터 그룹으로 저장할 수 있는 검색의 예입니다.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md) hello 다음과 같이 변경 중인 만들어 놓은 toohello 프로시저 toocreate 새 컴퓨터 그룹입니다.
>  
> - 컴퓨터 그룹을 포함 해야 하는 쿼리 toocreate hello `distinct Computer`합니다.  다음은 쿼리 toocreate 컴퓨터 그룹의 예입니다.<br>`Heartbeat | where Computer contains "srv" `
> - 새 컴퓨터 그룹을 만들 때 추가 toohello 이름에 별칭을 지정 해야 합니다.  아래 설명 된 대로 쿼리에서 hello 컴퓨터 그룹을 사용 하는 경우 hello 별칭을 사용 합니다.  

### <a name="log-search-api"></a>로그 검색 API
로그 검색 API는 hello를 사용 하 여 만든 컴퓨터 그룹을 hello 로그 검색을 사용 하 여 만든 검색으로 동일 합니다.

Hello 로그 검색 API를 사용 하 여 컴퓨터 그룹을 만드는 방법에 대 한 내용은 참조 하십시오 [로그 분석 로그에서 컴퓨터 그룹 검색 REST API](log-analytics-log-search-api.md#computer-groups)합니다.

### <a name="active-directory"></a>Active Directory
로그 분석 tooimport Active Directory 그룹 멤버 자격을 구성 하면 hello OMS 에이전트는 모든 도메인에 가입 된 컴퓨터의 그룹 구성원 hello 분석 합니다.  Active Directory에서 각 보안 그룹에 대 한 로그 분석에는 컴퓨터 그룹을 만들 및 각 컴퓨터 toohello 보안 그룹의 구성원은 해당 toohello 컴퓨터 그룹에 추가 됩니다.  이 멤버 자격은 4시간 간격으로 계속 업데이트됩니다.  

로그 분석에서 hello tooimport Active Directory 보안 그룹 구성 **컴퓨터 그룹** 로그 분석의 메뉴 **설정**합니다.  **자동화**를 선택한 다음 **컴퓨터에서 Active Directory 그룹 멤버 자격을 가져옵니다**.  추가 구성은 필요 없습니다.

![Active Directory의 컴퓨터 그룹](media/log-analytics-computer-groups/configure-activedirectory.png)

되 면 그룹 가져왔는지, hello 메뉴 목록 hello 수의 그룹 구성원을 포함 하는 컴퓨터 검색 고 hello 그룹을 가져올 수 있습니다.  이러한 링크 tooreturn hello 중 하나에서 클릭할 수 있는 **ComputerGroup** 이 정보가 포함 된 레코드입니다.

### <a name="windows-server-update-service"></a>Windows Server 업데이트 서비스
구성 하는 경우 로그 분석 tooimport WSUS 그룹 구성원 자격, hello OMS 에이전트는 모든 컴퓨터의 그룹 구성원을 대상으로 하는 hello을 분석 합니다.  클라이언트 쪽을 사용 하는 경우 연결 된 tooOMS 이며 부분에서는 모든 WSUS 그룹을 대상으로 하는 모든 컴퓨터를 대상으로 그룹 구성원 자격 가져오기가 tooLog 분석 합니다. Hello WSUS에 OMS 에이전트를 설치 해야 하는 hello를 대상으로 서버 쪽을 사용 하는 경우 서버 hello 그룹 멤버 자격 정보 toobe 위해에서 가져온 tooOMS 합니다.  이 멤버 자격은 4시간 간격으로 계속 업데이트됩니다. 

로그 분석에서 hello tooimport Active Directory 보안 그룹 구성 **컴퓨터 그룹** 로그 분석의 메뉴 **설정**합니다.  **Active Directory**를 선택한 다음 **컴퓨터에서 Active Directory 그룹 멤버 자격을 가져옵니다**.  추가 구성은 필요 없습니다.

![Active Directory의 컴퓨터 그룹](media/log-analytics-computer-groups/configure-wsus.png)

되 면 그룹 가져왔는지, hello 메뉴 목록 hello 수의 그룹 구성원을 포함 하는 컴퓨터 검색 고 hello 그룹을 가져올 수 있습니다.  이러한 링크 tooreturn hello 중 하나에서 클릭할 수 있는 **ComputerGroup** 이 정보가 포함 된 레코드입니다.

## <a name="managing-computer-groups"></a>컴퓨터 그룹 관리
로그 검색에서 생성 된 컴퓨터 그룹을 보거나 hello에서 로그 검색 API hello 수 **컴퓨터 그룹** 로그 분석에서 메뉴 **설정을**합니다.  Hello 클릭 **x** hello에 **제거** 열 toodelete hello 컴퓨터 그룹입니다.  Hello 클릭 **멤버를 볼** 해당 멤버를 반환 하는 그룹 toorun hello 그룹의 로그 검색에 대 한 아이콘입니다. 

![저장된 컴퓨터 그룹](media/log-analytics-computer-groups/configure-saved.png)

toomodify hello 그룹에서 새 hello로 동일 그룹 **범주** 및 **이름** toooverwrite hello 원래 그룹입니다.

## <a name="using-a-computer-group-in-a-log-search"></a>로그 검색에서 컴퓨터 그룹 사용
구문 toorefer tooa 컴퓨터 그룹 로그 검색에 다음 hello를 사용 합니다.  지정 하 여 hello **범주** 은 선택적 이며만 hello 이름과 같은 이름을 가지 범주에 있는 컴퓨터 그룹이 있는 경우에 필요 합니다. 

    $ComputerGroups[Category: Name]

검색을 실행 하는 경우 hello 검색에 포함 된 모든 컴퓨터 그룹의 구성원 hello 먼저 확인 됩니다.  Hello 그룹은 로그 검색을 기반으로, 해당 검색 hello 최상위 로그 검색을 수행 하기 전에 hello 그룹의 tooreturn hello 멤버를 실행 됩니다.

컴퓨터 그룹 hello는 일반적 사용 **IN** hello 다음 예제와 같이 hello 로그 검색에는 절:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리에서 컴퓨터 그룹을 사용 하 여 해당 별칭 hello 다음 예제와 같이 함수 처리 하 여:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>컴퓨터 그룹 레코드
Active Directory 또는 WSUS에서 만든 각 컴퓨터 그룹 구성원에 대 한 hello OMS 리포지토리에 레코드가 만들어집니다.  이러한 레코드에는 형식이 **ComputerGroup** 한 hello 속성의 다음 표에 hello 합니다.  로그 검색 기반의 컴퓨터 그룹에 대해서는 레코드가 만들어지지 않습니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| 컴퓨터 |Hello 구성원 컴퓨터의 이름입니다. |
| 그룹 |Hello 그룹의 이름입니다. |
| GroupFullName |Hello 원본과 소스 이름을 포함 하 여 전체 경로 toohello 그룹입니다. |
| GroupSource |그룹을 수집해 온 원본입니다. <br><br>ActiveDirectory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |그룹 hello hello 원본의 이름에서 수집 된 합니다.  Active Directory에 대 한 hello 도메인 이름입니다. |
| ManagementGroupName |SCOM 에이전트에 대 한 hello 관리 그룹의 이름입니다.  다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다. |
| TimeGenerated |날짜 및 시간 hello 컴퓨터 그룹을 만들거나 업데이트 합니다. |

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.  

