---
title: "aaaHow toocreate 클라우드 서비스 및 배포 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello 빠른 생성 메서드를 사용 하 여 Azure에서 클라우드 서비스 및 배포 합니다."
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
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="a64ce-103">어떻게 tooCreate 클라우드 서비스 및 배포</span><span class="sxs-lookup"><span data-stu-id="a64ce-103">How tooCreate and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a64ce-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a64ce-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="a64ce-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="a64ce-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="a64ce-106">hello Azure 클래식 포털 toocreate 있습니다에 대 한 두 가지 방법을 제공 하 고 클라우드 서비스 배포: **빠른 생성** 및 **사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-106">hello Azure classic portal provides two ways for you toocreate and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="a64ce-107">이 항목에서는 toouse 메서드 toocreate 빠른 생성 새 클라우드 서비스는 hello 하 고 다음 사용 하는 방법에 대해 설명 **업로드** tooupload 하 고 Azure에서 클라우드 서비스 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-107">This topic explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="a64ce-108">이 방법을 사용 하면 hello Azure 클래식 포털에서 작업을 진행 하면서 요구 사항을 모두 완료 하기 위한 편리 하 게 사용할 수 있는 링크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-108">When you use this method, hello Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="a64ce-109">을 사용 하는 클라우드 서비스를 만들 경우 준비 toodeploy hello에 둘 다를 수행할 수 있습니다 사용 하 여 동일한 시간 **사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="a64ce-110">클라우드 서비스에서 VSTS Visual Studio Team Services () toopublish 하려는 경우 사용 **빠른 생성**, VSTS에서 게시를 설정한 다음 **빠른 시작** 또는 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or hello dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="a64ce-111">개념</span><span class="sxs-lookup"><span data-stu-id="a64ce-111">Concepts</span></span>
<span data-ttu-id="a64ce-112">세 가지 구성 요소 순서 toodeploy Azure에서 클라우드로 응용 프로그램 서비스에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-112">Three components are required in order toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="a64ce-113">**서비스 정의**</span><span class="sxs-lookup"><span data-stu-id="a64ce-113">**Service Definition**</span></span>  
  <span data-ttu-id="a64ce-114">hello 클라우드 서비스 정의 파일 (.csdef) hello 역할 수를 포함 하 여 hello 서비스 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-114">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="a64ce-115">**서비스 구성**</span><span class="sxs-lookup"><span data-stu-id="a64ce-115">**Service Configuration**</span></span>  
  <span data-ttu-id="a64ce-116">hello 클라우드 서비스 구성 파일 (.cscfg) hello 클라우드 서비스 및 hello 역할 인스턴스 수를 비롯 한 개별 역할에 대 한 구성 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-116">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="a64ce-117">**서비스 패키지**</span><span class="sxs-lookup"><span data-stu-id="a64ce-117">**Service Package**</span></span>  
  <span data-ttu-id="a64ce-118">hello 서비스 패키지 (.cspkg) hello 응용 프로그램 코드 및 구성과 hello 서비스 정의 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-118">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="a64ce-119">이 대 한 자세히 알아볼 수 있습니다 및 방법을 toocreate 패키지 [여기](cloud-services-model-and-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-119">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="a64ce-120">앱 준비</span><span class="sxs-lookup"><span data-stu-id="a64ce-120">Prepare your app</span></span>
