---
title: "도메인 간 Id 관리를 위한 시스템 aaaUsing 자동으로 프로 비전 tooapplications Azure Active Directory에서에서 사용자 및 그룹 | Microsoft Docs"
description: "Azure Active Directory 사용자 및 그룹 tooany 응용 프로그램 또는 id 저장소는 프런트 웹 서비스에 의해 hello SCIM 프로토콜 사양에에서 정의 된 hello 인터페이스와 자동으로 구축할 수 있습니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>도메인 간 Id 관리 tooautomatically 사용자 프로 비전 및 Azure Active Directory tooapplications에서 그룹에 대 한 시스템을 사용 하 여

## <a name="overview"></a>개요
Azure Active Directory (Azure AD)에 사용자와 그룹 tooany 응용 프로그램 또는 id 저장소는 프런트 웹 서비스에 의해 hello에 정의 된 hello 인터페이스와 자동으로 구축할 수 [시스템 도메인 간 Identity Management (SCIM) 2.0 프로토콜 사양](https://tools.ietf.org/html/draft-ietf-scim-api-19)합니다. Azure Active Directory toocreate 요청을 보낼 수 있습니다, 그리고 수정 또는 할당 된 사용자 및 그룹 toohello 웹 서비스를 삭제 합니다. 그런 다음 hello 웹 서비스 hello 대상 id 저장소에 대 한 작업으로 이러한 요청을 변환할 수 있습니다. 

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 



![][0]
*그림 1: 웹 서비스를 통해 Azure Active Directory tooan id 저장소에서 프로 비전*

Azure AD tooenable single sign on 및 자동 사용자 프로 비전을 제공 하거나 SCIM 웹 서비스에 의해 프런트 되는 응용 프로그램에 hello "앱을 직접 bring" 기능을 함께에서이 기능을 사용할 수 있습니다.

Azure Active Directory에서 SCIM을 사용하는 방법에 대한 두 가지 사용 사례가 있습니다.

* **지 원하는 SCIM tooapplications 사용자 및 그룹을 프로 비전** SCIM 2.0을 지원 하 고 구성 없이 Azure AD와 작동 하는 인증에 대 한 OAuth 전달자 토큰을 사용 하는 응용 프로그램입니다.
* **다른 API 기반 프로 비전을 지원 되는 응용 프로그램에 대 한 프로 비전 솔루션을 빌드합니다** SCIM 아닌 응용 프로그램에 대 한 모든 API hello 응용 프로그램에서는 hello Azure AD SCIM 끝점 사이의 SCIM 끝점 tootranslate를 만들 수 있습니다 사용자 프로 비전 합니다. toohelp SCIM 끝점을 개발, toodo SCIM 끝점을 제공 하 고 SCIM 메시지를 변환 하는 방법을 보여 주는 코드 예제와 함께 공용 언어 인프라 (CLI) 라이브러리를 제공 합니다.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>사용자 및 그룹 tooapplications SCIM 지 프로 비전
Azure AD 구성된 tooautomatically 프로 비전 할당 된 사용자 및 그룹 tooapplications 구현 하는 수는 [도메인 간 Id 관리 2 (SCIM)에 대 한 시스템](https://tools.ietf.org/html/draft-ietf-scim-api-19) 웹 서비스 및 인증에 대 한 OAuth 전달자 토큰을 수락 . Hello SCIM 2.0 사양 내에서 응용 프로그램에는 이러한 요구 사항을 충족 해야 합니다.

* 사용자 및/또는 hello SCIM 프로토콜 섹션 3.3에 따라 그룹 만들기를 지원 합니다.  
* 사용자 및/또는 패치 요청 hello SCIM 프로토콜의 3.5.2 섹션에 따라 그룹 수정을 지원 합니다.  
* 3.4.1 hello SCIM 프로토콜의 섹션에 따라 알려진된 리소스 검색을 지원 합니다.  
* 사용자 및/또는 그룹의 hello SCIM 프로토콜 3.4.2 섹션에 따라 쿼리를 지원 합니다.  기본적으로 사용자는 externalId에서 쿼리되고 그룹은 displayName에서 쿼리됩니다.  
* 3.4.2 hello SCIM 프로토콜의 섹션에 따라 관리자가 사용자 ID로 쿼리를 지원 합니다.  
* 그룹 및 섹션 3.4.2 hello SCIM 프로토콜에 따라 멤버 ID 별로 쿼리를 지원 합니다.  
* Hello SCIM 프로토콜의 섹션 2.1에 따라 권한 부여에 대 한 OAuth 전달자 토큰을 허용합니다.

응용 프로그램 공급자 또는 응용 프로그램 공급자의 설명서를 통해 이러한 요구 사항과의 호환성을 확인합니다.

### <a name="getting-started"></a>시작
이 문서에 설명 된 hello SCIM 프로필을 지 원하는 응용 프로그램에 연결 된 tooAzure Active Directory 수 hello Azure AD 응용 프로그램 갤러리에서 hello "갤러리 아닌 응용 프로그램" 기능을 사용 합니다. 연결 된, Azure AD에서 실행 되 면 동기화 프로세스에 대 한 hello 응용 프로그램의 SCIM 끝점을 쿼리하여 여기서 20 분 마다 사용자 및 그룹을 할당 하 고 만들거나 toohello 할당 세부 정보에 따라 수정 합니다.

**tooconnect SCIM를 지 원하는 응용 프로그램:**

1. 역시 로그인[Azure 포털 hello](https://portal.azure.com)합니다. 
2. 너무 찾아보기 * * Azure Active Directory > 엔터프라이즈 응용 프로그램 및 선택 **새 응용 프로그램 > 모든 > 비 갤러리 응용 프로그램**합니다.
3. 응용 프로그램에 대 한 이름을 입력 하 고 클릭 **추가** 아이콘 toocreate 응용 프로그램 개체입니다.
    
  ![][1]
  *그림 2: Azure AD 응용 프로그램 갤러리*
    
4. Hello 결과 화면에서 선택 hello **프로 비전** hello 왼쪽된 열에는 탭 합니다.
5. Hello에 **프로 비전 모드** 메뉴 선택 **자동**합니다.
    
  ![][2]
  *그림 3: hello Azure 포털에서에서 프로 비전 구성*
    
6. Hello에 **테 넌 트 URL** 필드 hello 응용 프로그램의 SCIM 끝점의 hello URL을 입력 합니다. 예: https://api.contoso.com/scim/v2/
7. Hello SCIM 끝점 Azure AD 이외의 발급자 로부터 OAuth 전달자 토큰에 필요한 경우 복사 hello 선택적 hello에 OAuth 전달자 토큰을 필요한 **암호 토큰** 필드입니다. 이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다. ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.
8. Hello 클릭 **연결 테스트** 단추 toohave Azure Active Directory 시도 tooconnect toohello SCIM 끝점입니다. Hello 시도가 실패 한 경우 오류 정보가 표시 됩니다.  
9. Hello 시도 tooconnect toohello 응용 프로그램 성공 하는 경우 클릭 **저장** toosave hello에 대 한 관리자 자격 증명입니다.
10. Hello에 **매핑** 섹션에서 두 개의 선택할 수 있는 특성 매핑 집합이: 사용자 개체 및 그룹 개체에 대 한 하나 있습니다. Azure Active Directory tooyour 응용 프로그램에서 동기화 되는 각 하나의 tooreview hello 특성을 선택 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 응용 프로그램에서 사용 되는 toomatch hello 사용자 및 그룹입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

    >[!NOTE]
    >필요에 따라 hello "groups" 매핑을 해제 하 여 그룹 개체의 동기화를 비활성화할 수 있습니다. 

11. 아래 **설정**, hello **범위** 사용자 및 그룹 동기화 되는 또는 필드를 정의 합니다. Hello에 할당 사용자 및 그룹에만 동기화 합니다 "동기화만 할당 된 사용자 및 그룹" (권장)을 선택 하면 **사용자 및 그룹** 탭 합니다.
12. 구성을 완료 되 면 변경 hello **프로 비전 상태** 너무**에**합니다.
13. 클릭 **저장** toostart hello Azure AD에 프로 비전 서비스입니다. 
14. 사용자 및 그룹 (권장) 할당만 동기화 하는 경우 수 있는지 tooselect hello **사용자 및 그룹** 탭 하 고 hello 사용자 및/또는 toosync 원하는 그룹을 할당 합니다.

Hello 초기 동기화가 시작 되 면 hello를 사용할 수 있습니다 **감사 로그** 응용 프로그램에서 서비스를 프로 비전 하는 hello 수행한 모든 작업을 보여 주는 toomonitor 진행 상황을 탭 합니다. Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.

>[!NOTE]
>hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>응용 프로그램에 대한 고유한 프로비전 솔루션 구축
Azure Active Directory와 상호 작용하는 SCIM 웹 서비스를 만들어서 REST 또는 SOAP 사용자 프로비전 API를 제공하는 거의 모든 응용 프로그램에 대한 Single Sign-On 및 자동 사용자 프로비전을 사용하도록 설정할 수 있습니다.

방법은 다음과 같습니다.

1. Azure AD는 [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/)로 명명된 공용 언어 인프라 라이브러리를 제공합니다. 시스템 통합 업체 및 개발자가이 라이브러리 toocreate를 사용할 수 있으며 Azure AD tooany 응용 프로그램의 id 저장소에 연결할 수 SCIM 기반 웹 서비스 끝점을 배포 됩니다.
2. 매핑은 hello 웹 서비스 toomap hello 표준화 된 사용자 스키마 toohello 사용자 스키마와 hello 응용 프로그램에 필요한 프로토콜에서 구현 됩니다.
3. hello 끝점 URL은 hello 응용 프로그램 갤러리에서 사용자 지정 응용 프로그램의 일부분으로 Azure AD에 등록 됩니다.
4. 사용자 및 그룹에는 Azure AD에서 응용 프로그램 toothis 할당 됩니다. 할당, 시 큐 동기화 toobe toohello 대상 응용 프로그램에 저장 됩니다. hello 큐를 처리 하는 hello 동기화 프로세스에는 20 분 마다 실행 됩니다.

### <a name="code-samples"></a>코드 샘플
toomake이 프로세스는 더 쉽게 집합이 [코드 샘플](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) 제공 하는 SCIM 웹 서비스 끝점을 만드는 / 자동 프로 비전을 보여 줍니다. 한 가지 샘플은 사용자 및 그룹을 나타내는 쉼표로 구분된 값의 행이 있는 파일을 유지 관리하는 공급자입니다.  다른 hello hello Amazon 웹 서비스 Id 및 액세스 관리 서비스에 작동 하는 공급자입니다.  

**필수 구성 요소**

* Visual Studio 2013 이상
* [Azure SDK for .NET](https://azure.microsoft.com/downloads/)
* Windows 컴퓨터를 지 원하는 hello ASP.NET 4.5 toobe SCIM 끝점 hello로 사용 합니다. 이 컴퓨터는 hello 클라우드에서 액세스할 수 있어야 합니다.
* [Azure AD Premium의 평가판 또는 사용이 허가된 버전의 Azure 구독](https://azure.microsoft.com/services/active-directory/)
* hello AWS Amazon 샘플을 사용 하려면 hello에서 라이브러리 [Visual Studio 용 도구 키트에 AWS](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html)합니다. 자세한 내용은 hello 추가 정보를 참조 하십시오. hello 샘플에 포함 된 파일입니다.

### <a name="getting-started"></a>시작하기
Azure AD에서 프로 비전을 허용할 수 있는 SCIM 끝점 요청 hello 가장 쉬운 방법은 tooimplement toobuild 이며 hello 프로 비전 된 사용자 tooa 쉼표로 구분 된 값 (CSV) 파일을 출력 하는 hello 코드 샘플을 배포 합니다.

**toocreate 샘플 SCIM 끝점:**

1. hello 코드 예제 패키지를 다운로드 [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Hello 패키지의 압축을 푸는 C:\AzureAD-BYOA-Provisioning-Samples\와 같은 위치에서 Windows 컴퓨터에 배치 합니다.
3. 이 폴더에 Visual Studio에서 hello FileProvisioningAgent 솔루션을 시작 합니다.
4. 선택 **도구 > 라이브러리 패키지 관리자 > 패키지 관리자 콘솔**, hello 다음 hello FileProvisioningAgent 프로젝트 tooresolve hello 솔루션 참조에 대 한 명령을 실행 합니다.
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Hello FileProvisioningAgent 프로젝트를 빌드하십시오.
6. Hello 명령 프롬프트에서에서 응용 프로그램 Windows (Administrator)로 시작 하 고 hello를 사용 하 여 **cd** 명령 toochange hello 디렉터리 tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** 폴더입니다.
7. Hello < ip 주소 > hello Windows 컴퓨터의 hello IP 주소 또는 도메인 이름으로 바뀔, 다음 명령을 실행 합니다.
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. 창의에 **Windows 설정 > 네트워크 및 인터넷 설정을**선택, hello **Windows 방화벽 > 고급 설정**, 만들고는 **인바운드 규칙** 입니다 인바운드 액세스 tooport 9000을 허용합니다.
9. Hello Windows 컴퓨터가 라우터 뒤에 있는 경우 라우터 요구 구성 toobe tooperform 네트워크 액세스 변환 해당 포트 9000 간의 노출된 toohello 있는 hello 인터넷 및 포트 9000 hello Windows 컴퓨터에 있습니다. 이 Azure AD toobe 수 tooaccess 필요 hello 클라우드에서이 끝점입니다.

**hello 샘플 SCIM 끝점 Azure AD에서 tooregister 하 고:**

1. 역시 로그인[Azure 포털 hello](https://portal.azure.com)합니다. 
2. 너무 찾아보기 * * Azure Active Directory > 엔터프라이즈 응용 프로그램 및 선택 **새 응용 프로그램 > 모든 > 비 갤러리 응용 프로그램**합니다.
3. 응용 프로그램에 대 한 이름을 입력 하 고 클릭 **추가** 아이콘 toocreate 응용 프로그램 개체입니다. hello application 개체 생성은 의도 한 toorepresent hello 대상 앱 single sign-on, 및 뿐 아니라 hello SCIM 끝점 구현 tooand 프로비저닝 것입니다.
4. Hello 결과 화면에서 선택 hello **프로 비전** hello 왼쪽된 열에는 탭 합니다.
5. Hello에 **프로 비전 모드** 메뉴 선택 **자동**합니다.
    
  ![][2]
  *그림 4: hello Azure 포털에서에서 프로 비전 구성*
    
6. Hello에 **테 넌 트 URL** 필드 hello 인터넷에 노출 된 URL과 SCIM 끝점의 포트를 입력 합니다. 것 것 처럼 http://testmachine.contoso.com:9000 나 < ip 주소 > 인터넷을 hello는 http://<ip-address>:9000/ 노출 IP 주소입니다.  
7. Hello SCIM 끝점 Azure AD 이외의 발급자 로부터 OAuth 전달자 토큰에 필요한 경우 복사 hello 선택적 hello에 OAuth 전달자 토큰을 필요한 **암호 토큰** 필드입니다. 이 필드를 비워 두면 Azure AD에 각 요청에 따라 Azure AD에서 발급한 OAuth 전달자 토큰이 포함됩니다. ID 공급자로 Azure AD를 사용하는 앱은 Azure AD에서 발급한 토큰의 유효성을 검사할 수 있습니다.
8. Hello 클릭 **연결 테스트** 단추 toohave Azure Active Directory 시도 tooconnect toohello SCIM 끝점입니다. Hello 시도가 실패 한 경우 오류 정보가 표시 됩니다.  
9. Hello 시도 tooconnect toohello 응용 프로그램 성공 하는 경우 클릭 **저장** toosave hello에 대 한 관리자 자격 증명입니다.
10. Hello에 **매핑** 섹션에서 두 개의 선택할 수 있는 특성 매핑 집합이: 사용자 개체 및 그룹 개체에 대 한 하나 있습니다. Azure Active Directory tooyour 응용 프로그램에서 동기화 되는 각 하나의 tooreview hello 특성을 선택 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 응용 프로그램에서 사용 되는 toomatch hello 사용자 및 그룹입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.
11. 아래 **설정**, hello **범위** 사용자 및 그룹 동기화 되는 또는 필드를 정의 합니다. Hello에 할당 사용자 및 그룹에만 동기화 합니다 "동기화만 할당 된 사용자 및 그룹" (권장)을 선택 하면 **사용자 및 그룹** 탭 합니다.
12. 구성을 완료 되 면 변경 hello **프로 비전 상태** 너무**에**합니다.
13. 클릭 **저장** toostart hello Azure AD에 프로 비전 서비스입니다. 
14. 사용자 및 그룹 (권장) 할당만 동기화 하는 경우 수 있는지 tooselect hello **사용자 및 그룹** 탭 하 고 hello 사용자 및/또는 toosync 원하는 그룹을 할당 합니다.

Hello 초기 동기화가 시작 되 면 hello를 사용할 수 있습니다 **감사 로그** 응용 프로그램에서 서비스를 프로 비전 하는 hello 수행한 모든 작업을 보여 주는 toomonitor 진행 상황을 탭 합니다. Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.

hello 최종 단계는 hello 샘플을 확인 하는 tooopen hello hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug 폴더에 Windows 컴퓨터 TargetFile.csv 파일입니다. Hello를 프로 비전 프로세스를 실행 한 후이 파일에 할당 하 고 사용자 및 그룹을 프로 비전 하는 모든 hello 세부적인 표시 합니다.

### <a name="development-libraries"></a>개발 라이브러리
toodevelop toohello SCIM 사양을 준수 하는 웹 서비스 먼저 숙지 hello toohelp microsoft hello 개발 프로세스를 가속화할 제공 라이브러리를 따라. 

1. CLI(공용 언어 인프라) 라이브러리는 C#과 같은 해당 인프라에 따라 언어와 함께 사용하기 위해 제공됩니다. 이러한 라이브러리 중 하나 [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), 인터페이스 선언, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, hello 다음 그림에에서 표시 된: A hello 라이브러리를 사용 하는 개발자, 일반적으로 공급자 참조 될 수 있는 클래스와 해당 인터페이스를 구현 합니다. hello 라이브러리 hello 개발자 toodeploy toohello SCIM 사양을 준수 하는 웹 서비스를 사용 합니다. hello 웹 서비스는 인터넷 정보 서비스 또는 실행 가능한 모든 공용 언어 인프라 어셈블리 내에서 하거나 호스트할 수 있습니다. 요청에 일부 id 저장소 hello 개발자 toooperate 하 여 프로그래밍할 수는 호출 toohello 공급자 메서드로 변환 됩니다.
  
  ![][3]
  
2. [Express 경로 처리기](http://expressjs.com/guide/routing.html) 호출 (에 정의 된 대로 hello SCIM 사양), tooa node.js 웹 서비스를 나타내는 node.js 요청 개체를 구문 분석에 사용할 수 있습니다.   

### <a name="building-a-custom-scim-endpoint"></a>사용자 지정 SCIM 끝점 빌드
Hello CLI 라이브러리를 사용 하 여 해당 라이브러리를 사용 하는 개발자는 모든 실행 가능한 공용 언어 인프라 어셈블리 내에서 또는 인터넷 정보 서비스 내 서비스를 호스팅할 수 있습니다. Hello 주소 http://localhost:9000에서 있는 실행 가능한 어셈블리 내에서 서비스를 호스트에 대 한 샘플 코드는 다음과 같습니다. 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

이 서비스는 hello의 루트 인증 기관 hello 다음 중 하나는 HTTP 주소 및 서버 인증 인증서가 있어야 합니다. 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* Verisign
* WoSign

서버 인증 인증서에 바인딩된 tooa 호스트의 포트에는 Windows hello 네트워크 셸 유틸리티를 사용 하 여 될 수 있습니다. 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

여기서 hello hello certhash 인수에 제공 된 기간은 hello 인증서의 지문 안녕하세요 hello 값 hello appid 인수에 제공 되는 임의의 전역 고유 식별자입니다.  

인터넷 정보 서비스 내에서 toohost hello 서비스를 개발자 시작 hello 어셈블리의 hello 기본 네임 스페이스에 이름이 지정 된 클래스와 함께 CLA 코드 라이브러리 어셈블리를 빌드하는 것입니다.  이러한 클래스의 샘플은 다음과 같습니다. 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>끝점 인증 처리
Azure Active Directory에서 요청은 OAuth 2.0 전달자 토큰을 포함합니다.   모든 서비스 수신 hello 요청 hello 발급자 액세스 toohello Azure Active Directory Graph 웹 서비스에 대 한 예상 hello Azure Active Directory 테 넌을 대신 하 여 Azure Active Directory 것으로 인증 해야 합니다.  Hello 토큰에서 발급자 hello "iss"와 같은 경우 iss 클레임으로 식별 됩니다: "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/"입니다.  이 예제에서는 hello 클레임 값의 기본 주소 hello https://sts.windows.net, 발급자 hello 대로 Azure Active Directory를 식별, 동안 hello cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, 상대 주소 세그먼트의 고유 식별자 hello Azure Active 토큰이 발급 된 어떤 hello를 대신 하 여 디렉터리 테 넌 트.  Hello Azure Active Directory Graph 웹 서비스, 해당 서비스의 다음 hello 식별자에 액세스 하기 위한 hello 토큰이 발급 된 경우 00000002-0000-0000-c000-000000000000, 될 hello 토큰의 aud hello 값에서 무시 해야 합니다.  

SCIM 서비스를 빌드하기 위한 Microsoft에서 제공 하는 hello CLA 라이브러리를 사용 하는 개발자 Microsoft.Owin.Security.ActiveDirectory 패키지용 hello를 사용 하 여 다음이 단계를 수행 하 여 Azure Active Directory의 요청을 인증할 수 있습니다. 

1. 공급자에서 hello 서비스가 시작 될 때마다 호출 메서드 toobe를 반환 하 여 hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior 속성을 구현 합니다. 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. 다음 코드 toothat 메서드 toohave hello bearing 액세스 toohello Azure AD 그래프 웹 서비스에 대 한 지정 된 테 넌을 대신 하 여 Azure Active Directory에서 발급 한 토큰으로 인증 하는 hello 서비스 끝점의 모든 요청 tooany를 추가 합니다. 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>사용자 및 그룹 스키마
Azure Active Directory는 두 가지 유형의 리소스 tooSCIM 웹 서비스를 구성할 수 있습니다.  이러한 형식의 리소스는 사용자 및 그룹입니다.  

사용자 리소스는이 프로토콜 사양에 포함 된 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User hello 스키마 식별자로 식별 됩니다: http://tools.ietf.org/html/draft-ietf-scim-core-schema 합니다.  아래 표에 1, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스의 Azure Active Directory toohello 특성에 있는 사용자의 hello 특성의 hello 기본 매핑을 제공 됩니다.  

리소스 그룹 hello 스키마 식별자로 식별 됩니다 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 합니다.  테이블 2, 아래 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group 리소스의 Azure Active Directory toohello 특성에 있는 그룹의 hello 특성의 hello 기본 매핑 보여 줍니다.  

### <a name="table-1-default-user-attribute-mapping"></a>테이블 1: 기본 사용자 특성 매핑
| Azure Active Directory 사용자 | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |활성 |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |title |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>테이블 2: 기본 그룹 특성 매핑
| Azure Active Directory 그룹 | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |displayName |
| members |members |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>사용자 프로비저닝 및 프로비전 해제
다음 그림에서는 hello 메시지를 Azure Active Directory 다른 id 저장소에 사용자의 tooa SCIM 서비스 toomanage hello 주기를 전송 하는 번호입니다. hello 다이어그램에는 어떻게는 SCIM hello CLI 라이브러리를 사용 하 여 구현 Microsoft에서 제공한 서비스 만들기에 대 한 공급자의 toohello 메서드를 호출에 해당 요청을 변환 하는 같은 서비스를 보여 줍니다.  

![][4]
*그림 5: 사용자 프로비저닝 및 시퀀스 프로비전 해제*

1. Azure Active Directory 쿼리 externalId 특성 값이 사용자의 hello mailNickname 특성 값을 일치 하는 Azure AD에서 사용자에 대 한 서비스를 hello 합니다. hello 쿼리 jyoung은 Azure Active Directory에서 사용자의 mailNickname의 샘플에는이 예제에서는 같은 하이퍼텍스트 전송 프로토콜 (HTTP) 요청으로 표현 됩니다. 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 쿼리 방법으로 변환 됩니다.  해당 메서드의 hello 서명을 다음과 같습니다. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters 인터페이스의 hello 정의 다음과 같습니다. 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  다음 샘플 hello externalId 특성에 대 한 지정된 된 값으로 사용자에 대 한 쿼리의 hello, toohello 쿼리 메서드에 전달 하는 hello 인수 값은: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Hello 응답 tooa 쿼리 toohello 웹 서비스 사용자는 사용자의 hello mailNickname 특성 값과 일치 하는 externalId 특성 값에 대 한 모든 사용자가 반환 하지 않는 경우 그런 다음 Azure Active Directory 요청 사용자 해당 hello 서비스 제공 해당 toohello 하나 Azure Active Directory에 있습니다.  다음은 그러한 요청의 예제입니다. 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리는 호출 toohello hello 서비스 공급자의 Create 메서드를 해당 요청을 변환 합니다.  Create 메서드 hello이이 서명을 있습니다. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  요청 tooprovision 사용자에서에서 hello 리소스에 대 한 인수의 값이 hello는 hello Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스입니다. Hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas 라이브러리에 정의 된 Core2EnterpriseUser 클래스입니다.  Hello 요청 tooprovision hello 사용자에 성공 하면 다음 hello hello 메서드는 예상된 tooreturn hello Microsoft.SystemForCrossDomainIdentityManagement의 인스턴스. Hello 식별자 속성의 값이 hello Core2EnterpriseUser 클래스 toohello hello 새로 프로 비전 된 사용자의 고유 식별자를 설정합니다.  

3. tooupdate tooexist id 저장소에 알려진 사용자는 SCIM hello 서비스에서와 같은 요청 hello 해당 사용자의 현재 상태를 요청 하 여 Azure Active Directory 계속 진행 하 여 프런트: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 하는 서비스에 hello 요청 호출 toohello hello 서비스 공급자의 검색 방법으로 변환 됩니다.  Hello 서명의 hello 검색 메서드는 다음과 같습니다. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  사용자의 요청 tooretrieve hello 현재 상태 hello 예에서 hello hello 매개 변수 인수 값으로 제공 하는 hello 개체의 hello 속성 hello 값은 다음과 같습니다. 
  
  * 식별자: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. 참조 특성 toobe 업데이트 후 Azure Active Directory 쿼리 hello 서비스 toodetermine 여부 hello hello id 저장소의 hello 참조 특성의 현재 값 프런트 하 여 hello 서비스 이미 검색 hello 특성 값 Azure Active directory 의미 합니다. 사용자에 대 한 hello만는 hello의 현재 값이 방식으로 쿼리 됩니다 hello 관리자 특성이입니다. 특정 사용자 개체의 hello 관리자 특성에는 현재 특정 값이 있는지 여부를 요청 toodetermine의 예는 다음과 같습니다. 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  값 hello hello 특성 쿼리 매개 변수의 id hello hello 필터 쿼리 매개 변수 값으로 제공 하는 hello 식을 만족 하는 사용자 개체가 있는 경우 다음 hello 서비스는 urn: ietf:params:scim:schemas와 예상된 toorespond을 나타냅니다. 코어: 2.0:User 또는 urn: ietf:params:scim:schemas:extension:enterprise:2.0:User 리소스, 해당 리소스의 id 특성의 hello 값만 포함 합니다.  값의 hello hello **id** 특성 toohello 요청자 알려져 있습니다. 쿼리 매개 변수를 필터 하는 hello; hello 값에 포함 되어 hello에 대 한 질문의 목적은 toorequest 존재 여부 등 모든 개체를 확인 하는 hello 필터 식을 만족 하는 리소스에 대 한 최소 표현을 실제로입니다.   

  Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 쿼리 방법으로 변환 됩니다. hello 매개 변수 인수 hello 값으로 제공 하는 hello 개체의 hello 속성 hello 값은 다음과 같습니다. 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  여기에서 hello 인덱스 x의 hello 값 0 일 수 있습니다 및 hello hello 인덱스 y 값 수 1, 또는 x의 hello 값은 1 일 수 있으며 y의 hello 값 hello 필터에 대 한 쿼리 매개 변수는 hello 식의 hello 순서에 따라 0이 될 수 있습니다.   

5. Azure Active Directory tooan SCIM 서비스 tooupdate 사용자를에서 요청의 예는 다음과 같습니다. 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  SCIM 서비스를 구현 하기 위한 hello Microsoft 공용 언어 인프라 라이브러리는 hello 요청 호출 toohello hello 서비스 공급자의 Update 메서드를 변환 합니다. Hello 서명의 hello 큐브의 Update 메서드에 다음과 같습니다. 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    요청 tooupdate 사용자 hello 예제를 hello hello 패치 인수 값으로 제공 하는 hello 개체에는 이러한 속성 값에 있습니다. 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. SCIM service에 의해 프로 비전 toode id 저장소에서 사용자 프런트, Azure AD와 같은 요청을 보냅니다. 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Hello 서비스가 SCIM 서비스 구현에 대 한 Microsoft에서 제공 하는 hello 공용 언어 인프라 라이브러리를 사용 하 여 작성 된 경우에 hello 요청 호출 toohello hello 서비스 공급자의 Delete 메서드로 변환 됩니다.   해당 메서드에는 다음 서명이 있습니다. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  hello hello resourceIdentifier 인수 값으로 제공 하는 hello 개체의 사용자 요청 toode-프로 비전이의 hello 예에 이러한 속성 값: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>그룹 프로비전 및 프로비전 해제
hello 다음 그림에서는 hello 메시지 Azure AcD에 다른 id 저장소 그룹의 tooa SCIM 서비스 toomanage hello 주기를 보냅니다.  이러한 메시지 toousers 세 가지 방법으로 관련 된 hello 메시지에서 다릅니다. 

* 그룹 리소스의 hello 스키마 http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group으로 식별 됩니다.  
* Tooretrieve 그룹 해당 hello 멤버 특성을 규정 하는 요청은 toobe 응답 toohello 요청에 제공 된 모든 리소스에서 제외 합니다.  
* 요청 toodetermine hello 멤버 특성에 대 한 요청이 포함 됩니다는 참조 특성의 값을 특정 값에 있는지 여부.  

![][5]
*그림 6: 그룹 프로비전 및 시퀀스 프로비전 해제*

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [사용자 프로 비전/프로 비전 해제 tooSaaS 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [사용자 프로비저닝에 대한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)
* [특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [사용자 프로 비전에 대 한 필터 범위 지정](active-directory-saas-scoping-filters.md)
* [계정 프로비전 알림](active-directory-saas-account-provisioning-notifications.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
