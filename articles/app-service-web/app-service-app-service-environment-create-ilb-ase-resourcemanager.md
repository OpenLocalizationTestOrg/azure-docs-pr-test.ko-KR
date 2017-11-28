---
title: "aaaHow tooCreate는 ILB ASE를 사용 하 여 Azure 리소스 관리자 템플릿을 | Microsoft Docs"
description: "내부 프로그램 toocreate Azure 리소스 관리자 템플릿을 사용 하 여 분산 ASE를 로드 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a><span data-ttu-id="cc83d-103">어떻게 tooCreate는 ILB ASE를 사용 하 여 Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="cc83d-103">How tooCreate an ILB ASE Using Azure Resource Manager Templates</span></span>

> [!NOTE] 
> <span data-ttu-id="cc83d-104">앱 서비스 환경 v1 hello에 대 한이 문서는입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-104">This article is about hello App Service Environment v1.</span></span> <span data-ttu-id="cc83d-105">최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-105">There is a newer version of hello App Service Environment that is easier toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="cc83d-106">hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

## <a name="overview"></a><span data-ttu-id="cc83d-107">개요</span><span class="sxs-lookup"><span data-stu-id="cc83d-107">Overview</span></span>
<span data-ttu-id="cc83d-108">앱 서비스 환경은 공용 VIP 대신 가상 네트워크 내부 주소를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-108">App Service Environments can be created with a virtual network internal address instead of a public VIP.</span></span>  <span data-ttu-id="cc83d-109">이러한 내부 주소는 hello 내부 부하 분산 장치 (ILB) 호출 하는 Azure 구성 요소에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-109">This internal address is provided by an Azure component called hello internal load balancer (ILB).</span></span>  <span data-ttu-id="cc83d-110">ILB ASE hello Azure 포털을 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-110">An ILB ASE can be created using hello Azure portal.</span></span>  <span data-ttu-id="cc83d-111">Azure Resource Manager 템플릿을 통해 자동화 방식으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-111">It can also be created using automation by way of Azure Resource Manager templates.</span></span>  <span data-ttu-id="cc83d-112">이 문서에서는 hello 단계를 안내 하 고 구문 toocreate Azure 리소스 관리자 템플릿으로 ILB ASE를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-112">This article walks through hello steps and syntax needed toocreate an ILB ASE with Azure Resource Manager templates.</span></span>

<span data-ttu-id="cc83d-113">ILB ASE 생성을 자동화하는 과정은 세 단계로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-113">There are three steps involved in automating creation of an ILB ASE:</span></span>

1. <span data-ttu-id="cc83d-114">첫 번째 hello 기본 ASE 공용 VIP 대신 내부 부하 분산 장치 주소를 사용 하 여 가상 네트워크에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-114">First hello base ASE is created in a virtual network using an internal load balancer address instead of a public VIP.</span></span>  <span data-ttu-id="cc83d-115">이 단계의 일부로 루트 도메인 이름은 toohello ILB ASE 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-115">As part of this step, a root domain name is assigned toohello ILB ASE.</span></span>
2. <span data-ttu-id="cc83d-116">Hello ILB ASE를 만든 SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-116">Once hello ILB ASE is created, an SSL certificate is uploaded.</span></span>  
3. <span data-ttu-id="cc83d-117">hello 업로드 된 SSL 인증서가 명시적으로 할당 toohello ILB ASE "default" SSL 인증서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-117">hello uploaded SSL certificate is explicitly assigned toohello ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="cc83d-118">이 SSL 인증서에 사용할 SSL 트래픽 tooapps hello ILB ASE에 hello 공통 루트 할당 도메인 toohello (예: https://someapp.mycustomrootcomain.com) ASE를 사용 하 여 hello 응용 프로그램은 해결 되 면</span><span class="sxs-lookup"><span data-stu-id="cc83d-118">This SSL certificate will be used for SSL traffic tooapps on hello ILB ASE when hello apps are addressed using hello common root domain assigned toohello ASE (e.g. https://someapp.mycustomrootcomain.com)</span></span>

