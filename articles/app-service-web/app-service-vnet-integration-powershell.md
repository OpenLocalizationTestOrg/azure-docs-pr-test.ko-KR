---
title: "aaaConnect PowerShell을 사용 하 여 응용 프로그램 tooyour 가상 네트워크"
description: "PowerShell을 사용 하 여 tooconnect tooand 가상 네트워크와 작동 하는 방법에 대 한 지침"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="91cfc-103">PowerShell을 사용 하 여 응용 프로그램 tooyour 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="91cfc-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="91cfc-104">개요</span><span class="sxs-lookup"><span data-stu-id="91cfc-104">Overview</span></span>
<span data-ttu-id="91cfc-105">Azure 앱 서비스의 응용 프로그램 (웹, 모바일, 또는 API)를 연결할 수 있습니다 tooan 구독에서 Azure 가상 네트워크 (VNet).</span><span class="sxs-lookup"><span data-stu-id="91cfc-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="91cfc-106">이 기능은 VNet 통합이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="91cfc-107">hello VNet 통합 기능 toorun 가상 네트워크에 Azure 앱 서비스의 인스턴스 수 있는 hello 앱 서비스 환경 기능을 사용 하면 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="91cfc-108">hello VNet 통합 기능에 toointegrate hello 클래식 배포 모델 또는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 배포 되는 가상 네트워크에 사용할 수 있는 hello 새로운 포털에서 사용자 인터페이스 (UI) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="91cfc-109">Toolearn hello 기능에 대 한 자세한 참조 [앱을 Azure 가상 네트워크와 통합](web-sites-integrate-with-vnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="91cfc-110">이 문서는 toouse UI hello 하는 방법에 대 한 하지 않지만 대신 방법에 대 한 PowerShell을 사용 하 여 tooenable 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="91cfc-111">각 배포 모델에 대 한 hello 명령에서 다른 되므로이 문서는 각 배포 모델에 대 한 섹션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="91cfc-112">이 문서를 진행하기 전에 다음이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="91cfc-113">최신 Azure PowerShell SDK를 설치 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="91cfc-114">웹 플랫폼 설치 관리자 hello로이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="91cfc-115">표준 또는 프리미엄 SKU에서 실행 중인 Azure 앱 서비스의 앱</span><span class="sxs-lookup"><span data-stu-id="91cfc-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="91cfc-116">클래식 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="91cfc-116">Classic virtual networks</span></span>
<span data-ttu-id="91cfc-117">이 섹션에서는 hello 클래식 배포 모델을 사용 하는 가상 네트워크에 대 한 세 가지 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="91cfc-118">응용 프로그램 tooa 기존 가상 네트워크 게이트웨이 않았으며 지점 및 사이트 연결에 대해 구성 되어 있는 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="91cfc-119">앱에 대한 가상 네트워크 통합 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="91cfc-120">가상 네트워크에서 앱 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="91cfc-121">응용 프로그램 tooa 연결 클래식 VNet</span><span class="sxs-lookup"><span data-stu-id="91cfc-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="91cfc-122">tooconnect 앱 tooa 가상 네트워크는 다음 세 가지 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="91cfc-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="91cfc-123">것은 될 특정 가상 네트워크에 연결할 toohello 웹 앱을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="91cfc-124">hello 앱 지점 및 사이트 간 연결용 가상 네트워크 toohello 제공 될 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="91cfc-125">Hello 웹 응용 프로그램 인증서 toohello 가상 네트워크를 업로드 하 고 hello 지점-사이트 VPN 패키지 URI를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="91cfc-126">Hello 지점 및 사이트 패키지 URI와 hello 웹 응용 프로그램의 가상 네트워크 연결을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="91cfc-127">hello 첫 번째 및 세 번째 단계는 완전히 스크립트 가능 하지만 두 번째 단계 hello hello 포털 또는 액세스 tooperform을 통해 일회성 인 수동 작업이 필요한 **배치** 또는 **패치** hello 가상 네트워크에 대 한 작업 Azure 리소스 관리자 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="91cfc-128">이 옵션을 사용 toohave Azure 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="91cfc-129">시작하기 전에 게이트웨이가 설정되고 배포된 지점 및 사이트 간 연결이 이미 활성화된 클래식 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="91cfc-130">toocreate hello 게이트웨이 사용 하도록 설정한 지점 및 사이트 간 연결, 필요한 toouse hello 포털에 설명 된 대로 [VPN 게이트웨이 만들지][createvpngateway]합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="91cfc-131">hello 클래식 가상 네트워크 필요 toobe hello에 앱 서비스와 같은 구독을 통합 하는 해당 보류 hello 응용 프로그램을 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="91cfc-132">Azure PowerShell SDK 설정</span><span class="sxs-lookup"><span data-stu-id="91cfc-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="91cfc-133">PowerShell 창을 열고 다음을 사용하여 Azure 계정 및 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="91cfc-134">해당 명령의 열립니다 Azure 자격 증명 프롬프트 tooget 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="91cfc-135">에 로그인 한 후 hello 명령을 tooselect hello 구독 toouse 되도록 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="91cfc-136">가상 네트워크 및 앱 서비스 계획에 있는 hello 구독을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="91cfc-137">또는</span><span class="sxs-lookup"><span data-stu-id="91cfc-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="91cfc-138">이 문서에 사용된 변수</span><span class="sxs-lookup"><span data-stu-id="91cfc-138">Variables used in this article</span></span>
<span data-ttu-id="91cfc-139">toosimplify 명령을 설정 해 드립니다는 **$Configuration** hello 특정 구성 사용 하 여 PowerShell 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="91cfc-140">매개 변수 뒤 hello로 PowerShell에서 다음과 같이 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="91cfc-141">hello 응용 프로그램 위치에는 공백 없이 hello 위치 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="91cfc-142">예를 들어 미국 서부는 westus입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="91cfc-143">hello 다음 항목은 hello 인증서 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="91cfc-144">로컬 컴퓨터에서 쓰기 가능한 경로여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="91cfc-145">Hello 끝 tooinclude.cer 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="91cfc-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="91cfc-146">toosee 설정, 형식 **$Configuration**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="91cfc-147">이 섹션의 나머지 부분 hello 앞서 설명한 만든 변수 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="91cfc-148">Hello 가상 네트워크 toohello 앱 선언</span><span class="sxs-lookup"><span data-stu-id="91cfc-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="91cfc-149">다음 명령 tootell hello 앱을 사용할 것이 가상 네트워크는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="91cfc-150">이렇게 하면 hello 앱 toogenerate 필요한 인증서:</span><span class="sxs-lookup"><span data-stu-id="91cfc-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="91cfc-151">이 명령이 성공하면 **$vnet**에는 **속성** 변수가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="91cfc-152">hello **속성** 변수 모두는 인증서 지문 및 hello 인증서 데이터를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="91cfc-153">Hello 웹 응용 프로그램 인증서 toohello 가상 네트워크를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="91cfc-154">각 구독 및 가상 네트워크 조합에 일회성 수동 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="91cfc-155">즉, 구독 A tooVirtual 네트워크 A에서 응용 프로그램을 연결 하는 할 경우 toodo이이 단계 구성한 앱 수에 관계 없이 한 번만 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="91cfc-156">새 앱 tooanother 가상 네트워크를 추가 하는 경우 해야 toodo 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="91cfc-157">이 대 한 hello 이유는 Azure 앱 서비스의 구독 수준에는 인증서 집합을 생성 하는 hello 집합 hello 앱에 연결 하는 각 가상 네트워크에 대해 한 번 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="91cfc-158">hello 인증서는 이미 설정 되어 다음이 단계를 따라 또는 통합 한 경우 hello로 동일 hello 포털을 사용 하 여 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="91cfc-159">hello 첫 번째 단계는 toogenerate hello.cer 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="91cfc-160">hello 두 번째 단계는 tooupload hello.cer 파일 tooyour 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="91cfc-161">toogenerate hello.cer 파일 hello에 hello API 호출에서 이전 단계를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="91cfc-162">hello 인증서 섹션 hello 위치는 **$Configuration.GeneratedCertificatePath** 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="91cfc-163">tooupload hello 인증서를 직접 사용 하 여 hello [Azure 포털] [ azureportal] 및 **찾아보기 가상 네트워크 (클래식)** > **VPN연결**  >  **지점-사이트** > **인증서 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="91cfc-164">여기에서 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="91cfc-165">Hello 지점 및 사이트 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="91cfc-165">Get hello point-to-site package</span></span>
<span data-ttu-id="91cfc-166">웹 앱에 대 한 가상 네트워크 연결을 설정할 hello 다음 단계는 tooget hello 지점 및 사이트 패키지 하 고 tooyour 웹 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="91cfc-167">다음 예를 들어 C:\Azure\Templates\GetNetworkPackageUri.json 컴퓨터에 GetNetworkPackageUri.json 어딘가에 라는 템플릿 tooa 파일 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="91cfc-168">입력 매개 변수 설정:</span><span class="sxs-lookup"><span data-stu-id="91cfc-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="91cfc-169">Hello 스크립트를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="91cfc-170">hello 변수 **$output 합니다. Outputs.packageUri** tooyour 웹 응용 프로그램을 제공 하는 hello 패키지 URI toobe 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="91cfc-171">Hello 지점 및 사이트 패키지 tooyour 앱 업로드</span><span class="sxs-lookup"><span data-stu-id="91cfc-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="91cfc-172">hello 마지막 단계는이 패키지와 tooprovide hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="91cfc-173">Hello 다음 명령을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="91cfc-174">메시지가 기존 리소스를 덮어쓰는 tooconfirm를 묻는 확인 되었는지 tooallow 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="91cfc-175">이 명령은 성공 하면 앱 가상 네트워크에 연결 된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="91cfc-176">tooconfirm 성공 tooyour 응용 프로그램 콘솔을 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="91cfc-177">Hello 대상 가상 네트워크의 hello 이름과 일치 하는 값을 가진 WEBSITE_VNETNAME 라는 환경 변수 이면 모든 구성에 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="91cfc-178">클래식 VNet 통합 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="91cfc-178">Update classic VNet integration information</span></span>
<span data-ttu-id="91cfc-179">tooupdate 또는 사용자의 정보를 다시 동기화, 단순히 hello 첫 번째 위치에서 hello 통합을 만들 때 수행한 hello 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="91cfc-180">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-180">Those steps are:</span></span>

