---
title: "Azure AD Java 웹앱 시작 | Microsoft Docs"
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
ms.openlocfilehash: 5358404881b65d217ab36a41ca04a73f2c462c86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="java-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="4906f-103">Azure AD에서 Java 웹앱 로그인 및 로그아웃</span><span class="sxs-lookup"><span data-stu-id="4906f-103">Java web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4906f-104">Azure AD(Azure Active Directory)는 몇 개의 코드 줄만으로 단일 로그인 및 로그아웃을 제공하여 간단하게 웹앱의 ID 관리를 아웃소싱할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="4906f-105">Microsoft에서 구현한 커뮤니티 기반의 ADAL4J(Java용 Azure Active Directory 인증 라이브러리)를 사용하여 사용자를 Java 웹앱에서 로그인 및 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-105">You can sign users in and out of Java web apps by using the Microsoft implementation of the community-driven Azure Active Directory Authentication Library for Java (ADAL4J).</span></span>

<span data-ttu-id="4906f-106">이 문서에서는 ADAL4J를 사용하여 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-106">This article shows how to use the ADAL4J to:</span></span>

* <span data-ttu-id="4906f-107">Azure AD를 ID 공급자로 사용하여 사용자를 웹앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-107">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="4906f-108">일부 사용자 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-108">Display some user information.</span></span>
* <span data-ttu-id="4906f-109">앱에서 사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-109">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="4906f-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4906f-110">Before you get started</span></span>

