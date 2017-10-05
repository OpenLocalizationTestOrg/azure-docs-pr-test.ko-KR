---
title: "Azure Resource Manager 템플릿을 사용하여 ILB ASE를 만드는 방법 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 내부 부하 분산 장치 ASE를 만드는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 147ab76d38c8bbbf34d35ed6c2a194d97fe711ab
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-an-ilb-ase-using-azure-resource-manager-templates"></a><span data-ttu-id="1fec2-103">Azure Resource Manager 템플릿을 사용하여 ILB ASE를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1fec2-103">How To Create an ILB ASE Using Azure Resource Manager Templates</span></span>

> [!NOTE] 
> <span data-ttu-id="1fec2-104">이 문서는 ASE(App Service Environment) v1에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="1fec2-105">사용하기가 더 쉽고 더 강력한 인프라에서 실행되는 최신 버전의 App Service Environment가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="1fec2-106">새 버전에 대한 자세한 내용은 [App Service Environment 소개](../app-service/app-service-environment/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fec2-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

## <a name="overview"></a><span data-ttu-id="1fec2-107">개요</span><span class="sxs-lookup"><span data-stu-id="1fec2-107">Overview</span></span>
<span data-ttu-id="1fec2-108">앱 서비스 환경은 공용 VIP 대신 가상 네트워크 내부 주소를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-108">App Service Environments can be created with a virtual network internal address instead of a public VIP.</span></span>  <span data-ttu-id="1fec2-109">이 내부 주소는 ILB(내부 부하 분산 장치)라고 하는 Azure 구성 요소에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-109">This internal address is provided by an Azure component called the internal load balancer (ILB).</span></span>  <span data-ttu-id="1fec2-110">Azure 포털을 사용하여 ILB ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-110">An ILB ASE can be created using the Azure portal.</span></span>  <span data-ttu-id="1fec2-111">Azure Resource Manager 템플릿을 통해 자동화 방식으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-111">It can also be created using automation by way of Azure Resource Manager templates.</span></span>  <span data-ttu-id="1fec2-112">이 문서에서는 Azure Resource Manager 템플릿으로 ILB ASE를 만드는 데 필요한 단계와 구문을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-112">This article walks through the steps and syntax needed to create an ILB ASE with Azure Resource Manager templates.</span></span>

<span data-ttu-id="1fec2-113">ILB ASE 생성을 자동화하는 과정은 세 단계로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-113">There are three steps involved in automating creation of an ILB ASE:</span></span>

1. <span data-ttu-id="1fec2-114">먼저 공용 VIP 대신 내부 부하 분산 장치 주소를 사용하여 가상 네트워크에 기본 ASE가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-114">First the base ASE is created in a virtual network using an internal load balancer address instead of a public VIP.</span></span>  <span data-ttu-id="1fec2-115">이 단계의 일부로 루트 도메인 이름이 ILB ASE에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-115">As part of this step, a root domain name is assigned to the ILB ASE.</span></span>
2. <span data-ttu-id="1fec2-116">ILB ASE가 만들어지면 SSL 인증서가 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-116">Once the ILB ASE is created, an SSL certificate is uploaded.</span></span>  
3. <span data-ttu-id="1fec2-117">업로드된 SSL 인증서는 해당 "기본" SSL 인증서로 ILB ASE에 명시적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-117">The uploaded SSL certificate is explicitly assigned to the ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="1fec2-118">이 SSL 인증서는 ASE에 할당된 공용 루트 도메인을 사용하여 앱의 주소를 지정할 때 ILB ASE의 앱으로 이동되는 SSL 트래픽에 사용됩니다(예: https://someapp.mycustomrootcomain.com).</span><span class="sxs-lookup"><span data-stu-id="1fec2-118">This SSL certificate will be used for SSL traffic to apps on the ILB ASE when the apps are addressed using the common root domain assigned to the ASE (e.g. https://someapp.mycustomrootcomain.com)</span></span>

## <a name="creating-the-base-ilb-ase"></a><span data-ttu-id="1fec2-119">기본 ILB ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="1fec2-119">Creating the Base ILB ASE</span></span>
<span data-ttu-id="1fec2-120">Azure Resource Manager 템플릿 예제 및 관련 매개 변수 파일은 GitHub의 [여기][quickstartilbasecreate]에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-120">An example Azure Resource Manager template, and its associated parameters file, are available on GitHub [here][quickstartilbasecreate].</span></span>

<span data-ttu-id="1fec2-121">*azuredeploy.parameters.json* 파일에 있는 대부분의 매개 변수는 ILB ASE와 공용 VIP에 바인딩된 ASE 둘 다를 만들 때 공통적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-121">Most of the parameters in the *azuredeploy.parameters.json* file are common to creating both ILB ASEs, as well as ASEs bound to a public VIP.</span></span>  <span data-ttu-id="1fec2-122">아래 목록에서는 ILB ASE를 만들 때 특별한 고려 사항이 있거나 고유한 매개 변수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-122">The list below calls out parameters of special note, or that are unique, when creating an ILB ASE:</span></span>

* <span data-ttu-id="1fec2-123">*interalLoadBalancingMode*: 대부분의 경우 이 속성을 3으로 설정합니다. 이것은 포트 80/443의 HTTP/HTTPS 트래픽과 ASE의 FTP 서비스에서 수신하는 컨트롤/데이터 채널 포트가 ILB 할당 가상 네트워크 내부 주소에 바인딩될 것임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-123">*interalLoadBalancingMode*:  In most cases set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB allocated virtual network internal address.</span></span>  <span data-ttu-id="1fec2-124">대신, 이 속성을 2로 설정하면 FTP 서비스 관련 포트(컨트롤 및 데이터 채널)는 ILB 주소에 바인딩되지만, HTTP/HTTPS 트래픽은 공용 VIP에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-124">If this property is instead set to 2, then only the FTP service related ports (both control and data channels) will be bound to an ILB address, while the HTTP/HTTPS traffic will remain on the public VIP.</span></span>
* <span data-ttu-id="1fec2-125">*dnsSuffix*: 이 매개 변수는 ASE에 할당될 기본 루트 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-125">*dnsSuffix*:  This parameter defines the default root domain that will be assigned to the ASE.</span></span>  <span data-ttu-id="1fec2-126">Azure 앱 서비스의 공용 변형에서 모든 웹앱용 기본 루트 도메인은 *azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-126">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span></span>  <span data-ttu-id="1fec2-127">그러나 ILB ASE는 고객의 가상 네트워크 내부에 있으므로 공용 서비스의 기본 루트 도메인을 사용하는 것은 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-127">However since an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span></span>  <span data-ttu-id="1fec2-128">대신, ILB ASE에는 회사의 내부 가상 네트워크 내에서 사용하기 적합한 기본 루트 도메인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-128">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span>  <span data-ttu-id="1fec2-129">예를 들어 가상의 Contoso Corporation은 Contoso의 가상 네트워크 내에서만 확인 가능하고 액세스할 수 있는 앱에 기본 루트 도메인 *internal-contoso.com* 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-129">For example, a hypothetical Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to only be resolvable and accessible within Contoso's virtual network.</span></span> 
* <span data-ttu-id="1fec2-130">*ipSslAddressCount*: 이 매개 변수는 ILB ASE가 단일 ILB 주소만 가지므로 *azuredeploy.json* 파일에서 자동으로 기본값인 0을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-130">*ipSslAddressCount*:  This parameter is automatically defaulted to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span>  <span data-ttu-id="1fec2-131">ILB ASE에 대한 명시적 IP-SSL 주소는 없으므로 ILB ASE에 대한 IP-SSL 주소 풀을 0으로 설정해야 합니다. 그러지 않으면 프로비전 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-131">There are no explicit IP-SSL addresses for an ILB ASE, and hence the IP-SSL address pool for an ILB ASE must be set to zero, otherwise a provisioning error will occur.</span></span> 

<span data-ttu-id="1fec2-132">ILB ASE에 대해 *azuredeploy.parameters.json* 파일이 채워진 경우 다음과 같은 PowerShell 코드 조각을 사용하여 ILB ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-132">Once the *azuredeploy.parameters.json* file has been filled in for an ILB ASE, the ILB ASE can then be created using the following Powershell code snippet.</span></span>  <span data-ttu-id="1fec2-133">컴퓨터에는 Azure Resource Manager 템플릿 파일이 있는 위치와 일치하도록 파일 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-133">Change the file PATHs to match where the Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="1fec2-134">또한 Azure Resource Manager 배포 이름 및 리소스 그룹 이름에 대해 고유한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-134">Also remember to supply your own values for the Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="1fec2-135">Azure Resource Manager 템플릿이 제출되고 ILB ASE가 만들어지는 데 몇 시간 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-135">After the Azure Resource Manager template is submitted it will take a few hours for the ILB ASE to be created.</span></span>  <span data-ttu-id="1fec2-136">다 만들어지면 배포를 트리거한 구독에 대한 앱 서비스 환경 목록의 포털 UX에 ILB ASE가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-136">Once the creation completes, the ILB ASE will show up in the portal UX in the list of App Service Environments for the subscription that triggered the deployment.</span></span>

## <a name="uploading-and-configuring-the-default-ssl-certificate"></a><span data-ttu-id="1fec2-137">"기본" SSL 인증서 업로드 및 구성</span><span class="sxs-lookup"><span data-stu-id="1fec2-137">Uploading and Configuring the "Default" SSL Certificate</span></span>
<span data-ttu-id="1fec2-138">"기본" SSL 인증서가 앱에 대한 SSL 연결을 설정하는 데 사용하므로 ILB ASE를 만든 후에는 SSL 인증서를 ASE에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-138">Once the ILB ASE is created, an SSL certificate should be associated with the ASE as the "default" SSL certificate use for establishing SSL connections to apps.</span></span>  <span data-ttu-id="1fec2-139">가상의 Contoso Corporation 예제를 계속 살펴보면, ASE의 기본 DNS 접미사가 *internal-contoso.com*인 경우 *https://some-random-app.internal-contoso.com*에 연결하기 위해 **.internal-contoso.com*에 유효한 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-139">Continuing with the hypothetical Contoso Corporation example, if the ASE's default DNS suffix is *internal-contoso.com*, then a connection to *https://some-random-app.internal-contoso.com* requires an SSL certificate that is valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="1fec2-140">유효한 SSL 인증서를 구하는 방법에는 터미널 CA를 사용하거나, 외부 발급자로부터 인증서를 구입하거나, 자체 서명된 인증서를 사용하는 등 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-140">There are a variety of ways to obtain a valid SSL certificate including internal CAs, purchasing a certificate from an external issuer, and using a self-signed certificate.</span></span>  <span data-ttu-id="1fec2-141">SSL 인증서의 소스에 관계 없이 다음과 같은 인증서 특성을 올바르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-141">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="1fec2-142">*Subject*: 이 특성은 **.your-root-domain-here.com*으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-142">*Subject*:  This attribute must be set to **.your-root-domain-here.com*</span></span>
* <span data-ttu-id="1fec2-143">*주체 대체 이름*: 이 특성에는 **.your-root-domain-here.com* 및 **.scm.your-root-domain-here.com* 둘 다 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-143">*Subject Alternative Name*:  This attribute must include both **.your-root-domain-here.com*, and **.scm.your-root-domain-here.com*.</span></span>  <span data-ttu-id="1fec2-144">두 번째 항목을 포함해야 하는 이유는 각 앱과 연결된 SCM/Kudu 사이트에 대한 SSL 연결이 *your-app-name.scm.your-root-domain-here.com*형식의 주소를 사용하여 만들어지기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-144">The reason for the second entry is that SSL connections to the SCM/Kudu site associated with each app will be made using an address of the form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="1fec2-145">유효한 SSL 인증서가 있는 경우 두 가지 추가 준비 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-145">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span>  <span data-ttu-id="1fec2-146">SSL 인증서를 .pfx 파일로 변환/저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-146">The SSL certificate needs to be converted/saved as a .pfx file.</span></span>  <span data-ttu-id="1fec2-147">.pfx 파일에는 모든 중간 인증서 및 루트 인증서가 포함되어야 하며 암호로 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-147">Remember that the .pfx file needs to include all intermediate and root certificates, and also needs to be secured with a password.</span></span>

<span data-ttu-id="1fec2-148">SSL 인증서는 Azure Resource Manager 템플릿을 사용하여 업로드되므로 결과 .pfx 파일을 Base64 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-148">Then the resultant .pfx file needs to be converted into a base64 string because the SSL certificate will be uploaded using an Azure Resource Manager template.</span></span>  <span data-ttu-id="1fec2-149">Azure Resource Manager 템플릿은 텍스트 파일이므로 .pfx 파일은 템플릿의 매개 변수로 포함될 수 있게 Base64 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-149">Since Azure Resource Manager templates are text files, the .pfx file needs to be converted into a base64 string so it can be included as a parameter of the template.</span></span>

<span data-ttu-id="1fec2-150">아래의 PowerShell 코드 조각은 자체 서명된 인증서를 생성하고, 인증서를 .pfx 파일로 내보내고, .pfx 파일을 Base64 인코딩 문자열로 변환한 다음 Base64 인코딩 문자열을 개별 파일로 저장하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-150">The Powershell code snippet below shows an example of generating a self-signed certificate, exporting the certificate as a .pfx file, converting the .pfx file into a base64 encoded string, and then saving the base64 encoded string to a separate file.</span></span>  <span data-ttu-id="1fec2-151">Base64 인코딩을 위한 PowerShell 코드는 [PowerShell 스크립트 블로그][examplebase64encoding]에서 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-151">The Powershell code for base64 encoding was adapted from the [Powershell Scripts Blog][examplebase64encoding].</span></span>

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="1fec2-152">SSL 인증서가 생성되고 Base64 인코딩 문자열로 변환되면 [기본 SSL 인증서 구성][configuringDefaultSSLCertificate]에 대한 GitHub의 Azure Resource Manager 템플릿 예제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-152">Once the SSL certificate has been successfully generated and converted to a base64 encoded string, the example Azure Resource Manager template on GitHub for [configuring the default SSL certificate][configuringDefaultSSLCertificate] can be used.</span></span>

<span data-ttu-id="1fec2-153">*azuredeploy.parameters.json* 파일의 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-153">The parameters in the *azuredeploy.parameters.json* file are listed below:</span></span>

* <span data-ttu-id="1fec2-154">*appServiceEnvironmentName*: 구성하는 ILB ASE의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-154">*appServiceEnvironmentName*:  The name of the ILB ASE being configured.</span></span>
* <span data-ttu-id="1fec2-155">*existingAseLocation*: ILB ASE가 배포된 Azure 지역을 포함하는 텍스트 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-155">*existingAseLocation*:  Text string containing the Azure region where the ILB ASE was deployed.</span></span>  <span data-ttu-id="1fec2-156">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-156">For example:  "South Central US".</span></span>
* <span data-ttu-id="1fec2-157">*pfxBlobString*: .pfx 파일의 Base64 인코딩 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-157">*pfxBlobString*:  The based64 encoded string representation of the .pfx file.</span></span>  <span data-ttu-id="1fec2-158">앞서 표시된 코드 조각을 사용하여 "exportedcert.pfx.b64"에 포함된 문자열을 복사한 후 *pfxBlobString* 특성의 값으로 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-158">Using the code snippet shown earlier, you would copy the string contained in "exportedcert.pfx.b64" and paste it in as the value of the *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="1fec2-159">*password*: .pfx 파일을 보호하는 데 사용되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-159">*password*:  The password used to secure the .pfx file.</span></span>
* <span data-ttu-id="1fec2-160">*certificateThumbprint*: 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-160">*certificateThumbprint*:  The certificate's thumbprint.</span></span>  <span data-ttu-id="1fec2-161">PowerShell에서 이 값을 검색하는 경우(예: 이전 코드 조각의 *$certificate.Thumbprint* ) 값을 있는 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-161">If you retrieve this value from Powershell (e.g. *$certificate.Thumbprint* from the earlier code snippet), you can use the value as-is.</span></span>  <span data-ttu-id="1fec2-162">그러나 Windows 인증서 대화 상자의 값을 복사하는 경우 불필요한 공백을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-162">However if you copy the value from the Windows certificate dialog, remember to strip out the extraneous spaces.</span></span>  <span data-ttu-id="1fec2-163">*certificateThumbprint* 는 AF3143EB61D43F6727842115BB7F17BBCECAECAE와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-163">The *certificateThumbprint* should look something like:  AF3143EB61D43F6727842115BB7F17BBCECAECAE</span></span>
* <span data-ttu-id="1fec2-164">*certificateName*: 인증서를 식별하는 데 사용되는 직접 선택한 친숙한 문자열 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-164">*certificateName*:  A friendly string identifier of your own choosing used to identity the certificate.</span></span>  <span data-ttu-id="1fec2-165">이 이름은 SSL 인증서를 나타내는 *Microsoft.Web/certificates* 엔터티에 대한 고유한 Azure Resource Manager 식별자의 일부로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-165">The name is used as part of the unique Azure Resource Manager identifier for the *Microsoft.Web/certificates* entity representing the SSL certificate.</span></span>  <span data-ttu-id="1fec2-166">이름은 다음 접미사 \_yourASENameHere_InternalLoadBalancingASE와 함께 종료**해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-166">The name **must** end with the following suffix:  \_yourASENameHere_InternalLoadBalancingASE.</span></span>  <span data-ttu-id="1fec2-167">이 접미사는 포털에서 인증서가 ILB 지원 ASE 보안에 사용되는 표시기로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-167">This suffix is used by the portal as an indicator that the certificate is used for securing an ILB-enabled ASE.</span></span>

<span data-ttu-id="1fec2-168">*azuredeploy.parameters.json* 을 축약한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-168">An abbreviated example of *azuredeploy.parameters.json* is shown below:</span></span>

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

<span data-ttu-id="1fec2-169">*azuredeploy.parameters.json* 파일이 채워진 경우 다음과 같은 PowerShell 코드 조각을 사용하여 기본 SSL 인증서를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-169">Once the *azuredeploy.parameters.json* file has been filled in, the default SSL certificate can be configured using the following Powershell code snippet.</span></span>  <span data-ttu-id="1fec2-170">컴퓨터에는 Azure Resource Manager 템플릿 파일이 있는 위치와 일치하도록 파일 경로를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-170">Change the file PATHs to match where the Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="1fec2-171">또한 Azure Resource Manager 배포 이름 및 리소스 그룹 이름에 대해 고유한 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-171">Also remember to supply your own values for the Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="1fec2-172">Azure Resource Manager 템플릿이 제출된 후에 변경 내용을 적용하는 데 ASE 프런트 엔드당 대략 40분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-172">After the Azure Resource Manager template is submitted it will take roughly forty minutes minutes per ASE front-end to apply the change.</span></span>  <span data-ttu-id="1fec2-173">예를 들어 두 개의 프런트 엔드를 사용하는 기본 크기의 ASE가 있는 경우 템플릿을 완료하는 데 약 1시간 20분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-173">For example, with a default sized ASE using two front-ends, the template will take around one hour and twenty minutes to complete.</span></span>  <span data-ttu-id="1fec2-174">템플릿이 실행되는 동안에는 ASE 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-174">While the template is running the ASE will not be able to scaled.</span></span>  

<span data-ttu-id="1fec2-175">템플릿이 완료되면 ILB ASE의 앱에 HTTPS를 통해 액세스할 수 있으며 기본 SSL 인증서를 사용하여 연결이 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-175">Once the template completes, apps on the ILB ASE can be accessed over HTTPS and the connections will be secured using the default SSL certificate.</span></span>  <span data-ttu-id="1fec2-176">기본 SSL 인증서는 ILB ASE의 앱 주소는 응용 프로그램 이름과 기본 호스트 이름 조합을 사용하여 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-176">The default SSL certificate will be used when apps on the ILB ASE are addressed using a combination of the application name plus the default hostname.</span></span>  <span data-ttu-id="1fec2-177">예를 들어 *https://mycustomapp.internal-contoso.com*은 **.internal-contoso.com*에 대한 기본 SSL 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-177">For example *https://mycustomapp.internal-contoso.com* would use the default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="1fec2-178">그러나 공용 다중 테넌트 서비스에서 실행 중인 앱의 경우와 마찬가지로, 개발자는 개별 앱에 대한 사용자 지정 호스트 이름을 구성한 다음 개별 앱에 대해 고유한 SNI SSL 인증서 바인딩을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-178">However, just like apps running on the public multi-tenant service, developers can also configure custom host names for individual apps, and then configure unique SNI SSL certificate bindings for individual apps.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="1fec2-179">시작</span><span class="sxs-lookup"><span data-stu-id="1fec2-179">Getting started</span></span>
<span data-ttu-id="1fec2-180">앱 서비스 환경을 시작하려면 [앱 서비스 환경 소개](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1fec2-180">To get started with App Service Environments, see [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

<span data-ttu-id="1fec2-181">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fec2-181">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