## <a name="creating-hello-base-ilb-ase"></a><span data-ttu-id="cc83d-119">Hello 자료 ILB ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="cc83d-119">Creating hello Base ILB ASE</span></span>
<span data-ttu-id="cc83d-120">Azure Resource Manager 템플릿 예제 및 관련 매개 변수 파일은 GitHub의 [여기][quickstartilbasecreate]에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-120">An example Azure Resource Manager template, and its associated parameters file, are available on GitHub [here][quickstartilbasecreate].</span></span>

<span data-ttu-id="cc83d-121">Hello의 hello 매개 변수 대부분 *azuredeploy.parameters.json* 파일 일반적인 toocreating 두 ILB ASEs 뿐만 아니라 ASEs 바인딩된 tooa 공용 VIP 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-121">Most of hello parameters in hello *azuredeploy.parameters.json* file are common toocreating both ILB ASEs, as well as ASEs bound tooa public VIP.</span></span>  <span data-ttu-id="cc83d-122">out 매개 변수 관련 참고의 호출 아래 hello 목록 또는 하는 고유한 ILB ASE를 만들 때:</span><span class="sxs-lookup"><span data-stu-id="cc83d-122">hello list below calls out parameters of special note, or that are unique, when creating an ILB ASE:</span></span>

* <span data-ttu-id="cc83d-123">*interalLoadBalancingMode*: 대부분의 경우에서 포트 80/443에서 두 HTTP/HTTPS 트래픽을 즉이 too3 설정 및 hello 컨트롤/데이터 채널 포트 수신에 hello ASE tooby hello FTP 서비스, 바인딩된 tooan ILB 할당 될 가상 네트워크 내부 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-123">*interalLoadBalancingMode*:  In most cases set this too3, which means both HTTP/HTTPS traffic on ports 80/443, and hello control/data channel ports listened tooby hello FTP service on hello ASE, will be bound tooan ILB allocated virtual network internal address.</span></span>  <span data-ttu-id="cc83d-124">이 속성은 유일한 hello FTP 서비스를 관련 된 포트 (둘 다 제어 및 데이터 채널)이 바인딩될 too2, 설정 대신 tooan ILB 주소, 동안 hello HTTP/HTTPS 트래픽을 hello 공용 VIP에 그대로 남아 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-124">If this property is instead set too2, then only hello FTP service related ports (both control and data channels) will be bound tooan ILB address, while hello HTTP/HTTPS traffic will remain on hello public VIP.</span></span>
* <span data-ttu-id="cc83d-125">*dnsSuffix*:이 매개 변수 hello toohello ASE 할당할 수 있는 기본 루트 도메인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-125">*dnsSuffix*:  This parameter defines hello default root domain that will be assigned toohello ASE.</span></span>  <span data-ttu-id="cc83d-126">Azure 앱 서비스의 공용 변형을 hello hello 기본 루트 도메인 모든 웹 앱에 대 한는 *azurewebsites.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-126">In hello public variation of Azure App Service, hello default root domain for all web apps is *azurewebsites.net*.</span></span>  <span data-ttu-id="cc83d-127">그러나 ILB ASE 내부 tooa 고객의 가상 네트워크 이므로, 것 의미 toouse hello 공용 서비스 기본 루트 도메인으로 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-127">However since an ILB ASE is internal tooa customer's virtual network, it doesn't make sense toouse hello public service's default root domain.</span></span>  <span data-ttu-id="cc83d-128">대신, ILB ASE에는 회사의 내부 가상 네트워크 내에서 사용하기 적합한 기본 루트 도메인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-128">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span>  <span data-ttu-id="cc83d-129">가상 Contoso Corporation의 기본 루트 도메인을 사용할 수는 예를 들어 *내부 contoso.com* tooonly 의도 하는 응용 프로그램을 통해 확인 및 Contoso 가상 네트워크 내에서 액세스할 수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-129">For example, a hypothetical Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended tooonly be resolvable and accessible within Contoso's virtual network.</span></span> 
* <span data-ttu-id="cc83d-130">*ipSslAddressCount*:이 매개 변수는 자동으로 tooa hello에 0 값을 기본값으로 설정 *azuredeploy.json* ILB ASEs 단일 ILB 주소 하나만 있으므로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-130">*ipSslAddressCount*:  This parameter is automatically defaulted tooa value of 0 in hello *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span>  <span data-ttu-id="cc83d-131">ILB ASE에 대 한 명시적 IP SSL 주소가 없습니다. 있으며 따라서 hello ILB ASE에 대 한 IP SSL 주소 풀을 설정 해야 toozero, 그렇지 않으면 프로 비전 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-131">There are no explicit IP-SSL addresses for an ILB ASE, and hence hello IP-SSL address pool for an ILB ASE must be set toozero, otherwise a provisioning error will occur.</span></span> 

