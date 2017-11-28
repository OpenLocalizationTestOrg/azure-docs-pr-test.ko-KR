---
title: "aaaAzure AD Java 웹 응용 프로그램 시작 | Microsoft Docs"
description: "회사 또는 학교 계정을 사용하여 사용자가 로그인하는 Java 웹앱을 빌드할 수 있습니다."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 2b92b605-9cd5-4b99-bcbb-66c026558119
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 02/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 20ae95914e074507ed1a23966565ba950cc3a9dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="java-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="28125-103">Azure AD에서 Java 웹앱 로그인 및 로그아웃</span><span class="sxs-lookup"><span data-stu-id="28125-103">Java web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="28125-104">로그인 및 로그 아웃 하는 단일 단 몇 줄의 코드를 제공 함으로써 Azure Active Directory (Azure AD) 간단 하 게 하면 toooutsource 웹 응용 프로그램 id 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="28125-105">Hello 커뮤니티 기반 (ADAL4J) Java 용 Azure Active Directory 인증 라이브러리의 Microsoft 구현 hello를 사용 하 여 Java 웹 응용 프로그램 내부 및 외부 사용자가 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-105">You can sign users in and out of Java web apps by using hello Microsoft implementation of hello community-driven Azure Active Directory Authentication Library for Java (ADAL4J).</span></span>

<span data-ttu-id="28125-106">이 문서에서는 toouse를 ADAL4J hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28125-106">This article shows how toouse hello ADAL4J to:</span></span>

* <span data-ttu-id="28125-107">Hello id 공급자로 Azure AD를 사용 하 여 tooweb 앱에서 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-107">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="28125-108">일부 사용자 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-108">Display some user information.</span></span>
* <span data-ttu-id="28125-109">Hello 앱에서 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-109">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="28125-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="28125-110">Before you get started</span></span>

