---
title: "Azure App Service에 Spring Boot 응용 프로그램 배포 | Microsoft Docs"
description: "이 자습서는 개발자에게 Azure App Service에 Spring Boot 시작하기 웹앱을 배포하는 단계를 안내합니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="2de56-103">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="2de56-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="2de56-104">**[Spring Framework]**는 Java 개발자가 엔터프라이즈 수준 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션이며, 해당 플랫폼 맨 위에 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만들기 위한 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="2de56-105">이 자습서에서는 샘플 Spring Boot 시작하기 웹앱 만들어 [Azure App Service]에 배포하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2de56-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2de56-106">Prerequisites</span></span>

<span data-ttu-id="2de56-107">이 자습서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="2de56-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="2de56-109">최신 [JDK(Java Developer Kit)]</span><span class="sxs-lookup"><span data-stu-id="2de56-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="2de56-110">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="2de56-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="2de56-111">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2de56-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="2de56-112">Spring Boot 시작하기 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2de56-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="2de56-113">다음 단계에서는 간단한 Spring Boot 웹 응용 프로그램을 만들어 로컬로 테스트하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="2de56-114">명령 프롬프트를 열고 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2de56-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="2de56-115">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="2de56-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="2de56-116">[Spring Boot 시작하기] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2de56-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="2de56-117">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2de56-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="2de56-118">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2de56-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="2de56-119">웹앱이 만들어지면 디렉터리를 JAR 파일로 변경하고 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2de56-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="2de56-120">웹 브라우저를 통해 http://localhost:8080 으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="2de56-121">다음과 같이 **Greetings from Spring Boot!**라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="2de56-123">Java에서 사용할 Azure 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2de56-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="2de56-124">다음 단계에서는 Azure 웹앱을 만들고 Java에 필요한 설정을 구성하고 FTP 자격 증명을 구성하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="2de56-125">[Azure Portal]로 이동하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="2de56-126">Azure Portal의 계정에 로그인한 후 **App Services** 메뉴 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Azure 포털][AZ01]

1. <span data-ttu-id="2de56-128">**App Services** 페이지가 표시되면 **+ 추가**를 클릭하여 새 App Service를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![App Service 만들기][AZ02]

1. <span data-ttu-id="2de56-130">웹앱 템플릿 목록이 표시되면 기본 Microsoft 웹앱에 대한 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![웹앱 템플릿][AZ03]

1. <span data-ttu-id="2de56-132">웹앱 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![웹앱 만들기][AZ04]

1. <span data-ttu-id="2de56-134">웹앱에 고유한 이름을 제공하고 모든 추가 설정을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![웹앱 만들기 설정][AZ05]

1. <span data-ttu-id="2de56-136">웹앱을 만든 후 **App Services** 메뉴 아이콘을 클릭한 다음 새로 만든 웹앱을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![웹앱 나열][AZ06]