<span data-ttu-id="a64ce-121">클라우드 서비스를 배포 하기 전에 응용 프로그램 코드와 클라우드 서비스 구성 파일 (.cscfg)에서 hello 클라우드 서비스 패키지 (.cspkg)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-121">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="a64ce-122">Azure SDK hello 이러한 필수 배포 파일을 준비 하기 위한 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-122">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="a64ce-123">Hello에서 hello SDK를 설치할 수 있습니다 [Azure 다운로드](https://azure.microsoft.com/downloads/) toodevelop 원하는 hello 언어로 응용 프로그램 코드 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-123">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="a64ce-124">세 가지 클라우드 서비스 기능은 서비스 패키지를 내보내기 전에 특별히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="a64ce-125">Toodeploy 데이터 암호화에 대 한 Secure Sockets Layer (SSL)를 사용 하는 클라우드 서비스를 원하는 경우 [응용 프로그램을 구성](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) SSL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-125">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="a64ce-126">Tooconfigure 원격 데스크톱 연결 toorole 인스턴스를 원하는 경우 [hello 역할 구성](cloud-services-role-enable-remote-desktop.md) 원격 데스크톱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-126">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="a64ce-127">Tooconfigure를 클라우드 서비스에 대 한 모니터링 세부 정보 표시 하려는 경우 hello 클라우드 서비스에 대 한 Azure 진단을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-127">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="a64ce-128">*최소 모니터링* (hello 기본 수준 모니터링) 역할 인스턴스 (가상 컴퓨터)에 대 한 hello 호스트 운영 체제에서 수집한 성능 카운터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-128">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="a64ce-129">"자세한 정보 표시 모니터링 * hello 역할 인스턴스 tooenable 보다 자세하게 분석 응용 프로그램 처리 하는 동안 발생 하는 문제 내에서 성능 데이터를 기반으로 하는 추가 메트릭을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-129">"Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="a64ce-130">tooenable Azure 진단을 참조 하는 방법에 대해 toofind [Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-130">toofind out how tooenable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="a64ce-131">해야 클라우드 서비스 웹 역할 또는 작업자 역할의 배포와 toocreate [hello 서비스 패키지 만들기](cloud-services-model-and-package.md#servicepackagecspkg)합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-131">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a64ce-132">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a64ce-132">Before you begin</span></span>
* <span data-ttu-id="a64ce-133">Hello Azure SDK를 설치 하지 않은 경우 클릭 **Azure SDK 설치** tooopen hello [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/), 한 후 hello를 원하는 언어 toodevelop 코드에 대 한 hello SDK를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-133">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="a64ce-134">(해야 합니다. 영업 기회 toodo이 나중에.)</span><span class="sxs-lookup"><span data-stu-id="a64ce-134">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="a64ce-135">인증서를 요구 하는 모든 역할 인스턴스를 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-135">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="a64ce-136">클라우드 서비스에는 개인 키가 포함된 .pfx 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="a64ce-137">있습니다 수 [hello 인증서 tooAzure 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) hello 클라우드 서비스 배포를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="a64ce-137">You can [upload hello certificates tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy hello cloud service.</span></span>
* <span data-ttu-id="a64ce-138">Toodeploy hello 클라우드 서비스 tooan 선호도 그룹을 계획 하는 경우 hello 선호도 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-138">If you plan toodeploy hello cloud service tooan affinity group, create hello affinity group.</span></span> <span data-ttu-id="a64ce-139">클라우드 서비스 및 다른 Azure 서비스 toohello 선호도 그룹 toodeploy를 사용할 수 있는 영역에서 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-139">You can use an affinity group toodeploy your cloud service and other Azure services toohello same location in a region.</span></span> <span data-ttu-id="a64ce-140">Hello에 hello 선호도 그룹을 만들고 **네트워크** hello hello에 Azure 클래식 포털의 영역 **선호도 그룹** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a64ce-140">You can create hello affinity group in hello **Networks** area of hello Azure classic portal, on hello **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="a64ce-141">방법: 빠른 생성을 사용하여 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="a64ce-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="a64ce-142">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **새로**>**계산**>**클라우드 서비스** > **빨리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-142">In hello [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="a64ce-144">**URL**, 프로덕션 배포에서 클라우드 서비스에 액세스 하기 위한 하위 도메인 이름 toouse hello 공용 URL에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-144">In **URL**, enter a subdomain name toouse in hello public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="a64ce-145">프로덕션 배포에 대 한 hello URL 형식은: http://*myURL*. cloudapp.net에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-145">hello URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="a64ce-146">**지역 또는 선호도 그룹**, 선택 hello 지리적 지역 또는 선호도 그룹 toodeploy hello 하도록 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-146">In **Region or Affinity Group**, select hello geographic region or affinity group toodeploy hello cloud service to.</span></span> <span data-ttu-id="a64ce-147">선호도 그룹을 선택 toodeploy 클라우드 서비스 toohello 영역 내에서 다른 Azure 서비스와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-147">Select an affinity group if you want toodeploy your cloud service toohello same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="a64ce-148">**클라우드 서비스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="a64ce-150">Hello hello hello 창 맨 아래에 hello 메시지 영역의 hello 프로세스 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-150">You can monitor hello status of hello process in hello message area at hello bottom of hello window.</span></span>
   
    <span data-ttu-id="a64ce-151">hello **클라우드 서비스** hello 표시 되는 새 클라우드 서비스와 영역 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-151">hello **Cloud Services** area opens, with hello new cloud service displayed.</span></span> <span data-ttu-id="a64ce-152">Hello 상태 tooCreated 변경 되 면 클라우드 서비스 만들기를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-152">When hello status changes tooCreated, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="a64ce-154">방법: 클라우드 서비스에 대한 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="a64ce-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="a64ce-155">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-155">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click hello name of hello cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="a64ce-157">**인증서 업로드** 또는 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="a64ce-158">**파일**를 사용 하 여 **찾아보기** tooselect hello 인증서 (.pfx 파일).</span><span class="sxs-lookup"><span data-stu-id="a64ce-158">In **File**, use **Browse** tooselect hello certificate (.pfx file).</span></span>
4. <span data-ttu-id="a64ce-159">**암호**, hello hello 인증서 개인 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-159">In **Password**, enter hello private key for hello certificate.</span></span>
5. <span data-ttu-id="a64ce-160">**확인** (확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="a64ce-162">아래에 표시 된 hello 메시지 영역에서 hello 업로드의 hello 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-162">You can watch hello progress of hello upload in hello message area, shown below.</span></span> <span data-ttu-id="a64ce-163">Hello 업로드가 완료 되 면 hello 인증서 toohello 테이블을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-163">When hello upload completes, hello certificate is added toohello table.</span></span> <span data-ttu-id="a64ce-164">Hello 메시지 영역에서 확인 tooclose hello 메시지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-164">In hello message area, click OK tooclose hello message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="a64ce-166">방법: 클라우드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="a64ce-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="a64ce-167">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-167">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click hello name of hello cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="a64ce-168">**새 프로덕션 배포 업로드** 또는 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="a64ce-169">**배포 레이블**, 예를 들어 MyCloudServicev4-hello 새 배포에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-169">In **Deployment label**, enter a name for hello new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="a64ce-170">**패키지**를 사용 하 여 **찾아보기** tooselect hello 서비스 패키지 파일 (.cspkg) toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-170">In **Package**, use **Browse** tooselect hello service package file (.cspkg) toouse.</span></span>
5. <span data-ttu-id="a64ce-171">**구성**를 사용 하 여 **찾아보기** tooselect hello 서비스 구성 파일 (.cscfg) toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-171">In **Configuration**, use **Browse** tooselect hello service configure file (.cscfg) toouse.</span></span>
6. <span data-ttu-id="a64ce-172">Hello 클라우드 서비스 역할 인스턴스 중 하나만 포함 선택 hello **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 배포** 확인란 tooenable hello 배포 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-172">If hello cloud service will include any roles with only one instance, select hello **Deploy even if one or more roles contain a single instance** check box tooenable hello deployment tooproceed.</span></span>
   
    <span data-ttu-id="a64ce-173">만 azure 유지 관리 및 서비스 업데이트 중 99.95% 액세스 toohello 클라우드 서비스를 확인할 수 모든 역할에 두 개 이상의 인스턴스가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="a64ce-173">Azure can only guarantee 99.95 percent access toohello cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="a64ce-174">필요한 경우 hello에서 추가 역할 인스턴스를 추가할 수 있습니다 **배율** hello 클라우드 서비스를 배포한 후 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-174">If needed, you can add additional role instances on hello **Scale** page after you deploy hello cloud service.</span></span> <span data-ttu-id="a64ce-175">자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a64ce-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="a64ce-176">클릭 **확인** (확인 표시) toobegin hello 클라우드 서비스 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-176">Click **OK** (checkmark) toobegin hello cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="a64ce-178">Hello 메시지 영역에서 hello 배포의 hello 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-178">You can monitor hello status of hello deployment in hello message area.</span></span> <span data-ttu-id="a64ce-179">확인 toohide hello 메시지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-179">Click OK toohide hello message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="a64ce-181">배포가 완료되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="a64ce-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="a64ce-182">**Dashboard**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="a64ce-183">hello 상태가 표시 hello 서비스가 임을 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-183">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="a64ce-184">아래 **눈에 보는**, hello 사이트 URL tooopen 웹 브라우저에서 클라우드 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a64ce-184">Under **quick glance**, click hello site URL tooopen your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="a64ce-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a64ce-186">Next steps</span></span>
* <span data-ttu-id="a64ce-187">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a64ce-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="a64ce-188">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성</span><span class="sxs-lookup"><span data-stu-id="a64ce-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="a64ce-189">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="a64ce-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="a64ce-190">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="a64ce-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

