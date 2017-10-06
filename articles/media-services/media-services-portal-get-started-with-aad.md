---
title: "hello Azure 포털을 사용 하 여 Azure AD 인증 시작 aaaGet | Microsoft Docs"
description: "Azure 포털 tooaccess Azure Active Directory (Azure AD) 인증 tooconsume toouse hello Azure 미디어 서비스 API hello 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Azure AD 인증 시작

어떻게 toouse hello Azure 포털 tooaccess Azure Active Directory (Azure AD) 인증 tooaccess hello Azure 미디어 서비스 API에 알아봅니다.

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작하세요. 
- Media Services 계정. 자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정을 만들려면](media-services-portal-create-account.md)합니다.
- Hello를 검토 해야 [Azure AD 인증 개요를 사용 하 여 Azure 미디어 서비스 API에 액세스](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

Azure Media Services와 함께 Azure AD 인증을 사용할 때 두 가지 인증 옵션이 제공됩니다.

- **사용자 인증**. 미디어 서비스 리소스와 앱 toointeract hello를 사용 하는 사람을 인증 합니다. 먼저 hello 대화형 응용 프로그램에는 hello 사용자에 게 자격 라는 메시지 해야 합니다. 권한 있는 사용자 toomonitor 인코딩 작업에서 사용 하 여 관리 콘솔 응용 프로그램은 라이브 스트리밍 또는 예입니다. 
- **서비스 주체 인증**. 서비스를 인증합니다. 이 인증 방법을 일반적으로 사용하는 응용 프로그램은 디먼 서비스, 중간 계층 서비스 또는 예약된 작업(예: 웹앱, 함수 앱, 논리 앱, API 또는 마이크로 서비스)을 실행하는 앱입니다.

> [!IMPORTANT]
> 현재 미디어 서비스는 hello Azure 액세스 제어 서비스 인증 모델을 지원 합니다. 그러나 Access Control 권한 부여는 2018년 6월 1일부로 더 이상 사용되지 않을 예정입니다. Toohello Azure AD 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.

## <a name="select-hello-authentication-method"></a>Hello 인증 방법 선택

1. Hello에 [Azure 포털](https://portal.azure.com/), 미디어 서비스 계정을 선택 합니다.
2. 방법을 선택 tooconnect toohello 미디어 서비스 API입니다.

    ![연결 방법 선택 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>사용자 인증

tooconnect toohello 미디어 서비스 API를 사용 하 여 hello 사용자 인증 옵션, 클라이언트 응용 프로그램 hello 필요한 toorequest 매개 변수 뒤 hello에 Azure AD 토큰:  

* Azure AD 테넌트 끝점
* Media Services 리소스 URI
* Media Services(원시) 응용 프로그램 클라이언트 ID 
* Media Services(원시) 응용 프로그램 리디렉션 URI 
* REST Media Services의 리소스 URI

Hello에 이러한 매개 변수에 대해 hello 값을 가져올 수 **사용자 인증을 사용 하 여 미디어 서비스 API** 페이지. 

![사용자 인증으로 연결 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

미디어 서비스 API toohello hello 미디어 서비스 Microsoft.NET SDK를 사용 하 여 연결 하는 경우 hello 값 hello SDK의 일부분으로 사용할 수 있는 tooyou이 필요 합니다. 자세한 내용은 참조 [사용 하 여 Azure AD 인증 tooaccess hello.NET을 사용 하 여 Azure 미디어 서비스 API](media-services-dotnet-get-started-with-aad.md)합니다.

Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우 앞에서 설명한 hello 매개 변수를 사용 하 여 Azure AD 토큰 요청을 수동으로 만들 해야 있습니다. 자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.

## <a name="service-principal-authentication"></a>서비스 주체 인증

tooconnect toohello 미디어 서비스 API를 사용 하 여 서비스 보안 주체 옵션 hello, 중간 계층 응용 프로그램 (웹 API 또는 웹 응용 프로그램) 필요한 toorequest 매개 변수 뒤 hello에 Azure AD 토큰:  

* Azure AD 테넌트 끝점
* Media Services 리소스 URI 
* REST Media Services의 리소스 URI
* Azure AD 응용 프로그램 값: hello **클라이언트 ID** 및 **클라이언트 암호**

Hello에 이러한 매개 변수에 대해 hello 값을 가져올 수 **tooMedia 서비스 API 서비스 사용자와 연결** 페이지. 이 페이지 toocreate 새로운 Azure를 사용 하 여 AD 응용 프로그램 또는 tooselect 기존 합니다. Hello Azure AD 앱을 선택한 후 hello 클라이언트 ID (응용 프로그램 ID) 가져오고 hello 클라이언트 암호 (키) 값을 생성할 수 있습니다. 

![서비스 주체로 연결 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Hello 때 **서비스 사용자** hello 첫 번째 Azure AD 응용 프로그램이 hello 다음 조건을 충족 하는 선택, 블레이드를 엽니다.

- 등록된 Azure AD 응용 프로그램입니다.
- Hello 계정에 참가자 또는 Owner Role-Based 액세스 제어 권한을 보유 합니다.

후에 만들거나 Azure AD 앱 선택 만들고 수 있습니다 및 클라이언트 암호 (키)를 복사할 hello 클라이언트 ID (응용 프로그램 ID)입니다. hello 클라이언트 암호 및 클라이언트 ID는이 시나리오에서는 필요한 tooget hello 액세스 토큰입니다.

사용 권한을 toocreate Azure AD 앱 도메인 내에서 없다면 hello 블레이드의 hello Azure AD 앱 컨트롤 표시 되지 않습니다 하 고 경고 메시지가 표시 됩니다.

미디어 서비스 API toohello hello 미디어 서비스.NET SDK를 사용 하 여 연결 하는 경우 참조 [사용 하 여 Azure AD 인증 tooaccess hello.NET을 사용 하 여 Azure 미디어 서비스 API](media-services-dotnet-get-started-with-aad.md)합니다.

Hello 미디어 서비스.NET SDK 클라이언트를 사용 하지 않는 경우 수동으로 앞에서 설명한 hello 매개 변수를 사용 하 여 Azure AD 토큰 요청을 만들어야 합니다. 자세한 내용은 참조 [어떻게 toouse hello Azure AD 인증 라이브러리 tooget hello Azure AD 토큰](../active-directory/develop/active-directory-authentication-libraries.md)합니다.

### <a name="get-hello-client-id-and-client-secret"></a>Hello 클라이언트 ID 및 클라이언트 암호 가져오기

기존 Azure AD 응용 프로그램 또는 선택 하면 선택 hello 옵션 toocreate 새 hello 다음 단추가 표시 됩니다.

![[사용 권한 관리] 단추 및 [응용 프로그램 관리] 단추](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

Azure AD 응용 프로그램 블레이드 tooopen hello 클릭 **응용 프로그램 관리**합니다. Hello에 **응용 프로그램 관리** 블레이드에서 hello 앱의 클라이언트 ID (응용 프로그램 ID)를 가져올 수 있습니다. 선택 하면 클라이언트 암호 (키), toogenerate **키**합니다.

![응용 프로그램 블레이드 키 관리 옵션](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>사용 권한 및 hello 응용 프로그램 관리

Hello Azure AD 응용 프로그램을 선택한 후에 hello 응용 프로그램 및 권한을 관리할 수 있습니다. tooset 다른 응용 프로그램을 Azure AD 응용 프로그램 tooaccess 클릭 **사용 권한을 관리**합니다. 키 및 회신 Url 또는 tooedit hello 응용 프로그램의 매니페스트를 변경 하는 등의 관리 작업을 클릭 **응용 프로그램 관리**합니다.

### <a name="edit-hello-apps-settings-or-manifest"></a>Hello 응용 프로그램의 설정을 편집 하거나 매니페스트

클릭 하 여 tooedit hello 응용 프로그램의 설정 또는 매니페스트를 **응용 프로그램 관리**합니다.

![응용 프로그램 관리 페이지](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>다음 단계

시작 [tooyour 계정에 파일 업로드](media-services-portal-upload-files.md)합니다.
