---
title: "Mobile Engagement REST Api-수동 설치로 aaaAuthenticate"
description: "Toomanually Mobile Engagement REST Api에 대 한 인증을 설정 하는 방법을 설명 합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Mobile Engagement REST API를 사용한 인증 - 수동 설치
이 부록 설명서 너무는[Mobile Engagement REST Api로 인증](mobile-engagement-api-authentication.md)합니다. 첫 번째 tooget hello 컨텍스트의 읽이 없어야 합니다. 이 설명 hello Mobile Engagement REST Api를 사용 하 여 Azure 포털을 hello에 대 한 대체 방법을 toodo hello 일회성에 대해 설정 된 사용자 인증 설정이 끝났습니다. 

> [!NOTE]
> 아래의 hello 지침 기반으로이 [Active Directory 가이드](../azure-resource-manager/resource-group-create-service-principal-portal.md) 와 Mobile Engagement Api에 대 한 인증을 위해 필요한 사항에 대 한 사용자 지정 합니다. 따라서 아래 toounderstand hello 단계를 자세히 하려는 경우 tooit을 참조 하십시오. 
> 
> 

1. Hello 통해 Azure 계정 로그인 tooyour [클래식 포털](https://manage.windowsazure.com/)합니다.
2. 선택 **Active Directory** hello 왼쪽된 창에서.
   
     ![Active Directory 선택][1]
3. Hello 선택 **Active Directory 기본** Azure 포털에서 합니다. 
   
     ![디렉터리 선택][2]
   
   > [!IMPORTANT]
   > 이 방법은 hello 기본 Active Directory의 계정에서에서 작업 하 고 사용자가 만든 계정에 Active Directory에서 이렇게 하는 경우 작동 하지 것입니다는 경우에 작동 합니다. 
   > 
   > 
4. 디렉터리의 tooview hello 응용 프로그램에서 클릭 **응용 프로그램**합니다.
   
     ![응용 프로그램 보기][3]
5. **추가**를 클릭합니다. 
   
     ![응용 프로그램 추가][4]
6. **내 조직에서 개발 중인 응용 프로그램 추가**
   
     ![새 응용 프로그램][5]
7. Hello 응용 프로그램 이름 선택 hello 유형의 응용 프로그램으로를 입력 **웹 응용 프로그램 및/또는 웹 API** hello 다음 단추를 클릭 합니다.
   
     ![응용 프로그램 이름 지정][6]
8. **로그인 URL** 및 **앱 ID URI**에 대한 더미 URL을 제공할 수 있습니다. 이 시나리오에 사용 되지 않는 및 자체 hello Url 유효성이 검사 되지 않습니다.  
   
     ![응용 프로그램 속성][7]
9. 이 hello 끝 hello 다음과 같이 이전에 제공한 hello 이름의 AAD 응용 프로그램 해야 합니다. 이것이 **AD\_APP\_NAME**이며 메모해 둡니다.  
   
     ![앱 이름][8]
10. Hello 응용 프로그램 이름을 클릭 하 고 클릭 **구성**합니다.
    
      ![앱 구성][9]
11. Hello로 사용 될 클라이언트 ID를 메모해 **클라이언트\_ID** API를 호출 합니다. 
    
     ![앱 구성][10]
12. Toohello 아래로 스크롤하여 **키** 섹션 가급적 2 년 (만료) 기간을 사용 하 여 키를 추가 하 고 클릭 **저장**합니다. 
    
     ![앱 구성][11]
13. 즉시 hello 값 복사만 이제 표시 하는 저장 되지 않으므로 다시 표시 되지 것입니다 hello 키에 대 한 표시 되어 있습니다. 분실 한 경우 다음 나면 toogenerate 새 키입니다. Hello 됩니다 **CLIENT_SECRET** API를 호출 합니다. 
    
     ![앱 구성][12]
    
    > [!IMPORTANT]
    > 이 키는 hello 시간이 되 고, 그렇지 API 인증 하는 경우 더 이상 작동 하지 것입니다 너무 확인 되었는지 toorenew 지정한 hello 기간의 hello 끝에 만료 됩니다. 또한 손상되었다고 생각하는 경우 이 키를 삭제하고 다시 만들 수 있습니다.
    > 
    > 
14. 클릭 **끝점 보기** 이제 hello를 열 수 있는 단추 **앱 끝점** 대화 상자. 
    
    ![][13]
15. Hello 앱 끝점 대화 상자에서 복사 hello **OAUTH 2.0 토큰 끝점**합니다. 
    
    ![][14]
16. 이 끝점 hello hello hello URL의 GUID는 폼을 다음에 포함 될 프로그램 **TENANT_ID** 기록해 둡니다. 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. 이제이 응용 프로그램에 대 한 hello 권한을 tooconfigure 진행 됩니다. 이 대 한 hello tooopen 갖습니다 [Azure 포털](https://portal.azure.com)합니다. 
18. 클릭 **리소스 그룹** hello 및 **Mobile Engagement** 리소스 그룹입니다.  
    
    ![][15]
19. Hello 클릭 **Mobile Engagement** 리소스 그룹화 하 고 탐색 toohello **설정** 블레이드 여기 합니다. 
    
    ![][16]
20. 클릭 **사용자** 설정 블레이드에서 hello와 클릭 **추가** tooadd 사용자입니다. 
    
    ![][17]
21. **역할 선택**
    
    ![][18]
22. **소유자**
    
    ![][19]
23. 응용 프로그램의 hello 이름에 대해 **AD\_앱\_이름** hello 검색 상자에 있습니다. 여기에 기본적으로 표시되지 않습니다. 를 찾은 후 선택 하 고 클릭 **선택** hello hello 블레이드 맨 아래에 있습니다. 
    
    ![][20]
24. Hello에 **액세스 추가** 블레이드에서 것으로 표시 됩니다 **사용자 1, 0 그룹**합니다. 클릭 **확인** 이 블레이드 tooconfirm hello 변경 합니다. 
    
    ![][21]

필요한 hello AAD 구성을 완료 했으므로 되며 모든 집합 toocall hello Api 합니다. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



