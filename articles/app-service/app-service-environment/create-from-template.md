---
title: "aaaCreate 리소스 관리자 템플릿을 사용 하 여 Azure 앱 서비스 환경"
description: "에 대해 설명 어떻게 toocreate 리소스 관리자 템플릿을 사용 하 여 외부 웹 서비스 또는 ILB Azure 앱 서비스 환경"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="dcd6a-103">Azure Resource Manager 템플릿을 사용하여 ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="dcd6a-103">Create an ASE by using an Azure Resource Manager template</span></span>

## <a name="overview"></a><span data-ttu-id="dcd6a-104">개요</span><span class="sxs-lookup"><span data-stu-id="dcd6a-104">Overview</span></span>
<span data-ttu-id="dcd6a-105">Azure ASE(App Service Environment)는 인터넷에 액세스할 수 있는 끝점 또는 Azure VNet(Virtual Network)의 내부 주소에 있는 끝점을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span></span> <span data-ttu-id="dcd6a-106">끝점이 내부 끝점을 사용하여 만들어진 경우 ILB(내부 부하 분산 장치)를 호출하는 Azure구성 요소에서 해당 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span></span> <span data-ttu-id="dcd6a-107">내부 IP 주소에 ASE hello ILB ASE 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-107">hello ASE on an internal IP address is called an ILB ASE.</span></span> <span data-ttu-id="dcd6a-108">공용 끝점이 있는 hello ASE 외부 ASE 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-108">hello ASE with a public endpoint is called an External ASE.</span></span> 

<span data-ttu-id="dcd6a-109">ASE는 hello Azure 포털 또는 Azure 리소스 관리자 템플릿을 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-109">An ASE can be created by using hello Azure portal or an Azure Resource Manager template.</span></span> <span data-ttu-id="dcd6a-110">이 문서는 hello 단계와 리소스 관리자 템플릿으로 toocreate 외부 ASE 또는 ILB ASE 필요한 구문 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-110">This article walks through hello steps and syntax you need toocreate an External ASE or ILB ASE with Resource Manager templates.</span></span> <span data-ttu-id="dcd6a-111">toolearn toocreate ASE hello Azure 포털에서에서 참조 하는 방법을 [외부 ASE 확인] [ MakeExternalASE] 또는 [ILB ASE 확인][MakeILBASE]합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-111">toolearn how toocreate an ASE in hello Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="dcd6a-112">Hello Azure 포털에서에서 ASE를 만들면 시간 같거나에 기존 VNet toodeploy 선택 hello에서 VNet을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-112">When you create an ASE in hello Azure portal, you can create your VNet at hello same time or choose a preexisting VNet toodeploy into.</span></span> <span data-ttu-id="dcd6a-113">템플릿에서 ASE를 만들 경우 다음 항목을 미리 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-113">When you create an ASE from a template, you must start with:</span></span> 

* <span data-ttu-id="dcd6a-114">Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="dcd6a-114">A Resource Manager VNet.</span></span>
* <span data-ttu-id="dcd6a-115">해당 VNet의 서브넷</span><span class="sxs-lookup"><span data-stu-id="dcd6a-115">A subnet in that VNet.</span></span> <span data-ttu-id="dcd6a-116">ASE 서브넷 크기는 것이 좋습니다 `/25` 128 주소 tooaccomodate 미래 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-116">We recommend an ASE subnet size of `/25` with 128 addresses tooaccomodate future growth.</span></span> <span data-ttu-id="dcd6a-117">Hello ASE를 만든 후에 hello 크기를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-117">After hello ASE is created, you can't change hello size.</span></span>
* <span data-ttu-id="dcd6a-118">VNet에서 hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-118">hello resource ID from your VNet.</span></span> <span data-ttu-id="dcd6a-119">가상 네트워크 속성에서 hello Azure 포털에서에서이 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-119">You can get this information from hello Azure portal under your virtual network properties.</span></span>
* <span data-ttu-id="dcd6a-120">toodeploy에 원하는 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-120">hello subscription you want toodeploy into.</span></span>
* <span data-ttu-id="dcd6a-121">toodeploy에 원하는 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-121">hello location you want toodeploy into.</span></span>

<span data-ttu-id="dcd6a-122">tooautomate ASE 만들기:</span><span class="sxs-lookup"><span data-stu-id="dcd6a-122">tooautomate your ASE creation:</span></span>

