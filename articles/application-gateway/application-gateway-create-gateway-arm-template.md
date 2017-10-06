---
title: "Azure 응용 프로그램 게이트웨이-템플릿 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate Azure 응용 프로그램 게이트웨이 hello Azure 리소스 관리자 템플릿을 사용 하 여"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="ea329-103">Hello Azure 리소스 관리자 템플릿을 사용 하 여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ea329-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea329-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ea329-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ea329-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea329-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ea329-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea329-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ea329-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="ea329-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ea329-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ea329-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ea329-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ea329-110">Hello 클라우드 또는 온-프레미스에 있는지 여부를 장애 조치 및 다른 서버 간에 HTTP 요청 성능 라우팅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="ea329-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ea329-112">지원 되는 기능의 전체 목록은 toofind 방문 [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ea329-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="ea329-113">이 문서 다운로드 및 GitHub에서 기존 Azure 리소스 관리자 템플릿을 수정 하 고, GitHub, PowerShell 및 Azure CLI hello에서 hello 템플릿을 배포을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="ea329-114">Hello Azure 리소스 관리자 템플릿을 변경 하지 않고 GitHub에서 직접 단순히 배포 하는 경우 GitHub에서 toodeploy 서식 파일을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="ea329-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="ea329-115">Scenario</span></span>

<span data-ttu-id="ea329-116">이 시나리오에서는</span><span class="sxs-lookup"><span data-stu-id="ea329-116">In this scenario you will:</span></span>

* <span data-ttu-id="ea329-117">웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ea329-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="ea329-118">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 VirtualNetwork1인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ea329-119">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="ea329-120">Tooload hello 트래픽 분산을 원하는 hello 웹 서버에 대 한 두 개의 이전에 구성 된 백 엔드 Ip를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="ea329-121">이 서식 파일 예제에서는 hello 백 엔드 Ip는 10.0.1.10 및 10.0.1.11 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="ea329-122">이러한 설정은이 서식 파일에 대 한 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="ea329-123">toocustomize hello 템플릿 규칙, hello 수신기, SSL 및 hello azuredeploy.json 파일에서 다른 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![시나리오](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="ea329-125">다운로드 하 고 hello Azure 리소스 관리자 서식 파일 이해</span><span class="sxs-lookup"><span data-stu-id="ea329-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="ea329-126">GitHub에서 hello 기존 Azure 리소스 관리자 템플릿 toocreate 가상 네트워크 및 서브넷 2 개를 다운로드, 변경 수도, 있으며 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="ea329-127">따라서 toodo 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="ea329-128">너무 이동[웹 응용 프로그램 방화벽이 설정 되어 있으면 응용 프로그램 게이트웨이 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ea329-129">**azuredeploy.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ea329-130">컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="ea329-131">Azure 리소스 관리자 템플릿을 익숙한 경우에 7 toostep을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="ea329-132">Hello 저장 한 파일을 열고 아래 hello 내용을 확인 **매개 변수** 줄에서</span><span class="sxs-lookup"><span data-stu-id="ea329-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="ea329-133">Azure 리소스 관리자 템플릿 매개 변수는 배포하는 동안 채울 수 있는 값에 대한 자리 표시자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="ea329-134">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ea329-134">Parameter</span></span> | <span data-ttu-id="ea329-135">설명</span><span class="sxs-lookup"><span data-stu-id="ea329-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="ea329-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="ea329-136">**subnetPrefix**</span></span> |<span data-ttu-id="ea329-137">Hello 응용 프로그램 게이트웨이 서브넷에 대 한 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="ea329-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="ea329-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="ea329-139">Hello 응용 프로그램 게이트웨이의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-139">Size of hello application gateway.</span></span>  <span data-ttu-id="ea329-140">WAF는 중형 및 대형만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="ea329-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="ea329-141">**backendIpaddress1**</span></span> |<span data-ttu-id="ea329-142">Hello 첫 번째 웹 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="ea329-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="ea329-143">**backendIpaddress2**</span></span> |<span data-ttu-id="ea329-144">Hello 두 번째 웹 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="ea329-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="ea329-145">**wafEnabled**</span></span> | <span data-ttu-id="ea329-146">Toodetermine WAF 사용 되는 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="ea329-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="ea329-147">**wafMode**</span></span> | <span data-ttu-id="ea329-148">Hello 웹 응용 프로그램 방화벽의 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="ea329-149">사용 가능한 옵션은 **방지** 또는 **검색**입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="ea329-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="ea329-150">**wafRuleSetType**</span></span> | <span data-ttu-id="ea329-151">WAF에 대한 규칙 집합 유형.</span><span class="sxs-lookup"><span data-stu-id="ea329-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="ea329-152">현재 OWASP hello만 지원 되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="ea329-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="ea329-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="ea329-154">규칙 집합 버전.</span><span class="sxs-lookup"><span data-stu-id="ea329-154">Ruleset version.</span></span> <span data-ttu-id="ea329-155">OWASP CRS 2.2.9 퀵 및 3.0은 현재 지원 되는 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="ea329-156">Hello 내용을 확인 **리소스** 통지 hello 다음과 같은 속성 및:</span><span class="sxs-lookup"><span data-stu-id="ea329-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="ea329-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="ea329-157">**type**.</span></span> <span data-ttu-id="ea329-158">Hello 템플릿으로 생성 되는 리소스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="ea329-159">이 경우 hello 형식이 `Microsoft.Network/applicationGateways`, 응용 프로그램 게이트웨이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="ea329-160">**이름**.</span><span class="sxs-lookup"><span data-stu-id="ea329-160">**name**.</span></span> <span data-ttu-id="ea329-161">Hello 리소스에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-161">Name for hello resource.</span></span> <span data-ttu-id="ea329-162">공지 hello 사용 `[parameters('applicationGatewayName')]`, 해당 hello 이름이 입력으로 제공 되는 매개 변수 파일 또는가 배포 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="ea329-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="ea329-163">**properties**.</span></span> <span data-ttu-id="ea329-164">Hello 리소스에 대 한 속성 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-164">List of properties for hello resource.</span></span> <span data-ttu-id="ea329-165">이 템플릿은 응용 프로그램 게이트웨이 만드는 동안 hello 가상 네트워크와 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ea329-166">템플릿에 대한 자세한 내용은 [Resource Manager 템플릿 참조](/templates/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea329-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="ea329-167">너무 탐색[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ea329-168">**azuredeploy-parameters.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ea329-169">컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="ea329-170">Hello 저장 한 파일을 열고 hello hello 매개 변수 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="ea329-171">다음 시나리오에서 설명 하는 값 toodeploy hello 응용 프로그램 게이트웨이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="ea329-172">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-172">Save hello file.</span></span> <span data-ttu-id="ea329-173">와 같은 온라인 JSON 유효성 검사 도구를 사용 하 여 hello JSON 템플릿과 템플릿 매개 변수를 테스트할 수 있습니다 [JSlint.com](http://www.jslint.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="ea329-174">PowerShell을 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="ea329-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="ea329-175">Azure PowerShell을 처음 사용 하는 경우: [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 및 hello 지침 toosign Azure에 따르고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="ea329-176">로그인 tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="ea329-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="ea329-177">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="ea329-178">사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="ea329-179">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="ea329-180">필요한 경우 hello를 사용 하 여 리소스 그룹을 만들 **새로 AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ea329-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="ea329-181">다음 예제는 hello, 미국 동부 위치에 AppgatewayRG 라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="ea329-182">Hello 실행 **새로 AzureRmResourceGroupDeployment** cmdlet toodeploy hello 새 가상 네트워크 hello 앞에 다운로드 하 고 수정 된 서식 파일 및 매개 변수 파일을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="ea329-183">Hello Azure CLI를 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="ea329-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="ea329-184">Azure CLI를 사용 하 여 다운로드 한 toodeploy hello Azure 리소스 관리자 템플릿을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="ea329-185">Azure CLI 처음 사용 하는 경우 참조 [설치 하 고 Azure CLI hello 구성](/cli/azure/install-azure-cli) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="ea329-186">실행 hello, 필요한 경우 `az group create` 명령 toocreate hello 다음 코드 조각에에서 나와 있는 것 처럼 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="ea329-187">Hello hello 명령의 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-187">Notice hello output of hello command.</span></span> <span data-ttu-id="ea329-188">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="ea329-189">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea329-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="ea329-190">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="ea329-190">**-n (or --name)**.</span></span> <span data-ttu-id="ea329-191">Hello 새로운 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-191">Name for hello new resource group.</span></span> <span data-ttu-id="ea329-192">이 시나리오에서는 *appgatewayRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="ea329-193">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="ea329-193">**-l (or --location)**.</span></span> <span data-ttu-id="ea329-194">Azure 지역 hello 새 리소스 그룹이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="ea329-195">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="ea329-196">Hello 실행 `az group deployment create` cmdlet toodeploy hello 새 가상 네트워크 hello 템플릿 및 매개 변수를 사용 하 여 파일을 다운로드 하 고 hello 앞 단계에서에서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="ea329-197">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="ea329-198">-배포를 사용 하 여 hello Azure 리소스 관리자 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="ea329-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="ea329-199">-배포를 Azure 리소스 관리자 템플릿을 다른 방식으로 toouse가입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="ea329-200">Hello Azure 포털을 사용 하 여 쉽게 toouse 템플릿을 경우</span><span class="sxs-lookup"><span data-stu-id="ea329-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="ea329-201">너무 이동[웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="ea329-202">클릭 **tooAzure 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-202">Click **Deploy tooAzure**.</span></span>

    ![TooAzure 배포](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="ea329-204">Hello 포털에 배포 템플릿 hello에 대 한 hello 매개 변수를 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![매개 변수](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="ea329-206">선택 **toohello 약관 위에서 설명한 동의** 클릭 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="ea329-207">Hello 사용자 지정 배포 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="ea329-208">인증서 데이터 tooResource 관리자 템플릿으로 제공</span><span class="sxs-lookup"><span data-stu-id="ea329-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="ea329-209">템플릿을 사용 하 여 SSL을 사용 하는 경우 hello 인증서 toobe 업로드 되 고 대신 base64 문자열에 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="ea329-210">tooconvert.pfx 또는.cer tooa base64 문자열 hello 다음 명령 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="ea329-211">hello 다음 명령을 hello 인증서 tooa base64 문자열을 변환, toohello 템플릿을 제공 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="ea329-212">hello 예상 출력은 변수에 저장 하 고 hello 서식 파일에 붙여넣을 수 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="ea329-213">macOS</span><span class="sxs-lookup"><span data-stu-id="ea329-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="ea329-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ea329-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="ea329-215">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="ea329-215">Delete all resources</span></span>

<span data-ttu-id="ea329-216">이 문서의 단계를 수행 하는 hello 중 하나를 수행 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="ea329-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="ea329-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea329-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="ea329-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ea329-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="ea329-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea329-219">Next steps</span></span>

<span data-ttu-id="ea329-220">SSL 오프 로드 tooconfigure 방문: [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ea329-221">내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 방문: [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea329-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="ea329-222">부하 분산 옵션에 대한 자세한 정보는 다음을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ea329-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="ea329-223">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="ea329-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ea329-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ea329-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

