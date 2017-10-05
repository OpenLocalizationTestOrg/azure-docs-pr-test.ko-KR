---
title: "클라우드 서비스를 만들고 배포하는 방법 | Microsoft Docs"
description: "Azure 포털을 사용하여 클라우드 서비스를 만들고 배포하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="1bfe7-103">클라우드 서비스를 만들고 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="1bfe7-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1bfe7-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1bfe7-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="1bfe7-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="1bfe7-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="1bfe7-106">Azure 포털은 클라우드 서비스를 만들고 배포하는 두 가지 방법으로 *빨리 만들기* 및 *사용자 지정 만들기*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="1bfe7-107">이 문서는 빠른 생성 방법을 사용하여 새 클라우드 서비스를 만든 다음 **업로드** 를 사용하여 Azure에서 클라우드 서비스 패키지를 업로드하고 배포하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="1bfe7-108">이 방법을 사용하는 경우 작업을 진행하면서 모든 요구 사항을 완료하는 데 사용할 수 있는 편리한 링크를 Azure 포털에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="1bfe7-109">클라우드 서비스를 만들 때 배포할 준비가 되면 사용자 지정 만들기를 사용하여 동시에 둘 다를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfe7-110">VSTS(Visual Studio Team Services)에서 클라우드 서비스를 게시하려는 경우 빠른 생성을 사용한 다음 Azure 빠른 시작 또는 대시보드에서 VSTS 게시를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="1bfe7-111">자세한 내용은 [Visual Studio Team Services를 사용하여 Azure에 지속적인 전송][TFSTutorialForCloudService]을 참조하거나 **빠른 시작** 페이지에 대한 도움말을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="1bfe7-112">개념</span><span class="sxs-lookup"><span data-stu-id="1bfe7-112">Concepts</span></span>
<span data-ttu-id="1bfe7-113">Azure에서 응용 프로그램을 클라우드 서비스로 배포하려면 다음과 같은 세 가지 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="1bfe7-114">**서비스 정의**</span><span class="sxs-lookup"><span data-stu-id="1bfe7-114">**Service Definition**</span></span>  
  <span data-ttu-id="1bfe7-115">클라우드 서비스 정의 파일(.csdef)은 역할 수를 포함하여 서비스 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="1bfe7-116">**서비스 구성**</span><span class="sxs-lookup"><span data-stu-id="1bfe7-116">**Service Configuration**</span></span>  
  <span data-ttu-id="1bfe7-117">클라우드 서비스 구성 파일(.cscfg)은 역할 인스턴스 수를 포함하여 클라우드 서비스 및 개별 역할에 대한 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="1bfe7-118">**서비스 패키지**</span><span class="sxs-lookup"><span data-stu-id="1bfe7-118">**Service Package**</span></span>  
  <span data-ttu-id="1bfe7-119">서비스 패키지(.cspkg)에는 응용 프로그램 코드와 구성 및 서비스 정의 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="1bfe7-120">이러한 구성 요소에 대한 자세한 내용과 패키지를 만드는 방법은 [여기](cloud-services-model-and-package.md)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="1bfe7-121">앱 준비</span><span class="sxs-lookup"><span data-stu-id="1bfe7-121">Prepare your app</span></span>
