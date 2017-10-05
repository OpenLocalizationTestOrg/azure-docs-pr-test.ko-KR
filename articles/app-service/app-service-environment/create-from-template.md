---
title: "Resource Manager 템플릿을 사용하여 Azure App Service Environment 만들기"
description: "Resource Manager 템플릿을 사용하여 외부 또는 ILB Azure App Service Environment를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: e6b21086488352c1da914b4656ad1d216fd6de85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="14761-103">Azure Resource Manager 템플릿을 사용하여 ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="14761-103">Create an ASE by using an Azure Resource Manager template</span></span>

## <a name="overview"></a><span data-ttu-id="14761-104">개요</span><span class="sxs-lookup"><span data-stu-id="14761-104">Overview</span></span>
<span data-ttu-id="14761-105">Azure ASE(App Service Environment)는 인터넷에 액세스할 수 있는 끝점 또는 Azure VNet(Virtual Network)의 내부 주소에 있는 끝점을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span></span> <span data-ttu-id="14761-106">끝점이 내부 끝점을 사용하여 만들어진 경우 ILB(내부 부하 분산 장치)를 호출하는 Azure구성 요소에서 해당 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span></span> <span data-ttu-id="14761-107">내부 IP 주소의 ASE를 ILB ASE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-107">The ASE on an internal IP address is called an ILB ASE.</span></span> <span data-ttu-id="14761-108">공용 끝점이 있는 ASE를 외부 ASE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-108">The ASE with a public endpoint is called an External ASE.</span></span> 

