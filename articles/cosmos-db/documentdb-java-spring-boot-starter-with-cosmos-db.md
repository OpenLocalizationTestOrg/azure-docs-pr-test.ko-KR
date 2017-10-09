---
title: "aaaHow toouse hello Azure Cosmos DB DocumentDB API가 있는 스프링 부팅 시작"
description: "어떻게 tooconfigure는 응용 프로그램을 만들 hello Azure Cosmos DB DocumentDB API로 hello 스프링 부팅 이니셜라이저에 알아봅니다."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="2d940-104">어떻게 toouse hello Azure Cosmos DB DocumentDB api 스프링 부팅 시작</span><span class="sxs-lookup"><span data-stu-id="2d940-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="2d940-105">개요</span><span class="sxs-lookup"><span data-stu-id="2d940-105">Overview</span></span>

<span data-ttu-id="2d940-106">hello  **[Spring Framework]**  은 오픈 소스 솔루션으로 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="2d940-107">만들어지는 hello 더 이상 인기 있는 프로젝트 중 하나의 플랫폼은 [스프링 부팅], 독립 실행형 Java 응용 프로그램을 만들기 위한 간단한 방법을 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="2d940-108">스프링 부팅 toohelp 개발자 시작, 몇 가지 샘플 스프링 부팅 패키지에서 사용할 수 있는 <https://github.com/spring-guides/>합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="2d940-109">또한 toochoosing 기본 스프링 부팅 hello 목록에서 프로젝트, hello  **[스프링 Initializr]**  스프링 부팅의 사용자 지정 응용 프로그램을 만드는 것부터 시작 하는 개발자는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="2d940-110">Azure Cosmos DB는 개발자가 사용할 수 있는 전역으로 분산 데이터베이스 서비스 toowork 다양 한 DocumentDB, MongoDB, 그래프 및 테이블 Api와 같은 표준 Api 사용 하 여 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="2d940-111">Microsoft의 스프링 부팅 시작 DocumentDB Api를 사용 하 여 Azure Cosmos DB와 쉽게 통합 하는 개발자가 toouse 스프링 부팅 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="2d940-112">이 문서는 Azure Cosmos DB hello Azure 포털을 사용 하 여 hello를 사용 하 여 다음을 만드는 방법을 보여 **스프링 Initializr** toocreate 사용자 지정 java 응용 프로그램을 다음 hello 스프링 부팅 시작 기능 tooyour 사용자 정의 추가 응용 프로그램 toostore 데이터와 데이터 hello DocumentDB API를 사용 하 여 Azure Cosmos DB를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d940-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d940-113">Prerequisites</span></span>

<span data-ttu-id="2d940-114">필수 구성 요소를 다음 hello 순서 toofollow hello이이 문서의 단계에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="2d940-115">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="2d940-116">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="2d940-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="2d940-117">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="2d940-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="2d940-118">Hello Azure 포털을 사용 하 여 Azure Cosmos DB 만들기</span><span class="sxs-lookup"><span data-stu-id="2d940-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="2d940-119">찾아보기 toohello Azure 포털에서 <https://portal.azure.com/> 클릭 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure portal][AZ01]

1. <span data-ttu-id="2d940-121">**데이터베이스**를 클릭한 후 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure portal][AZ02]

1. <span data-ttu-id="2d940-123">Hello에 **Azure Cosmos DB** 페이지 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="2d940-124">고유한 입력 **ID**, 데이터베이스에 대 한 URI를 hello으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="2d940-125">예: *wingtiptoysdata.documents.azure.com*</span><span class="sxs-lookup"><span data-stu-id="2d940-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="2d940-126">선택 **SQL (문서 DB)** hello API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="2d940-127">Hello 선택 **구독** toouse 데이터베이스에 대 한 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="2d940-128">지정 여부 새 toocreate **리소스 그룹** 프로그램 데이터베이스에 대 한 하거나 기존 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="2d940-129">Hello 지정 **위치** 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="2d940-130">이러한 옵션을 지정한 경우 클릭 **만들기** toocreate 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure portal][AZ03]

