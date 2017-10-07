---
title: "hello 5 분 후에 Azure 포털에서에서 Umbraco 웹 앱 aaaDeploy | Microsoft Docs"
description: "얼마나 쉬운지 앱 서비스에서 toorun 웹 앱 샘플 ASP.NET 응용 프로그램을 배포 하 여에 대해 알아봅니다. 결과를 즉시 확인합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>5 분 내에 hello Azure 포털에서에서 Umbraco 웹 응용 프로그램을 배포 합니다.

이 자습서를 통해 배포 n [Umbraco](https://our.umbraco.org/) 웹 앱에 너무[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) (분)에서입니다.

![Umbraco 앱](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>필수 조건
Microsoft Azure 계정이 있어야 합니다. 계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.

> [!NOTE]
> Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다. 시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Hello ASP.NET 응용 프로그램 배포
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)를 엽니다.

    이 링크는 바로 가기 tooimmediately hello Azure 포털에서에서 새 Umbraco 응용 프로그램을 구성 합니다.

3. **앱 이름**에 웹앱 이름을 입력합니다. Hello 이름이 hello에 고유한 경우 hello 상자에서 녹색 확인 표시가 나타납니다 `azurewebsites.net` 도메인입니다.
   
5. **리소스 그룹**, 클릭 **새로 만들기** 새 toocreate [리소스 그룹](../azure-resource-manager/resource-group-overview.md), 이름을 지정 합니다.

7. **App Service 계획/위치** > **새로 만들기**를 클릭합니다. Hello 구성 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 표시 된 것 처럼:

    - **앱 서비스 계획**, 형식 hello 원하는 이름입니다.
    - **위치**, 위치 toohost 계획을 선택 합니다.
    - **가격 책정 계층**을 클릭한 다음 **F1 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.
    - **확인**을 클릭합니다.

    Umbraco CMS 구성 같아야 스크린 샷 다음 hello:

    ![구성 진행 중 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. **SQL Database** > **새 데이터베이스 만들기**를 클릭합니다. 표시 된 것 처럼 hello SQL 데이터베이스를 구성 합니다.

    - **이름**에 이름(예: **myDB**)을 입력합니다.
    - **가격 책정 계층**을 클릭한 다음 **F 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.
    - **대상 서버** > **새 서버 만들기**를 클릭합니다. 표시 된 것 처럼 hello 데이터베이스 서버를 구성 합니다.

        - **서버 이름**에 서버 이름을 입력합니다. Hello 이름이 hello에 고유한 경우 hello 상자에서 녹색 확인 표시가 나타납니다 `.database.windows.net` 도메인입니다.
        - **서버 관리자 로그인**, 형식 hello 원하는 관리자 사용자 이름입니다.
        - **암호** 및 **암호 확인**, hello 원하는 암호를 입력 합니다.
        - 위치 선택 hello 웹 앱에 사용할 동일한 위치를 hello 합니다.
        - 확인 **허용 azure 서비스 tooaccess 서버** 을 선택 합니다.
        - **선택**을 클릭합니다.
    
    - **선택**을 클릭합니다.

13. 클릭 **웹 앱 설정**hello 데이터베이스 사용자 이름 및 암호를 지정 하 고 클릭 **확인**합니다.

    Umbraco CMS 구성 같아야 스크린 샷 다음 hello:

    ![구성 완료 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. **만들기**를 클릭합니다.
    
    Umbraco 앱이 Azure에서 구성에 따라 만들어집니다. **배포를 시작했습니다.** 알림이 표시됩니다.

    ![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Umrbaco 웹앱 시작 및 관리

Azure에서 앱 배포가 완료되면 다른 알림이 표시됩니다.

![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Hello 알림을 클릭 하십시오. 이 누락 하는 경우 항상 액세스할 수 hello 알림 벨을 클릭 하 여 (![알림 아래-Azure 앱 서비스의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    이제 웹앱의 관리 [블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)(*블레이드*: 가로로 열리는 포털 페이지)가 표시됩니다.

3. Hello hello 개요 페이지의 위쪽에 클릭 **찾아보기**합니다.
   
    ![찾아보기 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    이제 hello Umbraco 표시 **시작** 페이지. Hello Umbraco 설치를 구성 하 고 함께 재생 시작!

    ![Umbraco 구성 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>다음 단계
* [ASP.NET 웹 응용 프로그램 tooAzure Visual Studio를 사용 하 여 응용 프로그램 서비스를 배포](app-service-web-get-started-dotnet.md) -toocreate hello 중 하나를 사용 하 여 Visual Studio에서 새 Azure 웹 앱에서 응용 프로그램 템플릿을 포함 하는 방법에 대해 알아봅니다.
* [프로그램 코드 tooAzure 앱 서비스 배포](web-sites-deploy.md)-FTP 또는 원본을 toodeploy 저장소를 제어 하는 방법에 대해 알아봅니다.
* [추가 기능 tooyour 첫 번째 웹 응용 프로그램](app-service-web-get-started-2.md) -걸릴 Azure 앱 toohello 다음 수준입니다. 사용자를 인증합니다. 요구에 따라 규모를 조정합니다. 몇 가지 성능 경고를 설정합니다. 이 모든 작업이 클릭 몇 번으로 가능합니다.