<span data-ttu-id="14761-109">Azure Portal 또는 Azure Resource Manager 템플릿을 사용하여 ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-109">An ASE can be created by using the Azure portal or an Azure Resource Manager template.</span></span> <span data-ttu-id="14761-110">이 문서에서는 Resource Manager 템플릿으로 외부 ASE 또는 ILB ASE를 만드는 데 필요한 단계와 구문을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-110">This article walks through the steps and syntax you need to create an External ASE or ILB ASE with Resource Manager templates.</span></span> <span data-ttu-id="14761-111">Azure Portal에서 ASE를 만드는 방법에 대해 알아보려면 [외부 ASE 만들기][MakeExternalASE] 또는 [ILB ASE 만들기][MakeILBASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14761-111">To learn how to create an ASE in the Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="14761-112">Azure Portal에서 ASE를 만들 때는 동시에 VNet를 만들거나 ASE를 배포할 기존 VNet를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-112">When you create an ASE in the Azure portal, you can create your VNet at the same time or choose a preexisting VNet to deploy into.</span></span> <span data-ttu-id="14761-113">템플릿에서 ASE를 만들 경우 다음 항목을 미리 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-113">When you create an ASE from a template, you must start with:</span></span> 

* <span data-ttu-id="14761-114">Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="14761-114">A Resource Manager VNet.</span></span>
* <span data-ttu-id="14761-115">해당 VNet의 서브넷</span><span class="sxs-lookup"><span data-stu-id="14761-115">A subnet in that VNet.</span></span> <span data-ttu-id="14761-116">향후 확장이 가능하도록 128개의 주소를 포함할 수 있는 `/25` 크기의 ASE 서브넷을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-116">We recommend an ASE subnet size of `/25` with 128 addresses to accomodate future growth.</span></span> <span data-ttu-id="14761-117">ASE를 만든 후에는 크기를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-117">After the ASE is created, you can't change the size.</span></span>
* <span data-ttu-id="14761-118">VNet의 리소스 ID.</span><span class="sxs-lookup"><span data-stu-id="14761-118">The resource ID from your VNet.</span></span> <span data-ttu-id="14761-119">Azure Portal의 가상 네트워크 속성에서 이 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-119">You can get this information from the Azure portal under your virtual network properties.</span></span>
* <span data-ttu-id="14761-120">ASE를 배포할 구독</span><span class="sxs-lookup"><span data-stu-id="14761-120">The subscription you want to deploy into.</span></span>
* <span data-ttu-id="14761-121">ASE를 배포할 위치</span><span class="sxs-lookup"><span data-stu-id="14761-121">The location you want to deploy into.</span></span>

<span data-ttu-id="14761-122">ASE 만들기를 자동화하려면:</span><span class="sxs-lookup"><span data-stu-id="14761-122">To automate your ASE creation:</span></span>

1. <span data-ttu-id="14761-123">템플릿에서 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14761-123">Create the ASE from a template.</span></span> <span data-ttu-id="14761-124">외부 ASE를 만드는 경우에는 이 단계를 수행하면 만들기가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-124">If you create an External ASE, you're finished after this step.</span></span> <span data-ttu-id="14761-125">ILB ASE를 만드는 경우에는 몇 가지 추가 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-125">If you create an ILB ASE, there are a few more things to do.</span></span>

2. <span data-ttu-id="14761-126">ILB ASE를 만든 후에 ILB ASE 도메인과 일치하는 SSL 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span></span>

3. <span data-ttu-id="14761-127">업로드된 SSL 인증서는 해당 "기본" SSL 인증서로서 ILB ASE에 명시적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-127">The uploaded SSL certificate is assigned to the ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="14761-128">이 SSL 인증서는 ASE에 할당된 공용 루트 도메인(예: https://someapp.mycustomrootcomain.com)을 사용할 때 ILB ASE의 앱으로 이동되는 SSL 트래픽에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-128">This certificate is used for SSL traffic to apps on the ILB ASE when they use the common root domain that's assigned to the ASE (for example, https://someapp.mycustomrootcomain.com).</span></span>


## <a name="create-the-ase"></a><span data-ttu-id="14761-129">ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="14761-129">Create the ASE</span></span>
<span data-ttu-id="14761-130">ASE를 만드는 Resource Manager 템플릿 및 관련 매개 변수 파일은 GitHub의 [예제][quickstartasev2create]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span></span>

<span data-ttu-id="14761-131">ILB ASE를 만들려는 경우에는 이 Resource Manager 템플릿 [예제][quickstartilbasecreate]를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="14761-131">If you want to make an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span></span> <span data-ttu-id="14761-132">해당 사용 사례를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-132">They cater to that use case.</span></span> <span data-ttu-id="14761-133">*azuredeploy.parameters.json* 파일에 있는 대부분의 매개 변수는 ILB ASE와 외부 ASE 둘 다를 만들 때 공통적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-133">Most of the parameters in the *azuredeploy.parameters.json* file are common to the creation of ILB ASEs and External ASEs.</span></span> <span data-ttu-id="14761-134">아래 목록에는 ILB ASE를 만들 때 특히 주의해야 하는 매개 변수 또는 고유한 매개 변수가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-134">The following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span></span>

* <span data-ttu-id="14761-135">*interalLoadBalancingMode*: 대부분의 경우에는 3으로 설정합니다. 이 값은 포트 80/443의 HTTP/HTTPS 트래픽과 ASE의 FTP 서비스에서 수신하는 컨트롤/데이터 채널 포트가 ILB 할당 가상 네트워크 내부 주소에 바인딩될 것임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-135">*interalLoadBalancingMode*: In most cases, set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB-allocated virtual network internal address.</span></span> <span data-ttu-id="14761-136">이 속성을 2로 설정하면 FTP 서비스 관련 포트(컨트롤 채널과 데이터 채널 둘 다)만 ILB 주소로 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-136">If this property is set to 2, only the FTP service-related ports (both control and data channels) are bound to an ILB address.</span></span> <span data-ttu-id="14761-137">HTTP/HTTPS 트래픽은 공용 VIP에 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-137">The HTTP/HTTPS traffic remains on the public VIP.</span></span>
* <span data-ttu-id="14761-138">*dnsSuffix*: 이 매개 변수는 ASE에 할당되는 기본 루트 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-138">*dnsSuffix*: This parameter defines the default root domain that's assigned to the ASE.</span></span> <span data-ttu-id="14761-139">Azure 앱 서비스의 공용 변형에서 모든 웹앱용 기본 루트 도메인은 *azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-139">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span></span> <span data-ttu-id="14761-140">ILB ASE는 고객의 가상 네트워크 내부에 있으므로 공용 서비스의 기본 루트 도메인을 사용하는 것은 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-140">Because an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span></span> <span data-ttu-id="14761-141">대신, ILB ASE에는 회사의 내부 가상 네트워크 내에서 사용하기 적합한 기본 루트 도메인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span> <span data-ttu-id="14761-142">예를 들어 Contoso Corporation은 Contoso의 가상 네트워크 내에서만 확인 가능하고 액세스할 수 있는 앱에 기본 루트 도메인 *internal-contoso.com*을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to be resolvable and accessible only within Contoso's virtual network.</span></span> 
* <span data-ttu-id="14761-143">*ipSslAddressCount*: 이 매개 변수는 *azuredeploy.json* 파일에서 자동으로 기본값인 0으로 지정됩니다. ILB ASE에는 ILB 주소가 하나뿐이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-143">*ipSslAddressCount*: This parameter automatically defaults to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span> <span data-ttu-id="14761-144">ILB ASE용 명시적 IP-SSL 주소는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-144">There are no explicit IP-SSL addresses for an ILB ASE.</span></span> <span data-ttu-id="14761-145">따라서 ILB ASE용 IP-SSL 주소 풀은 0으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-145">Hence, the IP-SSL address pool for an ILB ASE must be set to zero.</span></span> <span data-ttu-id="14761-146">그렇지 않으면 프로비전 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-146">Otherwise, a provisioning error occurs.</span></span> 

<span data-ttu-id="14761-147">*azuredeploy.parameters.json* 파일에 매개 변수를 입력한 후 PowerShell 코드 조각을 사용하여 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14761-147">After the *azuredeploy.parameters.json* file is filled in, create the ASE by using the PowerShell code snippet.</span></span> <span data-ttu-id="14761-148">컴퓨터의 Resource Manager 템플릿 파일 위치와 일치하도록 파일 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-148">Change the file paths to match the Resource Manager template-file locations on your machine.</span></span> <span data-ttu-id="14761-149">Resource Manager 배포 이름 및 리소스 그룹 이름에 대해 고유한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-149">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="14761-150">ASE가 작성되려면 1시간 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="14761-150">It takes about an hour for the ASE to be created.</span></span> <span data-ttu-id="14761-151">이 시간이 지나면 ASE가 Portal에서 배포를 트리거한 구독의 ASE 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-151">Then the ASE shows up in the portal in the list of ASEs for the subscription that triggered the deployment.</span></span>

## <a name="upload-and-configure-the-default-ssl-certificate"></a><span data-ttu-id="14761-152">"기본" SSL 인증서 업로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="14761-152">Upload and configure the "default" SSL certificate</span></span>
<span data-ttu-id="14761-153">SSL 인증서를 앱에 대한 SSL 연결을 설정하는 데 사용되는 "기본" SSL 인증서로 ASE와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-153">An SSL certificate must be associated with the ASE as the "default" SSL certificate that's used to establish SSL connections to apps.</span></span> <span data-ttu-id="14761-154">ASE의 기본 DNS 접미사가 *internal-contoso.com*인 경우 https://some-random-app.internal-contoso.com에 연결하려면 **.internal-contoso.com*에 유효한 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-154">If the ASE's default DNS suffix is *internal-contoso.com*, a connection to https://some-random-app.internal-contoso.com requires an SSL certificate that's valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="14761-155">내부 인증 기관을 사용하거나, 외부 발급자로부터 인증서를 구입하거나, 자체 서명된 인증서를 사용하는 등의 방법으로 유효한 SSL 인증서를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span></span> <span data-ttu-id="14761-156">SSL 인증서의 소스에 관계 없이 다음과 같은 인증서 특성을 올바르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-156">Regardless of the source of the SSL certificate, the following certificate attributes must be configured properly:</span></span>

* <span data-ttu-id="14761-157">**주체**: 이 특성은 **.your-root-domain-here.com*으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-157">**Subject**: This attribute must be set to **.your-root-domain-here.com*.</span></span>
* <span data-ttu-id="14761-158">**주체 대체 이름**: 이 특성에는 **.your-root-domain-here.com* 및 **.scm.your-root-domain-here.com*이 둘 다 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-158">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here.com* and **.scm.your-root-domain-here.com*.</span></span> <span data-ttu-id="14761-159">각 앱과 연결된 SCM/Kudu 사이트에 대한 SSL 연결은 *your-app-name.scm.your-root-domain-here.com* 형식의 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-159">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="14761-160">유효한 SSL 인증서가 있는 경우 두 가지 추가 준비 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-160">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span> <span data-ttu-id="14761-161">SSL 인증서를 .pfx 파일로 변환/저장합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-161">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="14761-162">.pfx 파일에는 모든 중간 인증서와 루트 인증서를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-162">Remember that the .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="14761-163">암호로 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-163">Secure it with a password.</span></span>

<span data-ttu-id="14761-164">SSL 인증서는 Azure Resource Manager 템플릿을 사용하여 업로드되므로 .pfx 파일을 Base64 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-164">The .pfx file needs to be converted into a base64 string because the SSL certificate is uploaded by using a Resource Manager template.</span></span> <span data-ttu-id="14761-165">Resource Manager 템플릿은 텍스트 파일이므로 .pfx 파일을 Base64 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-165">Because Resource Manager templates are text files, the .pfx file must be converted into a base64 string.</span></span> <span data-ttu-id="14761-166">이렇게 해당 파일을 템플릿의 매개 변수로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-166">This way it can be included as a parameter of the template.</span></span>

<span data-ttu-id="14761-167">아래 PowerShell 코드 조각을 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-167">Use the following PowerShell code snippet to:</span></span>

* <span data-ttu-id="14761-168">자체 서명된 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-168">Generate a self-signed certificate.</span></span>
* <span data-ttu-id="14761-169">인증서를 .pfx 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="14761-169">Export the certificate as a .pfx file.</span></span>
* <span data-ttu-id="14761-170">.pfx 파일을 Base64 인코딩 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-170">Convert the .pfx file into a base64-encoded string.</span></span>
* <span data-ttu-id="14761-171">Base64 인코딩 문자열을 별도의 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-171">Save the base64-encoded string to a separate file.</span></span> 

<span data-ttu-id="14761-172">이 Base64 인코딩용 PowerShell 코드는 [PowerShell 스크립트 블로그][examplebase64encoding]에서 가져와 수정한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-172">This PowerShell code for base64 encoding was adapted from the [PowerShell scripts blog][examplebase64encoding]:</span></span>

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="14761-173">SSL 인증서가 생성되고 Base64 인코딩 문자열로 변환되면 GitHub의 예제 Resource Manager 템플릿 [기본 SSL 인증서 구성][quickstartconfiguressl]을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="14761-173">After the SSL certificate is successfully generated and converted to a base64-encoded string, use the example Resource Manager template [Configure the default SSL certificate][quickstartconfiguressl] on GitHub.</span></span> 

<span data-ttu-id="14761-174">*azuredeploy.parameters.json* 파일의 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-174">The parameters in the *azuredeploy.parameters.json* file are listed here:</span></span>

* <span data-ttu-id="14761-175">*appServiceEnvironmentName*: 구성하는 ILB ASE의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-175">*appServiceEnvironmentName*: The name of the ILB ASE being configured.</span></span>
* <span data-ttu-id="14761-176">*existingAseLocation*: ILB ASE가 배포된 Azure 지역을 포함하는 텍스트 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-176">*existingAseLocation*: Text string containing the Azure region where the ILB ASE was deployed.</span></span>  <span data-ttu-id="14761-177">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-177">For example: "South Central US".</span></span>
* <span data-ttu-id="14761-178">*pfxBlobString*: .pfx 파일의 Base64 인코딩 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-178">*pfxBlobString*: The based64-encoded string representation of the .pfx file.</span></span> <span data-ttu-id="14761-179">위에 나와 있는 코드 조각을 사용하여 "exportedcert.pfx.b64"에 포함된 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-179">Use the code snippet shown earlier and copy the string contained in "exportedcert.pfx.b64".</span></span> <span data-ttu-id="14761-180">이 문자열을 *pfxBlobString* 특성의 값으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-180">Paste it in as the value of the *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="14761-181">*password*: .pfx 파일을 보호하는 데 사용되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-181">*password*: The password used to secure the .pfx file.</span></span>
* <span data-ttu-id="14761-182">*certificateThumbprint*: 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-182">*certificateThumbprint*: The certificate's thumbprint.</span></span> <span data-ttu-id="14761-183">PowerShell에서 이 값을 검색하는 경우(예: 이전 코드 조각의 *$certificate.Thumbprint*) 값을 있는 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-183">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from the earlier code snippet), you can use the value as is.</span></span> <span data-ttu-id="14761-184">Windows 인증서 대화 상자의 값을 복사하는 경우 불필요한 공백을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-184">If you copy the value from the Windows certificate dialog box, remember to strip out the extraneous spaces.</span></span> <span data-ttu-id="14761-185">*certificateThumbprint* 는 AF3143EB61D43F6727842115BB7F17BBCECAECAE와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="14761-185">The *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span></span>
* <span data-ttu-id="14761-186">*certificateName*: 인증서를 식별하는 데 사용되는 직접 선택한 친숙한 문자열 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-186">*certificateName*: A friendly string identifier of your own choosing used to identity the certificate.</span></span> <span data-ttu-id="14761-187">이 이름은 SSL 인증서를 나타내는 *Microsoft.Web/certificates* 엔터티에 대한 고유한 Resource Manager 식별자의 일부로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-187">The name is used as part of the unique Resource Manager identifier for the *Microsoft.Web/certificates* entity that represents the SSL certificate.</span></span> <span data-ttu-id="14761-188">이름은 *반드시* \_yourASENameHere_InternalLoadBalancingASE 접미사로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-188">The name *must* end with the following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span></span> <span data-ttu-id="14761-189">Azure Portal에서는 인증서가 ILB 지원 ASE를 보호하는 데 사용됨을 나타내는 표시기로 이 접미사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-189">The Azure portal uses this suffix as an indicator that the certificate is used to secure an ILB-enabled ASE.</span></span>

