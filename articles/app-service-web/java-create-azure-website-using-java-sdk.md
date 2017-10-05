---
title: "Java용 Azure SDK를 사용하여 Azure 앱 서비스에서 웹 앱 만들기"
description: "Java 용 Azure SDK를 사용하여 프로그래밍 방식으로 Azure 앱 서비스에 웹 앱을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="fab7b-103">Java용 Azure SDK를 사용하여 Azure 앱 서비스에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="fab7b-104">개요</span><span class="sxs-lookup"><span data-stu-id="fab7b-104">Overview</span></span>
<span data-ttu-id="fab7b-105">이 연습에서는 [Azure App Service][Azure App Service]에서 Web App을 만드는 Java 응용 프로그램용 Azure SDK를 만드는 방법을 나타낸 다음 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="fab7b-106">두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-106">It consists of two parts:</span></span>

* <span data-ttu-id="fab7b-107">1부에서는 웹 앱을 만드는 Java 응용 프로그램을 구축하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="fab7b-108">2부에서는 간단한 "Hello World" 앱을 만드는 방법을 보여준 다음, FTP 클라이언트를 사용하여 코드를 앱 서비스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fab7b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fab7b-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="fab7b-110">소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="fab7b-110">Software Installations</span></span>
<span data-ttu-id="fab7b-111">이 문서의 AzureWebDemo 응용 프로그램 코드는 Azure Java SDK 0.7.0을 사용하여 작성되었으며, [WebPI(웹 플랫폼 설치 관리자)][Web Platform Installer]를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="fab7b-112">또한, 최신 버전의 [Eclipse용 Azure Toolkit][Azure Toolkit for Eclipse]을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="fab7b-113">SDK를 설치한 후 **Maven 리포지토리**에서 **인덱스 업데이트**를 실행하여 Eclipse 프로젝트의 종속성을 업데이트한 다음 **종속성** 창에서 각 패키지의 최신 버전을 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="fab7b-114">**도움말 > 설치 세부 정보**를 클릭하여 Eclipse에 설치된 소프트웨어의 버전을 확인할 수 있습니다. 최소한 다음과 같은 버전이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="fab7b-115">Java용 Microsoft Azure 라이브러리 패키지 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="fab7b-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="fab7b-116">Java EE Developers용 Eclipse IDE 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="fab7b-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="fab7b-117">Azure에서 클라우드 리소스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="fab7b-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="fab7b-118">이 절차를 시작하기 전에 활성 Azure를 구독하고 Azure에서 기본 AD(Active Directory)를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="fab7b-119">Azure에 Active Directory(AD) 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="fab7b-120">Azure 구독에 Active Directory(AD)가 없는 경우, Microsoft 계정과 함께 [Azure 클래식 포털][Azure classic portal]로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="fab7b-121">다중 구독인 경우, **구독** 을 클릭하고 이 프로젝트에 대해 사용 하려는 구독에 대한 기본 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="fab7b-122">**적용** 을 클릭하여 해당 구독 뷰로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="fab7b-123">왼쪽 창에서 **Active Directory** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="fab7b-124">**새로 만들기 > 디렉터리 > 사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="fab7b-125">**디렉터리 추가**에서 **새 디렉터리 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="fab7b-126">**이름**에 디렉터리 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="fab7b-127">**도메인**에서 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="fab7b-128">기본적으로 디렉터리와 함께 포함된 기본 도메인 이름입니다. `<domain_name>.onmicrosoft.com` 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="fab7b-129">소유하는 다른 도메인 이름 또는 디렉터리 이름에 따라 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="fab7b-130">나중에, 조직에서 이미 사용하는 다른 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="fab7b-131">**국가 또는 지역**에서 사용자 로캘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="fab7b-132">AD에 대한 자세한 내용은 [Azure AD 디렉터리란?][What is an Azure AD directory]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="fab7b-133">Azure용 관리 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="fab7b-134">Java용 Azure SDK는 관리 인증서를 사용하여 Azure 구독으로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="fab7b-135">서비스 관리 API를 사용하여 구독 리소스를 관리하는 구독 소유자를 대신하여 역할하는 클라이언트 응용 프로그램을 인증하는데 사용하는 X.509 v3 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="fab7b-136">이 절차의 코드는 자체 서명된 인증서를 사용하여 Azure와 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="fab7b-137">이 절차는 인증서를 만들고 미리 [Azure 클래식 포털][Azure classic portal]로 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="fab7b-138">다음 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-138">This involves the following steps:</span></span>

