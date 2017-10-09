---
title: "OMS IT 서비스 관리 커넥터에서 aaaITSM 연결 | Microsoft Docs"
description: "IT 서비스 관리 커넥터와 함께 OMS toocentrally 모니터에서 ITSM 제품/서비스를 연결 하 고 hello ITSM 작업 항목을 관리 합니다."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>ITSM 제품/서비스를 IT Service Management Connector(미리 보기)에 연결
이 문서는 방법에 대 한 정보를 제공 tooconnect ITSM 제품/서비스 tooIT 서비스 관리 커넥터 및 중앙 집중식으로 OMS에서 작업 항목을 관리 합니다. IT Service Management Connector에 대한 자세한 내용은 [개요](log-analytics-itsmc-overview.md)를 참조하세요.

다음 제품/서비스는 hello 지원 됩니다.

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>System Center Service Manager tooIT OMS에서 서비스 관리 커넥터 연결

hello 다음 섹션에서는 방법에 대 한 tooconnect System Center Service Manager 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.

### <a name="prerequisites"></a>필수 조건

다음 필수 구성 요소가 충족 하는 hello 있는지 확인.

- IT Service Management Connector가 설치되어 있습니다.
추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)
- hello 서비스 관리자 웹 응용 프로그램 (웹 앱) 배포 및 구성 됩니다. 웹앱에 대한 정보는 [여기](#create-and-deploy-service-manager-web-app-service)를 참조하세요.
- 하이브리드 연결이 생성 및 구성되어 있습니다. 자세한 내용은: [구성 hello 하이브리드 연결](#configure-the-hybrid-connection)합니다.
- 지원되는 Service Manager 버전: 2012 R2 또는 2016
- 사용자 역할: [고급 운영자](https://technet.microsoft.com/library/ff461054.aspx)

### <a name="connection-procedure"></a>연결 절차

다음 프로시저 tooconnect hello System Center Service Manager 인스턴스 toohello IT 서비스 관리 커넥터를 사용 합니다.

1. 너무 이동**OMS** >**설정** > **연결 된 원본**합니다.
2. **ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.

    ![Service Manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. 다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결:

> [!NOTE]
> 이러한 모든 매개 변수는 필수입니다.

| **필드** | **설명** |
| --- | --- |
| **Name**   | IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello System Center Service Manager 인스턴스의 이름을 입력 합니다.  이 이름은 나중에 이 인스턴스/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 사용합니다. |
| **연결 형식 선택**   | **System Center Service Manager**를 선택합니다. |
| **서버 URL**   | Hello 서비스 관리자 웹 응용 프로그램의 hello URL을 입력 합니다. Service Manager 웹앱에 대한 자세한 내용은 [여기](#create-and-deploy-service-manager-web-app-service)에 나와 있습니다.
| **클라이언트 ID**   | Hello 웹 앱을 인증 하기 위한 (hello 자동 스크립트를 사용 하 여)을 생성 하는 hello 클라이언트 ID를 입력 합니다. Hello 자동화 된 스크립트에 대 한 자세한 정보는 [여기 합니다.](log-analytics-itsmc-service-manager-script.md)|
| **클라이언트 암호**   | 형식 hello 클라이언트 암호에 대 한이 ID 생성   |
| **데이터 동기화 범위**   | Hello toosync hello IT 서비스 관리 커넥터를 통해 지정 하는 Service Manager 작업 항목을 선택 합니다.  이러한 작업 항목을 Log Analytics로 가져옵니다. **옵션:** 인시던트, 변경 요청|
| **데이터 동기화** | Hello hello 데이터를 원하는 과거 일 수를 입력 합니다. **최대 제한**: 120일 |
| **ITSM 솔루션에서 새 구성 항목 만들기** | Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다. 옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다. **기본**: 사용하지 않도록 설정됩니다. |

성공적으로 연결 및 동기화된 경우:

- Service Manager의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다. 이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.

- OMS에서는 OMS 경고 또는 이 Service Manager 인스턴스의 로그 검색에서 인시던트를 만들 수 있습니다.

추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

### <a name="create-and-deploy-service-manager-web-app-service"></a>Service Manager 웹앱 서비스 만들기 및 배포

tooconnect OMS의 IT 서비스 관리 커넥터 hello로 온-프레미스 서비스 관리자 hello, Microsoft는 GitHub hello에 Service Manager 웹 응용 프로그램을 만들었습니다.

hello ITSM 웹 응용 프로그램에서 Service Manager에 대 한를 tooset 다음 hello지 않습니다.

- **Hello 웹 응용 프로그램 배포** – hello 웹 앱을 배포, hello 속성을 설정 및 Azure AD로 인증 합니다. Hello를 사용 하 여 hello 웹 앱을 배포할 수 있습니다 [스크립트 자동화 된](log-analytics-itsmc-service-manager-script.md) 는 Microsoft에서 제공 합니다.
- **Hello 하이브리드 연결을 구성** - [이 연결을 구성할](#configure-the-hybrid-connection)수동으로 합니다.

#### <a name="deploy-hello-web-app"></a>Hello 웹 응용 프로그램 배포
자동으로 사용 하 여 hello [스크립트](log-analytics-itsmc-service-manager-script.md) toodeploy 웹 응용 프로그램 hello hello 속성을 설정 하 고 Azure AD로 인증 합니다.

Hello 다음 필요한 세부 정보를 제공 하 여 hello 스크립트를 실행 합니다.

- Azure 구독 정보
- 리소스 그룹 이름
- 위치
- Service Manager 서버 세부 정보(서버 이름, 도메인, 사용자 이름 및 암호)
- 웹앱에 대한 사이트 이름 접두사
- ServiceBus 네임스페이스.

hello 스크립트 만듭니다 지정한 hello 이름을 사용 하 여 hello 웹 응용 프로그램 (몇 가지 추가 문자열 toomake와 함께 고유한 것). Hello 생성 **웹 앱 URL**, **클라이언트 ID** 및 **클라이언트 암호**합니다.

Hello 값 저장 사용할 있습니다 IT 서비스 관리 커넥터와 연결을 만들 때.

**Hello 웹 앱을 설치를 확인 합니다.**

1. 너무 이동**Azure 포털** > **리소스**합니다.
2. Hello 웹 앱 선택를 클릭 **설정** > **응용 프로그램 설정**합니다.
3. Hello 스크립트를 통해 hello 앱 배포의 hello 시 제공 하는 hello 서비스 관리자 인스턴스에 대 한 hello 정보를 확인 합니다.

### <a name="configure-hello-hybrid-connection"></a>Hello 하이브리드 연결을 구성 합니다.

OMS의 IT 서비스 관리 커넥터 hello로 hello 서비스 관리자 인스턴스를 연결 하는 프로시저 tooconfigure hello 하이브리드 연결을 수행 하는 hello를 사용 합니다.

1. Hello 서비스 관리자 웹 응용 프로그램 아래에서 찾을 **Azure 리소스**합니다.
2. **설정** > **네트워킹**을 클릭합니다.
3. **하이브리드 연결**에서 **하이브리드 연결 끝점 구성**을 클릭합니다.

    ![하이브리드 연결 네트워킹](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. Hello에 **하이브리드 연결** 블레이드에서 클릭 **하이브리드 연결을 추가할**합니다.

    ![하이브리드 연결 추가](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. Hello에 **하이브리드 연결 추가** 블레이드에서 클릭 **만들기 새 하이브리드 연결**합니다.

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Hello 다음 값을 입력 합니다.

    - **끝점 이름**: hello 새 하이브리드 연결의 이름을 지정 합니다.
    -  **끝점 호스트**: hello Service Manager 관리 서버의 FQDN입니다.
    - **끝점 포트**: 5724를 입력합니다.
    - **Servicebus 네임스페이스**: 기존 Servicebus 네임스페이스를 사용하거나 새로 만듭니다.
    - **위치**: hello 위치를 선택 합니다.
    -  **이름**: 만드는 경우 이름 toohello servicebus를 지정 합니다.

    ![하이브리드 연결 값](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. 클릭 **확인** tooclose hello **하이브리드 연결** 블레이드와 hello 하이브리드 연결을 만들기 시작 합니다.

    Hello 하이브리드 연결을 만든 후 hello 블레이드 아래에 표시 됩니다.

7. Hello 하이브리드 연결을 만든 후 hello 연결을 선택 하 고 클릭 **하이브리드 연결을 선택 하는 추가**합니다.

    ![새 하이브리드 연결](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Hello 수신기 설치 구성

다음과 같은 hello 하이브리드 연결에 대 한 프로시저 tooconfigure hello 수신기 설정이 hello를 사용 합니다.

1. Hello에 **하이브리드 연결** 블레이드에서 클릭 **연결 관리자 다운로드 hello** System Center Service Manager 인스턴스가 실행 되 고 hello 컴퓨터에 설치 합니다.

    Hello 설치가 완료 되 면 **하이브리드 연결 관리자 UI** 옵션은 아래에서 사용할 수 **시작** 메뉴.

2. **하이브리드 연결 관리자 UI**를 클릭하면 Azure 자격 증명을 지정하라는 메시지가 표시됩니다.

3. Azure 자격 증명으로 로그인 하 고 하이브리드 연결 hello 만들어진 구독을 선택 합니다.

4. **Save**를 클릭합니다.

하이브리드 연결이 성공적으로 설정됩니다.

![하이브리드 연결 성공](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Hello 하이브리드 연결을 만들고 확인 하 고 hello를 방문 하 여 hello 연결 테스트 서비스 관리자 웹 응용 프로그램을 배포 합니다. Tooconnect toohello OMS의 IT 서비스 관리 커넥터를 시도 하기 전에 hello 연결을 성공적으로 구성 해야 합니다.

hello 다음 이미지 표시 성공적으로 연결의 hello 세부 정보:

![하이브리드 연결 테스트](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>ServiceNow tooIT OMS에서 서비스 관리 커넥터 연결

hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect ServiceNow 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.

### <a name="prerequisites"></a>필수 조건

다음 필수 구성 요소가 충족 하는 hello 있는지 확인.

- IT Service Management Connector가 설치되어 있습니다. 추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)
- ServiceNow 지원 버전 – Fuji, Geneva, Helsinki

ServiceNow 관리자가 수행 해야 자신의 ServiceNow 인스턴스 다음에 오는 hello:
- 클라이언트 ID와 hello ServiceNow 제품에 대 한 클라이언트 암호를 생성 합니다. Toogenerate 클라이언트 ID 및 암호를 참조 하는 방법에 대 한 내용은 [OAuth 설치](http://wiki.servicenow.com/index.php?title=OAuth_Setup)합니다.
- Microsoft OMS (ServiceNow app) 통합에 대 한 hello 사용자 앱을 설치 합니다. [자세히 알아봅니다](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- 설치 된 hello 사용자 응용 프로그램에 대 한 통합 사용자 역할을 만듭니다. Toocreate hello 통합 사용자 역할을 하는 방법을 알아보려면 [여기](#create-integration-user-role-in-servicenow-app)합니다.


### <a name="connection-procedure"></a>**연결 절차**

다음 프로시저 toocreate ServiceNow 연결 hello를 사용 합니다.

1. 너무 이동**OMS** > **설정** > **연결 된 원본**합니다.
2. **ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.

    ![ServiceNow 연결](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. 다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결:

> [!NOTE]
> 이러한 모든 매개 변수는 필수입니다.

| **필드** | **설명** |
| --- | --- |
| **Name**   | IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello ServiceNow 인스턴스 이름을 입력 합니다.  이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다. |
| **연결 형식 선택**   | **ServiceNow**를 선택합니다. |
| **사용자 이름**   | Hello ServiceNow 앱 toosupport hello 연결 toohello IT 서비스 관리 커넥터에서에서 만든 hello 통합 사용자 이름을 입력 합니다. 추가 정보: [ServiceNow 앱 사용자 역할 만들기](#create-integration-user-role-in-servicenow-app)|
| **암호**   | 이 사용자 이름과 관련 된 hello 암호를 입력 합니다. **참고**: 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다.  |
| **서버 URL**   | 서비스 관리 커넥터 tooconnect tooIT 원하는 hello ServiceNow 인스턴스 hello URL을 입력 합니다. |
| **클라이언트 ID**   | 앞에서 생성 하는 OAuth2 인증 toouse 원하는 hello 클라이언트 ID를 입력 합니다.  클라이언트 ID 및 암호 생성에 대한 추가 정보: [OAuth 설정](http://wiki.servicenow.com/index.php?title=OAuth_Setup) |
| **클라이언트 암호**   | 형식 hello 클라이언트 암호에 대 한이 ID 생성   |
| **데이터 동기화 범위**   | Toosync tooOMS hello IT 서비스 관리 커넥터를 통해 원하는 hello ServiceNow 작업 항목을 선택 합니다.  로그 분석에 hello 선택한 값을 가져옵니다.   **옵션:** 인시던트 및 변경 요청|
| **데이터 동기화** | Hello hello 데이터를 원하는 과거 일 수를 입력 합니다. **최대 제한**: 120일 |
| **ITSM 솔루션에서 새 구성 항목 만들기** | Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다. 옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다. **기본**: 사용하지 않도록 설정됩니다. |


성공적으로 연결 및 동기화된 경우:

- ServiceNow 연결의 선택한 작업 항목을 OMS Log Analytics로 가져옵니다.  이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.
- OMS 경고 또는 이 ServiceNow 인스턴스의 로그 검색에서 인시던트, 경고 및 이벤트를 만들 수 있습니다.  


추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

### <a name="create-integration-user-role-in-servicenow-app"></a>ServiceNow 앱에서 통합 사용자 역할 만들기

사용자 hello 절차를 수행 합니다.

1.  Hello 방문 [ServiceNow 저장소](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) hello를 설치 하 고 **ServiceNow와 Microsoft OMS 통합을 위한 사용자 응용 프로그램** ServiceNow 인스턴스로.
2.  설치가 끝나면 hello ServiceNow 인스턴스, 검색 및 선택 Microsoft OMS integrator의 탐색 모음 왼쪽 hello를 방문 합니다.  
3.  **설치 검사 목록**을 클릭합니다.

    hello 상태가으로 표시 됩니다 **완료할** hello 사용자 역할은 아직 toobe 생성 합니다.

4.  Hello 텍스트에서 상자에 다음 너무**통합 사용자 만들기**, toohello OMS의 IT 서비스 관리 커넥터에 연결할 수 있는 hello 사용자에 대 한 hello 사용자 이름을 입력 합니다.
5.  이 사용자에 대 한 hello 암호를 입력 하 고 클릭 **확인**합니다.  

>[!NOTE]

> OMS에서 이러한 자격 증명 toomake hello ServiceNow 연결을 사용 합니다.

새로 만든 사용자 hello hello 기본 역할 할당 된 상태로 표시 됩니다.

기본 역할:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   itil
-   template_editor
-   view_changer

Hello 사용자가 성공적으로 만들어지면 hello 상태의 **설치 검사 목록 확인** hello 앱에 대해 생성 하는 hello 사용자 역할의 hello 세부 정보를 나열 tooCompleted 이동 합니다.

> [!NOTE]

> 사용자 toocreate tooallow **경고** 및 **이벤트** OMS에서 ServiceNow에서:

> - ServiceNow 인스턴스에 hello 이벤트 관리 모듈 설치를 설치를 확인 합니다.

> - Hello 다음 toohello 통합 사용자 역할을 추가 합니다.
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>연결 Provance tooIT OMS에서 서비스 관리 커넥터

hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect Provance 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.

### <a name="prerequisites"></a>필수 조건

다음 필수 구성 요소가 충족 하는 hello 있는지 확인.

- IT Service Management Connector가 설치되어 있습니다. 추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)
- Provance 앱을 Azure AD에 등록해야 합니다. 그래야 클라이언트 ID를 사용할 수 있게 됩니다. 자세한 내용은 참조 [어떻게 tooconfigure active directory 인증](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.
- 사용자 역할: 관리자

### <a name="connection-procedure"></a>연결 절차

다음 프로시저 toocreate Provance 연결 hello를 사용 합니다.

1. 너무 이동**OMS** > **설정** > **연결 된 원본**합니다.
2. **ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.  

    ![Provance 연결](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. 다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결 합니다.

> [!NOTE]
> 이러한 모든 매개 변수는 필수입니다.

| **필드** | **설명** |
| --- | --- |
| **Name**   | IT 서비스 관리 커넥터 hello로 tooconnect 원하는 hello Provance 인스턴스에 대 한 이름을 입력 합니다.  이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다. |
| **연결 형식 선택**   | **Provance**를 선택합니다. |
| **사용자 이름**   | Toohello IT 서비스 관리 커넥터에 연결할 수 있는 hello 사용자 이름을 입력 합니다.    |
| **암호**   | 이 사용자 이름과 관련 된 hello 암호를 입력 합니다. **참고:** 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다. _|
| **서버 URL**   | 서비스 관리 커넥터 tooconnect tooIT 원하는 Provance 인스턴스 hello URL을 입력 합니다. |
| **클라이언트 ID**   | Provance 인스턴스에 생성 된이 연결을 인증 하는 hello 클라이언트 ID를 입력 합니다.  클라이언트 ID에 대 한 자세한 내용은 참조 [어떻게 tooconfigure active directory 인증](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다. |
| **데이터 동기화 범위**   | Toosync tooOMS hello IT 서비스 관리 커넥터를 통해 원하는 hello Provance 작업 항목을 선택 합니다.  이러한 작업 항목을 Log Analytics로 가져옵니다.   **옵션:** 인시던트, 변경 요청|
| **데이터 동기화** | Hello hello 데이터를 원하는 과거 일 수를 입력 합니다. **최대 제한**: 120일 |
| **ITSM 솔루션에서 새 구성 항목 만들기** | Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다. 옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다. **기본**: 사용하지 않도록 설정됩니다.|

성공적으로 연결 및 동기화된 경우:

- Provance 연결의 선택한 작업 항목을 OMS **Log Analytics**로 가져옵니다.  이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.
- OMS 경고 또는 이 Provance 인스턴스의 로그 검색에서 인시던트 및 이벤트를 만들 수 있습니다.

추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Cherwell tooIT OMS에서 서비스 관리 커넥터 연결

hello 다음 섹션에서는 제공 방법에 대 한 세부 정보 tooconnect Cherwell 제품 toohello OMS의 IT 서비스 관리 커넥터입니다.

### <a name="prerequisites"></a>필수 조건

다음 필수 구성 요소가 충족 하는 hello 있는지 확인.

- IT Service Management Connector가 설치되어 있습니다. 추가 정보: [구성](log-analytics-itsmc-overview.md#configuration)
- 클라이언트 ID가 생성되었습니다. 추가 정보: [Cherwell용 클라이언트 ID 생성](#generate-client-id-for-cherwell)
- 사용자 역할: 관리자

### <a name="connection-procedure"></a>연결 절차

다음 프로시저 toocreate Cherwell 연결 hello를 사용 합니다.

1. 너무 이동**OMS** >  **설정** > **연결 된 원본**합니다.
2. **ITSM 커넥터**를 선택하고 **새 연결 추가**를 클릭합니다.  

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. 다음 표를 hello에 설명 된 대로 hello 정보를 입력 하 고 클릭 **저장** toocreate hello 연결 합니다.

> [!NOTE]
> 이러한 모든 매개 변수는 필수입니다.

| **필드** | **설명** |
| --- | --- |
| **Name**   | Hello Cherwell 인스턴스 원하는 tooconnect toohello IT 서비스 관리 커넥터에 대 한 이름을 입력 합니다.  이 이름은 나중에 이 ITSM/보기의 자세한 로그 분석에서 작업 항목을 구성할 때 OMS에서 사용합니다. |
| **연결 형식 선택**   | **Cherwell**을 선택합니다. |
| **사용자 이름**   | Toohello IT 서비스 관리 커넥터에 연결할 수 있는 hello Cherwell 사용자 이름을 입력 합니다. |
| **암호**   | 이 사용자 이름과 관련 된 hello 암호를 입력 합니다. **참고:** 사용자 이름 및 암호 인증 토큰 생성에 사용 되 고 hello OMS 서비스 내에서 아무 곳 이나 저장 되지 않습니다.|
| **서버 URL**   | 서비스 관리 커넥터 tooconnect tooIT 원하는 Cherwell 인스턴스 hello URL을 입력 합니다. |
| **클라이언트 ID**   | Cherwell 인스턴스에 생성 된이 연결을 인증 하는 hello 클라이언트 ID를 입력 합니다.   |
| **데이터 동기화 범위**   | Toosync hello IT 서비스 관리 커넥터를 통해 원하는 hello Cherwell 작업 항목을 선택 합니다.  이러한 작업 항목을 Log Analytics로 가져옵니다.   **옵션:** 인시던트, 변경 요청 |
| **데이터 동기화** | Hello hello 데이터를 원하는 과거 일 수를 입력 합니다. **최대 제한**: 120일 |
| **ITSM 솔루션에서 새 구성 항목 만들기** | Hello ITSM 제품에서 toocreate hello 구성 항목을 하려는 경우이 옵션을 선택 합니다. 옵션을 선택 하면 구성 항목 (발생할 경우 존재 하지 않는 Ci) hello에 ITSM 시스템 지원 OMS hello 영향을 받는 Ci를 만듭니다. **기본**: 사용하지 않도록 설정됩니다. |

성공적으로 연결 및 동기화된 경우:

- 이 Cherwell 연결에서 선택된 작업 항목을 OMS Log Analytics로 가져옵니다. 이러한 hello 요약을 볼 수 hello IT 서비스 관리 커넥터 타일에 작업 항목.
- OMS에서 이 Cherwell 인스턴스의 인시던트 및 이벤트를 만들 수 있습니다. 추가 정보: OMS 경고에 대한 ITSM 작업 항목 만들기 및 OMS 로그에서 ITSM 작업 항목 만들기

추가 정보: [OMS 경고에 대한 작업 항목 만들기 ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) 및 [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

### <a name="generate-client-id-for-cherwell"></a>Cherwell용 클라이언트 ID 생성

toogenerate는 Cherwell에 대 한 클라이언트가 D/키 hello, 절차를 수행 하는 hello를 사용 하 여:

1. 로그인 tooyour Cherwell 인스턴스 관리자로
2. **보안** > **REST API 클라이언트 설정 편집**을 클릭합니다.
3. **새 클라이언트 만들기** > **클라이언트 암호**를 선택합니다.

    ![Cherwell 사용자 ID](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>다음 단계
 - [OMS 경고에 대한 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [OMS 로그에서 ITSM 작업 항목 만들기](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [연결에 대한 Log Analytics 보기](log-analytics-itsmc-overview.md#using-the-solution)
