---
title: "Microsoft Azure Cloud Services FAQ에 대한 구성 및 관리 문제 | Microsoft Docs"
description: "이 문서는 Microsoft Azure Cloud Services의 구성 및 관리에 대한 질문과 대답을 나열합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 42b5d2947df92b4486fe149d046168208083dde2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="978c2-103">Azure Cloud Services의 구성 및 관리 문제: FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="978c2-103">Configuration and management issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="978c2-104">이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 구성 및 관리 문제에 대한 질문과 대답을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-104">This article includes frequently asked questions about configuration and management issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="978c2-105">크기 정보는 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-to-my-website"></a><span data-ttu-id="978c2-106">"nosniff"를 내 웹 사이트에 추가하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-106">How do I add "nosniff" to my website?</span></span>
<span data-ttu-id="978c2-107">클라이언트가 MIME 형식을 스니핑하지 않도록 하려면 *web.config* 파일에 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-107">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="978c2-108">IIS에서 설정으로도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-108">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="978c2-109">[일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서의 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-109">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a><span data-ttu-id="978c2-110">웹 역할에 IIS를 사용자 지정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-110">How do I customize IIS for a web role?</span></span>
<span data-ttu-id="978c2-111">[일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서의 IIS 시작 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-111">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="978c2-112">X 인스턴스 이상 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-112">I cannot scale beyond X instances</span></span>
<span data-ttu-id="978c2-113">사용자의 Azure 구독은 사용할 수 있는 코어 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-113">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="978c2-114">사용 가능한 모든 코어를 사용하는 경우 크기 조정은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-114">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="978c2-115">예를 들어 100개의 코어 제한이 있으면 클라우드 서비스에 대한 100개의 A1 크기 가상 컴퓨터 인스턴스나 50개의 A2 크기 가상 컴퓨터 인스턴스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-115">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a><span data-ttu-id="978c2-116">Cloud Services에 역할 기반 액세스를 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-116">How can I implement Role-Based Access for Cloud Services?</span></span>
<span data-ttu-id="978c2-117">Cloud Services는 Azure Resource Manager 기반 서비스가 아니므로 RBAC(역할 기반 액세스 제어) 모델을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-117">Cloud Services doesn't support the Role-Based Access Control (RBAC) model, as it's not an Azure Resource Manager based service.</span></span>

<span data-ttu-id="978c2-118">[Azure RBAC와 클래식 구독 관리자 비교](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-118">See [Azure RBAC vs. classic subscription administrators](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).</span></span>

## <a name="how-do-i-set-the-idle-timeout-for-azure-load-balancer"></a><span data-ttu-id="978c2-119">Azure Load Balancer에 유휴 시간 제한을 설정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-119">How do I set the idle timeout for Azure load balancer?</span></span>
<span data-ttu-id="978c2-120">다음과 같이 서비스 정의(csdef) 파일에서 시간 제한을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-120">You can specify the timeout in your service definition (csdef) file like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
<span data-ttu-id="978c2-121">자세한 정보는 [새로 만들기: Azure Load Balancer에 구성 가능한 유휴 시간 제한](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-121">See [New: Configurable Idle Timeout for Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) for more information.</span></span>

## <a name="can-microsoft-internal-engineers-rdp-to-cloud-service-instances-without-permission"></a><span data-ttu-id="978c2-122">Microsoft 내부 엔지니어는 허가 없이 클라우드 서비스 인스턴스에 RDP할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="978c2-122">Can Microsoft internal engineers RDP to cloud service instances without permission?</span></span>
<span data-ttu-id="978c2-123">Microsoft에서는 소유자 또는 지정된 사용자의 서면 승인(전자 메일 또는 기타 서면 통신)없이 내부 엔지니어가 클라우드 서비스에 RDP하도록 허용하지 않는 엄격한 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-123">Microsoft follows a strict process that will not allow internal engineers to RDP into your cloud service without written permission (email or other written communication) from the owner or their designee.</span></span>

## <a name="why-is-the-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a><span data-ttu-id="978c2-124">내 클라우드 서비스 SSL 인증서의 인증서 체인이 완료되지 않은 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="978c2-124">Why is the certificate chain of my cloud service SSL certificate incomplete?</span></span>
<span data-ttu-id="978c2-125">고객은 리프 인증서가 아닌 전체 인증서 체인(리프 인증서, 중간 인증서 및 루트 인증서)을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-125">We recommend that customers install the full certificate chain (leaf cert, intermediate certs, and root cert) instead of just the leaf certificate.</span></span> <span data-ttu-id="978c2-126">방금 리프 인증서를 설치한 경우 Windows CTL을 탐색하여 인증서 체인을 빌드하기 위해 Windows를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-126">When you install just the leaf certificate, you rely on Windows to build the certificate chain by walking the CTL.</span></span> <span data-ttu-id="978c2-127">Windows가 인증서의 유효성을 검사할 때 Azure 또는 Windows 업데이트에서 일시적인 네트워크 또는 DNS 문제가 발생하는 경우 인증서는 잘못된 것으로 간주될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-127">If intermittent network or DNS issues occur in Azure or Windows Update when Windows is trying to validate the certificate, the certificate may be considered invalid.</span></span> <span data-ttu-id="978c2-128">전체 인증서 체인을 설치하여 이 문제를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-128">By installing the full certificate chain, this problem can be avoided.</span></span> <span data-ttu-id="978c2-129">[체인된 SSL 인증서를 설치하는 방법](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/)의 블로그는 이 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-129">The blog at [How to install a chained SSL certificate](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) shows how to do this.</span></span>

## <a name="how-do-i-associate-a-static-ip-address-to-my-cloud-service"></a><span data-ttu-id="978c2-130">클라우드 서비스에 고정 IP 주소를 연결하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-130">How do I associate a static IP address to my cloud service?</span></span>
<span data-ttu-id="978c2-131">고정 IP 주소를 설정하려면 예약된 IP 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-131">To set up a static IP address, you need to create a reserved IP.</span></span> <span data-ttu-id="978c2-132">이 예약된 IP는 새 클라우드 서비스 또는 기존 배포에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-132">This reserved IP can be associated to a new cloud service or to an existing deployment.</span></span> <span data-ttu-id="978c2-133">자세한 내용은 다음과 같은 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-133">See the following documents for details:</span></span>
* [<span data-ttu-id="978c2-134">예약된 IP 주소를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="978c2-134">How to create a reserved IP address</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [<span data-ttu-id="978c2-135">기존 클라우드 서비스의 IP 주소 예약</span><span class="sxs-lookup"><span data-stu-id="978c2-135">Reserve the IP address of an existing cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [<span data-ttu-id="978c2-136">예약된 IP를 새 클라우드 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="978c2-136">Associate a reserved IP to a new cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [<span data-ttu-id="978c2-137">실행 중인 배포에 예약된 IP 연결</span><span class="sxs-lookup"><span data-stu-id="978c2-137">Associate a reserved IP to a running deployment</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [<span data-ttu-id="978c2-138">서비스 구성 파일을 사용하여 클라우드 서비스에 예약된 IP 연결</span><span class="sxs-lookup"><span data-stu-id="978c2-138">Associate a reserved IP to a cloud service by using a service configuration file</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-the-quota-limit-for-my-cloud-service"></a><span data-ttu-id="978c2-139">클라우드 서비스에 대한 할당량 제한은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="978c2-139">What is the quota limit for my cloud service?</span></span>
<span data-ttu-id="978c2-140">[서비스 특정 제한](../azure-subscription-service-limits.md#subscription-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-140">See [Service-specific limits](../azure-subscription-service-limits.md#subscription-limits).</span></span>

## <a name="why-does-the-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a><span data-ttu-id="978c2-141">클라우드 서비스 VM의 드라이브에 사용 가능한 디스크 공간이 거의 표시되지 않는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="978c2-141">Why does the drive on my cloud service VM show very little free disk space?</span></span>
<span data-ttu-id="978c2-142">이 동작은 정상적이며 응용 프로그램에 문제가 발생하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-142">This is expected behavior, and it shouldn't cause any issue to your application.</span></span> <span data-ttu-id="978c2-143">저널은 Azure PaaS VM에서 %uproot% 드라이브에 설정되며 이 기능은 기본적으로 파일이 차지하는 공간의 두 배를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-143">Journaling is turned on for the %uproot% drive in Azure PaaS VMs, which essentially consumes double the amount of space that files normally take up.</span></span> <span data-ttu-id="978c2-144">그러나 이를 사소하게 만드는 몇 가지 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-144">However there are several things to be aware of that essentially turn this into a non-issue.</span></span>

<span data-ttu-id="978c2-145">%approot% 드라이브 크기는 <.cspkg 크기 + 최대 저널 크기 + 여유 공간의 여백> 또는 1.5GB 중 더 큰 값으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-145">The %approot% drive size is calculated as <size of .cspkg + max journal size + a margin of free space>, or 1.5 GB, whichever is larger.</span></span> <span data-ttu-id="978c2-146">VM의 크기는 이 계산과 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-146">The size of your VM has no bearing on this calculation.</span></span> <span data-ttu-id="978c2-147">(VM 크기는 임시 C: 드라이브의 크기에 영향을 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="978c2-147">(The VM size only affects the size of the temporary C: drive.)</span></span> 

<span data-ttu-id="978c2-148">%approot% 드라이브에 작성하도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-148">It is unsupported to write to the %approot% drive.</span></span> <span data-ttu-id="978c2-149">Azure VM에 작성하는 경우 임시 LocalStorage 리소스에서 수행해야 합니다(또는 Blob Storage, Azure Files 등과 같은 다른 옵션).</span><span class="sxs-lookup"><span data-stu-id="978c2-149">If you are writing to the Azure VM, you must do so in a temporary LocalStorage resource (or other option, such as Blob storage, Azure Files, etc.).</span></span> <span data-ttu-id="978c2-150">따라서 %approot% 폴더에서 사용 가능한 공간의 크기는 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-150">So the amount of free space on the %approot% folder is not meaningful.</span></span> <span data-ttu-id="978c2-151">응용 프로그램을 %approot% 드라이브에 작성하는지 확실하지 않은 경우 몇 일 동안 서비스를 실행한 다음 "이전" 및 "이후" 크기를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-151">If you are not sure if your application is writing to the %approot% drive, you can always let your service run for a few days and then compare the "before" and "after" sizes.</span></span> 

<span data-ttu-id="978c2-152">Azure에서는 %approot% 드라이브에 아무 것도 작성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-152">Azure will not write anything to the %approot% drive.</span></span> <span data-ttu-id="978c2-153">.cspkg에서 VHD가 생성되고 Azure VM에 탑재되면 이 드라이브에 작성될 수 있는 유일한 항목은 사용자의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-153">Once the VHD is created from your .cspkg and mounted into the Azure VM, the only thing that might write to this drive is your application.</span></span> 

<span data-ttu-id="978c2-154">저널 설정을 구성할 수 없으므로 끌 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-154">The journal settings are non-configurable, so you can't turn it off.</span></span>

## <a name="what-are-the-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a><span data-ttu-id="978c2-155">Azure 기본 IPS/IDS와 DDoS에서 제공하는 기능이란?</span><span class="sxs-lookup"><span data-stu-id="978c2-155">What are the features and capabilities that Azure basic IPS/IDS and DDOS provides?</span></span>
<span data-ttu-id="978c2-156">Azure에는 위협으로부터 보호하기 위해 데이터 센터 실제 서버에 있는 IP/ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-156">Azure has IPS/IDS in datacenter physical servers to defend against threats.</span></span> <span data-ttu-id="978c2-157">또한 고객은 웹 응용 프로그램 방화벽, 네트워크 방화벽, 맬웨어 방지 프로그램, 침입 감지 및 방지 시스템(IDS/IPS) 등과 같은 타사 보안 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-157">In addition, customers can deploy third-party security solutions, such as web application firewalls, network firewalls, antimalware, intrusion detection, prevention systems (IDS/IPS), and more.</span></span> <span data-ttu-id="978c2-158">자세한 내용은 [데이터 및 자산 보호 및 글로벌 보안 표준 준수](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-158">For more information, see [Protect your data and assets and comply with global security standards](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).</span></span>

<span data-ttu-id="978c2-159">Microsoft에서는 서버, 네트워크 및 응용 프로그램을 지속적으로 모니터링하여 위협을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-159">Microsoft continuously monitors servers, networks, and applications to detect threats.</span></span> <span data-ttu-id="978c2-160">Azure의 다면적 위협 관리 접근 방식은 침입 감지, DDoS(Distributed Denial-of-Service) 공격 방지, 침투 테스트, 동작 분석, 이상 감지 및 Machine Learning을 사용하여 방어를 지속적으로 강화하고 위험을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-160">Azure's multipronged threat-management approach uses intrusion detection, distributed denial-of-service (DDoS) attack prevention, penetration testing, behavioral analytics, anomaly detection, and machine learning to constantly strengthen its defense and reduce risks.</span></span> <span data-ttu-id="978c2-161">Azure용 Microsoft 맬웨어 방지 프로그램은 Azure Cloud Services 및 가상 컴퓨터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-161">Microsoft Antimalware for Azure protects Azure cloud services and virtual machines.</span></span> <span data-ttu-id="978c2-162">웹 응용 프로그램 방화벽, 네트워크 방화벽, 맬웨어 방지 프로그램, 침입 감지 및 방지 시스템(IDS/IPS) 등과 같은 타사 보안 솔루션을 배포하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-162">You have the option to deploy third-party security solutions in addition, such as web application fire walls, network firewalls, antimalware, intrusion detection and prevention systems (IDS/IPS), and more.</span></span>

## <a name="why-does-iis-stop-writing-to-the-log-directory"></a><span data-ttu-id="978c2-163">IIS에서 로그 디렉터리에 작성을 중지하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="978c2-163">Why does IIS stop writing to the log directory?</span></span>
<span data-ttu-id="978c2-164">로그 디렉터리에 작성할 로컬 저장소 할당량을 모두 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-164">You have exhausted the local storage quota for writing to the log directory.</span></span><span data-ttu-id="978c2-165"> 이를 수정하기 위해 다음 세 가지 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-165"> To correct this, you can do one of three things:</span></span>
* <span data-ttu-id="978c2-166">IIS에 진단을 사용하도록 설정하고 진단을 주기적으로 Blob Storage에 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-166">Enable diagnostics for IIS and have the diagnostics periodically moved to blob storage.</span></span>
* <span data-ttu-id="978c2-167">로깅 디렉터리에서 로그 파일을 수동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-167">Manually remove log files from the logging directory.</span></span>
* <span data-ttu-id="978c2-168">로컬 리소스에 대한 할당량 제한을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-168">Increase quota limit for local resources.</span></span>

<span data-ttu-id="978c2-169">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-169">For more information, see the following documents:</span></span>
* [<span data-ttu-id="978c2-170">Azure Storage에서 진단 데이터 저장 및 보기</span><span class="sxs-lookup"><span data-stu-id="978c2-170">Store and view diagnostic data in Azure Storage</span></span>](cloud-services-dotnet-diagnostics-storage.md)
* [<span data-ttu-id="978c2-171">클라우드 서비스에서 IIS 로그 작성 중지</span><span class="sxs-lookup"><span data-stu-id="978c2-171">IIS Logs stops writing in cloud service</span></span>](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-the-purpose-of-the-windows-azure-tools-encryption-certificate-for-extensions"></a><span data-ttu-id="978c2-172">"확장을 위한 Windows Azure Tools 암호화 인증서"의 목적은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="978c2-172">What is the purpose of the "Windows Azure Tools Encryption Certificate for Extensions"?</span></span>
<span data-ttu-id="978c2-173">이러한 인증서는 클라우드 서비스에 확장명을 추가할 때마다 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-173">These certificates are automatically created whenever an extension is added to the cloud service.</span></span> <span data-ttu-id="978c2-174">가장 일반적으로 WAD 확장 또는 RDP 확장이지만 맬웨어 방지 또는 로그 수집기 확장과 같은 다른 항목일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-174">Most commonly, this is the WAD extension or the RDP extension, but it could be others, such as the Antimalware or Log Collector extension.</span></span> <span data-ttu-id="978c2-175">이러한 인증서는 확장을 위해 개인 구성을 암호화하고 암호 해독하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-175">These certificates are only used for encrypting and decrypting the private configuration for the extension.</span></span> <span data-ttu-id="978c2-176">만료 날짜를 확인하지 않으므로 인증서가 만료되는지는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-176">The expiration date is never checked, so it doesn’t matter if the certificate is expired.</span></span> 

<span data-ttu-id="978c2-177">이러한 인증서를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-177">You can ignore these certificates.</span></span> <span data-ttu-id="978c2-178">인증서를 정리하려면 모두 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-178">If you want to clean up the certificates, you can try deleting them all.</span></span> <span data-ttu-id="978c2-179">Azure에서 사용 중인 인증서를 삭제하려면 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-179">Azure will throw an error if you try to delete a certificate that is in use.</span></span>

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-to-the-instance"></a><span data-ttu-id="978c2-180">"RDP"하지 않고 인스턴스에서 CSR(인증서 서명 요청)을 생성하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="978c2-180">How can I generate a Certificate Signing Request (CSR) without "RDP-ing" in to the instance?</span></span>
<span data-ttu-id="978c2-181">다음 지침 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978c2-181">See the following guidance document:</span></span>

>[<span data-ttu-id="978c2-182">WAWS(Windows Azure 웹 사이트)를 사용하기 위해 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="978c2-182">Obtaining a certificate for use with Windows Azure Web Sites (WAWS)</span></span>](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

<span data-ttu-id="978c2-183">CSR은 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-183">Please note that a CSR is just a text file.</span></span> <span data-ttu-id="978c2-184">인증서를 궁극적으로 사용하는 컴퓨터에서 만들어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-184">It does NOT have to be created from the machine where the certificate will ultimately be used.</span></span><span data-ttu-id="978c2-185"> 이 문서가 App Service를 위해 작성되었지만 CSR 생성은 일반적이며 Cloud Services에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="978c2-185"> Although this document is written for an App Service, the CSR creation is generic and applies also for Cloud Services.</span></span>
