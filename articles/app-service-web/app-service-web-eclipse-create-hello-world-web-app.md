---
title: "사용 하 여 기본 Azure 웹 앱 aaaCreate Eclipse | Microsoft Docs"
description: "이 자습서에서는 어떻게 toouse hello Azure 도구 키트에 Eclipse toocreate Azure 용 Hello World 웹 응용 프로그램입니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Eclipse를 사용하여 기본 Azure Web App 만들기
이 자습서에서는 어떻게 toocreate hello를 사용 하 여 기본 Hello World 응용 프로그램 tooAzure 웹 앱으로 배포 및 [Azure Toolkit for Eclipse]합니다. 기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.

이 자습서를 완료 하는 경우 비슷한 toohello 웹 브라우저에서 볼 때 그림을 다음 응용 프로그램에 표시 됩니다.

![Hello World 앱의 미리 보기][01]

## <a name="prerequisites"></a>필수 조건
* JDK(Java 개발자 키트), v 1.8 이상.
* Eclipse IDE for Java EE Developers, Luna 이상. <http://www.eclipse.org/downloads/>에서 다운로드할 수 있습니다.
* Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: [Apache Tomcat] 또는 [Jetty])
* Azure 구독은 <https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있습니다.
* hello [Azure Toolkit for Eclipse]합니다. Hello Azure 도구 키트를 설치 하는 방법에 대 한 정보를 참조 하십시오. [Azure Toolkit for Eclipse 설치 hello]합니다.

## <a name="toocreate-a-hello-world-application"></a>toocreate Hello World 응용 프로그램
먼저 java 프로젝트를 만듭니다.

1. Eclipse를 시작 하 고 hello 메뉴 **파일**, 클릭 **새로**, 클릭 하 고 **동적 웹 프로젝트**합니다. (표시 되지 않으면 **동적 웹 프로젝트** 클릭 한 후 사용 가능한 프로젝트로 표시 **파일** 및 **새로**, 수행가 다음를 hello 다음: 클릭 **파일**, 클릭 **새로**, 클릭 **프로젝트...** 를 확장 하 고 **웹**, 클릭 **동적 웹 프로젝트**를 클릭 하 고 **다음**.)
2. 이 자습서에서는 이름을 hello 프로젝트 **MyWebApp**합니다. 화면에는 비슷한 toohello 다음 표시 됩니다.
   
    ![새로운 동적 웹 프로젝트 만들기][02]
3. **Finish**를 클릭합니다.
4. Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다. **WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.
5. Hello에 **JSP 파일 새로** 대화 상자, 이름 hello 파일 **index.jsp**, hello 상위 폴더를 유지 **MyWebApp/WebContent**, 클릭 하 고 **다음**.
6. Hello에 **JSP 템플릿 선택** 대화 상자에서이 자습서 선택의 목적을 위해 **새 JSP 파일 (html)**, 클릭 하 고 **마침**합니다.
7. Eclipse에서 index.jsp 파일이 열리면 텍스트 toodynamically 디스플레이에서 추가 **Hello World!** hello 기존 내 `<body>` 요소입니다. 업데이트 한 후 `<body>` 콘텐츠 hello 다음 예제와 유사 합니다.
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. index.jsp를 저장합니다.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy 프로그램 응용 프로그램 tooan Azure 웹 응용 프로그램 컨테이너
여러 가지 방법으로 여는 Java 웹 응용 프로그램 tooAzure를 배포할 수 있습니다. 이 자습서에서는 가장 간단한 hello 중 하나를 설명: 응용 프로그램에 배포 된 Azure 웹 응용 프로그램 컨테이너 tooan 됩니다-특수 프로젝트 형식 이나 추가 도구 없는 필요 합니다. hello JDK 및 hello 웹 컨테이너 소프트웨어는 사용자에 게 제공 Azure에서 이므로 없습니다 필요 tooupload 고유한; 하기만 하면 Java 웹 앱입니다. 결과적으로, 응용 프로그램에 대 한 게시 프로세스 hello 초, 분 하지 걸립니다.