<span data-ttu-id="14761-190">*azuredeploy.parameters.json*을 축약한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-190">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span></span>

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

<span data-ttu-id="14761-191">*azuredeploy.parameters.json* 파일에 매개 변수를 입력한 후 PowerShell 코드 조각을 사용하여 기본 SSL 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-191">After the *azuredeploy.parameters.json* file is filled in, configure the default SSL certificate by using the PowerShell code snippet.</span></span> <span data-ttu-id="14761-192">컴퓨터에 Resource Manager 템플릿 파일이 있는 위치와 일치하도록 파일 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-192">Change the file paths to match where the Resource Manager template files are located on your machine.</span></span> <span data-ttu-id="14761-193">Resource Manager 배포 이름 및 리소스 그룹 이름에 대해 고유한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-193">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="14761-194">변경 내용이 적용되려면 ASE 프런트 엔드당 약 40분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="14761-194">It takes roughly 40 minutes per ASE front end to apply the change.</span></span> <span data-ttu-id="14761-195">예를 들어 두 개의 프런트 엔드를 사용하는 기본 크기 ASE의 경우 템플릿을 완료하는 데 약 1시간 20분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-195">For example, for a default-sized ASE that uses two front ends, the template takes around one hour and 20 minutes to complete.</span></span> <span data-ttu-id="14761-196">템플릿이 실행되는 동안에는 ASE 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-196">While the template is running, the ASE can't scale.</span></span>  

