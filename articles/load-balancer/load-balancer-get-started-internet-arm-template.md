---
title: "인터넷 연결 부하 분산 장치 만들기 - Azure 템플릿 | Microsoft Docs"
description: "템플릿을 사용하여 Resource Manager에서 인터넷 연결 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="c68d0-103">템플릿을 사용하여 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="c68d0-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c68d0-104">포털</span><span class="sxs-lookup"><span data-stu-id="c68d0-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="c68d0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c68d0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="c68d0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c68d0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="c68d0-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="c68d0-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c68d0-108">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c68d0-109">또한 [클래식 배포 모델을 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 배울 수 있습니다](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c68d0-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="c68d0-110">클릭하여 배포하는 방식으로 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="c68d0-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="c68d0-111">공용 저장소에서 사용할 수 있는 샘플 템플릿은 위에 설명된 시나리오를 생성하는 데 사용된 기본값을 포함하는 매개 변수 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="c68d0-112">클릭하여 배포하는 방식으로 이 템플릿을 배포하려면 [이 링크](http://go.microsoft.com/fwlink/?LinkId=544801)에 따라 **Azure에 배포**를 클릭하고 필요한 경우 기본 매개 변수 값을 대체하고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="c68d0-113">PowerShell을 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="c68d0-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="c68d0-114">PowerShell을 사용하여 다운로드한 템플릿을 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="c68d0-115">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하고 지침을 끝까지 따르면서 Azure에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="c68d0-116">**New-AzureRmResourceGroupDeployment** cmdlet을 실행하고 템플릿을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="c68d0-117">Azure CLI를 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="c68d0-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="c68d0-118">Azure CLI를 사용하여 템플릿을 배포하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c68d0-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="c68d0-119">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c68d0-120">아래와 같이 **azure config mode** 명령을 실행하여 Resource Manager 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c68d0-121">다음은 위의 명령에 대해 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c68d0-122">브라우저에서 [빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)으로 이동하고 json 파일의 내용을 복사하여 컴퓨터에 새 파일로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="c68d0-123">이 시나리오의 경우 아래 값을 **c:\lb\azuredeploy.parameters.json**이라는 파일로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="c68d0-124">위에서 다운로드하여 수정한 템플릿과 매개 변수 파일로 **azure group deployment create** cmdlet을 실행하여 새 부하 분산 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c68d0-125">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c68d0-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="c68d0-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c68d0-126">Next steps</span></span>

[<span data-ttu-id="c68d0-127">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="c68d0-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c68d0-128">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="c68d0-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c68d0-129">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c68d0-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
