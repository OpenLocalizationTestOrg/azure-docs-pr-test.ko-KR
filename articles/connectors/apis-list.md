---
title: "Azure 논리 앱에 대 한 aaaConnectors | Microsoft Docs"
description: "모든 hello 사용 가능한 Microsoft에서 관리 하는 커넥터 toobuild에서 선택 하 고 논리 앱 만들기"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>커넥터 목록
> [!TIP]
> hello [A-Z 전체 목록은](#az) (이 항목)의 논리 앱에서 사용할 수는 모든 hello 사용할 수 있는 커넥터를 나열 합니다. [Connector 세부 정보](/connectors/) 모든 트리거 및 hello swagger에 정의 된 작업과 각 커넥터에 대 한 모든 제한을 나열 합니다.

커넥터는 논리 앱을 만들 때 필수적인 부분입니다. 이러한 커넥터를 사용 하 여 온-프레미스 확장 및 사용자가 만드는 데이터 이미 있는 데이터와 응용 프로그램 toodo 서로 다른 것 클라우드 실제로 있습니다. hello 커넥터 hello 범주에 따라 사용할 수 있습니다. 

* **표준 커넥터**: 논리 앱을 만들 때 자동으로 제공되고 포함됩니다. Service Bus, Power BI, Oracle Database, OneDrive 등을 예로 들 수 있습니다.

* **통합 계정 커넥터**: 통합 계정을 구입할 때 제공됩니다. 이러한 커넥터를 사용하면 XML을 변환하여 유효성을 검사하고, AS2/X12/EDIFACT를 사용하여 기업 간 메시지를 처리하고, 플랫 파일을 인코딩 및 디코딩할 수 있습니다. BizTalk Server와 함께 작업 하는 경우 이러한 커넥터 잘 맞는 tooexpand BizTalk에는 워크플로 Azure로는 합니다.  

    또한 BizTalk 서버에는 [논리 앱 어댑터](https://msdn.microsoft.com/library/mt787163.aspx) tooa 논리 앱을 보내고 받는 논리 앱에서 포함 된 합니다.

* **엔터프라이즈 커넥터**: MQ 및 SAP가 포함됩니다. 추가 비용 지불 시 사용할 수 있습니다. 

[논리 앱 가격](https://azure.microsoft.com/pricing/details/logic-apps/) 및 [가격 책정 모델](../logic-apps/logic-apps-pricing.md) hello 비용에 자세한 정보를 제공 합니다. 

## <a name="popular-connectors"></a>인기 있는 커넥터
이러한 커넥터를 사용하여 데이터와 정보를 성공적으로 처리하는 수천 개의 응용 프로그램과 수백만 개의 실행이 있습니다. 다음 표에서 hello 가장 인기 있는 hello와 일부 즐겨찾기 사용자 들을 보여 줍니다.

| |  |  |  |
| --- | --- | --- | --- |
| [![API 아이콘][AzureBlobStorageicon]<br/>**Azure Blob<br/>Storage**][AzureBlobStoragedoc] | 작업 하려는 경우 tooautomate 모든 저장소 계정과,에이 커넥터에서 보면 해야 합니다. CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 지원합니다. | [![API 아이콘][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | C# 또는 node.js의 사용자 지정 코드 조각을 실행하는 함수를 만들고 논리 앱에서 이러한 함수를 사용합니다.  |
| [![API 아이콘][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | 커넥터에 대 한 대부분 요청 hello 중 하나입니다. 잠재 고객을 사용한 워크플로 자동화 하는 트리거 및 작업 toohelp을 있습니다. | [![API 아이콘][Event-Hubs-icon]<br/>**Event Hubs**][event-hubs-doc] | Event Hub의 이벤트를 사용하고 게시합니다. 예를 들어 이벤트 허브를 사용 하 여 논리 앱에서 출력을 가져올 수 있으며 다음 hello 출력 tooa 실시간 분석 공급자를 보냅니다. |
| [![API 아이콘][FTPicon]<br/>**FTP**][FTPdoc] | FTP 서버에서 액세스할 수 있는 경우 인터넷 hello 다음 워크플로 toowork 파일 및 폴더를 자동화할 수 있습니다. <br/><br/>SFTP은 hello SFTP 커넥터와 함께 사용할 수도 있습니다. | [![API 아이콘][HTTPicon]<br/>**HTTP**][httpdoc] | 논리 앱 toocommunicate 끝점 모든 끝점과 함께 사용 하 여 HTTP를 통해. |
| [![API 아이콘][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | 트리거 및 더 많은 작업 toouse Office 365 전자 메일 및 워크플로 내에서 이벤트를 많이 합니다. <br/><br/>이 커넥터를 포함 한 *전자 메일을 승인* 동작 tooapprove 휴가 요청 경비 보고서, 및 등입니다. <br/><br/>Office 365 사용자 hello Office 365 사용자 커넥터와 함께 사용할 수 있습니다.| [![API 아이콘][HTTP-Requesticon]<br/>**요청/응답**][HTTP-Requestdoc] | 이 커넥터는 HTTPS URL을 제공합니다. Hello 논리 앱 요청 toothis URL을 받으면 hello 논리 앱 시작 합니다. |
| [![API 아이콘][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | 쉽게 프로그램 Salesforce 계정 tooget 액세스 tooobjects, 잠재 고객 같은 등을 사용 하 여 로그인 합니다. |  [![API 아이콘][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | 트리거 및 작업 toodo 비동기 메시징 및 큐, 구독 및 항목 게시/구독 hello 논리 앱 내에서 가장 인기 있는 커넥터를 포함합니다. |
|  [![API 아이콘][SharePointicon]<br/>**SharePoint<br/>온라인**][SharePointdoc] | SharePoint로 작업을 수행하며 자동화가 도움이 되는 경우 이 커넥터를 자세히 살펴보시기 바랍니다. 온-프레미스 SharePoint 및 SharePoint Online과 함께 사용할 수 있습니다. | [![API 아이콘][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Hello 중 가장 사용 하는 커넥터, tooan를 연결할 수 있는 온-프레미스 SQL Server 및 Azure SQL 데이터베이스입니다. | 
| [![API 아이콘][Twittericon]<br/>**Twitter**][Twitterdoc] | Twitter 계정으로 간단하게 로그인한 후 새 트윗이 게시될 때 워크플로를 시작합니다. 그런 다음 이러한 트 윗 tooa SQL 데이터베이스 또는 SharePoint 목록을 저장 합니다. | | | 

## <a name="integration-account-connectors"></a>통합 계정 커넥터 

엔터프라이즈 통합 팩 (EIP) hello 커넥터는 잘 알려진 toohello BizTalk Server 커뮤니티를 포함 합니다. 구입할 때는 [통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), 용량도 커넥터 다음 hello: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API 아이콘][as2icon]<br/>**AS2</br>디코딩**][as2decode] | [![API 아이콘][as2icon]<br/>**AS2</br>인코딩**][as2encode] | [![API 아이콘][x12icon]<br/>**EDIFACT</br>디코딩**][EDIFACTdecode] | [![API 아이콘][x12icon]<br/>**EDIFACT</br>인코딩**][EDIFACTencode] |
[![API 아이콘][flatfileicon]<br/>**플랫 파일</br>인코딩**][flatfiledoc] | [![API 아이콘][flatfiledecodeicon]<br/>**플랫 파일</br>디코딩**][flatfiledecodedoc] | [![API 아이콘][integrationaccounticon]<br/>**통합<br/>계정**][integrationaccountdoc] | [![API 아이콘][xmltransformicon]<br/>**변환<br/>XML**][xmltransformdoc] |
| [![API 아이콘][x12icon]<br/>**X12</br>디코딩**][x12decode] | [![API 아이콘][x12icon]<br/>**X12</br>인코딩**][x12encode] | [![API 아이콘][xmlvalidateicon]<br/>**XML <br/>유효성 검사**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>엔터프라이즈 커넥터

논리 앱 내에서 tooyour 엔터프라이즈 응용 프로그램을 연결 합니다.

|  |  |
| --- | --- |
|[![API 아이콘][MQicon]<br/>**MQ**][mqdoc]|[![API 아이콘][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>A-Z 전체 목록

[Connector 세부 정보](/connectors/) 모든 트리거 및 hello swagger에 정의 된 작업을 나열 하 고 각 커넥터에 대 한 모든 제한을 나열 합니다.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 약속 일정<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure AD(Active Directory)<br/>Azure API Management<br/>Azure App Services<br/>Azure 응용 프로그램<br/>Azure Automation<br/>[Azure Blob Storage][azureblobstoragedoc]<br/>Azure 데이터 레이크<br/>Azure DocumentDB(Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Azure 큐<br/>Azure 리소스 관리자<br/>[Azure SQL Database][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>벤치마크 전자 메일<br/>Bing Search<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito 양식<br/>Cognitive Services Computer Vision API<br/>Cognitive Services Face API<br/>Cognitive Services LUIS<br/>Cognitive Services 텍스트 분석<br/>Common Data Service<br/>콘텐츠 변환<br/>제어-종료<br/>[사용자 지정 API/웹앱][api/web-appdoc]<br/><br/><a name="d"></a>데이터 작업<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>동적 NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Event Hubs][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[파일 시스템][filesystemdoc]<br/>[플랫 파일][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>Freshservice<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google 캘린더<br/>Google 연락처<br/>Google 드라이브<br/>Google Sheets<br/>Google 태스크<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>통합 계정<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>중간<br/>Microsoft Forms<br/>Microsoft 팀<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN 날씨<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365 사용자<br/>Office 365 비디오<br/>OneDrive<br/>OneDrive for Business<br/>OneNote(Business)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook 고객 관리자<br/>Outlook 작업<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[요청/응답][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP 응용 프로그램 서버][sapconnector]<br/>[SAP 메시지 서버][sapconnector]<br/>[일정][recurrencedoc]<br/>범위<br/>SendGrid<br/>메시지 toobatch 보내기<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>스트라이프<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork 프로젝트<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[XML 변환][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>변수<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML 유효성 검사][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> Azure 계정에 등록 하기 전에 Azure 논리 앱 시작 tooget 너무 이동[논리 앱 시도](https://tryappservice.azure.com/?appservice=logic)합니다. 단기 시작 논리 앱을 즉시 만들 수 있습니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.

## <a name="connectors-as-triggers-and-actions"></a>트리거 및 작업으로 사용되는 커넥터

**트리거**는 논리 앱의 인스턴스를 시작하거나 실행합니다. 일부 커넥터는 특정 이벤트가 발생하면 앱에 알리는 트리거를 제공합니다. 예를 들어 hello FTP 커넥터는 hello `OnUpdatedFile` 파일 업데이트 될 때 논리 앱을 시작 하는 트리거. 

논리 앱 유형의 트리거인 다음 hello를 다음과 같습니다.  

* *트리거를 폴링하여*:이 트리거 새 데이터에 대 한 서비스에 지정 된 빈도 toocheck 폴링합니다. 

    새 데이터를 사용할 수 있는 논리 앱의 새 인스턴스를 입력으로 hello 데이터도 실행 됩니다. 

* *트리거를 푸시*:이 트리거는 끝점에서 데이터를 수신 대기 또는 이벤트에 대 한 toohappen, 다음 트리거에서 논리 앱의 새 인스턴스.

* *되풀이 트리거*: 이 트리거는 정해진 일정에 따라 논리 앱의 인스턴스를 인스턴스화합니다.

또한 커넥터는 워크플로에서 사용할 수 있는 **작업**을 제공합니다. 예를 들어 논리 앱은 데이터를 조회한 후 나중에 이 데이터를 논리 앱에서 사용할 수 있습니다. 보다 구체적으로, SQL 데이터베이스에서 고객 데이터를 조회 수 있으며 다음이 고객 데이터 toobuild을 워크플로에서 사용. 

> [!TIP]
> [커넥터 개요](connectors-overview.md)는 트리거 및 작업에 대한 세부 정보를 제공합니다. 


## <a name="message-manipulation-actions"></a>메시지 조작 작업

논리 앱에는 페이로드 데이터를 변경 또는 조작할 수 있는 기본 제공 작업이 포함되어 있습니다. 기본 제공 hello **데이터 작업** 커넥터 포함 작업을 수행 하는 hello: 

| | |
|---|---|
| **작성** | 빌드 또는 toouse 값 이나 개체를 나중에 생성 또는 때 워크플로 작성 합니다. 예를 들어 여러 단계에서 값이 포함 된 JSON 개체를 작성 하거나 실행 논리 앱의 뒷부분에 나오는 상수 tooreference 계산할 수 있습니다. |
| **CSV 테이블 만들기**<br/>**HTML 테이블 만들기** | 배열 결과 집합을 CSV 또는 HTML 테이블로 변환합니다. 예를 들어 hello CRM "레코드" 동작을 추가 하 고 오늘 추가 된 레코드에 대 한 필터를 추가 합니다. 그런 다음 전자 메일에서 HTML 테이블로 hello 결과 보냅니다. |
| **배열 필터링**(쿼리) | 관심이 있는 결과 집합 toohello 항목을 필터링 합니다. 예를 들어 있는 모든 트 윗 검색 `#Azure`, 다음 "필터" hello 반환 트 윗 tooonly 반환 결과 `Tweeted_by_followers > 50`합니다. |
| **Join** | 구분 기호를 사용하여 배열을 조인합니다. 예를 들어 hello 키 구를 검색 작업에는 키 구의 배열을 반환합니다. `,` 또는 비슷한 것을 사용하여 핵심 문구를 "조인"할 수 있습니다. 따라서 `["Some", "Phrase"]` 대신 `"Some, Phrase"`가 있습니다. |
| **JSON 구문 분석** | 구문 분석 하 고 hello 디자이너에서 JSON 개체에서 값에 액세스 합니다. 예를 들어 Azure 함수는 JSON 페이로드를 반환 하는 경우 다음 구문을 분석할 수 있습니다 것 나중에 다른 단계에서에서 tooaccess hello JSON 속성입니다. 또한 hello 동작 해당 hello JSON 일치 hello 지정된 런타임에 스키마를 확인합니다. | 
| **선택** | 추가 처리를 위해 배열의 특정 속성을 선택합니다. SQL에서 "레코드 나열" 작업을 수행했더니 15개 열이 반환되는 경우 그 중에서 추가로 처리할 열 몇 개만 선택합니다. hello 출력은 선택한 hello 속성을 포함 하는 배열입니다. |

## <a name="custom-connectors-and-azure-certification"></a>사용자 지정 커넥터 및 Azure 인증 

커넥터를 사용할 수 없는 사용자 지정 코드를 실행 하는 Api toocall, hello 논리 앱 플랫폼으로 확장할 수 있습니다 [는 사용자 지정 커넥터 REST 기반 API 앱을 만드는](../logic-apps/logic-apps-create-api-app.md)합니다. 

사용자 지정 API 앱 공개할 toouse Azure에서 toomake 하려는 경우 다음 위한 추천 toohello 제출 [Microsoft Azure 인증 프로그램](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/)합니다.

## <a name="get-help"></a>도움말 보기

tooask 질문과 대답 질문 다른 Azure 논리 앱 사용자가 수행 하는 참조 이동 toohello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

커넥터 항목이나 중요하다고 생각 한 세부 정보를 빠뜨린 것이 있습니까? 그렇다면 tooour 기존 항목을 추가 하 여 도움을 줍니다 하거나 직접 작성 하는 것입니다. 설명서는 오픈 소스이며 GitHub에서 호스트됩니다. [GitHub 리포지토리](https://github.com/Microsoft/azure-docs)에서 시작하세요. 

## <a name="next-steps"></a>다음 단계
* [첫 번째 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)
* [논리 앱에 대한 사용자 지정 API 만들기](../logic-apps/logic-apps-create-api-app.md)
* [논리 앱 모니터링](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "App Service API Apps과 논리 앱 통합"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Azure Blob Storage 커넥터와 Blob 컨테이너의 파일 관리"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "논리 앱을 Azure Functions와 통합"
[db2doc]: ./connectors-create-api-db2.md "TooIBM DB2 hello 클라우드 또는 온-프레미스에 연결 합니다. 행 업데이트, 테이블 가져오기 등"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "CRM Online 데이터로 작업할 수 있도록 tooDynamics CRM Online에 연결"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "TooAzure 이벤트 허브를 연결 합니다. Logic Apps과 Event Hubs 간 이벤트 주고 받기"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Tooan 온-프레미스 파일 시스템에 연결"
[ftpdoc]: ./connectors-create-api-ftp.md "FTP tooan 연결 / FTPS 서버에 업로드 하 고, 같은 FTP 작업에 가져오기, 파일 등를 삭제 합니다."
[httpdoc]: ./connectors-native-http.md "Hello HTTP 커넥터와 함께 HTTP 호출 만들기"
[http-requestdoc]: ./connectors-native-reqres.md "HTTP 요청 및 응답 tooyour 논리 앱에 대 한 작업 추가"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "HTTP + Swagger 커넥터를 사용하여 HTTP 호출"
[informixdoc]: ./connectors-create-api-informix.md "TooInformix hello 클라우드 또는 온-프레미스에 연결 합니다. 행, hello 테이블 목록 및 읽기"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "중첩된 워크플로와 논리 앱 통합"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Tooyour Office 365 계정을 연결 하세요. 메일 전송과 수신, 일정과 연락처 관리 등"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Oracle 데이터베이스 tooadd tooan, 삽입, 행 삭제 등 연결"
[mqdoc]: ./connectors-create-api-mq.md "TooMQ 온-프레미스 또는 Azure를 연결 하 고, 전송 및 메시지를 수신 합니다."
[recurrencedoc]:  ./connectors-native-recurrence.md "논리 앱에 대한 되풀이 작업 트리거"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Tooyour Salesforce 계정을 연결 하세요. 계정, 잠재 고객, 영업 기회 관리 등"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Tooan 온-프레미스 SAP 시스템에 연결"
[service-busdoc]: ./connectors-create-api-servicebus.md "Service Bus 큐 및 항목에서 메시지를 보내고 Service Bus 큐 및 구독에서 메시지를 받습니다."
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "온라인 tooSharePoint를 연결 합니다. 문서 관리, 항목 나열 등"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "TooSharePoint 프레미스 서버에 연결 합니다. 문서 관리, 항목 나열 등"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "TooAzure SQL 데이터베이스 또는 SQL server에 연결 합니다. SQL Database 테이블에서 항목 생성, 업데이트, 가져오기 및 삭제"
[twitterdoc]: ./connectors-create-api-twitter.md "TooTwitter를 연결 합니다. 타임라인 가져오기, 트윗에 게시 등"
[webhookdoc]: ./connectors-native-webhook.md "Webhook 동작 및 트리거 tooyour 논리 앱 추가"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "엔터프라이즈 통합 AS2에 대해 알아봅니다."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "엔터프라이즈 통합 X12에 대해 알아봅니다."
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "엔터프라이즈 통합 플랫 파일에 대해 알아봅니다."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "엔터프라이즈 통합 플랫 파일에 대해 알아봅니다."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "엔터프라이즈 통합 XML 유효성 검사에 대해 알아봅니다."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "엔터프라이즈 통합 변환에 대해 알아봅니다."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "엔터프라이즈 통합 AS2 디코딩에 대해 알아봅니다."
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "엔터프라이즈 통합 AS2 인코딩에 대해 알아봅니다."
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "엔터프라이즈 통합 X12 디코딩에 대해 알아봅니다."
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "엔터프라이즈 통합 X12 인코딩에 대해 알아봅니다."
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "엔터프라이즈 통합 EDIFACT 디코딩에 대해 알아봅니다."
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "엔터프라이즈 통합 EDIFACT 인코딩에 대해 알아봅니다."
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "통합 계정에서 스키마, 맵, 파트너 등을 조회"


[boxDoc]: ./connectors-create-api-box.md "TooBox를 연결 합니다. 파일 업로드, 가져오기, 삭제, 나열 등"
[delaydoc]: ./connectors-native-delay.md "지연된 작업 수행"
[dropboxdoc]: ./connectors-create-api-dropbox.md "TooDropbox를 연결 합니다. 파일 업로드, 가져오기, 삭제, 나열 등"
[facebookdoc]: ./connectors-create-api-facebook.md "TooFacebook를 연결 합니다. Tooa 타임 라인 사후, 피드, 페이지 및 기타 가져오기"
[githubdoc]: ./connectors-create-api-github.md "TooGitHub 연결 하 고 문제를 추적 합니다."
[google-drivedoc]: ./connectors-create-api-googledrive.md "데이터와 함께 작동할 수 있도록 tooGoogleDrive 연결"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "시트를 수정할 수 있습니다 수 있도록 tooGoogle 시트 연결"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "작업을 관리할 수 있도록 tooGoogle 태스크를 연결 합니다."
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "TooGoogle 일정을 연결 하 고 일정을 관리할 수 있습니다."
[http-responsedoc]: ./connectors-native-reqres.md "HTTP 요청 및 응답 tooyour 논리 앱에 대 한 작업 추가"
[instagramdoc]: ./connectors-create-api-instagram.md "TooInstagram를 연결 합니다. 이벤트에서 트리거 또는 작업"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Tooyour MailChimp 계정을 연결 하세요. 메일 관리 및 자동화"
[mandrilldoc]: ./connectors-create-api-mandrill.md "TooMandrill 통신에 대 한 연결"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "TooMicrosoft 변환기를 연결 합니다. 텍스트 번역, 언어 감지 등" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Office 365 비디오에 대한 비디오 정보, 비디오 목록과 채널 및 재생 URL 가져오기"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Tooyour 연결 개인 Microsoft OneDrive. 파일 업로드, 삭제, 나열 등"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Microsoft OneDrive tooyour 비즈니스를 연결 합니다. 파일 업로드, 삭제, 나열 등"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Tooyour Outlook 사서함을 연결 합니다. 전자 메일, 일정, 연락처 관리 등"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "TooMicrosoft Project Online을 연결 합니다. 프로젝트, 태스크, 리소스 관리 등"
[querydoc]: ./connectors-native-query.md "선택 하 고 hello 쿼리 동작을 가진 배열 필터링"
[rssdoc]: ./connectors-create-api-rss.md "게시 및 피드 항목을 검색 하 고, 새 항목은 게시 된 tooan RSS 때 작업을 트리거할 피드입니다."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "TooSendGrid를 연결 합니다. 전자 메일 보내기 및 수신자 목록 관리"
[sftpdoc]: ./connectors-create-api-sftp.md "Tooyour SFTP 계정을 연결 하세요. 파일 업로드, 가져오기, 삭제 등"
[slackdoc]: ./connectors-create-api-slack.md "TooSlack 연결 하 고 tooSlack 채널 메시지를 게시 합니다."
[smtpdoc]: ./connectors-create-api-smtp.md "첨부 파일이 있는 메일을 보내고 tooa SMTP 서버 연결"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "TooSparkPost 통신에 대 한 연결"
[trellodoc]: ./connectors-create-api-trello.md "TooTrello를 연결 합니다. 프로젝트 관리 및 다른 사람과 작업 구성"
[twiliodoc]: ./connectors-create-api-twilio.md "TooTwilio를 연결 합니다. 메시지 보내기 및 가져오기, 사용 가능한 번호 가져오기 수신 전화 번호 관리 등"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "TooWunderlist를 연결 합니다. 태스크 및 할 일 목록 관리, 동기화된 업무 유지 등"
[yammerdoc]: ./connectors-create-api-yammer.md "TooYammer를 연결 합니다. 메시지 게시, 새 메시지 가져오기 등"
[youtubedoc]: ./connectors-create-api-youtube.md "TooYouTube를 연결 합니다. 비디오 및 채널 관리"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
