---
title: "aaaAzure AD Java 명령줄 시작 | Microsoft Docs"
description: "어떻게 toobuild Java tooaccess API의에서 사용자가 서명 하는 줄 앱을 명령입니다."
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
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="9c03b-103">Java 명령줄 응용 프로그램 tooAccess API를 사용 하 여 Azure AD와</span><span class="sxs-lookup"><span data-stu-id="9c03b-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="9c03b-104">Azure AD는 단순 하 고 간단 toooutsource 웹 앱의 id 관리, single 로그인 및 로그 아웃 코드 몇 줄만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="9c03b-105">Java 웹 응용 프로그램에서 이렇게 되도록 하려면 Microsoft에서 구현한 커뮤니티 기반 ADAL4J hello 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="9c03b-106">다음의 경우 ADAL4J를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="9c03b-107">Hello 사용자 hello id 공급자로 Azure AD를 사용 하 여 hello 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="9c03b-108">Hello 사용자에 대 한 일부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-108">Display some information about hello user.</span></span>
* <span data-ttu-id="9c03b-109">Sign hello hello 앱에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="9c03b-110">이 toodo 순서, 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="9c03b-111">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="9c03b-112">응용 프로그램 toouse hello ADAL4J 라이브러리를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="9c03b-113">Hello ADAL4J 라이브러리 tooissue 로그인 및 로그 아웃 요청 tooAzure AD 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="9c03b-114">Hello 사용자에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-114">Print out data about hello user.</span></span>

<span data-ttu-id="9c03b-115">시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="9c03b-116">어떤 tooregister에 Azure AD 테 넌 트 응용 프로그램 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="9c03b-117">없는 경우 하나 이미 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="9c03b-118">1.  Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="9c03b-119">tooenable 앱 tooauthenticate 사용자가 테 넌 트에 tooregister 새 응용 프로그램을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="9c03b-120">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9c03b-121">Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="9c03b-122">클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9c03b-123">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="9c03b-124">Hello 화면에 따라 수행 하 고 새 **웹 응용 프로그램 및/또는 WebAPI**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="9c03b-125">hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend-사용자가 설명 합니다</span><span class="sxs-lookup"><span data-stu-id="9c03b-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="9c03b-126">hello **로그온 URL** hello 응용 프로그램의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="9c03b-127">hello 스 켈 레 톤의 기본값은 `http://localhost:8080/adal4jsample/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="9c03b-128">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="9c03b-129">이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="9c03b-130">Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="9c03b-131">hello **앱 ID URI** 응용 프로그램에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="9c03b-132">hello 규칙은 toouse `https://<tenant-domain>/<app-name>`, 예: `http://localhost:8080/adal4jsample/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="9c03b-133">한 번 응용 프로그램에 대 한 hello 포털에서 만듭니다는 **키** hello에서 **설정** 응용 프로그램에 대 한 페이지를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="9c03b-134">곧 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="9c03b-135">2. App toouse ADAL4J 라이브러리 및 Maven을 사용 하 여 필수 구성 요소 설정</span><span class="sxs-lookup"><span data-stu-id="9c03b-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="9c03b-136">여기서 ADAL4J toouse hello OpenID Connect 인증 프로토콜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9c03b-137">ADAL4J tooissue 사용 되는 로그인 및 로그 아웃 요청, hello 사용자의 세션을 관리 되며 다른 작업 간에 hello 사용자에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="9c03b-138">프로젝트의 루트 디렉터리를 hello 열거나 만들 `pom.xml` hello 찾습니다 `// TODO: provide dependencies for Maven` hello 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="9c03b-139">3. Hello Java PublicClient 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9c03b-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="9c03b-140">앞서 설명한 대로 hello hello 로그인 한 사용자에 대 한 Graph API tooget 데이터 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="9c03b-141">이 toobe 우리 쉽게에 대해 두 파일 toorepresent 만들어야 우리는 **디렉터리 개체** 및 개별 파일 toorepresent hello **사용자** hello java 개체 지향 패턴 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="9c03b-142">파일을 만들 `DirectoryObject.java` 있는 toostore 모든 DirectoryObject (있습니다 느낄 수 있으며 무료 toouse이 나중에 작업을 수행할 수 있습니다 다른 그래프 쿼리에)에 대 한 기본 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="9c03b-143">아래에서 잘라내고 붙여 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="9c03b-144">컴파일 및 hello 예제 실행</span><span class="sxs-lookup"><span data-stu-id="9c03b-144">Compile and run hello sample</span></span>
<span data-ttu-id="9c03b-145">Tooyour 루트 디렉터리 외부로 돌려보내는 변경 하 고 다음 명령 toobuild hello 샘플을 사용 하 여 함께 저장 하기만 hello 실행 `maven`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="9c03b-146">이 hello ´ ֲ `pom.xml` 파일 종속성에 대 한 직접 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="9c03b-147">이제 `/targets` 디렉터리에 `adal4jsample.war` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="9c03b-148">Tomcat 컨테이너에는 배포 하 고 hello URL을 방문 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="9c03b-149">것을 매우 쉽게 toodeploy 전쟁 hello 최신 Tomcat 서버와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="9c03b-150">너무 이동한`http://localhost:8080/manager/` 업로드에 hello 지침에 따라 프로그램 ' adal4jsample.war' 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="9c03b-151">드립니다 autodeploy hello 올바른 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9c03b-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c03b-152">Next Steps</span></span>
<span data-ttu-id="9c03b-153">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-153">Congratulations!</span></span> <span data-ttu-id="9c03b-154">이제 정상 작동 hello 기능 tooauthenticate 사용자가 있는 Java 응용 프로그램, 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 하 고 hello 사용자에 대 한 기본 정보를 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="9c03b-155">아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="9c03b-156">참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c03b-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

