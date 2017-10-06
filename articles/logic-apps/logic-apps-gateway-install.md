---
title: "Azure 논리 앱-aaaInstall 온-프레미스 데이터 게이트웨이 | Microsoft Docs"
description: "온-프레미스 데이터 원본에 액세스 하기 전에 빠른 데이터 전송 및 온-프레미스 데이터 원본과 논리 앱 간에 암호화를 위한 hello 온-프레미스 데이터 게이트웨이 설치"
keywords: "데이터에 액세스, 온-프레미스, 데이터 전송, 암호화, 데이터 원본"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Azure 논리 앱에 대 한 hello 온-프레미스 데이터 게이트웨이 설치 합니다.

논리 앱에서 온-프레미스 데이터 원본에 액세스 하기 전에 설치 하 고 hello 온-프레미스 데이터 게이트웨이 설치 해야 합니다. hello 게이트웨이 빠른 데이터 전송 및 온-프레미스 시스템과 논리 앱 간에 암호화를 제공 하는 브리지 역할을 합니다. hello 게이트웨이 hello Azure 서비스 버스를 통해 암호화 된 채널에 온-프레미스 원본에서 데이터를 릴레이합니다. 모든 트래픽이 hello 게이트웨이 에이전트의 보안 아웃 바운드 트래픽이으로 시작 합니다. 에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](#gateway-cloud-service)합니다.

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

다음이 단계 표시 방법을 toofirst 설치 hello 온-프레미스 데이터 게이트웨이 하기 전에 [hello 게이트웨이와 논리 앱 간의 연결을 설정](./logic-apps-gateway-connection.md)합니다. 지원되는 커넥터에 대한 자세한 내용은 [Azure Logic Apps용 커넥터](https://docs.microsoft.com/azure/connectors/apis-list)를 참조하세요. 

Toouse 다른 서비스와 게이트웨이 hello 하는 방법에 대 한 내용은 다음이 문서를 참조 합니다.

*   [Microsoft Power BI 온-프레미스 데이터 게이트웨이](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services 온-프레미스 데이터 게이트웨이](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow 온-프레미스 데이터 게이트웨이](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps 온-프레미스 데이터 게이트웨이](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>요구 사항

**최소**:

* .NET 4.5 Framework
* 64비트 버전의 Windows 7 또는 Windows Server 2008 R2 이상

**권장**:

* 8 코어 CPU
* 8GB 메모리
* 64비트 버전의 Windows 2012 R2 이상

**중요 고려 사항**:

* 로컬 컴퓨터에만 hello 온-프레미스 데이터 게이트웨이 설치 합니다.
도메인 컨트롤러에 hello 게이트웨이 설치할 수 없습니다.

   > [!TIP]
   > Hello에 tooinstall hello 게이트웨이 없는 데이터 소스와 같은 컴퓨터. toominimize 대기 시간 hello 또는 가능한 tooyour 데이터 소스로 동일 가까운 hello 게이트웨이 설치할 수 있습니다 컴퓨터 권한이 있다고 가정 합니다.

* Hello 게이트웨이 해제, toosleep, 이동 또는 hello 게이트웨이 이러한 상황에서 실행할 수 없기 때문에 toohello 인터넷에 연결 하지 않는 컴퓨터에 설치 하지 마십시오. 또한 무선 네트워크에서는 게이트웨이 성능이 저하될 수 있습니다.

* 설치하는 동안 Microsoft 계정이 아니라 Azure Active Directory(Azure AD)에서 관리하는 [회사 또는 학교 계정](https://docs.microsoft.com/azure/active-directory/sign-up-organization)으로 로그인해야 합니다. 

  동일한 작업 hello 또는 학교 계정을 나중에 hello Azure toouse 있는 포털 만들고 게이트웨이 설치와 게이트웨이 리소스를 연결 합니다. 그런 다음 프로그램 논리 앱 및 hello 온-프레미스 데이터 소스 간 hello 연결을 만들 때이 게이트웨이 리소스를 선택 합니다. [Azure AD 회사 또는 학교 계정을 사용해야 하는 이유는 무엇인가요?](#why-azure-work-school-account)

  > [!TIP]
  > Office 365 서비스에 등록하고 실제 회사 전자 메일을 제공하지 않은 경우 로그인 주소는 jeff@contoso.onmicrosoft.com과 같을 수 있습니다. 

* 14.16.6317.4 버전 보다 이전 하는 설치 관리자를 설정 하는 기존 게이트웨이 사용 하도록 설정한 경우 실행 중인 hello 최신 설치 관리자에서 게이트웨이 위치를 변경할 수 없습니다. 그러나 새 게이트웨이를 최신 설치 관리자 tooset hello 대신 원하는 hello 위치와 사용할 수 있습니다.
  
  하지만 이전 버전 14.16.6317.4, 게이트웨이 설치 관리자 있는 게이트웨이 설치 하지 않은 경우 아직 다운로드 하 고 수 hello 최신 설치 관리자를 사용 합니다.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Hello 데이터 게이트웨이 설치

1.  [다운로드 하 고 hello 게이트웨이 설치 관리자는 로컬 컴퓨터에서 실행](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409)합니다.

2. 검토 하 고 hello 개인정보취급방침 및 사용 약관에 동의 합니다.

3. Tooinstall hello 게이트웨이 저장할 로컬 컴퓨터의 hello 경로 지정 합니다.

4. 메시지가 표시되면 Microsoft 계정이 아닌 Azure 회사 또는 학교 계정을 사용하여 로그인합니다.

   ![Azure 회사 또는 학교 계정으로 로그인](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. 이제 hello로 설치 된 게이트웨이 등록 [게이트웨이 클라우드 서비스](#gateway-cloud-service)합니다. **이 컴퓨터에 새 게이트웨이 등록**을 선택합니다.

   hello 게이트웨이 클라우드 서비스를 암호화 하 고 데이터 원본 자격 증명 및 게이트웨이 세부 정보를 저장 합니다. 
   또한 hello 서비스 온-프레미스 쿼리 및 논리 앱, hello 온-프레미스 데이터 게이트웨이 및 데이터 원본 간의 그 결과 라우트합니다.

6. 게이트웨이 설치에 대한 이름을 제공합니다. 복구 키를 만든 다음 복구 키를 확인합니다. 

   > [!IMPORTANT] 
   > 복구 키는 8자 이상이어야 합니다. 저장 하 고 안전한 장소에 hello 키를 보관 해야 합니다. Toomigrate, 원하는 때이 키도 필요 복원 또는 기존 게이트웨이를 사용 합니다.

   1. toochange hello 기본 지역 hello 게이트웨이 클라우드 서비스 및 Azure 서비스 버스 게이트웨이 설치 프로그램에서 사용 하는 선택 **변경 지역**합니다.

      ![지역 변경](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      hello 기본 영역이 Azure AD 테 넌 트와 연결 된 hello 영역이입니다.

   2. Hello 다음 창에서 엽니다 hello **선택 영역** 너무 다른 지역을 선택 합니다.

      ![다른 지역 선택](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      예를 들어 있습니다 수 선택 hello 논리 앱와 동일한 지역 또는 select hello 지역 가장 가까운 tooyour 온-프레미스 데이터 원본 대기 시간을 줄일 수 있도록 합니다. 게이트웨이 리소스와 논리 앱은 서로 다른 위치에 있을 수 있습니다.

      > [!IMPORTANT]
      > 설치 후에 이 지역을 변경할 수 없습니다. 또한이 지역 결정 하 고 게이트웨이 hello Azure 리소스를 만들 수 있는 hello 위치를 제한 합니다. 따라서 Azure에서 게이트웨이 리소스를 만들 때 hello 리소스 위치 게이트웨이 설치 중에 선택한 hello 영역 일치 하는지 확인 합니다.
      > 
      > 원할 경우 다른 지역의 toouse 게이트웨이 나중에 새 게이트웨이 설정 해야 합니다.

   3. 준비가 되면 **완료**를 선택합니다.

7. 할 수 있도록 hello Azure 포털에서에서이 단계에 따라 [게이트웨이에 대 한 Azure 리소스 만들기](../logic-apps/logic-apps-gateway-connection.md)합니다. 

에 대 한 자세한 내용은 [hello 데이터 게이트웨이가 어떻게 작동](#gateway-cloud-service)합니다.

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>기존 게이트웨이 마이그레이션, 복원 또는 사용

이러한 작업 tooperform, hello 게이트웨이 설치할 때 지정 된 hello 복구 키를 있어야 합니다.

1. 컴퓨터의 시작 메뉴에서 **온-프레미스 데이터 게이트웨이**를 선택합니다.

2. Hello 설치 관리자가 열립니다. 그러면 로그인에 사용한 후 hello 동일한 Azure 회사 또는 tooinstall hello 게이트웨이 사용 하는 이전 학교 계정.

3. **기존 게이트웨이 마이그레이션, 복원 또는 사용**을 선택합니다.

4. Toomigrate, 복원 또는 인수를 통해 하려는 hello 게이트웨이에 대 한 hello 이름 및 복구 키를 제공 합니다.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Hello 게이트웨이 다시 시작

hello 게이트웨이 Windows 서비스로 실행 됩니다. 다른 Windows 서비스와 마찬가지로 시작 하 고 여러 가지 방법으로 hello 서비스를 중지할 수 있습니다. 예를 들어 hello 게이트웨이 실행 하는 hello 컴퓨터에서 승격 된 권한으로 명령 프롬프트를 열고 하 고 이러한 명령 중 하나를 실행할 수 있습니다.

* 이 명령을 실행 toostop hello 서비스:
  
    `net stop PBIEgwService`

* 이 명령을 실행 toostart hello 서비스:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Windows 서비스 계정

hello 온-프레미스 데이터 게이트웨이 toouse 설정 `NT SERVICE\PBIEgwService` Windows hello에 대 한 서비스 로그온 자격 증명입니다. 기본적으로 hello 게이트웨이 hello 컴퓨터에 대 한 "서비스로 로그온" 권한을 hello에 hello 게이트웨이 설치 하는 위치에 있습니다.

> [!NOTE]
> tooon 온-프레미스 데이터 원본에 연결 하는 데 사용 되는 hello 계정 및 Azure 작업 hello hello Windows 서비스 계정을 다른 또는 학교 계정 toocloud 서비스에서 toosign를 사용 합니다.

## <a name="configure-a-firewall-or-proxy"></a>방화벽 또는 프록시 구성

hello 게이트웨이 아웃 바운드 연결을 너무 만듭니다 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다. 사용자 게이트웨이에 대 한 프록시 정보 tooprovide 참조 [프록시 설정 구성](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/)합니다.

toocheck 방화벽 또는 프록시 연결을 차단할 수 있는지 여부를 확인 컴퓨터 실제로 toohello를 연결할 수 있는지 여부를 인터넷 및 hello [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다. PowerShell 창에서 다음 명령을 실행합니다.

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> 이 명령은 네트워크 연결 및 연결 toohello Azure 서비스 버스에만 테스트합니다. Hello 명령 할당 되지 않은 하므로 toodo hello 게이트웨이 또는 hello 게이트웨이 클라우드 서비스를 암호화 하 고 자격 증명 및 게이트웨이 세부 정보를 저장 합니다. 
>
> 또한 이 명령은 Windows Server 2012 R2 이상 및 Windows 8.1 이상에서만 사용할 수 있습니다. 텔넷 이전 운영 체제 버전에서 사용할 수 있습니다 너무 연결을 테스트 합니다. [Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.

결과는 비슷한 예는 toothis 같아야 합니다.

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

경우 **TcpTestSucceeded** 너무 설정 하지 않으면**True**, 방화벽으로 차단 될 수 있습니다. Toobe를 포괄적인 원하는 경우 대체 hello **ComputerName** 및 **포트** 아래 나열 된 값과 hello 값 [포트 구성](#configure-ports) 이 항목의 합니다.

hello 방화벽 연결 Azure 서비스 버스 toohello Azure 데이터 센터를 사용 하면 해당 hello를 차단도 될 수 있습니다. 이 시나리오에서 상황이 발생 하는 경우 승인 (차단 해제) 모든 hello 해당 지역에서 해당 데이터 센터에 대 한 IP 주소입니다. 이러한 IP 주소에 대 한 [get hello Azure IP 주소 목록 여기](https://www.microsoft.com/download/details.aspx?id=41653)합니다.

## <a name="configure-ports"></a>포트 구성

hello 게이트웨이 아웃 바운드 연결을 너무 만듭니다[Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/) 아웃 바운드 포트는 통신: TCP 443 (기본값), 5671, 5672, 9350 9354 통해. hello 게이트웨이 인바운드 포트가 필요 하지 않습니다. [Azure Service Bus 및 하이브리드 솔루션](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)에 대해 자세히 알아봅니다.

| 도메인 이름 | 아웃바운드 포트 | 설명 |
| --- | --- | --- |
| *.analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | AMQP(고급 메시지 큐 프로토콜) | 
| *.servicebus.windows.net | 443, 9350-9354 | TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | Hello 게이트웨이 hello Power BI 서비스에 연결할 수 없는 경우 tootest 인터넷 연결을 사용 합니다. | 

다운로드 하 고 hello를 사용 하 여 수 hello 도메인 대신 tooapprove IP 주소를 설정한 경우 [Microsoft Azure 데이터 센터 IP 범위 목록을](https://www.microsoft.com/download/details.aspx?id=41653)합니다. 경우에 따라 hello Azure 서비스 버스 연결은 정규화 된 도메인 이름이 아닌 IP 주소와 함께 만들어집니다.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Hello 데이터 게이트웨이 어떻게 작동 합니까?

hello 데이터 게이트웨이 논리 앱, hello 게이트웨이 클라우드 서비스 및 온-프레미스 데이터 원본 간의 신속 하 고 보안 통신을 용이 하 게 합니다. 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

따라서 hello 클라우드에서 hello 사용자 tooyour 연결 된 요소와 상호 작용 하는 경우 온-프레미스 데이터 원본:

1. hello 게이트웨이 클라우드 서비스 hello 데이터 원본에 대 한 암호화 hello 자격 증명과 함께 쿼리를 만들고 게이트웨이 tooprocess hello에 대 한 hello 쿼리 toohello 큐를 보냅니다.

2. hello 게이트웨이 클라우드 서비스 hello 쿼리를 분석 하 고 hello 요청 toohello Azure 서비스 버스를 푸시합니다.

3. hello 온-프레미스 데이터 게이트웨이 보류 중인 요청 hello에 대 한 Azure 서비스 버스를 폴링합니다.

4. hello 쿼리 가져오고 hello 자격 증명의 암호를 해독 toohello 데이터 원본 자격 증명으로 연결 하는 hello 게이트웨이 합니다.

5. hello 게이트웨이 hello 쿼리 toohello 실행할 데이터 소스에 보냅니다.

6. hello 결과 hello 데이터 원본, 백 toohello 게이트웨이 및 toohello 게이트웨이 클라우드 서비스에서 전송 됩니다. hello 게이트웨이 클라우드 서비스 사용 하 여 hello 결과.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="general"></a>일반

**Q:**: hello 클라우드에서 SQL Azure와 같은 데이터 원본에는 게이트웨이 필요 한가요? <br/>
**A**: 아니요. 게이트웨이는 tooon 온-프레미스 데이터 원본만 연결합니다.

**Q:**: hello 게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 설치 되어 있습니까? <br/>
**A**: 아니요. hello 게이트웨이 제공 된 hello 연결 정보를 사용 하 여 toohello 데이터 소스를 연결 합니다. 이런이 의미에서 클라이언트 응용 프로그램으로 hello 게이트웨이 것이 좋습니다. hello 게이트웨이 hello 기능 tooconnect toohello 서버 이름을 제공 하는 필요 합니다.

<a name="why-azure-work-school-account"></a>

**Q:**: 이유 해야 합니까는 Azure 회사 또는 학교 사용에 대 한 계정 toosign? <br/>
**A**: Azure 작업을 사용 하 여 또는 학교 계정을 hello 온-프레미스 데이터 게이트웨이 설치할 때만 있습니다. 로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다. 일반적으로 Azure AD 계정의 사용자 계정 이름 (UPN)는 hello 전자 메일 주소와 일치 합니다.

**Q**: 자격 증명은 어디에 저장되나요? <br/>
**A**: hello 입력 한 자격 증명이 데이터 원본에 대 한 암호화 및 hello 게이트웨이 클라우드 서비스에 저장 됩니다. hello 온-프레미스 데이터 게이트웨이에 hello 자격 증명의 암호가 해독 됩니다.

**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요? <br/>
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다. 모든 환경은 다름와 전송 중인 데이터 양을 hello hello 결과 영향을 줍니다. ExpressRoute를 사용 하 여 온-프레미스 및 hello Azure 데이터 센터 간 처리량의 수준을 tooguarantee를 도움이 될 수 있습니다.
처리량 hello 타사 도구 Azure 속도 테스트 앱 toohelp 계기를 사용할 수 있습니다.

**Q:**: hello 게이트웨이에서 실행 중인 쿼리 tooa 데이터 원본에 대 한 hello 대기 시간 이란? Hello 최상의 아키텍처는 무엇입니까? <br/>
**A**: tooreduce 네트워크 대기 시간, 가능한 데이터 원본 닫기 toohello로 hello 게이트웨이 설치 합니다. Hello 실제 데이터 원본에 hello 게이트웨이 설치할 수 있습니다,이 근접 단어는 발생 하는 hello 대기 시간을 최소화 합니다. 너무 hello 데이터 센터를 것이 좋습니다. 예를 들어 해당 서비스는 hello 미국 서 부 데이터 센터를 사용 하는 경우 Azure VM에서 호스팅되는 SQL Server 있으면 Azure VM에에서 있어야 hello West US 너무 합니다. 이 근접 대기 시간을 최소화 하 고 hello Azure VM에서 송신 요금을 방지 합니다.

**Q:**: 보낸 결과 백 toohello 클라우드 인가요? <br/>
**A**: 결과 hello Azure 서비스 버스를 통해 전송 됩니다.

**Q:**: hello 클라우드에서 한 인바운드 연결 toohello 게이트웨이가 있습니까? <br/>
**A**: 아니요. hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 사용합니다.

**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요? 수행할 작업 tooopen 필요 합니까? <br/>
**A**: hello 포트 및 호스트 게이트웨이 사용 하 여 hello를 참조 하십시오.

**Q:**: hello 실제 Windows 서비스 섞어?<br/>
**A**: hello 게이트웨이 서비스에서 Power BI 엔터프라이즈 게이트웨이 서비스를 호출 됩니다.

**Q:**: Azure Active Directory 계정으로 실행 하는 게이트웨이 Windows 서비스 hello 수 있습니까? <br/>
**A**: 아니요. hello Windows 서비스에는 유효한 Windows 계정이 있어야 합니다. 기본적으로 hello 서비스는 NT SERVICE\PBIEgwService hello 서비스 SID로 실행 됩니다.

### <a name="high-availability-and-disaster-recovery"></a>고가용성 및 재해 복구

**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요? <br/>
**A**: hello 복구 키 toorestore 사용 하거나 게이트웨이 이동할 수 있습니다. Hello 게이트웨이 설치할 때 hello 복구 키를 지정 합니다.

**Q:**: hello 복구 키의 hello 이점은 무엇입니까? <br/>
**A**: hello 복구 키 방식으로 toomigrate 제공 하거나 재해가 발생 한 후 게이트웨이 설정을 복구 합니다.

**Q:**: hello 게이트웨이와 함께 고가용성 시나리오를 사용 하기 위한 계획이 있습니까? <br/>
**A**: hello 로드맵에 이러한 시나리오는 했지만 아직 시간대가 없습니다.

## <a name="troubleshooting"></a>문제 해결

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Q:**: 어떻게 하는 쿼리를 보내는 toohello 온-프레미스 데이터 원본을 볼 수 있습니까? <br/>
**A**: hello 전송 된 쿼리를 포함 하는 쿼리 추적을 설정할 수 있습니다. Toochange 쿼리 문제 해결를 수행할 때 toohello 원래 값을 추적 해야 합니다. 쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.

또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다. 예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.

**Q:**: hello 게이트웨이 로그는 어디에 있습니까? <br/>
**A**: 이 항목 뒷부분에 나오는 도구를 참조하세요.

### <a name="update-toohello-latest-version"></a>Toohello 최신 버전을 업데이트 합니다.

Hello 게이트웨이 버전이 오래 되 면 많은 문제가 발생할 수 있습니다. 좋은 일반 사례로 hello 최신 버전을 사용 해야 합니다. 한 달 이상 hello 게이트웨이 업데이트 하지 않은 경우 hello 최신 버전의 hello 게이트웨이 설치 하는 것이 좋습니다. 수도 있으며 hello 문제를 재현할 수 있는지를 볼 수 있습니다.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>오류: tooadd 사용자 toogroup을 못했습니다. (-2147463168 PBIEgwService 성능 로그 사용자)

지원 되지 않는 도메인 컨트롤러에 tooinstall hello 게이트웨이 시도 하면이 오류가 발생할 수 있습니다. 도메인 컨트롤러가 아닌 컴퓨터에 hello 게이트웨이 배포 하 고 있는지 확인 합니다.

## <a name="tools"></a>도구

### <a name="collect-logs-from-hello-gateway-configurer"></a>Hello 게이트웨이 configurer에서 로그를 수집 합니다.

Hello 게이트웨이에 대 한 여러 로그를 수집할 수 있습니다. 항상 hello 로그를 시작!

#### <a name="installer-logs"></a>설치 관리자 로그

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>구성 로그

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>엔터프라이즈 게이트웨이 서비스 로그

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>이벤트 로그

데이터 관리 게이트웨이 및 PowerBIGateway 로그 hello를 찾을 수 있습니다 **응용 프로그램 및 서비스 로그**합니다.

### <a name="fiddler-trace"></a>Fiddler 추적

[Fiddler](http://www.telerik.com/fiddler) 는 HTTP 트래픽을 모니터링하는 Telerik의 무료 도구입니다. Hello hello 클라이언트 컴퓨터에서 Power BI 서비스를 사용 하 여이 트래픽을 볼 수 있습니다. 이 서비스는 오류 및 기타 관련된 정보를 표시할 수 있습니다.

## <a name="next-steps"></a>다음 단계
    
* [논리 앱에서 tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md)
* [엔터프라이즈 통합 기능](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Azure Logic Apps용 커넥터](../connectors/apis-list.md)