1. <span data-ttu-id="dcd6a-123">서식 파일에서 hello ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-123">Create hello ASE from a template.</span></span> <span data-ttu-id="dcd6a-124">외부 ASE를 만드는 경우에는 이 단계를 수행하면 만들기가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-124">If you create an External ASE, you're finished after this step.</span></span> <span data-ttu-id="dcd6a-125">ILB ASE를 만들면 더 많은 작업 toodo 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-125">If you create an ILB ASE, there are a few more things toodo.</span></span>

2. <span data-ttu-id="dcd6a-126">ILB ASE를 만든 후에 ILB ASE 도메인과 일치하는 SSL 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span></span>

3. <span data-ttu-id="dcd6a-127">hello 업로드 된 SSL 인증서가 할당 toohello ILB ASE "default" SSL 인증서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-127">hello uploaded SSL certificate is assigned toohello ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="dcd6a-128">이 인증서는 hello 공통 루트 도메인에 할당 된 toohello ASE (예를 들어 https://someapp.mycustomrootcomain.com)를 사용할 때 SSL 트래픽 tooapps ILB ASE hello에 대 한 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-128">This certificate is used for SSL traffic tooapps on hello ILB ASE when they use hello common root domain that's assigned toohello ASE (for example, https://someapp.mycustomrootcomain.com).</span></span>


## <a name="create-hello-ase"></a><span data-ttu-id="dcd6a-129">Hello ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="dcd6a-129">Create hello ASE</span></span>
<span data-ttu-id="dcd6a-130">ASE를 만드는 Resource Manager 템플릿 및 관련 매개 변수 파일은 GitHub의 [예제][quickstartasev2create]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span></span>

<span data-ttu-id="dcd6a-131">Toomake ILB ASE를 사용 하도록 하려는 경우 이러한 리소스 관리자 템플릿을 사용 하 여 [예제][quickstartilbasecreate]합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-131">If you want toomake an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span></span> <span data-ttu-id="dcd6a-132">이므로 toothat 사용 사례를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-132">They cater toothat use case.</span></span> <span data-ttu-id="dcd6a-133">Hello의 hello 매개 변수 대부분 *azuredeploy.parameters.json* 파일 ILB ASEs 및 외부 ASEs 일반적인 toohello 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-133">Most of hello parameters in hello *azuredeploy.parameters.json* file are common toohello creation of ILB ASEs and External ASEs.</span></span> <span data-ttu-id="dcd6a-134">hello 다음 목록에서는 관련 참고의 매개 변수 또는 ILB ASE를 만들 때 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-134">hello following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span></span>

* <span data-ttu-id="dcd6a-135">*interalLoadBalancingMode*: 대부분의 경우에서 80/443 포트에서 HTTP/HTTPS 트래픽을 모두 즉이 too3를 설정 하 고 hello 컨트롤/데이터 채널 포트 hello ASE에 tooby hello FTP 서비스를 수신 대기, 바인딩된 tooan ILB 할당 된 가상 네트워크 됩니다 내부 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-135">*interalLoadBalancingMode*: In most cases, set this too3, which means both HTTP/HTTPS traffic on ports 80/443, and hello control/data channel ports listened tooby hello FTP service on hello ASE, will be bound tooan ILB-allocated virtual network internal address.</span></span> <span data-ttu-id="dcd6a-136">이 속성은 too2을 설정 하는 경우 유일한 hello FTP 서비스와 관련 된 포트 (둘 다 제어 및 데이터 채널)는 바인딩된 tooan ILB 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-136">If this property is set too2, only hello FTP service-related ports (both control and data channels) are bound tooan ILB address.</span></span> <span data-ttu-id="dcd6a-137">HTTP/HTTPS 트래픽을 hello hello 공용 VIP에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-137">hello HTTP/HTTPS traffic remains on hello public VIP.</span></span>
* <span data-ttu-id="dcd6a-138">*dnsSuffix*:이 매개 변수는 할당 된 toohello ASE hello 기본 루트 도메인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-138">*dnsSuffix*: This parameter defines hello default root domain that's assigned toohello ASE.</span></span> <span data-ttu-id="dcd6a-139">Azure 앱 서비스의 공용 변형을 hello hello 기본 루트 도메인 모든 웹 앱에 대 한는 *azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-139">In hello public variation of Azure App Service, hello default root domain for all web apps is *azurewebsites.net*.</span></span> <span data-ttu-id="dcd6a-140">ILB ASE 내부 tooa 고객의 가상 네트워크 이기 때문에 것으로 감지 toouse hello 공용 서비스 기본 루트 도메인을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-140">Because an ILB ASE is internal tooa customer's virtual network, it doesn't make sense toouse hello public service's default root domain.</span></span> <span data-ttu-id="dcd6a-141">대신, ILB ASE에는 회사의 내부 가상 네트워크 내에서 사용하기 적합한 기본 루트 도메인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span> <span data-ttu-id="dcd6a-142">Contoso Corporation의 기본 루트 도메인을 사용할 수는 예를 들어 *내부 contoso.com* 의도 한 toobe 확인 가능한 및 Contoso 가상 네트워크 내 에서만 액세스할 수 있는 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended toobe resolvable and accessible only within Contoso's virtual network.</span></span> 
* <span data-ttu-id="dcd6a-143">*ipSslAddressCount*:이 매개 변수의 tooa hello에 0 값을 자동으로 기본값 *azuredeploy.json* ILB ASEs 단일 ILB 주소 하나만 있으므로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-143">*ipSslAddressCount*: This parameter automatically defaults tooa value of 0 in hello *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span> <span data-ttu-id="dcd6a-144">ILB ASE용 명시적 IP-SSL 주소는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-144">There are no explicit IP-SSL addresses for an ILB ASE.</span></span> <span data-ttu-id="dcd6a-145">따라서 toozero hello ILB ASE에 대 한 IP SSL 주소 풀에 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-145">Hence, hello IP-SSL address pool for an ILB ASE must be set toozero.</span></span> <span data-ttu-id="dcd6a-146">그렇지 않으면 프로비전 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-146">Otherwise, a provisioning error occurs.</span></span> 