<span data-ttu-id="14761-197">템플릿이 완료되면 HTTPS를 통해 ILB ASE의 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-197">After the template finishes, apps on the ILB ASE can be accessed over HTTPS.</span></span> <span data-ttu-id="14761-198">연결은 기본 SSL 인증서를 통해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-198">The connections are secured by using the default SSL certificate.</span></span> <span data-ttu-id="14761-199">응용 프로그램 이름과 기본 호스트 이름의 조합을 사용하여 ILB ASE의 앱에 주소를 지정할 때 기본 SSL 인증서가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-199">The default SSL certificate is used when apps on the ILB ASE are addressed by using a combination of the application name plus the default host name.</span></span> <span data-ttu-id="14761-200">예를 들어 https://mycustomapp.internal-contoso.com은 **.internal-contoso.com*용 기본 SSL 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-200">For example, https://mycustomapp.internal-contoso.com uses the default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="14761-201">그러나 개발자는 공용 다중 테넌트 서비스에서 실행되는 앱과 마찬가지로 개별 앱에 대해 사용자 지정 호스트 이름을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-201">However, just like apps that run on the public multitenant service, developers can configure custom host names for individual apps.</span></span> <span data-ttu-id="14761-202">또한 개별 앱에 대해 고유한 SNI SSL 인증서 바인딩을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-202">They also can configure unique SNI SSL certificate bindings for individual apps.</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="14761-203">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="14761-203">App Service Environment v1</span></span> ##
<span data-ttu-id="14761-204">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14761-204">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="14761-205">위의 정보는 ASEv2를 기준으로 작성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-205">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="14761-206">이 섹션은 ASEv1과 ASEv2의 차이를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="14761-206">This section shows you the differences between ASEv1 and ASEv2.</span></span>

