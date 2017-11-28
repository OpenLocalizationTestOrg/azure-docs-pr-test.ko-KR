---
title: "aaaCreate hello Azure SDK를 사용 하 여 Java 용 Azure 앱 서비스의 웹 앱"
description: "Toocreate 프로그래밍 방식으로 사용 하 여 Azure 앱 서비스 웹 앱의 Azure SDK for Java hello 방법에 대해 알아봅니다."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="3427b-103">Java 용 Azure SDK hello를 사용 하 여 Azure 앱 서비스의 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="3427b-104">개요</span><span class="sxs-lookup"><span data-stu-id="3427b-104">Overview</span></span>
<span data-ttu-id="3427b-105">이 연습에서는 toocreate는 Azure SDK for Java 응용 프로그램의 웹 앱을 만드는 [Azure 앱 서비스][Azure App Service], 다음 응용 프로그램 tooit를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="3427b-106">두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-106">It consists of two parts:</span></span>

* <span data-ttu-id="3427b-107">1 부 방법을 toobuild Java 응용 프로그램을 만드는 웹 응용 프로그램 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="3427b-108">2 부에서는 방법을 toocreate 간단한 "Hello World" JSP 응용 프로그램을 다음 FTP 사용 하 여 클라이언트 toodeploy 코드 tooApp 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3427b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3427b-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="3427b-110">소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="3427b-110">Software Installations</span></span>
<span data-ttu-id="3427b-111">이 문서에 응용 프로그램 코드 AzureWebDemo hello를 사용 하 여 설치할 수 있는 Azure Java SDK 0.7.0를 사용 하 여 쓴 hello [웹 플랫폼 설치 관리자] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="3427b-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="3427b-112">또한 있는지 toouse hello 최신 버전의 확인 hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3427b-113">Hello SDK를 설치한 후 실행 하 여 hello 종속성 Eclipse 프로젝트에서 업데이트 **인덱스 업데이트** 에 **Maven 저장소**, hello hello에 각 패키지의 최신 버전을 다시 추가  **종속성** 창.</span><span class="sxs-lookup"><span data-stu-id="3427b-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="3427b-114">클릭 하 여 Eclipse에서 설치 된 소프트웨어의 hello 버전을 확인할 수 **도움말 > 설치 세부 정보**; 하면 해야가 적어도 hello 다음 버전:</span><span class="sxs-lookup"><span data-stu-id="3427b-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="3427b-115">Java용 Microsoft Azure 라이브러리 패키지 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="3427b-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="3427b-116">Java EE Developers용 Eclipse IDE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="3427b-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="3427b-117">Azure에서 클라우드 리소스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="3427b-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="3427b-118">이 절차를 시작 하기 전에 toohave 활성 Azure 구독 필요 하 고 Active Directory (AD) Azure에서 기본값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="3427b-119">Azure에 Active Directory(AD) 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="3427b-120">Hello에 로그인 하면 않는 아직 없는 경우 Active Directory (AD) Azure 구독에서 [Azure 클래식 포털] [ Azure classic portal] Microsoft 계정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="3427b-121">여러 구독이 있는 경우 클릭 **구독** 및 기본 디렉터리 선택 hello hello 구독에 대 한 원하는 toouse이이 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="3427b-122">클릭 **적용** tooswitch toothat 구독 보기.</span><span class="sxs-lookup"><span data-stu-id="3427b-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="3427b-123">선택 **Active Directory** hello 왼쪽 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="3427b-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="3427b-124">**새로 만들기 > 디렉터리 > 사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="3427b-125">**디렉터리 추가**에서 **새 디렉터리 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="3427b-126">**이름**에 디렉터리 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="3427b-127">**도메인**에서 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="3427b-128">디렉터리를 사용 하 여 기본적으로 포함 되는 기본 도메인 이름 hello 형식은 `<domain_name>.onmicrosoft.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="3427b-129">Hello 디렉터리 이름 또는 사용자가 소유한 다른 도메인 이름에 따라 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="3427b-130">나중에, 조직에서 이미 사용하는 다른 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="3427b-131">**국가 또는 지역**에서 사용자 로캘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="3427b-132">AD에 대한 자세한 내용은 [Azure AD 디렉터리란?][What is an Azure AD directory]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3427b-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="3427b-133">Azure용 관리 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="3427b-134">Azure SDK for Java hello Azure 구독을 관리 인증서 tooauthenticate를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="3427b-135">이들은 tooauthenticate hello 구독 소유자 toomanage 구독 리소스를 대신 하 여 서비스 관리 API tooact hello를 사용 하는 클라이언트 응용 프로그램을 사용 하는 X.509 v3 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="3427b-136">이 절차에서는 hello 코드는 Azure와 함께 자체 서명 된 인증서 tooauthenticate를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="3427b-137">이 절차에서는 인증서 toocreate 필요 하 고이 toohello 업로드 [Azure 클래식 포털] [ Azure classic portal] 미리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="3427b-138">이 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-138">This involves hello following steps:</span></span>

