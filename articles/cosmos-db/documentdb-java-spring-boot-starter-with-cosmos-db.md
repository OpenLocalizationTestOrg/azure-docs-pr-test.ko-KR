---
title: "Azure DB Cosmos DocumentDB API에서 Spring Boot Starter를 사용하는 방법"
description: "Azure Cosmos DB DocumentDB API에서 Spring Boot Initializer를 사용하여 만든 응용 프로그램을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 273cc750857c5e466882060a38ac0f3475811e98
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Azure DB Cosmos DocumentDB API에서 Spring Boot Starter를 사용하는 방법

## <a name="overview"></a>개요

**[Spring Framework]**는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다. 해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다. Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다. 기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]**를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.

Azure Cosmos DB는 개발자가 DocumentDB, MongoDB, Graph 및 Table API와 같은 표준 API를 사용하여 데이터를 사용할 수 있도록 하는 전역 분산 데이터베이스 서비스입니다. Microsoft의 Spring Boot Starter를 사용하면 개발자가 DocumentDB API를 사용하여 Azure Cosmos DB와 쉽게 통합하는 Spring Boot 응용 프로그램을 사용할 수 있습니다.

이 문서에서는 Azure Portal을 사용하여 Azure Cosmos DB를 만들고, **Spring Initializr**를 사용하여 사용자 지정 java 응용 프로그램을 만들고, Spring Boot Starter 기능을 사용자 지정 응용 프로그램에 추가하여 데이터를 저장하고 DocumentDB API를 사용하여 Azure Cosmos DB에서 데이터를 검색하는 방법을 보여줍니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.

* [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상

* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Azure Portal을 사용하여 Azure Cosmos DB 만들기

1. <https://portal.azure.com/>의 Azure Portal로 이동하고 **+새로 만들기**를 클릭합니다.

   ![Azure portal][AZ01]

1. **데이터베이스**를 클릭한 후 **Azure Cosmos DB**를 클릭합니다.

   ![Azure portal][AZ02]

1. **Azure Cosmos DB** 페이지에서 다음 정보를 입력합니다.

   * 고유한 **ID**를 입력합니다. 이 항목은 데이터베이스의 URI로 사용합니다. 예: *wingtiptoysdata.documents.azure.com*
   * API에 **SQL(Document DB)**을 선택합니다.
   * 데이터베이스에 사용하려는 **구독**을 선택합니다.
   * 데이터베이스에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.
   * 데이터베이스의 **위치**를 지정합니다.
   
   이러한 옵션을 지정한 경우 **만들기**를 클릭하여 데이터베이스를 만듭니다.

   ![Azure portal][AZ03]

1. 데이터베이스를 만든 경우 Azure **대시보드** 뿐 아니라 **모든 리소스** 및 **Azure Cosmos DB** 페이지에도 나열됩니다. 해당 위치 중 하나에서 데이터베이스를 클릭하여 캐시에 대한 속성 페이지를 열 수 있습니다.

   ![Azure portal][AZ04]

1. 데이터베이스에 대한 속성 페이지가 표시되면 **액세스 키**를 클릭하고 데이터베이스에 대한 URI 및 액세스 키를 복사합니다. 이러한 값은 Spring Boot 응용 프로그램에서 사용하게 됩니다.

   ![Azure portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Spring Initializr를 사용하여 간단한 Spring Boot 응용 프로그램 만들기

1. <https://start.spring.io/>로 이동합니다.

1. **Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 **프로젝트를 생성**하는 단추를 클릭합니다.

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.example.wintiptoys*).
   >

1. 메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI02]