1. <span data-ttu-id="91cfc-181">구성 정보를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-181">Define your configuration information.</span></span>
2. <span data-ttu-id="91cfc-182">Hello 가상 네트워크 toohello 앱을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="91cfc-183">Hello 지점 및 사이트 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="91cfc-184">Hello 지점 및 사이트 패키지 tooyour 앱을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="91cfc-185">클래식 VNet에서 앱 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="91cfc-186">toodisconnect hello 앱 가상 네트워크 통합 하는 동안 설정 된 hello 구성 정보를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="91cfc-187">해당 정보를 사용 하는 하나의 명령 toodisconnect 다음 가상 네트워크에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="91cfc-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="91cfc-188">리소스 관리자 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="91cfc-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="91cfc-189">리소스 관리자 가상 네트워크에는 클래식 가상 네트워크와 비교했을 때 일부 프로세스를 간소화하는 Azure Resource Manager API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="91cfc-190">Hello 다음 작업을 완료 하는 데 도움이 되는 스크립트를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="91cfc-191">리소스 관리자 가상 네트워크를 만들고 앱을 여기에 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="91cfc-192">게이트웨이를 만들고 기존 리소스 관리자 가상 네트워크에서 지점 및 사이트 간 연결을 구성 후 앱을 함께 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="91cfc-193">게이트웨이가 있고 지점 및 사이트 간 연결이 활성화된 기존 리소스 관리자 가상 네트워크와 앱을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="91cfc-194">가상 네트워크에서 앱 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="91cfc-195">리소스 관리자 VNet 앱 서비스 통합 스크립트</span><span class="sxs-lookup"><span data-stu-id="91cfc-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="91cfc-196">다음 스크립트를 tooa 파일을 저장 하는 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="91cfc-197">Toouse hello 스크립트를 사용 하지 않으려는 경우 느껴집니다 여기에서 무료 toolearn toosee 어떻게 tooset 리소스 관리자 가상 네트워크와 함께 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="91cfc-198">Hello 스크립트의 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-198">Save a copy of hello script.</span></span> <span data-ttu-id="91cfc-199">이 문서에서는 V2VnetAllinOne.ps1라고 하지만 다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="91cfc-200">이 스크립트에 대한 인수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-200">There are no arguments for this script.</span></span> <span data-ttu-id="91cfc-201">단순히 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-201">You simply run it.</span></span> <span data-ttu-id="91cfc-202">hello 먼저 hello 스크립트 처리 해 toosign에 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="91cfc-203">에 로그인 한 후 hello 스크립트는 사용자 계정에 대 한 세부 정보를 가져오고 구독 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="91cfc-204">자격 증명에 대 한 hello 요청을 세 지 않고, hello 초기 스크립트 실행은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="91cfc-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="91cfc-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="91cfc-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="91cfc-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="91cfc-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="91cfc-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="91cfc-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="91cfc-208">Choose an option: 3</span></span>

    <span data-ttu-id="91cfc-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="91cfc-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="91cfc-210">Hello 응용 프로그램의 리소스 그룹을 입력 하십시오: hcdemo rg hello 응용 프로그램의 이름을 입력 하십시오: v2vnetpowershell 하 신 toodo 원하는?</span><span class="sxs-lookup"><span data-stu-id="91cfc-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="91cfc-211">새 가상 네트워크 tooan 앱 추가</span><span class="sxs-lookup"><span data-stu-id="91cfc-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="91cfc-212">기존 가상 네트워크 tooan 앱 추가</span><span class="sxs-lookup"><span data-stu-id="91cfc-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="91cfc-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="91cfc-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="91cfc-214">hello이이 단원의 나머지 부분에서는 이러한 세 가지 옵션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="91cfc-215">리소스 관리자 VNet 만들기 및 통합</span><span class="sxs-lookup"><span data-stu-id="91cfc-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="91cfc-216">toocreate 및 사용 하 여 리소스 관리자 배포 모델을 hello와 응용 프로그램을 통합 하 여 새 가상 네트워크 선택 **1) 새 가상 네트워크 tooan 앱 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="91cfc-217">Hello 가상 네트워크의 hello 이름 하면이 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="91cfc-218">필자의 경우 hello 설정을 뒤에서 볼 수 v2pshell hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="91cfc-219">hello 스크립트는 생성 중인 hello 가상 네트워크에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="91cfc-220">hello 값 중 하나를 변경할 수 있습니까 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="91cfc-221">이 예제에서는 실행 hello 다음 설정 된 가상 네트워크를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="91cfc-222">Toochange hello 값을 입력 **Y** hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="91cfc-223">Hello 가상 네트워크 설정에 만족 하는 경우 입력 **N** 하거나 단순히 hello 설정을 변경 하는 방법에 대 한 메시지가 표시 되 면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="91cfc-224">대 완료 될 때까지 여기에서 hello 스크립트를 알려 줍니다 일부 어떤 it' i toocreate hello 가상 네트워크 게이트웨이 시작 되기 전까지 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="91cfc-225">해당 단계 tooan 시간을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-225">That step can take up tooan hour.</span></span> <span data-ttu-id="91cfc-226">이 단계 동안 진행률 표시기가 없습니다 있지만 hello 게이트웨이가 때 만들어짐 알 hello 스크립트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="91cfc-227">말할 hello 스크립트 작업을 마치면 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="91cfc-228">이 시점에서 hello 이름을 가진 리소스 관리자 가상 네트워크 및 선택한 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="91cfc-229">이 새로운 가상 네트워크도 앱과 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="91cfc-230">기존 리소스 관리자 VNet와 앱 통합</span><span class="sxs-lookup"><span data-stu-id="91cfc-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="91cfc-231">에 게이트웨이 또는 지점 및 사이트 연결 없는 리소스 관리자 가상 네트워크를 제공 하는 경우 기존 가상 네트워크와 통합 하는 경우 hello 스크립트를 설정 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="91cfc-232">Hello VNET에 이미 이러한 일 들을 설정 하는 경우 hello 스크립트 직선 toohello 응용 프로그램 통합을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="91cfc-233">toostart이이 프로세스를 선택 하기만 하면 **2) 기존 가상 네트워크 tooan 앱 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="91cfc-234">Hello에 있는 기존 리소스 관리자 가상 네트워크에 있는 경우에이 옵션은 사용할 앱과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="91cfc-235">Hello 옵션을 선택한 후 리소스 관리자 가상 네트워크의 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="91cfc-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="91cfc-236">v2demonetwork</span></span>
    2) <span data-ttu-id="91cfc-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="91cfc-237">v2pshell</span></span>
    3) <span data-ttu-id="91cfc-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="91cfc-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="91cfc-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="91cfc-239">v2asenetwork</span></span>
    5) <span data-ttu-id="91cfc-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="91cfc-240">v2pshell2</span></span>

    <span data-ttu-id="91cfc-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="91cfc-241">Choose an option: 5</span></span>

