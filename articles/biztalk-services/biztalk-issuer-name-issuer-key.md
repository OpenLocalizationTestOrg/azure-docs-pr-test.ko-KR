---
title: "aaaIssuer 이름 및 발급자 키에서 BizTalk 서비스 | Microsoft Docs"
description: "자세한 내용은 tooretrieve 발급자 이름을 지정 하는 방법 및 ACS (액세스 제어)에 BizTalk 서비스 또는 서비스 버스에 대 한 발급자 키입니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk 서비스: 발급자 이름 및 발급자 키

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 서비스는 hello 서비스 버스 발급자 이름 및 발급자 키 hello 액세스 제어 발급자 이름 및 발급자 키를 사용합니다. 구체적으로 살펴보면 다음과 같습니다.

| 작업 | 발급자 이름 및 발급자 키 |
| --- | --- |
| Visual Studio에서 응용 프로그램 배포 |액세스 제어 발급자 이름 및 발급자 키 |
| Hello Azure BizTalk 서비스 포털 구성 |액세스 제어 발급자 이름 및 발급자 키 |
| Visual Studio에서 BizTalk 어댑터 서비스 hello를 사용 하 여 LOB 릴레이 만들기 |서비스 버스 발급자 이름 및 발급자 키 |

이 항목에서는 hello 단계 tooretrieve hello 발급자 이름 및 발급자 키를 나열 합니다. 

## <a name="access-control-issuer-name-and-issuer-key"></a>액세스 제어 발급자 이름 및 발급자 키
hello 다음 hello 액세스 제어 발급자 이름 및 발급자 키가 사용 됩니다.

* Azure BizTalk 서비스 응용 프로그램에서 Visual Studio에서 만든: toosuccessfully tooAzure Visual Studio에서에서 BizTalk 서비스 응용 프로그램을 배포, hello 액세스 제어 발급자 이름 및 발급자 키를 입력 합니다. 
* Azure BizTalk 서비스 포털 hello: BizTalk 서비스를 만들고 엽니다 hello BizTalk 서비스 포털에 대 한 액세스 제어 발급자 이름 및 발급자 키와 배포에 대해 자동으로 등록 됩니다 때 hello 같은 액세스 제어 값입니다.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>가져오기 hello 액세스 제어 발급자 이름과 발급자 키

인증 및 get toouse ACS 발급자 이름과 발급자 키 값을 hello, hello 전체 단계 포함:

1. Hello 설치 [Azure Powershell cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)합니다.
2. Azure 계정을 추가합니다. `Add-AzureAccount`
3. 구독 이름을 반환합니다. `get-azuresubscription`
4. 사용 중인 구독을 선택합니다. `select-azuresubscription <name of your subscription>` 
5. 새 네임스페이스를 만듭니다. `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    예:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Hello 새 ACS 네임 스페이스를 만들면 (있음 몇 분 정도 걸릴 수 있습니다) hello 발급자 이름과 발급자 키 값 hello 연결 문자열에 나열 됩니다. 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
발급자 이름 = SharedSecretIssuer  
발급자 키 = SharedSecretKey

Hello에 더 [New-azuresbnamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>서비스 버스 발급자 이름 및 발급자 키
서비스 버스 발급자 이름 및 발급자 키는 BizTalk 어댑터 서비스에 사용됩니다. Visual Studio에서 BizTalk 서비스 프로젝트에서 hello BizTalk 어댑터 서비스 tooconnect tooan 온-프레미스의 업무 (LOB) 시스템을 사용합니다. tooconnect, hello LOB 릴레이 만들고 LOB 시스템 정보를 입력 합니다. 이 작업을 수행 하는 경우 hello 서비스 버스 발급자 이름 및 발급자 키 입력할 수도 있습니다.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>tooretrieve hello 서비스 버스 발급자 이름 및 발급자 키
1. Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.
2. Hello 왼쪽된 탐색 창에서 선택 **서비스 버스**합니다.
3. 네임스페이스를 선택합니다. Hello 작업 표시줄에서 선택 **연결 정보**합니다. Hello 표시 **기본 발급자** (발급자 이름) 및 **기본 키** (발급자 키)입니다. 이 값은 복사할 수 있습니다.  

toosummarize:  
발급자 이름 = 기본 발급자  
발급자 키 = 기본 키

## <a name="next"></a>다음
추가 Azure BizTalk 서비스 항목:

* [Hello Azure BizTalk Services SDK 설치](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [자습서: Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>참고 항목
* [방법: ACS 관리 서비스를 사용 하 여 tooConfigure 서비스 Id](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk 서비스: 프로비저닝 상태 차트](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk 서비스: 백업 및 복원](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk 서비스: 제한](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

