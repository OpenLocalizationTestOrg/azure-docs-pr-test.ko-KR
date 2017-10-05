---
title: "Azure에 사용자 지정 Java 웹 앱 업로드"
description: "이 자습서에서는 Azure 앱 서비스 웹 앱에 사용자 지정 Java 웹 앱을 업로드하는 방법을 보여줍니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="b61d9-103">Azure에 사용자 지정 Java 웹 앱 업로드</span><span class="sxs-lookup"><span data-stu-id="b61d9-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="b61d9-104">이 항목에서는 [Azure 앱 서비스] 웹앱에 사용자 지정 Java 웹앱을 업로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="b61d9-105">이 항목에는 모든 Java 웹 사이트이나 웹 앱에 적용되는 정보와 특정 응용 프로그램의 일부 예제도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="b61d9-106">[Azure 앱 서비스에서 자바 웹앱 만들기](web-sites-java-get-started.md)에서 설명한 대로 Azure는 Azure 포털의 구성 UI, Azure 마켓플레이스를 사용하여 Java 웹앱을 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="b61d9-107">이 자습서는 Azure 포털 구성 UI 또는 Azure 마켓플레이스를 사용하지 않으려는 경우의 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="b61d9-108">구성 지침</span><span class="sxs-lookup"><span data-stu-id="b61d9-108">Configuration guidelines</span></span>
<span data-ttu-id="b61d9-109">다음에서는 Azure의 사용자 지정 Java 웹 앱에 필요한 설정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="b61d9-110">Java 프로세스에서 사용하는 HTTP 포트는 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="b61d9-111">이 프로세스에서는 환경 변수 `HTTP_PLATFORM_PORT`의 포트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="b61d9-112">단일 HTTP 수신기 이외의 모든 수신 포트는 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="b61d9-113">Tomcat에서는 종료, HTTPS 및 AJP 포트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="b61d9-114">컨테이너는 IPv4 트래픽에 대해서만 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="b61d9-115">응용 프로그램의 **startup** 명령은 구성에서 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="b61d9-116">쓰기 권한이 있는 디렉터리가 필요한 응용 프로그램은 Azure 웹앱의 콘텐츠 디렉터리(**D:\home**)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="b61d9-117">환경 변수 `HOME`은 D:\home을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="b61d9-118">필요에 따라 환경 변수를 web.config 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="b61d9-119">web.config httpPlatform 구성</span><span class="sxs-lookup"><span data-stu-id="b61d9-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="b61d9-120">다음에서는 web.config 내의 **httpPlatform** 형식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="b61d9-121">**arguments** (기본값 = "").</span><span class="sxs-lookup"><span data-stu-id="b61d9-121">**arguments** (Default="").</span></span> <span data-ttu-id="b61d9-122">**processPath** 설정에서 지정한 실행 파일 또는 스크립트의 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="b61d9-123">예제( **processPath** 도 함께 표시):</span><span class="sxs-lookup"><span data-stu-id="b61d9-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="b61d9-124">**processPath** - HTTP 요청을 수신 대기하는 프로세스를 시작할 실행 파일 또는 스크립트의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="b61d9-125">예제:</span><span class="sxs-lookup"><span data-stu-id="b61d9-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="b61d9-126">**rapidFailsPerMinute**(기본값 = 10). **processPath**에 지정된 프로세스에 대해 허용되는 분당 작동 중단 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="b61d9-127">이 제한을 초과한 경우 **HttpPlatformHandler** 에서 남은 시간(분) 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="b61d9-128">**requestTimeout**(기본값 = "00:02:00"). **HttpPlatformHandler**가 `%HTTP_PLATFORM_PORT%`에서 수신 대기하는 프로세스의 응답을 대기하는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="b61d9-129">**startupRetryCount**(기본값 = 10). **HttpPlatformHandler**가 **processPath**에 지정된 프로세스 시작을 시도하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="b61d9-130">자세한 내용은 **startupTimeLimit** 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b61d9-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="b61d9-131">**startupTimeLimit**(기본값 = 10초). 실행 파일/스크립트가 포트에서 수신 대기하는 프로세스를 시작할 때까지 **HttpPlatformHandler**가 대기하는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="b61d9-132">이 시간 제한을 초과하는 경우 **HttpPlatformHandler**가 프로세스를 중단하고 프로세스의 시작을 **startupRetryCount**번 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="b61d9-133">**stdoutLogEnabled**(기본값 = "true"). true인 경우 **processPath** 설정에 지정된 프로세스의 **stdout** 및 **stderr**가 **stdoutLogFile**(**stdoutLogFile** 섹션 참조)에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="b61d9-134">**stdoutLogFile**(기본값 = "d:\home\LogFiles\httpPlatformStdout.log"). **processPath**에 지정된 프로세스의 **stdout** 및 **stderr**가 로깅될 절대 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="b61d9-135">`%HTTP_PLATFORM_PORT%`는 **arguments**의 일부 또는 **httpPlatform** **environmentVariables** 목록의 일부로 지정해야 하는 특수 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="b61d9-136">이 자리 표시자는 **HttpPlatformHandler**에서 내부적으로 생성한 포트로 대체되므로 **processPath**에서 지정한 프로세스가 이 포트에서 수신 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="b61d9-137">배포</span><span class="sxs-lookup"><span data-stu-id="b61d9-137">Deployment</span></span>
<span data-ttu-id="b61d9-138">Java 기반 웹 앱은 IIS(인터넷 정보 서비스) 기반 웹 응용 프로그램에서 사용하는 것과 대부분 동일한 방법을 통해 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="b61d9-139">FTP, Git 및 Kudu는 모두 배포 메커니즘으로 지원되며, 웹 앱의 통합 SCM 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="b61d9-140">WebDeploy는 프로토콜로 작동하지만 Visual Studio에서 Java를 개발하지 않으므로 WebDeploy는 Java 웹 앱 배포 사용 사례로 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="b61d9-141">응용 프로그램 구성 예제</span><span class="sxs-lookup"><span data-stu-id="b61d9-141">Application configuration Examples</span></span>
<span data-ttu-id="b61d9-142">다음 응용 프로그램에 대해 앱 서비스 웹 앱에서 Java 응용 프로그램을 사용하도록 설정하는 방법을 보여 주는 예제로 web.config 파일 및 응용 프로그램 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="b61d9-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="b61d9-143">Tomcat</span></span>
<span data-ttu-id="b61d9-144">앱 서비스 웹 앱과 함께 제공되는 Tomcat에는 두 가지 변형이 있지만 Tomcat에서는 계속 고객별 인스턴스를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="b61d9-145">다음은 다른 JVM(Java Virtual Machine)으로 Tomcat을 설치한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="b61d9-146">Tomcat 쪽에서 변경해야 할 몇 가지 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="b61d9-147">다음을 설정하도록 server.xml을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="b61d9-148">종료 포트 = -1</span><span class="sxs-lookup"><span data-stu-id="b61d9-148">Shutdown port = -1</span></span>
* <span data-ttu-id="b61d9-149">HTTP 커넥터 포트 = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="b61d9-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="b61d9-150">HTTP 커넥터 주소 = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="b61d9-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="b61d9-151">HTTPS 및 AJP 커넥터를 주석으로 처리</span><span class="sxs-lookup"><span data-stu-id="b61d9-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="b61d9-152">또한 `java.net.preferIPv4Stack=true`를 추가할 수 있는 catalina.properties 파일에서 IPv4 설정도 지정할 수 있음</span><span class="sxs-lookup"><span data-stu-id="b61d9-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="b61d9-153">Direct3d 호출은 앱 서비스 웹 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="b61d9-154">이러한 호출을 사용하지 않도록 설정하려면 응용 프로그램에서 해당 호출을 수행하는 다음 Java 옵션을 추가합니다. `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="b61d9-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="b61d9-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="b61d9-155">Jetty</span></span>
<span data-ttu-id="b61d9-156">Tomcat의 경우와 마찬가지로 고객이 고유한 Jetty 인스턴스를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="b61d9-157">Jetty의 전체 설치를 실행하는 경우 구성은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="b61d9-158">start.ini에서 `java.net.preferIPv4Stack=true`를 설정하도록 Jetty 구성을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="b61d9-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="b61d9-159">Springboot</span></span>
<span data-ttu-id="b61d9-160">Springboot 응용 프로그램을 실행하려면 JAR 또는 WAR 파일을 업로드하고 다음 web.config 파일을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="b61d9-161">web.config 파일은 wwwroot 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="b61d9-162">web.config에서 인수가 JAR 파일을 가리키도록 조정합니다. 다음 예제에서 JAR 파일은 wwwroot 폴더에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="b61d9-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="b61d9-163">Hudson</span></span>
<span data-ttu-id="b61d9-164">이 테스트에서는 구성을 설정하는 데 Hudson 3.1.2 war 및 기본 Tomcat 7.0.50 인스턴스를 사용하지만 UI는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="b61d9-165">Hudson이 소프트웨어 빌드 도구이므로 웹 앱에서 **AlwaysOn** 플래그를 설정할 수 있는 전용 인스턴스에 Hudson을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="b61d9-166">**d:\home\site\wwwroot**와 같이 웹앱의 루트 디렉토리에서 **webapps** 디렉토리를 만들고(디렉토리가 없는 경우), Hudson.war을 **d:\home\site\wwwroot\webapps**에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="b61d9-167">Apache Maven 3.0.5(Hudson과 호환됨)를 다운로드하여 **d:\home\site\wwwroot**에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="b61d9-168">**d:\home\site\wwwroot**에서 web.config를 만들어 다음 내용을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="b61d9-169">이제 웹 앱을 다시 시작하여 변경 내용을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="b61d9-170">http://yourwebapp/hudson에 연결하여 Hudson을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="b61d9-171">Hudson에서 자체 구성을 완료하면 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="b61d9-173">Hudson 구성 페이지에 액세스합니다. **Manage Hudson**을 클릭한 다음 **시스템 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="b61d9-174">아래와 같이 JDK를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-174">Configure the JDK as shown below:</span></span>
   
    ![Hudson 구성](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="b61d9-176">아래와 같이 Maven을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-176">Configure Maven as shown below:</span></span>
   
    ![Maven 구성](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="b61d9-178">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-178">Save the settings.</span></span> <span data-ttu-id="b61d9-179">Hudson을 구성하였으므로 이제 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="b61d9-180">Hudson에 대한 자세한 내용은 [http://hudson-ci.org](http://hudson-ci.org)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b61d9-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="b61d9-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="b61d9-181">Liferay</span></span>
<span data-ttu-id="b61d9-182">Liferay는 앱 서비스 웹 앱에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="b61d9-183">Liferay에 상당한 메모리가 필요할 수 있으므로, 충분한 메모리를 제공할 수 있는 중대형 전용 작업자에서 웹 앱을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="b61d9-184">또한 Liferay는 시작하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="b61d9-185">이런 이유로 웹 앱을 **Always On**으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="b61d9-186">Liferay를 다운로드한 후에 Tomcat과 함께 제공되는 Liferay 6.1.2 Community Edition GA3을 사용하여 다음 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="b61d9-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="b61d9-187">**Server.xml**</span></span>

* <span data-ttu-id="b61d9-188">종료 포트를 -1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="b61d9-189">HTTP 커넥터를 `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="b61d9-190">AJP 커넥터를 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="b61d9-191">**liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** 폴더에서 이름이 **portal-ext.properties**인 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="b61d9-192">이 파일에 다음과 같은 줄을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="b61d9-193">tomcat-7.0.40 폴더와 동일한 디렉터리 수준에서 다음 내용을 포함한 **web.config** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="b61d9-194">**httpPlatform** 블록 아래에 **requestTimeout**이 “00:10:00”으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="b61d9-195">해당 시간을 줄일 수 있지만 그러면 Liferay가 부트스트랩하는 동안 시간 제한 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="b61d9-196">이 값을 변경하면 Tomcat server.xml의 **connectionTimeout** 도 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="b61d9-197">위의 web.config에서는 JRE_HOME 환경 변수가 64비트 JDK를 가리키도록 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="b61d9-198">기본값은 32비트지만 Liferay에 상당한 수준의 메모리가 필요할 수 있으므로 64비트 JDK를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="b61d9-199">이러한 내용을 변경하면 Liferay를 실행하는 웹앱을 다시 시작한 후 http://yourwebapp을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="b61d9-200">Liferay 포털은 웹 앱 루트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b61d9-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b61d9-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b61d9-201">Next steps</span></span>
<span data-ttu-id="b61d9-202">Liferay에 대한 자세한 내용은 [http://www.liferay.com](http://www.liferay.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b61d9-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="b61d9-203">Java에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b61d9-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure 앱 서비스]: http://go.microsoft.com/fwlink/?LinkId=529714
