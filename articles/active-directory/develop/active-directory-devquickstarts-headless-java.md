---
title: "Azure AD Java 명령줄 시작 | Microsoft Docs"
description: "API 액세스를 위해 사용자를 로그인하는 Java 명령줄 앱을 빌드하는 방법"
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="067bc-103">Azure AD에서 API를 액세스하기 위해 Java 명령줄 앱 사용</span><span class="sxs-lookup"><span data-stu-id="067bc-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="067bc-104">Azure AD를 사용하면 단순하고 간편하게 웹앱의 ID 관리를 아웃소싱하고 몇 개의 코드 줄만으로 단일 로그인 및 로그아웃을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="067bc-105">Java 웹앱에서는 Microsoft에서 구현한 커뮤니티 기반 ADAL4J를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="067bc-106">다음의 경우 ADAL4J를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="067bc-107">ID 공급자로 Azure AD를 사용하여 사용자를 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="067bc-108">사용자에 대한 일부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-108">Display some information about the user.</span></span>
* <span data-ttu-id="067bc-109">앱에서 사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-109">Sign the user out of the app.</span></span>

<span data-ttu-id="067bc-110">이 작업을 수행하려면 다음 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="067bc-111">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="067bc-112">앱을 설정하여 ADAL4J 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="067bc-113">ADAL4J 라이브러리를 사용하여 Azure AD에 로그인 및 로그아웃 요청 실행</span><span class="sxs-lookup"><span data-stu-id="067bc-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="067bc-114">사용자에 대한 데이터를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-114">Print out data about the user.</span></span>

<span data-ttu-id="067bc-115">시작하려면 [앱 기본 사항을 다운로드](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="067bc-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="067bc-116">응용 프로그램을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="067bc-117">테넌트가 아직 없는 경우 [가져오는 방법을 알아봅니다](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="067bc-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="067bc-118">1.  Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="067bc-119">앱에서 사용자를 인증할 수 있게 하려면 먼저 새 응용 프로그램을 테넌트에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="067bc-120">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="067bc-121">오른쪽 위에서 계정을 클릭하고 **디렉터리** 목록에서 응용 프로그램을 등록하려는 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="067bc-122">왼쪽 탐색 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="067bc-123">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="067bc-124">프롬프트에 따라 새 **웹 응용 프로그램 및/또는 WebAPI**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="067bc-125">응용 프로그램의 **이름** 은 최종 사용자에게 응용 프로그램을 설명하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="067bc-126">**로그온 URL** 은 앱의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="067bc-127">기본값은 `http://localhost:8080/adal4jsample/`입니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="067bc-128">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="067bc-129">이 값은 다음 섹션에서 필요하므로 응용 프로그램 탭에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="067bc-130">응용 프로그램에 대한 **설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="067bc-131">**앱 ID URI** 는 응용 프로그램의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="067bc-132">규칙은 `https://<tenant-domain>/<app-name>`(예: `http://localhost:8080/adal4jsample/`)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="067bc-133">앱 포털에서 응용 프로그램의 **설정** 페이지에서 **키**를 만들고 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="067bc-134">곧 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="067bc-135">2. Maven을 사용하여 ADAL4J 라이브러리 및 필수 구성 요소를 사용하도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="067bc-136">여기서는 OpenID Connect 인증 프로토콜을 사용하도록 ADAL4J를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="067bc-137">ADAL4J은 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하고, 사용자에 대한 정보를 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="067bc-138">프로젝트의 루트 디렉터리에서 `pom.xml`을 열거나 만들고 `// TODO: provide dependencies for Maven`를 찾아서 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="067bc-139">3. Java PublicClient 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="067bc-140">앞서 설명한 대로 Graph API를 사용하여 로그인한 사용자에 대한 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="067bc-141">이 작업을 쉽게 수행하려면 Java의 OO 패턴을 사용할 수 있도록 **디렉터리 개체**를 나타내는 파일과 **사용자**를 나타내는 개별 파일을 모두 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="067bc-142">DirectoryObject에 대한 기본 데이터를 저장하는 데 사용하는 `DirectoryObject.java`라는 파일을 만듭니다.(나중에 수행할 수 있는 다른 Graph 쿼리에 이 파일을 자유롭게 사용할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="067bc-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="067bc-143">아래에서 잘라내고 붙여 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="067bc-144">샘플 컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="067bc-144">Compile and run the sample</span></span>
<span data-ttu-id="067bc-145">루트 디렉터리로 다시 변경하고 다음 명령을 실행하여 `maven`을 사용하여 모은 샘플을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="067bc-146">여기에는 종속성에 대해 작성한 `pom.xml` 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="067bc-147">이제 `/targets` 디렉터리에 `adal4jsample.war` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="067bc-148">Tomcat 컨테이너에서 해당 파일을 배포하고 URL를 방문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="067bc-149">최신 Tomcat 서버를 사용하여 WAR를 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="067bc-150">`http://localhost:8080/manager/`로 이동하여 'adal4jsample.war' 파일을 업로드하기 위한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="067bc-151">올바른 끝점을 사용하여 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="067bc-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="067bc-152">Next Steps</span></span>
<span data-ttu-id="067bc-153">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-153">Congratulations!</span></span> <span data-ttu-id="067bc-154">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 Java 응용 프로그램이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="067bc-155">아직 일부 사용자로 테넌트를 채우지 않은 경우 지금 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="067bc-156">참조를 위해 완료된 샘플(사용자 구성 값 제외)이 [여기에 .zip으로 제공](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)되거나 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067bc-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

