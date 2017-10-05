---
title: "Azure DNS와 Azure 리소스 통합 | Microsoft Docs"
description: "Azure DNS를 함께 사용하여 Azure 리소스에 대해 DNS를 제공하는 방법에 대해 알아봅니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: e0e7144c38c36f1583e0bcb7dfffba26e9a8bdad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-dns-to-provide-custom-domain-settings-for-an-azure-service"></a><span data-ttu-id="3a39d-103">Azure DNS를 사용하여 Azure 서비스에 대해 사용자 지정 도메인 설정 제공</span><span class="sxs-lookup"><span data-stu-id="3a39d-103">Use Azure DNS to provide custom domain settings for an Azure service</span></span>

<span data-ttu-id="3a39d-104">Azure DNS는 사용자 지정 도메인을 지원하거나 FQDN(정규화된 도메인 이름)이 있는 모든 Azure 리소스에 대해 사용자 지정 도메인용 DNS를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-104">Azure DNS provides DNS for a custom domain for any of your Azure resources that support custom domains or that have a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="3a39d-105">예를 들어, Azure 웹앱이 있으며 사용자가 contoso.com 또는 www.contoso.com을 FQDN으로 사용하여 액세스하도록 설정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-105">An example is you have an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span> <span data-ttu-id="3a39d-106">이 문서에서는 사용자 지정 도메인을 사용하기 위해 Azure DNS로 Azure 서비스를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-106">This article walks you through configuring your Azure service with Azure DNS for using custom domains.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a39d-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3a39d-107">Prerequisites</span></span>

<span data-ttu-id="3a39d-108">사용자 지정 도메인에 대해 Azure DNS를 사용하려면 먼저 도메인을 Azure DNS에 위임해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-108">In order to use Azure DNS for your custom domain, you must first delegate your domain to Azure DNS.</span></span> <span data-ttu-id="3a39d-109">위임을 위해 이름 서버를 구성하는 방법에 대한 지침은 [도메인을 Azure DNS에 위임](./dns-delegate-domain-azure-dns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a39d-109">Visit [Delegate a domain to Azure DNS](./dns-delegate-domain-azure-dns.md) for instructions on how to configure your name servers for delegation.</span></span> <span data-ttu-id="3a39d-110">도메인이 Azure DNS 영역에 위임되면 필요한 DNS 레코드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-110">Once your domain is delegated to your Azure DNS zone, you are able to configure the DNS records needed.</span></span>

