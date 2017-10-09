---
title: "System Center Operations Manager와 지도 통합 aaaService | Microsoft Docs"
description: "서비스 맵을 Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 Operations Management Suite 솔루션 및 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다. 이 문서에서는 서비스 맵을 사용 하 여 tooautomatically Operations Manager에서 배포 응용 프로그램 다이어그램을 만듭니다."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>System Center Operations Manager와 서비스 맵 통합
  > [!NOTE]
  > 이 기능은 공개 미리 보기 상태입니다.
  > 
  
Operations Management Suite 서비스 맵을 자동으로 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 검색 하 고 서비스 간의 통신 hello를 매핑합니다. 서비스 맵을 tooview를 중요 한 서비스를 제공 하는 상호 연결 된 시스템으로, 생각 서버 hello 수 있습니다. 서비스 맵을 구성 에이전트 hello 설치 외에도 필요 하지 않고도 모든 TCP 연결 아키텍처 교차 서버, 프로세스 및 포트 간의 연결을 나타냅니다. 자세한 내용은 참조 hello [서비스 맵을 설명서](operations-management-suite-service-map.md)합니다.

서비스 맵 및 System Center Operations Manager 간 통합이 서비스 맵에서 hello 동적 종속성 맵을 기반으로 하는 Operations Manager에서 배포 응용 프로그램 다이어그램을 자동으로 만들 수 있습니다.