* <span data-ttu-id="fab7b-139">클라이언트 인증서를 나타내는 PFX 파일을 생성하고 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="fab7b-140">PFX 파일에서 관리 인증서(CER 파일)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="fab7b-141">CER 파일을 Azure 구독에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="fab7b-142">Java가 해당 형식을 사용하여 인증서를 인증하기 때문에 PFX 파일을 JKS로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="fab7b-143">로컬 JKS 파일을 참조하는 응용 프로그램의 인증 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="fab7b-144">이 절차를 완료하면 CER 인증서는 Azure 구독에 상주하며 JKS 인증서는 로컬 드라이브에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="fab7b-145">관리 인증서에 대한 자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드][Create and Upload a Management Certificate for Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="fab7b-146">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-146">Create a certificate</span></span>
<span data-ttu-id="fab7b-147">자체 서명된 인증서를 만들려면, 운영 체제에서 명령 콘솔을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="fab7b-148">**참고:** 이 명령을 실행하는 컴퓨터에 JDK가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="fab7b-149">또한 keytool 경로는 JDK를 설치한 위치에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="fab7b-150">자세한 내용은 Java 온라인 문서의 [키 및 인증서 관리 도구(keytool)][Key and Certificate Management Tool (keytool)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="fab7b-151">.Pfx 파일을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="fab7b-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="fab7b-152">.cer 파일을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="fab7b-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="fab7b-153">설명:</span><span class="sxs-lookup"><span data-stu-id="fab7b-153">where:</span></span>

* <span data-ttu-id="fab7b-154">`<java-install-dir>` Java를 설치한 디렉터리의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="fab7b-155">`<keystore-id>` 키 저장소 항목 ID입니다(예: `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="fab7b-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="fab7b-156">`<cert-store-dir>` 인증서를 저장할 디렉터리의 경로입니다(예: `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="fab7b-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="fab7b-157">`<cert-file-name>` 인증서의 이름입니다(예: `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="fab7b-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="fab7b-158">`<password>` 인증서를 보호하기 위해 선택하는 암호입니다. 최소 6자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="fab7b-159">권장하지는 않지만 암호 없이 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="fab7b-160">`<dname>` 별칭과 연관되는 X.500 고유 이름이며 자체 서명된 인증서의 발급자 및 주제 필드로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="fab7b-161">자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드][Create and Upload a Management Certificate for Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="fab7b-162">인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="fab7b-162">Upload the certificate</span></span>
<span data-ttu-id="fab7b-163">자체 서명된 인증서를 Azure에 업로드하려면 클래식 포털의 **설정** 페이지로 이동한 다음 **관리 인증서** 탭을 클릭합니다. 페이지의 맨 아래에서 **업로드** 를 클릭하고 사용자가 만든 CER 파일의 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="fab7b-164">PFX 파일을 JKS로 변환</span><span class="sxs-lookup"><span data-stu-id="fab7b-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="fab7b-165">Windows 명령 프롬프트에서(관리자로 실행), cd를 사용하여 인증서를 포함한 디렉토리로 이동하고 다음 명령을 실행합니다. 여기서 `<java-install-dir>`은 사용자 컴퓨터에 설치된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="fab7b-166">메시지가 표시되면 대상 키 저장소 암호를 입력합니다. 이 암호는 JKS 파일의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="fab7b-167">메시지가 표시되면 원본 키 저장소 암호를 입력합니다. 이 암호는 PFX 파일에 대 해 지정된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="fab7b-168">두 암호가 동일하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="fab7b-169">권장하지는 않지만 암호 없이 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="fab7b-170">웹 앱 만들기 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="fab7b-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="fab7b-171">Eclipse 작업 영역 및 Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="fab7b-172">이 섹션에서는 AzureWebDemo라는 웹 앱 만들기 응용 프로그램을 위한 Maven 프로젝트 및 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="fab7b-173">새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-173">Create a new Maven project.</span></span> <span data-ttu-id="fab7b-174">**파일 > 새로 만들기 > Maven 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="fab7b-175">**새 Maven 프로젝트**에서 **간단한 프로젝트 만들기** 및 **기본 작업 영역 위치 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="fab7b-176">**새 Maven 프로젝트**의 두 번째 페이지에서 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="fab7b-177">그룹 ID: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="fab7b-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="fab7b-178">아티팩트 ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="fab7b-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="fab7b-179">버전: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="fab7b-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="fab7b-180">패키징: jar</span><span class="sxs-lookup"><span data-stu-id="fab7b-180">Packaging: jar</span></span>
   * <span data-ttu-id="fab7b-181">이름: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="fab7b-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="fab7b-182">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-182">Click **Finish**.</span></span>
3. <span data-ttu-id="fab7b-183">프로젝트 탐색기에서 새 프로젝트의 pom.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="fab7b-184">**종속성** 탭을 선택합니다. 새 프로젝트이면, 아직 패키지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="fab7b-185">Maven 리포지토리 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="fab7b-186">**창 > 보기 표시 > 기타 > Maven > Maven 리포지토리**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="fab7b-187">**Maven 리포지토리** 보기는 IDE의 아래쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="fab7b-188">**전역 리포지토리**를 열고 **중앙** 리포지토리를 마우스 오른쪽 단추로 클릭한 다음 **인덱스 다시 작성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="fab7b-189">이 단계는 사용자의 연결 속도에 따라 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="fab7b-190">인덱스를 다시 빌드하면, **중앙** Maven 저장소에 Microsoft Azure 패키지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="fab7b-191">**종속성**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="fab7b-192">**그룹 ID 입력...**에 `azure-management`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="fab7b-193">기본 관리 및 앱 서비스 웹 앱 관리에 대한 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="fab7b-194">**참고:** 새 버전 릴리스 후 종속성을 업데이트하면, 이 목록에서 각 종속성을 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="fab7b-195">**추가**를 클릭하고 각 종속성을 선택한 후에는 **종속성** 목록에서 새 버전 번호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="fab7b-196">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-196">Click **OK**.</span></span> <span data-ttu-id="fab7b-197">그러면 Azure 패키지가 **종속성** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="fab7b-198">Azure SDK를 호출하여 웹 앱을 만들도록 Java 코드 작성</span><span class="sxs-lookup"><span data-stu-id="fab7b-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="fab7b-199">다음으로, 앱 서비스 웹 앱을 만드는 Java 용 Azure SDK에서 API를 호출하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="fab7b-200">기본 진입점 코드를 포함하는 Java 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="fab7b-201">[프로젝트 탐색기]에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **새로 만들기 > 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="fab7b-202">**새 Java 클래스**에서, 클래스의 이름을 `WebCreator`로 지정하고 **public static void main** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="fab7b-203">선택 항목은 다음과 같이 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="fab7b-204">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-204">Click **Finish**.</span></span> <span data-ttu-id="fab7b-205">프로젝트 탐색기에 WebCreator.java 파일이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="fab7b-206">Azure API를 호출하여 앱 서비스 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="fab7b-207">필요한 가져오기 추가</span><span class="sxs-lookup"><span data-stu-id="fab7b-207">Add necessary imports</span></span>
<span data-ttu-id="fab7b-208">WebCreator.java에서, 다음 가져오기를 추가합니다. 이 가져오기는 Azure API 사용을 위한 관리 라이브러리의 클래스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="fab7b-209">주 진입점 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="fab7b-209">Define the main entry point class</span></span>
<span data-ttu-id="fab7b-210">AzureWebDemo 응용 프로그램의 목적은 웹 서비스 웹 앱을 만드는 것이기 때문에, 이 응용 프로그램의 기본 클래스에 대한 이름을 `WebAppCreator`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="fab7b-211">이 클래스는 Azure 서비스 관리 API를 호출하여 웹 앱을 만드는 주 진입점 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="fab7b-212">웹 앱 및 웹 공간에 대한 다음 매개 변수 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="fab7b-213">사용자 고유의 Azure 구독 ID 및 인증서 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="fab7b-214">설명:</span><span class="sxs-lookup"><span data-stu-id="fab7b-214">where:</span></span>

* <span data-ttu-id="fab7b-215">`<subscription-id>` 리소스를 만들려는 Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="fab7b-216">`<certificate-store-path>` 로컬 인증서 저장소 디렉터리의 JKS 파일에 대한 경로 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="fab7b-217">예를 들어, Linux에 대해서는 `C:/Certificates/CertificateName.jks`이며 Windows에 대해서는 `C:\Certificates\CertificateName.jks`입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="fab7b-218">`<certificate-password>` JKS 인증서를 만들 때 지정한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="fab7b-219">`webAppName` 선택한 모든 이름일 수 있습니다. 이 프로시저는 이름 `WebDemoWebApp`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="fab7b-220">전체 도메인 이름은 `domainName`이 추가된 `webAppName`으로 이 경우 전체 도메인은 `webdemowebapp.azurewebsites.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="fab7b-221">`domainName` 위와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="fab7b-222">`webSpaceName`은 [WebSpaceNames][WebSpaceNames] 클래스에 정의된 값 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="fab7b-223">`appServicePlanName` 위와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="fab7b-224">**참고:** 이 응용 프로그램을 실행할 때마다 다시 실행하기 전에 `webAppName` 및 `appServicePlanName` 값을 변경하거나 Azure Portal에서 웹앱을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="fab7b-225">그렇지 않은 경우, 동일한 리소스가 Azure에 이미 존재하기 때문에 실행이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="fab7b-226">웹 만들기 메서드 정의</span><span class="sxs-lookup"><span data-stu-id="fab7b-226">Define the web creation method</span></span>
<span data-ttu-id="fab7b-227">다음으로, 웹 앱을 만드는 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="fab7b-228">이 메서드, `createWebApp`는 웹 앱 및 웹 공간의 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="fab7b-229">App Service Web Apps 관리 클라이언트도 만들고 구성하며, [WebSiteManagementClient][WebSiteManagementClient] 개체로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="fab7b-230">관리 클라이언트는 웹 앱을 작성하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="fab7b-231">서비스 관리 API를 호출하여 응용 프로그램이 웹 앱(만들기, 업데이트 및 삭제와 같은 작업 수행)을 관리할 수 있는 RESTful 웹 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="fab7b-232">코드는 성공 또는 실패를 나타내는 응답의 HTTP 상태를 출력하고 성공하는 경우 작성한 웹 앱의 이름을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="fab7b-233">Main () 메서드 정의</span><span class="sxs-lookup"><span data-stu-id="fab7b-233">Define the main() method</span></span>
<span data-ttu-id="fab7b-234">createWebApp()을 호출하여 웹 앱을 만드는 main () 메서드 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="fab7b-235">마지막으로 `main`에서 `createWebApp`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="fab7b-236">응용 프로그램을 실행하고 웹 앱 작성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="fab7b-237">응용 프로그램이 실행되는 지를 확인하려면 **실행 > 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="fab7b-238">응용 프로그램 실행이 완료되면, Eclipse 콘솔에서 다음 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="fab7b-239">Azure 클래식 포털에 로그인하고 **웹 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="fab7b-240">새 웹 앱은 몇 분 내에 웹 앱 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="fab7b-241">웹 앱에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="fab7b-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="fab7b-242">AzureWebDemo를 실행하고 새 웹 앱을 만든 후 클래식 포털로 로그인하고 **웹 앱**를 마우스 오른쪽 단추로 클릭하고 **WebDemoWebApp** in the **웹 앱** 목록에서 새 버전 번호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="fab7b-243">웹앱의 대시보드 페이지에서 **찾아보기** 또는 `webdemowebapp.azurewebsites.net` URL을 클릭하여 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="fab7b-244">아직 웹 앱에 게시된 내용이 없기 때문에 빈 자리 표시자 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="fab7b-245">다음으로, "Hello World" 응용 프로그램을 만들고 웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="fab7b-246">JSP Hello World 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="fab7b-247">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fab7b-247">Create the application</span></span>
<span data-ttu-id="fab7b-248">웹 응용 프로그램을 웹에 배포하는 방법을 보여주려면, 다음 절차에서는 간단한 "Hello World" Java 응용 프로그램을 만들고 응용 프로그램에서 만든 웹 서비스 웹 앱에 업로드 하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="fab7b-249">**파일 > 새로 만들기 > 동적 웹 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="fab7b-250">이름을 `JSPHello`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-250">Name it `JSPHello`.</span></span> <span data-ttu-id="fab7b-251">이 대화 상자에서 다른 설정을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="fab7b-252">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="fab7b-253">[프로젝트 탐색기]에서 **JSPHello** 프로젝트를 확장하고 **WebContent**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기 > JSP 파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="fab7b-254">새 JSP 파일 대화 상자에서 새 파일의 이름을 `index.jsp`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="fab7b-255">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-255">Click **Next**.</span></span>
3. <span data-ttu-id="fab7b-256">**JSP 템플릿 선택** 대화 상자에서 **새 JSP 파일(html)**을 선택하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="fab7b-257">Index.jsp에서, `<head>` 및 `<body>` 섹션 태그에서 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="fab7b-258">localhost에서 Hello World 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="fab7b-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="fab7b-259">이 응용 프로그램을 실행하기 전에 몇 가지 속성을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="fab7b-260">**JSPHello** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="fab7b-261">**속성** 대화 상자에서 **Java 빌드 경로**를 선택하고 **주문 및 내보내기** 탭을 선택하고 **JRE 시스템 라이브러리**를 확인한 다음 **위로**를 클릭하여 목록의 위쪽으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="fab7b-262">또한 **속성** 대화 상자에서 **대상 런타임**을 선택하고 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="fab7b-263">**새 서버 런타임 환경** 대화 상자에서 **Apache Tomcat v7.0**과 같은 서버를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="fab7b-264">**Tomcat 서버** 대화 상자에서 **이름**을 `Apache Tomcat v7.0`으로 설정하고 **Tomcat 설치 디렉터리**를 사용하려는 Tomcat 서버 버전이 설치된 디렉터리로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="fab7b-265">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-265">Click **Finish**.</span></span>
5. <span data-ttu-id="fab7b-266">그러면 **속성** 대화 상자의 **대상 런타임**으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="fab7b-267">**Apache Tomcat v7.0**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="fab7b-268">Eclipse **실행** 메뉴에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="fab7b-269">**다음으로 실행** 대화 상자에서 **서버에서 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="fab7b-270">**서버에서 실행** 대화 상자에서 **Tomcat v7.0 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="fab7b-271">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-271">Click **Finish**.</span></span>
7. <span data-ttu-id="fab7b-272">응용 프로그램이 실행되면 다음 메시지를 표시하는 Eclipse의 localhost 창(`http://localhost:8080/JSPHello/`)에 **JSPHello** 페이지가 표시되면서 다음 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="fab7b-273">WAR로 응용 프로그램 내보내기</span><span class="sxs-lookup"><span data-stu-id="fab7b-273">Export the application as a WAR</span></span>
<span data-ttu-id="fab7b-274">웹 앱을 배포할 수 있도록 웹 보관 파일 (WAR) 파일로 웹 프로젝트 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="fab7b-275">다음 웹 프로젝트 파일은 WebContent 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="fab7b-276">WebContent 폴더를 마우스 오른쪽 단추로 클릭하고 **내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="fab7b-277">**선택 내보내기** 대화 상자에서 **웹 > WAR** 파일을 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="fab7b-278">**WAR 내보내기** 대화 상자에서 현재 프로젝트에서 src 디렉터리를 선택하고 끝에 WAR 파일의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="fab7b-279">예:</span><span class="sxs-lookup"><span data-stu-id="fab7b-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="fab7b-280">WAR 파일의 배포에 대한 자세한 내용은 [Java 응용 프로그램을 Azure 앱 서비스 웹 앱에 추가](web-sites-java-add-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="fab7b-281">FTP를 사용하여 Hello World 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="fab7b-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="fab7b-282">응용 프로그램을 게시할 타사 FTP 클라이언트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="fab7b-283">이 절차에서는 Azure로 빌드된 Kudu 콘솔 및 편리한 그래픽 UI의 널리 사용되는 도구인 FileZilla의 두 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="fab7b-284">**참고:** Eclipse용 Azure 도구 키트는 저장소 계정 및 클라우드 서비스에 대한 배포를 지원하지만, 현재는 웹앱에 대한 배포를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="fab7b-285">[Eclipse에서 Azure용 Hello World 응용 프로그램을 만들기](http://msdn.microsoft.com/library/azure/hh690944.aspx)에서 설명한 대로 Azure 배포 프로젝트를 사용하여 저장소 계정 및 클라우드 서비스를 배포할 수 있지만 웹 앱에는 배포하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="fab7b-286">FTP 또는 GitHub와 같은 다른 메서드를 사용하여 웹 앱에 파일을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="fab7b-287">**참고:** Windows 명령 프롬프트(Windows와 함께 제공되는 명령줄 FTP.EXE 유틸리티)에서 FTP를 사용하는 것은 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="fab7b-288">FTP.EXE와 같은 활성 FTP를 사용하는 FTP 클라이언트는 방화벽을 통해 작동하는 데 자주 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="fab7b-289">활성 FTP는 FTP 서버가 연결에 실패할 가능성이 있는 내부 LAN 기반 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="fab7b-290">FTP를 사용하여 웹 서비스 웹 앱에 배포에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="fab7b-291">FTP 유틸리티를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="fab7b-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="fab7b-292">배포 자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="fab7b-292">Set up deployment credentials</span></span>
<span data-ttu-id="fab7b-293">**AzureWebDemo** 응용 프로그램을 실행하여 웹 앱을 만드는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="fab7b-294">이 위치에 파일을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="fab7b-295">클래식 포털에 로그인하고 **웹 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="fab7b-296">**WebDemoWebApp** 은 웹 앱 목록에 표시되며 실행 중인지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="fab7b-297">**WebDemoWebApp**을 클릭하여 해당 **대시보드** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="fab7b-298">**대시보드** 페이지의 **간략 상태**에서 **배포 자격 증명 설정**(배포 자격 증명이 이미 있는 경우 **배포 자격 증명 재설정**)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="fab7b-299">배포 자격 증명은 Microsoft 계정과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="fab7b-300">Git 및 FTP를 사용하여 배포하는 데 사용할 수 있는 사용자 이름 및 암호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="fab7b-301">이러한 자격 증명을 사용하여 Microsoft 계정에 연결된 모든 Azure 구독에서 모든 웹 앱에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="fab7b-302">대화 상자에서 Git 및 FTP 배포 자격 증명을 제공하고 나중에 사용할 사용자 이름 및 암호를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="fab7b-303">FTP 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="fab7b-303">Get FTP connection information</span></span>
<span data-ttu-id="fab7b-304">FTP를 사용하여 새로 만든 웹 앱에 응용 프로그램 파일을 배포하려면 연결 정보를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="fab7b-305">두 가지 방법으로 연결 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="fab7b-306">한 가지 방법은 웹 앱의 **대시보드** 페이지를 방문하는 것이고, 다른 방법은 웹 앱의 게시 프로필을 다운로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="fab7b-307">게시 프로필은 Azure 앱 서비스에서 웹 앱에 대한 FTP 호스트 이름 및 로그온 자격 증명과 같은 정보를 제공하는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="fab7b-308">이 사용자 이름 및 암호를 사용하여 Azure 계정과 연결된 모든 구독에서 하나가 아닌 모든 웹 앱에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="fab7b-309">[Azure Portal][Azure Portal]의 웹앱 블레이드에서 FTP 연결 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="fab7b-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="fab7b-310">**Essentials**에서 **FTP 호스트 이름**을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="fab7b-311">`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`와 유사한 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="fab7b-312">**Essentials**에서 **FTP/배포 사용자 이름**을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="fab7b-313">*webappname\deployment-username* 형식으로 있습니다(예: `WebDemoWebApp\deployer77`).</span><span class="sxs-lookup"><span data-stu-id="fab7b-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="fab7b-314">게시 프로필에서 FTP 연결 정보를 얻으려면:</span><span class="sxs-lookup"><span data-stu-id="fab7b-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="fab7b-315">웹 앱의 블레이드에서 **게시 프로필 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="fab7b-316">.Publishsettings 파일을 로컬 드라이브에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="fab7b-317">XML 편집기나 텍스트 편집기에서.publishsettings 파일을 열고 `publishMethod="FTP"`을 포함한 `<publishProfile>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="fab7b-318">다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="fab7b-319">다음과 같이 웹 앱의 `publishProfile` 설정은 FileZilla 사이트 관리자 설정으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="fab7b-320">`publishUrl`은 **FTP 호스트 이름**과 같으며 **호스트**에서 설정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="fab7b-321">`publishMethod="FTP"`는 **프로토콜**을 **FTP-파일 전송 프로토콜**로, **암호화**를 **일반 FTP 사용**으로 설정함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="fab7b-322">`userName` 및 `userPWD`는 배포 자격 증명을 재설정할 때 지정한 실제 사용자 이름 및 암호 값의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="fab7b-323">`userName`은 **배포 / FTP 사용자**와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="fab7b-324">FileZilla에서는 **사용자** 및 **암호**로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="fab7b-325">`ftpPassiveMode="True"`는 FTP 사이트에서 수동 FTP 전송을 사용함을 의미하며, **전송 설정** 탭에서 **수동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="fab7b-326">Java 응용 프로그램을 호스트하도록 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="fab7b-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="fab7b-327">응용 프로그램을 게시하기 전에, 웹 앱이 Java 응용 프로그램을 호스팅할 수 있도록 몇 가지 구성 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="fab7b-328">클래식 포털에서 웹앱의 **대시보드** 페이지로 이동하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="fab7b-329">**구성** 페이지에서 다음 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="fab7b-330">**Java 버전**에서 기본값은 **Off**입니다. 응용 프로그램에서 대상으로 하는 Java 버전을 선택합니다(예: 1.7.0_51).</span><span class="sxs-lookup"><span data-stu-id="fab7b-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="fab7b-331">이렇게 수행한 후 **웹 컨테이너**가 Tomcat 서버 버전으로 설정되어 있는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="fab7b-332">**기본 문서**에서, index.jsp를 추가하고 위쪽 목록으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="fab7b-333">(웹 앱에 대한 기본 파일은 hostingstart.html입니다.)</span><span class="sxs-lookup"><span data-stu-id="fab7b-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="fab7b-334">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="fab7b-335">Kudu를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="fab7b-335">Publish your application using Kudu</span></span>
<span data-ttu-id="fab7b-336">응용 프로그램을 게시하는 한 가지 방법은 Azure에 기본 제공되는 Kudu 디버그 콘솔을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="fab7b-337">kudu는 안정적이며 웹 서비스 웹 앱 및 Tomcat 서버와 일치된다고 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="fab7b-338">다음 형식의 URL로 이동하여 웹 앱에 대한 콘솔에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="fab7b-339">이 절차의 경우, Kudu 콘솔은 다음 URL에 있습니다. 이 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="fab7b-340">최상위 메뉴에서 **디버그 콘솔 > CMD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="fab7b-341">콘솔 명령줄에서 `/site/wwwroot`로 이동합니다(페이지 위쪽의 디렉터리 보기에서 `site`, `wwwroot`을 차례로 클릭).</span><span class="sxs-lookup"><span data-stu-id="fab7b-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="fab7b-342">**Java 버전**을 지정한 후, Tomcat 서버는 webapps 디렉터리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="fab7b-343">콘솔 명령줄에서 webapps 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="fab7b-344">`<project-path>/JSPHello/src/`에서 JSPHello.war를 끌어 `/site/wwwroot/webapps` 아래 Kudu 디렉토리로 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="fab7b-345">Tomcat이 압축을 풀기 때문에 "여기로 끌어서 업로드하고 압축" 영역으로 끌어놓지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="fab7b-346">처음에 JSPHello.war는 단독으로 디렉터리 영역에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="fab7b-347">짧은 시간(약 5분 미만)에 Tomcat 서버는 JSPHello 압축을 해제한 디렉터리로 WAR 파일의 압축을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="fab7b-348">ROOT 디렉터리를 클릭하여 Index.jsp의 압축을 해제하고 복사하는 지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="fab7b-349">그런 경우, 압축이 해제된 JSPHello 디렉터리가 만들어졌는지 여부를 볼 수 있는 webapps 디렉터리로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="fab7b-350">이 항목이 표시되지 않으면 대기하고 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="fab7b-351">FileZilla를 사용하여 응용 프로그램 게시(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="fab7b-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="fab7b-352">응용 프로그램을 게시하는데 사용할 수 있는 다른 도구는 FileZilla로, 편리한 그래픽 UI가 있는 타사 FTP 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="fab7b-353">없는 경우, [http://filezilla-project.org/](http://filezilla-project.org/) 에서 FileZilla를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="fab7b-354">클라이언트 사용에 대한 자세한 내용은 [FileZilla 설명서](https://wiki.filezilla-project.org/Documentation) 및 [FTP 클라이언트 - 4부: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx)(영문) 블로그 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fab7b-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="fab7b-355">FileZilla에서 **파일 > Site Manager**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="fab7b-356">**Site Manager** 대화 상자에서 **새 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="fab7b-357">비어 있는 새 FTP 사이트는 이름을 입력하라는 메시지를 표시하는 **항목 선택** 에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="fab7b-358">이 절차에 대한 이름을 `AzureWebDemo-FTP`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="fab7b-359">**일반** 탭에서 다음 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="fab7b-360">**호스트:** 대시보드에서 복사한 **FTP 호스트 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="fab7b-361">**포트:** 이 항목은 수동 전송이고 서버가 사용할 포트를 결정하므로 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="fab7b-362">**프로토콜:** FTP 파일 전송 프로토콜</span><span class="sxs-lookup"><span data-stu-id="fab7b-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="fab7b-363">**암호화:** 일반 FTP 사용</span><span class="sxs-lookup"><span data-stu-id="fab7b-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="fab7b-364">**로그온 유형:** 일반</span><span class="sxs-lookup"><span data-stu-id="fab7b-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="fab7b-365">**사용자:** 대시보드에서 복사한 배포/FTP 사용자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="fab7b-366">완전한 FTP 사용자 이름으로 *webappname\username* 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="fab7b-367">**암호:** 배포 자격 증명을 설정할 때 지정한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="fab7b-368">**전송 설정** 탭에서 **수동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="fab7b-369">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-369">Click **Connect**.</span></span> <span data-ttu-id="fab7b-370">성공하는 경우, FileZilla의 콘솔은 `Status: Connected` 메시지를 표시하며 `LIST` 명령을 실행하여 디렉터리 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="fab7b-371">**로컬** 사이트 패널에서 JSPHello.war 파일이 상주하는 원본 디렉터리를 선택합니다. 경로는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="fab7b-372">**원격** 사이트 패널에서 대상 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="fab7b-373">WAR 앱 루트 아래 `webapps` 디렉토리로 WAR 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="fab7b-374">`/site/wwwroot`로 이동하고 `wwwroot`를 마우스 오른쪽 단추로 클릭하고 **디렉터리 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="fab7b-375">디렉터리의 이름을 `webapps` 로 지정하고 해당 디렉터리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="fab7b-376">JSPHello.war을 `/site/wwwroot/webapps`에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="fab7b-377">**로컬** 파일 목록에서 JSPHello.war를 선택하고 마우스 오른쪽 단추로 클릭하고 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="fab7b-378">`/site/wwwroot/webapps`에 보이도록 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="fab7b-379">webapps 디렉터리로 JSPHello.war를 복사한 후, Tomcat 서버는 자동으로 파일을 WAR 파일로 압축 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="fab7b-380">Tomcat 서버가 거의 즉시 압축 해제를 시작하더라도, 파일이 FTP 클라이언트에 표시되기 까지는 긴 시간(몇 시간)이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="fab7b-381">웹 앱에서 Hello World 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="fab7b-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="fab7b-382">WAR 파일을 업로드하고 Tomcat 서버가 압축을 해제한 `JSPHello` 디렉터리를 만든 후, `http://webdemowebapp.azurewebsites.net/JSPHello`로 이동하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="fab7b-383">**참고:** 클래식 포털에서 **찾아보기**를 클릭하면 "이 Java 기반 웹 응용 프로그램이 성공적으로 만들었습니다."라는 기본 웹 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="fab7b-384">기본 웹 페이지 대신 응용 프로그램 출력을 보려면 웹 페이지를 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="fab7b-385">응용 프로그램이 실행되면 다음 출력이 있는 웹 페이지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="fab7b-386">Azure 리소스 정리</span><span class="sxs-lookup"><span data-stu-id="fab7b-386">Clean up Azure resources</span></span>
<span data-ttu-id="fab7b-387">이 절차에서는 앱 서비스 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="fab7b-388">존재하는 한 리소스에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="fab7b-389">테스트나 개발에 웹 앱을 계속 사용하지 않으려면, 중지 또는 삭제를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="fab7b-390">중지된 웹 앱은 여전히 작은 요금을 부과하지만 언제든지 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="fab7b-391">웹 앱을 삭제하면 업로드한 데이터를 모두 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="fab7b-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