1. Eclipse의 프로젝트 탐색기에서 **MyWebApp**을 마우스 오른쪽 단추로 클릭합니다.
2. Hello 상황에 맞는 메뉴에서 선택 **Azure**, 클릭 **Azure 웹 앱으로 게시 중...**
   
    ![Azure 웹앱으로 게시][03]
   
    또는 hello 프로젝트 탐색기에서에서 웹 응용 프로그램 프로젝트를 선택한 상태에서 클릭할 수 있는 hello **게시** hello 도구 모음을 선택 드롭다운 단추 **Azure 웹 앱으로 게시** 여기에서:
   
    ![Azure 웹앱으로 게시][14]
3. 아직 Eclipse에서 Azure에 등록 하지 않은 경우에 Azure 계정에 증명된 toosign를 수 있습니다.
   
    ![Azure 로그인 대화 상자][04]
   
    있으면 여러 Azure 계정에 로그인 하는 hello 프롬프트 hello 하는 동안 일부 프로세스 표시 될 수 있습니다 두 번 이상 toobe 나타나는 경우에 hello 동일 합니다. 이 지침에 설명 된 hello 기호 다음 계속 합니다.
4. Azure 계정에 성공적으로 로그인을 한 후 hello **구독 관리** 대화 상자에 자격 증명으로 연결 된 구독 목록이 표시 됩니다. 나열 된 여러 구독이 있는 경우 그 중 특정 하위 집합만 toowork toouse 않을 것 hello를 필요에 따라 선택을 취소할 수 있습니다. 구독을 선택했으면 **닫기**를 클릭합니다.
   
    ![구독 대화 상자 관리][05]
5. Hello 때 **tooAzure 웹 응용 프로그램 컨테이너 배포** 대화 상자가 나타나면 사용자가 이전에 만든 모든 웹 응용 프로그램 컨테이너 표시 됩니다; hello 목록 모든 컨테이너를 만들지 않은 경우 비어 있게 됩니다.
   
    ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][06]