<span data-ttu-id="dcd6a-147">Hello 후 *azuredeploy.parameters.json* hello PowerShell 코드 조각을 사용 하 여 hello ASE를 만들기, 파일에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-147">After hello *azuredeploy.parameters.json* file is filled in, create hello ASE by using hello PowerShell code snippet.</span></span> <span data-ttu-id="dcd6a-148">Hello 파일 경로 toomatch hello 리소스 관리자 템플릿 파일 위치에 컴퓨터를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-148">Change hello file paths toomatch hello Resource Manager template-file locations on your machine.</span></span> <span data-ttu-id="dcd6a-149">Toosupply hello 리소스 관리자 배포 이름 및 hello 리소스 그룹 이름에 대 한 고유한 값을 고려 하세요.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-149">Remember toosupply your own values for hello Resource Manager deployment name and hello resource group name:</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="dcd6a-150">Hello ASE toobe 생성에 대 한 시간에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-150">It takes about an hour for hello ASE toobe created.</span></span> <span data-ttu-id="dcd6a-151">그런 다음 hello ASE hello 포털 ASEs hello 배포를 트리거한 hello 구독에 대 한 hello 목록에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-151">Then hello ASE shows up in hello portal in hello list of ASEs for hello subscription that triggered hello deployment.</span></span>

## <a name="upload-and-configure-hello-default-ssl-certificate"></a><span data-ttu-id="dcd6a-152">업로드 하 고 hello "기본" SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="dcd6a-152">Upload and configure hello "default" SSL certificate</span></span>
<span data-ttu-id="dcd6a-153">SSL 인증서를 사용 하는 tooestablish SSL 연결 tooapps hello "기본" SSL 인증서로 hello ASE와 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-153">An SSL certificate must be associated with hello ASE as hello "default" SSL certificate that's used tooestablish SSL connections tooapps.</span></span> <span data-ttu-id="dcd6a-154">Hello ASE의 기본 DNS 접미사가 *내부 contoso.com*, 연결 toohttps://some-random-app.internal-contoso.com에 유효한 SSL 인증서가 필요 **.internal contoso.com* .</span><span class="sxs-lookup"><span data-stu-id="dcd6a-154">If hello ASE's default DNS suffix is *internal-contoso.com*, a connection toohttps://some-random-app.internal-contoso.com requires an SSL certificate that's valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="dcd6a-155">내부 인증 기관을 사용하거나, 외부 발급자로부터 인증서를 구입하거나, 자체 서명된 인증서를 사용하는 등의 방법으로 유효한 SSL 인증서를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span></span> <span data-ttu-id="dcd6a-156">Hello SSL 인증서의 hello 소스에 관계 없이 hello 인증서 특성에 따라 올바르게 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-156">Regardless of hello source of hello SSL certificate, hello following certificate attributes must be configured properly:</span></span>

