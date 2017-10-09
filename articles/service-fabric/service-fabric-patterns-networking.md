---
title: "Azure Service Fabric에 대 한 aaaNetworking 패턴 | Microsoft Docs"
description: "서비스 패브릭에 대 한 일반적인 네트워킹 패턴에 설명 하 고 어떻게 toocreate Azure 네트워킹 기능을 사용 하 여 클러스터 합니다."
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
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="bf021-103">Service Fabric 네트워킹 패턴</span><span class="sxs-lookup"><span data-stu-id="bf021-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="bf021-104">다른 Azure 네트워킹 기능으로 Azure Service Fabric 클러스터를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="bf021-105">이 문서에서는 보여줍니다 어떻게 toocreate 클러스터를 사용 하 여 hello 같은 기능:</span><span class="sxs-lookup"><span data-stu-id="bf021-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="bf021-106">기존 가상 네트워크 또는 서브넷</span><span class="sxs-lookup"><span data-stu-id="bf021-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="bf021-107">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="bf021-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="bf021-108">내부 전용 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf021-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="bf021-109">내부 및 외부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf021-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="bf021-110">Service Fabric은 표준 가상 컴퓨터 확장 집합에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="bf021-111">가상 컴퓨터 확장 집합에서 사용할 수 있는 모든 기능을 Service Fabric 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="bf021-112">서비스 패브릭 및 가상 컴퓨터 크기 집합에 대 한 hello Azure 리소스 관리자 템플릿의 네트워킹 섹션 hello와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="bf021-113">다른 쉽게 tooincorporate tooan 기존 가상 네트워크를 배포한 후에 네트워킹 Azure express 경로, Azure VPN 게이트웨이, 네트워크 보안 그룹 및 가상 네트워크 피어 링 같은 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="bf021-114">Service Fabric은 한 가지 측면에서 다른 네트워킹 기능과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="bf021-115">hello [Azure 포털](https://portal.azure.com) 내부적으로 사용 하 여 hello 서비스 패브릭 리소스 공급자 toocall tooa 클러스터 tooget 정보 노드 및 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="bf021-116">서비스 패브릭 리소스 공급자 hello hello 관리 끝점에 대 한 인바운드 액세스 공개적으로 액세스할 수 있는 toohello HTTP 게이트웨이 포트 (포트 19080, 기본적으로) 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="bf021-117">[서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 사용 하 여 hello 관리 끝점 toomanage 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="bf021-118">또한 hello 서비스 패브릭 리소스 공급자 toodisplay hello Azure 포털에서에서 클러스터에 대 한이 포트 tooquery 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="bf021-119">메시지와 같은 포트 19080 hello 서비스 패브릭 리소스 공급자에서 액세스할 수 없는 경우 *노드를 찾을 수 없습니다* hello 포털에 표시 및 노드 및 응용 프로그램 목록을 빈 상태로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="bf021-120">Toosee hello Azure 포털에서에서 클러스터를, 부하 분산 장치는 공용 IP 주소를 노출 해야 하 고 네트워크 보안 그룹에는 들어오는 포트 19080 트래픽을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="bf021-121">설치 프로그램에서 이러한 요구 사항에 맞지 않으면 hello Azure 포털 클러스터의 hello 상태를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="bf021-122">템플릿</span><span class="sxs-lookup"><span data-stu-id="bf021-122">Templates</span></span>

<span data-ttu-id="bf021-123">모든 Service Fabric 템플릿은 [하나의 다운로드 파일](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="bf021-124">있어야 수 toodeploy hello 템플릿을으로-hello 다음 PowerShell 명령을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="bf021-125">Hello를 먼저 읽어 기존 Azure 가상 네트워크 템플릿이나 hello 고정 공용 IP 서식 파일을 배포 하는 경우 hello [설치 초기](#initialsetup) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="bf021-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="bf021-126">초기 설치</span><span class="sxs-lookup"><span data-stu-id="bf021-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="bf021-127">기존 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="bf021-127">Existing virtual network</span></span>

<span data-ttu-id="bf021-128">다음 예제는 hello에서 hello에 ExistingRG vnet을 명명 된 기존 가상 네트워크와 시작 **ExistingRG** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="bf021-129">hello 서브넷의 기본을 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-129">hello subnet is named default.</span></span> <span data-ttu-id="bf021-130">이러한 기본 리소스는 hello Azure 포털 toocreate 표준 가상 컴퓨터 (VM)를 사용 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="bf021-131">Hello VM을 만들지 않고 hello 가상 네트워크 및 서브넷을 만들 수 있지만 클러스터 tooan 기존 가상 네트워크를 추가 하는 hello 주요 목표는 tooprovide 네트워크 연결 tooother Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="bf021-132">VM 만들기 hello 기존 가상 네트워크는 일반적으로 사용 방법의 좋은 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="bf021-133">서비스 패브릭 클러스터를만 내부 부하 분산 장치, 없이 공용 IP 주소를 사용 하는 경우 사용할 수 있습니다 VM과 해당 공용 IP는 보안으로 hello *상자 점프*합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="bf021-134">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="bf021-134">Static public IP address</span></span>

<span data-ttu-id="bf021-135">고정 공용 IP 주소는 일반적으로 VM 또는 Vm에 할당 된 hello에서 별도로 관리 되는 전용된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="bf021-136">(것과 반대로 tooin hello 서비스 패브릭 클러스터 리소스 그룹으로 자체) 전용된 네트워킹 리소스 그룹에 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="bf021-137">Hello에 staticIP1 라는 고정 공용 IP 주소 만들기 같은 ExistingRG 리소스 그룹 hello Azure 포털에서에서 또는 PowerShell을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="bf021-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="bf021-138">Service Fabric 템플릿</span><span class="sxs-lookup"><span data-stu-id="bf021-138">Service Fabric template</span></span>

<span data-ttu-id="bf021-139">이 문서의 예제 hello 사용 하 여 hello 서비스 패브릭 template.json 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="bf021-140">클러스터를 만들기 전에 hello 표준 포털 마법사 toodownload hello hello 포털에서 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="bf021-141">사용할 수도 있습니다 hello 템플릿 중 하나에 hello [템플릿 갤러리](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), hello 같은 [다섯 개 노드 서비스 패브릭 클러스터](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="bf021-142">기존 가상 네트워크 또는 서브넷</span><span class="sxs-lookup"><span data-stu-id="bf021-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="bf021-143">다음 두 개의 새 매개 변수 tooreference hello 기존 가상 네트워크를 추가 하 고 hello 기존 서브넷의 hello 서브넷 매개 변수 toohello 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

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


2. <span data-ttu-id="bf021-144">변경 hello `vnetID` 변수 toopoint toohello 기존 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="bf021-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="bf021-145">Azure에서 새 가상 네트워크를 만들지 않도록 리소스에서 `Microsoft.Network/virtualNetworks`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="bf021-146">Hello에서 가상 네트워크의 hello 주석 `dependsOn` 특성 `Microsoft.Compute/virtualMachineScaleSets`새 가상 네트워크를 만드는 방법에 의존 하지 않으므로:</span><span class="sxs-lookup"><span data-stu-id="bf021-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="bf021-147">Hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="bf021-148">배포 후 가상 네트워크가 포함 되어야 hello 새 크기 집합 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="bf021-149">hello 기존 가상 네트워크 및 서브넷 hello 가상 컴퓨터 조정 집합 노드 유형이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="bf021-150">또한 프로토콜 RDP (원격 데스크톱) tooaccess hello hello 가상 네트워크에 이미 있던 VM을 사용할 수 있으며 tooping hello에 대 한 새 크기 집합 Vm:</span><span class="sxs-lookup"><span data-stu-id="bf021-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="bf021-151">또 다른 예에 대 한 참조 [이름이 아닌 특정 tooService 패브릭](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="bf021-152">고정 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="bf021-152">Static public IP address</span></span>

1. <span data-ttu-id="bf021-153">고정 IP 리소스 그룹, 이름 및 정규화 된 도메인 이름 (FQDN)을 기존 hello hello 이름에 대 한 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="bf021-154">Hello 제거 `dnsName` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="bf021-155">(hello 고정 IP 주소에 이미 하나 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="bf021-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="bf021-156">변수 tooreference hello 기존의 고정 IP 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="bf021-157">Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="bf021-158">Hello에서 IP 주소 hello 주석 `dependsOn` 특성 `Microsoft.Network/loadBalancers`새 IP 주소를 만드는 방법에 의존 하지 않으므로:</span><span class="sxs-lookup"><span data-stu-id="bf021-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="bf021-159">Hello에 `Microsoft.Network/loadBalancers` 리소스, 변경 hello `publicIPAddress` 요소의 `frontendIPConfigurations` tooreference hello 새로 만든 대신 기존의 고정 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="bf021-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="bf021-160">Hello에 `Microsoft.ServiceFabric/clusters` 리소스를 변경 `managementEndpoint` toohello DNS FQDN hello 고정 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="bf021-161">보안 클러스터를 사용 하는 경우 반드시 변경 해야 *http://* 너무*https://*합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="bf021-162">(Note는이 단계는 tooService 패브릭 클러스터에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="bf021-163">가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="bf021-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="bf021-164">Hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="bf021-165">배포 후 볼 수 있습니다 프로그램 부하 분산 장치가 바인딩된 toohello 공용 정적 IP 주소를 hello 있는 다른 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="bf021-166">서비스 패브릭 클라이언트 연결 끝점 hello 및 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 끝점 지점 toohello DNS FQDN hello 고정 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="bf021-167">내부 전용 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf021-167">Internal-only load balancer</span></span>

<span data-ttu-id="bf021-168">이 시나리오는 내부 전용 부하 분산 장치 hello 기본 서비스 패브릭 템플릿 hello 외부 부하 분산 장치를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="bf021-169">Hello 서비스 패브릭 리소스 공급자 및 hello Azure 포털에 대 한 의미를 hello 앞 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bf021-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="bf021-170">Hello 제거 `dnsName` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="bf021-171">(필수는 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="bf021-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="bf021-172">경우에 따라 고정 할당 방법을 사용할 때 고정 IP 주소 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="bf021-173">동적 할당 방법을 사용 하는 경우 불필요 toodo이이 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="bf021-174">Azure에서 새 IP 주소를 만들지 않도록 리소스에서 `Microsoft.Network/publicIPAddresses`를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="bf021-175">Hello IP 주소를 제거 `dependsOn` 특성 `Microsoft.Network/loadBalancers`새 IP 주소를 만드는 방법에 의존 하지 않으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="bf021-176">Hello 가상 네트워크 추가 `dependsOn` hello 부하 분산 장치는 이제 hello 가상 네트워크에서 서브넷 hello에 의존 하기 때문에 특성:</span><span class="sxs-lookup"><span data-stu-id="bf021-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

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

5. <span data-ttu-id="bf021-177">Hello 부하 분산 장치의 변경 `frontendIPConfigurations` 사용 하 여 설정 된 `publicIPAddress`, toousing 서브넷 및 `privateIPAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="bf021-178">`privateIPAddress`에서는 미리 정의된 고정 내부 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="bf021-179">동적 IP 주소를 toouse 제거 hello `privateIPAddress` 요소를 한 다음 `privateIPAllocationMethod` 너무**동적**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

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

6. <span data-ttu-id="bf021-180">Hello에 `Microsoft.ServiceFabric/clusters` 리소스를 변경 `managementEndpoint` toopoint toohello 내부 부하 분산 장치 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="bf021-181">보안 클러스터를 사용 하는 경우 반드시 변경 해야 *http://* 너무*https://*합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="bf021-182">(Note는이 단계는 tooService 패브릭 클러스터에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="bf021-183">가상 컴퓨터 확장 집합을 사용하는 경우에는 이 단계를 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="bf021-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="bf021-184">Hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="bf021-185">부하 분산 장치 배포 후 hello 정적 10.0.0.250 개인 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="bf021-186">동일한 가상 네트워크의 다른 컴퓨터가 있는 경우에 내부 toohello을 이동할 수 있습니다 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="bf021-187">Tooone hello 부하 분산 장치 뒤 hello 노드를 연결 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="bf021-188">내부 및 외부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf021-188">Internal and external load balancer</span></span>

<span data-ttu-id="bf021-189">이 시나리오에서는 시작 hello 기존 단일 노드 형식 외부 부하 분산 장치를 추가 하는 hello에 대 한 내부 부하 분산 장치는 형식이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="bf021-190">연결 하는 백 엔드 포트 tooa 백 엔드 주소 풀만 tooa 단일 부하 분산 장치를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="bf021-191">응용 프로그램 포트를 포함할 부하 분산 장치 및 관리 끝점을 포함할 부하 분산 장치를 선택합니다(포트 19000 및 19080).</span><span class="sxs-lookup"><span data-stu-id="bf021-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="bf021-192">Hello 내부 부하 분산 장치에 hello 관리 끝점을 설정 하는 경우 유의 hello에 서비스 패브릭 리소스 공급자 제한은 유지 hello 문서의 앞부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="bf021-193">예에서 hello 사용 하 여 hello 관리 끝점 hello 외부 부하 분산 장치에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="bf021-194">또한 포트 80 응용 프로그램 포트를 추가 하 고 hello 내부 부하 분산 장치에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="bf021-195">노드 형식 두 클러스터의 노드 유형의 hello 외부 부하 분산 장치에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="bf021-196">hello 다른 노드 형식에 있는 경우 hello 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bf021-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="bf021-197">hello 포털에서 만든 두 노드 형식 서식 파일 (이 두 가지 부하 분산 장치 함께 제공)에 있는 두 노드 형식 클러스터 toouse hello 두 번째 부하 분산 장치 tooan 내부 부하 분산 장치를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="bf021-198">자세한 내용은 참조 hello [내부 전용 부하 분산 장치](#internallb) 섹션.</span><span class="sxs-lookup"><span data-stu-id="bf021-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="bf021-199">Hello 정적 내부 부하 분산 장치 IP 주소 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="bf021-200">(Toousing 동적 IP 주소를 관련된 정보,이 문서의 이전 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="bf021-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="bf021-201">응용 프로그램 포트 80 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="bf021-202">hello 기존 tooadd 내부 버전 복사 하 고, 붙여 넣고, 추가 변수 네트워킹 "-Int" toohello 이름:</span><span class="sxs-lookup"><span data-stu-id="bf021-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

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

4. <span data-ttu-id="bf021-203">AppPort1 hello 기본 포털 템플릿을 추가 하는 응용 프로그램 포트 80을 사용 하는 hello 포털에서 생성 된 템플릿을 사용 하 여 시작 하는 경우 (포트 80) hello 외부 부하 분산 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="bf021-204">이 경우 AppPort1 hello 외부 부하 분산 장치에서 제거 `loadBalancingRules` 및 프로브를 있으므로 toohello 내부 부하 분산 장치를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

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
        } /* Remove AppPort1 from hello external load balancer.
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
        } /* Remove AppPort1 from hello external load balancer.
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

5. <span data-ttu-id="bf021-205">두 번째 `Microsoft.Network/loadBalancers` 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="bf021-206">Hello에 생성 된 유사한 toohello 내부 부하 분산 장치 검색 [내부 전용 부하 분산 장치](#internallb) hello를 사용 하 여 하지만 섹션 "-Int" 부하 분산 장치 변수 및 구현만 hello 응용 프로그램 포트 80입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="bf021-207">이 제거 `inboundNatPools`, hello 공용 부하 분산 장치에 tookeep RDP 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="bf021-208">Hello 내부 부하 분산 장치에 RDP 하려는 경우 이동 `inboundNatPools` hello 외부 부하 분산 장치 toothis 내부에서 부하 분산 장치:</span><span class="sxs-lookup"><span data-stu-id="bf021-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
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
                                /* Switch from Public tooPrivate IP address
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
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
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
                    /* Add hello probe for hello app port. */
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

6. <span data-ttu-id="bf021-209">`networkProfile` hello에 대 한 `Microsoft.Compute/virtualMachineScaleSets` 리소스를 hello 내부 백 엔드 주소 풀을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

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

7. <span data-ttu-id="bf021-210">Hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="bf021-211">배포 후 hello 리소스 그룹에 두 개의 부하 분산 장치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="bf021-212">Hello 부하 분산 장치를 찾을 때는 hello 공용 IP 주소 및 관리 끝점 (포트 19000 및 19080) 할당 toohello 공용 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="bf021-213">Hello 정적 내부 IP 주소와 응용 프로그램 끝점 (포트 80)가 할당 된 toohello 내부 볼 수 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="bf021-214">부하 분산 장치 사용 하 여 hello 동일한 가상 컴퓨터 크기 집합 백 엔드 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="bf021-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf021-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf021-215">Next steps</span></span>
[<span data-ttu-id="bf021-216">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="bf021-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