6. 하지 Azure 웹 응용 프로그램 컨테이너 전에, 또는 toopublish 원하는 경우 응용 프로그램 tooa 새 컨테이너를 만든 경우 단계를 수행 하는 hello를 사용 합니다. 그렇지 않은 경우 기존 웹 응용 프로그램 컨테이너를 선택 하 고 아래의 7 toostep를 건너 뜁니다.
   
   1. **새로 만들기...**
      
       ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][15]
   2. hello **새 웹 응용 프로그램 컨테이너** 대화 상자가 표시 됩니다.
      
       ![새 웹앱 컨테이너 대화 상자][07a]
   3. 입력 한 **DNS 레이블을** 웹 응용 프로그램 컨테이너;에 대해 Azure에서 웹 응용 프로그램에 대 한 hello 호스트 URL의 hello 리프 DNS 레이블을 형성 합니다. (해당 hello 이름은 사용 가능 하 고 tooAzure 웹 응용 프로그램의 명명 요구 사항 준수 note).
   4. Hello에 **웹 컨테이너** 드롭 다운 메뉴에서 응용 프로그램에 대 한 선택 hello 적절 한 소프트웨어.
      
       현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다. Hello 선택한 소프트웨어의 최근 배포를 Azure에서 제공 됩니다 및 Oracle에서 만들어져 Azure에서 제공 하는 JDK 8의 최근 배포에서 실행 됩니다.
   5. Hello에 **구독** 드롭 다운 메뉴에서 선택 hello 구독 toouse이이 배포에 대 한 합니다.
   6. Hello에 **리소스 그룹** 드롭 다운 메뉴에서 사용할 tooassociate 웹 앱 선택 hello 리소스 그룹입니다. (Azure 리소스 그룹을 사용 하면 toogroup 관련 리소스 함께 예, 삭제할 수 있습니다 함께 있도록.)
      
       Skip toostep g 아래 또는 다음 이러한 사용 하 여 hello 단계 toocreate 새 리소스 그룹 및 (있는 경우 모든) 기존 리소스 그룹을 선택할 수 있습니다.
      
      * **새로 만들기...**
      * hello **새 리소스 그룹** 대화 상자가 표시 됩니다.
        
          ![새 리소스 그룹 대화 상자][08]
      * Hello hello에 **이름** 텍스트 상자에 새 리소스 그룹 이름을 지정 합니다.
      * Hello hello에 **지역** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 리소스 그룹에 대 한 위치입니다.
      * 선택 사항: 기본적으로 Java 8의 최근 배포 배포 될 Azure에서 자동으로 사용자 JVM으로 tooyour 웹 응용 프로그램 컨테이너입니다. 그러나 웹 앱에 필요한 경우 다른 버전과 hello JVM의 분포 지정할 수 있습니다. 웹 앱에 대 한 JDK toospecify hello 클릭 hello **JDK** 탭을 hello 다음 옵션 중 하나를 선택 합니다.
        
        * **Hello 기본 Azure 웹 앱 서비스에서 제공 하는 JDK 배포**:이 옵션의 Java 8 최근 배포를 배포 합니다.
        * **타사 JDK를 Azure에서 사용할 수 있는 배포**:이 옵션을 통해 Microsoft Azure에서 제공 하는 Jdk의 hello 목록에서 toochoose 수 있습니다.
        * **이 다운로드 위치에서 나만의 JDK 배포**:이 옵션을 통해 toospecify 수 ZIP 파일로 패키지 해야 및 tooeither를 공개적으로 사용할 수 있는 다운로드 위치 또는 Azure 저장소 계정에 업로드는 사용자 고유의 JDK 배포 하면 액세스할 수 있으며
          
          ![새 웹앱 컨테이너 대화 상자][07b]
   7. **확인**을 클릭합니다.
   8. hello **앱 서비스 계획** 드롭 다운 메뉴는 선택한 리소스 그룹 hello와 관련 된 hello 앱 서비스 계획을 나열 합니다. (앱 서비스 계획 가격 책정 계층 및 계산 인스턴스 크기 hello hello 웹 응용 프로그램의 hello 위치와 같은 정보를 지정 하는 데 사용 합니다. App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)
      
       (있는 경우 하나)는 기존 앱 서비스 계획 선택할 수 있습니다 및 toostep h 아래의 건너뛰거나 이러한 단계 toocreate 새 앱 서비스 계획을 수행 하는 hello를 사용 하 여:
      
      * **새로 만들기...**
      * hello **새 앱 서비스 계획** 대화 상자가 표시 됩니다.
        
          ![새 App Service 계획 대화 상자][09]
      * Hello hello에 **이름** 입력란을 새 앱 서비스 계획에 대 한 이름을 지정 합니다.
      * Hello hello에 **위치** 드롭 다운 메뉴에서 선택 hello 적절 한 Azure 데이터 센터 hello 계획에 대 한 위치입니다.
      * Hello hello에 **가격 책정 계층** 드롭 다운 메뉴에서 선택 hello hello 계획에 대 한 가격 책정 적절 합니다. 테스트 목적으로 **무료**를 선택할 수 있습니다.
      * Hello hello에 **인스턴스 크기** 드롭 다운 메뉴에서 hello 계획에 대 한 선택 hello 적절 한 인스턴스 크기입니다. 테스트 목적으로 **Small**을 선택할 수 있습니다.
   9. 모든 단계는 hello 완료 되 면 hello 새 웹 응용 프로그램 컨테이너 대화 상자 그림 다음 hello와 유사 합니다.
      
       ![새 웹앱 컨테이너 대화 상자][10]
   10. 클릭 **확인** toocomplete hello 만드는 새 웹 응용 프로그램 컨테이너입니다.
       
        에 대 한 hello 목록은 hello 웹 응용 프로그램 컨테이너 toobe 몇 초 기다린 새로 고쳐지고 새로 만든 웹 응용 프로그램 컨테이너 hello 목록에서 선택 됩니다.
7. 이제 웹 응용 프로그램 tooAzure의 준비 toocomplete hello 초기 배포 됩니다.
   
    ![TooAzure 웹 응용 프로그램 컨테이너 대화 상자 배포][11]
   
    클릭 **확인** toodeploy Java 응용 프로그램 toohello 웹 응용 프로그램 컨테이너를 선택 합니다.
   
    기본적으로 응용 프로그램의 응용 프로그램 서버 hello 하위 디렉터리로 배포 됩니다. 원하는 toobe hello 루트 응용 프로그램으로 배포를 하는 경우 확인 hello **tooroot 배포** 확인란을 클릭 하기 전에 **확인**합니다.