* <span data-ttu-id="dcd6a-157">**제목**:이 속성을 너무 설정 되어야 합니다. **루트 도메인 here.com.your*합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-157">**Subject**: This attribute must be set too**.your-root-domain-here.com*.</span></span>
* <span data-ttu-id="dcd6a-158">**주체 대체 이름**: 이 특성에는 **.your-root-domain-here.com* 및 **.scm.your-root-domain-here.com*이 둘 다 포함되어야 합니다. Hello 폼의 주소를 사용 하는 SSL 연결 toohello 각 앱과 연결 된 SCM/Kudu 사이트 *your-app-name.scm.your-root-domain-here.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-158">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here.com* and **.scm.your-root-domain-here.com*. SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="dcd6a-159">유효한 SSL 인증서가 있는 경우 두 가지 추가 준비 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-159">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span> <span data-ttu-id="dcd6a-160">.Pfx 파일로 hello SSL 인증서를 convert/저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-160">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="dcd6a-161">Hello.pfx 파일 해야 모든 중간 포함 한 루트 인증서를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-161">Remember that hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="dcd6a-162">암호로 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-162">Secure it with a password.</span></span>

<span data-ttu-id="dcd6a-163">hello.pfx 파일 toobe 리소스 관리자 템플릿을 사용 하 여 hello SSL 인증서가 업로드 하기 때문에 base64 문자열로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-163">hello .pfx file needs toobe converted into a base64 string because hello SSL certificate is uploaded by using a Resource Manager template.</span></span> <span data-ttu-id="dcd6a-164">리소스 관리자 템플릿을 텍스트 파일 이기 때문에 base64 문자열로 hello.pfx 파일을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-164">Because Resource Manager templates are text files, hello .pfx file must be converted into a base64 string.</span></span> <span data-ttu-id="dcd6a-165">이렇게 hello 서식 파일의 매개 변수로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-165">This way it can be included as a parameter of hello template.</span></span>

<span data-ttu-id="dcd6a-166">다음 PowerShell 코드 조각을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-166">Use hello following PowerShell code snippet to:</span></span>

* <span data-ttu-id="dcd6a-167">자체 서명된 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-167">Generate a self-signed certificate.</span></span>
* <span data-ttu-id="dcd6a-168">Hello 인증서를.pfx 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-168">Export hello certificate as a .pfx file.</span></span>
* <span data-ttu-id="dcd6a-169">Hello.pfx 파일을 base 64로 인코딩된 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-169">Convert hello .pfx file into a base64-encoded string.</span></span>
* <span data-ttu-id="dcd6a-170">Hello base64 인코딩 문자열 tooa 별도 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-170">Save hello base64-encoded string tooa separate file.</span></span> 

<span data-ttu-id="dcd6a-171">이 PowerShell 코드 base64 인코딩에 대 한 hello에서 변형 되었습니다 [PowerShell 스크립트 블로그][examplebase64encoding]:</span><span class="sxs-lookup"><span data-stu-id="dcd6a-171">This PowerShell code for base64 encoding was adapted from hello [PowerShell scripts blog][examplebase64encoding]:</span></span>

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="dcd6a-172">Hello SSL 인증서가 성공적으로 생성 된 tooa base64 인코딩 문자열로 변환 후 hello 예제 리소스 관리자 템플릿을 사용 [구성 hello 기본 SSL 인증서] [ quickstartconfiguressl] GitHub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-172">After hello SSL certificate is successfully generated and converted tooa base64-encoded string, use hello example Resource Manager template [Configure hello default SSL certificate][quickstartconfiguressl] on GitHub.</span></span> 

<span data-ttu-id="dcd6a-173">hello에 대 한 매개 변수를 hello *azuredeploy.parameters.json* 파일 여기에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-173">hello parameters in hello *azuredeploy.parameters.json* file are listed here:</span></span>

