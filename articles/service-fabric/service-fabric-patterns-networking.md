---
title: "Azure Service Fabric의 네트워킹 패턴 | Microsoft Docs"
description: "Service Fabric에 대한 일반적인 네트워킹 패턴과 Azure 네트워킹 기능을 사용하여 클러스터를 만드는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="db690-103">Service Fabric 네트워킹 패턴</span><span class="sxs-lookup"><span data-stu-id="db690-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="db690-104">다른 Azure 네트워킹 기능으로 Azure Service Fabric 클러스터를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="db690-105">이 문서에서는 다음과 같은 기능을 사용하여 클러스터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db690-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="db690-106">기존 가상 네트워크 또는 서브넷</span><span class="sxs-lookup"><span data-stu-id="db690-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="db690-107">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="db690-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="db690-108">내부 전용 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="db690-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="db690-109">내부 및 외부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="db690-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="db690-110">Service Fabric은 표준 가상 컴퓨터 확장 집합에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="db690-111">가상 컴퓨터 확장 집합에서 사용할 수 있는 모든 기능을 Service Fabric 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="db690-112">가상 컴퓨터 확장 집합 및 Service Fabric에 대한 Azure Resource Manager 템플릿의 네트워킹 섹션은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="db690-113">기존 가상 네트워크에 배포한 후 Azure ExpressRoute, Azure VPN Gateway, 네트워크 보안 그룹 및 가상 네트워크의 피어링 등의 다른 네트워킹 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="db690-114">Service Fabric은 한 가지 측면에서 다른 네트워킹 기능과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="db690-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="db690-115">[Azure Portal](https://portal.azure.com)이 내부적으로 SFRP(Service Fabric 리소스 공급자)를 사용하여 노드 및 응용 프로그램에 대한 정보를 얻기 위해 클러스터를 호출한다는 것이 바로 그것입니다.</span><span class="sxs-lookup"><span data-stu-id="db690-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="db690-116">Service Fabric 리소스 공급자는 관리 끝점에서 HTTP 게이트웨이 포트(기본적으로 19080)에 대해 공개적으로 액세스 가능한 인바운드 액세스 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="db690-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 관리 끝점을 사용하여 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="db690-118">또한 Service Fabric 리소스 공급자는 Azure Portal에 표시하기 위해 클러스터에 대한 정보를 쿼리하는 데도 이 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="db690-119">Service Fabric 리소스 공급자에서 포트 19080에 액세스할 수 없으면 포털에 *노드를 찾을 수 없음* 메시지가 표시되고 노드 및 응용 프로그램 목록이 빈 상태로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="db690-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="db690-120">Azure Portal에서 클러스터를 보려는 경우 부하 분산 장치가 공용 IP 주소를 노출해야 하고 네트워크 보안 그룹은 들어오는 포트 19080 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="db690-121">설정이 이러한 요구 사항을 충족하지 않는 경우 Azure Portal에 클러스터의 상태가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="db690-122">템플릿</span><span class="sxs-lookup"><span data-stu-id="db690-122">Templates</span></span>

