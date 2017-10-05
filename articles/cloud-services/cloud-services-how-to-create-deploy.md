---
title: "클라우드 서비스를 만들고 배포하는 방법 | Microsoft Docs"
description: "Azure에서 빨리 만들기 방법을 사용하여 클라우드 서비스를 만들고 배포하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 2a2172a78bfd3ac923edbc9de366b035629dd27b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="4fb57-103">클라우드 서비스를 만들고 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="4fb57-103">How to Create and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fb57-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4fb57-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="4fb57-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="4fb57-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="4fb57-106">Azure 클래식 포털은 클라우드 서비스를 만들고 배포하는 두 가지 방법으로 **빨리 만들기** 및 **사용자 지정 만들기**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="4fb57-107">이 토픽에서는 빠른 생성 방법을 사용하여 새 클라우드 서비스를 만든 다음 **업로드** 를 사용하여 Azure에서 클라우드 서비스 패키지를 업로드하고 배포하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="4fb57-108">이 방법을 사용하는 경우 작업을 진행하면서 모든 요구 사항을 완료하는 데 사용할 수 있는 편리한 링크를 Azure 클래식 포털에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="4fb57-109">클라우드 서비스를 만들 때 배포할 준비가 되면 **사용자 지정 만들기**를 사용하여 동시에 둘 다를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="4fb57-110">VSTS(Visual Studio Team Services)에서 클라우드 서비스를 게시하려는 경우 **빠른 생성**을 사용한 다음 **빠른 시작** 또는 대시보드에서 VSTS 게시를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or the dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="4fb57-111">개념</span><span class="sxs-lookup"><span data-stu-id="4fb57-111">Concepts</span></span>
<span data-ttu-id="4fb57-112">Azure에서 응용 프로그램을 클라우드 서비스로 배포하려면 다음과 같은 세 가지 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-112">Three components are required in order to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="4fb57-113">**서비스 정의**</span><span class="sxs-lookup"><span data-stu-id="4fb57-113">**Service Definition**</span></span>  
  <span data-ttu-id="4fb57-114">클라우드 서비스 정의 파일(.csdef)은 역할 수를 포함하여 서비스 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-114">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="4fb57-115">**서비스 구성**</span><span class="sxs-lookup"><span data-stu-id="4fb57-115">**Service Configuration**</span></span>  
  <span data-ttu-id="4fb57-116">클라우드 서비스 구성 파일(.cscfg)은 역할 인스턴스 수를 포함하여 클라우드 서비스 및 개별 역할에 대한 구성 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-116">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="4fb57-117">**서비스 패키지**</span><span class="sxs-lookup"><span data-stu-id="4fb57-117">**Service Package**</span></span>  
  <span data-ttu-id="4fb57-118">서비스 패키지(.cspkg)에는 응용 프로그램 코드와 구성 및 서비스 정의 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-118">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="4fb57-119">이러한 구성 요소에 대한 자세한 내용과 패키지를 만드는 방법은 [여기](cloud-services-model-and-package.md)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-119">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="4fb57-120">앱 준비</span><span class="sxs-lookup"><span data-stu-id="4fb57-120">Prepare your app</span></span>
