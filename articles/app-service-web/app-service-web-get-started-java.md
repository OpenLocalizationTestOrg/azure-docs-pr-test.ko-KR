---
title: "aaaCreate Azure에서 첫 번째 Java 웹 앱"
description: "기본 Java 응용 프로그램을 배포 하 여 toorun 앱 서비스에서 앱 웹 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Azure에서 첫 번째 Java 웹앱 만들기

hello [웹 앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 의 기능 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 자체 패치, 확장성이 뛰어난 웹 호스팅 서비스를 제공 합니다. 이 퀵 스타트의 toodeploy Java 앱 tooApp 서비스 hello를 사용 하 여 웹 하는 방법을 보여 줍니다. [Eclipse IDE for Java EE Developers](http://www.eclipse.org/)합니다.

!["Hello Azure!" 예제 웹앱](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른이 시작 설치:

* 무료 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)합니다. 이 빠른 시작은 Eclipse Neon을 사용합니다.
* hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation)합니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Eclipse에서 동적 웹 프로젝트 만들기

Eclipse에서 **파일** > **새로 만들기** > **동적 웹 프로젝트**를 선택합니다.

Hello에 **새 동적 웹 프로젝트** 대화 상자, 이름 hello 프로젝트 **MyFirstJavaOnAzureWebApp**를 선택 하 고 **마침**합니다.
   
![새 동적 웹 프로젝트 대화 상자](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>JSP 페이지 추가

프로젝트 탐색기 표시되지 않으면 복원합니다.

![Eclipse용 Java EE 작업 영역](./media/app-service-web-get-started-java/pe.png)

프로젝트 탐색기에서 확장 hello **MyFirstJavaOnAzureWebApp** 프로젝트.
**WebContent**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **JSP 파일**을 선택합니다.

![프로젝트 탐색기에서 새 JSP 파일에 대한 메뉴](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

Hello에 **JSP 파일 새로** 대화 상자:

* 이름 hello 파일 **index.jsp**합니다.
* **마침**을 선택합니다.

  ![새 JSP 파일 대화 상자](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

Hello index.jsp 파일에서 대체 hello `<body></body>` 요소 태그를 다음 hello로:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Hello 변경 내용을 저장 합니다.

## <a name="publish-hello-web-app-tooazure"></a>웹 앱 tooAzure hello 게시

프로젝트 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Azure** > **Azure 웹 앱으로 게시**합니다.

![Azure 웹앱으로 게시 상황에 맞는 메뉴](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

Hello에 **Azure 로그인** 대화 상자, 유지 hello **Interactive'** 옵션을 선택한 다음 선택 **로그인**합니다.

Hello 로그인 지침을 따릅니다.

### <a name="deploy-web-app-dialog-box"></a>웹앱 배포 대화 상자

Tooyour Azure 계정에에서 로그인 한 후 hello **웹 응용 프로그램 배포** 대화 상자가 나타납니다.

**만들기**를 선택합니다.

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>앱 서비스 만들기 대화 상자

hello **응용 프로그램 서비스 만들기** 기본 값으로 대화 상자가 나타납니다. 번호 hello **170602185241** hello 뒤에 표시 된 이미지 대화 상자에 따라 달라 집니다.

![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/cas1.png)

Hello에 **응용 프로그램 서비스 만들기** 대화 상자:

* Hello 웹 앱에 대 한 이름을 생성 하는 hello를 유지 합니다. 이 이름은 Azure에서 고유해야 합니다. hello 이름은 hello 웹 앱에 대 한 hello URL 주소의 일부입니다. 예를 들어: hello 웹 응용 프로그램 이름이 **MyJavaWebApp**, URL은 hello *myjavawebapp.azurewebsites.net*합니다.
* Hello 기본 웹 컨테이너를 유지 합니다.
* Azure 구독을 선택합니다.
* Hello에 **앱 서비스 계획** 탭:

  * **새로 만들기**: 이름인 hello hello 앱 서비스 계획의 hello 기본값을 유지 합니다.
  * **위치**: **유럽 서부** 또는 인접 위치를 선택합니다.
  * **가격 책정 계층**: 선택 hello 무료 옵션입니다. 기능의 경우 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.

   ![앱 서비스 만들기 대화 상자](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>리소스 그룹 탭

선택 hello **리소스 그룹** 탭 합니다. Hello 리소스 그룹에 대 한 hello 생성 된 기본 값을 유지 합니다.

![리소스 그룹 탭](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

**만들기**를 선택합니다.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

hello Azure 도구 키트 hello 웹 앱을 만들고 한 진행률 대화 상자를 표시 합니다.

![App Service 만들기 진행률 대화 상자](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>웹앱 배포 대화 상자

Hello에 **웹 응용 프로그램 배포** 대화 상자에서 **tooroot 배포**합니다. 응용 프로그램 서비스에 있는 경우 *wingtiptoys.azurewebsites.net* toohello 루트, 라는 hello 웹 앱을 배포 하지 않는 및 **MyFirstJavaOnAzureWebApp** 너무 배포 *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*합니다.

![웹앱 배포 대화 상자](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

hello 대화 상자 표시 hello Azure, JDK, 및 웹 컨테이너 선택 합니다.

선택 **배포** toopublish hello 웹 응용 프로그램 tooAzure 합니다.

Hello 게시 완료 되 면 선택 hello **게시 됨** hello에 대 한 링크 **Azure 활동 로그** 대화 상자.

![Azure 활동 로그 대화 상자](./media/app-service-web-get-started-java/aal.png)

축하합니다. 웹 앱 tooAzure 성공적으로 배포 했습니다. 

!["Hello Azure!" 예제 웹앱](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Hello 웹 응용 프로그램 업데이트

Hello 샘플 JSP 코드 tooa 서로 다른 메시지를 변경 합니다.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Hello 변경 내용을 저장 합니다.

프로젝트 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Azure** > **Azure 웹 앱으로 게시**합니다.

hello **웹 응용 프로그램 배포** 표시 hello 이전에 만든 응용 프로그램 서비스와 대화 상자가 나타납니다. 

> [!NOTE]
> 선택 **tooroot 배포** 게시 될 때마다 합니다.
>

Hello 웹 사이트를 선택 하 고 선택 **배포**,이 명령은 hello 변경 내용을 게시 합니다.

Hello 때 **게시** 링크가 표시 toobrowse toohello 웹 앱을 선택 하 고 hello 변경 내용을 확인 합니다.

## <a name="manage-hello-web-app"></a>Hello 웹 응용 프로그램 관리

Toohello 이동 <a href="https://portal.azure.com" target="_blank">Azure 포털</a> 만든 toosee hello 웹 앱입니다.

Hello 왼쪽된 메뉴에서 선택 **리소스 그룹**합니다.

![포털 탐색 tooresource 그룹](media/app-service-web-get-started-java/rg.png)

Hello 리소스 그룹을 선택 합니다. hello 페이지에는이 빠른 시작에서 만든 hello 리소스가 표시 됩니다.

![리소스 그룹 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

웹 앱 선택 hello (**webapp 170602193915** hello 이미지 앞에).

hello **개요** 페이지가 나타납니다. 이 페이지에서는 hello 응용 프로그램에서 수행 하는 방법을 볼 수 있습니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. hello 탭 hello hello 페이지의 왼쪽에 열 수 있는 다양 한 구성 hello를 표시 합니다. 

![Azure Portal의 App Service 페이지](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [사용자 지정 도메인 매핑](app-service-web-tutorial-custom-domain.md)
