---
title: "내부 부하 분산 장치 만들기 - Azure 템플릿 | Microsoft Docs"
description: "리소스 관리자에서 템플릿을 사용하여 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 5e0278cf5c605298932d6ac55d147a1c43fd9d23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="53c08-103">템플릿을 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="53c08-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53c08-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="53c08-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="53c08-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53c08-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="53c08-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53c08-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="53c08-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="53c08-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="53c08-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="53c08-109">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="53c08-110">클릭하여 배포하는 방식으로 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="53c08-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="53c08-111">공용 저장소에서 사용할 수 있는 샘플 템플릿은 위에 설명된 시나리오를 생성하는 데 사용된 기본값을 포함하는 매개 변수 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="53c08-112">클릭하여 배포하는 방식으로 이 템플릿을 배포하려면 [이 링크](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)에 따라 **Azure에 배포**를 클릭하고 필요한 경우 기본 매개 변수 값을 대체하고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="53c08-113">PowerShell을 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="53c08-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="53c08-114">PowerShell을 사용하여 다운로드한 템플릿을 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="53c08-115">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하고 지침을 끝까지 따르면서 Azure에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="53c08-116">매개 변수 파일을 로컬 디스크에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="53c08-117">파일을 편집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="53c08-118">**New-AzureRmResourceGroupDeployment** cmdlet을 실행하고 템플릿을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="53c08-119">Azure CLI를 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="53c08-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="53c08-120">Azure CLI를 사용하여 템플릿을 배포하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="53c08-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="53c08-121">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="53c08-122">아래와 같이 **azure config mode** 명령을 실행하여 Resource Manager 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="53c08-123">다음은 위의 명령에 대해 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="53c08-124">매개 변수 파일을 열고 해당 내용을 선택한 후 컴퓨터의 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="53c08-125">이 예에서는 매개 변수 파일을 *parameters.json*에 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="53c08-126">위에서 다운로드하여 수정한 템플릿과 매개 변수 파일로 **azure group deployment create** 명령을 실행하여 새 내부 부하 분산 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="53c08-127">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53c08-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="53c08-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53c08-128">Next steps</span></span>

[<span data-ttu-id="53c08-129">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="53c08-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="53c08-130">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="53c08-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

