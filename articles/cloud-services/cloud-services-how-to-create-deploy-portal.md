---
title: "aaaHow toocreate 클라우드 서비스 및 배포 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure 포털을 사용 하 여 클라우드 서비스 및 배포 합니다."
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
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="eb6a4-103">어떻게 toocreate 클라우드 서비스 및 배포</span><span class="sxs-lookup"><span data-stu-id="eb6a4-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb6a4-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="eb6a4-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="eb6a4-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="eb6a4-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="eb6a4-106">hello Azure 포털 toocreate 있습니다에 대 한 두 가지 방법을 제공 하 고 클라우드 서비스 배포: *빠른 생성* 및 *사용자 지정 만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="eb6a4-107">이 문서에서는 toouse 메서드 toocreate 빠른 생성 새 클라우드 서비스는 hello 하 고 다음 사용 하는 방법에 대해 설명 **업로드** tooupload 하 고 Azure에서 클라우드 서비스 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="eb6a4-108">이 방법을 사용 하면 hello Azure 포털에서 작업을 진행 하면서 요구 사항을 모두 완료 하기 위한 편리 하 게 사용할 수 있는 링크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="eb6a4-109">을 사용 하는 클라우드 서비스를 만들 경우 준비 toodeploy hello에 둘 다를 수행할 수 있습니다 동시 사용자 지정 만들기 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="eb6a4-110">클라우드 서비스에서 VSTS Visual Studio Team Services () toopublish 하려는 경우 빠른 생성을 사용 하 고 hello Azure 빠른 시작 또는 hello 대시보드에서 VSTS 게시를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="eb6a4-111">자세한 내용은 참조 [Visual Studio Team Services를 사용 하 여 지속적인 업데이트 tooAzure][TFSTutorialForCloudService], 또는 hello에 대 한 도움말을 참조 하십시오 **빠른 시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="eb6a4-112">개념</span><span class="sxs-lookup"><span data-stu-id="eb6a4-112">Concepts</span></span>
<span data-ttu-id="eb6a4-113">세 가지 구성 요소가 필요한 toodeploy Azure에서 클라우드 서비스로 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="eb6a4-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="eb6a4-114">**서비스 정의**</span><span class="sxs-lookup"><span data-stu-id="eb6a4-114">**Service Definition**</span></span>  
  <span data-ttu-id="eb6a4-115">hello 클라우드 서비스 정의 파일 (.csdef) hello 역할 수를 포함 하 여 hello 서비스 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="eb6a4-116">**서비스 구성**</span><span class="sxs-lookup"><span data-stu-id="eb6a4-116">**Service Configuration**</span></span>  
  <span data-ttu-id="eb6a4-117">hello 클라우드 서비스 구성 파일 (.cscfg) hello 클라우드 서비스 및 hello 역할 인스턴스 수를 비롯 한 개별 역할에 대 한 구성 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="eb6a4-118">**서비스 패키지**</span><span class="sxs-lookup"><span data-stu-id="eb6a4-118">**Service Package**</span></span>  
  <span data-ttu-id="eb6a4-119">hello 서비스 패키지 (.cspkg) hello 응용 프로그램 코드 및 구성과 hello 서비스 정의 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="eb6a4-120">이 대 한 자세히 알아볼 수 있습니다 및 방법을 toocreate 패키지 [여기](cloud-services-model-and-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="eb6a4-121">앱 준비</span><span class="sxs-lookup"><span data-stu-id="eb6a4-121">Prepare your app</span></span>
<span data-ttu-id="eb6a4-122">클라우드 서비스를 배포 하기 전에 응용 프로그램 코드와 클라우드 서비스 구성 파일 (.cscfg)에서 hello 클라우드 서비스 패키지 (.cspkg)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="eb6a4-123">Azure SDK hello 이러한 필수 배포 파일을 준비 하기 위한 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="eb6a4-124">Hello에서 hello SDK를 설치할 수 있습니다 [Azure 다운로드](https://azure.microsoft.com/downloads/) toodevelop 원하는 hello 언어로 응용 프로그램 코드 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="eb6a4-125">세 가지 클라우드 서비스 기능은 서비스 패키지를 내보내기 전에 특별히 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="eb6a4-126">Toodeploy 데이터 암호화에 대 한 Secure Sockets Layer (SSL)를 사용 하는 클라우드 서비스를 원하는 경우 [응용 프로그램을 구성](cloud-services-configure-ssl-certificate-portal.md#modify) SSL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="eb6a4-127">Tooconfigure 원격 데스크톱 연결 toorole 인스턴스를 원하는 경우 [hello 역할 구성](cloud-services-role-enable-remote-desktop-new-portal.md) 원격 데스크톱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="eb6a4-128">Tooconfigure를 클라우드 서비스에 대 한 모니터링 세부 정보 표시 하려는 경우 hello 클라우드 서비스에 대 한 Azure 진단을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="eb6a4-129">*최소 모니터링* (hello 기본 수준 모니터링) 역할 인스턴스 (가상 컴퓨터)에 대 한 hello 호스트 운영 체제에서 수집한 성능 카운터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="eb6a4-130">*자세한 정보 표시 모니터링* hello 역할 인스턴스 tooenable 보다 자세하게 분석 응용 프로그램 처리 하는 동안 발생 하는 문제 내에서 성능 데이터를 기반으로 하는 추가 메트릭을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="eb6a4-131">tooenable Azure 진단을 참조 하는 방법에 대해 toofind [Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="eb6a4-132">해야 클라우드 서비스 웹 역할 또는 작업자 역할의 배포와 toocreate [hello 서비스 패키지 만들기](cloud-services-model-and-package.md#servicepackagecspkg)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eb6a4-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="eb6a4-133">Before you begin</span></span>
* <span data-ttu-id="eb6a4-134">Hello Azure SDK를 설치 하지 않은 경우 클릭 **Azure SDK 설치** tooopen hello [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/), 한 후 hello를 원하는 언어 toodevelop 코드에 대 한 hello SDK를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="eb6a4-135">(해야 합니다. 영업 기회 toodo이 나중에.)</span><span class="sxs-lookup"><span data-stu-id="eb6a4-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="eb6a4-136">인증서를 요구 하는 모든 역할 인스턴스를 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="eb6a4-137">클라우드 서비스에는 개인 키가 포함된 .pfx 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="eb6a4-138">Hello 클라우드 서비스 배포를 만들 때 hello 인증서 tooAzure를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="eb6a4-139">만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="eb6a4-139">Create and deploy</span></span>
1. <span data-ttu-id="eb6a4-140">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eb6a4-141">클릭 **새로 만들기 > 계산**, 한 다음 tooand 클릭 아래로 스크롤하여 **클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="eb6a4-143">새 hello에 **클라우드 서비스** 블레이드에서 hello에 대 한 값을 입력 **DNS 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="eb6a4-144">새 **리소스 그룹** 을 만들거나 기존 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="eb6a4-145">**위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-145">Select a **Location**.</span></span>
6. <span data-ttu-id="eb6a4-146">**패키지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-146">Click **Package**.</span></span> <span data-ttu-id="eb6a4-147">Hello 열립니다 **패키지 업로드** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="eb6a4-148">Hello 필수 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-148">Fill in hello required fields.</span></span> <span data-ttu-id="eb6a4-149">역할에 단일 인스턴스가 포함된 경우 **단일 인스턴스가 포함된 역할이 하나 이상 있는 경우에도 배포합니다.** 가 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="eb6a4-150">**배포 시작** 이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="eb6a4-151">클릭 **확인** hello 닫힙니다 **패키지 업로드** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="eb6a4-152">모든 인증서 tooadd가 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="eb6a4-154">인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="eb6a4-154">Upload a certificate</span></span>
<span data-ttu-id="eb6a4-155">배포 패키지 되었으면 [toouse 인증서 구성](cloud-services-configure-ssl-certificate-portal.md#modify), 이제 hello 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="eb6a4-156">선택 **인증서**, 등과 hello **인증서 추가** 블레이드에서 hello SSL 인증서.pfx 파일을 선택 하 고 hello를 입력 하십시오 **암호** hello 인증서에 대 한</span><span class="sxs-lookup"><span data-stu-id="eb6a4-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="eb6a4-157">클릭 **연결 인증서**, 클릭 하 고 **확인** hello에 **인증서 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="eb6a4-158">클릭 **만들기** hello에 **클라우드 서비스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="eb6a4-159">Hello 배포 hello에 도달한 경우 **준비** 상태, toohello 다음 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="eb6a4-161">배포가 완료되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="eb6a4-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="eb6a4-162">Hello 클라우드 서비스 인스턴스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="eb6a4-163">hello 상태가 표시 hello 서비스가 임을 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="eb6a4-164">아래 **Essentials**, hello 클릭 **사이트 URL** tooopen 웹 브라우저에서 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb6a4-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="eb6a4-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb6a4-166">Next steps</span></span>
* <span data-ttu-id="eb6a4-167">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eb6a4-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="eb6a4-168">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="eb6a4-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="eb6a4-169">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eb6a4-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="eb6a4-170">[SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="eb6a4-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
