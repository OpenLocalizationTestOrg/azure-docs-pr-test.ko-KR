---
title: "스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 aaaDeploy | Microsoft Docs"
description: "이 자습서에서는 hello 단계 toodeploy hello 스프링 부팅 시작 웹 앱 tooAzure 서비스 응용 프로그램 개발자에 게 안내 합니다."
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
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="491ce-103">스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="491ce-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="491ce-104">hello  **[Spring Framework]**  은 오픈 소스 솔루션으로는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되며 해당 플랫폼 위에 빌드되는 hello 더 이상 인기 있는 프로젝트 중 하나 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 있는 간단한 접근 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="491ce-105">이 자습서에서는 안내 하지만 hello 샘플 스프링 부팅 시작 웹 응용 프로그램을 만들고 너무 배포[Azure 앱 서비스]합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="491ce-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="491ce-106">Prerequisites</span></span>

<span data-ttu-id="491ce-107">이 자습서에서는 toocomplete hello 단계 순서 toohave hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="491ce-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="491ce-109">최신 [JDK(Java Developer Kit)]</span><span class="sxs-lookup"><span data-stu-id="491ce-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="491ce-110">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="491ce-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="491ce-111">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="491ce-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="491ce-112">Hello 스프링 부팅 시작 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="491ce-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="491ce-113">hello 다음 단계는 단계를 안내 hello 필요한 toocreate 간단한 스프링 부팅 웹 응용 프로그램 이며 로컬로 테스트할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="491ce-114">명령 프롬프트를 열고 응용 프로그램 및 toothat 디렉터리를 변경 합니다; 로컬 디렉터리 toohold 만들 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="491ce-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="491ce-115">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="491ce-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="491ce-116">복제 hello [스프링 부팅 시작] ; 방금 만든 hello 디렉터리로 샘플 프로젝트 예:</span><span class="sxs-lookup"><span data-stu-id="491ce-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="491ce-117">디렉터리 toohello 완료 된 프로젝트를 변경 합니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="491ce-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="491ce-118">Maven;를 사용 하 여 hello JAR 파일 빌드 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="491ce-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="491ce-119">Hello 웹 응용 프로그램을 만든 후 toohello JAR 파일 디렉터리를 변경 하 고 hello 웹 응용 프로그램 시작 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="491ce-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="491ce-120">Toohttp://localhost:8080 웹 브라우저를 사용 하 여 검색 하 여 hello 웹 앱을 테스트 하거나 hello curl을 사용할 수 있는 경우 다음 예제에서는 같은 hello 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="491ce-121">Hello 메시지 표시의 뒤에 표시 됩니다: **스프링 부팅의!**</span><span class="sxs-lookup"><span data-stu-id="491ce-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="491ce-123">Java에서 사용할 Azure 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="491ce-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="491ce-124">단계를 수행 하는 hello 과정을 단계별로 hello 단계 toocreate Azure 웹 앱 하 고 Java에 대 한 hello 필요한 설정을 구성 하 고 FTP 자격 증명을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="491ce-125">Toohello 찾아보기 [Azure 포털] 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="491ce-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="491ce-126">를 hello Azure 포털에서 사용자의 계정에 로그인 한 후에 대 한 hello 메뉴 아이콘을 클릭 합니다. **응용 프로그램 서비스**:</span><span class="sxs-lookup"><span data-stu-id="491ce-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure portal][AZ01]

1. <span data-ttu-id="491ce-128">Hello 때 **응용 프로그램 서비스** 페이지가 표시 되 면 클릭 **+ 추가** toocreate 새 앱 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![App Service 만들기][AZ02]

1. <span data-ttu-id="491ce-130">Hello 웹 응용 프로그램 템플릿 목록이 표시 되 면 hello에 대 한 hello 링크를 클릭 기본 Microsoft 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![웹앱 템플릿][AZ03]

1. <span data-ttu-id="491ce-132">Hello 웹 응용 프로그램 템플릿에 대 한 hello 정보 페이지 표시 되 면 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![웹앱 만들기][AZ04]

1. <span data-ttu-id="491ce-134">웹앱에 고유한 이름을 제공하고 모든 추가 설정을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![웹앱 만들기 설정][AZ05]

1. <span data-ttu-id="491ce-136">웹 앱을 만든 후에 대 한 hello 메뉴 아이콘을 클릭 합니다. **응용 프로그램 서비스**, 새로 만든 웹 응용 프로그램을 클릭 한 다음:</span><span class="sxs-lookup"><span data-stu-id="491ce-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![웹앱 나열][AZ06]

1. <span data-ttu-id="491ce-138">웹 앱이 표시 되 면 다음 단계는 hello를 사용 하 여 hello Java 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="491ce-139">a.</span><span class="sxs-lookup"><span data-stu-id="491ce-139">a.</span></span> <span data-ttu-id="491ce-140">Hello 클릭 **응용 프로그램 설정** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="491ce-141">b.</span><span class="sxs-lookup"><span data-stu-id="491ce-141">b.</span></span> <span data-ttu-id="491ce-142">선택 **Java 8** hello Java 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="491ce-143">c.</span><span class="sxs-lookup"><span data-stu-id="491ce-143">c.</span></span> <span data-ttu-id="491ce-144">선택 **Newest** hello 부 Java 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="491ce-145">d.</span><span class="sxs-lookup"><span data-stu-id="491ce-145">d.</span></span> <span data-ttu-id="491ce-146">선택 **최신 Tomcat 8.5** hello 웹 컨테이너에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="491ce-147">(이 컨테이너는 실제로 사용 되지 않으면 Azure 사용 스프링 부팅 응용 프로그램에서 hello 컨테이너입니다.)</span><span class="sxs-lookup"><span data-stu-id="491ce-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="491ce-148">e.</span><span class="sxs-lookup"><span data-stu-id="491ce-148">e.</span></span> <span data-ttu-id="491ce-149">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-149">Click **Save**.</span></span>

   ![응용 프로그램 설정][AZ07]