<span data-ttu-id="4fb57-121">클라우드 서비스를 배포하려면 먼저 응용 프로그램 코드 및 클라우드 서비스 구성 파일(.cscfg)에서 클라우드 서비스 패키지(.cspkg)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-121">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="4fb57-122">Azure SDK는 필요한 배포 파일을 준비하는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-122">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="4fb57-123">[Azure 다운로드](https://azure.microsoft.com/downloads/) 페이지에서 응용 프로그램 코드를 개발하려는 언어로 SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-123">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="4fb57-124">세 가지 클라우드 서비스 기능은 서비스 패키지를 내보내기 전에 특별히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="4fb57-125">데이터 암호화에 SSL(Secure Sockets Layer)을 사용하는 클라우드 서비스를 배포하려는 경우 SSL에 맞게 [응용 프로그램을 구성](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-125">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="4fb57-126">역할 인스턴스에 대한 원격 데스크톱 연결을 구성하려면 원격 데스크톱에 대한 [역할을 구성](cloud-services-role-enable-remote-desktop.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-126">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="4fb57-127">클라우드 서비스에 대해 자세한 모니터링을 구성하려면 클라우드 서비스에 Azure 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-127">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="4fb57-128">*최소 모니터링* (기본 모니터링 수준)에서는 역할 인스턴스(가상 컴퓨터)에 대해 호스트 운영 체제에서 수집된 성능 카운터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-128">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="4fb57-129">"자세한 모니터링*에서는 역할 인스턴스 내 성능 데이터를 기반으로 추가 메트릭을 수집하여 응용 프로그램 처리 중 발생하는 문제를 보다 자세히 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-129">"Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="4fb57-130">Azure 진단을 사용하도록 설정하는 방법에 대해 알아보려면 [Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fb57-130">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="4fb57-131">웹 역할 또는 작업자 역할 배포를 통해 클라우드 서비스를 만들려면 [서비스 패키지를 만들어야](cloud-services-model-and-package.md#servicepackagecspkg)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-131">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4fb57-132">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4fb57-132">Before you begin</span></span>
* <span data-ttu-id="4fb57-133">Azure SDK를 설치하지 않은 경우 **Azure SDK 설치** 를 클릭하여 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)를 열고 코드를 개발하려는 언어의 SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-133">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="4fb57-134">이 작업은 나중에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-134">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="4fb57-135">역할 인스턴스에 인증서가 필요한 경우 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-135">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="4fb57-136">클라우드 서비스에는 개인 키가 포함된 .pfx 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="4fb57-137">클라우드 서비스를 만들고 배포할 때 [Azure에 인증서를 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-137">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="4fb57-138">클라우드 서비스를 선호도 그룹에 배포하려면 선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-138">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="4fb57-139">선호도 그룹을 사용하면 클라우드 서비스 및 다른 Azure 서비스를 지역의 동일한 위치에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-139">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="4fb57-140">선호도 그룹은 Azure 클래식 포털의 **네트워크** 영역에 있는 **선호도 그룹** 페이지에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-140">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="4fb57-141">방법: 빠른 생성을 사용하여 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="4fb57-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="4fb57-142">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **새로 만들기**>**계산**>**클라우드 서비스**>**빨리 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-142">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="4fb57-144">**URL**에서 프로덕션 배포의 클라우드 서비스에 액세스하기 위한 공용 URL에 사용할 하위 도메인을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-144">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="4fb57-145">프로덕션 배포의 URL 형식은 http://*myURL*.cloudapp.net입니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-145">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="4fb57-146">**지역 또는 선호도 그룹**에서 클라우드 서비스를 배포할 지역 또는 선호도 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-146">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span></span> <span data-ttu-id="4fb57-147">클라우드 서비스를 지역 내의 다른 Azure 서비스와 동일한 위치에 배포하려면 선호도 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-147">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="4fb57-148">**클라우드 서비스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="4fb57-150">창 아래쪽에 있는 메시지 영역에서 프로세스의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-150">You can monitor the status of the process in the message area at the bottom of the window.</span></span>
   
    <span data-ttu-id="4fb57-151">**클라우드 서비스** 영역이 열리고 새 클라우드 서비스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-151">The **Cloud Services** area opens, with the new cloud service displayed.</span></span> <span data-ttu-id="4fb57-152">상태가 만들어짐으로 바뀌면 클라우드 서비스 만들기가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-152">When the status changes to Created, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="4fb57-154">방법: 클라우드 서비스에 대한 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="4fb57-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="4fb57-155">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하고 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-155">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="4fb57-157">**인증서 업로드** 또는 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="4fb57-158">**파일**에서 **찾아보기**를 사용하여 인증서(.pfx 파일)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-158">In **File**, use **Browse** to select the certificate (.pfx file).</span></span>
4. <span data-ttu-id="4fb57-159">**암호**에 인증서의 개인 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-159">In **Password**, enter the private key for the certificate.</span></span>
5. <span data-ttu-id="4fb57-160">**확인** (확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="4fb57-162">아래와 같이 메시지 영역에서 업로드의 진행률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-162">You can watch the progress of the upload in the message area, shown below.</span></span> <span data-ttu-id="4fb57-163">업로드가 완료되면 인증서가 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-163">When the upload completes, the certificate is added to the table.</span></span> <span data-ttu-id="4fb57-164">메시지 영역에서 확인을 클릭하여 메시지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-164">In the message area, click OK to close the message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="4fb57-166">방법: 클라우드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="4fb57-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="4fb57-167">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭한 다음 클라우드 서비스의 이름을 클릭하고 **대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-167">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="4fb57-168">**새 프로덕션 배포 업로드** 또는 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="4fb57-169">**배포 레이블**에 새 배포의 이름(예: MyCloudServicev4)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-169">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="4fb57-170">**패키지**에서 **찾아보기**를 사용하여 사용할 서비스 패키지 파일(.cspkg)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-170">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span></span>
5. <span data-ttu-id="4fb57-171">**구성**에서 **찾아보기**를 사용하여 사용할 서비스 구성 파일(.cscfg)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-171">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span></span>
6. <span data-ttu-id="4fb57-172">클라우드 서비스에 인스턴스가 하나만 있는 역할이 포함되어 있으면 **Deploy even if one or more roles contain a single instance** 확인란을 선택하여 배포가 계속 진행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-172">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span></span>
   
    <span data-ttu-id="4fb57-173">Azure는 모든 역할에 둘 이상의 인스턴스가 있는 경우에만 유지 관리 및 서비스 업데이트 중 클라우드 서비스에 대한 99.95%의 액세스를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-173">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="4fb57-174">필요한 경우 클라우드 서비스를 배포한 후 **크기 조정** 페이지에서 추가 역할 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-174">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span></span> <span data-ttu-id="4fb57-175">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fb57-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="4fb57-176">**확인** (확인 표시)을 클릭하여 클라우드 서비스 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-176">Click **OK** (checkmark) to begin the cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="4fb57-178">메시지 영역에서 배포의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-178">You can monitor the status of the deployment in the message area.</span></span> <span data-ttu-id="4fb57-179">확인을 클릭하여 메시지를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-179">Click OK to hide the message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="4fb57-181">배포가 완료되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="4fb57-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="4fb57-182">**Dashboard**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="4fb57-183">서비스가 **실행 중**상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-183">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="4fb57-184">**간략 상태**에서 사이트 URL을 클릭하여 웹 브라우저에서 클라우드 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4fb57-184">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="4fb57-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fb57-186">Next steps</span></span>
* <span data-ttu-id="4fb57-187">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4fb57-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="4fb57-188">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성</span><span class="sxs-lookup"><span data-stu-id="4fb57-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="4fb57-189">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4fb57-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="4fb57-190">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="4fb57-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