1. <span data-ttu-id="2d940-132">데이터베이스를 만든 경우 Azure에 나열 됩니다 **대시보드**뿐만 아니라 hello 아래에서 **모든 리소스** 및 **Azure Cosmos DB** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="2d940-133">캐시에 대 한 해당 위치 tooopen hello 속성 페이지 중 하나에서 해당 데이터베이스를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure portal][AZ04]

1. <span data-ttu-id="2d940-135">데이터베이스에 대 한 hello 속성 페이지를 표시할 때 클릭 **선택키가** 데이터베이스에 대 한 URI 및 액세스 키를 복사 하 고 스프링 부팅 응용 프로그램에서 이러한 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="2d940-137">스프링 Initializr hello로 간단한 스프링 부팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2d940-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="2d940-138">너무 찾아보기<https://start.spring.io/>합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="2d940-139">Toogenerate 되도록 지정 된 **Maven** 프로젝트를 **Java**, hello 입력 **그룹** 및 **아티팩트** 응용 프로그램에 대 한 이름 및 클릭 한 다음 너무 hello 단추**프로젝트 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="2d940-141">스프링 Initializr hello hello를 사용 하 여 **그룹** 및 **아티팩트** 이름 toocreate hello 패키지 이름; 예를 들면: *com.example.wintiptoys*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="2d940-142">메시지가 표시 되 면 hello 프로젝트 tooa 경로 로컬 컴퓨터에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI02]

1. <span data-ttu-id="2d940-144">로컬 시스템에 hello 파일, 압축을 푼 후 간단한 스프링 부팅 응용 프로그램 편집을 위해 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="2d940-146">스프링 부팅 앱 toouse hello Azure 스프링 부팅 시작 구성</span><span class="sxs-lookup"><span data-stu-id="2d940-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="2d940-147">Hello 찾을 *pom.xml* ; 응용 프로그램의 hello 디렉터리에에서 파일의 예:</span><span class="sxs-lookup"><span data-stu-id="2d940-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="2d940-148">또는</span><span class="sxs-lookup"><span data-stu-id="2d940-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Hello pom.xml 파일 찾기][PM01]