1. <span data-ttu-id="491ce-151">단계를 수행 하는 hello를 사용 하 여 FTP 배포 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="491ce-152">a.</span><span class="sxs-lookup"><span data-stu-id="491ce-152">a.</span></span> <span data-ttu-id="491ce-153">Hello 클릭 **배포 자격 증명** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="491ce-154">b.</span><span class="sxs-lookup"><span data-stu-id="491ce-154">b.</span></span> <span data-ttu-id="491ce-155">사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-155">Specify your username and password.</span></span>

   <span data-ttu-id="491ce-156">c.</span><span class="sxs-lookup"><span data-stu-id="491ce-156">c.</span></span> <span data-ttu-id="491ce-157">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-157">Click **Save**.</span></span>

   ![배포 자격 증명 지정][AZ08]

1. <span data-ttu-id="491ce-159">단계를 수행 하는 hello를 사용 하 여 FTP 연결 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="491ce-160">a.</span><span class="sxs-lookup"><span data-stu-id="491ce-160">a.</span></span> <span data-ttu-id="491ce-161">Hello 클릭 **배포 자격 증명** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="491ce-162">b.</span><span class="sxs-lookup"><span data-stu-id="491ce-162">b.</span></span> <span data-ttu-id="491ce-163">전체 FTP 사용자 이름 및 URL을 복사한 hello이이 자습서의 다음 섹션에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![FTP URL 및 자격 증명][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="491ce-165">스프링 부팅 웹 응용 프로그램 tooAzure 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="491ce-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="491ce-166">단계를 수행 하는 hello 단계별로 안내해 줍니다 hello 단계 toodeploy 프로그램 스프링 부팅 웹 응용 프로그램 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="491ce-167">Windows 메모장 같은 텍스트 편집기를 열고 및 새 문서에 텍스트를 다음 hello 붙여 넣은 다음 hello 파일으로 저장 *web.config*:</span><span class="sxs-lookup"><span data-stu-id="491ce-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
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

1. <span data-ttu-id="491ce-168">Hello를 저장 한 후 *web.config* 파일 tooyour 시스템으로 hello URL, username 및 password hello 앞에이 자습서의 단원에서에서 사용 하 여 FTP 통해 tooyour 웹 앱에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="491ce-169">예:</span><span class="sxs-lookup"><span data-stu-id="491ce-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="491ce-170">웹 응용 프로그램의 변경 hello 원격 디렉터리 toohello 루트 폴더 (\program */사이트/wwwroot*) 다음 스프링 부팅 응용 프로그램에서 hello JAR 파일을 복사 하 고 hello *web.config* 앞에서.</span><span class="sxs-lookup"><span data-stu-id="491ce-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="491ce-171">예:</span><span class="sxs-lookup"><span data-stu-id="491ce-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="491ce-172">프로그램 JAR을 배포 하면 및 *web.config* 파일 tooyour 웹 앱 toorestart hello Azure 포털을 사용 하 여 웹 앱 필요:</span><span class="sxs-lookup"><span data-stu-id="491ce-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="491ce-173">웹 브라우저를 사용 하 여 tooyour 웹 앱의 URL을 탐색 하 여 hello 웹 앱을 테스트 하거나 hello curl을 사용할 수 있는 경우 다음 예제에서는 같은 hello 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="491ce-174">Hello 메시지 표시의 뒤에 표시 됩니다: **스프링 부팅의!**</span><span class="sxs-lookup"><span data-stu-id="491ce-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![샘플 앱 찾아보기][SB02]

## <a name="next-steps"></a><span data-ttu-id="491ce-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="491ce-176">Next steps</span></span>

<span data-ttu-id="491ce-177">Azure에서 스프링 부팅 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="491ce-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="491ce-178">Hello Azure 컨테이너 서비스에서에서 Linux에서 스프링 부팅 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="491ce-179">Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="491ce-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="491ce-180">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="491ce-181">FTP를 사용 하 여 depoying 웹 앱 tooAzure에 대 한 자세한 내용은 참조 하십시오. [프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포]합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="491ce-182">Hello 스프링 부팅 샘플 프로젝트에 대 한 자세한 내용은 참조 하십시오. [스프링 부팅 시작]합니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="491ce-183">스프링 부팅 응용 프로그램 시작 하기 도움말을 참조 hello **스프링 Initializr** https://start.spring.io/에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="491ce-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="491ce-184">웹앱의 추가 설정 구성에 대한 자세한 내용은 [Azure App Service에서 웹앱 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="491ce-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure 앱 서비스]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Azure 포털]: https://portal.azure.com/
[Azure App Service에서 웹앱 구성]: /azure/app-service-web/web-sites-configure
[프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 부팅 시작]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

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
