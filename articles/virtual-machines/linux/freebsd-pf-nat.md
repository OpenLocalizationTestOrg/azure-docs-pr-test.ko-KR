---
title: "Azure에서 FreeBSD 패킷 필터를 사용하여 방화벽 만들기 | Microsoft Docs"
description: "Azure에서 FreeBSD의 PF를 사용하여 NAT 방화벽을 배포하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: cd777291a1321eabf4efe0d7b9b101f932d9398b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-freebsds-packet-filter-to-create-a-secure-firewall-in-azure"></a><span data-ttu-id="1ece2-103">Azure에서 FreeBSD 패킷 필터를 사용하여 보안 방화벽을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1ece2-103">How to use FreeBSD's Packet Filter to create a secure firewall in Azure</span></span>
<span data-ttu-id="1ece2-104">이 문서에서는 일반 웹 서버 시나리오에 대해 Azure Resource Manager 템플릿을 통해 FreeBSD 패킷 필터를 사용하여 NAT 방화벽을 배포하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-104">This article introduces how to deploy a NAT firewall using FreeBSD’s Packer Filter through Azure Resource Manager template for common web server scenario.</span></span>

## <a name="what-is-pf"></a><span data-ttu-id="1ece2-105">PF란?</span><span class="sxs-lookup"><span data-stu-id="1ece2-105">What is PF?</span></span>
<span data-ttu-id="1ece2-106">PF(패킷 필터 또는 pf)는 BSD에서 사용이 허가된 상태 저장 패킷 필터로, 방화벽을 위한 소프트웨어의 핵심 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-106">PF (Packet Filter, also written pf) is a BSD licensed stateful packet filter, a central piece of software for firewalling.</span></span> <span data-ttu-id="1ece2-107">PF는 빠르게 발전해 왔으며 현재 사용 가능한 다른 방화벽에 비해 여러 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-107">PF has since evolved quickly and now has several advantages over other available firewalls.</span></span> <span data-ttu-id="1ece2-108">NAT(네트워크 주소 변환)는 처음부터 PF에 포함되었으며, 이후에 ALTQ를 통합하고 PF의 구성을 통해 구성할 수 있게 함으로써 패킷 스케줄러 및 활성 큐 관리 기능이 PF에 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-108">Network Address Translation (NAT) is in PF since day one, then packet scheduler and active queue management have been integrated into PF, by integrating the ALTQ and making it configurable through PF's configuration.</span></span> <span data-ttu-id="1ece2-109">장애 조치(failover) 및 중복성을 위한 pfsync 및 CARP, 세션 인증을 위한 authpf, 까다로운 FTP 프로토콜을 방화벽으로 쉽게 차단하기 위한 ftp-proxy 등의 기능도 PF를 확장했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-109">Features such as pfsync and CARP for failover and redundancy, authpf for session authentication, and ftp-proxy to ease firewalling the difficult FTP protocol, have also extended PF.</span></span> <span data-ttu-id="1ece2-110">즉, PF는 강력하고 풍부한 기능을 갖춘 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-110">In short, PF is a powerful and feature-rich firewall.</span></span> 

