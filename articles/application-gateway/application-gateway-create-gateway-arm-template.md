---
title: "Azure Application Gateway 만들기 - 템플릿 | Microsoft Docs"
description: "이 페이지에서는 Azure 리소스 관리자 템플릿을 사용하여 Azure 응용 프로그램 게이트웨이를 만드는 지침을 제공합니다."
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="edf37-103">Azure 리소스 관리자 템플릿을 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="edf37-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="edf37-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="edf37-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="edf37-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf37-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="edf37-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf37-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="edf37-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="edf37-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="edf37-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="edf37-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="edf37-109">Azure 응용 프로그램 게이트웨이는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="edf37-110">클라우드 또는 온-프레미스에 상관없이 서로 다른 서버 간에 장애 조치(failover) 및 성능 라우팅 HTTP 요청을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="edf37-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타를 포함하여 다양한 ADC(Application Delivery Controller) 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="edf37-112">지원되는 기능의 전체 목록을 찾으려면 [Application Gateway 개요](application-gateway-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="edf37-113">이 문서에서는 GitHub에서 기존 Azure Resource Manager 템플릿을 다운로드 및 수정하고 GitHub, PowerShell 및 Azure CLI에서 템플릿을 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="edf37-114">변경하지 않고 GitHub에서 직접 Azure 리소스 관리자 템플릿을 배포하는 경우 GitHub에서 템플릿 배포로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="edf37-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="edf37-115">Scenario</span></span>

<span data-ttu-id="edf37-116">이 시나리오에서는</span><span class="sxs-lookup"><span data-stu-id="edf37-116">In this scenario you will:</span></span>

* <span data-ttu-id="edf37-117">웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="edf37-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="edf37-118">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 VirtualNetwork1인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="edf37-119">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="edf37-120">트래픽을 부하 분산하려는 웹 서버에 대해 이전에 구성된 백 엔드 IP 2개를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="edf37-121">이 템플릿 예제에서 백 엔드 IP는 10.0.1.10 및 10.0.1.11이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="edf37-122">이러한 설정은 이 템플릿에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="edf37-123">템플릿을 사용자 지정하려면 규칙, 수신기, SSL 및 azuredeploy.json 파일의 기타 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![시나리오](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="edf37-125">Azure 리소스 관리자 템플릿 다운로드 및 이해</span><span class="sxs-lookup"><span data-stu-id="edf37-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="edf37-126">GitHub에서 가상 네트워크 및 두 개의 서브넷을 만들기 위한 기존 Azure 리소스 관리자 템플릿을 다운로드하고 원하는 대로 변경한 후 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="edf37-127">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="edf37-128">[웹 응용 프로그램 방화벽이 설정된 Application Gateway 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="edf37-129">**azuredeploy.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="edf37-130">파일을 컴퓨터의 로컬 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="edf37-131">Azure 리소스 관리자 템플릿에 익숙한 경우 7단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="edf37-132">저장한 파일을 열고 줄에서 **parameters** 아래의 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="edf37-133">Azure 리소스 관리자 템플릿 매개 변수는 배포하는 동안 채울 수 있는 값에 대한 자리 표시자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="edf37-134">매개 변수</span><span class="sxs-lookup"><span data-stu-id="edf37-134">Parameter</span></span> | <span data-ttu-id="edf37-135">설명</span><span class="sxs-lookup"><span data-stu-id="edf37-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="edf37-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="edf37-136">**subnetPrefix**</span></span> |<span data-ttu-id="edf37-137">응용 프로그램 게이트웨이 서브넷에 대한 CIDR 블록</span><span class="sxs-lookup"><span data-stu-id="edf37-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="edf37-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="edf37-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="edf37-139">Application Gateway의 크기.</span><span class="sxs-lookup"><span data-stu-id="edf37-139">Size of the application gateway.</span></span>  <span data-ttu-id="edf37-140">WAF는 중형 및 대형만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="edf37-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="edf37-141">**backendIpaddress1**</span></span> |<span data-ttu-id="edf37-142">첫 번째 웹 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="edf37-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="edf37-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="edf37-143">**backendIpaddress2**</span></span> |<span data-ttu-id="edf37-144">두 번째 웹 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="edf37-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="edf37-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="edf37-145">**wafEnabled**</span></span> | <span data-ttu-id="edf37-146">WAF가 사용되도록 설정되어 있는지를 결정하는 설정</span><span class="sxs-lookup"><span data-stu-id="edf37-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="edf37-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="edf37-147">**wafMode**</span></span> | <span data-ttu-id="edf37-148">웹 응용 프로그램 방화벽의 모드</span><span class="sxs-lookup"><span data-stu-id="edf37-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="edf37-149">사용 가능한 옵션은 **방지** 또는 **검색**입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="edf37-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="edf37-150">**wafRuleSetType**</span></span> | <span data-ttu-id="edf37-151">WAF에 대한 규칙 집합 유형.</span><span class="sxs-lookup"><span data-stu-id="edf37-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="edf37-152">현재 OWASP만 지원되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="edf37-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="edf37-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="edf37-154">규칙 집합 버전.</span><span class="sxs-lookup"><span data-stu-id="edf37-154">Ruleset version.</span></span> <span data-ttu-id="edf37-155">OWASP CRS 2.2.9 및 3.0이 현재 지원되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="edf37-156">**resources** 아래의 내용을 확인하고 다음 속성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="edf37-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="edf37-157">**type**.</span></span> <span data-ttu-id="edf37-158">템플릿에 의해 생성되는 리소스의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-158">Type of resource being created by the template.</span></span> <span data-ttu-id="edf37-159">이 경우 형식은 응용 프로그램 게이트웨이를 나타내는 `Microsoft.Network/applicationGateways`입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="edf37-160">**이름**.</span><span class="sxs-lookup"><span data-stu-id="edf37-160">**name**.</span></span> <span data-ttu-id="edf37-161">리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-161">Name for the resource.</span></span> <span data-ttu-id="edf37-162">`[parameters('applicationGatewayName')]`이 사용됩니다. 이것은 해당 이름이 배포 중에 사용자 또는 매개 변수 파일에 의한 입력으로 제공됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="edf37-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="edf37-163">**properties**.</span></span> <span data-ttu-id="edf37-164">리소스의 속성 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-164">List of properties for the resource.</span></span> <span data-ttu-id="edf37-165">이 템플릿은 응용 프로그램 게이트웨이를 만드는 동안 가상 네트워크 및 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="edf37-166">템플릿에 대한 자세한 내용은 [Resource Manager 템플릿 참조](/templates/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="edf37-167">[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="edf37-168">**azuredeploy-parameters.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="edf37-169">파일을 컴퓨터의 로컬 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="edf37-170">저장한 파일을 열고 매개 변수 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="edf37-171">다음 값을 사용하여 이 시나리오에 설명된 응용 프로그램 게이트웨이를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="edf37-172">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-172">Save the file.</span></span> <span data-ttu-id="edf37-173">[JSlint.com](http://www.jslint.com/)같은 JSON 유효성 검사 도구를 사용하여 JSON 템플릿과 매개 변수 템플릿을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="edf37-174">PowerShell을 사용하여 Azure 리소스 관리자 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="edf37-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="edf37-175">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하고 지침에 따라 Azure에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="edf37-176">PowerShell에 로그인</span><span class="sxs-lookup"><span data-stu-id="edf37-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="edf37-177">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="edf37-178">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="edf37-179">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="edf37-180">필요한 경우 **New-AzureResourceGroup** cmdlet을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="edf37-181">다음 예제에서는 미국 동부 위치에 AppgatewayRG라고 하는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="edf37-182">**New-AzureRmResourceGroupDeployment** cmdlet을 실행하고 위에서 다운로드한 후 수정한 이전의 템플릿 및 매개 변수 파일을 사용하여 새 가상 네트워크를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="edf37-183">Azure CLI를 사용하여 Azure 리소스 관리자 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="edf37-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="edf37-184">Azure CLI를 사용하여 다운로드한 Azure Resource Manager 템플릿을 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="edf37-185">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](/cli/azure/install-azure-cli)을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="edf37-186">필요한 경우 다음 코드 조각과 같이 `az group create` 명령을 실행하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="edf37-187">명령의 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-187">Notice the output of the command.</span></span> <span data-ttu-id="edf37-188">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="edf37-189">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="edf37-190">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="edf37-190">**-n (or --name)**.</span></span> <span data-ttu-id="edf37-191">새 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-191">Name for the new resource group.</span></span> <span data-ttu-id="edf37-192">이 시나리오에서는 *appgatewayRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="edf37-193">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="edf37-193">**-l (or --location)**.</span></span> <span data-ttu-id="edf37-194">새 리소스 그룹이 생성되는 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="edf37-195">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="edf37-196">`az group deployment create` cmdlet을 실행하고 이전 단계에서 다운로드한 후 수정한 템플릿 및 매개 변수를 사용하여 새 가상 네트워크를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="edf37-197">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="edf37-198">클릭하여 배포를 사용하여 Azure 리소스 관리자 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="edf37-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="edf37-199">클릭하여 배포는 Azure 리소스 관리자 템플릿을 사용하는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="edf37-200">Azure 포털에서 템플릿을 사용하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="edf37-201">[웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="edf37-202">**Deploy to Azure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-202">Click **Deploy to Azure**.</span></span>

    ![Deploy to Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="edf37-204">포털에서 배포 템플릿에 대한 매개 변수를 채우고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![매개 변수](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="edf37-206">**위에 명시된 사용 약관에 동의함**을 선택한 다음 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="edf37-207">사용자 지정 배포 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="edf37-208">Resource Manager 템플릿에 인증서 데이터 제공</span><span class="sxs-lookup"><span data-stu-id="edf37-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="edf37-209">템플릿과 함께 SSL을 사용하는 경우 인증서를 업로드하는 대신 base64 문자열에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="edf37-210">.pfx 또는 .cer을 base64 문자열로 변환하려면 다음 명령 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="edf37-211">다음 명령은 인증서를 base64 문자열로 변환하며, 그러면 인증서를 템플릿에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="edf37-212">예상 출력은 변수에 저장되고 템플릿에 붙여넣을 수 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="edf37-213">macOS</span><span class="sxs-lookup"><span data-stu-id="edf37-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="edf37-214">Windows</span><span class="sxs-lookup"><span data-stu-id="edf37-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="edf37-215">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="edf37-215">Delete all resources</span></span>

<span data-ttu-id="edf37-216">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계 중 하나를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="edf37-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="edf37-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf37-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="edf37-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="edf37-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="edf37-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edf37-219">Next steps</span></span>

<span data-ttu-id="edf37-220">SSL 오프로드를 구성하려는 경우 [SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="edf37-221">내부 부하 분산 장치에서 사용하도록 응용 프로그램 게이트웨이를 구성하려면 [ILB(내부 부하 분산 장치)를 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-ilb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="edf37-222">부하 분산 옵션에 대한 자세한 정보는 다음을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="edf37-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="edf37-223">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="edf37-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="edf37-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="edf37-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