* <span data-ttu-id="dcd6a-174">*appServiceEnvironmentName*: hello 구성 되 고 ILB ASE의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-174">*appServiceEnvironmentName*: hello name of hello ILB ASE being configured.</span></span>
* <span data-ttu-id="dcd6a-175">*existingAseLocation*: hello ILB ASE를 배포할 Azure 지역 hello 포함 된 텍스트 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-175">*existingAseLocation*: Text string containing hello Azure region where hello ILB ASE was deployed.</span></span>  <span data-ttu-id="dcd6a-176">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-176">For example: "South Central US".</span></span>
* <span data-ttu-id="dcd6a-177">*pfxBlobString*: hello hello.pfx 파일의 based64로 인코딩된 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-177">*pfxBlobString*: hello based64-encoded string representation of hello .pfx file.</span></span> <span data-ttu-id="dcd6a-178">앞에 표시 된 hello 코드 조각을 사용 하 고 "exportedcert.pfx.b64"에 포함 된 hello 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-178">Use hello code snippet shown earlier and copy hello string contained in "exportedcert.pfx.b64".</span></span> <span data-ttu-id="dcd6a-179">Hello의 hello 값으로 붙여 *pfxBlobString* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-179">Paste it in as hello value of hello *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="dcd6a-180">*암호*: hello 사용 되는 암호 toosecure hello.pfx 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-180">*password*: hello password used toosecure hello .pfx file.</span></span>
* <span data-ttu-id="dcd6a-181">*certificateThumbprint*: hello 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-181">*certificateThumbprint*: hello certificate's thumbprint.</span></span> <span data-ttu-id="dcd6a-182">PowerShell에서이 값을 검색 하는 경우 (예를 들어 *$certificate 합니다. 지문* hello에서 이전 코드 조각)을 그대로 hello 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-182">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from hello earlier code snippet), you can use hello value as is.</span></span> <span data-ttu-id="dcd6a-183">Hello Windows 인증서 대화 상자에서 hello 값을 복사 하는 경우 불필요 한 공백 hello 아웃 toostrip을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-183">If you copy hello value from hello Windows certificate dialog box, remember toostrip out hello extraneous spaces.</span></span> <span data-ttu-id="dcd6a-184">hello *certificateThumbprint* AF3143EB61D43F6727842115BB7F17BBCECAECAE 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-184">hello *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span></span>
* <span data-ttu-id="dcd6a-185">*certificateName*: tooidentity hello 인증서를 사용 하는 사용자가 선택한의 문자열 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-185">*certificateName*: A friendly string identifier of your own choosing used tooidentity hello certificate.</span></span> <span data-ttu-id="dcd6a-186">hello 이름이 hello에 대 한 hello 고유한 리소스 관리자 식별자의 일부로 사용 됩니다 *Microsoft.Web/certificates* hello SSL 인증서를 나타내는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-186">hello name is used as part of hello unique Resource Manager identifier for hello *Microsoft.Web/certificates* entity that represents hello SSL certificate.</span></span> <span data-ttu-id="dcd6a-187">hello 이름 *해야* hello 접미사를 다음으로 끝나는: \_yourASENameHere_InternalLoadBalancingASE 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-187">hello name *must* end with hello following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span></span> <span data-ttu-id="dcd6a-188">표시기 hello 인증서를 사용 하는 toosecure ILB 사용이 가능한 ASE를 그대로 hello Azure 포털에서이 접미사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-188">hello Azure portal uses this suffix as an indicator that hello certificate is used toosecure an ILB-enabled ASE.</span></span>

<span data-ttu-id="dcd6a-189">*azuredeploy.parameters.json*을 축약한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-189">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span></span>

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

<span data-ttu-id="dcd6a-190">Hello 후 *azuredeploy.parameters.json* hello PowerShell 코드 조각을 사용 하 여 hello 기본 SSL 인증서를 구성, 파일에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-190">After hello *azuredeploy.parameters.json* file is filled in, configure hello default SSL certificate by using hello PowerShell code snippet.</span></span> <span data-ttu-id="dcd6a-191">Hello 파일 경로 toomatch hello 리소스 관리자 템플릿 파일이 컴퓨터에 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-191">Change hello file paths toomatch where hello Resource Manager template files are located on your machine.</span></span> <span data-ttu-id="dcd6a-192">Toosupply hello 리소스 관리자 배포 이름 및 hello 리소스 그룹 이름에 대 한 고유한 값을 고려 하세요.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-192">Remember toosupply your own values for hello Resource Manager deployment name and hello resource group name:</span></span>

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="dcd6a-193">ASE 프런트 엔드 tooapply hello 변경 당 약 40 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-193">It takes roughly 40 minutes per ASE front end tooapply hello change.</span></span> <span data-ttu-id="dcd6a-194">예를 들어 두 개의 프런트 엔드를 사용 하는 기본 크기의 ASE hello 템플릿 1 시간 및 20 분 toocomplete 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-194">For example, for a default-sized ASE that uses two front ends, hello template takes around one hour and 20 minutes toocomplete.</span></span> <span data-ttu-id="dcd6a-195">Hello 템플릿 실행 되는 동안 hello ASE 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-195">While hello template is running, hello ASE can't scale.</span></span>  

