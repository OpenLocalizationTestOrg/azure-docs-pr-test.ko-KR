---
title: "Azure BizTalk 서비스에 대 한 aaaRelease 노트 | Microsoft Docs"
description: "Hello Azure BizTalk 서비스에 대 한 알려진 문제를 나열 합니다."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Azure BizTalk 서비스에 대한 릴리스 정보

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

hello Microsoft Azure BizTalk 서비스에 대 한 hello 릴리스 정보에는이 버전의 알려진 문제 hello를 포함 합니다.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>BizTalk 서비스의 hello 11 월 업데이트의 새로운 기능
* Hello BizTalk 서비스 포털에서에서 휴지 암호화를 사용할 수 있습니다. [BizTalk 서비스 포털에서 휴지 상태의 암호화 사용](https://msdn.microsoft.com/library/azure/dn874052.aspx)을 참조하세요.

## <a name="update-history"></a>업데이트 내역
### <a name="october-update"></a>10월 업데이트
* 조직 계정이 지원됩니다.  
  * **시나리오**: Microsoft 계정(예: user@live.com)을 사용하여 BizTalk 서비스 배포를 등록했습니다. 이 시나리오에서는 Microsoft 계정 사용자를 관리할 수만 hello BizTalk 서비스 포털을 사용 하 여 BizTalk 서비스를 hello 합니다. 조직 계정을 사용할 수 없습니다.  
  * **시나리오**: Azure Active Directory의 조직 계정(예: user@fabrikam.com 또는 user@contoso.com)을 사용하여 BizTalk 서비스 배포를 등록했습니다. 이 시나리오에서는 hello 관리할 수 같은 조직 내의 Azure Active Directory 사용자만 BizTalk 서비스 hello BizTalk 서비스 포털을 사용 하 여 hello 합니다. Microsoft 계정을 사용할 수 없습니다.  
* Hello Azure 클래식 포털에서에서 BizTalk 서비스를 만들 때 자동으로 hello BizTalk 서비스 포털에에서 등록 됩니다.
  * **시나리오**: BizTalk 서비스를 만든 hello Azure 클래식 포털에 로그인 한 다음 선택 **관리** hello 맨 처음에 대 한 합니다. Hello BizTalk 서비스 포털도 열립니다 hello BizTalk 서비스가 자동으로 등록 하 고 배포에 대해 준비 합니다.  
    참조 [등록 하 고 BizTalk 서비스 배포에서 업데이트 hello BizTalk 서비스 포털](https://msdn.microsoft.com/library/azure/hh689837.aspx)합니다.  

### <a name="august-14-update"></a>8월 14일 업데이트
* 이제 규약과 브리지 분리 – 거래 업체 규약 및 브리지 hello BizTalk 서비스 포털에서에서 분리 됩니다. 이제 규약 및 브리지를 별도로 만들 하 고 런타임 브리지에서 EDI 메시지 hello hello 값에 따라 tooan 규약을 확인 합니다. [Azure BizTalk 서비스에서 규약 만들기](https://msdn.microsoft.com/library/azure/hh689908.aspx), [BizTalk 서비스 포털을 사용하여 EDI 브리지 만들기](https://msdn.microsoft.com/library/azure/dn793986.aspx), [BizTalk 서비스 포털을 사용하여 AS2 브리지 만들기](https://msdn.microsoft.com/library/azure/dn793993.aspx) 및 [런타임에 브리지를 규약으로 확인하는 방법](https://msdn.microsoft.com/library/azure/dn794001.aspx)을 참조하세요.  
* 계약에 대 한 hello 옵션 toocreate 템플릿은 중단 되었습니다.  
* 이제 hello 송신 측 규약에 대 한 각 스키마에 대 한 서로 다른 구분 기호 집합을 지정할 수 있습니다. 이 구성은 송신 측 규약의 프로토콜 설정 아래에 지정됩니다. 자세한 내용은 [Azure BizTalk 서비스에 X12 규약 만들기](https://msdn.microsoft.com/library/azure/hh689847.aspx) 및 [Azure BizTalk 서비스에 EDIFACT 규약 만들기](https://msdn.microsoft.com/library/azure/dn606267.aspx)를 참조하세요. 두 개의 새 엔터티가 TPM OM API toohello hello에 대 한도 추가 같은 목적으로 사용 합니다. [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) 및 [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx)를 참조하세요.  
* 파생 형식을 포함한 표준 XSD 항목이 이제 지원됩니다. [맵에 표준 XSD 항목 사용](https://msdn.microsoft.com/library/azure/dn793987.aspx) 및 [매핑 시나리오 및 예제에서 파생 형식 사용](https://msdn.microsoft.com/library/azure/dn793997.aspx)을 참조하세요.  
* AS2는 메시지 서명을 위한 새 MIC 알고리즘 및 새로운 암호화 알고리즘을 지원합니다. [Azure BizTalk 서비스에서 AS2 규약 만들기](https://msdn.microsoft.com/library/azure/hh689890.aspx)를 참조하세요.  
  ## <a name="know-issues"></a>알려진 문제

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>BizTalk 서비스 포털 업데이트 후의 연결 문제
  Hello BizTalk 서비스를 업그레이드 하는 동안 BizTalk 서비스 포털에 열이 있는 경우에 tooroll toohello 서비스를 변경, hello BizTalk 서비스 포털에 연결 문제가 발생할 수 있습니다.  
  문제를 해결 hello 브라우저를 다시 시작 hello 브라우저 캐시를 삭제 하거나 개인 모드에서 hello 포털을 시작 될 수 있습니다.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>오류 또는 BizTalk 서비스 프로젝트에서 경고를 클릭 하면 visual Studio IDE hello 아티팩트를 찾을 수 없습니다.
Visual Studio 2012 업데이트 3 RC 1 hello toofix hello 문제를 설치 합니다.  

### <a name="custom-binding-project-reference"></a>사용자 지정 바인딩 프로젝트 참조
Hello BizTalk 서비스 프로젝트를 Visual Studio 솔루션에서의 경우 다음을 고려 합니다.  

* BizTalk 서비스 프로젝트와 사용자 지정 바인딩 프로젝트, 동일한 Visual Studio 솔루션 hello 합니다. BizTalk 서비스 프로젝트 hello 참조 toothis 사용자 지정 바인딩 프로젝트 파일을 있습니다.
* BizTalk 서비스 프로젝트 hello 참조 tooa 사용자 지정 바인딩/동작 DLL에 있습니다.

Visual Studio에서 솔루션을 성공적으로 hello '빌드' 있습니다. 그런 다음 '다시 빌드' 하거나 '정리' hello 솔루션입니다. 그 후 빌드하거나 정리를 다시 다음 hello 오류가 발생 합니다.  
  없습니다 toocopy 파일 <Path tooDLL> too"bin\Debug\FileName.dll"입니다. hello 프로세스가 다른 프로세스에서 사용 되 고 'bin\Debug\FileName.dll' hello 파일을 액세스할 수 없습니다.  

#### <a name="workaround"></a>해결 방법
* 경우 [Visual Studio 2012 업데이트 3](https://www.microsoft.com/download/details.aspx?id=39305) 가 설치 되어 있으면 hello 다음 두 가지 옵션:
  
  * Visual Studio를 다시 시작하거나
  * Hello 솔루션을 다시 시작 합니다. 그런 다음 hello 솔루션에서 빌드만을 수행 합니다.  
* 경우 [Visual Studio 2012 업데이트 3](https://www.microsoft.com/download/details.aspx?id=39305) 가 설치 되지 않은 작업 관리자를 열고 hello 프로세스 탭, hello MSBuild.exe 프로세스를 클릭을 hello 프로세스 끝내기 단추를 클릭 합니다.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>라우팅 tooBasicHttpRelay 끝점에서 지원 되지 않습니다 브리지 및 BizTalk 서비스 포털 수 없는 문자가 HTTP 헤더로 승격 된 경우
승격 된 속성의 일부분으로 인쇄할 수 없는 문자를 사용 하 여 메시지에 대 한 이러한 메시지 hello BasicHttpRelay 바인딩을 사용 하는 라우트된 toorelay 대상이 될 수 없습니다. 또한 hello 및 대상에 대 한 인코딩되지 않은 blob에 대 한 URL로 인코딩된 추적의 일부분으로 사용할 수 있는 속성을 승격 합니다.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>Hello 보낼 비동기 MDN 옵션 선택 하지 않은 경우에 MDN이 비동기적으로 전송
Hello를 선택한 경우 다음과 같은이 시나리오를 고려해 **비동기 MDN 보내기** 확인란을 선택 하 고 URL toosend hello 비동기 MDN을 지정 to, 다음 hello 확인란 선택을 취소 하 고 **비동기 MDN 보내기** 확인란 다시 hello MDN은 여전히 보낸된 toohello hello 옵션 toosend 비동기 Mdn을 선택 하지 않은 경우에 URL을 지정 합니다.  
선택을 취소 해야이 문제를 해결 hello hello 선택을 취소 하기 전에 URL을 지정 **비동기 MDN 보내기** 확인란을 선택 하 고 다음 hello AS2 규약을 배포 합니다.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>빈 메시지 전송 toobe toohello 유효한 교환 발생 하는 외부에 공백 문자가 끝점 일시 중단
IEA 세그먼트 외부에 공백이 있으면 hello 디스어셈블러는 현재 교환의 끝으로이 처리 하 고 공백으로 다음 메시지로 hello 다음 집합에서 찾습니다. 정상적인 메시지 하나가 toohello 경로 대상 보내집니다 및 빈 메시지 하나가 hello 보내집니다 알 수 유효한 교환 하지 이므로 끝점 일시 중단 합니다.  

### <a name="tracking-in-biztalk-services-portal"></a>Azure BizTalk 서비스 포털에서 추적
Toohello EDI 메시지 처리 및 상관 관계를 추적 이벤트가 캡처됩니다. Hello 프로토콜 단계 외부에서 메시지가 실패 하면 추적 성공으로 표시 됩니다. 이 경우 참조 hello 아래 LOG 섹션에서 toohello **세부 정보** 열에 **추적** 오류 세부 정보에 대 한 합니다.
hello X12 수신 및 송신 설정 ([x12 만들기 Azure BizTalk 서비스의 계약](https://msdn.microsoft.com/library/azure/hh689847.aspx)) hello 프로토콜 단계에 정보를 제공 합니다.  

### <a name="update-agreement"></a>업데이트 규약
BizTalk 서비스 포털 hello가 있습니다 toomodify hello를 Id의 한정자 규약이 구성 된 경우. 이로 인해 속성이 일치하지 않을 수 있습니다. 예를 들어, zz: 1234567 및 zz: 7654321 hello 한정자를 사용 하 여 규약입니다. Hello BizTalk 서비스 포털 프로필 설정에서 zz: 1234567 toobe 01:ChangedValue 변경할 수 있습니다. Hello 계약 열고 01:ChangedValue zz: 1234567 대신 표시 됩니다.
toomodify hello 삭제 hello 규약 id의 한정자 업데이트 **Identities** 에 파트너 프로필 hello 한 다음 다시 hello 계약입니다.  

> AZURE.WARNING 이 동작은 X12 및 AS2에 영향을 줍니다.  
> 
> 

### <a name="as2-attachments"></a>AS2 첨부 파일
AS2 메시지의 첨부 파일의 송신 및 수신은 지원되지 않습니다. 특히, 첨부 파일은 자동으로 무시 하 고 hello 메시지 본문을 일반 AS2 메시지로 처리 됩니다.  

### <a name="resources-remembering-path"></a>리소스: 경로 기억
추가할 때 **리소스**, hello 대화 상자 창이 hello 사용 했던 경로가 tooadd 리소스를 기억 하지 않을 수 있습니다. tooremember hello 이전에 사용 되는 경로 너무 hello BizTalk 서비스 포털 웹 사이트를 추가 하는 시도**신뢰할 수 있는 사이트** Internet Explorer에서 합니다.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>변경 내용을 저장 하지 않고 hello 엔터티 이름 브리지 및 닫기 hello 프로젝트의 이름을 바꾸면 오류가 발생 hello 엔터티를 다시 여세요
순서에 따라 hello의 시나리오를 고려 합니다.  

* 브리지 (예: XML 단방향 브리지) tooa BizTalk 서비스 프로젝트 추가  
* Hello 브리지 hello 엔터티 이름 속성에 대 한 값을 지정 하 여 이름을 바꿉니다. 이 지정한 hello 이름의 hello 관련된.bridgeconfig 파일을 이름을 바꿉니다.  
* Hello 변경 내용을 저장 하지 않고 (Visual Studio에서 탭 hello 닫아) hello.bcs 파일을 닫습니다.  
* Hello 솔루션 탐색기에서에서 다시 hello.bcs 파일을 엽니다.  
  Hello 관련된.bridgeconfig 파일에 있는 hello 새 이름을 지정한 경우 동안 hello 디자인 화면에서 엔터티 이름을 hello 여전히 hello 이전 이름 인지를 확인할 수 있습니다. Tooopen hello 브리지 구성에서 hello 브리지 구성 요소를 두 번 클릭 하면 다음 오류가 hello를 메시지가 나타납니다.  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid이이 시나리오에서는 실행 중인 BizTalk 서비스 프로젝트의 hello 엔터티 이름을 바꾼 후 변경 내용을 저장 하 고 있는지 확인 합니다.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>Visual Studio 프로젝트에서 아티팩트가 제외되어도 BizTalk 서비스 프로젝트가 성공적으로 빌드됩니다.
추가 아티팩트 (예를 들어 XSD 파일) tooa BizTalk 서비스 프로젝트, (예를 들어 지정 하 여 요청 메시지 유형으로), hello 브리지 구성에에서 해당 아티팩트를 포함 하 고 있는 다음 hello Visual Studio 프로젝트에서 제외 되는 시나리오를 살펴보겠습니다. 이러한 경우 hello 프로젝트를 빌드하면 제공 되지 것입니다 오류 삭제 hello 아티팩트는 hello 디스크 hello에 사용할 수 있는 위치 hello Visual Studio 프로젝트에 포함 된 위치와 동일 합니다.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>BizTalk 서비스 프로젝트 hello hello 브리지를 구성 하는 동안 스키마 가용성을 확인 하지 않습니다.
BizTalk 서비스 프로젝트에서 toohello 프로젝트에 추가 된 스키마는 다른 스키마를 가져오는 경우 BizTalk 서비스 프로젝트 hello 확인 하지 않습니다 hello 가져온된 스키마 toohello 프로젝트에 추가 되는지 여부. Toobuild 이러한 프로젝트를 시도 하면 빌드 오류가 발생 하지 않습니다.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>XML 요청-회신 브리지에 대 한 hello 응답 메시지는 항상 utf-8 문자 집합임
이 릴리스에 대 한 XML 요청-회신 브리지에서 hello 응답 메시지의 hello charset tooUTF 8 항상 설정 됩니다.
  
### <a name="user-defined-datatypes"></a>사용자 정의 데이터 형식
hello BizTalk Adapter Pack 어댑터 hello BizTalk 어댑터 서비스 기능 내에서 어댑터 작업에 대 한 사용자 정의 데이터 형식을 활용할 수 있습니다.
사용자 정의 데이터를 사용할 때는 hello 파일 (.dll) toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ 또는 toohello 전역 어셈블리 캐시 (GAC) hello BizTalk 어댑터 서비스 서비스를 호스트 하는 hello 서버에 복사 합니다. 그렇지 않으면 다음 오류가 hello hello 클라이언트에서 발생할 수 있습니다.  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> 것이 권장된 toouse GACUtil.exe tooinstall hello 전역 어셈블리 캐시에 파일을 합니다. GACUtil.exe 문서 어떻게 toouse이 도구 및 hello Visual Studio 명령줄 옵션입니다.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Hello BizTalk 어댑터 서비스 웹 사이트를 다시 시작
설치 hello **BizTalk 어댑터 서비스 런타임*** hello 만듭니다 **BizTalk 어댑터 서비스** hello를 포함 하는 IIS의 웹 사이트 **BAService** 응용 프로그램입니다. **BAService** 내부적으로 사용 하 여 릴레이 바인딩 tooextend hello의 도달 범위 온-프레미스 서비스 끝점 toohello 클라우드 응용 프로그램입니다. Hello 온-프레미스 서비스가 시작 될 경우에 hello 해당 릴레이 끝점을 호스팅된 서비스에서 온-프레미스, 서비스 버스 hello에 등록 됩니다.  

중지 하 고 응용 프로그램을 시작 하는 경우 응용 프로그램 자동 시작에 대 한 hello 구성은 인식 되지 않습니다. 따라서 **BAService** 가 중지 항상 다시 시작 해야 hello **BizTalk 어댑터 서비스** 웹 사이트를 대신 합니다. 시작 하거나 중지 hello **BAService** 응용 프로그램입니다.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>LOB 구성 요소의 주소 및 엔터티 이름에 특수 문자를 사용할 수 없음
LOB 구성 요소의 주소 및 엔터티 이름에 특수 문자를 사용하지 않아야 합니다. 이렇게 하면, hello BizTalk 서비스 프로젝트를 배포 하는 동안 오류가 발생 합니다. 특정 '%'와 같은 문자가, hello BizTalk 어댑터 서비스 웹 사이트 수 중지 상태로 이동한 다음 toomanually 시작 해야 합니다.

### <a name="test-map-with-get-context-property"></a>컨텍스트 속성 가져오기로 맵 테스트
변환에 **컨텍스트 속성 가져오기** 매핑 작업이 포함된 경우 **맵 테스트**는 실패합니다. 임시 해결 방법으로 대체 hello **컨텍스트 속성 가져오기** String Concatenate 맵 작업을 더미 데이터가 포함 된 맵 작업입니다. Hello 대상 스키마를 채우는 되 고 다른 전송 기능을 테스트할 수 있습니다.

### <a name="test-map-property-does-not-display"></a>TestMap 속성이 표시되지 않음
hello **Testmap** Visual Studio에서 속성을 표시 하지 않습니다. 이 경우 hello 발생할 수 있습니다 **속성** 창과 hello **솔루션 탐색기** 창을 동시에 도킹 되지 됩니다. tooresolve이, 도킹 hello **속성** 및 hello **솔루션 탐색기** windows 합니다.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>DateTime 서식 다시 지정 드롭다운이 회색 표시됨
DateTime Reformat 맵 작업이 추가 될 때 toohello 디자인 화면 및 구성한 hello 서식 드롭다운 목록이 회색 수 있습니다. Hello 컴퓨터 디스플레이 설정 된 경우 이러한 현상이 **중간 – 125%** 또는 **크게 – 150%**합니다. tooresolve, 너무 hello 표시 설정**작게 – 100% (기본값)** 다음 hello 단계를 사용 하 여:  

1. 열기 hello **제어판** 클릭 **모양 및 개인 설정**합니다.
2. **디스플레이**를 클릭합니다.
3. **작게 – 100%(기본값)**를 클릭하고 **적용**을 클릭합니다.

hello **형식** 드롭다운 목록이 정상적으로 작동 합니다.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Hello BizTalk 서비스 포털에서에서 중복 규약
Hello를 시나리오를 따르는 것이 좋습니다.

1. Hello 거래 업체 관리 OM API를 사용 하 여 규약을 만듭니다.
2. 서로 다른 두 탭에 있는 hello BizTalk 서비스 포털에서에서 hello 규약을 엽니다.
3. 두 hello 탭에서 hello 규약을 배포 합니다.
4. 결과적으로, 두 hello 규약이 배포 된 hello BizTalk 서비스 포털에에서 중복 항목이 생성

**해결 방법**. Hello BizTalk 서비스 포털에서에서 hello 중복 규약 중 하나를 열고 배포를 취소 합니다.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>브리지는 hello 아티팩트 저장소에서 인증서를 업데이트 한 후에 업데이트 된 인증서를 사용 하지 않습니다.
Hello 다음 시나리오를 고려해 야 합니다.  

**시나리오 1: 지문을 기반 인증서를 사용 하 여 브리지 tooa 서비스 끝점에서 메시지 전송 보안**  
BizTalk 서비스 프로젝트에서 지문 기반 인증서를 사용하는 시나리오를 고려해 보세요. 다른 지문을 이름은 동일 하지만 hello BizTalk 서비스 프로젝트를 적절 하 게 업데이트 하지 않으면 hello로 hello BizTalk 서비스 포털에에서 hello 인증서를 업데이트 합니다. 이 시나리오에서는 hello 이전 인증서 데이터가 채널 캐시 hello에에서 계속 있을 수 있으므로 hello 브리지 tooprocess hello 메시지를 계속 될 수 있습니다. 그 후에는 메시지 처리에 실패합니다.  

**해결 방법**: hello BizTalk 서비스 프로젝트에에서 hello 인증서를 업데이트 하 고 hello 프로젝트를 다시 배포 합니다.  

**시나리오 2: 이름 기반 동작 tooidentify 인증서를 사용 하 여 브리지 tooa 서비스 끝점에서 메시지 전송 보안**

BizTalk 서비스 프로젝트에서 이름 기반 동작 tooidentify 인증서를 사용 하는 시나리오를 살펴보겠습니다. BizTalk 서비스 포털 hello에 hello 인증서를 업데이트 하지만 hello BizTalk 서비스 프로젝트를 그에 따라 업데이트 되지 않습니다. 이 시나리오에서는 hello 이전 인증서 데이터가 채널 캐시 hello에에서 계속 있을 수 있으므로 hello 브리지 tooprocess hello 메시지를 계속 될 수 있습니다. 그 후에는 메시지 처리에 실패합니다.  

**해결 방법**: hello BizTalk 서비스 프로젝트에에서 hello 인증서를 업데이트 하 고 hello 프로젝트를 다시 배포 합니다.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>브리지는 hello SQL 데이터베이스가 오프 라인 상태인 경우에 tooprocess 메시지를 계속
BizTalk 서비스 브리지 hello hello (저장 하는 배포 된 아티팩트와 파이프라인 등의 정보를 실행 하는 hello) Microsoft Azure SQL 데이터베이스를 오프 라인 상태인 경우에 한 동안 tooprocess 메시지를 계속 합니다. BizTalk 서비스에 캐시 hello 아티팩트 및 연결 구성을 사용 하 여 때문입니다.
하지 않을 경우 브리지 tooprocess hello 메시지 hello SQL 데이터베이스를 오프 라인 상태일 때, BizTalk 서비스 PowerShell cmdlet toostop hello를 사용 하 여 또는 hello BizTalk 서비스를 일시 중단할 수 있습니다. 참조 [Azure BizTalk 서비스 관리 샘플](http://go.microsoft.com/fwlink/p/?LinkID=329019) hello Windows PowerShell cmdlet toomanage 작업에 대 한 합니다.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>브리지의 사용자 지정 코드 구성 요소 내에서 읽기 hello XML 메시지에 추가 BOM 문자가 포함 됩니다.
브리지의 사용자 지정 코드 내에서 XML 메시지 tooread 원하는 시나리오를 고려 합니다. .NET API System.Text.Encoding.UTF8.GetString(bytes) hello를 사용 하는 경우 hello 메시지 hello 시작 시 hello 출력에 추가 BOM 문자가 포함 됩니다. 따라서 hello 출력 tooinclude hello 하지 않을 경우 사용 해야 추가 BOM 문자가 ```System.IO.StreamReader().ReadToEnd()```합니다.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>WCF를 사용 하 여 tooa 브리지에 메시지를 보내는 확장 되지 않습니다.
메시지 전송 WCF를 사용 하 여 tooa 브리지를 확장 하지 않습니다. 확장성 있는 클라이언트를 원하는 경우 대신 HttpWebRequest를 사용해야 합니다.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>BizTalk 서비스 미리 보기 tooGeneral 가용성 (GA)에서 업그레이드 한 후 토큰 공급자 오류 정보 업그레이드:
활성 배치가 있는 EDI 또는 AS2 규약이 있습니다. Hello BizTalk 서비스 미리 보기 tooGA에서 업그레이드 되 면 hello 다음 발생할 수 있습니다.

* 오류: hello 토큰 공급자가 없습니다 tooprovide 보안 토큰입니다. 토큰 공급자 반환 메시지: hello 원격 이름을 확인할 수 없습니다.
* 배치 작업이 취소됩니다.

**해결 방법**: hello BizTalk 서비스가 업데이트 된 tooGeneral 가용성 (GA) 되 면 hello 규약을 다시 배포 합니다.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>업그레이드: 도구 상자 표시 hello 이전 연결 아이콘이 hello BizTalk 서비스 SDK를 업그레이드 한 후
Hello hello 브리지를 나타내는 이전 아이콘이 포함 하는, BizTalk 서비스 SDK의 이전 버전을 업그레이드 한 후 hello 도구 상자 tooshow hello hello 연결에 대 한 이전 아이콘이 계속 됩니다. 그러나 브리지 tooBizTalk 서비스 프로젝트 designer 화면을 추가 하는 경우 hello 화면 hello 새로 만들기 아이콘을 표시 합니다.  

**해결 방법**. Hello.tbd 파일을 삭제 하 여이 문제를 해결할 수 있습니다 <system drive>: \Users\<사용자 > \AppData\Local\Microsoft\VisualStudio\11.0 합니다.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>업그레이드: tooGA 미리 보기에서에서 BizTalk 포털 업데이트에 사용할 수 없으면 해당 hello EDI 기능을 나타내는 오류가 표시 될 수 있습니다.
Hello BizTalk 서비스는 미리 보기 tooGA에서 업그레이드 하는 동안 hello BizTalk 서비스 포털에 로그인 되어, hello hello 포털에서 다음 오류가 발생할 수 있습니다.  

이 기능은 이 버전의 Microsoft Azure BizTalk 서비스의 일부로 사용할 수 없습니다. toouse 이러한 기능 tooan 적합 한 에디션을 전환 합니다.  

**해결 방법**: hello 포털, close 및 open hello 브라우저 및 hello 포털로 로그에서 로그 아웃 합니다.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>업그레이드: 새 추적 데이터가 표시 되지 않으면 BizTalk Services는 업그레이드 된 tooGA 후
BizTalk 서비스 미리 보기 구독에 배포된 XML 브리지가 있는 시나리오를 가정해 봅니다. Toohello 브리지가 메시지를 보낼 고 추적 데이터를 해당 하는 hello hello BizTalk 서비스 포털에서 사용할 수 있습니다. 이제, hello BizTalk 서비스 포털과 BizTalk 서비스의 런타임 비트는 업그레이드 된 tooGA 및 이전에 배포한 동일한 브리지 끝점 메시지 toohello 보낼, 추적 데이터는 hello 업그레이드 후 보낸 메시지에 대 한 표시 되지 않습니다.  

### <a name="pipelines-versus-bridges"></a>파이프라인과 브리지
이 설명서에서는 hello 용어 '파이프라인'과 '연결' 같은 의미로 사용 됩니다. 동일한 hello 둘 다 기본적으로 의미는 BizTalk 서비스에 배포 된 메시지 처리 단위입니다.  

### <a name="concepts"></a>개념
[BizTalk 서비스](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