## <a name="get-started"></a><span data-ttu-id="1ece2-111">시작</span><span class="sxs-lookup"><span data-stu-id="1ece2-111">Get started</span></span>
<span data-ttu-id="1ece2-112">웹 서버에 대해 클라우드에서 보안 방화벽을 설정하려는 경우 지금 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-112">If you are interested in setting up a secure firewall in the cloud for your web servers, then let’s get started.</span></span> <span data-ttu-id="1ece2-113">네트워킹 토폴로지를 설정하기 위해 이 Azure Resource Manager 템플릿에 사용된 스크립트를 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-113">You can also apply the scripts used in this Azure Resource Manager template to set up your networking topology.</span></span>
<span data-ttu-id="1ece2-114">Azure Resource Manager 템플릿은 Nginx 웹 서버가 설치 및 구성된 2대의 FreeBSD 가상 컴퓨터와 PF를 사용하여 NAT/리디렉션을 수행하는 FreeBSD 가상 컴퓨터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-114">The Azure Resource Manager template set up a FreeBSD virtual machine that performs NAT /redirection using PF and two FreeBSD virtual machines with the Nginx web server installed and configured.</span></span> <span data-ttu-id="1ece2-115">두 웹 서버 송신 트래픽에 대해 NAT를 수행하는 것 외에도, NAT/리디렉션 가상 컴퓨터는 HTTP 요청을 가로챈 후 로빈 방식으로 두 웹 서버로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-115">In addition to performing NAT for the two web servers egress traffic, the NAT/redirection virtual machine intercepts HTTP requests and redirect them to the two web servers in round-robin fashion.</span></span> <span data-ttu-id="1ece2-116">VNet은 라우팅할 수 없는 개인 IP 주소 공간 10.0.0.2/24를 사용하며 사용자는 템플릿의 매개 변수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-116">The VNet uses the private non-routable IP address space 10.0.0.2/24 and you can modify the parameters of the template.</span></span> <span data-ttu-id="1ece2-117">또한 Azure Resource Manager 템플릿은 대상 IP 주소를 기준으로 Azure 기본 경로를 재정의하는 데 사용되는 개별 경로 컬렉션에 해당하는 전체 VNet에 대해 경로 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-117">The Azure Resource Manager template also defines a route table for the whole VNet, which is a collection of individual routes used to override Azure default routes based on the destination IP address.</span></span> 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a><span data-ttu-id="1ece2-119">Azure CLI를 통해 배포</span><span class="sxs-lookup"><span data-stu-id="1ece2-119">Deploy through Azure CLI</span></span>
<span data-ttu-id="1ece2-120">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-120">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="1ece2-121">[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-121">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1ece2-122">다음 예제는 `West US` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-122">The following example creates a resource group name `myResourceGroup` in the `West US` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="1ece2-123">다음으로 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-123">Next, deploy the template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="1ece2-124">같은 경로 아래에 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json)을 다운로드하고 `adminPassword`, `networkPrefix` 및 `domainNamePrefix`와 같은 자체 리소스 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-124">Download [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) under the same path and define your own resource values, such as `adminPassword`, `networkPrefix`, and `domainNamePrefix`.</span></span> 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

<span data-ttu-id="1ece2-125">약 5분 후에 `"provisioningState": "Succeeded"` 정보를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-125">After about five minutes, you will get the information of `"provisioningState": "Succeeded"`.</span></span> <span data-ttu-id="1ece2-126">그런 후에 프런트 엔드 VM(NAT)에 대해 ssh를 수행하거나 프런트 엔드 VM(NAT)의 공용 IP 주소 또는 FQDN을 사용하여 브라우저에서 Nginx 웹 서버에 액세스할 수 잇습니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-126">Then you can ssh to the frontend VM (NAT) or access Nginx web server in a browser using the public IP address or FQDN of the frontend VM (NAT).</span></span> <span data-ttu-id="1ece2-127">다음 예제에서는 `myResourceGroup` 리소스 그룹의 프런트 엔드 VM(NAT)에 할당된 FQDN 및 공용 IP 주소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-127">The following example lists FQDN and public IP address that assigned to the frontend VM (NAT) in the `myResourceGroup` resource group.</span></span> 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a><span data-ttu-id="1ece2-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ece2-128">Next steps</span></span>
<span data-ttu-id="1ece2-129">Azure에서 자체 NAT을 설정하려고 하나요?</span><span class="sxs-lookup"><span data-stu-id="1ece2-129">Do you want to set up your own NAT in Azure?</span></span> <span data-ttu-id="1ece2-130">무료 오픈 소스면서 강력한 기능을 원하시나요?</span><span class="sxs-lookup"><span data-stu-id="1ece2-130">Open Source, free but powerful?</span></span> <span data-ttu-id="1ece2-131">그렇다면 PF가 적격입니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-131">Then PF is a good choice.</span></span> <span data-ttu-id="1ece2-132">[pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) 템플릿을 사용하면 일반적인 웹 서버 시나리오에 대해 Azure에서 FreeBSD PF를 사용하여 라운드 로빈 부하 분산 방식으로 NAT 방화벽을 설정하는 데 5분이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="1ece2-132">By using the template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), you only need five minutes to set up a NAT firewall with round-robin load balancing using FreeBSD's PF in Azure for common web server scenario.</span></span> 

<span data-ttu-id="1ece2-133">Azure의 FreeBSD 제품에 대해 알아보려면 [Azure의 FreeBSD 소개](freebsd-intro-on-azure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ece2-133">If you want to learn the offering of FreeBSD in Azure, refer to [introduction to FreeBSD on Azure](freebsd-intro-on-azure.md).</span></span>

<span data-ttu-id="1ece2-134">PF에 대한 자세한 내용은 [FreeBSD 핸드북](https://www.freebsd.org/doc/handbook/firewalls-pf.html) 또는 [PF-사용자 가이드](https://www.freebsd.org/doc/handbook/firewalls-pf.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ece2-134">If you want to know more about PF, refer to [FreeBSD handbook](https://www.freebsd.org/doc/handbook/firewalls-pf.html) or [PF-User's Guide](https://www.freebsd.org/doc/handbook/firewalls-pf.html).</span></span>