<span data-ttu-id="cc83d-132">한 번 hello *azuredeploy.parameters.json* 파일 채워진에 대 한 ILB ASE hello hello 다음 Powershell 코드 조각을 사용 하 여 ILB ASE을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-132">Once hello *azuredeploy.parameters.json* file has been filled in for an ILB ASE, hello ILB ASE can then be created using hello following Powershell code snippet.</span></span>  <span data-ttu-id="cc83d-133">Hello 파일 경로 toomatch hello Azure 리소스 관리자 템플릿 파일이 컴퓨터에 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-133">Change hello file PATHs toomatch where hello Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="cc83d-134">또한 toosupply hello Azure 리소스 관리자 배포 이름 및 리소스 그룹 이름에 대 한 고유한 값을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-134">Also remember toosupply your own values for hello Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="cc83d-135">Hello Azure 리소스 관리자 후 서식 파일 전송 되는 hello ILB ASE toobe 생성에 대 한 몇 시간이 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-135">After hello Azure Resource Manager template is submitted it will take a few hours for hello ILB ASE toobe created.</span></span>  <span data-ttu-id="cc83d-136">Hello 생성 되 면 hello ILB ASE hello 포털 UX hello hello 배포를 트리거한 hello 구독에 대 한 앱 서비스 환경 목록에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-136">Once hello creation completes, hello ILB ASE will show up in hello portal UX in hello list of App Service Environments for hello subscription that triggered hello deployment.</span></span>

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a><span data-ttu-id="cc83d-137">업로드 하 고 hello "기본" SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="cc83d-137">Uploading and Configuring hello "Default" SSL Certificate</span></span>
<span data-ttu-id="cc83d-138">한 번 만든 ILB ASE hello, SSL 인증서를 연결 해야 할지 hello ASE SSL 연결 tooapps 설정 하기 위한 기본"hello" SSL 인증서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-138">Once hello ILB ASE is created, an SSL certificate should be associated with hello ASE as hello "default" SSL certificate use for establishing SSL connections tooapps.</span></span>  <span data-ttu-id="cc83d-139">접미사는 hello ASE의 기본 DNS 경우 hello 가상 Contoso Corporation 예제를 계속 *내부 contoso.com*, 연결 후 너무*https://some-random-app.internal-contoso.com*에 유효한 SSL 인증서가 필요 **.internal contoso.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-139">Continuing with hello hypothetical Contoso Corporation example, if hello ASE's default DNS suffix is *internal-contoso.com*, then a connection too*https://some-random-app.internal-contoso.com* requires an SSL certificate that is valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="cc83d-140">내부 Ca를 포함 하는 외부 발급자 로부터 인증서를 구매 하 고 자체 서명 된 인증서를 사용 하 여 유효한 SSL 인증서는 다양 한 방법으로 tooobtain 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-140">There are a variety of ways tooobtain a valid SSL certificate including internal CAs, purchasing a certificate from an external issuer, and using a self-signed certificate.</span></span>  <span data-ttu-id="cc83d-141">Hello SSL 인증서의 hello 소스에 관계 없이 hello 다음 인증서 특성 필요 toobe 올바르게 구성.</span><span class="sxs-lookup"><span data-stu-id="cc83d-141">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="cc83d-142">*제목*:이 속성을 너무 설정 되어야 합니다. **루트 도메인 here.com.your*</span><span class="sxs-lookup"><span data-stu-id="cc83d-142">*Subject*:  This attribute must be set too**.your-root-domain-here.com*</span></span>
* <span data-ttu-id="cc83d-143">*주체 대체 이름*:이 특성이 모두 포함 해야 합니다 **루트 도메인 here.com.your*, 및 **.scm.your-루트-도메인-here.com*합니다.  hello hello 두 번째 항목에 대 한 이유는 각 앱과 연결 된 SCM/Kudu 사이트 걸 수 hello 폼의 주소를 사용 하는 SSL 연결 toohello *your-app-name.scm.your-root-domain-here.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-143">*Subject Alternative Name*:  This attribute must include both **.your-root-domain-here.com*, and **.scm.your-root-domain-here.com*.  hello reason for hello second entry is that SSL connections toohello SCM/Kudu site associated with each app will be made using an address of hello form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="cc83d-144">유효한 SSL 인증서가 있는 경우 두 가지 추가 준비 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-144">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span>  <span data-ttu-id="cc83d-145">hello SSL 인증서를.pfx 파일로 변환/저장 toobe가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-145">hello SSL certificate needs toobe converted/saved as a .pfx file.</span></span>  <span data-ttu-id="cc83d-146">반드시 해당 hello.pfx 파일 tooinclude 모든 중간 및 루트 인증서가 필요 하 고는 암호로 보호 toobe에도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-146">Remember that hello .pfx file needs tooinclude all intermediate and root certificates, and also needs toobe secured with a password.</span></span>

