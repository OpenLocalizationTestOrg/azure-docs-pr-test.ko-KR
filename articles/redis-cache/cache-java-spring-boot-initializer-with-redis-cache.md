---
title: "Redis Cache를 사용하도록 Spring Boot Initializer 앱을 구성하는 방법"
description: "Azure Redis Cache를 사용하도록 Spring Initializer를 사용하여 만든 Spring Boot 응용 프로그램을 구성하는 방법에 대해 알아봅니다."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Redis Cache
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: fb3fc96a2136b7c326bb0eb291b7204e7acf0190
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="e951a-104">Redis Cache를 사용하도록 Spring Boot Initializer 앱을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="e951a-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="e951a-105">개요</span><span class="sxs-lookup"><span data-stu-id="e951a-105">Overview</span></span>

<span data-ttu-id="e951a-106">**[Spring Framework]**는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-106">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e951a-107">해당 플랫폼 맨 위에 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만들기 위한 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-107">One of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e951a-108">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e951a-109">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]**를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="e951a-110">이 문서에서는 Azure Portal을 사용하여 Redis Cache를 만들고, **Spring Initializr**를 사용하여 사용자 지정 응용 프로그램을 만든 다음 Redis Cache를 사용하여 데이터를 저장하고 검색하는 Java 웹 응용 프로그램을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e951a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e951a-111">Prerequisites</span></span>

<span data-ttu-id="e951a-112">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="e951a-113">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="e951a-114">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="e951a-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="e951a-115">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="e951a-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e951a-116">Azure에 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="e951a-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="e951a-117"><https://portal.azure.com/>의 Azure Portal로 이동하고 **+새로 만들기**의 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Azure 포털][AZ01]

1. <span data-ttu-id="e951a-119">**데이터베이스**를 클릭하고 **Redis Cache**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure portal][AZ02]

1. <span data-ttu-id="e951a-121">**새 Redis Cache** 페이지에서 캐시에 **DNS 이름**을 입력하고 **구독**, **리소스 그룹**, **위치** 및 **가격 책정 계층**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-121">On the **New Redis Cache** page, enter the **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="e951a-122">이러한 옵션을 지정한 경우 **만들기**를 클릭하여 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-122">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Azure portal][AZ03]

1. <span data-ttu-id="e951a-124">캐시가 완료되면 Azure **대시보드**뿐만 아니라 **모든 리소스** 및 **Redis Caches** 페이지에서도 나열된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="e951a-125">해당 위치 중 하나에서 캐시를 클릭하여 캐시의 속성 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-125">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Azure portal][AZ04]

1. <span data-ttu-id="e951a-127">캐시의 속성 목록이 포함된 페이지가 표시되면 **액세스 키**를 클릭하고 캐시의 액세스 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-127">When the page which contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure portal][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="e951a-129">Spring Initializr를 사용하여 사용자 지정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e951a-129">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="e951a-130"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-130">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e951a-131">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-131">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e951a-133">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.contoso.myazuredemo*).</span><span class="sxs-lookup"><span data-stu-id="e951a-133">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="e951a-134">**웹** 섹션까지 아래로 스크롤하고 **웹**의 확인란을 선택한 다음 **NoSQL** 섹션까지 아래로 스크롤하고 **Redis**의 확인란을 선택하고 페이지 아래쪽으로 스크롤한 다음 **프로젝트를 생성**하는 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-134">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![전체 Spring Initializr 옵션][SI02]

1. <span data-ttu-id="e951a-136">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-136">When prompted, download the project to a path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI03]

1. <span data-ttu-id="e951a-138">로컬 시스템에서 파일의 압축을 푼 후에 사용자 지정 Spring Boot 응용 프로그램을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-138">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="e951a-140">Redis Cache를 사용하도록 사용자 지정 Spring Boot 구성</span><span class="sxs-lookup"><span data-stu-id="e951a-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="e951a-141">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![application.properties 파일 찾기][RE01]

1. <span data-ttu-id="e951a-143">텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 캐시의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6380

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![application.properties 파일 편집][RE02]

1. <span data-ttu-id="e951a-145">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-145">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="e951a-146">패키지의 소스 폴더 아래에서 *controller*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-146">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="e951a-147">또는</span><span class="sxs-lookup"><span data-stu-id="e951a-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="e951a-148">*컨트롤러* 폴더에 *HelloController.java*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-148">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="e951a-149">텍스트 편집기에서 파일을 열고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-149">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve the DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve the port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve the access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object to connect to your Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object to store/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string to your cache.
         jedis.set("greeting", "Hello World!");

         // Return the string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="e951a-150">여기에서 `com.contoso.myazuredemo`를 프로젝트의 패키지 이름으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-150">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="e951a-151">*HelloController.java* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-151">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="e951a-152">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="e951a-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e951a-153">웹 브라우저를 통해 http://localhost:8080 으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-153">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="e951a-154">샘플 컨트롤러에서 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e951a-154">You should see the "Hello World!"</span></span> <span data-ttu-id="e951a-155">메시지가 표시되어야 합니다. 이 메시지는 Redis Cache에서 동적으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="e951a-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e951a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e951a-156">Next steps</span></span>

<span data-ttu-id="e951a-157">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e951a-157">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e951a-158">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e951a-158">Deploy a Spring Boot Application to the Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="e951a-159">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e951a-159">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="e951a-160">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e951a-160">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e951a-161">Azure에서 Java로 Redis Cache를 시작하는 방법에 대한 자세한 내용은 [Java에서 Azure Redis Cache를 사용하는 방법][Redis Cache with Java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e951a-161">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

<span data-ttu-id="e951a-162">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="e951a-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="e951a-163">[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="e951a-163">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="e951a-164">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e951a-164">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="e951a-165">[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="e951a-165">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="e951a-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="e951a-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="e951a-167">[Spring Initializr]: https://start.spring.io/</span><span class="sxs-lookup"><span data-stu-id="e951a-167">[Spring Initializr]: https://start.spring.io/</span></span>
<span data-ttu-id="e951a-168">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="e951a-168">[Spring Framework]: https://spring.io/</span></span>
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
