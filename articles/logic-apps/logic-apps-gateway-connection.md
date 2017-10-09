---
title: "Azure 논리 앱에 대 한 온-프레미스에서 데이터 원본을 aaaAccess | Microsoft Docs"
description: "논리 앱에서 온-프레미스 데이터 원본에 액세스할 수 있도록 hello 온-프레미스 데이터 게이트웨이를 설정합니다"
keywords: "데이터에 액세스, 온-프레미스, 데이터 전송, 암호화, 데이터 원본"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>온-프레미스 hello 온-프레미스 데이터 게이트웨이 사용 하 여 논리 앱에서 데이터 원본 액세스

논리 앱에서 온-프레미스에서 데이터 원본을 tooaccess 논리 앱 지원 되는 커넥터와 함께 사용할 수 있는 온-프레미스 데이터 게이트웨이를 설정 합니다. hello 게이트웨이 빠른 데이터 전송 및 온-프레미스 데이터 원본과 논리 앱 간에 암호화를 제공 하는 브리지 역할을 합니다. hello 게이트웨이 hello Azure 서비스 버스를 통해 암호화 된 채널에 온-프레미스 원본에서 데이터를 릴레이합니다. 모든 트래픽이 hello 게이트웨이 에이전트의 보안 아웃 바운드 트래픽이으로 시작 합니다. 에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](logic-apps-gateway-install.md#gateway-cloud-service)합니다. 

hello 게이트웨이 온-프레미스 toothese 데이터 원본 연결을 지원합니다.

*   BizTalk Server 2016
*   DB2  
*   파일 시스템
*   Informix
*   MQ
*   MySQL
*   Oracle 데이터베이스
*   PostgreSQL
*   SAP 응용 프로그램 서버 
*   SAP 메시지 서버
*   SharePoint
*   SQL Server
*   Teradata

이러한 단계는 어떻게 tooset hello 온-프레미스 데이터 게이트웨이 toowork 논리 앱을 보여 줍니다. 지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](../connectors/apis-list.md)를 참조하세요. 

Toouse 다른 서비스와 게이트웨이 hello 하는 방법에 대 한 내용은 다음이 문서를 참조 합니다.