1. 로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 응용 프로그램을 편집할 준비를 합니다.

   ![사용자 지정 Spring Boot 프로젝트 파일][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Azure Spring Boot Starter를 사용하도록 Spring Boot 앱 구성

1. 앱의 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   또는

   `/users/example/home/wingtiptoys/pom.xml`

   ![pom.xml 파일 찾기][PM01]

1. 텍스트 편집기에서 *pom.xml* 파일을 열고 다음 줄을 `<dependencies>` 목록에 추가합니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![pom.xml 파일 편집][PM02]

1. *pom.xml* 파일을 저장하고 닫습니다.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Azure Cosmos DB를 사용하도록 Spring Boot 앱 구성

1. 앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾습니다.

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   또는

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![application.properties 파일 찾기][RE01]

1. 텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 데이터베이스의 적절한 속성으로 바꿉니다.

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![application.properties 파일 편집][RE02]

1. *application.properties* 파일을 저장하고 닫습니다.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>기본 데이터베이스 기능을 구현하는 샘플 코드 추가

이 섹션에서는 사용자 데이터 저장을 위해 두 가지 Java 클래스를 만든 다음, 기본 응용 프로그램 클래스를 수정하여 사용자 클래스의 인스턴스를 만들고 데이터베이스에 저장합니다.

### <a name="define-a-basic-class-for-storing-user-data"></a>사용자 데이터를 저장하기 위한 기본 클래스 정의

1. 기본 응용 프로그램 Java 파일과 동일한 디렉터리에 *User.java*라는 새 파일을 만듭니다.

1. 텍스트 편집기에서 *User.java* 파일을 다음 줄을 파일에 추가하여 데이터베이스에서 값을 저장하고 검색하는 일반 사용자 클래스를 정의합니다.

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

1. *User.java* 파일을 저장하고 닫습니다.

### <a name="define-a-data-repository-interface"></a>데이터 리포지토리 인터페이스 정의

1. 기본 응용 프로그램 Java 파일과 동일한 디렉터리에 *UserRepository.java*라는 새 파일을 만듭니다.

1. 텍스트 편집기에서 *UserRepository.java* 파일을 열고 파일에 다음 줄을 추가하여 기본 DocumentDB 리포지토리 인터페이스를 확장하는 사용자 리포지토리 인터페이스를 정의합니다.

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. *UserRepository.java* 파일을 저장하고 닫습니다.

### <a name="modify-the-main-application-class"></a>기본 응용 프로그램 클래스 수정

1. 앱의 패키지 디렉터리에서 기본 응용 프로그램 Java 파일을 찾습니다. 예:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   또는

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![응용 프로그램 Java 파일 찾기][JV01]

1. 텍스트 편집기에서 응용 프로그램 Java 파일을 열고 다음 줄을 파일에 추가합니다.

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

1. 기본 응용 프로그램 Java 파일을 저장하고 닫습니다.

## <a name="build-and-test-your-app"></a>앱 빌드 및 테스트

1. 명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:

   `cd C:\SpringBoot\wingtiptoys`

   또는

   `cd /users/example/home/wingtiptoys`

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. 응용 프로그램에 여러 런타임 메시지가 표시되고 `User: testFirstName testLastName` 메시지가 표시되어 값을 성공적으로 저장하고 데이터베이스에서 검색했음을 나타내야 합니다.

   ![응용 프로그램에서 성공적인 출력][JV02]

1. 선택 사항: 콘텐츠를 보기 위해 **문서 탐색기**를 클릭하고 표시된 목록에서 항목을 선택하여 데이터베이스의 속성 페이지에서 Azure Cosmos DB의 콘텐츠를 보도록 Azure Portal을 사용할 수 있습니다.

   ![문서 탐색기를 사용하여 데이터 보기][JV03]

## <a name="next-steps"></a>다음 단계

Azure Cosmos DB 및 Java를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Cosmos DB 설명서]

* [Azure Cosmos DB: Java 및 Azure Portal에서 DocumentDB API 앱 빌드][Build a DocumentDB API app with Java]

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure의 Spring Boot DocumenDB Starter](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Azure App Service에 Spring Boot 응용 프로그램 배포](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

<!-- URL List -->

[Azure Cosmos DB 설명서]: /azure/cosmos-db/
[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
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