1. <span data-ttu-id="2de56-138">웹앱이 표시되면 다음 단계를 사용하여 Java 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="2de56-139">a.</span><span class="sxs-lookup"><span data-stu-id="2de56-139">a.</span></span> <span data-ttu-id="2de56-140">**응용 프로그램 설정** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="2de56-141">b.</span><span class="sxs-lookup"><span data-stu-id="2de56-141">b.</span></span> <span data-ttu-id="2de56-142">Java 버전으로 **Java 8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="2de56-143">c.</span><span class="sxs-lookup"><span data-stu-id="2de56-143">c.</span></span> <span data-ttu-id="2de56-144">부 Java 버전으로 **가장 최근 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="2de56-145">d.</span><span class="sxs-lookup"><span data-stu-id="2de56-145">d.</span></span> <span data-ttu-id="2de56-146">웹 컨테이너로 **최신 Tomcat 8.5**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="2de56-147">(이 컨테이너는 실제로 사용되지 않습니다. Azure는 Spring Boot 응용 프로그램의 컨테이너를 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="2de56-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="2de56-148">e.</span><span class="sxs-lookup"><span data-stu-id="2de56-148">e.</span></span> <span data-ttu-id="2de56-149">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-149">Click **Save**.</span></span>

   ![응용 프로그램 설정][AZ07]

1. <span data-ttu-id="2de56-151">다음 단계를 사용하여 FTP 배포 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="2de56-152">a.</span><span class="sxs-lookup"><span data-stu-id="2de56-152">a.</span></span> <span data-ttu-id="2de56-153">**배포 자격 증명** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="2de56-154">b.</span><span class="sxs-lookup"><span data-stu-id="2de56-154">b.</span></span> <span data-ttu-id="2de56-155">사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-155">Specify your username and password.</span></span>

   <span data-ttu-id="2de56-156">c.</span><span class="sxs-lookup"><span data-stu-id="2de56-156">c.</span></span> <span data-ttu-id="2de56-157">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-157">Click **Save**.</span></span>

   ![배포 자격 증명 지정][AZ08]

1. <span data-ttu-id="2de56-159">다음 단계를 사용하여 FTP 연결 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="2de56-160">a.</span><span class="sxs-lookup"><span data-stu-id="2de56-160">a.</span></span> <span data-ttu-id="2de56-161">**배포 자격 증명** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="2de56-162">b.</span><span class="sxs-lookup"><span data-stu-id="2de56-162">b.</span></span> <span data-ttu-id="2de56-163">전체 FTP 사용자 이름 및 URL을 복사하고 이 자습서의 다음 섹션을 위해 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![FTP URL 및 자격 증명][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="2de56-165">Azure에 Spring Boot 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="2de56-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="2de56-166">다음 단계에서는 Azure에 Spring Boot 웹앱을 배포하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="2de56-167">Windows 메모장과 같은 텍스트 편집기를 열고 새 문서에 다음 텍스트를 붙여넣은 후 파일을 *web.config*로 저장합니다</span><span class="sxs-lookup"><span data-stu-id="2de56-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="2de56-168">*web.config* 파일을 시스템에 저장한 후 이 자습서의 이전 섹션에 나온 URL, 사용자 이름 및 암호를 사용하여 FTP를 통해 웹앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="2de56-169">예:</span><span class="sxs-lookup"><span data-stu-id="2de56-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="2de56-170">원격 디렉터리를 웹앱의 루트 폴더(*/site/wwwroot*)로 변경한 다음 Spring Boot 응용 프로그램의 JAR 파일과 앞에서의 *web.config*를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="2de56-171">예:</span><span class="sxs-lookup"><span data-stu-id="2de56-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="2de56-172">JAR 파일과 *web.config* 파일을 웹앱에 배포한 후 Azure Portal을 사용하여 웹앱을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="2de56-173">웹 브라우저를 사용해 웹앱의 URL로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="2de56-174">다음과 같이 **Greetings from Spring Boot!**라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2de56-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![샘플 앱 찾아보기][SB02]

## <a name="next-steps"></a><span data-ttu-id="2de56-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2de56-176">Next steps</span></span>

<span data-ttu-id="2de56-177">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="2de56-178">Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="2de56-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="2de56-179">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="2de56-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="2de56-180">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="2de56-181">FTP를 사용하여 Azure에 웹앱을 배포하는 방법에 대한 자세한 내용은 [FTP/S를 사용하여 Azure App Service에 앱 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="2de56-182">Spring Boot 샘플 프로젝트에 대한 자세한 내용은 [Spring Boot 시작하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="2de56-183">자체 Spring Boot 응용 프로그램을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="2de56-184">웹앱의 추가 설정 구성에 대한 자세한 내용은 [Azure App Service에서 웹앱 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2de56-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="2de56-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="2de56-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="2de56-186">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="2de56-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="2de56-187">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="2de56-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="2de56-188">[Azure App Service에서 웹앱 구성]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="2de56-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="2de56-189">[FTP/S를 사용하여 Azure App Service에 앱 배포]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="2de56-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="2de56-190">[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="2de56-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="2de56-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="2de56-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="2de56-192">[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="2de56-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="2de56-193">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="2de56-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="2de56-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="2de56-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="2de56-195">[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="2de56-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="2de56-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="2de56-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="2de56-197">[Spring Boot 시작하기]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="2de56-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="2de56-198">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="2de56-198">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