8. Hello을 다음으로 표시 되어야 **Azure 활동 로그** 보기는 웹 응용 프로그램의 hello 배포 상태를 나타냅니다.
   
    ![Azure 동작 로그][12]
   
    hello 배포 프로세스를 웹 응용 프로그램 tooAzure 몇 초 이내에 수행 해야 toocomplete 합니다. 때 응용 프로그램 준비, 나타납니다 이라는 링크가 **게시 됨** hello에 **상태** 열입니다. Hello 링크를 클릭할 때 걸리는 있습니다 tooyour 배포 웹 앱의 홈 페이지입니다.

## <a name="updating-your-web-app"></a>웹앱 업데이트
실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.

* 기존 Java 웹 앱의 hello 배포를 업데이트할 수 있습니다.
* 추가 Java 응용 프로그램 toohello 게시할 수 동일한 웹 응용 프로그램 컨테이너입니다.

두 경우 모두 hello 프로세스는 동일 하 고 몇 초 밖에 걸리지:

1. Hello Eclipse 프로젝트 탐색기에서 tooan 기존 웹 응용 프로그램 컨테이너를 추가 하거나 tooupdate hello Java 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다.
2. Hello 상황에 맞는 메뉴에 표시 되 면 선택 **Azure** 차례로 **Azure 웹 앱으로 게시 중...**
3. 이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다. Java 응용 프로그램 tooand 클릭 다시 게시 하거나 toopublish 하나 선택 hello **확인**합니다.

몇 초 후 hello **Azure 활동 로그** 보기에 따라 업데이트 된 배포 표시 됩니다 **게시 됨** 하면 웹 브라우저에서 업데이트 된 응용 프로그램 수 tooverify 됩니다.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>기존 웹앱 시작, 중지 또는 다시 시작
toostart (모든 배포 된 hello Java 응용 프로그램에 포함)는 기존 Azure 웹 앱 컨테이너를 중지, hello를 사용할 수 있습니다 또는 **Azure 탐색기** 보기.

경우 hello **Azure 탐색기** 뷰가 이미 열려 있지 않으면 다음을 클릭 하 여 열 수, **창** Eclipse에서 메뉴를 클릭 한 다음 **보기 표시**, 다음 **다른...** , 다음 **Azure**, 클릭 하 고 **Azure 탐색기**합니다. 이전 로그 하지 않은 경우 물어봅니다 toodo 하므로 합니다.

Hello 때 **Azure 탐색기** 뷰가 표시 됩니다, 사용 하 여 이러한 단계 toostart 따르거나 웹 응용 프로그램을 중지 합니다. 

1. Hello 확장 **Azure** 노드.
2. Hello 확장 **웹 앱** 노드. 
3. 마우스 오른쪽 단추로 클릭 hello 원하는 웹 응용 프로그램입니다.
4. Hello 상황에 맞는 메뉴에 표시 되 면 클릭 **시작**, **중지**, 또는 **다시 시작**합니다. Note hello 메뉴 선택은 상황에 맞는 인식만 실행 중인 웹 응용 프로그램을 중지 하거나은 현재 실행 되는 웹 응용 프로그램을 시작 합니다.
   
    ![기존 웹앱 중지][13]

## <a name="next-steps"></a>다음 단계
Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:

* [Azure Toolkit for Eclipse]
  * [Azure Toolkit for Eclipse 설치 hello]
  * *Eclipse에서 Azure용 Hello World 웹앱 만들기(이 문서)*
  * [Hello Azure Toolkit for Eclipse에서 새로운 이란]
* [IntelliJ용 Azure 도구 키트]
  * [IntelliJ 용 hello Azure 도구 키트 설치]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]
  * [Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터]합니다.

Azure 웹 앱을 만드는 방법에 대 한 자세한 내용은 참조 hello [웹 응용 프로그램 개요]합니다.

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-intellij-create-hello-world-web-app.md
[Azure Toolkit for Eclipse 설치 hello]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ../azure-toolkit-for-intellij-installation.md
[Hello Azure Toolkit for Eclipse에서 새로운 이란]: ../azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[웹 응용 프로그램 개요]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