* <span data-ttu-id="4906f-111">[앱 기본 사항](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)을 다운로드하거나 [완성된 샘플](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="4906f-111">Download the [app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip), or download the [completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>
* <span data-ttu-id="4906f-112">또한 앱을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-112">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="4906f-113">Azure AD 테넌트가 아직 없는 경우 [가져오는 방법을 알아봅니다](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="4906f-113">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="4906f-114">준비가 완료되면 다음 9가지 섹션의 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-114">When you are ready, follow the procedures in the next nine sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="4906f-115">1단계: Azure AD에 새 앱 등록</span><span class="sxs-lookup"><span data-stu-id="4906f-115">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="4906f-116">사용자를 인증하도록 앱을 설정하려면 먼저 다음을 수행하여 앱을 테넌트에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-116">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="4906f-117">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4906f-118">위쪽 모음에서 계정 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-118">On the top bar, click your account name.</span></span> <span data-ttu-id="4906f-119">**디렉터리** 목록에서 앱을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-119">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="4906f-120">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-120">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4906f-121">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-121">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4906f-122">프롬프트에 따라 새 **웹 응용 프로그램 및/또는 WebAPI**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-122">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="4906f-123">**이름**은 사용자에게 앱에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-123">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="4906f-124">**로그온 URL**은 앱의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-124">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="4906f-125">기본 사항의 기본 URL은 http://localhost:8080/adal4jsample/입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-125">The skeleton's default URL is http://localhost:8080/adal4jsample/.</span></span>
6. <span data-ttu-id="4906f-126">등록이 완료되면 Azure AD가 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-126">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="4906f-127">다음 섹션에서 사용할 수 있도록 앱 페이지의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-127">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="4906f-128">응용 프로그램에 대한 **설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-128">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="4906f-129">**앱 ID URI**는 앱의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-129">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="4906f-130">명명 규칙은 `https://<tenant-domain>/<app-name>`(예: `http://localhost:8080/adal4jsample/`)입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-130">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `http://localhost:8080/adal4jsample/`).</span></span>

<span data-ttu-id="4906f-131">앱용 포털에 있는 경우 **설정** 페이지에서 앱용 키를 만든 후 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-131">When you are in the portal for the app, create and copy a key for the app on the **Settings** page.</span></span> <span data-ttu-id="4906f-132">이 키는 바로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-132">You'll need the key shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-adal4j-and-prerequisites-by-using-maven"></a><span data-ttu-id="4906f-133">2단계: Maven을 사용하여 ADAL4J 및 필수 구성 요소를 사용하도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="4906f-133">Step 2: Set up the app to use the ADAL4J and prerequisites by using Maven</span></span>
<span data-ttu-id="4906f-134">이 단계에서는 OpenID Connect 인증 프로토콜을 사용하도록 ADAL4J를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-134">In this step, you configure the ADAL4J to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4906f-135">ADAL4J를 사용하여 로그인 및 로그아웃 요청을 실행하고, 사용자 세션을 관리하고, 사용자 정보를 가져오는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-135">You use the ADAL4J to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

<span data-ttu-id="4906f-136">프로젝트의 루트 디렉터리에서 `pom.xml`을 열거나 만들고, `// TODO: provide dependencies for Maven`을 찾은 후 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-136">In the root directory of your project, open/create `pom.xml`, locate `// TODO: provide dependencies for Maven`, and replace it with the following:</span></span>

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

## <a name="step-3-create-the-java-web-app-files-web-inf"></a><span data-ttu-id="4906f-137">3단계: Java 웹앱 파일 만들기(WEB-INF)</span><span class="sxs-lookup"><span data-stu-id="4906f-137">Step 3: Create the Java web app files (WEB-INF)</span></span>
<span data-ttu-id="4906f-138">이 단계에서는 OpenID Connect 인증 프로토콜을 사용하도록 Java 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-138">In this step, you configure the Java web app to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4906f-139">ADAL4J를 사용하여 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하고, 사용자에 대한 정보를 가져오는 등의 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-139">Use the ADAL4J to issue sign-in and sign-out requests, manage the user's session, get information about the user, and so forth.</span></span>

1. <span data-ttu-id="4906f-140">\webapp\WEB-INF\, 아래에 있는 web.xml 파일을 열고 앱 구성 값을 이 XML에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-140">Open the web.xml file located under \webapp\WEB-INF\, and enter the app configuration values in the XML.</span></span> <span data-ttu-id="4906f-141">이 XML 파일에는 다음 코드가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-141">The XML file should contain the following code:</span></span>

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

 * <span data-ttu-id="4906f-142">YOUR_CLIENT_ID은(는) 등록 포털에서 앱에 할당된 **응용 프로그램 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-142">YOUR_CLIENT_ID is the **Application Id** assigned to your app in the registration portal.</span></span>
 * <span data-ttu-id="4906f-143">YOUR_CLIENT_SECRET는 포털에서 만든 **응용 프로그램 암호**입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-143">YOUR_CLIENT_SECRET is the **Application Secret** that you created in the portal.</span></span>
 * <span data-ttu-id="4906f-144">YOUR_TENANT_NAME은 앱의 **테넌트 이름**(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-144">YOUR_TENANT_NAME is the **tenant name** of your app (for example, contoso.onmicrosoft.com).</span></span>

 <span data-ttu-id="4906f-145">XML 파일에서 볼 수 있는 것처럼 /secure URL을 방문할 때마다 BasicFilter를 사용하는 mvc-dispatcher라는 JSP(JavaServer Pages) 또는 Java 서블릿 웹앱을 작성하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-145">As you can see in the XML file, you are writing a JavaServer Pages (JSP) or Java Servlet web app called mvc-dispatcher that uses BasicFilter whenever you visit the /secure URL.</span></span> <span data-ttu-id="4906f-146">동일한 코드에서 보호된 콘텐ㅇ츠에 대한 위치로 /secure를 사용하고 Azure AD에서 강제 인증을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-146">In the same code, you use /secure as a place for the protected content and to force authentication to Azure AD.</span></span>

2. <span data-ttu-id="4906f-147">\webapp\WEB-INF\, 아래에 있는 mvc-dispatcher-servlet.xml 파일을 만들고 다음 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-147">Create the mvc-dispatcher-servlet.xml file located under \webapp\WEB-INF\, and enter the following code:</span></span>

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

 <span data-ttu-id="4906f-148">이 코드는 웹앱에 Spring을 사용하도록 지시하고 다음 단계에서 작성하게 될 JSP 파일을 찾을 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-148">This code tells the web app to use Spring, and it indicates where to find the JSP file, which you write in the next section.</span></span>

## <a name="step-4-create-the-jsp-view-files-for-basicfilter-mvc"></a><span data-ttu-id="4906f-149">4단계: JSP 보기 파일 만들기(BasicFilter MVC용)</span><span class="sxs-lookup"><span data-stu-id="4906f-149">Step 4: Create the JSP View files (for BasicFilter MVC)</span></span>
<span data-ttu-id="4906f-150">이제 WEB-INF에서 웹앱을 설정하는 과정이 절반 정도 진행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-150">You are half-way through setting up your web app in WEB-INF.</span></span> <span data-ttu-id="4906f-151">다음으로, 웹앱이 실행하는 BasicFilter MVC(모델 뷰 컨트롤러)에 대한 JSP 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-151">Next, you create the JSP files for BasicFilter model view controller (MVC), which the web app executes.</span></span> <span data-ttu-id="4906f-152">구성하는 동안 이러한 파일을 만드는 힌트가 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-152">We hinted at creating the files during the configuration.</span></span>

<span data-ttu-id="4906f-153">앞서 XML 구성 파일에서 JSP 파일을 로드하는 `/` 리소스가 있으며 BasicFilter라는 필터를 통과하는 `/secure` 리소스가 있다는 사실을 Java에 알렸습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-153">Earlier, you told Java in the XML configuration files that you have a `/` resource that loads JSP files, and you have a `/secure` resource that passes through a filter, which you called BasicFilter.</span></span>

<span data-ttu-id="4906f-154">JSP 파일을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-154">To create the JSP files, do the following:</span></span>

1. <span data-ttu-id="4906f-155">Index.jsp 파일(\webapp\)을 만든 후 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-155">Create the index.jsp file (located under \webapp\), and then paste the following code:</span></span>

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

 <span data-ttu-id="4906f-156">이 코드는 필터로 보호되는 보안 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-156">This code simply redirects to a secure page that is protected by the filter.</span></span>

2. <span data-ttu-id="4906f-157">발생할 수 있는 모든 오류를 catch하는 error.jsp 파일을 동일한 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-157">In the same directory, create an error.jsp file to catch any errors that might happen:</span></span>

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
3. <span data-ttu-id="4906f-158">해당 페이지를 보안 웹 페이지로 만들려면 \webapp 아래에 \secure라는 하위 폴더를 만들어 디렉터리가 \webapp\secure가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-158">To make that secure webpage, create a folder under \webapp called \secure so that the directory is now \webapp\secure.</span></span>
4. <span data-ttu-id="4906f-159">\Webapp\secure 디렉터리에 aad.jsp 파일을 만든 후 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-159">In the \webapp\secure directory, create an aad.jsp file, and then paste the following code:</span></span>

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

    <span data-ttu-id="4906f-160">이 페이지는 BasicFilter 서블릿이 읽은 후 ADAJ4J를 사용하여 실행하는 특정 요청으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-160">This page redirects to specific requests, which the BasicFilter servlet reads and then executes on by using the ADAJ4J.</span></span>

<span data-ttu-id="4906f-161">이제 서블릿이 해당 작업을 수행할 수 있도록 Java 파일을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-161">You now need to set up the Java files so that the servlet can do its work.</span></span>

## <a name="step-5-create-some-java-helper-files-for-basicfilter-mvc"></a><span data-ttu-id="4906f-162">5단계: 일부 Java 도우미 파일 만들기(BasicFilter MVC용)</span><span class="sxs-lookup"><span data-stu-id="4906f-162">Step 5: Create some Java helper files (for BasicFilter MVC)</span></span>
<span data-ttu-id="4906f-163">이 단계의 목표는 다음과 같은 Java 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-163">Our goal in this step is to create Java files that:</span></span>

* <span data-ttu-id="4906f-164">사용자의 로그인 및 로그아웃을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-164">Allow for sign-in and sign-out of the user.</span></span>
* <span data-ttu-id="4906f-165">사용자에 대한 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-165">Get some data about the user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4906f-166">사용자에 대한 데이터를 가져오려면 Azure AD에서 Graph API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-166">To get data about the user, use the Graph API from Azure AD.</span></span> <span data-ttu-id="4906f-167">Graph API는 개별 사용자를 포함하여 조직에 대한 데이터를 가져오는 데 사용할 수 있는 안전한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-167">The Graph API is a secure webservice that you can use to grab data about your organization, including individual users.</span></span> <span data-ttu-id="4906f-168">이 방법은 다음을 보장하므로 토큰의 중요한 미리 필터링하는 것보다 더 나은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-168">This approach is better than pre-filling sensitive data in tokens, because it ensures that:</span></span>
    > * <span data-ttu-id="4906f-169">데이터를 요청하는 사용자에게 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-169">The users who ask for the data are authorized.</span></span>
    > * <span data-ttu-id="4906f-170">우연히 토큰(예: 탈옥된 휴대폰 캐시 또는 데스크톱의 웹 브라우저 캐시)을 손에 넣더라도 사용자 또는 조직에 대한 중요 세부 정보는 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-170">Anyone who might happen to grab the token (from a jailbroken phone or web-browser cache on a desktop, for example) cannot obtain important details about the user or the organization.</span></span>

<span data-ttu-id="4906f-171">이 작업을 위한 일부 Java 파일을 작성하려면</span><span class="sxs-lookup"><span data-stu-id="4906f-171">To write some Java files for this work:</span></span>

1. <span data-ttu-id="4906f-172">adal4jsample이라는 루트 디렉터리에 모든 Java 파일을 저장하기 위한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-172">Create a folder in your root directory called adal4jsample to store all the Java files.</span></span>

    <span data-ttu-id="4906f-173">이 예제에서는 Java 파일에 네임스페이스 com.microsoft.aad.adal4jsample을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-173">In this example, you are using the namespace com.microsoft.aad.adal4jsample in the Java files.</span></span> <span data-ttu-id="4906f-174">대부분의 IDE는 이러한 용도로 중첩된 폴더 구조(예: /com/microsoft/aad/adal4jsample)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-174">Most IDEs create a nested folder structure for this purpose (for example, /com/microsoft/aad/adal4jsample).</span></span> <span data-ttu-id="4906f-175">이 작업을 수행할 수 있지만 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-175">You can do this also, but it is not necessary.</span></span>

2. <span data-ttu-id="4906f-176">이 폴더 안에 JSONHelper.java라는 파일을 만듭니다. 이 파일은 토큰에서 JSON 데이터를 구문 분석하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-176">Inside this folder, create a file called JSONHelper.java, which you'll use to help parse the JSON data from your tokens.</span></span> <span data-ttu-id="4906f-177">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-177">To create the file, paste the following code:</span></span>

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
     * This class provides the methods to parse JSON data from a JSON-formatted
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
         *            The JSON string that holds the collection
         * @return A JSON array that contains all the collection objects
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
         * @return A JSON object that contains the DirectoryObject
         * @throws Exception
         */
        public static JSONObject fetchDirectoryObjectJSONObject(JSONObject jsonObject) throws Exception {
            JSONObject jObj = new JSONObject();
            jObj = jsonObject.optJSONObject("responseMsg");
            return jObj;
        }

        /**
         * This method parses the skip token from a JSON-formatted string.
         *
         * @param jsonData
         *            The JSON-formatted string
         * @return The skipToken
         * @throws Exception
         */
        public static String fetchNextSkiptoken(JSONObject jsonObject) throws Exception {
            String skipToken = "";
            // Parse the skip token out of the string.
            skipToken = jsonObject.optJSONObject("responseMsg").optString("odata.nextLink");

            if (!skipToken.equalsIgnoreCase("")) {
                // Remove the unnecessary prefix from the skip token.
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
            // Parse the skip token out of the string.
            deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.deltaLink");
            if (deltaLink == null || deltaLink.length() == 0) {
                deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.nextLink");
                logger.info("deltaLink empty, nextLink ->" + deltaLink);

            }
            if (!deltaLink.equalsIgnoreCase("")) {
                // Remove the unnecessary prefix from the skip token.
                int index = deltaLink.indexOf("deltaLink=") + (new String("deltaLink=")).length();
                deltaLink = deltaLink.substring(index);
            }
            return deltaLink;
        }

        /**
         * This method creates a string consisting of a JSON document with all
         * the necessary elements set from the HttpServletRequest request.
         *
         * @param request
         *            The HttpServletRequest
         * @return The string containing the JSON document
         * @throws Exception
         *             If there is any error processing the request.
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
         * This is a generic method that copies the simple attribute values from an
         * argument jsonObject to an argument generic object.
         *
         * @param jsonObject
         *            The jsonObject from where the attributes are to be copied.
         * @param destObject
         *            The object where the attributes should be copied to.
         * @throws Exception
         *             Throws an Exception when the operation is unsuccessful.
         */
        public static <T> void convertJSONObjectToDirectoryObject(JSONObject jsonObject, T destObject) throws Exception {

            // Get the list of all the field names.
            Field[] fieldList = destObject.getClass().getDeclaredFields();

            // For all the declared field.
            for (int i = 0; i < fieldList.length; i++) {
                // If the field is of type String, that is
                // if it is a simple attribute.
                if (fieldList[i].getType().equals(String.class)) {
                    // Invoke the corresponding set method of the destObject using
                    // the argument taken from the jsonObject.
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

3. <span data-ttu-id="4906f-178">HttpClientHelper.java라는 파일을 만듭니다. 이 파일은 Azure AD 끝점에서 HTTP 데이터를 구문 분석하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-178">Create a file called HttpClientHelper.java, which you will use to help parse the HTTP data from your Azure AD endpoint.</span></span> <span data-ttu-id="4906f-179">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-179">To create the file, paste the following code:</span></span>

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

            // Send the http message payload to the server.
            if (payLoad != null) {
                conn.setDoOutput(true);
                OutputStreamWriter osw = new OutputStreamWriter(conn.getOutputStream());
                osw.write(payLoad);
                osw.flush();
                osw.close();
            }

            // Get the message response from the server.
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

## <a name="step-6-create-the-java-graph-api-model-files-for-basicfilter-mvc"></a><span data-ttu-id="4906f-180">6단계: Java Graph API 모델 파일 만들기(BasicFilter MVC용)</span><span class="sxs-lookup"><span data-stu-id="4906f-180">Step 6: Create the Java Graph API Model files (for BasicFilter MVC)</span></span>
<span data-ttu-id="4906f-181">앞서 설명한 대로 Graph API를 사용하여 로그인한 사용자에 대한 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-181">As indicated previously, you use the Graph API to get data about the signed-in user.</span></span> <span data-ttu-id="4906f-182">이 프로세스를 쉽게 수행할 수 있도록 디렉터리 개체를 나타내는 파일 및 사용자를 나타내는 파일을 둘 다 만들어서 Java의 OO 패턴을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-182">To make this process easy, create both a file to represent a Directory object and a file to represent the user so that the OO pattern of Java can be used.</span></span>

1. <span data-ttu-id="4906f-183">디렉터리 개체에 대한 기본 데이터를 저장하는 데 사용하는 DirectoryObject.java라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-183">Create a file called DirectoryObject.java, which you use to store basic data about any Directory object.</span></span> <span data-ttu-id="4906f-184">나중에 수행할 수 있는 다른 Graph 쿼리에 대해 이 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-184">You can use this file later for any other Graph queries you might perform.</span></span> <span data-ttu-id="4906f-185">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-185">To create the file, paste the following code:</span></span>

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

2. <span data-ttu-id="4906f-186">디렉터리에서 사용자에 대한 기본 데이터를 저장하는 데 사용하는 User.java라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-186">Create a file called User.java, which you use to store basic data about any user from the directory.</span></span> <span data-ttu-id="4906f-187">이것은 디렉터리 데이터에 대한 기본 getter 및 setter 메서드로, 다음 코드를 붙여 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-187">These are basic getter and setter methods for directory data, so you can paste the following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.security.acl.Group;
    import java.util.ArrayList;

    import javax.xml.bind.annotation.XmlRootElement;

    import org.json.JSONObject;

    /**
    *  The **User** class holds together all the members of a WAAD User entity and all the access methods and set methods.
    *  @author Azure Active Directory Contributor
    */
    @XmlRootElement
    public class User extends DirectoryObject{

        // The following are the individual private members of a User object that holds
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
        protected boolean isDeleted;  // this will move to dto

        /**
         * These four properties are for future use.
         */
        // managerDisplayname of this user.
        protected String managerDisplayname;

        // The directReports holds a list of directReports.
        private ArrayList<User> directReports;

        // The groups holds a list of group entities this user belongs to.
        private ArrayList<Group> groups;

        // The roles holds a list of role entities this user belongs to.
        private ArrayList<Group> roles;

        /**
         * The constructor for the **User** class. Initializes the dynamic lists and managerDisplayname variables.
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
         * @return The objectId of this user.
         */
        public String getObjectId() {
            return objectId;
        }

        /**
         * @param objectId The objectId to set to this User object.
         */
        public void setObjectId(String objectId) {
            this.objectId = objectId;
        }

        /**
         * @return The objectType of this user.
         */
        public String getObjectType() {
            return objectType;
        }

        /**
         * @param objectType The objectType to set to this User object.
         */
        public void setObjectType(String objectType) {
            this.objectType = objectType;
        }

        /**
         * @return The userPrincipalName of this user.
         */
        public String getUserPrincipalName() {
            return userPrincipalName;
        }

        /**
         * @param userPrincipalName The userPrincipalName to set to this User object.
         */
        public void setUserPrincipalName(String userPrincipalName) {
            this.userPrincipalName = userPrincipalName;
        }

        /**
         * @return The usageLocation of this user.
         */
        public String getUsageLocation() {
            return usageLocation;
        }

        /**
         * @param usageLocation The usageLocation to set to this User object.
         */
        public void setUsageLocation(String usageLocation) {
            this.usageLocation = usageLocation;
        }

        /**
         * @return The telephoneNumber of this user.
         */
        public String getTelephoneNumber() {
            return telephoneNumber;
        }

        /**
         * @param telephoneNumber The telephoneNumber to set to this User object.
         */
        public void setTelephoneNumber(String telephoneNumber) {
            this.telephoneNumber = telephoneNumber;
        }

        /**
         * @return The surname of this user.
         */
        public String getSurname() {
            return surname;
        }

        /**
         * @param surname The surname to set to this User object.
         */
        public void setSurname(String surname) {
            this.surname = surname;
        }

        /**
         * @return The streetAddress of this user.
         */
        public String getStreetAddress() {
            return streetAddress;
        }

        /**
         * @param streetAddress The streetAddress to set to this user.
         */
        public void setStreetAddress(String streetAddress) {
            this.streetAddress = streetAddress;
        }

        /**
         * @return The state of this user.
         */
        public String getState() {
            return state;
        }

        /**
         * @param state The state to set to this User object.
         */
        public void setState(String state) {
            this.state = state;
        }

        /**
         * @return The preferredLanguage of this user.
         */
        public String getPreferredLanguage() {
            return preferredLanguage;
        }

        /**
         * @param preferredLanguage The preferredLanguage to set to this user.
         */
        public void setPreferredLanguage(String preferredLanguage) {
            this.preferredLanguage = preferredLanguage;
        }

        /**
         * @return The postalCode of this user.
         */
        public String getPostalCode() {
            return postalCode;
        }

        /**
         * @param postalCode The postalCode to set to this user.
         */
        public void setPostalCode(String postalCode) {
            this.postalCode = postalCode;
        }

        /**
         * @return The physicalDeliveryOfficeName of this user.
         */
        public String getPhysicalDeliveryOfficeName() {
            return physicalDeliveryOfficeName;
        }

        /**
         * @param physicalDeliveryOfficeName The physicalDeliveryOfficeName to set to this User object.
         */
        public void setPhysicalDeliveryOfficeName(String physicalDeliveryOfficeName) {
            this.physicalDeliveryOfficeName = physicalDeliveryOfficeName;
        }

        /**
         * @return The passwordPolicies of this user.
         */
        public String getPasswordPolicies() {
            return passwordPolicies;
        }

        /**
         * @param passwordPolicies The passwordPolicies to set to this User object.
         */
        public void setPasswordPolicies(String passwordPolicies) {
            this.passwordPolicies = passwordPolicies;
        }

        /**
         * @return The mobile of this user.
         */
        public String getMobile() {
            return mobile;
        }

        /**
         * @param mobile The mobile to set to this User object.
         */
        public void setMobile(String mobile) {
            this.mobile = mobile;
        }

        /**
         * @return The password of this user.
         */
        public String getPassword() {
            return password;
        }

        /**
         * @param password The mobile to set to this User object.
         */
        public void setPassword(String password) {
            this.password = password;
        }

        /**
         * @return The mail of this user.
         */
        public String getMail() {
            return mail;
        }

        /**
         * @param mail The mail to set to this User object.
         */
        public void setMail(String mail) {
            this.mail = mail;
        }

        /**
         * @return The MailNickname of this user.
         */
        public String getMailNickname() {
            return mailNickname;
        }

        /**
         * @param mail The MailNickname to set to this User object.
         */
        public void setMailNickname(String mailNickname) {
            this.mailNickname = mailNickname;
        }

        /**
         * @return The jobTitle of this user.
         */
        public String getJobTitle() {
            return jobTitle;
        }

        /**
         * @param jobTitle The jobTitle to set to this User object.
         */
        public void setJobTitle(String jobTitle) {
            this.jobTitle = jobTitle;
        }

        /**
         * @return The givenName of this user.
         */
        public String getGivenName() {
            return givenName;
        }

        /**
         * @param givenName The givenName to set to this User object.
         */
        public void setGivenName(String givenName) {
            this.givenName = givenName;
        }

        /**
         * @return The facsimileTelephoneNumber of this user.
         */
        public String getFacsimileTelephoneNumber() {
            return facsimileTelephoneNumber;
        }

        /**
         * @param facsimileTelephoneNumber The facsimileTelephoneNumber to set to this User object.
         */
        public void setFacsimileTelephoneNumber(String facsimileTelephoneNumber) {
            this.facsimileTelephoneNumber = facsimileTelephoneNumber;
        }

        /**
         * @return The displayName of this user.
         */
        public String getDisplayName() {
            return displayName;
        }

        /**
         * @param displayName The displayName to set to this User object.
         */
        public void setDisplayName(String displayName) {
            this.displayName = displayName;
        }

        /**
         * @return The dirSyncEnabled of this user.
         */
        public String getDirSyncEnabled() {
            return dirSyncEnabled;
        }

        /**
         * @param dirSyncEnabled The dirSyncEnabled to set to this User object.
         */
        public void setDirSyncEnabled(String dirSyncEnabled) {
            this.dirSyncEnabled = dirSyncEnabled;
        }

        /**
         * @return The department of this user.
         */
        public String getDepartment() {
            return department;
        }

        /**
         * @param department The department to set to this User object.
         */
        public void setDepartment(String department) {
            this.department = department;
        }

        /**
         * @return The lastDirSyncTime of this user.
         */
        public String getLastDirSyncTime() {
            return lastDirSyncTime;
        }

        /**
         * @param lastDirSyncTime The lastDirSyncTime to set to this User object.
         */
        public void setLastDirSyncTime(String lastDirSyncTime) {
            this.lastDirSyncTime = lastDirSyncTime;
        }

        /**
         * @return The country of this user.
         */
        public String getCountry() {
            return country;
        }

        /**
         * @param country The country to set to this user.
         */
        public void setCountry(String country) {
            this.country = country;
        }

        /**
         * @return The city of this user.
         */
        public String getCity() {
            return city;
        }

        /**
         * @param city The city to set to this user.
         */
        public void setCity(String city) {
            this.city = city;
        }

        /**
         * @return The accountEnabled attribute of this user.
         */
        public String getAccountEnabled() {
            return accountEnabled;
        }

        /**
         * @param accountEnabled The accountEnabled to set to this user.
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
    * The DirectReports class holds the essential data for a single DirectReport entry. That is,
    * it holds the displayName and the objectId of the direct entry. It also provides the
    * access methods to set or get the displayName and the ObjectId of this entry.
    */
    //class DirectReport extends User{
    //
    //    private String displayName;
    //    private String objectId;
    //     
    //    /**
    //     * Two arguments Constructor for the DirectReport class.
    //     * @param displayName
    //     * @param objectId
    //     */
    //    public DirectReport(String displayName, String objectId){
    //        this.displayName = displayName;
    //        this.objectId = objectId;
    //    }
    //
    //    /**
    //     * @return The displayName of this direct report entry.
    //     */
    //    public String getDisplayName() {
    //        return displayName;
    //    }
    //
    //    
    //    /**
    //     *  @return The objectId of this direct report entry.
    //     */
    //    public String getObjectId() {
    //        return objectId;
    //    }
    //
    //}

    ```

## <a name="step-7-create-the-authentication-model-and-controller-files-for-basicfilter"></a><span data-ttu-id="4906f-188">7단계: 인증 모델 및 컨트롤러 파일 만들기(BasicFilter용)</span><span class="sxs-lookup"><span data-stu-id="4906f-188">Step 7: Create the authentication model and controller files (for BasicFilter)</span></span>
<span data-ttu-id="4906f-189">Java가 길어질 수 있지만 작업은 거의 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-189">We acknowledge that Java can be verbose, but you're almost done.</span></span> <span data-ttu-id="4906f-190">BasicFilter 서블릿을 작성하여 요청을 처리하기 전에 ADAL4J에 필요한 추가 도우미 파일을 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-190">Before you write the BasicFilter servlet to handle the requests, you need to write some more helper files that the ADAL4J needs.</span></span>

1. <span data-ttu-id="4906f-191">로그인된 사용의 상태를 확인하는 데 사용하는 메서드를 제공하는 AuthHelper.java라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-191">Create a file called AuthHelper.java, which will give you methods to use to determine the state of the signed-in user.</span></span> <span data-ttu-id="4906f-192">이러한 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-192">The methods include:</span></span>

 * <span data-ttu-id="4906f-193">**isAuthenticated()**: 사용자가 로그인했는지 여부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-193">**isAuthenticated()**: Returns whether the user is signed in.</span></span>
 * <span data-ttu-id="4906f-194">**containsAuthenticationData()**: 토큰에 데이터가 있는지 여부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-194">**containsAuthenticationData()**: Returns whether the token has data.</span></span>
 * <span data-ttu-id="4906f-195">**isAuthenticationSuccessful()**: 사용자에 대한 인증이 성공적으로 수행되었는지 여부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-195">**isAuthenticationSuccessful()**: Returns whether the authentication was successful for the user.</span></span>

 <span data-ttu-id="4906f-196">AuthHelper.java 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-196">To create the AuthHelper.java file, paste the following code:</span></span>

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

2. <span data-ttu-id="4906f-197">ADAL4J에 필요한 변경할 수 없는 일부 변수를 제공하는 AuthParameterNames.java라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-197">Create a file called AuthParameterNames.java, which gives you some immutable variables that the ADAL4J requires.</span></span> <span data-ttu-id="4906f-198">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-198">To create the file, paste the following code:</span></span>

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

3. <span data-ttu-id="4906f-199">MVC 패턴의 컨트롤러에 해당하는 AadController.java라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-199">Create a file called AadController.java, which is the controller of your MVC pattern.</span></span> <span data-ttu-id="4906f-200">이 파일은 JSP 컨트롤러를 제공하고 앱에 대한 보안/aad URL 끝점을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-200">The file gives you the JSP controller and exposes the secure/aad URL endpoint for the app.</span></span> <span data-ttu-id="4906f-201">또한 이 파일에는 Graph 쿼리도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-201">The file also includes the graph query.</span></span> <span data-ttu-id="4906f-202">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-202">To create the file, paste the following code:</span></span>

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
            // Set the appropriate header fields in the request header.
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

## <a name="step-8-create-the-basicfilter-file-for-basicfilter-mvc"></a><span data-ttu-id="4906f-203">8단계: BasicFilter 파일 만들기(BasicFilter MVC용)</span><span class="sxs-lookup"><span data-stu-id="4906f-203">Step 8: Create the BasicFilter file (for BasicFilter MVC)</span></span>
<span data-ttu-id="4906f-204">이제 JSP 보기 파일의 요청을 처리하는 BasicFilter.java 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-204">You can now create the BasicFilter.java file, which handles the requests from the JSP View files.</span></span> <span data-ttu-id="4906f-205">이 파일을 만들려면 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-205">To create the file, paste the following code:</span></span>

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
                    // if authenticated, how to check for valid session?
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

<span data-ttu-id="4906f-206">이 서블릿은 ADAL4J가 앱에서 실행할 것으로 예상하는 모든 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-206">This servlet exposes all the methods that the ADAL4J will expect from the app to run.</span></span> <span data-ttu-id="4906f-207">이러한 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-207">The methods include:</span></span>

* <span data-ttu-id="4906f-208">**getAccessTokenFromClientCredentials()**: 암호에서 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-208">**getAccessTokenFromClientCredentials()**: Gets the access token from the secret.</span></span>
* <span data-ttu-id="4906f-209">**getAccessTokenFromRefreshToken()**: 새로 고침 토큰에서 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-209">**getAccessTokenFromRefreshToken()**: Gets the access token from a refresh token.</span></span>
* <span data-ttu-id="4906f-210">**getAccessToken()**: 사용하는 OpenID Connect 흐름에서 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-210">**getAccessToken()**: Gets the access token from an OpenID Connect flow (which you use).</span></span>
* <span data-ttu-id="4906f-211">**createSessionPrincipal()**: Graph API 액세스에 사용할 세션 보안 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-211">**createSessionPrincipal()**: Creates a session principal to use for Graph API access.</span></span>
* <span data-ttu-id="4906f-212">**getRedirectUrl()**: 포털에 입력한 값과 비교하기 위해 redirectURL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-212">**getRedirectUrl()**: Gets the redirectURL to compare it with the value you entered in the portal.</span></span>

## <a name="step-9-compile-and-run-the-sample-in-tomcat"></a><span data-ttu-id="4906f-213">9단계: Tomcat에서 샘플 컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="4906f-213">Step 9: Compile and run the sample in Tomcat</span></span>

1. <span data-ttu-id="4906f-214">루트 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-214">Change to your root directory.</span></span>
2. <span data-ttu-id="4906f-215">`maven`을 사용하여 함께 사용할 샘플을 빌드하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-215">To build the sample you just put together by using `maven`, run the following command:</span></span>

    `$ mvn package`

 <span data-ttu-id="4906f-216">이 명령은 종속성에 대해 작성한 pom.xml 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-216">This command uses the pom.xml file that you wrote for dependencies.</span></span>

<span data-ttu-id="4906f-217">이제 adal4jsample.war 파일이 /targets 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-217">You should now have a adal4jsample.war file in your /targets directory.</span></span> <span data-ttu-id="4906f-218">Tomcat 컨테이너에 파일을 배포하고 http://localhost:8080/adal4jsample/ URL을 방문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-218">You can deploy the file in your Tomcat container and visit the http://localhost:8080/adal4jsample/ URL.</span></span>

> [!NOTE]
> <span data-ttu-id="4906f-219">최신 Tomcat 서버를 사용하여 .war 파일을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-219">You can easily deploy a .war file with the latest Tomcat servers.</span></span> <span data-ttu-id="4906f-220">http://localhost:8080/manager/로 이동하고 adal4jsample.war 파일 업로드에 대 한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-220">Go to http://localhost:8080/manager/, and follow the instructions for uploading the adal4jsample.war file.</span></span> <span data-ttu-id="4906f-221">올바른 끝점을 사용하여 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-221">It will autodeploy for you with the correct endpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4906f-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4906f-222">Next steps</span></span>
<span data-ttu-id="4906f-223">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 Java 앱이 작동하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-223">You now have a working Java app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the users.</span></span> <span data-ttu-id="4906f-224">아직 사용자로 테넌트를 채우지 않은 경우 지금 채우는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-224">If you haven't already populated your tenant with users, now is a good time to do so.</span></span>

<span data-ttu-id="4906f-225">추가 참조를 위해서는 다음 두 가지 방법 중 하나로 완성된 샘플(사용자 구성 값 제외)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-225">For additional reference, you can get the completed sample (without your configuration values) in either of two ways:</span></span>

* <span data-ttu-id="4906f-226">[.zip 파일](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-226">Download it as a [.zip file](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip).</span></span>
* <span data-ttu-id="4906f-227">다음 명령을 입력하여 GitHub에서 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="4906f-227">Clone the file from GitHub by entering the following command:</span></span>

 ```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```
