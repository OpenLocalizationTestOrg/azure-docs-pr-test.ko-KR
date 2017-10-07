---
title: "aaaHow tooconfigure 스프링 부팅 이니셜라이저 앱 toouse Redis 캐시"
description: "어떻게 tooconfigure는 스프링 부팅 응용 프로그램을 만들 hello 스프링 Initializr toouse Azure Redis Cache에 알아봅니다."
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
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>어떻게 tooconfigure 스프링 부팅 이니셜라이저 앱 toouse Redis 캐시

## <a name="overview"></a>개요

hello  **[Spring Framework]**  은 오픈 소스 솔루션으로는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 됩니다. 빌드되는 hello 더 이상 인기 있는 프로젝트의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 간단한 방법을 제공 하는 합니다. 스프링 부팅 toohelp 개발자 시작, 몇 가지 샘플 스프링 부팅 패키지에서 사용할 수 있는 <https://github.com/spring-guides/>합니다. 또한 toochoosing 기본 스프링 부팅 hello 목록에서 프로젝트, hello  **[스프링 Initializr]**  스프링 부팅의 사용자 지정 응용 프로그램을 만드는 것부터 시작 하는 개발자는 데 도움이 됩니다.

이 문서에서는 hello hello를 사용 하 여 Azure 포털을 사용 하 여 Redis 캐시를 만드는 과정 **스프링 Initializr** toocreate 사용자 지정 응용 프로그램을 만들고 난 후 Java 웹 응용 프로그램 저장 하 고 사용 하 여 데이터를 검색 하 여 Redis 캐시 합니다.

## <a name="prerequisites"></a>필수 조건

필수 구성 요소를 다음 hello 순서 toofollow hello이이 문서의 단계에 필요 합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.

* [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상

* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-a-redis-cache-on-azure"></a>Azure에 Redis 캐시 만들기

1. 찾아보기 toohello Azure 포털에서 <https://portal.azure.com/> hello 항목에 대 한 클릭 **+ 새로 만들기**합니다.

   ![Azure portal][AZ01]

1. **데이터베이스**를 클릭하고 **Redis Cache**를 클릭합니다.

   ![Azure portal][AZ02]

1. Hello에 **새 Redis 캐시** 페이지에서 입력 hello **DNS 이름** 캐시에서 지정 하면 **구독**, **리소스 그룹**,  **위치**, 및 **가격 책정 계층**합니다. 이러한 옵션을 지정한 경우 클릭 **만들기** toocreate 캐시 합니다.

   ![Azure portal][AZ03]

1. 캐시 완료 되 면 Azure에 나열 볼 수 있습니다 **대시보드**뿐만 아니라 hello 아래에서 **모든 리소스**, 및 **Redis 캐시** 페이지입니다. 캐시에 대 한 모든 해당 위치 tooopen hello 속성 페이지에서 캐시를 클릭할 수 있습니다.

   ![Azure portal][AZ04]

1. Hello 캐시에 대 한 속성 목록이 포함 된 hello 페이지가 표시 되 면 클릭 **선택키가** 캐시에 대 한 액세스 키를 복사 합니다.

   ![Azure portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>스프링 Initializr hello를 사용 하 여 사용자 지정 응용 프로그램 만들기

1. 너무 찾아보기<https://start.spring.io/>합니다.

1. Toogenerate 되도록 지정 된 **Maven** 프로젝트를 **Java**, hello 입력 **그룹** 및 **Aritifact** 응용 프로그램에 대 한 이름 다음 링크를 클릭 hello 너무**스위치 toohello 정식 버전** hello 스프링 Initializr의 합니다.

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > 스프링 Initializr hello hello ´ ֲ **그룹** 및 **Aritifact** 이름 toocreate hello 패키지 이름; 예를 들면: *com.contoso.myazuredemo*합니다.
   >

1. Toohello 아래로 스크롤하여 **웹** 섹션 및에 대 한 hello 확인란 **웹**, toohello 아래로 스크롤한 **NoSQL** 섹션 및에 대 한 hello 확인란 **Redis**, 한 다음 hello 페이지의 맨 아래 toohello 스크롤하여 너무 hello 단추 클릭**프로젝트 생성**합니다.

   ![전체 Spring Initializr 옵션][SI02]

1. 메시지가 표시 되 면 hello 프로젝트 tooa 경로 로컬 컴퓨터에 다운로드 합니다.

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI03]

1. 로컬 시스템에 hello 파일, 압축을 푼 후 사용자 지정 스프링 부팅 응용 프로그램 편집을 위해 수 있습니다.

   ![사용자 지정 Spring Boot 프로젝트 파일][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>사용자 지정 프로그램 스프링 부팅 toouse Redis 캐시 구성

1. Hello 찾을 *application.properties* hello에 대 한 파일 *리소스* 응용 프로그램의 디렉터리 또는 존재 하지 않는 경우 hello 파일을 만들 합니다.

   ![Hello application.properties 파일 찾기][RE01]

1. 열기 hello *application.properties* 텍스트 편집기에서 파일을 다음 줄 toohello 파일 hello를 추가 하 고 캐시에서 적절 한 속성을 hello hello 샘플 값으로 바꾸십시오.

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Hello application.properties 파일 편집][RE02]

1. 저장 후 닫기 hello *application.properties* 파일입니다.

1. 라는 폴더를 만듭니다 *컨트롤러* 패키지;에 대 한 원본 폴더 hello 예:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   또는

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. 라는 새 파일을 만들어 *HelloController.java* hello에 *컨트롤러* 폴더입니다. 텍스트 편집기에서 hello 파일을 열고 다음 코드 tooit hello를 추가 합니다.

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   Tooreplace 할 `com.contoso.myazuredemo` 프로젝트에 대 한 hello 패키지 이름을 사용 합니다.

1. 저장 후 닫기 hello *HelloController.java* 파일입니다.

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Toohttp://localhost:8080 웹 브라우저를 사용 하 여 검색 하 여 hello 웹 앱을 테스트 하거나 hello curl을 사용할 수 있는 경우 다음 예제에서는 같은 hello 구문을 사용 합니다.

   ```shell
   curl http://localhost:8080
   ```

   "Hello World!" hello를 나타나야 합니다. 메시지가 표시되어야 합니다. 이 메시지는 Redis Cache에서 동적으로 검색됩니다.

## <a name="next-steps"></a>다음 단계

Azure에서 스프링 부팅 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램을 실행합니다.](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.

가져오기에 대 한 자세한 내용은 참조 Redis Cache를 사용 하 여 Azure에서 Java를 통해 시작 [toouse Azure Redis 캐시 방법 Java와 함께][Redis Cache with Java]합니다.

<!-- URL List -->

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
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