<span data-ttu-id="cc83d-147">그런 다음 hello 결과.pfx 파일 toobe Azure 리소스 관리자 템플릿을 사용 하 여 hello SSL 인증서를 업로드할 수는 때문에 base64 문자열로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-147">Then hello resultant .pfx file needs toobe converted into a base64 string because hello SSL certificate will be uploaded using an Azure Resource Manager template.</span></span>  <span data-ttu-id="cc83d-148">Azure 리소스 관리자 템플릿을 텍스트 파일, toobe hello 서식 파일의 매개 변수로 포함 될 수 있도록 base64 문자열로 변환 hello.pfx 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-148">Since Azure Resource Manager templates are text files, hello .pfx file needs toobe converted into a base64 string so it can be included as a parameter of hello template.</span></span>

<span data-ttu-id="cc83d-149">아래 hello Powershell 코드 조각 자체 서명 된 인증서를 생성 하는 모양의 예제가 나와 hello 인증서 내보내기.pfx 파일로 hello.pfx 파일로 변환 하는 base64 인코딩 문자열입니다로 인코딩된 문자열 tooa 별도 파일을 다음 hello base64를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-149">hello Powershell code snippet below shows an example of generating a self-signed certificate, exporting hello certificate as a .pfx file, converting hello .pfx file into a base64 encoded string, and then saving hello base64 encoded string tooa separate file.</span></span>  <span data-ttu-id="cc83d-150">hello에서 변형 되었습니다 base64 인코딩을 대 한 Powershell 코드를 hello [Powershell 스크립트 블로그][examplebase64encoding]합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-150">hello Powershell code for base64 encoding was adapted from hello [Powershell Scripts Blog][examplebase64encoding].</span></span>

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="cc83d-151">Hello SSL 인증서가 성공적으로 생성 하 고 변환 된 tooa base64 인코딩된 문자열을 hello에 대 한 GitHub의 예제에서는 Azure Resource Manager 템플릿 [hello 기본 SSL 인증서 구성] [ configuringDefaultSSLCertificate] 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-151">Once hello SSL certificate has been successfully generated and converted tooa base64 encoded string, hello example Azure Resource Manager template on GitHub for [configuring hello default SSL certificate][configuringDefaultSSLCertificate] can be used.</span></span>

