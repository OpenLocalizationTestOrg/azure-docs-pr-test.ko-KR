---
title: "Azure 앱 서비스 웹 앱에 Java 응용 프로그램 추가"
description: "이 자습서에서는 페이지 또는 응용 프로그램을 Java를 사용하도록 이미 구성된 Azure 앱 서비스 웹 앱의 인스턴스를 추가하는 방법을 보여줍니다."
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
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="efcec-103">Azure 앱 서비스 웹 앱에 Java 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="efcec-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="efcec-104">[Azure 앱 서비스에서 Java 웹 앱 만들기](web-sites-java-get-started.md)에 설명된 대로 [Azure App Service][Azure App Service]에서 Java 웹 앱을 초기화하면, **webapps** 폴더에 WAR을 배치하여 응용 프로그램을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="efcec-105">**webapps** 폴더의 탐색 경로는 웹 앱 인스턴스 설정 방법에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="efcec-106">Azure Marketplace를 사용하여 웹앱을 설정한 경우 **webapps** 폴더의 경로는 **d:\home\site\wwwroot\bin\application\_server\webapps**의 형식이며, 여기서 **application\_server**는 Web Apps 인스턴스에 적용되는 응용 프로그램 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="efcec-107">Azure 구성 UI를 사용하여 웹앱을 설정한 경우 **webapps** 폴더의 경로는 **d:\home\site\wwwroot\webapps**의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="efcec-108">소스 제어를 사용하여 [연속 통합 시나리오](app-service-continuous-deployment.md)에 포함된 응용 프로그램 또는 웹 페이지를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="efcec-109">또한 FTP는 응용 프로그램 또는 웹 페이지 업로드를 위한 옵션입니다. FTP를 통해 응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [Azure App Service에 앱 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efcec-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="efcec-110">Tomcat 웹 앱에 대한 참고 사항: **webapps** 폴더에 WAR 파일을 업로드하면 Tomcat 응용 프로그램 서버에서 해당 파일을 추가했는지 검색한 후 자동으로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="efcec-111">파일(WAR 이외 파일)을 루트 디렉터리로 복사한 경우에는 해당 파일을 사용하기 전에 응용 프로그램 서버를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="efcec-112">Azure에서 실행되는 Tomcat Java 웹 앱의 자동 로드 기능은 추가 중인 새 WAR 파일이나 **webapps** 폴더에 추가된 새 파일 또는 디렉터리를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="efcec-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="efcec-113">참고 항목</span><span class="sxs-lookup"><span data-stu-id="efcec-113">See Also</span></span>
<span data-ttu-id="efcec-114">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efcec-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="efcec-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="efcec-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="efcec-116">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="efcec-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="efcec-117">[Azure App Service에 앱 배포]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="efcec-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