* <span data-ttu-id="3427b-139">클라이언트 인증서를 나타내는 PFX 파일을 생성하고 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="3427b-140">Hello PFX 파일에서 관리 인증서 (CER 파일)를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="3427b-141">Hello CER 파일 tooyour Azure 구독을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="3427b-142">인증서를 사용 하 여 해당 형식을 tooauthenticate을 사용 하 여 Java 하므로 hello PFX 파일 JKS를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="3427b-143">Toohello 로컬 JKS 파일 참조는 hello 응용 프로그램의 인증 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="3427b-144">이 절차를 완료 하면 hello CER 인증서는 Azure 구독에 있으며 hello JKS 인증서는 로컬 드라이브에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="3427b-145">관리 인증서에 대한 자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드][Create and Upload a Management Certificate for Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3427b-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="3427b-146">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-146">Create a certificate</span></span>
<span data-ttu-id="3427b-147">toocreate 고유한 자체 서명 된 인증서를 운영 체제에서 명령 콘솔을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="3427b-148">**참고:** 이 명령을 실행 하는 hello 컴퓨터 hello JDK 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="3427b-149">또한 hello 경로 toohello keytool hello JDK 설치 하는 hello 위치에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="3427b-150">자세한 내용은 참조 [키 및 인증서 관리 도구 (keytool)] [ Key and Certificate Management Tool (keytool)] hello Java 온라인 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="3427b-151">toocreate hello.pfx 파일:</span><span class="sxs-lookup"><span data-stu-id="3427b-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="3427b-152">toocreate hello.cer 파일:</span><span class="sxs-lookup"><span data-stu-id="3427b-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="3427b-153">설명:</span><span class="sxs-lookup"><span data-stu-id="3427b-153">where:</span></span>

* <span data-ttu-id="3427b-154">`<java-install-dir>`Java 설치한 hello 경로 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="3427b-155">`<keystore-id>`hello keystore 항목 식별자입니다 (예를 들어 `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="3427b-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="3427b-156">`<cert-store-dir>`toostore 인증서 원하는 hello 경로 toohello 디렉터리 (예를 들어 `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="3427b-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="3427b-157">`<cert-file-name>`hello hello 인증서 파일 이름입니다 (예를 들어 `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="3427b-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="3427b-158">`<password>`tooprotect hello 인증서;를 선택 하는 hello 암호 이 길이 최소 6 자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="3427b-159">권장하지는 않지만 암호 없이 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="3427b-160">`<dname>`별칭을와 관련 된 hello X.500 고유 이름의 toobe 이며 hello 자체 서명 된 인증서의 주체 필드 및 hello 발급자로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="3427b-161">자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드][Create and Upload a Management Certificate for Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3427b-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="3427b-162">Hello 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="3427b-162">Upload hello certificate</span></span>
<span data-ttu-id="3427b-163">자체 서명 된 인증서 tooAzure tooupload 이동 toohello **설정** hello 클래식 포털에서 페이지 클릭 hello **관리 인증서** 탭 합니다. 클릭 **업로드** hello hello 맨 아래에 만든 hello CER 파일의 위치 toohello 이동한 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="3427b-164">JKS hello PFX 파일 변환</span><span class="sxs-lookup"><span data-stu-id="3427b-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="3427b-165">Hello (관리자로 실행) 하는 Windows 명령 프롬프트에서에서 cd toohello 포함 된 디렉터리 인증서 hello 하 고 hello 다음, 명령을 실행 합니다. 여기서 `<java-install-dir>` 는 Java를 컴퓨터에 설치 하는 hello 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="3427b-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="3427b-166">메시지가 표시 되 면 입력 hello 대상 키 저장소 암호입니다. hello JKS 파일에 대 한 hello 암호가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="3427b-167">메시지가 표시 되 면 입력 hello 소스 키 저장소 암호입니다. 이것이 hello PFX 파일에 대 한 지정한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="3427b-168">hello 두 개의 암호가 같은 hello toobe가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="3427b-169">권장하지는 않지만 암호 없이 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="3427b-170">웹 앱 만들기 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="3427b-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="3427b-171">만들 hello Eclipse 작업 공간 및 Maven 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3427b-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="3427b-172">이 섹션의 작업 영역 및 hello 웹 앱 만들기 응용 프로그램에서 AzureWebDemo 라는 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="3427b-173">새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-173">Create a new Maven project.</span></span> <span data-ttu-id="3427b-174">**파일 > 새로 만들기 > Maven 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="3427b-175">**새 Maven 프로젝트**에서 **간단한 프로젝트 만들기** 및 **기본 작업 영역 위치 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="3427b-176">두 번째 페이지의 hello **새 Maven 프로젝트**, hello 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="3427b-177">그룹 ID: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="3427b-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="3427b-178">아티팩트 ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="3427b-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="3427b-179">버전: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="3427b-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="3427b-180">패키징: jar</span><span class="sxs-lookup"><span data-stu-id="3427b-180">Packaging: jar</span></span>
   * <span data-ttu-id="3427b-181">이름: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="3427b-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="3427b-182">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-182">Click **Finish**.</span></span>
3. <span data-ttu-id="3427b-183">Pom.xml 파일을 hello 새 프로젝트의 프로젝트 탐색기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="3427b-184">선택 hello **종속성** 탭 합니다. 새 프로젝트이면, 아직 패키지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="3427b-185">열기 hello Maven 리포지토리를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="3427b-186">**창 > 보기 표시 > 기타 > Maven > Maven 리포지토리**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="3427b-187">hello **Maven 저장소** 보기가 hello IDE hello 맨 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="3427b-188">열기 **전역 저장소**를 마우스 오른쪽 단추로 클릭 hello **중앙** 리포지토리와 선택 **인덱스 다시 작성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="3427b-189">이 단계는 hello 연결 속도에 따라 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="3427b-190">Hello 인덱스 다시 작성 하는 경우 패키지가 표시 됩니다 hello Microsoft Azure의 hello **중앙** Maven 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="3427b-191">**종속성**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="3427b-192">**그룹 ID 입력...**에 `azure-management`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="3427b-193">기본 관리 및 응용 프로그램 서비스 웹 앱 관리에 대 한 hello 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="3427b-194">**참고:** toore 필요한 새 버전 릴리스 후 hello 종속성을 업데이트 하는 경우-각 hello 종속성이이 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="3427b-195">클릭 한 후 **추가** hello 새 버전 번호로 hello 나타나는 각 종속성을 선택 하 고 **종속성** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="3427b-196">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-196">Click **OK**.</span></span> <span data-ttu-id="3427b-197">hello에 표시 한 다음 Azure 패키지 hello **종속성** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="3427b-198">Azure SDK 호출 hello 하 여 Java 코드 tooCreate 웹 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="3427b-199">다음으로, Java toocreate hello 앱 서비스 웹 앱에 대 한 hello Azure SDK의에서 Api를 호출 하는 hello 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="3427b-200">Java 클래스 toocontain hello 주 진입점 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="3427b-201">프로젝트 탐색기에서 hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **새로 만들기 > 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="3427b-202">**새로운 Java 클래스**, hello 클래스 이름을 `WebCreator` hello를 확인 하 고 **public static void main** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="3427b-203">hello 선택 항목은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="3427b-204">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-204">Click **Finish**.</span></span> <span data-ttu-id="3427b-205">hello WebCreator.java 파일이 프로젝트 탐색기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="3427b-206">앱 서비스 웹 앱 hello Azure API tooCreate를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="3427b-207">필요한 가져오기 추가</span><span class="sxs-lookup"><span data-stu-id="3427b-207">Add necessary imports</span></span>
<span data-ttu-id="3427b-208">WebCreator.java에서 다음 imports; hello를 추가 합니다. 이러한 imports Azure Api를 사용 하기 위한 hello에 대 한 액세스 tooclasses 관리 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="3427b-209">Hello 주 진입점 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-209">Define hello main entry point class</span></span>
<span data-ttu-id="3427b-210">Hello AzureWebDemo 응용 프로그램의 hello 목적은 toocreate 앱 서비스 웹 앱 이기 때문에이 응용 프로그램에 대 한 hello 주 클래스 이름을 `WebAppCreator`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="3427b-211">이 클래스는 hello Azure 서비스 관리 API toocreate hello 웹 응용 프로그램을 호출 하는 hello 주 항목 지점 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="3427b-212">Hello hello 웹 앱 및 웹 공간에 대 한 매개 변수 정의 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="3427b-213">사용자 고유의 Azure 구독 ID 및 인증서 정보 tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="3427b-214">설명:</span><span class="sxs-lookup"><span data-stu-id="3427b-214">where:</span></span>

* <span data-ttu-id="3427b-215">`<subscription-id>`toocreate hello 리소스 원하는 hello Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="3427b-216">`<certificate-store-path>`로컬 인증서 저장소 디렉터리의 hello 경로 파일 이름을 toohello JKS 파일이입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="3427b-217">예를 들어, Linux에 대해서는 `C:/Certificates/CertificateName.jks`이며 Windows에 대해서는 `C:\Certificates\CertificateName.jks`입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="3427b-218">`<certificate-password>`JKS 인증서를 만들 때 지정한 hello 암호가입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="3427b-219">`webAppName`선택; 이름 이 절차에서는 hello 이름 `WebDemoWebApp`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="3427b-220">전체 도메인 이름을 hello는 hello `webAppName` hello로 `domainName` 추가 좋으므로 사례에서는 hello 전체 도메인은 `webdemowebapp.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="3427b-221">`domainName` 위와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="3427b-222">`webSpaceName`hello에 정의 된 hello 값 중 하나 여야 합니다 [WebSpaceNames] [ WebSpaceNames] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="3427b-223">`appServicePlanName` 위와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="3427b-224">**참고:** 될 때마다가 응용이 프로그램 실행의 toochange hello 값이 필요한 `webAppName` 및 `appServicePlanName` (또는 hello Azure 포털에서 웹 앱 hello 삭제) hello 응용 프로그램을 다시 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3427b-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="3427b-225">그렇지 않으면 hello 동일한 리소스 이미 존재 하므로 Azure에서 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="3427b-226">Hello 웹 생성 방법 정의</span><span class="sxs-lookup"><span data-stu-id="3427b-226">Define hello web creation method</span></span>
<span data-ttu-id="3427b-227">다음으로 메서드 toocreate hello 웹 응용 프로그램을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="3427b-228">이 방법에서는 `createWebApp`, hello 웹 응용 프로그램의 성능과 hello 웹 공간 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="3427b-229">또한 만들어지고 hello에 정의 된 hello 앱 서비스 웹 앱 관리 클라이언트를 구성 [WebSiteManagementClient] [ WebSiteManagementClient] 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="3427b-230">hello 관리 클라이언트는 키 toocreating 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="3427b-231">Hello 서비스 관리 API를 호출 하 여 응용 프로그램 toomanage 웹 앱 (예: 만들기, update 및 delete 작업 수행)을 허용 하는 RESTful 웹 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="3427b-232">hello 코드 성공 또는 실패를 나타내는 hello 응답의 HTTP 상태 hello을 출력 하 고 성공 하면 웹 앱을 만들 hello의 hello 이름을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="3427b-233">Hello main () 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-233">Define hello main() method</span></span>
<span data-ttu-id="3427b-234">해당 호출 createWebApp() toocreate hello 웹 앱 hello main () 메서드 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="3427b-235">마지막으로 `main`에서 `createWebApp`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="3427b-236">Hello 응용 프로그램을 실행 하 고 웹 응용 프로그램 만들기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="3427b-237">응용 프로그램을 실행 하는 tooverify 클릭 **실행 > 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="3427b-238">Hello 응용 프로그램 실행이 완료 된 hello Eclipse 콘솔에 출력 뒤 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="3427b-239">Hello Azure 클래식 포털에 로그인 하 고 클릭 **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="3427b-240">hello 새 웹 앱은 몇 분 안에 hello 웹 응용 프로그램 목록에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="3427b-241">응용 프로그램 toohello 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="3427b-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="3427b-242">AzureWebDemo을 실행 하 고 클릭 hello 새 웹 앱, hello 클래식 포털에 로그인을 만든 후 **웹 앱**를 선택 하 고 **WebDemoWebApp** hello에 **웹 앱** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="3427b-243">Hello 웹 앱의 대시보드 페이지에서 클릭 **찾아보기** (hello URL을 클릭 하거나 `webdemowebapp.azurewebsites.net`) toonavigate tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="3427b-244">콘텐츠 게시 toohello 웹 응용 프로그램을 아직 되지 않았기 때문에 빈 자리 표시자 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="3427b-245">그런 다음 "Hello World" 응용 프로그램을 만들고 toohello 웹 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="3427b-246">JSP Hello World 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="3427b-247">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3427b-247">Create hello application</span></span>
<span data-ttu-id="3427b-248">응용 프로그램 toohello 웹 toodeploy hello 어떻게 순서 toodemonstrate에서 절차를 수행 방법을 보여 줍니다 toocreate 간단한 "Hello World" Java 응용 프로그램 및 toohello 응용 프로그램을 만들 앱 서비스 웹 앱을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="3427b-249">**파일 > 새로 만들기 > 동적 웹 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="3427b-250">이름을 `JSPHello`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-250">Name it `JSPHello`.</span></span> <span data-ttu-id="3427b-251">Toochange 필요 하지 않으면이 대화 상자에 있는 다른 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="3427b-252">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="3427b-253">프로젝트 탐색기에서 확장 hello **JSPHello** 프로젝트를 마우스 오른쪽 단추로 클릭 **WebContent**, 클릭 **새로 만들기 > JSP 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="3427b-254">Hello JSP 파일 새로 만들기 대화 상자에서 hello 새 파일 이름을 `index.jsp`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="3427b-255">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-255">Click **Next**.</span></span>
3. <span data-ttu-id="3427b-256">Hello에 **JSP 템플릿 선택** 대화 상자에서 **새 JSP 파일 (html)** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="3427b-257">Index.jsp에서 hello 코드 hello에 다음 추가 `<head>` 및 `<body>` 태그 섹션:</span><span class="sxs-lookup"><span data-stu-id="3427b-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="3427b-258">Localhost에 hello Hello World 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="3427b-259">이 응용 프로그램을 실행 하기 전에 몇 가지 속성 tooconfigure 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="3427b-260">마우스 오른쪽 단추로 클릭 hello **JSPHello** 프로젝트를 마우스 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="3427b-261">Hello에 **속성** 대화: 선택 **Java 빌드 경로**선택, hello **순서 및 내보내기** 탭 **JRE 시스템 라이브러리**, 클릭 **를** toomove 것 hello 목록의 toohello 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="3427b-262">Hello에도 **속성** 대화: 선택 **대상으로 하는 런타임** 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="3427b-263">Hello에 **서버 런타임 환경** 대화 상자에서 서버와 같은 선택 **Apache Tomcat v7.0** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="3427b-264">Hello에 **Tomcat 서버** 대화 상자에서 **이름** 너무`Apache Tomcat v7.0`, 설정 및 **Tomcat 설치 디렉터리** hello 버전을 설치한 toohello 디렉터리 Tomcat 서버 toouse 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="3427b-265">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-265">Click **Finish**.</span></span>
5. <span data-ttu-id="3427b-266">돌아옵니다 toohello **대상으로 하는 런타임** hello의 페이지 **속성** 대화입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="3427b-267">**Apache Tomcat v7.0**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="3427b-268">Hello Eclipse에서에서 **실행** 메뉴를 클릭 하 여 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="3427b-269">Hello에 **실행** 대화 상자에서 **서버에서 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="3427b-270">Hello에 **서버에서 실행** 대화 상자에서 **Tomcat 서버 v7.0**:</span><span class="sxs-lookup"><span data-stu-id="3427b-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="3427b-271">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-271">Click **Finish**.</span></span>
7. <span data-ttu-id="3427b-272">응용 프로그램이 실행 될 때는 hello, hello 표시 되어야 **JSPHello** Eclipse에서 localhost 창에 표시 된 페이지 (`http://localhost:8080/JSPHello/`) 표시, 아래와 같은 메시지가 hello:</span><span class="sxs-lookup"><span data-stu-id="3427b-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="3427b-273">전쟁 hello 응용 프로그램 내보내기</span><span class="sxs-lookup"><span data-stu-id="3427b-273">Export hello application as a WAR</span></span>
<span data-ttu-id="3427b-274">웹 앱 toohello 배포할 수 있도록 웹 보관 파일 (WAR) 파일로 hello 웹 프로젝트 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="3427b-275">hello 다음 웹 프로젝트 파일에에서 있는 hello WebContent 폴더:</span><span class="sxs-lookup"><span data-stu-id="3427b-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="3427b-276">Hello WebContent 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="3427b-277">Hello에 **선택 내보내기** 대화 상자에서 클릭 **웹 > WAR** 클릭 한 다음 파일을 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="3427b-278">Hello에 **WAR 내보내기** 대화 상자에서 hello 현재 프로젝트에 hello src 디렉터리를 선택 하 고 hello 끝 hello WAR 파일의 hello 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="3427b-279">예:</span><span class="sxs-lookup"><span data-stu-id="3427b-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="3427b-280">WAR 파일의 배포에 대 한 자세한 내용은 참조 하십시오. [Java 응용 프로그램 tooAzure 앱 서비스 웹 앱 추가](web-sites-java-add-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="3427b-281">Hello World 응용 프로그램 사용 하 여 FTP hello 배포</span><span class="sxs-lookup"><span data-stu-id="3427b-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="3427b-282">제 3 자 FTP 클라이언트 toopublish hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="3427b-283">이 절차에서는 두 가지 옵션인: hello Kudu 콘솔; Azure에 기본 제공 및 FileZilla, 편리 하 게,이 그래픽 UI가 포함 된 널리 사용 되는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="3427b-284">**참고:** Eclipse 지원 배포 toostorage 계정 및 클라우드 서비스, 하지만 현재 tooweb 앱 배포를 지원 하지 않는 Azure 도구 키트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="3427b-285">Toostorage 계정을 배포 하 고 클라우드 서비스에 설명 된 대로 Azure 배포 프로젝트를 사용 하 여 [Hello World 응용 프로그램 만들기 azure Eclipse에서](http://msdn.microsoft.com/library/azure/hh690944.aspx), 있지만 앱이 아니라 tooweb 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="3427b-286">FTP 또는 GitHub tootransfer 파일 tooyour 웹 앱과 같은 다른 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="3427b-287">**참고:** hello Windows 명령 프롬프트 (hello FTP.EXE 있는 명령줄 유틸리티 Windows에 포함)에서 FTP를 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="3427b-288">FTP.EXE, 같은 활성 FTP를 사용 하는 FTP 클라이언트 방화벽을 통해 toowork를 자주 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="3427b-289">활성 FTP 내부 LAN 기반 주소 지정, toowhich FTP 서버 tooconnect 삭제가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="3427b-290">FTP를 사용 하 여 배포 tooan 앱 서비스 웹 앱에 대 한 자세한 내용은 다음 항목 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3427b-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="3427b-291">FTP 유틸리티를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="3427b-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="3427b-292">배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="3427b-292">Set up deployment credentials</span></span>
<span data-ttu-id="3427b-293">Hello를 실행 해야 **AzureWebDemo** 응용 프로그램 toocreate 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="3427b-294">파일 toothis 위치를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="3427b-295">Hello 클래식 포털에 로그인 하 고 클릭 **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="3427b-296">확인 **WebDemoWebApp** 웹 응용 프로그램의 hello 목록에 표시 되 고 실행 중인지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3427b-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="3427b-297">클릭 **WebDemoWebApp** tooopen 해당 **대시보드** 페이지.</span><span class="sxs-lookup"><span data-stu-id="3427b-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="3427b-298">Hello에 **대시보드** 페이지의 **빠른 보기**, 클릭 **배포 자격 증명 설정** (배포 자격 증명을 이미 보유 하는 경우이 읽지  **배포 자격 증명 재설정**).</span><span class="sxs-lookup"><span data-stu-id="3427b-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="3427b-299">배포 자격 증명은 Microsoft 계정과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="3427b-300">해야 toospecify 사용자 이름 및 암호를 toodeploy Git 및 FTP를 사용 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="3427b-301">Microsoft 계정과 연결 된 모든 Azure 구독에 이러한 자격 증명 toodeploy tooany 웹 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="3427b-302">나중에 사용할 Git 및 FTP 배포 자격 증명 hello 대화 및 레코드 hello 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="3427b-303">FTP 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="3427b-303">Get FTP connection information</span></span>
<span data-ttu-id="3427b-304">toouse FTP toodeploy 응용 프로그램 파일 toohello 새로 만든 웹 응용 프로그램에서 연결 정보 tooobtain 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="3427b-305">두 가지 tooobtain 연결 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="3427b-306">한 가지 방법은 toovisit hello 웹 앱의 **대시보드** 페이지, hello 다른 방법으로 toodownload hello 웹 앱의 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="3427b-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="3427b-307">hello 게시 프로필은 Azure 앱 서비스에서 웹 앱에 대 한 FTP 호스트 이름 및 로그온 자격 증명 등의 정보를 제공 하는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="3427b-308">이 사용자 이름 및 암호 toodeploy tooany 웹 앱이 하나만 아니라 Azure 계정 hello와 관련 된 모든 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="3427b-309">hello에 hello 웹 앱 블레이드 tooobtain FTP 연결 정보 [Azure 포털][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="3427b-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="3427b-310">아래 **Essentials**, 찾기 및 hello 복사 **FTP 호스트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="3427b-311">다음과 같은 URI를 너무 이것이`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="3427b-312">**Essentials**에서 **FTP/배포 사용자 이름**을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="3427b-313">Hello 양식 아무런 *webappname\deployment-username*; 예를 들면 `WebDemoWebApp\deployer77`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="3427b-314">hello에서 tooobtain FTP 연결 정보가 게시 프로필:</span><span class="sxs-lookup"><span data-stu-id="3427b-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="3427b-315">Hello 웹 앱 블레이드 클릭 **Get 게시 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="3427b-316">.Publishsettings 파일 tooyour 로컬 드라이브를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="3427b-317">XML 편집기나 텍스트 편집기에서 hello.publishsettings 파일을 열고 hello `<publishProfile>` 요소를 포함 하 `publishMethod="FTP"`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="3427b-318">Hello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="3427b-319">해당 hello 웹 응용 프로그램의 참고 `publishProfile` 설정 toohello FileZilla 사이트 관리자 설정을 다음과 같이 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="3427b-320">`publishUrl`와 동일 하 게 hello은 **FTP 호스트 이름**, 설정한 값에 hello **호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="3427b-321">`publishMethod="FTP"`설정 하는 수단 **프로토콜** 너무**FTP-파일 전송 프로토콜**, 및 **암호화** 너무**일반 FTP를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="3427b-322">`userName`및 `userPWD` hello 배포 자격 증명을 다시 설정할 때 지정한 사용자 이름 및 암호 값이 실제 hello에 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="3427b-323">`userName`와 동일 하 게 hello은 **배포 사용자 FTP /**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="3427b-324">매핑되는 너무**사용자** 및 **암호** FileZilla에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="3427b-325">`ftpPassiveMode="True"`수동 FTP 전송;을 사용 하 여 해당 hello FTP 사이트 의미 합니다. 선택 **수동** hello에 **전송 설정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="3427b-326">Hello 웹 앱 toohost Java 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="3427b-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="3427b-327">Hello 응용 프로그램을 게시 하기 전에 필요한 toochange 몇 가지 구성 설정을 hello 웹 앱 호스팅할 수는 Java 응용 프로그램 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="3427b-328">Hello 클래식 포털에서 toohello 웹 앱의 이동 **대시보드** 페이지 클릭 하 여 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="3427b-329">Hello에 **구성** 페이지에서 다음 설정을 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="3427b-330">**Java 버전** hello 기본값은 **오프**; select hello Java 버전 응용 프로그램이 대상; 예를 들면 1.7.0_51 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="3427b-331">이렇게 하면 되었는지도 확인 **웹 컨테이너** tooa 버전의 Tomcat 서버에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="3427b-332">**기본 문서**, index.jsp를 추가 하 고 toohello hello 목록의 맨 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="3427b-333">(웹 앱에 대 한 기본 파일 hello hostingstart.html입니다.)</span><span class="sxs-lookup"><span data-stu-id="3427b-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="3427b-334">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="3427b-335">Kudu를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="3427b-335">Publish your application using Kudu</span></span>
<span data-ttu-id="3427b-336">한 가지 방법은 toopublish hello 응용 프로그램은 toouse hello Kudu 디버그 Azure에 기본 제공 되는 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="3427b-337">Kudu는 안정적이 고 응용 프로그램 서비스 웹 앱 및 Tomcat 서버와 일치 toobe를 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="3427b-338">Hello 다음 폼의 tooa URL을 탐색 하 여 hello 웹 앱에 대 한 hello 콘솔에 액세스 하면:</span><span class="sxs-lookup"><span data-stu-id="3427b-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="3427b-339">이 절차에 대 한 hello Kudu 콘솔에 위치한 url; hello toothis 위치 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="3427b-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="3427b-340">Hello 상단 메뉴에서 선택 **디버그 콘솔 > CMD**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="3427b-341">Hello 콘솔 명령줄에서 이동 너무`/site/wwwroot` (키를 누르거나 `site`, 다음 `wwwroot` hello hello 페이지 위쪽에 표시 되는 hello 디렉터리 뷰에서):</span><span class="sxs-lookup"><span data-stu-id="3427b-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="3427b-342">**Java 버전**을 지정한 후, Tomcat 서버는 webapps 디렉터리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="3427b-343">Hello 콘솔 명령줄에서 toohello webapps 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="3427b-344">JSPHello.war 끌어 `<project-path>/JSPHello/src/` hello Kudu 디렉터리 보기 아래에 `/site/wwwroot/webapps`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="3427b-345">수행 하지 끌어 toohello "여기에 끌어 놓으십시오 tooupload 및 zip" 영역 되므로 Tomcat 압축 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="3427b-346">첫 번째 JSPHello.war에 단독으로 hello 디렉터리 영역에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="3427b-347">짧은 시간 (5 분 미만이 아마도) Tomcat 서버 압축을 풉니다 hello WAR 파일을 압축을 푼 JSPHello 디렉터리로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="3427b-348">Index.jsp에 압축 되 고 복사 여부 hello 루트 디렉터리 toosee를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="3427b-349">이 경우 백 toohello webapps 디렉터리 toosee hello 해체 JSPHello 디렉터리가 만들어졌는지 여부를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="3427b-350">이 항목이 표시되지 않으면 대기하고 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="3427b-351">FileZilla를 사용하여 응용 프로그램 게시(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3427b-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="3427b-352">Toopublish hello 응용 프로그램을 사용할 수 있는 기능도 FileZilla를 편리 하 게,이 그래픽 UI 사용 하 여 인기 있는 제 3 자 FTP 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="3427b-353">없는 경우, [http://filezilla-project.org/](http://filezilla-project.org/) 에서 FileZilla를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="3427b-354">Hello 클라이언트 사용에 대 한 자세한 내용은 참조 hello [FileZilla 설명서](https://wiki.filezilla-project.org/Documentation) 및이 블로그 항목 [FTP 클라이언트-4 부: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="3427b-355">FileZilla에서 **파일 > Site Manager**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="3427b-356">Hello에 **사이트 관리자** 대화 상자를 클릭 하 여 **새 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="3427b-357">빈 새 FTP 사이트에 표시 됩니다 **선택 항목** tooprovide 이름을 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="3427b-358">이 절차에 대한 이름을 `AzureWebDemo-FTP`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="3427b-359">Hello에 **일반** 탭 hello 다음 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="3427b-360">**호스트:** Enter hello **FTP 호스트 이름** hello 대시보드에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="3427b-361">**포트:** (이 이름을 비워둡니다 수동 전송 고 hello 서버 hello 포트 toouse를 결정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3427b-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="3427b-362">**프로토콜:** FTP 파일 전송 프로토콜</span><span class="sxs-lookup"><span data-stu-id="3427b-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="3427b-363">**암호화:** 일반 FTP 사용</span><span class="sxs-lookup"><span data-stu-id="3427b-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="3427b-364">**로그온 유형:** 일반</span><span class="sxs-lookup"><span data-stu-id="3427b-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="3427b-365">**사용자:** Enter hello 배포 hello 대시보드에서 복사한 사용자 FTP /입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="3427b-366">에 hello 폼 hello 전체 FTP 사용자 이름인 *webappname\username*합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="3427b-367">**암호:** hello 배포 자격 증명을 설정 하면 지정 된 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="3427b-368">Hello에 **전송 설정** 탭에서 **수동**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="3427b-369">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-369">Click **Connect**.</span></span> <span data-ttu-id="3427b-370">성공 FileZilla의 콘솔 표시 됩니다는 `Status: Connected` 메시지 및 문제는 `LIST` toolist hello 디렉터리 내용을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="3427b-371">Hello에 **로컬** 사이트 패널 선택 hello 원본 디렉터리에 어느 hello JSPHello.war 파일이 있으며 hello 경로 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="3427b-372">Hello에 **원격** 사이트 패널, 대상 폴더 선택 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="3427b-373">Hello WAR 파일 toohello 배포할 `webapps` hello 웹 앱의 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="3427b-374">너무 이동`/site/wwwroot`를 마우스 오른쪽 단추로 클릭 `wwwroot`를 선택 하 고 **디렉터리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="3427b-375">이름 hello 디렉터리 `webapps` 하 고 해당 디렉터리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="3427b-376">너무 JSPHello.war 전송`/site/wwwroot/webapps`합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="3427b-377">Hello에서 JSPHello.war 선택 **로컬** 파일 목록에서 마우스 오른쪽 단추로 클릭 하 고 선택 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="3427b-378">`/site/wwwroot/webapps`에 보이도록 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="3427b-379">Tomcat 서버는 자동 압축 풀기 JSPHello.war toohello webapps 디렉터리를 복사한 다음 (압축) hello hello WAR 파일의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="3427b-380">Tomcat 서버 압축을 풀지 거의 즉시 시작 되지만 오래 걸릴 수 있습니다 (시간 수) hello FTP 클라이언트에서 파일 tooappear hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="3427b-381">Hello 웹 응용 프로그램에서 hello Hello World 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="3427b-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="3427b-382">Hello WAR 파일을 업로드 하 고 Tomcat 서버에는 압축을 푼 만들어져 있는지 확인 한 후 `JSPHello` 디렉터리 찾아보기 너무`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="3427b-383">**참고:** 누르면 **찾아보기** hello 클래식 포털에서 표시 될 수 있습니다 hello 기본 웹 페이지 "Java 기반 웹 응용 프로그램에이 성공적으로 만들었습니다." 라는</span><span class="sxs-lookup"><span data-stu-id="3427b-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="3427b-384">Hello 기본 웹 페이지 대신 순서 tooview hello 응용 프로그램 출력의 toorefresh hello 웹 페이지를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="3427b-385">Hello 응용 프로그램을 실행 하는 경우 다음 출력 hello로 웹 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="3427b-386">Azure 리소스 정리</span><span class="sxs-lookup"><span data-stu-id="3427b-386">Clean up Azure resources</span></span>
<span data-ttu-id="3427b-387">이 절차에서는 앱 서비스 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="3427b-388">있는 그대로 hello 리소스에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="3427b-389">Toocontinue hello 웹 응용 프로그램을 사용 하 여 테스트 또는 개발에 대 한 제외를 중지 하거나 삭제를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="3427b-390">중지된 웹 앱은 여전히 작은 요금을 부과하지만 언제든지 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="3427b-391">웹 응용 프로그램 삭제 tooit 업로드 하는 모든 데이터를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="3427b-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