## <a name="prerequisites"></a>필수 조건
* 일련의 서버를 관리하는 Operations Manager 관리 그룹
* Hello 서비스 맵 솔루션을 사용할 수 있는 Operations Management Suite 작업 영역입니다.
* 보내는 데이터 tooService 지도 및 Operations Manager에서 관리 하는 서버 (적어도 하나) 집합입니다. Windows 및 Linux 서버가 지원됩니다.
* 액세스 toohello hello Operations Management Suite 작업 영역에 연관 된 Azure 구독에 있는 서비스 보안 주체입니다. 자세한 내용은 이동 너무[서비스 사용자를 만들](#creating-a-service-principal)합니다.

## <a name="install-hello-service-map-management-pack"></a>Hello 서비스 맵 관리 팩을 설치
Hello Microsoft.SystemCenter.ServiceMap 관리 팩 번들 (Microsoft.SystemCenter.ServiceMap.mpb)를 가져와서 서비스 맵 및 Operations Manager 간의 hello 통합을 사용 합니다. hello 번들 다음 관리 팩 hello를 포함 되어 있습니다.
* Microsoft Service Map Application Views
* Microsoft System Center Service Map Internal
* Microsoft System Center Service Map Overrides
* Microsoft System Center Service Map

## <a name="configure-hello-service-map-integration"></a>Hello 서비스 맵을 통합 구성
Hello 서비스 맵 관리 팩을 새 노드를 설치한 후 **서비스 맵을**, 아래에 표시 됩니다 **Operations Management Suite** hello에 **관리** 창. 

서비스 맵 통합 tooconfigure 다음 hello지 않습니다.

1. tooopen hello 구성 마법사 hello **서비스 맵 개요** 창에서 클릭 **추가 작업 영역**합니다.  

    ![서비스 맵 개요 창](media/oms-service-map/scom-configuration.png)

2. Hello에 **연결 구성** 창 hello 테 넌 트 이름 또는 ID, 응용 프로그램 ID (라고도 hello 사용자 이름 또는 clientID) 및 hello 서비스 사용자의 암호를 입력 한 다음 클릭 **다음**합니다. 자세한 내용은 이동 너무[서비스 사용자를 만들](#creating-a-service-principal)합니다.

    ![hello 연결 구성 창](media/oms-service-map/scom-config-spn.png)

3. Hello에 **구독 선택** 창의 hello Azure 구독, Azure 리소스 그룹 (hello Operations Management Suite 작업 영역에 포함 된 hello) 및 Operations Management Suite 작업 영역을 선택 하 고 클릭 **다음**합니다.

    ![hello Operations Manager 구성 작업 영역](media/oms-service-map/scom-config-workspace.png)

4. Hello에 **컴퓨터 그룹 선택** 서비스 맵 컴퓨터 그룹을 선택할 창 toosync tooOperations 관리자를 선택 합니다. 클릭 **컴퓨터 그룹 추가/제거**, 그룹의 hello 목록에서 선택 **사용 가능한 컴퓨터 그룹**를 클릭 하 고 **추가**합니다.  그룹을 선택 하면 완료 했으면 클릭 **확인** toofinish 합니다.
    
    ![hello Operations Manager 구성 컴퓨터 그룹](media/oms-service-map/scom-config-machine-groups.png)
    
5. Hello에 **서버 선택** Operations Manager와 이러한 서비스 맵을 간의 toosync hello 서버를 사용 하 여 서비스 맵 서버 그룹 hello를 구성 창. **서버 추가/제거**를 클릭합니다.   
    
    서버에 대 한 분산된 응용 프로그램 다이어그램 toobuild를 통합 하는 hello에 대 한 hello 서버 여야 합니다.

    * Operations Manager에서 관리됨
    * 서비스 맵에서 관리됨
    * Hello 서비스 맵 서버 그룹에에서 나열 된

    ![hello Operations Manager 구성 그룹](media/oms-service-map/scom-config-group.png)

6. 선택 사항: hello 관리 서버 리소스 풀 toocommunicate Operations Management Suite로 선택한 다음 클릭 **작업 영역 추가**합니다.

    ![hello Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-pool.png)

    분 tooconfigure 걸릴 수도 있으며 hello Operations Management Suite 작업 영역을 등록. 구성 된 후 Operations Manager Operations Management Suite에서 hello 첫 번째 서비스 맵을 동기화를 시작 합니다.

    ![hello Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>서비스 맵 모니터링
Hello Operations Management Suite 작업 영역 연결 되 면 hello에 새 폴더를 서비스 맵을 표시 됩니다 **모니터링** hello Operations Manager 콘솔의 창.

![hello Operations Manager 모니터링 창](media/oms-service-map/scom-monitoring.png)

hello 서비스 맵을 폴더에 4 개의 노드가 있습니다.
* **활성 경고**: Operations Manager에서 서비스 맵을 사이의 hello 통신에 대 한 모든 hello 활성 경고를 나열 합니다.  이러한 경고는 Operations Management Suite 중인 동기화 된 tooOperations 관리자에 게 알립니다. 

* **서버**: 목록을 모니터링 하는 hello 서버를 서비스 맵에서 toosync를 구성 합니다.

    ![hello Operations Manager 서버 모니터링 창](media/oms-service-map/scom-monitoring-servers.png)

* **컴퓨터 그룹 종속성 보기**: 서비스 맵에서 동기화되는 모든 컴퓨터 그룹을 나열합니다. 배포 응용 프로그램 다이어그램의 모든 그룹 tooview를 클릭할 수 있습니다.

    ![hello Operations Manager 배포 응용 프로그램 다이어그램](media/oms-service-map/scom-group-dad.png)

* **서버 종속성 보기**: 서비스 맵에서 동기화되는 모든 서버를 나열합니다. 배포 응용 프로그램 다이어그램의 모든 서버 tooview를 클릭할 수 있습니다.

    ![hello Operations Manager 배포 응용 프로그램 다이어그램](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>편집 하거나 hello 작업 영역 삭제
Hello 통해 구성 된 hello 작업 영역을 삭제 하거나 편집할 수 **서비스 맵 개요** 창 (**관리** 창 > **Operations Management Suite**  >  **서비스 맵**). 지금은 하나의 Operations Management Suite 작업 영역만 구성할 수 있습니다.

![hello Operations Manager 편집 작업 영역 창](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>규칙 및 재정의 구성
규칙을 _Microsoft.SystemCenter.ServiceMapImport.Rule_, 서비스 맵에서 tooperiodically 인출 정보 만들어집니다. toochange 동기화 시간 hello 규칙의 재정의 구성할 수 있습니다 (**제작** 창 > **규칙** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![hello Operations Manager 재정의 속성 창](media/oms-service-map/scom-overrides.png)

* **Enabled** – 자동 업데이트를 사용하거나 사용하지 않도록 설정합니다. 
* **IntervalMinutes**: hello 업데이트 간격을 다시 설정 합니다. hello 기본 간격은 1 시간입니다. Toosync 서버 지도 더 자주 하려는 경우에 hello 값을 변경할 수 있습니다.
* **TimeoutSeconds**: hello 요청 시간이 초과 되기 전에 시간의 hello 길이 다시 설정 합니다. 
* **TimeWindowMinutes**: 데이터를 쿼리 하기 위한 hello 시간 창 다시 설정 합니다. 기본값은 60분입니다. 서비스 맵을에서 허용 하는 hello 최대 값은 60 분입니다.

## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항

hello 현재 디자인 표시 hello 다음 문제 및 제한 사항:
* Tooa 단일 Operations Management Suite 작업 영역에만 연결할 수 있습니다.
* Hello 통해 수동으로 서버 toohello 서비스 맵 서버 그룹을 추가할 수는 있지만 **제작** 창에서 해당 서버에 대 한 hello 맵을 즉시 동기화 되지 않은 경우.  동기화 됩니다 서비스 맵에서 hello 다음 동기화 주기 중입니다.
* Toohello 분산 응용 프로그램 다이어그램 hello 관리 팩에서 만든 변경 하면 서비스 맵을 사용 하 여 다음 동기화 hello에 가능성이 해당 변경 내용은 덮어씁니다.

## <a name="create-a-service-principal"></a>서비스 주체 만들기
서비스 주체 만들기에 대한 공식적인 Azure 설명서를 보려면 다음을 참조하세요.
* [PowerShell을 사용하여 서비스 주체 만들기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Azure CLI를 사용하여 서비스 주체 만들기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Hello Azure 포털을 사용 하 여 서비스 사용자 만들기](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>사용자 의견
서비스 맵 또는 이 설명서에 대한 의견이 있습니까? 기능을 제안하거나 기존 제안에 투표할 수 있는 [사용자 의견 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)를 방문하세요.