<span data-ttu-id="dcd6a-196">Hello 템플릿 완료 되 면 앱 ILB ASE hello에 HTTPS를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-196">After hello template finishes, apps on hello ILB ASE can be accessed over HTTPS.</span></span> <span data-ttu-id="dcd6a-197">hello 연결은 hello 기본 SSL 인증서를 사용 하 여 보안이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-197">hello connections are secured by using hello default SSL certificate.</span></span> <span data-ttu-id="dcd6a-198">hello 응용 프로그램 이름 및 hello 기본 호스트 이름 조합을 사용 하 여 hello ILB ASE에 응용 프로그램은 해결 되 면 hello 기본 SSL 인증서가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-198">hello default SSL certificate is used when apps on hello ILB ASE are addressed by using a combination of hello application name plus hello default host name.</span></span> <span data-ttu-id="dcd6a-199">Https://mycustomapp.internal-contoso.com hello 기본 SSL 인증서를 사용 하는 예를 들어 **.internal contoso.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-199">For example, https://mycustomapp.internal-contoso.com uses hello default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="dcd6a-200">그러나 다중 테 넌 트 서비스를 공개 하는 hello에 실행 되는 앱에서와 마찬가지로 개발자는 개별 응용 프로그램에 대 한 사용자 지정 호스트 이름을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-200">However, just like apps that run on hello public multitenant service, developers can configure custom host names for individual apps.</span></span> <span data-ttu-id="dcd6a-201">또한 개별 앱에 대해 고유한 SNI SSL 인증서 바인딩을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-201">They also can configure unique SNI SSL certificate bindings for individual apps.</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="dcd6a-202">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="dcd6a-202">App Service Environment v1</span></span> ##
<span data-ttu-id="dcd6a-203">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-203">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="dcd6a-204">앞에 정보 hello ASEv2 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-204">hello preceding information was based on ASEv2.</span></span> <span data-ttu-id="dcd6a-205">이 섹션 ASEv1와 ASEv2 차이점 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-205">This section shows you hello differences between ASEv1 and ASEv2.</span></span>

<span data-ttu-id="dcd6a-206">, ASEv1 관리 hello 리소스를 모두 수동으로.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-206">In ASEv1, you manage all of hello resources manually.</span></span> <span data-ttu-id="dcd6a-207">Hello 프런트 엔드, 작업자 및 IP 기반 SSL에 사용 되는 IP 주소를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-207">That includes hello front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="dcd6a-208">앱 서비스 계획을 확장할 수 있습니다, 전에 수평 확장 해야 합니다 hello 작업자 풀 toohost 원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-208">Before you can scale out your App Service plan, you must scale out hello worker pool that you want toohost it.</span></span>

<span data-ttu-id="dcd6a-209">ASEv1은 ASEv2와는 다른 가격 책정 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-209">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="dcd6a-210">ASEv1에서는 할당된 각 코어에 대한 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-210">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="dcd6a-211">여기에는 작업을 호스트하지 않는 프런트 엔드 또는 작업자에 사용되는 코어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-211">That includes cores that are used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="dcd6a-212">ASEv1에서 hello 기본 최대 규모의 ASE 크기가 55 총 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-212">In ASEv1, hello default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="dcd6a-213">여기에는 작업자 및 프런트 엔드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-213">That includes workers and front ends.</span></span> <span data-ttu-id="dcd6a-214">한 이점은 tooASEv1은 클래식 가상 네트워크와 리소스 관리자 가상 네트워크에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-214">One advantage tooASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="dcd6a-215">toolearn ASEv1에 대 한 자세한 참조 [앱 서비스 환경 v1 소개][ASEv1Intro]합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-215">toolearn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<span data-ttu-id="dcd6a-216">리소스 관리자 템플릿을 사용 하 여 프로그램 ASEv1 toocreate 참조 [ILB ASE v1 리소스 관리자 템플릿을 사용 하 여 만들][ILBASEv1Template]합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-216">toocreate an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span></span>


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