<span data-ttu-id="db690-123">모든 Service Fabric 템플릿은 [하나의 다운로드 파일](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="db690-124">다음 PowerShell 명령을 사용하여 템플릿을 있는 그대로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="db690-125">기존 Azure Virtual Network 템플릿 또는 고정 공용 IP 템플릿을 배포하는 경우 먼저 이 문서의 [초기 설치](#initialsetup) 섹션을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="db690-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="db690-126">초기 설치</span><span class="sxs-lookup"><span data-stu-id="db690-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="db690-127">기존 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="db690-127">Existing virtual network</span></span>

<span data-ttu-id="db690-128">다음 예제에서는 **ExistingRG** 리소스 그룹에 ExistingRG-vnet이라는 기존 가상 네트워크로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="db690-129">서브넷의 이름은 default입니다.</span><span class="sxs-lookup"><span data-stu-id="db690-129">The subnet is named default.</span></span> <span data-ttu-id="db690-130">이러한 기본 리소스는 Azure Portal을 사용하여 표준 VM(가상 컴퓨터)을 만들 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db690-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="db690-131">VM을 만들지 않고 가상 네트워크 및 서브넷을 만들 수 있지만 기존 가상 네트워크에 클러스터를 추가하는 주요 목표는 다른 VM에 대한 네트워크 연결을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db690-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="db690-132">VM을 만드는 작업은 기존 가상 네트워크가 일반적으로 사용되는 방식의 좋은 예제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="db690-133">Service Fabric 클러스터가 공용 IP 주소 없이 내부 부하 분산 장치만 사용하는 경우 VM 및 해당 공용 IP를 보안 *점프 서버*로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="db690-134">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="db690-134">Static public IP address</span></span>

<span data-ttu-id="db690-135">고정 공용 IP 주소는 일반적으로 할당된 VM과는 별도로 관리되는 전용 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="db690-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="db690-136">Service Fabric 클러스터 리소스 그룹 자체와는 달리 전용 네트워킹 리소스 그룹에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="db690-137">Azure Portal 또는 Powershell을 통해 동일한 ExistingRG 리소스 그룹에 이름이 staticIP1인 고정 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db690-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="db690-138">Service Fabric 템플릿</span><span class="sxs-lookup"><span data-stu-id="db690-138">Service Fabric template</span></span>

<span data-ttu-id="db690-139">이 문서의 예제에서는 Service Fabric template.json을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="db690-140">클러스터를 만들기 전에 표준 포털 마법사를 사용하여 포털에서 템플릿을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="db690-141">[템플릿 갤러리](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric)에서 [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)와 같은 템플릿 하나를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="db690-142">기존 가상 네트워크 또는 서브넷</span><span class="sxs-lookup"><span data-stu-id="db690-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="db690-143">서브넷 매개 변수를 기존 서브넷의 이름으로 변경하고 기존 가상 네트워크를 참조하는 두 개의 새 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="db690-144">`vnetID` 변수를 기존 가상 네트워크를 가리키도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="db690-145">Azure에서 새 가상 네트워크를 만들지 않도록 리소스에서 `Microsoft.Network/virtualNetworks`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="db690-146">새 가상 네트워크를 만드는 데만 의존하지 않도록 `Microsoft.Compute/virtualMachineScaleSets`의 `dependsOn` 특성에서 가상 네트워크를 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="db690-147">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="db690-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="db690-148">배포 후 가상 네트워크에는 새 확장 집합 VM이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="db690-149">가상 네트워크 확장 집합 노드 형식은 기존 가상 네트워크 및 서브넷을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="db690-150">또한 RDP(원격 데스크톱 프로토콜 )를 사용하여 가상 네트워크에 이미 있던 VM에 액세스하고 새 확장 집합 VM을 Ping할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="db690-151">또 다른 예제를 보려면 [Service Fabric에 국한되지 않는 항목](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db690-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="db690-152">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="db690-152">Static public IP address</span></span>

1. <span data-ttu-id="db690-153">기존 고정 IP 리소스 그룹의 이름 및 FQDN(정규화된 도메인 이름)에 대한 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="db690-154">`dnsName` 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="db690-155">(고정 IP 주소에 매개 변수가 이미 하나 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="db690-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="db690-156">기존 고정 IP를 참조하는 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="db690-157">Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="db690-158">새 IP 주소를 만드는 데만 의존하지 않도록 `Microsoft.Network/loadBalancers`의 `dependsOn` 특성에서 IP 주소를 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="db690-159">`Microsoft.Network/loadBalancers` 리소스에서 새로 만든 IP 주소가 아닌 기존의 고정 IP 주소를 참조하도록 `frontendIPConfigurations`의 `publicIPAddress` 요소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="db690-160">`Microsoft.ServiceFabric/clusters` 리소스에서 `managementEndpoint`를 고정 IP 주소의 DNS FQDN으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="db690-161">보안 클러스터를 사용하는 경우 *http://*를 *https://*로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="db690-162">(이 단계는 Service Fabric 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="db690-163">가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="db690-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="db690-164">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="db690-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="db690-165">배포 후에는 부하 분산 장치가 다른 리소스 그룹의 공용 고정 IP 주소에 바인딩된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="db690-166">Service Fabric 클라이언트 연결 끝점 및 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 끝점은 고정 IP 주소의 DNS FQDN을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="db690-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="db690-167">내부 전용 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="db690-167">Internal-only load balancer</span></span>

<span data-ttu-id="db690-168">이 시나리오에서는 기본 Service Fabric 템플릿의 외부 부하 분산 장치를 내부 전용 부하 분산 장치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db690-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="db690-169">Azure Portal 및 Service Fabric 리소스 공급자의 의미에 대해서는 이전 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="db690-170">`dnsName` 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="db690-171">(필수는 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="db690-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="db690-172">경우에 따라 고정 할당 방법을 사용할 때 고정 IP 주소 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="db690-173">동적 할당 방법을 사용하는 경우 이 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="db690-174">Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="db690-175">새 IP 주소를 만드는 데만 의존하지 않도록 `Microsoft.Network/loadBalancers`의 IP 주소 `dependsOn` 특성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="db690-176">이제 부하 분산 장치는 가상 네트워크의 서브넷에 의존하므로 가상 네트워크 `dependsOn` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="db690-177">부하 분산 장치의 `frontendIPConfigurations` 설정을 `publicIPAddress`를 사용하는 방식에서 서브넷 및 `privateIPAddress`를 사용하는 방식으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="db690-178">`privateIPAddress`에서는 미리 정의된 고정 내부 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="db690-179">동적 IP 주소를 사용하려면 `privateIPAddress` 요소를 제거한 다음 `privateIPAllocationMethod`를 **Dynamic**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="db690-180">`Microsoft.ServiceFabric/clusters` 리소스에서 내부 부하 분산 장치 주소를 가리키도록 `managementEndpoint`를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="db690-181">보안 클러스터를 사용하는 경우 *http://*를 *https://*로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="db690-182">(이 단계는 Service Fabric 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="db690-183">가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="db690-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="db690-184">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="db690-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="db690-185">배포 후에 부하 분산 장치는 개인 정적 10.0.0.250 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="db690-186">동일한 가상 네트워크에 다른 컴퓨터가 있는 경우 내부 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 끝점으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="db690-187">부하 분산 장치 뒤의 노드 중 하나로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="db690-188">내부 및 외부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="db690-188">Internal and external load balancer</span></span>

<span data-ttu-id="db690-189">이 시나리오는 기존 단일 노드 형식 외부 부하 분산 장치로 시작하고 동일한 노드 형식에 대한 내부 부하 분산 장치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="db690-190">백 엔드 주소 풀에 연결된 백 엔드 포트는 단일 부하 분산 장치에만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="db690-191">응용 프로그램 포트를 포함할 부하 분산 장치 및 관리 끝점을 포함할 부하 분산 장치를 선택합니다(포트 19000 및 19080).</span><span class="sxs-lookup"><span data-stu-id="db690-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="db690-192">내부 부하 분산 장치에 관리 끝점을 둘 경우 이 문서 앞부분에서 제시된 Service Fabric 리소스 공급자 제한 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="db690-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="db690-193">사용하는 예제에서 관리 끝점은 외부 부하 분산 장치에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="db690-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="db690-194">또한 포트 80을 응용 프로그램 포트에 추가한 후 내부 부하 분산 장치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="db690-195">두 노드 형식 클러스터에서 한 노드 형식은 외부 부하 분산 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="db690-196">다른 노드 형식은 내부 부하 분산 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="db690-197">두 노드 형식 클러스터를 사용하려면 포털에서 만들어진 두 노드 형식 템플릿(두 가지 부하 분산 장치와 함께 제공)에서 두 번째 부하 분산 장치를 내부 부하 분산 장치로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="db690-198">자세한 내용은 [내부 전용 부하 분산 장치](#internallb) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db690-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="db690-199">고정 내부 부하 분산 장치 IP 주소 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="db690-200">(동적 IP 주소 사용과 관련된 내용은 이 문서 이전 섹션을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="db690-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="db690-201">응용 프로그램 포트 80 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="db690-202">기존 네트워킹 변수의 내부 버전을 추가하려면 복사한 후 붙여 넣고 이름에 "-Int"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="db690-203">응용 프로그램 포트 80을 사용하는 포털에서 생성된 템플릿으로 시작하는 경우 기본 포털 템플릿은 외부 부하 분산 장치에 AppPort1(포트 80)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="db690-204">이 경우 외부 부하 분산 장치 `loadBalancingRules` 및 프로브에서 AppPort1을 제거하여 내부 부하 분산 장치에 추가할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="db690-205">두 번째 `Microsoft.Network/loadBalancers` 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="db690-206">[내부 전용 부하 분산 장치](#internallb) 섹션에서 만든 내부 부하 분산 장치와 비슷해 보이지만 "-Int" 부하 분산 장치 변수를 사용하고 응용 프로그램 포트 80만 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="db690-207">또한 `inboundNatPools`를 제거하여 RDP 끝점을 공용 부하 분산 장치에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="db690-208">내부 부하 분산 장치의 RDP를 원할 경우 외부 부하 분산 장치의 `inboundNatPools`를 이 내부 부하 분산 장치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public to Private IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add the probe for the app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="db690-209">`Microsoft.Compute/virtualMachineScaleSets` 리소스에 대한 `networkProfile`에서 내부 백 엔드 주소 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="db690-210">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="db690-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="db690-211">배포 후 리소스 그룹에서 두 개의 부하 분산 장치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="db690-212">부하 분산 장치를 찾아보면 공용 IP 주소와 공용 IP 주소에 할당된 관리 끝점(포트 19000 및 19080)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="db690-213">또한 고정 내부 IP 주소와 내부 부하 분산 장치에 할당된 응용 프로그램 끝점(포트 80)도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db690-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="db690-214">두 부하 분산 장치 모두 동일한 가상 컴퓨터 확장 집합 백 엔드 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db690-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db690-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db690-215">Next steps</span></span>
[<span data-ttu-id="db690-216">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="db690-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