* <span data-ttu-id="28125-111">Hello 다운로드 [앱 스 켈 레 톤](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip), hello 다운로드 또는 [완성 된 샘플](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-111">Download hello [app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip), or download hello [completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>
* <span data-ttu-id="28125-112">어떤 tooregister hello 앱에서 Azure AD 테 넌 트가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-112">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="28125-113">Azure AD 테 넌 트가 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-113">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="28125-114">준비 되 면 hello 다음 9 섹션의 hello 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="28125-114">When you are ready, follow hello procedures in hello next nine sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="28125-115">1 단계: Azure AD와 hello 새 앱 등록</span><span class="sxs-lookup"><span data-stu-id="28125-115">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="28125-116">tooset hello 앱 tooauthenticate 사용자를 처음 등록할 테 넌 트에 hello 다음을 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="28125-116">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="28125-117">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="28125-118">Hello 위쪽 막대에서 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-118">On hello top bar, click your account name.</span></span> <span data-ttu-id="28125-119">Hello에서 **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-119">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="28125-120">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-120">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="28125-121">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-121">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="28125-122">Hello 프롬프트 toocreate에 따라 한 **웹 응용 프로그램 및/또는 WebAPI**합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-122">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="28125-123">**이름** hello 앱 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-123">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="28125-124">**로그온 URL** hello hello 응용 프로그램의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-124">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="28125-125">hello 뼈대 기본 URL은 http://localhost:8080/adal4jsample /.</span><span class="sxs-lookup"><span data-stu-id="28125-125">hello skeleton's default URL is http://localhost:8080/adal4jsample/.</span></span>
6. <span data-ttu-id="28125-126">Azure AD를 hello 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당</span><span class="sxs-lookup"><span data-stu-id="28125-126">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="28125-127">Hello 다음 섹션의 앱 페이지 toouse hello에서에서 hello 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-127">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="28125-128">Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-128">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="28125-129">hello **앱 ID URI** hello 앱에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-129">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="28125-130">hello 명명 규칙은 `https://<tenant-domain>/<app-name>` (예를 들어 `http://localhost:8080/adal4jsample/`).</span><span class="sxs-lookup"><span data-stu-id="28125-130">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `http://localhost:8080/adal4jsample/`).</span></span>

<span data-ttu-id="28125-131">Hello 앱에 대 한 hello 포털에 있는 경우 만들고 hello 응용 프로그램에 액세스 hello에 대 한 키를 복사 **설정을** 페이지.</span><span class="sxs-lookup"><span data-stu-id="28125-131">When you are in hello portal for hello app, create and copy a key for hello app on hello **Settings** page.</span></span> <span data-ttu-id="28125-132">Hello 키를 곧 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-132">You'll need hello key shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-adal4j-and-prerequisites-by-using-maven"></a><span data-ttu-id="28125-133">2 단계: Maven을 사용 하 여 hello 앱 toouse hello ADAL4J 및 필수 구성 요소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-133">Step 2: Set up hello app toouse hello ADAL4J and prerequisites by using Maven</span></span>
<span data-ttu-id="28125-134">이 단계에서는 hello ADAL4J toouse hello OpenID Connect 인증 프로토콜을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-134">In this step, you configure hello ADAL4J toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="28125-135">하면 hello ADAL4J tooissue 로그인 및 로그 아웃 요청을 사용 하 여, 사용자 세션 관리, 사용자 정보 가져오기 등.</span><span class="sxs-lookup"><span data-stu-id="28125-135">You use hello ADAL4J tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

<span data-ttu-id="28125-136">Hello 프로젝트의 루트 디렉터리를 열거나 만들 `pom.xml`, 찾습니다 `// TODO: provide dependencies for Maven`, hello 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28125-136">In hello root directory of your project, open/create `pom.xml`, locate `// TODO: provide dependencies for Maven`, and replace it with hello following:</span></span>

```Java

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4jsample</artifactId>
    <packaging>war</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>adal4jsample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.1</version>
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
        <!-- Spring 3 dependencies -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>sample-for-adal4j</finalName>
        <plugins>
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
                <artifactId>maven-war-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <warName>${project.artifactId}</warName>
                    <source>${project.basedir}\src</source>
                    <target>${maven.compiler.target}</target>
                    <encoding>utf-8</encoding>
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
        </plugins>
    </build>

    </project>
```

## <a name="step-3-create-hello-java-web-app-files-web-inf"></a><span data-ttu-id="28125-137">3 단계: hello Java 웹 응용 프로그램 파일 (웹-INF) 만들기</span><span class="sxs-lookup"><span data-stu-id="28125-137">Step 3: Create hello Java web app files (WEB-INF)</span></span>
<span data-ttu-id="28125-138">이 단계에서는 hello Java 웹 응용 프로그램 toouse hello OpenID Connect 인증 프로토콜을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-138">In this step, you configure hello Java web app toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="28125-139">Hello ADAL4J tooissue 로그인 및 로그 아웃 요청을 사용 하 여 hello 사용자의 세션을 관리 hello 사용자에 대 한 정보 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-139">Use hello ADAL4J tooissue sign-in and sign-out requests, manage hello user's session, get information about hello user, and so forth.</span></span>

1. <span data-ttu-id="28125-140">열기 hello web.xml에 있는 파일에 \webapp\WEB-INF\, hello XML에에서 hello 응용 프로그램 구성 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-140">Open hello web.xml file located under \webapp\WEB-INF\, and enter hello app configuration values in hello XML.</span></span> <span data-ttu-id="28125-141">hello XML 파일에 코드 다음 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-141">hello XML file should contain hello following code:</span></span>

    ```xml

    <?xml version="1.0"?>
    <web-app id="WebApp_ID" version="2.4"
        xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
        http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
        <display-name>Archetype Created Web Application</display-name>
        <context-param>
            <param-name>authority</param-name>
            <param-value>https://login.microsoftonline.com/</param-value>
        </context-param>
        <context-param>
            <param-name>tenant</param-name>
            <param-value>YOUR_TENANT_NAME</param-value>
        </context-param>
        <filter>
            <filter-name>BasicFilter</filter-name>
            <filter-class>com.microsoft.aad.adal4jsample.BasicFilter</filter-class>
            <init-param>
                <param-name>client_id</param-name>
                <param-value>YOUR_CLIENT_ID</param-value>
            </init-param>
            <init-param>
                <param-name>secret_key</param-name>
                <param-value>YOUR_CLIENT_SECRET</param-value>
            </init-param>
        </filter>
        <filter-mapping>
            <filter-name>BasicFilter</filter-name>
            <url-pattern>/secure/*</url-pattern>
        </filter-mapping>
        <servlet>
            <servlet-name>mvc-dispatcher</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
            <load-on-startup>1</load-on-startup>
        </servlet>
        <servlet-mapping>
            <servlet-name>mvc-dispatcher</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/mvc-dispatcher-servlet.xml</param-value>
        </context-param>
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
    </web-app>
    ```

 * <span data-ttu-id="28125-142">YOUR_CLIENT_ID는 hello **응용 프로그램 Id** hello 등록 포털에서 tooyour 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-142">YOUR_CLIENT_ID is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
 * <span data-ttu-id="28125-143">YOUR_CLIENT_SECRET는 hello **응용 프로그램 암호** hello 포털에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-143">YOUR_CLIENT_SECRET is hello **Application Secret** that you created in hello portal.</span></span>
 * <span data-ttu-id="28125-144">YOUR_TENANT_NAME는 hello **테 넌 트 이름** 응용 프로그램 (예: contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="28125-144">YOUR_TENANT_NAME is hello **tenant name** of your app (for example, contoso.onmicrosoft.com).</span></span>

 <span data-ttu-id="28125-145">Hello XML 파일에 보시 hello 방문 / URL secure 때마다 BasicFilter를 사용 하 여 mvc 발송자 라고 JavaServer 페이지 (JSP) 또는 해 Java 서블릿에 웹 앱을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-145">As you can see in hello XML file, you are writing a JavaServer Pages (JSP) or Java Servlet web app called mvc-dispatcher that uses BasicFilter whenever you visit hello /secure URL.</span></span> <span data-ttu-id="28125-146">Hello에 동일한 코드를 사용 하 여 / 있습니다 hello 보호 된 콘텐츠 및 tooforce 인증 tooAzure AD에 대 한 지점으로 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-146">In hello same code, you use /secure as a place for hello protected content and tooforce authentication tooAzure AD.</span></span>

2. <span data-ttu-id="28125-147">\Webapp\WEB-INF 아래에 있는 hello mvc-발송자-servlet.xml 파일을 만들\, hello 코드 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-147">Create hello mvc-dispatcher-servlet.xml file located under \webapp\WEB-INF\, and enter hello following code:</span></span>

    ```xml

    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:context="http://www.springframework.org/schema/context"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="
            http://www.springframework.org/schema/beans     
            http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd">
        <context:component-scan base-package="com.microsoft.aad.adal4jsample" />
        <bean
            class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix">
                <value>/</value>
            </property>
            <property name="suffix">
                <value>.jsp</value>
            </property>
        </bean>
    </beans>
    ```

 <span data-ttu-id="28125-148">이 코드는 hello 웹 응용 프로그램 toouse 스프링 지시 며 여기서 toofind hello hello 다음 섹션에서 작성 된 JSP 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="28125-148">This code tells hello web app toouse Spring, and it indicates where toofind hello JSP file, which you write in hello next section.</span></span>

## <a name="step-4-create-hello-jsp-view-files-for-basicfilter-mvc"></a><span data-ttu-id="28125-149">4 단계: hello JSP 보기 파일이 작성 (BasicFilter MVC)</span><span class="sxs-lookup"><span data-stu-id="28125-149">Step 4: Create hello JSP View files (for BasicFilter MVC)</span></span>
<span data-ttu-id="28125-150">이제 WEB-INF에서 웹앱을 설정하는 과정이 절반 정도 진행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-150">You are half-way through setting up your web app in WEB-INF.</span></span> <span data-ttu-id="28125-151">다음으로 hello JSP 파일 BasicFilter 모델 뷰 컨트롤러 (MVC)을 어떤 hello 웹 응용 프로그램 실행을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-151">Next, you create hello JSP files for BasicFilter model view controller (MVC), which hello web app executes.</span></span> <span data-ttu-id="28125-152">म hello 구성 하는 동안 hello 파일 만들기에 그 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-152">We hinted at creating hello files during hello configuration.</span></span>

<span data-ttu-id="28125-153">Java hello 동안의 총 이전에 적용 해야 하는 XML 구성 파일을 `/` JSP 파일을 로드 하는 리소스에 `/secure` BasicFilter를 호출 하는 필터를 통해 전달 되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-153">Earlier, you told Java in hello XML configuration files that you have a `/` resource that loads JSP files, and you have a `/secure` resource that passes through a filter, which you called BasicFilter.</span></span>

<span data-ttu-id="28125-154">toocreate hello JSP 파일을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-154">toocreate hello JSP files, do hello following:</span></span>

1. <span data-ttu-id="28125-155">Hello index.jsp 파일을 만듭니다 (\webapp 아래에 있는\), 붙여넣기 hello 코드를 누른 다음:</span><span class="sxs-lookup"><span data-stu-id="28125-155">Create hello index.jsp file (located under \webapp\), and then paste hello following code:</span></span>

    ```jsp
    <html>
    <body>
        <h2>Hello World!</h2>
        <ul>
        <li><a href="secure/aad">Secure Page</a></li>
        </ul>
    </body>
    </html>
    ```

 <span data-ttu-id="28125-156">이 코드는 단순히 tooa hello 필터에 의해 보호 되는 보안 페이지를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-156">This code simply redirects tooa secure page that is protected by hello filter.</span></span>

2. <span data-ttu-id="28125-157">동일한 디렉터리 hello 하 만들 error.jsp 파일 toocatch 발생할 수 있는 모든 오류:</span><span class="sxs-lookup"><span data-stu-id="28125-157">In hello same directory, create an error.jsp file toocatch any errors that might happen:</span></span>

    ```jsp

    <html>
    <body>
        <h2>ERROR PAGE!</h2>
        <p>
            Exception -
            <%=request.getAttribute("error")%></p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
    </body>
    </html>
    ```
3. <span data-ttu-id="28125-158">웹 페이지에서 보호 하는 toomake \webapp hello 디렉터리는 이제 \webapp\secure 있도록 \secure 호출 아래에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-158">toomake that secure webpage, create a folder under \webapp called \secure so that hello directory is now \webapp\secure.</span></span>
4. <span data-ttu-id="28125-159">Hello \webapp\secure 디렉터리에 aad.jsp 파일을 만들려면 복사한 후 코드 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="28125-159">In hello \webapp\secure directory, create an aad.jsp file, and then paste hello following code:</span></span>

    ```jsp

    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>AAD Secure Page</title>
        </head>
        <body>

        <h1>Directory - Users List</h1>
        <p>${users}</p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?cc=1">Get new Access Token via Client Credentials</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?refresh=1">Get new Access Token via Refresh Token</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
        </body>
    </html>
    ```

    <span data-ttu-id="28125-160">이 페이지는 hello BasicFilter servlet 읽고 ADAJ4J hello를 사용 하 여 다음에 실행 toospecific 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-160">This page redirects toospecific requests, which hello BasicFilter servlet reads and then executes on by using hello ADAJ4J.</span></span>

<span data-ttu-id="28125-161">이제 해야 hello Java 파일을 tooset hello servlet 작업을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-161">You now need tooset up hello Java files so that hello servlet can do its work.</span></span>

## <a name="step-5-create-some-java-helper-files-for-basicfilter-mvc"></a><span data-ttu-id="28125-162">5단계: 일부 Java 도우미 파일 만들기(BasicFilter MVC용)</span><span class="sxs-lookup"><span data-stu-id="28125-162">Step 5: Create some Java helper files (for BasicFilter MVC)</span></span>
<span data-ttu-id="28125-163">이 단계에서 목표는 파일의 Java toocreate:</span><span class="sxs-lookup"><span data-stu-id="28125-163">Our goal in this step is toocreate Java files that:</span></span>

* <span data-ttu-id="28125-164">Hello 사용자의 로그 아웃 및 로그인에 대 한 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-164">Allow for sign-in and sign-out of hello user.</span></span>
* <span data-ttu-id="28125-165">Hello 사용자에 대 한 일부 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28125-165">Get some data about hello user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="28125-166">hello 사용자에 대 한 데이터 tooget hello Azure ad에서 Graph API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-166">tooget data about hello user, use hello Graph API from Azure AD.</span></span> <span data-ttu-id="28125-167">hello Graph API는 개별 사용자를 포함 하 여 조직에 대 한 toograb 데이터를 사용할 수 있는 안전한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-167">hello Graph API is a secure webservice that you can use toograb data about your organization, including individual users.</span></span> <span data-ttu-id="28125-168">이 방법은 다음을 보장하므로 토큰의 중요한 미리 필터링하는 것보다 더 나은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-168">This approach is better than pre-filling sensitive data in tokens, because it ensures that:</span></span>
    > * <span data-ttu-id="28125-169">hello 사용자에 게 hello 데이터에 대 한 요청 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28125-169">hello users who ask for hello data are authorized.</span></span>
    > * <span data-ttu-id="28125-170">모든 사용자에 게 toograb hello 토큰 (예: 바탕 화면에서 탈 옥 전화 또는 웹 브라우저 캐시)에서 발생할 수 hello 사용자 또는 조직 hello에 대 한 중요 한 세부 정보를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-170">Anyone who might happen toograb hello token (from a jailbroken phone or web-browser cache on a desktop, for example) cannot obtain important details about hello user or hello organization.</span></span>

<span data-ttu-id="28125-171">일부 Java toowrite이이 작업에 대 한 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-171">toowrite some Java files for this work:</span></span>

1. <span data-ttu-id="28125-172">폴더 만들기 루트에 디렉터리 adal4jsample toostore 모든 hello Java 파일 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-172">Create a folder in your root directory called adal4jsample toostore all hello Java files.</span></span>

    <span data-ttu-id="28125-173">이 예제에서는 hello Java 파일에서 네임 스페이스 com.microsoft.aad.adal4jsample hello를 사용 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-173">In this example, you are using hello namespace com.microsoft.aad.adal4jsample in hello Java files.</span></span> <span data-ttu-id="28125-174">대부분의 IDE는 이러한 용도로 중첩된 폴더 구조(예: /com/microsoft/aad/adal4jsample)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-174">Most IDEs create a nested folder structure for this purpose (for example, /com/microsoft/aad/adal4jsample).</span></span> <span data-ttu-id="28125-175">이 작업을 수행할 수 있지만 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-175">You can do this also, but it is not necessary.</span></span>

2. <span data-ttu-id="28125-176">이 폴더 안에 JSONHelper.java를 사용 하 여 파일을 만들 toohelp 구문 분석 hello JSON 데이터를 사용자가 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-176">Inside this folder, create a file called JSONHelper.java, which you'll use toohelp parse hello JSON data from your tokens.</span></span> <span data-ttu-id="28125-177">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-177">toocreate hello file, paste hello following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.lang.reflect.Field;
    import java.util.Arrays;
    import java.util.Enumeration;
    import java.util.List;

    import javax.servlet.http.HttpServletRequest;

    import org.apache.commons.lang3.text.WordUtils;
    import org.apache.log4j.Logger;
    import org.json.JSONArray;
    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This class provides hello methods tooparse JSON data from a JSON-formatted
     * string.
     *
     * @author Azure Active Directory contributor
     *
     */
    public class JSONHelper {

        private static Logger logger = Logger.getLogger(JSONHelper.class);

        JSONHelper() {
            // PropertyConfigurator.configure("log4j.properties");
        }

        /**
         * This method parses a JSON array out of a collection of JSON objects
         * within a string.
         *
         * @param jSonData
         *            hello JSON string that holds hello collection
         * @return A JSON array that contains all hello collection objects
         * @throws Exception
         */
        public static JSONArray fetchDirectoryObjectJSONArray(JSONObject jsonObject) throws Exception {
            JSONArray jsonArray = new JSONArray();
            jsonArray = jsonObject.optJSONObject("responseMsg").optJSONArray("value");
            return jsonArray;
        }

        /**
         * This method parses a JSON object out of a collection of JSON objects
         * within a string.
         *
         * @param jsonObject
         * @return A JSON object that contains hello DirectoryObject
         * @throws Exception
         */
        public static JSONObject fetchDirectoryObjectJSONObject(JSONObject jsonObject) throws Exception {
            JSONObject jObj = new JSONObject();
            jObj = jsonObject.optJSONObject("responseMsg");
            return jObj;
        }

        /**
         * This method parses hello skip token from a JSON-formatted string.
         *
         * @param jsonData
         *            hello JSON-formatted string
         * @return hello skipToken
         * @throws Exception
         */
        public static String fetchNextSkiptoken(JSONObject jsonObject) throws Exception {
            String skipToken = "";
            // Parse hello skip token out of hello string.
            skipToken = jsonObject.optJSONObject("responseMsg").optString("odata.nextLink");

            if (!skipToken.equalsIgnoreCase("")) {
                // Remove hello unnecessary prefix from hello skip token.
                int index = skipToken.indexOf("$skiptoken=") + (new String("$skiptoken=")).length();
                skipToken = skipToken.substring(index);
            }
            return skipToken;
        }

        /**
         * @param jsonObject
         * @return
         * @throws Exception
         */
        public static String fetchDeltaLink(JSONObject jsonObject) throws Exception {
            String deltaLink = "";
            // Parse hello skip token out of hello string.
            deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.deltaLink");
            if (deltaLink == null || deltaLink.length() == 0) {
                deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.nextLink");
                logger.info("deltaLink empty, nextLink ->" + deltaLink);

            }
            if (!deltaLink.equalsIgnoreCase("")) {
                // Remove hello unnecessary prefix from hello skip token.
                int index = deltaLink.indexOf("deltaLink=") + (new String("deltaLink=")).length();
                deltaLink = deltaLink.substring(index);
            }
            return deltaLink;
        }

        /**
         * This method creates a string consisting of a JSON document with all
         * hello necessary elements set from hello HttpServletRequest request.
         *
         * @param request
         *            hello HttpServletRequest
         * @return hello string containing hello JSON document
         * @throws Exception
         *             If there is any error processing hello request.
         */
        public static String createJSONString(HttpServletRequest request, String controller) throws Exception {
            JSONObject obj = new JSONObject();
            try {
                Field[] allFields = Class.forName(
                        "com.microsoft.windowsazure.activedirectory.sdk.graph.models." + controller).getDeclaredFields();
                String[] allFieldStr = new String[allFields.length];
                for (int i = 0; i < allFields.length; i++) {
                    allFieldStr[i] = allFields[i].getName();
                }
                List<String> allFieldStringList = Arrays.asList(allFieldStr);
                Enumeration<String> fields = request.getParameterNames();

                while (fields.hasMoreElements()) {

                    String fieldName = fields.nextElement();
                    String param = request.getParameter(fieldName);
                    if (allFieldStringList.contains(fieldName)) {
                        if (param == null || param.length() == 0) {
                            if (!fieldName.equalsIgnoreCase("password")) {
                                obj.put(fieldName, JSONObject.NULL);
                            }
                        } else {
                            if (fieldName.equalsIgnoreCase("password")) {
                                obj.put("passwordProfile", new JSONObject("{\"password\": \"" + param + "\"}"));
                            } else {
                                obj.put(fieldName, param);
                            }
                        }
                    }
                }
            } catch (JSONException e) {
                e.printStackTrace();
            } catch (SecurityException e) {
                e.printStackTrace();
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            }            
            return obj.toString();
        }

        /**
         *
         * @param key
         * @param value
         * @return string format of this JSON object
         * @throws Exception
         */
        public static String createJSONString(String key, String value) throws Exception {

            JSONObject obj = new JSONObject();
            try {
                obj.put(key, value);
            } catch (JSONException e) {
                e.printStackTrace();
            }

            return obj.toString();
        }

        /**
         * This is a generic method that copies hello simple attribute values from an
         * argument jsonObject tooan argument generic object.
         *
         * @param jsonObject
         *            hello jsonObject from where hello attributes are toobe copied.
         * @param destObject
         *            hello object where hello attributes should be copied to.
         * @throws Exception
         *             Throws an Exception when hello operation is unsuccessful.
         */
        public static <T> void convertJSONObjectToDirectoryObject(JSONObject jsonObject, T destObject) throws Exception {

            // Get hello list of all hello field names.
            Field[] fieldList = destObject.getClass().getDeclaredFields();

            // For all hello declared field.
            for (int i = 0; i < fieldList.length; i++) {
                // If hello field is of type String, that is
                // if it is a simple attribute.
                if (fieldList[i].getType().equals(String.class)) {
                    // Invoke hello corresponding set method of hello destObject using
                    // hello argument taken from hello jsonObject.
                    destObject
                            .getClass()
                            .getMethod(String.format("set%s", WordUtils.capitalize(fieldList[i].getName())),
                                    new Class[] { String.class })
                            .invoke(destObject, new Object[] { jsonObject.optString(fieldList[i].getName()) });
                }
            }
        }

        public static JSONArray joinJSONArrays(JSONArray a, JSONArray b) {
            JSONArray comb = new JSONArray();
            for (int i = 0; i < a.length(); i++) {
                comb.put(a.optJSONObject(i));
            }
            for (int i = 0; i < b.length(); i++) {
                comb.put(b.optJSONObject(i));
            }
            return comb;
        }

    }

    ```

3. <span data-ttu-id="28125-178">HttpClientHelper.java 사용 하는 파일을 만들 toohelp 구문 분석 hello Azure AD 끝점에서 HTTP 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-178">Create a file called HttpClientHelper.java, which you will use toohelp parse hello HTTP data from your Azure AD endpoint.</span></span> <span data-ttu-id="28125-179">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-179">toocreate hello file, paste hello following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.io.BufferedReader;
    import java.io.ByteArrayOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.OutputStreamWriter;
    import java.net.HttpURLConnection;

    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This is Helper class for all RestClient class.
     *
     * @author Azure Active Directory Contributor
     *
     */
    public class HttpClientHelper {

        public HttpClientHelper() {
            super();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            BufferedReader reader = null;
            if (isSuccess) {
                reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {
                reader = new BufferedReader(new InputStreamReader(conn.getErrorStream()));
            }
            StringBuffer stringBuffer = new StringBuffer();
            String line = "";
            while ((line = reader.readLine()) != null) {
                stringBuffer.append(line);
            }

            return stringBuffer.toString();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, String payLoad) throws IOException {

            // Send hello http message payload toohello server.
            if (payLoad != null) {
                conn.setDoOutput(true);
                OutputStreamWriter osw = new OutputStreamWriter(conn.getOutputStream());
                osw.write(payLoad);
                osw.flush();
                osw.close();
            }

            // Get hello message response from hello server.
            BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            String line = "";
            StringBuffer stringBuffer = new StringBuffer();
            while ((line = br.readLine()) != null) {
                stringBuffer.append(line);
            }

            br.close();

            return stringBuffer.toString();
        }

        public static byte[] getByteaArrayFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            InputStream is = conn.getInputStream();
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            byte[] buff = new byte[1024];
            int bytesRead = 0;

            while ((bytesRead = is.read(buff, 0, buff.length)) != -1) {
                baos.write(buff, 0, bytesRead);
            }

            byte[] bytes = baos.toByteArray();
            baos.close();
            return bytes;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processResponse(int responseCode, String errorCode, String errorMsg) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            response.put("errorCode", errorCode);
            response.put("errorMsg", errorMsg);

            return response;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processGoodRespStr(int responseCode, String goodRespStr) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (goodRespStr.equalsIgnoreCase("")) {
                response.put("responseMsg", "");
            } else {
                response.put("responseMsg", new JSONObject(goodRespStr));
            }

            return response;
        }

        /**
         * for good response
         *
         * @param responseCode
         * @param responseMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processBadRespStr(int responseCode, String responseMsg) throws JSONException {

            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (responseMsg.equalsIgnoreCase("")) { // good response is empty string
                response.put("responseMsg", "");
            } else { // bad response is json string
                JSONObject errorObject = new JSONObject(responseMsg).optJSONObject("odata.error");

                String errorCode = errorObject.optString("code");
                String errorMsg = errorObject.optJSONObject("message").optString("value");
                response.put("responseCode", responseCode);
                response.put("errorCode", errorCode);
                response.put("errorMsg", errorMsg);
            }

            return response;
        }

    }

    ```

## <a name="step-6-create-hello-java-graph-api-model-files-for-basicfilter-mvc"></a><span data-ttu-id="28125-180">6 단계: hello Java 그래프 API 모델 파일 만들기 (BasicFilter MVC)에 대 한</span><span class="sxs-lookup"><span data-stu-id="28125-180">Step 6: Create hello Java Graph API Model files (for BasicFilter MVC)</span></span>
<span data-ttu-id="28125-181">앞에서 설명한 대로 hello hello 로그인 한 사용자에 대 한 Graph API tooget 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-181">As indicated previously, you use hello Graph API tooget data about hello signed-in user.</span></span> <span data-ttu-id="28125-182">이 프로세스는 쉽고 toomake 모두 파일 toorepresent 디렉터리 개체 및 사용자를 만듭니다 파일 toorepresent hello java 해당 hello 개체 지향 패턴을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-182">toomake this process easy, create both a file toorepresent a Directory object and a file toorepresent hello user so that hello OO pattern of Java can be used.</span></span>

1. <span data-ttu-id="28125-183">DirectoryObject.java 있는 파일을 만들 디렉터리 개체에 대 한 기본 데이터 toostore 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-183">Create a file called DirectoryObject.java, which you use toostore basic data about any Directory object.</span></span> <span data-ttu-id="28125-184">나중에 수행할 수 있는 다른 Graph 쿼리에 대해 이 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-184">You can use this file later for any other Graph queries you might perform.</span></span> <span data-ttu-id="28125-185">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-185">toocreate hello file, paste hello following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    /**
     * @author Azure Active Directory Contributor
     *
     */
    public abstract class DirectoryObject {

        public DirectoryObject() {
            super();
        }

        /**
         *
         * @return
         */
        public abstract String getObjectId();

        /**
         * @param objectId
         */
        public abstract void setObjectId(String objectId);

        /**
         *
         * @return
         */
        public abstract String getObjectType();

        /**
         *
         * @param objectType
         */
        public abstract void setObjectType(String objectType);

        /**
         *
         * @return
         */
        public abstract String getDisplayName();

        /**
         *
         * @param displayName
         */
        public abstract void setDisplayName(String displayName);

    }

    ```

2. <span data-ttu-id="28125-186">User.java 있는 파일을 만들 toostore hello 디렉터리에서 모든 사용자에 대 한 기본 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-186">Create a file called User.java, which you use toostore basic data about any user from hello directory.</span></span> <span data-ttu-id="28125-187">다음은 코드 다음 hello를 붙여 넣을 수 있도록 디렉터리 데이터에 대 한 기본 getter 및 setter 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="28125-187">These are basic getter and setter methods for directory data, so you can paste hello following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.security.acl.Group;
    import java.util.ArrayList;

    import javax.xml.bind.annotation.XmlRootElement;

    import org.json.JSONObject;

    /**
    *  hello **User** class holds together all hello members of a WAAD User entity and all hello access methods and set methods.
    *  @author Azure Active Directory Contributor
    */
    @XmlRootElement
    public class User extends DirectoryObject{

        // hello following are hello individual private members of a User object that holds
        // a particular simple attribute of a User object.
        protected String objectId;
        protected String objectType;
        protected String accountEnabled;
        protected String city;
        protected String country;
        protected String department;
        protected String dirSyncEnabled;
        protected String displayName;
        protected String facsimileTelephoneNumber;
        protected String givenName;
        protected String jobTitle;
        protected String lastDirSyncTime;
        protected String mail;
        protected String mailNickname;
        protected String mobile;
        protected String password;
        protected String passwordPolicies;
        protected String physicalDeliveryOfficeName;
        protected String postalCode;
        protected String preferredLanguage;
        protected String state;
        protected String streetAddress;
        protected String surname;
        protected String telephoneNumber;
        protected String usageLocation;
        protected String userPrincipalName;
        protected boolean isDeleted;  // this will move toodto

        /**
         * These four properties are for future use.
         */
        // managerDisplayname of this user.
        protected String managerDisplayname;

        // hello directReports holds a list of directReports.
        private ArrayList<User> directReports;

        // hello groups holds a list of group entities this user belongs to.
        private ArrayList<Group> groups;

        // hello roles holds a list of role entities this user belongs to.
        private ArrayList<Group> roles;

        /**
         * hello constructor for hello **User** class. Initializes hello dynamic lists and managerDisplayname variables.
         */
        public User(){
            directReports = null;
            groups = new ArrayList<Group>();
            roles = new ArrayList<Group>();
            managerDisplayname = null;
        }
    //    
    //    public User(String displayName, String objectId){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //    }
    //    
    //    public User(String displayName, String objectId, String userPrincipalName, String accountEnabled){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //        setUserPrincipalName(userPrincipalName);
    //        setAccountEnabled(accountEnabled);
    //    }
    //    

        /**
         * @return hello objectId of this user.
         */
        public String getObjectId() {
            return objectId;
        }

        /**
         * @param objectId hello objectId tooset toothis User object.
         */
        public void setObjectId(String objectId) {
            this.objectId = objectId;
        }

        /**
         * @return hello objectType of this user.
         */
        public String getObjectType() {
            return objectType;
        }

        /**
         * @param objectType hello objectType tooset toothis User object.
         */
        public void setObjectType(String objectType) {
            this.objectType = objectType;
        }

        /**
         * @return hello userPrincipalName of this user.
         */
        public String getUserPrincipalName() {
            return userPrincipalName;
        }

        /**
         * @param userPrincipalName hello userPrincipalName tooset toothis User object.
         */
        public void setUserPrincipalName(String userPrincipalName) {
            this.userPrincipalName = userPrincipalName;
        }

        /**
         * @return hello usageLocation of this user.
         */
        public String getUsageLocation() {
            return usageLocation;
        }

        /**
         * @param usageLocation hello usageLocation tooset toothis User object.
         */
        public void setUsageLocation(String usageLocation) {
            this.usageLocation = usageLocation;
        }

        /**
         * @return hello telephoneNumber of this user.
         */
        public String getTelephoneNumber() {
            return telephoneNumber;
        }

        /**
         * @param telephoneNumber hello telephoneNumber tooset toothis User object.
         */
        public void setTelephoneNumber(String telephoneNumber) {
            this.telephoneNumber = telephoneNumber;
        }

        /**
         * @return hello surname of this user.
         */
        public String getSurname() {
            return surname;
        }

        /**
         * @param surname hello surname tooset toothis User object.
         */
        public void setSurname(String surname) {
            this.surname = surname;
        }

        /**
         * @return hello streetAddress of this user.
         */
        public String getStreetAddress() {
            return streetAddress;
        }

        /**
         * @param streetAddress hello streetAddress tooset toothis user.
         */
        public void setStreetAddress(String streetAddress) {
            this.streetAddress = streetAddress;
        }

        /**
         * @return hello state of this user.
         */
        public String getState() {
            return state;
        }

        /**
         * @param state hello state tooset toothis User object.
         */
        public void setState(String state) {
            this.state = state;
        }

        /**
         * @return hello preferredLanguage of this user.
         */
        public String getPreferredLanguage() {
            return preferredLanguage;
        }

        /**
         * @param preferredLanguage hello preferredLanguage tooset toothis user.
         */
        public void setPreferredLanguage(String preferredLanguage) {
            this.preferredLanguage = preferredLanguage;
        }

        /**
         * @return hello postalCode of this user.
         */
        public String getPostalCode() {
            return postalCode;
        }

        /**
         * @param postalCode hello postalCode tooset toothis user.
         */
        public void setPostalCode(String postalCode) {
            this.postalCode = postalCode;
        }

        /**
         * @return hello physicalDeliveryOfficeName of this user.
         */
        public String getPhysicalDeliveryOfficeName() {
            return physicalDeliveryOfficeName;
        }

        /**
         * @param physicalDeliveryOfficeName hello physicalDeliveryOfficeName tooset toothis User object.
         */
        public void setPhysicalDeliveryOfficeName(String physicalDeliveryOfficeName) {
            this.physicalDeliveryOfficeName = physicalDeliveryOfficeName;
        }

        /**
         * @return hello passwordPolicies of this user.
         */
        public String getPasswordPolicies() {
            return passwordPolicies;
        }

        /**
         * @param passwordPolicies hello passwordPolicies tooset toothis User object.
         */
        public void setPasswordPolicies(String passwordPolicies) {
            this.passwordPolicies = passwordPolicies;
        }

        /**
         * @return hello mobile of this user.
         */
        public String getMobile() {
            return mobile;
        }

        /**
         * @param mobile hello mobile tooset toothis User object.
         */
        public void setMobile(String mobile) {
            this.mobile = mobile;
        }

        /**
         * @return hello password of this user.
         */
        public String getPassword() {
            return password;
        }

        /**
         * @param password hello mobile tooset toothis User object.
         */
        public void setPassword(String password) {
            this.password = password;
        }

        /**
         * @return hello mail of this user.
         */
        public String getMail() {
            return mail;
        }

        /**
         * @param mail hello mail tooset toothis User object.
         */
        public void setMail(String mail) {
            this.mail = mail;
        }

        /**
         * @return hello MailNickname of this user.
         */
        public String getMailNickname() {
            return mailNickname;
        }

        /**
         * @param mail hello MailNickname tooset toothis User object.
         */
        public void setMailNickname(String mailNickname) {
            this.mailNickname = mailNickname;
        }

        /**
         * @return hello jobTitle of this user.
         */
        public String getJobTitle() {
            return jobTitle;
        }

        /**
         * @param jobTitle hello jobTitle tooset toothis User object.
         */
        public void setJobTitle(String jobTitle) {
            this.jobTitle = jobTitle;
        }

        /**
         * @return hello givenName of this user.
         */
        public String getGivenName() {
            return givenName;
        }

        /**
         * @param givenName hello givenName tooset toothis User object.
         */
        public void setGivenName(String givenName) {
            this.givenName = givenName;
        }

        /**
         * @return hello facsimileTelephoneNumber of this user.
         */
        public String getFacsimileTelephoneNumber() {
            return facsimileTelephoneNumber;
        }

        /**
         * @param facsimileTelephoneNumber hello facsimileTelephoneNumber tooset toothis User object.
         */
        public void setFacsimileTelephoneNumber(String facsimileTelephoneNumber) {
            this.facsimileTelephoneNumber = facsimileTelephoneNumber;
        }

        /**
         * @return hello displayName of this user.
         */
        public String getDisplayName() {
            return displayName;
        }

        /**
         * @param displayName hello displayName tooset toothis User object.
         */
        public void setDisplayName(String displayName) {
            this.displayName = displayName;
        }

        /**
         * @return hello dirSyncEnabled of this user.
         */
        public String getDirSyncEnabled() {
            return dirSyncEnabled;
        }

        /**
         * @param dirSyncEnabled hello dirSyncEnabled tooset toothis User object.
         */
        public void setDirSyncEnabled(String dirSyncEnabled) {
            this.dirSyncEnabled = dirSyncEnabled;
        }

        /**
         * @return hello department of this user.
         */
        public String getDepartment() {
            return department;
        }

        /**
         * @param department hello department tooset toothis User object.
         */
        public void setDepartment(String department) {
            this.department = department;
        }

        /**
         * @return hello lastDirSyncTime of this user.
         */
        public String getLastDirSyncTime() {
            return lastDirSyncTime;
        }

        /**
         * @param lastDirSyncTime hello lastDirSyncTime tooset toothis User object.
         */
        public void setLastDirSyncTime(String lastDirSyncTime) {
            this.lastDirSyncTime = lastDirSyncTime;
        }

        /**
         * @return hello country of this user.
         */
        public String getCountry() {
            return country;
        }

        /**
         * @param country hello country tooset toothis user.
         */
        public void setCountry(String country) {
            this.country = country;
        }

        /**
         * @return hello city of this user.
         */
        public String getCity() {
            return city;
        }

        /**
         * @param city hello city tooset toothis user.
         */
        public void setCity(String city) {
            this.city = city;
        }

        /**
         * @return hello accountEnabled attribute of this user.
         */
        public String getAccountEnabled() {
            return accountEnabled;
        }

        /**
         * @param accountEnabled hello accountEnabled tooset toothis user.
         */
        public void setAccountEnabled(String accountEnabled) {
            this.accountEnabled = accountEnabled;
        }

        public boolean isIsDeleted() {
            return this.isDeleted;
        }

        public void setIsDeleted(boolean isDeleted) {
            this.isDeleted = isDeleted;
        }

        @Override
        public String toString() {
            return new JSONObject(this).toString();
        }

        public String getManagerDisplayname(){
            return managerDisplayname;
        }

        public void setManagerDisplayname(String managerDisplayname){
            this.managerDisplayname = managerDisplayname;
        }
    }

    /**
    * hello DirectReports class holds hello essential data for a single DirectReport entry. That is,
    * it holds hello displayName and hello objectId of hello direct entry. It also provides the
    * access methods tooset or get hello displayName and hello ObjectId of this entry.
    */
    //class DirectReport extends User{
    //
    //    private String displayName;
    //    private String objectId;
    //     
    //    /**
    //     * Two arguments Constructor for hello DirectReport class.
    //     * @param displayName
    //     * @param objectId
    //     */
    //    public DirectReport(String displayName, String objectId){
    //        this.displayName = displayName;
    //        this.objectId = objectId;
    //    }
    //
    //    /**
    //     * @return hello displayName of this direct report entry.
    //     */
    //    public String getDisplayName() {
    //        return displayName;
    //    }
    //
    //    
    //    /**
    //     *  @return hello objectId of this direct report entry.
    //     */
    //    public String getObjectId() {
    //        return objectId;
    //    }
    //
    //}

    ```

## <a name="step-7-create-hello-authentication-model-and-controller-files-for-basicfilter"></a><span data-ttu-id="28125-188">7 단계: hello 인증 모델과 컨트롤러 파일이 작성 (BasicFilter)</span><span class="sxs-lookup"><span data-stu-id="28125-188">Step 7: Create hello authentication model and controller files (for BasicFilter)</span></span>
<span data-ttu-id="28125-189">Java가 길어질 수 있지만 작업은 거의 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-189">We acknowledge that Java can be verbose, but you're almost done.</span></span> <span data-ttu-id="28125-190">Hello BasicFilter servlet toohandle hello 요청을 작성 하기 전에 몇 가지 더 많은 도우미 파일 ADAL4J 필요한 해당 hello toowrite를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-190">Before you write hello BasicFilter servlet toohandle hello requests, you need toowrite some more helper files that hello ADAL4J needs.</span></span>

1. <span data-ttu-id="28125-191">AuthHelper.java 있습니다 메서드 toouse toodetermine hello 상태의 hello 로그인 한 사용자 제공 하 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-191">Create a file called AuthHelper.java, which will give you methods toouse toodetermine hello state of hello signed-in user.</span></span> <span data-ttu-id="28125-192">hello 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-192">hello methods include:</span></span>

 * <span data-ttu-id="28125-193">**isAuthenticated()**: hello 사용자가 로그인 하는지 여부를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-193">**isAuthenticated()**: Returns whether hello user is signed in.</span></span>
 * <span data-ttu-id="28125-194">**containsAuthenticationData()**: hello 토큰 데이터 있는지 여부를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-194">**containsAuthenticationData()**: Returns whether hello token has data.</span></span>
 * <span data-ttu-id="28125-195">**isAuthenticationSuccessful()**: hello 인증 hello 사용자에 대 한 성공 여부를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-195">**isAuthenticationSuccessful()**: Returns whether hello authentication was successful for hello user.</span></span>

 <span data-ttu-id="28125-196">toocreate는 AuthHelper.java 파일 hello, hello 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-196">toocreate hello AuthHelper.java file, paste hello following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.util.Map;

    import javax.servlet.http.HttpServletRequest;

    import com.microsoft.aad.adal4j.AuthenticationResult;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
    import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

    public final class AuthHelper {

        public static final String PRINCIPAL_SESSION_NAME = "principal";

        private AuthHelper() {
        }

        public static boolean isAuthenticated(HttpServletRequest request) {
            return request.getSession().getAttribute(PRINCIPAL_SESSION_NAME) != null;
        }

        public static AuthenticationResult getAuthSessionObject(
                HttpServletRequest request) {
            return (AuthenticationResult) request.getSession().getAttribute(
                    PRINCIPAL_SESSION_NAME);
        }

        public static boolean containsAuthenticationData(
                HttpServletRequest httpRequest) {
            Map<String, String[]> map = httpRequest.getParameterMap();
            return httpRequest.getMethod().equalsIgnoreCase("POST") && (httpRequest.getParameterMap().containsKey(
                            AuthParameterNames.ERROR)
                            || httpRequest.getParameterMap().containsKey(
                                    AuthParameterNames.ID_TOKEN) || httpRequest
                            .getParameterMap().containsKey(AuthParameterNames.CODE));
        }

        public static boolean isAuthenticationSuccessful(
                AuthenticationResponse authResponse) {
            return authResponse instanceof AuthenticationSuccessResponse;
        }
    }
    ```

2. <span data-ttu-id="28125-197">ADAL4J 필요한 해당 hello AuthParameterNames.java 일부 변경할 수 없는 변수를 제공 하 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-197">Create a file called AuthParameterNames.java, which gives you some immutable variables that hello ADAL4J requires.</span></span> <span data-ttu-id="28125-198">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-198">toocreate hello file, paste hello following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    public final class AuthParameterNames {

        private AuthParameterNames() {
        }

        public static String ERROR = "error";
        public static String ERROR_DESCRIPTION = "error_description";
        public static String ERROR_URI = "error_uri";
        public static String ID_TOKEN = "id_token";
        public static String CODE = "code";
    }
    ```

3. <span data-ttu-id="28125-199">MVC 패턴의 hello 컨트롤러는 AadController.java 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-199">Create a file called AadController.java, which is hello controller of your MVC pattern.</span></span> <span data-ttu-id="28125-200">hello 파일을 제공 하면 hello 앱에 대 한 hello JSP 컨트롤러 고 hello 보안/aad URL 끝점을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-200">hello file gives you hello JSP controller and exposes hello secure/aad URL endpoint for hello app.</span></span> <span data-ttu-id="28125-201">또한 hello 파일 hello 그래프 쿼리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-201">hello file also includes hello graph query.</span></span> <span data-ttu-id="28125-202">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-202">toocreate hello file, paste hello following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.net.HttpURLConnection;
    import java.net.URL;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpSession;

    import org.json.JSONArray;
    import org.json.JSONObject;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;

    import com.microsoft.aad.adal4j.AuthenticationResult;

    @Controller
    @RequestMapping("/secure/aad")
    public class AadController {

        @RequestMapping(method = { RequestMethod.GET, RequestMethod.POST })
        public String getDirectoryObjects(ModelMap model, HttpServletRequest httpRequest) {
            HttpSession session = httpRequest.getSession();
            AuthenticationResult result = (AuthenticationResult) session.getAttribute(AuthHelper.PRINCIPAL_SESSION_NAME);
            if (result == null) {
                model.addAttribute("error", new Exception("AuthenticationResult not found in session."));
                return "/error";
            } else {
                String data;
                try {
                    data = this.getUsernamesFromGraph(result.getAccessToken(), session.getServletContext()
                            .getInitParameter("tenant"));
                    model.addAttribute("users", data);
                } catch (Exception e) {
                    model.addAttribute("error", e);
                    return "/error";
                }
            }
            return "/secure/aad";
        }

        private String getUsernamesFromGraph(String accessToken, String tenant) throws Exception {
            URL url = new URL(String.format("https://graph.windows.net/%s/users?api-version=2013-04-05", tenant,
                    accessToken));

            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            // Set hello appropriate header fields in hello request header.
            conn.setRequestProperty("api-version", "2013-04-05");
            conn.setRequestProperty("Authorization", accessToken);
            conn.setRequestProperty("Accept", "application/json;odata=minimalmetadata");
            String goodRespStr = HttpClientHelper.getResponseStringFromConn(conn, true);
            // logger.info("goodRespStr ->" + goodRespStr);
            int responseCode = conn.getResponseCode();
            JSONObject response = HttpClientHelper.processGoodRespStr(responseCode, goodRespStr);
            JSONArray users = new JSONArray();

            users = JSONHelper.fetchDirectoryObjectJSONArray(response);

            StringBuilder builder = new StringBuilder();
            User user = null;
            for (int i = 0; i < users.length(); i++) {
                JSONObject thisUserJSONObject = users.optJSONObject(i);
                user = new User();
                JSONHelper.convertJSONObjectToDirectoryObject(thisUserJSONObject, user);
                builder.append(user.getUserPrincipalName() + "<br/>");
            }
            return builder.toString();
        }

    }

    ```

## <a name="step-8-create-hello-basicfilter-file-for-basicfilter-mvc"></a><span data-ttu-id="28125-203">8 단계: (BasicFilter MVC)에 대 한 hello BasicFilter 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="28125-203">Step 8: Create hello BasicFilter file (for BasicFilter MVC)</span></span>
<span data-ttu-id="28125-204">이제 파일 hello JSP 보기에서에서 hello 요청을 처리 하는 hello BasicFilter.java 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-204">You can now create hello BasicFilter.java file, which handles hello requests from hello JSP View files.</span></span> <span data-ttu-id="28125-205">코드 다음 붙여넣기 hello toocreate hello 파일:</span><span class="sxs-lookup"><span data-stu-id="28125-205">toocreate hello file, paste hello following code:</span></span>

```Java

package com.microsoft.aad.adal4jsample;

import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.net.URI;
import java.net.URLEncoder;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;
import com.nimbusds.oauth2.sdk.AuthorizationCode;
import com.nimbusds.openid.connect.sdk.AuthenticationErrorResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

public class BasicFilter implements Filter {

    private String clientId = "";
    private String clientSecret = "";
    private String tenant = "";
    private String authority;

    public void destroy() {

    }

    public void doFilter(ServletRequest request, ServletResponse response,
            FilterChain chain) throws IOException, ServletException {

        if (request instanceof HttpServletRequest) {
            HttpServletRequest httpRequest = (HttpServletRequest) request;
            HttpServletResponse httpResponse = (HttpServletResponse) response;
            try {

                String currentUri = request.getScheme()
                        + "://"
                        + request.getServerName()
                        + ("http".equals(request.getScheme())
                                && request.getServerPort() == 80
                                || "https".equals(request.getScheme())
                                && request.getServerPort() == 443 ? "" : ":"
                                + request.getServerPort())
                        + httpRequest.getRequestURI();
                String fullUrl = currentUri
                        + (httpRequest.getQueryString() != null ? "?"
                                + httpRequest.getQueryString() : "");
                // check if user has a session
                if (!AuthHelper.isAuthenticated(httpRequest)) {
                    if (AuthHelper.containsAuthenticationData(httpRequest)) {
                        Map<String, String> params = new HashMap<String, String>();
                        for (String key : request.getParameterMap().keySet()) {
                            params.put(key,
                                    request.getParameterMap().get(key)[0]);
                        }
                        AuthenticationResponse authResponse = AuthenticationResponseParser
                                .parse(new URI(fullUrl), params);
                        if (AuthHelper.isAuthenticationSuccessful(authResponse)) {

                            AuthenticationSuccessResponse oidcResponse = (AuthenticationSuccessResponse) authResponse;
                            AuthenticationResult result = getAccessToken(
                                    oidcResponse.getAuthorizationCode(),
                                    currentUri);
                            createSessionPrincipal(httpRequest, result);
                        } else {
                            AuthenticationErrorResponse oidcResponse = (AuthenticationErrorResponse) authResponse;
                            throw new Exception(String.format(
                                    "Request for auth code failed: %s - %s",
                                    oidcResponse.getErrorObject().getCode(),
                                    oidcResponse.getErrorObject()
                                            .getDescription()));
                        }
                    } else {
                            // not authenticated
                            httpResponse.setStatus(302);
                            httpResponse
                                    .sendRedirect(getRedirectUrl(currentUri));
                            return;
                    }
                } else {
                    // if authenticated, how toocheck for valid session?
                    AuthenticationResult result = AuthHelper
                            .getAuthSessionObject(httpRequest);

                    if (httpRequest.getParameter("refresh") != null) {
                        result = getAccessTokenFromRefreshToken(
                                result.getRefreshToken(), currentUri);
                    } else {
                        if (httpRequest.getParameter("cc") != null) {
                            result = getAccessTokenFromClientCredentials();
                        } else {
                            if (result.getExpiresOnDate().before(new Date())) {
                                result = getAccessTokenFromRefreshToken(
                                        result.getRefreshToken(), currentUri);
                            }
                        }
                    }
                    createSessionPrincipal(httpRequest, result);
                }
            } catch (Throwable exc) {
                httpResponse.setStatus(500);
                request.setAttribute("error", exc.getMessage());
                httpResponse.sendRedirect(((HttpServletRequest) request)
                        .getContextPath() + "/error.jsp");
            }
        }
        chain.doFilter(request, response);
    }

    private AuthenticationResult getAccessTokenFromClientCredentials()
            throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", new ClientCredential(clientId,
                            clientSecret), null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private AuthenticationResult getAccessTokenFromRefreshToken(
            String refreshToken, String currentUri) throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByRefreshToken(refreshToken,
                            new ClientCredential(clientId, clientSecret), null,
                            null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;

    }

    private AuthenticationResult getAccessToken(
            AuthorizationCode authorizationCode, String currentUri)
            throws Throwable {
        String authCode = authorizationCode.getValue();
        ClientCredential credential = new ClientCredential(clientId,
                clientSecret);
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByAuthorizationCode(authCode, new URI(
                            currentUri), credential, null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private void createSessionPrincipal(HttpServletRequest httpRequest,
            AuthenticationResult result) throws Exception {
        httpRequest.getSession().setAttribute(
                AuthHelper.PRINCIPAL_SESSION_NAME, result);
    }

    private String getRedirectUrl(String currentUri)
            throws UnsupportedEncodingException {
        String redirectUrl = authority
                + this.tenant
                + "/oauth2/authorize?response_type=code%20id_token&scope=openid&response_mode=form_post&redirect_uri="
                + URLEncoder.encode(currentUri, "UTF-8") + "&client_id="
                + clientId + "&resource=https%3a%2f%2fgraph.windows.net"
                + "&nonce=" + UUID.randomUUID() + "&site_id=500879";
        return redirectUrl;
    }

    public void init(FilterConfig config) throws ServletException {
        clientId = config.getInitParameter("client_id");
        authority = config.getServletContext().getInitParameter("authority");
        tenant = config.getServletContext().getInitParameter("tenant");
        clientSecret = config.getInitParameter("secret_key");
    }

}

```

<span data-ttu-id="28125-206">이 servlet 해당 hello ADAL4J hello 앱 toorun에서 예상 되는 모든 hello 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-206">This servlet exposes all hello methods that hello ADAL4J will expect from hello app toorun.</span></span> <span data-ttu-id="28125-207">hello 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-207">hello methods include:</span></span>

* <span data-ttu-id="28125-208">**getAccessTokenFromClientCredentials()**: hello 암호에서 hello 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28125-208">**getAccessTokenFromClientCredentials()**: Gets hello access token from hello secret.</span></span>
* <span data-ttu-id="28125-209">**getAccessTokenFromRefreshToken()**: 새로 고침 토큰을 통한 hello 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28125-209">**getAccessTokenFromRefreshToken()**: Gets hello access token from a refresh token.</span></span>
* <span data-ttu-id="28125-210">**getaccesstoken ()**: hello 액세스 (사용) 하는 OpenID Connect 흐름에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28125-210">**getAccessToken()**: Gets hello access token from an OpenID Connect flow (which you use).</span></span>
* <span data-ttu-id="28125-211">**createSessionPrincipal()**: Graph API 액세스에 대 한 세션 주 toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28125-211">**createSessionPrincipal()**: Creates a session principal toouse for Graph API access.</span></span>
* <span data-ttu-id="28125-212">**getRedirectUrl()**: 가져옵니다 hello redirectURL toocompare hello와 것 값 hello 포털에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-212">**getRedirectUrl()**: Gets hello redirectURL toocompare it with hello value you entered in hello portal.</span></span>

## <a name="step-9-compile-and-run-hello-sample-in-tomcat"></a><span data-ttu-id="28125-213">9 단계: 컴파일 및 Tomcat에서 hello 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-213">Step 9: Compile and run hello sample in Tomcat</span></span>

1. <span data-ttu-id="28125-214">Tooyour 루트 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-214">Change tooyour root directory.</span></span>
2. <span data-ttu-id="28125-215">나타납니까 함께 사용 하 여 toobuild hello 샘플 `maven`실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="28125-215">toobuild hello sample you just put together by using `maven`, run hello following command:</span></span>

    `$ mvn package`

 <span data-ttu-id="28125-216">이 명령은 hello pom.xml 파일 종속성에 대 한 작성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-216">This command uses hello pom.xml file that you wrote for dependencies.</span></span>

<span data-ttu-id="28125-217">이제 adal4jsample.war 파일이 /targets 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-217">You should now have a adal4jsample.war file in your /targets directory.</span></span> <span data-ttu-id="28125-218">Tomcat 컨테이너에서 hello 파일을 배포할 수 있으며 hello http://localhost:8080/adal4jsample/URL을 방문 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-218">You can deploy hello file in your Tomcat container and visit hello http://localhost:8080/adal4jsample/ URL.</span></span>

> [!NOTE]
> <span data-ttu-id="28125-219">최신 Tomcat 서버 hello와.war 파일을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-219">You can easily deploy a .war file with hello latest Tomcat servers.</span></span> <span data-ttu-id="28125-220">Toohttp://localhost:8080/관리자/이동한 hello adal4jsample.war 파일을 업로드 하기 위한 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="28125-220">Go toohttp://localhost:8080/manager/, and follow hello instructions for uploading hello adal4jsample.war file.</span></span> <span data-ttu-id="28125-221">드립니다 autodeploy hello 올바른 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-221">It will autodeploy for you with hello correct endpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="28125-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28125-222">Next steps</span></span>
<span data-ttu-id="28125-223">이제 작업 중인 사용자 인증, 안전 하 게 웹 OAuth 2.0을 사용 하 여 Api를 호출 하 고 수 있는 hello 사용자에 대 한 기본 정보를 얻을 Java 앱 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-223">You now have a working Java app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello users.</span></span> <span data-ttu-id="28125-224">사용자와 테 넌 트 채워진 이미 하지 않은 경우 이제은 좋은 시간 toodo 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-224">If you haven't already populated your tenant with users, now is a good time toodo so.</span></span>

<span data-ttu-id="28125-225">추가 참조에 대 한 두 가지 방법 중 하나로 구성 값) (없이 완료 hello 샘플을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28125-225">For additional reference, you can get hello completed sample (without your configuration values) in either of two ways:</span></span>

* <span data-ttu-id="28125-226">[.zip 파일](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28125-226">Download it as a [.zip file](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip).</span></span>
* <span data-ttu-id="28125-227">복제 hello 파일 GitHub에서 hello 다음 명령을 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="28125-227">Clone hello file from GitHub by entering hello following command:</span></span>

 ```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```