1. <span data-ttu-id="2d940-150">열기 hello *pom.xml* 텍스트 편집기에서 파일을 추가 뒤의 줄 toolist hello `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="2d940-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Hello pom.xml 파일 편집][PM02]

1. <span data-ttu-id="2d940-152">저장 후 닫기 hello *pom.xml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="2d940-153">스프링 부팅 앱 toouse Azure Cosmos DB 구성</span><span class="sxs-lookup"><span data-stu-id="2d940-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="2d940-154">Hello 찾을 *application.properties* hello에 대 한 파일 *리소스* 응용 프로그램의 디렉터리 예:</span><span class="sxs-lookup"><span data-stu-id="2d940-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="2d940-155">또는</span><span class="sxs-lookup"><span data-stu-id="2d940-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Hello application.properties 파일 찾기][RE01]

1. <span data-ttu-id="2d940-157">열기 hello *application.properties* 파일 텍스트 편집기에서 다음 줄 toohello 파일 hello를 추가 하 고 데이터베이스에 대 한 적절 한 속성을 hello hello 샘플 값으로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="2d940-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Hello application.properties 파일 편집][RE02]

1. <span data-ttu-id="2d940-159">저장 후 닫기 hello *application.properties* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="2d940-160">샘플 코드 tooimplement 기본 데이터베이스 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="2d940-161">이 섹션의 사용자 데이터를 저장 하기 위한 두 개의 Java 클래스 만들고 주 응용 프로그램 클래스 toocreate hello 사용자 클래스의 인스턴스를 수정 하 고 tooyour 데이터베이스를 저장 하는 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="2d940-162">사용자 데이터를 저장하기 위한 기본 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="2d940-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="2d940-163">라는 새 파일을 만들어 *User.java* hello에 기본 응용 프로그램 Java 파일과 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="2d940-164">열기 hello *User.java* 텍스트 편집기에서 파일을 hello 다음 줄 toohello 파일 toodefine 저장 하 고 데이터베이스에서 값을 검색 하는 일반 사용자 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="2d940-165">저장 후 닫기 hello *User.java* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="2d940-166">데이터 리포지토리 인터페이스 정의</span><span class="sxs-lookup"><span data-stu-id="2d940-166">Define a data repository interface</span></span>

1. <span data-ttu-id="2d940-167">라는 새 파일을 만들어 *UserRepository.java* hello에 기본 응용 프로그램 Java 파일과 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="2d940-168">열기 hello *UserRepository.java* 텍스트 편집기에서 파일을 hello 다음 줄 toohello 파일 toodefine hello 기본 DocumentDB 리포지토리 인터페이스를 확장 하는 사용자 리포지토리 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="2d940-169">저장 후 닫기 hello *UserRepository.java* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="2d940-170">Hello 주 응용 프로그램 클래스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-170">Modify hello main application class</span></span>

1. <span data-ttu-id="2d940-171">응용 프로그램;의 hello 패키지 디렉터리에서 hello 주 응용 프로그램 Java 파일 찾기 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="2d940-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="2d940-172">또는</span><span class="sxs-lookup"><span data-stu-id="2d940-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Hello 응용 프로그램이 Java 파일 찾기][JV01]

1. <span data-ttu-id="2d940-174">텍스트 편집기에서 hello 기본 응용 프로그램 Java 파일을 열고 다음 줄 toohello 파일 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="2d940-175">저장 하 고 hello 기본 응용 프로그램 Java 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="2d940-176">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2d940-176">Build and test your app</span></span>

1. <span data-ttu-id="2d940-177">명령 프롬프트를 열고 디렉터리 toohello 폴더 변경 위치 프로그램 *pom.xml* 파일은 예:</span><span class="sxs-lookup"><span data-stu-id="2d940-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="2d940-178">또는</span><span class="sxs-lookup"><span data-stu-id="2d940-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="2d940-179">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="2d940-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="2d940-180">응용 프로그램에 여러 런타임 메시지에 표시 되 고 hello 메시지를 확인 해야 `User: testFirstName testLastName` tooindicate 있는지 값 성공적으로 저장 되어 데이터베이스에서 검색을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Hello 응용 프로그램에서 성공적으로 출력][JV02]

1. <span data-ttu-id="2d940-182">선택 사항: 사용할 수 있습니다 프로그램 Azure Cosmos DB hello 속성 페이지에서의 hello Azure 포털 tooview hello 내용을 데이터베이스에 대 한 클릭 하 여 **Document Explorer**, 다음을 선택 하 고 항목을 표시 하는 hello 목록 tooview hello에서 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![사용 하 여 hello Document Explorer tooview 데이터][JV03]

## <a name="next-steps"></a><span data-ttu-id="2d940-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d940-184">Next steps</span></span>

<span data-ttu-id="2d940-185">Cosmos DB Azure 및 Java를 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="2d940-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="2d940-186">[Azure Cosmos DB 설명서]</span><span class="sxs-lookup"><span data-stu-id="2d940-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="2d940-187">[Azure Cosmos DB: Java 통해 DocumentDB API 앱을 빌드하고 hello Azure 포털][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="2d940-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="2d940-188">Azure에서 스프링 부팅 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="2d940-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="2d940-189">Azure의 Spring Boot DocumenDB Starter</span><span class="sxs-lookup"><span data-stu-id="2d940-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="2d940-190">스프링 부팅 응용 프로그램 toohello Azure 앱 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="2d940-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="2d940-191">Hello Azure 컨테이너 서비스의에서 Kubernetes 클러스터에서 스프링 부팅 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="2d940-192">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="2d940-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Cosmos DB 설명서]: /azure/cosmos-db/
[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[스프링 부팅]: http://projects.spring.io/spring-boot/
[스프링 Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