<span data-ttu-id="91cfc-242">단순히 hello와 toointegrate 원하는 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="91cfc-243">지점 및 사이트 연결을 사용 하도록 설정 되어 있는 게이트웨이 이미 있는 경우 hello 스크립트 가상 네트워크에 앱을 간단히 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="91cfc-244">게이트웨이 toospecify hello 게이트웨이 서브넷을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="91cfc-245">게이트웨이 서브넷은 가상 네트워크 주소 공간에 있어야 하고 다른 서브넷에 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="91cfc-246">게이트웨이가 없는 가상 네트워크가 있고 이 단계를 실행하는 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="91cfc-247">이 예제에서는 hello 설정을 뒤에 있는 가상 네트워크 게이트웨이 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="91cfc-248">Toochange, 이러한 설정을 사용할 경우이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="91cfc-249">그렇지 않은 경우 Enter 키를 누릅니다 및 hello 스크립트는 게이트웨이 만들고 앱 tooyour 가상 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="91cfc-250">hello 게이트웨이 만든 시간은 경우에 한 시간 여전히, 염두에서 계속가지고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="91cfc-251">Hello 스크립트는 예를 들어 모든 항목 완료 되 면 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="91cfc-252">리소스 관리자 VNet에서 앱 연결 끊기</span><span class="sxs-lookup"><span data-stu-id="91cfc-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="91cfc-253">가상 네트워크에서 응용 프로그램 연결을 해제 해도 hello 게이트웨이 작동 중지 하거나 지점 및 사이트 연결을 사용 하지 않도록 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="91cfc-254">어차피 다른 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="91cfc-255">것도 끊어지지 않습니다 것 hello 이외의 다른 앱에서 사용자가 제공한 하나.</span><span class="sxs-lookup"><span data-stu-id="91cfc-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="91cfc-256">tooperform이이 작업을 선택 **3) 응용 프로그램에서 가상 네트워크를 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="91cfc-257">이를 수행할 때 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="91cfc-258">Hello 스크립트 표시 되지만 delete을 hello 가상 네트워크는 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="91cfc-259">것 바로 제거 하는 hello 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-259">It’s just removing hello integration.</span></span> <span data-ttu-id="91cfc-260">원하는 작업 인지 확인 한 후, toodo hello 명령 매우 신속 하 게 처리 되 고 알려 **True** 완료 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="91cfc-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