<span data-ttu-id="3a39d-111">[Azure Function Apps](#azure-function-app), [Azure IoT](#azure-iot), [공용 IP 주소](#public-ip-address), [App Service(Web Apps)](#app-service-web-apps), [Blob Storage](#blob-storage) 및 [Azure CDN](#azure-cdn)에 대해 베니티 또는 사용자 지정 도메인을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-111">You can configure a vanity or custom domain for [Azure Function Apps](#azure-function-app), [Azure IoT](#azure-iot), [Public IP addresses](#public-ip-address), [App Service (Web Apps)](#app-service-web-apps), [Blob storage](#blob-storage), and [Azure CDN](#azure-cdn).</span></span>

## <a name="azure-function-app"></a><span data-ttu-id="3a39d-112">Azure 함수 앱</span><span class="sxs-lookup"><span data-stu-id="3a39d-112">Azure Function App</span></span>

<span data-ttu-id="3a39d-113">Azure 함수 앱에 대해 사용자 지정 도메인을 구성하기 위해 함수 앱 자체의 구성은 물론 CNAME 레코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-113">To configure a custom domain for Azure function apps, a CNAME record is created as well as configuration on the function app itself.</span></span>
 
<span data-ttu-id="3a39d-114">**기타** > **함수 앱**으로 이동하고 함수 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-114">Navigate to **Other** > **Function App** and select your Function App.</span></span> <span data-ttu-id="3a39d-115">**플랫폼 기능**을 클릭하고 **네트워킹** 아래에서 **사용자 지정 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-115">Click **Platform features** and under **NETWORKING** click **Custom domains**.</span></span>

![함수 앱 블레이드](./media/dns-custom-domain/functionapp.png)

<span data-ttu-id="3a39d-117">**사용자 지정 도메인** 블레이드에서 현재 URL을 기록해 두세요. 이 주소는 생성된 DNS 레코드에 대한 별칭으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-117">Note the current url on the **Custom domains** blade, this address is used as the alias for the DNS record created.</span></span>

![사용자 지정 도메인 블레이드](./media/dns-custom-domain/functionshostname.png)

<span data-ttu-id="3a39d-119">DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-119">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-120">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-120">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>

|<span data-ttu-id="3a39d-121">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-121">Property</span></span>  |<span data-ttu-id="3a39d-122">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-122">Value</span></span>  |<span data-ttu-id="3a39d-123">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-123">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-124">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-124">Name</span></span>     | <span data-ttu-id="3a39d-125">myfunctionapp</span><span class="sxs-lookup"><span data-stu-id="3a39d-125">myfunctionapp</span></span>        | <span data-ttu-id="3a39d-126">이 값과 도메인 이름 레이블을 함께 사용하면 사용자 지정 도메인 이름에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-126">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="3a39d-127">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-127">Type</span></span>     | <span data-ttu-id="3a39d-128">CNAME</span><span class="sxs-lookup"><span data-stu-id="3a39d-128">CNAME</span></span>        | <span data-ttu-id="3a39d-129">별칭을 사용하는 CNAME 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-129">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="3a39d-130">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-130">TTL</span></span>     | <span data-ttu-id="3a39d-131">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-131">1</span></span>        | <span data-ttu-id="3a39d-132">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-132">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-133">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-133">TTL unit</span></span>     | <span data-ttu-id="3a39d-134">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-134">Hours</span></span>        | <span data-ttu-id="3a39d-135">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-135">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-136">Alias</span><span class="sxs-lookup"><span data-stu-id="3a39d-136">Alias</span></span>     | <span data-ttu-id="3a39d-137">adatumfunction.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="3a39d-137">adatumfunction.azurewebsites.net</span></span>        | <span data-ttu-id="3a39d-138">이 예에서 별칭을 만드는 DNS 이름은 함수 앱에 기본적으로 제공된 DNS 이름인 adatumfunction.azurewebsites.net입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-138">The DNS name you are creating the alias for, in this example it is the adatumfunction.azurewebsites.net DNS name provided by default to the function app.</span></span>        |

<span data-ttu-id="3a39d-139">다시 함수 앱으로 돌아가 **플랫폼 기능**을 클릭하고 **네트워킹** 아래에서 **사용자 지정 도메인**을 클릭한 후 **호스트 이름** 아래에서 **+ 호스트 이름 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-139">Navigate back to your function app, click **Platform features**, and under **NETWORKING** click **Custom domains**, then under **Hostnames** click **+ Add hostname**.</span></span>

<span data-ttu-id="3a39d-140">**호스트 이름 추가** 블레이드에서 **호스트 이름** 텍스트 필드에 CNAME 레코드를 입력하고 **유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-140">On the **Add hostname** blade, enter the CNAME record in the **hostname** text field and click **Validate**.</span></span> <span data-ttu-id="3a39d-141">레코드를 찾을 수 없는 경우 **호스트 이름 추가** 단추가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-141">If the record was able to be found, the **Add hostname** button appears.</span></span> <span data-ttu-id="3a39d-142">**호스트 이름 추가**를 클릭하여 별칭을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-142">Click **Add hostname** to add the alias.</span></span>

![함수 앱 호스트 이름 추가 블레이드](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a><span data-ttu-id="3a39d-144">Azure IoT</span><span class="sxs-lookup"><span data-stu-id="3a39d-144">Azure IoT</span></span>

<span data-ttu-id="3a39d-145">Azure IoT에는 서비스 자체에 필요한 어떠한 사용자 지정도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-145">Azure IoT does not have any customizations that are needed on the service itself.</span></span> <span data-ttu-id="3a39d-146">IoT Hub에서 사용자 지정 도메인을 사용하려면 해당 리소스를 가리키는 CNAME 레코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-146">To use a custom domain with an IoT Hub only a CNAME record pointed to the resources is needed.</span></span>

<span data-ttu-id="3a39d-147">**사물 인터넷** > **IoT Hub**로 이동하고 IoT Hub를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-147">Navigate to **Internet of Things** > **IoT Hub** and select your IoT hub.</span></span> <span data-ttu-id="3a39d-148">**개요** 블레이드에서 IoT Hub의 FQDN을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-148">On the **Overview** blade, note the FQDN of the IoT hub.</span></span>

![IoT Hub 블레이드](./media/dns-custom-domain/iot.png)

<span data-ttu-id="3a39d-150">다음으로, DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-150">Next, navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-151">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-151">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="3a39d-152">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-152">Property</span></span>  |<span data-ttu-id="3a39d-153">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-153">Value</span></span>  |<span data-ttu-id="3a39d-154">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-154">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-155">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-155">Name</span></span>     | <span data-ttu-id="3a39d-156">myiothub</span><span class="sxs-lookup"><span data-stu-id="3a39d-156">myiothub</span></span>        | <span data-ttu-id="3a39d-157">이 값과 도메인 이름 레이블을 함께 사용하면 IoT Hub에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-157">This value along with the domain name label is the FQDN for the IoT hub.</span></span>        |
|<span data-ttu-id="3a39d-158">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-158">Type</span></span>     | <span data-ttu-id="3a39d-159">CNAME</span><span class="sxs-lookup"><span data-stu-id="3a39d-159">CNAME</span></span>        | <span data-ttu-id="3a39d-160">별칭을 사용하는 CNAME 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-160">Use a CNAME record is using an alias.</span></span>
|<span data-ttu-id="3a39d-161">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-161">TTL</span></span>     | <span data-ttu-id="3a39d-162">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-162">1</span></span>        | <span data-ttu-id="3a39d-163">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-163">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-164">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-164">TTL unit</span></span>     | <span data-ttu-id="3a39d-165">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-165">Hours</span></span>        | <span data-ttu-id="3a39d-166">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-166">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-167">Alias</span><span class="sxs-lookup"><span data-stu-id="3a39d-167">Alias</span></span>     | <span data-ttu-id="3a39d-168">adatumIOT.azure-devices.net</span><span class="sxs-lookup"><span data-stu-id="3a39d-168">adatumIOT.azure-devices.net</span></span>        | <span data-ttu-id="3a39d-169">이 예에서 별칭을 만드는 DNS 이름은 IoT Hub에 제공된 호스트 이름인 adatumIOT.azure-devices.net입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-169">The DNS name you are creating the alias for, in this example it is the adatumIOT.azure-devices.net host name provided by the IoT hub.</span></span>

<span data-ttu-id="3a39d-170">레코드를 만든 후 `nslookup`을 사용하여 CNAME 레코드에서 이름 확인을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-170">Once the record is created, test name resolution with the CNAME record using `nslookup`</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="3a39d-171">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="3a39d-171">Public IP address</span></span>

<span data-ttu-id="3a39d-172">Application Gateway, Load Balancer, Cloud Service, Resource Manager VM, 클래식 VM처럼 공용 IP 주소 리소스를 사용하는 서비스에 대해 사용자 지정 도메인을 구성하기 위해 CNAME 레코드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-172">To configure a custom domain for services that use a public IP address resource such as Application Gateway, Load Balancer, Cloud Service, Resource Manager VMs, and, Classic VMs, a CNAME record used.</span></span>

<span data-ttu-id="3a39d-173">**네트워킹** > **공용 IP 주소**로 이동하고 공용 IP 리소스를 선택하고 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-173">Navigate to **Networking** > **Public IP address**, select the Public IP resource and click **Configuration**.</span></span> <span data-ttu-id="3a39d-174">표시된 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-174">Notate the IP address shown.</span></span>

![공용 ip 블레이드](./media/dns-custom-domain/publicip.png)

<span data-ttu-id="3a39d-176">DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-176">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-177">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-177">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="3a39d-178">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-178">Property</span></span>  |<span data-ttu-id="3a39d-179">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-179">Value</span></span>  |<span data-ttu-id="3a39d-180">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-180">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-181">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-181">Name</span></span>     | <span data-ttu-id="3a39d-182">mywebserver</span><span class="sxs-lookup"><span data-stu-id="3a39d-182">mywebserver</span></span>        | <span data-ttu-id="3a39d-183">이 값과 도메인 이름 레이블을 함께 사용하면 사용자 지정 도메인 이름에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-183">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="3a39d-184">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-184">Type</span></span>     | <span data-ttu-id="3a39d-185">A</span><span class="sxs-lookup"><span data-stu-id="3a39d-185">A</span></span>        | <span data-ttu-id="3a39d-186">리소스가 IP 주소이므로 A 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-186">Use an A record as the resource is an IP address.</span></span>        |
|<span data-ttu-id="3a39d-187">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-187">TTL</span></span>     | <span data-ttu-id="3a39d-188">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-188">1</span></span>        | <span data-ttu-id="3a39d-189">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-189">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-190">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-190">TTL unit</span></span>     | <span data-ttu-id="3a39d-191">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-191">Hours</span></span>        | <span data-ttu-id="3a39d-192">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-192">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-193">IP 주소</span><span class="sxs-lookup"><span data-stu-id="3a39d-193">IP Address</span></span>     | <your ip address>       | <span data-ttu-id="3a39d-194">공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-194">The public IP address.</span></span>|

![A 레코드 만들기](./media/dns-custom-domain/arecord.png)

<span data-ttu-id="3a39d-196">A 레코드가 생성되면 `nslookup`을 실행하여 레코드 확인의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-196">Once the A record is created, run `nslookup` to validate the record resolves.</span></span>

![공용 ip dns 조회](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a><span data-ttu-id="3a39d-198">App Service(Web Apps)</span><span class="sxs-lookup"><span data-stu-id="3a39d-198">App Service (Web Apps)</span></span>

<span data-ttu-id="3a39d-199">다음 단계는 앱 서비스 웹앱에 대해 사용자 지정 도메인을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-199">The following steps take you through configuring a custom domain for an app service web app.</span></span>

<span data-ttu-id="3a39d-200">**웹 및 모바일** > **App Service**로 이동하고 사용자 지정 도메인 이름을 구성하는 리소스를 선택하고 **사용자 지정 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-200">Navigate to **Web & Mobile** > **App Service** and select the resource you are configuring a custom domain name, and click **Custom domains**.</span></span>

<span data-ttu-id="3a39d-201">**사용자 지정 도메인** 블레이드에서 현재 URL을 기록해 두세요. 이 주소는 생성된 DNS 레코드에 대한 별칭으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-201">Note the current url on the **Custom domains** blade, this address is used as the alias for the DNS record created.</span></span>

![사용자 지정 도메인 블레이드](./media/dns-custom-domain/url.png)

<span data-ttu-id="3a39d-203">DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-203">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-204">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-204">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="3a39d-205">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-205">Property</span></span>  |<span data-ttu-id="3a39d-206">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-206">Value</span></span>  |<span data-ttu-id="3a39d-207">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-207">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-208">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-208">Name</span></span>     | <span data-ttu-id="3a39d-209">mywebserver</span><span class="sxs-lookup"><span data-stu-id="3a39d-209">mywebserver</span></span>        | <span data-ttu-id="3a39d-210">이 값과 도메인 이름 레이블을 함께 사용하면 사용자 지정 도메인 이름에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-210">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="3a39d-211">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-211">Type</span></span>     | <span data-ttu-id="3a39d-212">CNAME</span><span class="sxs-lookup"><span data-stu-id="3a39d-212">CNAME</span></span>        | <span data-ttu-id="3a39d-213">별칭을 사용하는 CNAME 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-213">Use a CNAME record is using an alias.</span></span> <span data-ttu-id="3a39d-214">리소스에서 IP 주소를 사용한 경우 A 레코드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-214">If the resource used an IP address, an A record would be used.</span></span>        |
|<span data-ttu-id="3a39d-215">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-215">TTL</span></span>     | <span data-ttu-id="3a39d-216">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-216">1</span></span>        | <span data-ttu-id="3a39d-217">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-217">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-218">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-218">TTL unit</span></span>     | <span data-ttu-id="3a39d-219">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-219">Hours</span></span>        | <span data-ttu-id="3a39d-220">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-220">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-221">Alias</span><span class="sxs-lookup"><span data-stu-id="3a39d-221">Alias</span></span>     | <span data-ttu-id="3a39d-222">webserver.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="3a39d-222">webserver.azurewebsites.net</span></span>        | <span data-ttu-id="3a39d-223">이 예에서 별칭을 만드는 DNS 이름은 웹앱에 기본적으로 제공된 DNS 이름인 webserver.azurewebsites.net입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-223">The DNS name you are creating the alias for, in this example it is the webserver.azurewebsites.net DNS name provided by default to the web app.</span></span>        |


![CNAME 레코드 만들기](./media/dns-custom-domain/createcnamerecord.png)

<span data-ttu-id="3a39d-225">사용자 지정 도메인 이름을 위해 구성된 앱 서비스로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-225">Navigate back to the app service that is configured for the custom domain name.</span></span> <span data-ttu-id="3a39d-226">**사용자 지정 도메인**을 클릭한 후 **호스트 이름**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-226">Click **Custom domains**, then click **Hostnames**.</span></span> <span data-ttu-id="3a39d-227">생성한 CNAME 레코드를 추가하려면 **+ 호스트 이름 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-227">To add the CNAME record you created, click **+ Add hostname**.</span></span>

![그림 1](./media/dns-custom-domain/figure1.png)

<span data-ttu-id="3a39d-229">프로세스가 완료되면 **nslookup**을 실행하여 이름 확인이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-229">Once the process is complete, run **nslookup** to validate name resolution is working.</span></span>

![그림 1](./media/dns-custom-domain/finalnslookup.png)

<span data-ttu-id="3a39d-231">App Service에 사용자 지정 도메인을 매핑하는 방법에 대한 자세한 내용은 [Azure Web Apps에 기존 사용자 지정 DNS 이름 매핑](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a39d-231">To learn more about mapping a custom domain to App Service, visit [Map an existing custom DNS name to Azure Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

<span data-ttu-id="3a39d-232">사용자 지정 도메인을 구매해야 하는 경우 App Service 도메인에 대해 자세히 알아보려면 [Azure Web Apps에 대한 사용자 지정 도메인 이름 구입](../app-service-web/custom-dns-web-site-buydomains-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a39d-232">If you need to purchase a custom domain, visit [Buy a custom domain name for Azure Web Apps](../app-service-web/custom-dns-web-site-buydomains-web-app.md) to learn more about App Service domains.</span></span>

## <a name="blob-storage"></a><span data-ttu-id="3a39d-233">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="3a39d-233">Blob storage</span></span>

<span data-ttu-id="3a39d-234">다음 단계에서는 asverify 메서드를 사용하여 Blob Storage 계정에 대해 CNAME 레코드를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-234">The following steps take you through configuring a CNAME record for a blob storage account using the asverify method.</span></span> <span data-ttu-id="3a39d-235">이 메서드는 가동 중지 시간이 없음을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-235">This method ensures there is no downtime.</span></span>

<span data-ttu-id="3a39d-236">**Storage** > **저장소 계정**으로 이동하여 저장소 계정을 선택하고 **사용자 지정 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-236">Navigate to **Storage** > **Storage Accounts**, select your storage account, and click **Custom domain**.</span></span> <span data-ttu-id="3a39d-237">2단계 아래에서 FQDN을 기록해 둡니다. 이 값은 첫 번째 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-237">Notate the FQDN under step 2, this value is used to create the first CNAME record</span></span>

![Blob Storage 사용자 지정 도메인](./media/dns-custom-domain/blobcustomdomain.png)

<span data-ttu-id="3a39d-239">DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-239">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-240">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-240">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="3a39d-241">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-241">Property</span></span>  |<span data-ttu-id="3a39d-242">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-242">Value</span></span>  |<span data-ttu-id="3a39d-243">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-243">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-244">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-244">Name</span></span>     | <span data-ttu-id="3a39d-245">asverify.mystorageaccount</span><span class="sxs-lookup"><span data-stu-id="3a39d-245">asverify.mystorageaccount</span></span>        | <span data-ttu-id="3a39d-246">이 값과 도메인 이름 레이블을 함께 사용하면 사용자 지정 도메인 이름에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-246">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="3a39d-247">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-247">Type</span></span>     | <span data-ttu-id="3a39d-248">CNAME</span><span class="sxs-lookup"><span data-stu-id="3a39d-248">CNAME</span></span>        | <span data-ttu-id="3a39d-249">별칭을 사용하는 CNAME 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-249">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="3a39d-250">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-250">TTL</span></span>     | <span data-ttu-id="3a39d-251">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-251">1</span></span>        | <span data-ttu-id="3a39d-252">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-252">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-253">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-253">TTL unit</span></span>     | <span data-ttu-id="3a39d-254">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-254">Hours</span></span>        | <span data-ttu-id="3a39d-255">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-255">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-256">Alias</span><span class="sxs-lookup"><span data-stu-id="3a39d-256">Alias</span></span>     | <span data-ttu-id="3a39d-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3a39d-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span></span>        | <span data-ttu-id="3a39d-258">이 예에서 별칭을 만드는 DNS 이름은 저장소 계정에 기본적으로 제공된 DNS 이름인 asverify.adatumfunctiona9ed.blob.core.windows.net입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-258">The DNS name you are creating the alias for, in this example it is the asverify.adatumfunctiona9ed.blob.core.windows.net DNS name provided by default to the storage account.</span></span>        |

<span data-ttu-id="3a39d-259">**Storage** > **저장소 계정**을 클릭하여 저장소 계정으로 돌아가 저장소 계정을 선택하고 **사용자 지정 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-259">Navigate back to your storage account by clicking **Storage** > **Storage Accounts**, select your storage account and click **Custom domain**.</span></span> <span data-ttu-id="3a39d-260">텍스트 상자에 asverify 접두사 없이 생성한 별칭을 입력하고 [간접 CNAME 유효성 검사 사용]을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-260">Type in the alias you created without the asverify prefix in the text box, check **Use indirect CNAME validation, and click **Save**.</span></span> <span data-ttu-id="3a39d-261">이 단계가 완료되면 DNS 영역으로 돌아가 asverify 접두사 없이 CNAME 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-261">Once this step is complete, return to your DNS zone and create a CNAME record without the asverify prefix.</span></span>  <span data-ttu-id="3a39d-262">이후에는 cdnverify 접두사가 있는 CNAME 레코드를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-262">After that point, you are safe to delete the CNAME record with the cdnverify prefix.</span></span>

![Blob Storage 사용자 지정 도메인](./media/dns-custom-domain/indirectvalidate.png)

<span data-ttu-id="3a39d-264">`nslookup`을 실행하여 DNS 확인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3a39d-264">Validate DNS resolution by running `nslookup`</span></span>

<span data-ttu-id="3a39d-265">사용자 지정 도메인을 Blob Storage 끝점에 매핑하는 방법에 대해 자세히 알아보려면 [Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a39d-265">To learn more about mapping a custom domain to a blob storage endpoint visit [Configure a custom domain name for your Blob storage endpoint](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)</span></span>

## <a name="azure-cdn"></a><span data-ttu-id="3a39d-266">Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3a39d-266">Azure CDN</span></span>

<span data-ttu-id="3a39d-267">다음 단계에서는 cdnverify 메서드를 사용하여 CDN 끝점에 대해 CNAME 레코드를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-267">The following steps take you through configuring a CNAME record for a CDN endpoint using the cdnverify method.</span></span> <span data-ttu-id="3a39d-268">이 메서드는 가동 중지 시간이 없음을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-268">This method ensures there is no downtime.</span></span>

<span data-ttu-id="3a39d-269">**네트워킹** > **CDN 프로필**로 이동하여 CDN 프로필을 선택하고 **일반** 아래에서 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-269">Navigate to **Networking** > **CDN Profiles**, select your CDN profile, and click **Endpoints** under **General**.</span></span>

<span data-ttu-id="3a39d-270">작업 중인 끝점을 선택하고 **+ 사용자 지정 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-270">Select the endpoint you are working with and click **+ Custom domain**.</span></span> <span data-ttu-id="3a39d-271">이 값으로 **끝점 호스트 이름**은 CNAME 레코드가 가리키는 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-271">Note the **Endpoint hostname** as this value is the record that the CNAME record points to.</span></span>

![CDN 사용자 지정 도메인](./media/dns-custom-domain/endpointcustomdomain.png)

<span data-ttu-id="3a39d-273">DNS 영역으로 이동하고 **+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-273">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="3a39d-274">**레코드 집합 추가** 블레이드에서 다음 정보를 입력하고 **확인**을 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-274">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>

|<span data-ttu-id="3a39d-275">속성</span><span class="sxs-lookup"><span data-stu-id="3a39d-275">Property</span></span>  |<span data-ttu-id="3a39d-276">값</span><span class="sxs-lookup"><span data-stu-id="3a39d-276">Value</span></span>  |<span data-ttu-id="3a39d-277">설명</span><span class="sxs-lookup"><span data-stu-id="3a39d-277">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="3a39d-278">이름</span><span class="sxs-lookup"><span data-stu-id="3a39d-278">Name</span></span>     | <span data-ttu-id="3a39d-279">cdnverify.mycdnendpoint</span><span class="sxs-lookup"><span data-stu-id="3a39d-279">cdnverify.mycdnendpoint</span></span>        | <span data-ttu-id="3a39d-280">이 값과 도메인 이름 레이블을 함께 사용하면 사용자 지정 도메인 이름에 대한 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-280">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="3a39d-281">형식</span><span class="sxs-lookup"><span data-stu-id="3a39d-281">Type</span></span>     | <span data-ttu-id="3a39d-282">CNAME</span><span class="sxs-lookup"><span data-stu-id="3a39d-282">CNAME</span></span>        | <span data-ttu-id="3a39d-283">별칭을 사용하는 CNAME 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-283">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="3a39d-284">TTL</span><span class="sxs-lookup"><span data-stu-id="3a39d-284">TTL</span></span>     | <span data-ttu-id="3a39d-285">1</span><span class="sxs-lookup"><span data-stu-id="3a39d-285">1</span></span>        | <span data-ttu-id="3a39d-286">1은 1시간 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-286">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="3a39d-287">TTL 단위</span><span class="sxs-lookup"><span data-stu-id="3a39d-287">TTL unit</span></span>     | <span data-ttu-id="3a39d-288">시간</span><span class="sxs-lookup"><span data-stu-id="3a39d-288">Hours</span></span>        | <span data-ttu-id="3a39d-289">시간 측정으로 시간(Hour)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-289">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="3a39d-290">Alias</span><span class="sxs-lookup"><span data-stu-id="3a39d-290">Alias</span></span>     | <span data-ttu-id="3a39d-291">cdnverify.adatumcdnendpoint.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="3a39d-291">cdnverify.adatumcdnendpoint.azureedge.net</span></span>        | <span data-ttu-id="3a39d-292">이 예에서 별칭을 만드는 DNS 이름은 저장소 계정에 기본적으로 제공된 DNS 이름인 cdnverify.adatumcdnendpoint.azureedge.net입니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-292">The DNS name you are creating the alias for, in this example it is the cdnverify.adatumcdnendpoint.azureedge.net DNS name provided by default to the storage account.</span></span>        |

<span data-ttu-id="3a39d-293">**네트워킹** > **CDN 프로필**을 클릭하여 CDN 끝점으로 돌아가 CDN 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-293">Navigate back to your CDN endpoint by clicking **Networking** > **CDN Profiles**, and select your CDN profile.</span></span> <span data-ttu-id="3a39d-294">**+ 사용자 지정 도메인**을 클릭하고 cdnverify 접두사 없이 CNAME 레코드 별칭을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-294">Click **+ Custom domain** and enter your CNAME record alias without the cdnverify prefix and click **Add**.</span></span>

<span data-ttu-id="3a39d-295">이 단계가 완료되면 DNS 영역으로 돌아가 cdnverify 접두사 없이 CNAME 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-295">Once this step is complete, return to your DNS zone and create a CNAME record without the cdnverify prefix.</span></span>  <span data-ttu-id="3a39d-296">이후에는 cdnverify 접두사가 있는 CNAME 레코드를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-296">After that point, you are safe to delete the CNAME record with the cdnverify prefix.</span></span> <span data-ttu-id="3a39d-297">CDN에 대한 자세한 정보 및 중간 등록 단계 없이 사용자 지정 도메인을 구성하는 방법은 [Azure CDN 콘텐츠를 사용자 지정 도메인에 매핑](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a39d-297">For more information on CDN and how to configure a custom domain without the intermediate registration step visit [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a39d-298">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a39d-298">Next steps</span></span>

<span data-ttu-id="3a39d-299">[Azure에서 호스트되는 서비스에 대해 역방향 DNS 구성](dns-reverse-dns-for-azure-services.md) 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a39d-299">Learn how to [configure reverse DNS for services hosted in Azure](dns-reverse-dns-for-azure-services.md).</span></span>