<span data-ttu-id="1bfe7-122">클라우드 서비스를 배포하려면 먼저 응용 프로그램 코드 및 클라우드 서비스 구성 파일(.cscfg)에서 클라우드 서비스 패키지(.cspkg)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="1bfe7-123">Azure SDK는 필요한 배포 파일을 준비하는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="1bfe7-124">[Azure 다운로드](https://azure.microsoft.com/downloads/) 페이지에서 응용 프로그램 코드를 개발하려는 언어로 SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="1bfe7-125">세 가지 클라우드 서비스 기능은 서비스 패키지를 내보내기 전에 특별히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="1bfe7-126">데이터 암호화에 SSL(Secure Sockets Layer)을 사용하는 클라우드 서비스를 배포하려는 경우 SSL에 맞게 [응용 프로그램을 구성](cloud-services-configure-ssl-certificate-portal.md#modify) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="1bfe7-127">역할 인스턴스에 대한 원격 데스크톱 연결을 구성하려면 원격 데스크톱에 대한 [역할을 구성](cloud-services-role-enable-remote-desktop-new-portal.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="1bfe7-128">클라우드 서비스에 대해 자세한 모니터링을 구성하려면 클라우드 서비스에 Azure 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="1bfe7-129">*최소 모니터링* (기본 모니터링 수준)에서는 역할 인스턴스(가상 컴퓨터)에 대해 호스트 운영 체제에서 수집된 성능 카운터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="1bfe7-130">*세부 정보 표시 모니터링* 에서는 역할 인스턴스 내 성능 데이터를 기반으로 추가 메트릭을 수집하여 응용 프로그램 처리 중 발생하는 문제를 보다 자세히 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="1bfe7-131">Azure 진단을 사용하도록 설정하는 방법에 대해 알아보려면 [Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="1bfe7-132">웹 역할 또는 작업자 역할 배포를 통해 클라우드 서비스를 만들려면 [서비스 패키지를 만들어야](cloud-services-model-and-package.md#servicepackagecspkg)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1bfe7-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1bfe7-133">Before you begin</span></span>
* <span data-ttu-id="1bfe7-134">Azure SDK를 설치하지 않은 경우 **Azure SDK 설치** 를 클릭하여 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)를 열고 코드를 개발하려는 언어의 SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="1bfe7-135">이 작업은 나중에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="1bfe7-136">역할 인스턴스에 인증서가 필요한 경우 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="1bfe7-137">클라우드 서비스에는 개인 키가 포함된 .pfx 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="1bfe7-138">클라우드 서비스를 만들고 배포할 때 Azure에 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="1bfe7-139">만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="1bfe7-139">Create and deploy</span></span>
1. <span data-ttu-id="1bfe7-140">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1bfe7-141">**새로 만들기 > 계산**을 클릭한 다음 아래로 스크롤하여 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="1bfe7-143">새 **클라우드 서비스** 블레이드에서 **DNS 이름**의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="1bfe7-144">새 **리소스 그룹** 을 만들거나 기존 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="1bfe7-145">**위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-145">Select a **Location**.</span></span>
6. <span data-ttu-id="1bfe7-146">**패키지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-146">Click **Package**.</span></span> <span data-ttu-id="1bfe7-147">그러면 **패키지 업로드** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="1bfe7-148">필수 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-148">Fill in the required fields.</span></span> <span data-ttu-id="1bfe7-149">역할에 단일 인스턴스가 포함된 경우 **단일 인스턴스가 포함된 역할이 하나 이상 있는 경우에도 배포합니다.** 가 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="1bfe7-150">**배포 시작** 이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="1bfe7-151">**확인**을 클릭하면 **패키지 업로드** 블레이드가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="1bfe7-152">추가할 인증서가 없는 경우 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="1bfe7-154">인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="1bfe7-154">Upload a certificate</span></span>
<span data-ttu-id="1bfe7-155">배포 패키지가 [인증서를 사용하도록 구성되었으면](cloud-services-configure-ssl-certificate-portal.md#modify)이제 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="1bfe7-156">**인증서**를 선택하고 **인증서 추가** 블레이드에서 SSL 인증서 .pfx 파일을 선택한 다음 인증서에 대한 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="1bfe7-157">**인증서 첨부**를 클릭한 다음 **인증서 추가** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="1bfe7-158">**클라우드 서비스** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="1bfe7-159">배포가 **준비** 상태에 도달하면 다음 단계로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="1bfe7-161">배포가 완료되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="1bfe7-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="1bfe7-162">클라우드 서비스 인스턴스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="1bfe7-163">서비스가 **실행 중**상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="1bfe7-164">**Essentials**에서 **사이트 URL**을 클릭하여 웹 브라우저에서 클라우드 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1bfe7-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="1bfe7-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1bfe7-166">Next steps</span></span>
* <span data-ttu-id="1bfe7-167">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1bfe7-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="1bfe7-168">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="1bfe7-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="1bfe7-169">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1bfe7-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="1bfe7-170">[SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="1bfe7-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