<span data-ttu-id="cc83d-152">hello에 대 한 매개 변수를 hello *azuredeploy.parameters.json* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-152">hello parameters in hello *azuredeploy.parameters.json* file are listed below:</span></span>

* <span data-ttu-id="cc83d-153">*appServiceEnvironmentName*: hello 구성 되 고 ILB ASE의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-153">*appServiceEnvironmentName*:  hello name of hello ILB ASE being configured.</span></span>
* <span data-ttu-id="cc83d-154">*existingAseLocation*: hello ILB ASE를 배포할 Azure 지역 hello 포함 된 텍스트 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-154">*existingAseLocation*:  Text string containing hello Azure region where hello ILB ASE was deployed.</span></span>  <span data-ttu-id="cc83d-155">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-155">For example:  "South Central US".</span></span>
* <span data-ttu-id="cc83d-156">*pfxBlobString*: hello based64 인코딩된 hello.pfx 파일의 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-156">*pfxBlobString*:  hello based64 encoded string representation of hello .pfx file.</span></span>  <span data-ttu-id="cc83d-157">앞에서 살펴본 hello 코드 조각을 사용 하 여, "exportedcert.pfx.b64"에 포함 된 hello 문자열을 복사 하는 hello의 hello 값으로 붙여 *pfxBlobString* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-157">Using hello code snippet shown earlier, you would copy hello string contained in "exportedcert.pfx.b64" and paste it in as hello value of hello *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="cc83d-158">*암호*: hello 사용 되는 암호 toosecure hello.pfx 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-158">*password*:  hello password used toosecure hello .pfx file.</span></span>
* <span data-ttu-id="cc83d-159">*certificateThumbprint*: hello 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-159">*certificateThumbprint*:  hello certificate's thumbprint.</span></span>  <span data-ttu-id="cc83d-160">Powershell에서이 값을 검색 하는 경우 (예: *$certificate 합니다. 지문* hello에서 이전 코드 조각의), hello 값으로 사용할 수 있습니다-됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-160">If you retrieve this value from Powershell (e.g. *$certificate.Thumbprint* from hello earlier code snippet), you can use hello value as-is.</span></span>  <span data-ttu-id="cc83d-161">그러나 hello Windows 인증서 대화 상자에서 hello 값을 복사 하는 경우 불필요 한 공백 hello 아웃 toostrip을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-161">However if you copy hello value from hello Windows certificate dialog, remember toostrip out hello extraneous spaces.</span></span>  <span data-ttu-id="cc83d-162">hello *certificateThumbprint* 다음과 같아야 합니다: AF3143EB61D43F6727842115BB7F17BBCECAECAE</span><span class="sxs-lookup"><span data-stu-id="cc83d-162">hello *certificateThumbprint* should look something like:  AF3143EB61D43F6727842115BB7F17BBCECAECAE</span></span>
* <span data-ttu-id="cc83d-163">*certificateName*: tooidentity hello 인증서를 사용 하는 사용자가 선택한의 문자열 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-163">*certificateName*:  A friendly string identifier of your own choosing used tooidentity hello certificate.</span></span>  <span data-ttu-id="cc83d-164">hello 이름이 hello에 대 한 hello 고유 Azure 리소스 관리자 식별자의 일부로 사용 됩니다 *Microsoft.Web/certificates* hello SSL 인증서를 나타내는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-164">hello name is used as part of hello unique Azure Resource Manager identifier for hello *Microsoft.Web/certificates* entity representing hello SSL certificate.</span></span>  <span data-ttu-id="cc83d-165">hello 이름 **해야** hello 접미사를 다음으로 끝나는: \_yourASENameHere_InternalLoadBalancingASE 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-165">hello name **must** end with hello following suffix:  \_yourASENameHere_InternalLoadBalancingASE.</span></span>  <span data-ttu-id="cc83d-166">이 접미사는 hello 포털에서 사용 표시기 hello 인증서를 ILB 사용이 가능한 ASE를 보안에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-166">This suffix is used by hello portal as an indicator that hello certificate is used for securing an ILB-enabled ASE.</span></span>

