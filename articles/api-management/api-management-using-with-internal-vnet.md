---
title: "내부 가상 네트워크에서 Azure API Management를 사용하는 방법 | Microsoft Docs"
description: "내부 가상 네트워크에서 Azure API Management를 설정하고 구성하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="d2071-103">내부 가상 네트워크에서 Azure API Management를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2071-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="d2071-104">Azure VNETs(Virtual Networks)를 사용하면 API Management를 통해 인터넷에서 액세스할 수 없는 API를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="d2071-105">여러 가지 VPN 기술을 연결하는 데 사용할 수 있으며, API Management를 다음 두 가지 주요 모드로 VNET 내에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="d2071-106">외부</span><span class="sxs-lookup"><span data-stu-id="d2071-106">External</span></span>
* <span data-ttu-id="d2071-107">내부</span><span class="sxs-lookup"><span data-stu-id="d2071-107">Internal</span></span>

## <span data-ttu-id="d2071-108"><a name="overview"> </a>개요</span><span class="sxs-lookup"><span data-stu-id="d2071-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="d2071-109">API Management를 내부 가상 네트워크 모드로 배포하는 경우 모든 서비스 끝점(게이트웨이, 개발자 포털, 게시자 포털, 직접 관리 및 Git)은 액세스를 제어하는 가상 네트워크 내부에서만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="d2071-110">서비스 끝점은 공용 DNS 서버에 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="d2071-111">내부 모드에서 API Management를 사용하면 다음 시나리오를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="d2071-112">사이트 간 연결 또는 ExpressRoute VPN 연결을 사용하여 외부의 타사에서 개인 데이터 센터에 호스팅한 API에 안전하게 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="d2071-113">공통 게이트웨이를 통해 클라우드 기반 API와 온-프레미스 API를 공개함으로써 하이브리드 클라우드 시나리오를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="d2071-114">단일 게이트웨이 끝점을 사용하여 여러 지리적 위치에서 호스팅되는 API를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="d2071-115"><a name="enable-vpn"> </a>내부 가상 네트워크에 API Management 만들기</span><span class="sxs-lookup"><span data-stu-id="d2071-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="d2071-116">내부 가상 네트워크의 API Management 서비스는 ILB(내부 부하 분산 장치) 뒤에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="d2071-117">ILB의 IP 주소는 [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) 범위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="d2071-118">Azure Portal을 사용하여 VNET 연결 사용</span><span class="sxs-lookup"><span data-stu-id="d2071-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="d2071-119">먼저 [API Management 서비스 만들기][Create API Management service] 단계에 따라 API Management 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="d2071-120">그런 다음 API Management를 설정하여 가상 네트워크 내에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![내부 가상 네트워크에서 APIM 설정을 위한 메뉴][api-management-using-internal-vnet-menu]

<span data-ttu-id="d2071-122">배포가 성공하면 대시보드에 서비스의 내부 가상 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![내부 VNET이 구성된 API Management 대시보드][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="d2071-124">PowerShell cmdlet을 사용하여 VNET 연결 사용</span><span class="sxs-lookup"><span data-stu-id="d2071-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="d2071-125">PowerShell cmdlet을 사용하여 VNET 연결을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="d2071-126">**VNET 내부에 API Management 서비스 만들기**: [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) cmdlet을 사용하여 VNET 내에 Azure API Management 서비스를 만들고 내부 VNET 유형을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="d2071-127">**VNET 내부에 기존 API Management 서비스 배포**: [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) cmdlet을 사용하여 가상 네트워크 내부로 기존 Azure API Management 서비스를 이동하고 내부 VNET 유형을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="d2071-128"><a name="apim-dns-configuration"></a>DNS 구성</span><span class="sxs-lookup"><span data-stu-id="d2071-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="d2071-129">외부 가상 네트워크 모드에서 API Management를 사용하는 경우 Azure에서 DNS를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="d2071-130">내부 가상 네트워크 모드의 경우 자체의 DNS를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="d2071-131">API Management 서비스는 IP 주소에서 오는 요청을 수신 대기하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="d2071-132">서비스 끝점(게이트웨이, 개발자 포털, 게시자 포털, 직접 관리 끝점 및 Git 포함)에 구성된 호스트 이름에 대한 요청에만 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="d2071-133">기본 호스트 이름에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="d2071-133">Access on default host names:</span></span>
<span data-ttu-id="d2071-134">예를 들어 "contoso"라는 공용 Azure 클라우드에서 API Management 서비스를 만들면 기본적으로 다음 서비스 끝점이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="d2071-135">게이트웨이/프록시 - contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="d2071-136">게시자 포털 및 개발자 포털 - contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="d2071-137">직접 관리 끝점 - contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="d2071-138">GIT - contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="d2071-139">이러한 API Management 서비스 끝점에 액세스하려면 API Management를 배포한 가상 네트워크에 연결된 서브넷에 Virtual Machine을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="d2071-140">서비스의 내부 가상 IP 주소가 10.0.0.5라고 가정하면 다음과 같이 호스트 파일 매핑(%SystemDrive%\drivers\etc\hosts)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="d2071-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="d2071-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="d2071-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="d2071-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="d2071-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="d2071-145">그런 다음 만든 Virtual Machine에서 모든 서비스 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="d2071-146">가상 네트워크에서 사용자 지정 DNS 서버를 사용하는 경우 A DNS 레코드를 만들고 가상 네트워크의 어느 곳에서나 이러한 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="d2071-147">사용자 지정 도메인 이름에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="d2071-147">Access on custom domain names:</span></span>
<span data-ttu-id="d2071-148">기본 호스트 이름으로 API Management 서비스에 액세스하지 않으려면 아래와 같이 모든 서비스 끝점에 대해 사용자 지정 도메인 이름을 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![API Management를 위한 사용자 지정 도메인 설정][api-management-custom-domain-name]

<span data-ttu-id="d2071-150">그런 다음 DNS 서버에 A 레코드를 만들어 가상 네트워크 내에서만 액세스할 수 있는 이러한 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2071-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="d2071-151"><a name="related-content"> </a>관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="d2071-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="d2071-152">[VNET에 APIM을 설정하는 동안의 일반 네트워크 구성 문제][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="d2071-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="d2071-153">가상 네트워크 FAQ</span><span class="sxs-lookup"><span data-stu-id="d2071-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* <span data-ttu-id="d2071-154">[DNS에 A 레코드 만들기](https://msdn.microsoft.com/en-us/library/bb727018.aspx)(영문)</span><span class="sxs-lookup"><span data-stu-id="d2071-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span></span>

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
