---
title: "aaaAdd Java 응용 프로그램 tooAzure 앱 서비스 웹 앱"
description: "이 자습서 tooadd 이미 있는 Azure 앱 서비스 웹 앱의 페이지 또는 응용 프로그램 tooyour 인스턴스 toouse Java를 구성 하는 방법을 보여 줍니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="4066b-103">Java 응용 프로그램 tooAzure 앱 서비스 웹 앱 추가</span><span class="sxs-lookup"><span data-stu-id="4066b-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="4066b-104">Java 웹 응용 프로그램 초기화 되 면 [Azure 앱 서비스] [ Azure App Service] 에 문서화 된 대로 [Azure 앱 서비스에서 Java 웹 앱을 만들](web-sites-java-get-started.md)를 배치 하 여 응용 프로그램을 업로드할 수 있습니다 프로그램 전쟁 hello에 **webapps** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="4066b-105">탐색 경로 toohello hello **webapps** 폴더를 웹 응용 프로그램 인스턴스를 설정 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="4066b-106">Hello Azure Marketplace를 사용 하 여 웹 앱을 설정 하면 경로 toohello hello **webapps** 폴더는 hello 형태로 **d:\home\site\wwwroot\bin\application\_server\webapps**여기서 **응용 프로그램\_서버** 웹 앱 인스턴스에 대 한 적용 hello 응용 프로그램 서버 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="4066b-107">Hello Azure 구성 UI 사용 하 여 웹 앱을 설정 하면 경로 toohello hello **webapps** 폴더는 hello 형태로 **d:\home\site\wwwroot\webapps**합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="4066b-108">응용 프로그램 또는 웹 페이지를 포함 하 여 소스 제어 tooupload를 사용할 수 있습니다 [연속 통합 시나리오](app-service-continuous-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="4066b-109">FTP는 또한 응용 프로그램 또는 웹 페이지; 업로드 하기 위한 옵션 FTP를 통한 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 [프로그램 응용 프로그램 tooAzure 앱 서비스 배포]합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="4066b-110">Tomcat 웹 앱에 대 한 참고: WAR 파일 toohello에 업로드 했으므로 **webapps** 폴더 hello Tomcat 응용 프로그램 서버에서 되었음을 감지 하면 추가한 것 자동으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="4066b-111">참고 (WAR 파일)을 제외한 파일 toohello 루트 디렉터리를 복사 하는 경우 hello 응용 프로그램 서버는 해당 파일을 사용 하기 전에 다시 시작 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="4066b-112">hello Azure에서 실행 되는 Tomcat Java 웹 앱에 대 한 hello autoload 기능 추가, 새 WAR 파일을 삭제 하거나 새 파일 또는 디렉터리 추가 toohello **webapps** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="4066b-113">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4066b-113">See Also</span></span>
<span data-ttu-id="4066b-114">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="4066b-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="4066b-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="4066b-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[프로그램 응용 프로그램 tooAzure 앱 서비스 배포]: ./web-sites-deploy.md
