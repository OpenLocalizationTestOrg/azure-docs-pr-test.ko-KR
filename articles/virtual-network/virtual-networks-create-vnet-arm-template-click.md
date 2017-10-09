---
title: "가상 네트워크 aaaCreate | Azure 리소스 관리자 템플릿 | Microsoft Docs"
description: "가상 a toocreate Azure 리소스 관리자 템플릿을 사용 하 여 네트워크 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="99142-103">Azure Resource Manager 템플릿을 사용하여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="99142-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="99142-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="99142-105">Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="99142-106">hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="99142-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="99142-107">이 문서에서는 Azure 리소스 관리자 템플릿을 사용 하 여 toocreate hello 리소스 관리자 배포를 통해 VNet을 모델링 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="99142-108">리소스 관리자를 통해 다른 도구를 사용 하 여 VNet을 만들 하거나 hello 다음 목록에서에서 다른 옵션을 선택 하 여 hello 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="99142-109">포털</span><span class="sxs-lookup"><span data-stu-id="99142-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="99142-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99142-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="99142-111">CLI</span><span class="sxs-lookup"><span data-stu-id="99142-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="99142-112">템플릿</span><span class="sxs-lookup"><span data-stu-id="99142-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="99142-113">포털(클래식)</span><span class="sxs-lookup"><span data-stu-id="99142-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="99142-114">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="99142-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="99142-115">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="99142-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="99142-116">에 대해 설명 합니다 방법을 toodownload 수정 및 ARM 템플릿을 GitHub에서 기존 및 GitHub, PowerShell 및 Azure CLI hello hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="99142-117">단순히 hello ARM 템플릿을 변경 하지 않고 GitHub에서 직접 배포 하는 경우 너무 건너뛸[github에서 서식 파일을 배포](#deploy-the-arm-template-by-using-click-to-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="99142-118">다운로드 하 고 hello Azure 리소스 관리자 서식 파일 이해</span><span class="sxs-lookup"><span data-stu-id="99142-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="99142-119">GitHub에서 VNet 및 서브넷 2 개를 만들기 위한 hello 기존 서식 파일을 다운로드, 변경 수도, 있으며 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="99142-120">따라서 toodo hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="99142-121">너무 이동[hello 샘플 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="99142-122">**azuredeploy.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="99142-123">컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="99142-124">서식 파일에 익숙한 경우 7 toostep를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="99142-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="99142-125">방금 저장 한 hello 파일을 열고 아래 hello 내용을 확인 **매개 변수** 줄 5에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="99142-126">ARM 템플릿 매개 변수는 배포하는 동안 채울 수 있는 값에 대한 자리 표시자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="99142-127">매개 변수</span><span class="sxs-lookup"><span data-stu-id="99142-127">Parameter</span></span> | <span data-ttu-id="99142-128">설명</span><span class="sxs-lookup"><span data-stu-id="99142-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="99142-129">**위치**</span><span class="sxs-lookup"><span data-stu-id="99142-129">**location**</span></span> |<span data-ttu-id="99142-130">Azure 지역 VNet hello를 만들 위치</span><span class="sxs-lookup"><span data-stu-id="99142-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="99142-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="99142-131">**vnetName**</span></span> |<span data-ttu-id="99142-132">Hello에 대 한 이름을 새 VNet</span><span class="sxs-lookup"><span data-stu-id="99142-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="99142-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="99142-133">**addressPrefix**</span></span> |<span data-ttu-id="99142-134">주소 공간 CIDR 형식에서 VNet hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="99142-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="99142-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="99142-135">**subnet1Name**</span></span> |<span data-ttu-id="99142-136">이름 hello에 대 한 첫 번째 VNet</span><span class="sxs-lookup"><span data-stu-id="99142-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="99142-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="99142-137">**subnet1Prefix**</span></span> |<span data-ttu-id="99142-138">Hello 첫 번째 서브넷에 대 한 CIDR 블록</span><span class="sxs-lookup"><span data-stu-id="99142-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="99142-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="99142-139">**subnet2Name**</span></span> |<span data-ttu-id="99142-140">Hello에 대 한 이름을 VNet의 두 번째</span><span class="sxs-lookup"><span data-stu-id="99142-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="99142-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="99142-141">**subnet2Prefix**</span></span> |<span data-ttu-id="99142-142">Hello 두 번째 서브넷에 대 한 CIDR 블록</span><span class="sxs-lookup"><span data-stu-id="99142-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="99142-143">GitHub에서 유지 관리되는 Azure 리소스 관리자 템플릿은 시간이 지나면서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="99142-144">사용 하기 전에 hello 서식 파일을 확인 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="99142-145">Hello 내용을 확인 **리소스** hello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="99142-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="99142-146">**type**.</span></span> <span data-ttu-id="99142-147">Hello 템플릿으로 생성 되는 리소스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="99142-148">이 경우 VNet를 나타내는 **Microsoft.Network/virtualNetworks**입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="99142-149">**이름**.</span><span class="sxs-lookup"><span data-stu-id="99142-149">**name**.</span></span> <span data-ttu-id="99142-150">Hello 리소스에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-150">Name for hello resource.</span></span> <span data-ttu-id="99142-151">공지 hello 사용 **[parameters('vnetName')]**, 어떤 의미 hello hello 사용자 또는 매개 변수 파일에서 배포 중 입력으로 제공 하는 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99142-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="99142-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="99142-152">**properties**.</span></span> <span data-ttu-id="99142-153">Hello 리소스에 대 한 속성 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-153">List of properties for hello resource.</span></span> <span data-ttu-id="99142-154">이 템플릿은 VNet 만드는 동안 hello 주소 공간 및 서브넷 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="99142-155">너무 탐색[hello 샘플 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="99142-156">**azuredeploy-paremeters.json**을 클릭하고 **RAW**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="99142-157">컴퓨터에 hello 파일 tooa 로컬 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="99142-158">방금 저장 한 hello 파일을 열고 hello hello 매개 변수 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="99142-159">다음 toodeploy hello hello 시나리오에 설명 된 VNet 아래의 값에는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="99142-160">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="99142-161">PowerShell을 사용 하 여 hello 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="99142-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="99142-162">다음 PowerShell을 사용 하 여 다운로드 한 단계 toodeploy hello 템플릿을 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="99142-163">PowerShell 설치 및 구성 Azure hello의 hello 단계를 완료 하 여 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 문서.</span><span class="sxs-lookup"><span data-stu-id="99142-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="99142-164">다음 명령은 toocreate hello 새 리소스 그룹을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="99142-165">hello 명령은 명명 된 리소스 그룹을 만듭니다 *TestRG* hello에 *중미* azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="99142-166">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99142-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="99142-167">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="99142-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="99142-168">다음 명령을 toodeploy hello hello 템플릿 및 매개 변수 파일 다운로드 하 고 위에서 수정를 사용 하 여 새 VNet hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="99142-169">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="99142-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="99142-170">실행된 hello 다음 명령은 hello의 tooview hello 속성 새 VNet:</span><span class="sxs-lookup"><span data-stu-id="99142-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="99142-171">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="99142-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="99142-172">-배포를 사용 하 여 hello 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="99142-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="99142-173">Microsoft 및 열기 toohello 커뮤니티에서 유지 관리 미리 정의 된 Azure 리소스 관리자 템플릿 업로드 tooa GitHub 리포지토리를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99142-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="99142-174">이러한 템플릿은 GitHub에서 배포할 수 있습니다 또는 다운로드 하 고 수정 toofit 요구 사항.</span><span class="sxs-lookup"><span data-stu-id="99142-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="99142-175">toodeploy 템플릿으로 두 서브넷으로 VNet을 만드는 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="99142-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="99142-176">브라우저에서 탐색 너무[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="99142-177">템플릿 hello 목록 아래로 스크롤하여 클릭 **101 vnet-2 서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="99142-178">Hello 확인 **README.md** 파일을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-178">Check hello **README.md** file, as shown below.</span></span>

    ![Github의 READEME.md 파일](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="99142-180">클릭 **tooAzure 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="99142-181">필요한 경우 Azure 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="99142-182">Hello에 **매개 변수** 블레이드에서 hello 값 toouse toocreate 새 VNet을 클릭 한 다음 입력 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="99142-183">hello 다음 그림과 hello 시나리오에 대 한 hello 값:</span><span class="sxs-lookup"><span data-stu-id="99142-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![ARM 템플릿 매개 변수](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="99142-185">클릭 **리소스 그룹** 선택한 리소스 그룹 tooadd hello VNet, 하거나 클릭 **새로 만들기** tooadd hello VNet tooa 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="99142-186">hello 다음 그림은 hello 리소스 이라는 새 리소스 그룹에 대 한 그룹 설정을 **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="99142-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![리소스 그룹](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="99142-188">필요한 경우 변경할 hello **구독** 및 **위치** VNet에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="99142-189">Hello의 타일로 toosee hello VNet를 하지 않으려면 **시작 보드**, 사용 하지 않도록 설정 **Pin tooStartboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="99142-190">클릭 **약관**hello 조건을 읽고 클릭 **구입** tooagree 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="99142-191">클릭 **만들기** toocreate hello VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Preview 포털에서 배포 타일 제출](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="99142-193">Hello 배포 완료 되 면 hello Azure 포털에서 **더 많은 서비스**, 형식 *가상 네트워크* hello 필터 상자가 표시 되 면 가상 네트워크 toosee hello 가상 네트워크 블레이드 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="99142-194">Hello 블레이드에서 클릭 *TestVNet*합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="99142-195">Hello에 *TestVNet* 블레이드에서 클릭 **서브넷** hello 다음 그림에에서 나와 있는 것 처럼 toosee 만든 hello 서브넷:</span><span class="sxs-lookup"><span data-stu-id="99142-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Preview 포털에서 VNet 만들기](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="99142-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99142-197">Next steps</span></span>

<span data-ttu-id="99142-198">자세한 내용은 방법 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="99142-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="99142-199">읽는 hello 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-hero-tutorial.md) 또는 [Linux VM을 만들](../virtual-machines/linux/quick-create-portal.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="99142-200">Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.</span><span class="sxs-lookup"><span data-stu-id="99142-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="99142-201">hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="99142-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="99142-202">가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크.</span><span class="sxs-lookup"><span data-stu-id="99142-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="99142-203">자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-arm.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="99142-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