<span data-ttu-id="14761-207">ASEv1에서는 모든 리소스를 수동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-207">In ASEv1, you manage all of the resources manually.</span></span> <span data-ttu-id="14761-208">여기에는 IP 기반 SSL에 사용되는 프런트 엔드, 작업자 및 IP 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-208">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="14761-209">App Service 계획을 규모 확장하려면 먼저 해당 App Service를 호스트할 작업자 풀을 규모 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-209">Before you can scale out your App Service plan, you must scale out the worker pool that you want to host it.</span></span>

<span data-ttu-id="14761-210">ASEv1은 ASEv2와는 다른 가격 책정 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-210">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="14761-211">ASEv1에서는 할당된 각 코어에 대한 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="14761-211">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="14761-212">여기에는 작업을 호스트하지 않는 프런트 엔드 또는 작업자에 사용되는 코어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-212">That includes cores that are used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="14761-213">ASEv1에서 ASE의 기본 최대 규모 크기는 총 55개의 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-213">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="14761-214">여기에는 작업자 및 프런트 엔드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="14761-214">That includes workers and front ends.</span></span> <span data-ttu-id="14761-215">ASEv1의 한 가지 장점은 클래식 가상 네트워크 및 Resource Manager 가상 네트워크에 배포할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14761-215">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="14761-216">ASEv1에 대해 자세히 알아보려면 [App Service Environment v1 소개][ASEv1Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14761-216">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<span data-ttu-id="14761-217">Resource Manager 템플릿을 사용하여 ASEv1을 만들려는 경우 [Resource Manager 템플릿을 사용하여 ILB ASE v1 만들기][ILBASEv1Template]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14761-217">To create an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span></span>


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