<span data-ttu-id="cc83d-167">*azuredeploy.parameters.json* 을 축약한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-167">An abbreviated example of *azuredeploy.parameters.json* is shown below:</span></span>

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

<span data-ttu-id="cc83d-168">한 번 hello *azuredeploy.parameters.json* 파일 채워진, 다음 Powershell 코드 조각을 hello를 사용 하 여 hello 기본 SSL 인증서를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-168">Once hello *azuredeploy.parameters.json* file has been filled in, hello default SSL certificate can be configured using hello following Powershell code snippet.</span></span>  <span data-ttu-id="cc83d-169">Hello 파일 경로 toomatch hello Azure 리소스 관리자 템플릿 파일이 컴퓨터에 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-169">Change hello file PATHs toomatch where hello Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="cc83d-170">또한 toosupply hello Azure 리소스 관리자 배포 이름 및 리소스 그룹 이름에 대 한 고유한 값을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-170">Also remember toosupply your own values for hello Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="cc83d-171">후 hello Azure 리소스 관리자 템플릿은 분이 걸립니다 대략 40 분 ASE 프런트 엔드 tooapply hello 변경 당 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-171">After hello Azure Resource Manager template is submitted it will take roughly forty minutes minutes per ASE front-end tooapply hello change.</span></span>  <span data-ttu-id="cc83d-172">예를 들어 기본값 두 프런트 엔드가 사용 하 여 크기의 ASE hello 템플릿을 걸립니다 1 시간 및 20 분 toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cc83d-172">For example, with a default sized ASE using two front-ends, hello template will take around one hour and twenty minutes toocomplete.</span></span>  <span data-ttu-id="cc83d-173">Hello 템플릿 실행 되는 동안 hello ASE 수 tooscaled 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-173">While hello template is running hello ASE will not be able tooscaled.</span></span>  

<span data-ttu-id="cc83d-174">Hello 템플릿 완료 되 면 앱 ILB ASE hello에 HTTPS를 통해 액세스할 수 있으며 hello 기본 SSL 인증서를 사용 하 여 hello 연결이 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-174">Once hello template completes, apps on hello ILB ASE can be accessed over HTTPS and hello connections will be secured using hello default SSL certificate.</span></span>  <span data-ttu-id="cc83d-175">hello 응용 프로그램 이름과 hello 기본 호스트 이름 조합을 사용 하 여 hello ILB ASE에 응용 프로그램은 해결 되 면 hello 기본 SSL 인증서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-175">hello default SSL certificate will be used when apps on hello ILB ASE are addressed using a combination of hello application name plus hello default hostname.</span></span>  <span data-ttu-id="cc83d-176">예를 들어 *https://mycustomapp.internal-contoso.com* hello 기본 SSL 인증서에 대 한 사용 **.internal contoso.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-176">For example *https://mycustomapp.internal-contoso.com* would use hello default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="cc83d-177">그러나 hello 공개 하는 다중 테 넌 트 서비스에서 실행 중인 앱에서와 마찬가지로 개발자 개별 앱에 대 한 사용자 지정 호스트 이름을 구성할 수도 구성 하는 다음 개별 앱에 대 한 SNI SSL 인증서 바인딩을 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-177">However, just like apps running on hello public multi-tenant service, developers can also configure custom host names for individual apps, and then configure unique SNI SSL certificate bindings for individual apps.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="cc83d-178">시작</span><span class="sxs-lookup"><span data-stu-id="cc83d-178">Getting started</span></span>
<span data-ttu-id="cc83d-179">앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="cc83d-179">tooget started with App Service Environments, see [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

<span data-ttu-id="cc83d-180">모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc83d-180">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