*   [Microsoft Power BI 온-프레미스 데이터 게이트웨이](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services 온-프레미스 데이터 게이트웨이](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow 온-프레미스 데이터 게이트웨이](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps 온-프레미스 데이터 게이트웨이](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>요구 사항

* 이미 있어야 [hello 데이터 게이트웨이 로컬 컴퓨터에 설치](logic-apps-gateway-install.md)합니다.

* 동일한 작업 hello 또는 학교 계정을 사용한 너무 toouse 있는 toohello Azure 포털에에서 로그인 할 때[hello 온-프레미스 데이터 게이트웨이 설치](logic-apps-gateway-install.md#requirements)합니다. 사용자 로그인 계정에 게이트웨이 설치에 대 한 hello Azure 포털에서에서 게이트웨이 리소스를 만들 때 Azure 구독 toouse가 있어야 합니다.

* 게이트웨이 설치는 Azure 게이트웨이 리소스에서 이미 요구할 수 없습니다. 게이트웨이 설치 tooonly 하나의 Azure 게이트웨이 리소스에 연결할 수 있습니다. 클레임은 hello 설치를 다른 리소스에 대 한 사용할 수 있도록 hello 게이트웨이 리소스를 만들 때 발생 합니다.

## <a name="set-up-hello-data-gateway-connection"></a>Hello 데이터 게이트웨이 연결을 설정 합니다.

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Hello 온-프레미스 데이터 게이트웨이 설치

아직 하지 않는 경우 따라 hello [단계 tooinstall hello 온-프레미스 데이터 게이트웨이](logic-apps-gateway-install.md)합니다. Hello로 계속 하기 전에 다른 단계 hello 데이터 게이트웨이 로컬 컴퓨터에 설치 되어 있는지 확인 합니다.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Hello 온-프레미스 데이터 게이트웨이에 대 한 Azure 리소스 만들기

로컬 컴퓨터에 hello 게이트웨이 설치한 후 Azure에 리소스로 데이터 게이트웨이 만들어야 합니다. 또한 이 단계는 Azure 구독과 게이트웨이 리소스를 연결합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다. Toouse hello 동일한 Azure 회사 또는 학교 전자 메일 주소 사용 tooinstall hello 게이트웨이 있는지 확인 합니다.

2. Azure의 hello 왼쪽된 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이** 다음과 같이 합니다.

   !["온-프레미스 데이터 게이트웨이" 찾기](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Hello에 **연결 게이트웨이 만들기** 블레이드에서 이러한 세부 정보 toocreate 데이터 게이트웨이 리소스를 제공 합니다.

    * **이름**: 게이트웨이 리소스의 이름을 입력합니다. 

    * **구독**: 선택 hello 게이트웨이 리소스와 Azure 구독 tooassociate 합니다. 
    이 구독 해야 hello 논리 앱과 동일한 구독 합니다.
   
      hello 기본 구독 hello toosign에 사용한 Azure 계정 기반으로 합니다.

    * **리소스 그룹**: 게이트웨이 리소스를 배포하기 위해 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다. 
    리소스 그룹을 통해 관련된 Azure 자산을 컬렉션으로 관리할 수 있습니다.

    * **위치**: Azure 위치 toohello이를 제한 하는 동안 hello 게이트웨이 클라우드 서비스에 대해 선택 된 동일한 지역 [게이트웨이 설치](logic-apps-gateway-install.md)합니다. 

      > [!NOTE]
      > Hello 게이트웨이 리소스 위치 hello 게이트웨이 클라우드 서비스 위치와 일치 하는지 확인 합니다. 그렇지 않은 경우 게이트웨이 설치 나타나지 않을 tooselect 있습니다 설치 하는 hello 게이트웨이 목록에 hello 다음 단계에서.
      > 
      > 게이트웨이 리소스 및 논리 앱에 서로 다른 지역을 사용할 수 있습니다.

    * **설치 이름**: 게이트웨이 설치 선택 되어 있지 않으면 이전에 설치한 hello 게이트웨이 선택 합니다. 

    tooadd hello 게이트웨이 리소스 tooyour Azure 대시보드를 선택 **Pin toodashboard**합니다. 
    작업을 완료하면 **만들기**를 선택합니다.

    예:

    ![온-프레미스 데이터 게이트웨이 toocreate 세부 정보를 제공 합니다.](./media/logic-apps-gateway-connection/createblade.png)

    hello 주요 Azure 왼쪽된 메뉴에서 언제 든 지 데이터 게이트웨이 너무 이동 toofind 또는 보기 **더 서비스** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이**합니다.

    ![너무 이동 "더 많은 서비스", "엔터프라이즈 통합", "온-프레미스 데이터 게이트웨이"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. 논리 앱 toohello 온-프레미스 데이터 게이트웨이 연결 합니다.

데이터 게이트웨이 리소스를 생성 하 고 Azure 구독에 연결 된 해당 리소스 한 논리 앱 및 hello 데이터 게이트웨이 간의 연결을 만듭니다.

> [!NOTE]
> 게이트웨이 연결 위치에에서 존재 해야 hello 동일 지역 있지만 논리 앱으로 다른 지역에 존재 하는 데이터 게이트웨이 사용할 수 있습니다.

1. Hello Azure 포털에서에서 만들거나 논리가 응용 프로그램 디자이너에서 논리 앱을 엽니다.

2. 온-프레미스 연결을 지원하는 SQL Server와 같은 커넥터를 추가합니다.

3. 선택 표시 된 hello 순서에 따라 **온-프레미스 데이터 게이트웨이 통해 연결**, 고유 연결 이름을 제공 하 고 필요한 정보를 hello 하 고 toouse 원하는 hello 데이터 게이트웨이 리소스를 선택 합니다. 작업을 완료하면 **만들기**를 선택합니다.

   > [!TIP]
   > 고유한 연결 이름을 통해 나중에, 특히 여러 연결을 만들 때 해당 연결을 쉽게 식별할 수 있습니다. 해당 하는 경우 hello 정규화 된 도메인에서 사용자 이름을 포함 합니다. 

   ![논리 앱과 데이터 게이트웨이 간에 연결 만들기](./media/logic-apps-gateway-connection/blankconnection.png)

축, 한 게이트웨이 연결 논리 앱 toouse 준비가 되었습니다.

## <a name="edit-your-gateway-connection-settings"></a>게이트웨이 연결 설정 편집

논리 앱에 대 한 게이트웨이 연결을 만든 후에 해당 특정 연결에 대 한 toolater 업데이트 hello 설정을 할 수 있습니다.

1. toofind hello 게이트웨이 연결:

   * Hello 논리 앱 블레이드에서 아래 **개발 도구**선택, **API 연결**합니다. 
   
     hello **API 연결** 게이트웨이 연결을 포함 하 여 논리 앱과 연결 된 모든 API 연결 창에 표시 합니다.

     ![이동 tooyour 논리 앱을 "연결 API" 선택](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Hello 주요 Azure 왼쪽된 메뉴에서 이동할 너무 또는 **더 서비스** > **웹 및 모바일 서비스** > **API 연결** 모든 API 연결에 대 한 Azure 구독과 연결 된 포함 하 여 게이트웨이 연결 합니다. 

   * Hello 주 Azure 왼쪽 메뉴에서 너무를 이동 또는**모든 리소스** 모든 API 연결에 대 한 Azure 구독과 연결 된 게이트웨이 연결을 포함 합니다.

2. Tooview 또는 편집을 선택 하는 hello 게이트웨이 연결을 선택 **편집 API 연결**합니다.

   > [!TIP]
   > 업데이트가 적용 되지 않습니다, 그래도 [hello 게이트웨이 Windows 서비스를 다시 시작 및 중지](./logic-apps-gateway-install.md#restart-gateway)합니다.

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>온-프레미스 데이터 게이트웨이 리소스 전환 또는 삭제

toocreate 다른 게이트웨이 리소스를 다른 리소스와 게이트웨이 연결 하거나 hello 게이트웨이 리소스를 제거, hello 게이트웨이 설치에 영향을 주지 않고 hello 게이트웨이 리소스를 삭제할 수 있습니다. 

1. Hello 주요 Azure 왼쪽된 메뉴에서 이동할 너무**모든 리소스**합니다. 
2. 데이터 게이트웨이 리소스를 찾아 선택합니다.
3. 선택 **온-프레미스 데이터 게이트웨이**, hello 리소스 도구 모음에서 선택 하 고 **삭제**합니다.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>질문과 대답

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>다음 단계

* [논리 앱 보안](./logic-apps-securing-a-logic-app.md)
* [논리 앱에 대한 일반적인 예제 및 시나리오](./logic-apps-examples-and-scenarios.md)
