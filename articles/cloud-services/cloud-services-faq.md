---
title: "Azure Cloud Services 역할 FAQ | Microsoft Docs"
description: "Azure Cloud Services에 대한 질문과 대답입니다. 인증서, 웹 역할 및 작업자 역할에 대한 몇 가지 일반적인 질문의 답변이 제공됩니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="4bc4f-104">클라우드 서비스 FAQ</span><span class="sxs-lookup"><span data-stu-id="4bc4f-104">Cloud Services FAQ</span></span>
<span data-ttu-id="4bc4f-105">이 문서는 Microsoft Azure 클라우드 서비스에 대한 일부 자주 묻는 질문을 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="4bc4f-106">또한 일반적인 Azure 가격 책정 및 지원 정보는 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) 를 방문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="4bc4f-107">크기 정보는 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="4bc4f-108">인증서</span><span class="sxs-lookup"><span data-stu-id="4bc4f-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="4bc4f-109">어디에 내 인증서를 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="4bc4f-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="4bc4f-110">**내**</span><span class="sxs-lookup"><span data-stu-id="4bc4f-110">**My**</span></span>  
  <span data-ttu-id="4bc4f-111">개인 키를 포함한 응용 프로그램 인증서(\*.pfx, \*.p12)</span><span class="sxs-lookup"><span data-stu-id="4bc4f-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="4bc4f-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="4bc4f-112">**CA**</span></span>  
  <span data-ttu-id="4bc4f-113">모든 중간 인증서를 이 저장소(정책 및 하위 CA)로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="4bc4f-114">**루트**</span><span class="sxs-lookup"><span data-stu-id="4bc4f-114">**ROOT**</span></span>  
  <span data-ttu-id="4bc4f-115">루트 CA 저장소이므로 기본 루트 CA 인증서를 여기로 이동시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="4bc4f-116">만료된 인증서를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-116">I can't remove expired certificate</span></span>
<span data-ttu-id="4bc4f-117">Azure에서는 사용 중인 인증서를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="4bc4f-118">인증서를 사용하는 배포를 삭제하거나 다른 또는 갱신된 인증서로 배포를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="4bc4f-119">만료된 인증서 삭제</span><span class="sxs-lookup"><span data-stu-id="4bc4f-119">Delete an expired certificate</span></span>
<span data-ttu-id="4bc4f-120">인증서를 사용하지 않으면 [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet을 사용하여 인증서를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="4bc4f-121">확장명이 Windows Azure 서비스 관리라는 인증서가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="4bc4f-122">이러한 인증서는 원격 데스크톱 확장과 같은 클라우드 서비스에 확장명을 추가할 때마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="4bc4f-123">이러한 인증서는 확장명의 개인 구성을 암호화하고 암호 해독하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="4bc4f-124">이러한 인증서가 만료되는 경우 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="4bc4f-125">만료 날짜를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="4bc4f-126">삭제한 인증서가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="4bc4f-127">대개 Visual Studio와 같은 사용 중인 도구 때문에 계속 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="4bc4f-128">인증서를 사용하는 도구에 다시 연결할 때마다 다시 Azure에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="4bc4f-129">내 인증서가 자꾸 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-129">My certificates keep disappearing</span></span>
<span data-ttu-id="4bc4f-130">가상 컴퓨터 인스턴스가 재활용되면 모든 로컬 변경 내용이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="4bc4f-131">[시작 태스크](cloud-services-startup-tasks.md) 를 사용하여 역할이 시작될 때마다 가상 컴퓨터에 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="4bc4f-132">포털에서 내 관리 인증서를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="4bc4f-133">[관리 인증서](../azure-api-management-certs.md) Azure 클래식 포털에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="4bc4f-134">현재의 Azure 포털에서는 관리 인증서를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="4bc4f-135">어떻게 하면 관리 인증서를 사용하지 않도록 설정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4bc4f-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="4bc4f-136">[관리 인증서](../azure-api-management-certs.md) 는 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="4bc4f-137">더 이상 사용되게 하지 않으려면 Azure 클래식 포털을 통해 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="4bc4f-138">특정 IP 주소에 대한 SSL 인증서를 만들려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4bc4f-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="4bc4f-139">[인증서 만들기 자습서](cloud-services-certs-create.md)에 나오는 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="4bc4f-140">IP 주소를 DNS 이름으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="4bc4f-141">보안</span><span class="sxs-lookup"><span data-stu-id="4bc4f-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="4bc4f-142">SSL 3.0 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="4bc4f-142">Disable SSL 3.0</span></span>
<span data-ttu-id="4bc4f-143">SSL 3.0을 사용하지 않도록 설정하고 TLS 보안을 사용하려면 https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/ 블로그 게시물에 설명되어 있는 시작 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="4bc4f-144">웹 사이트에 **nosniff** 추가</span><span class="sxs-lookup"><span data-stu-id="4bc4f-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="4bc4f-145">클라이언트가 MIME 형식을 스니핑하지 않도록 하려면 *web.config* 파일에 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="4bc4f-146">IIS에서 설정으로도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="4bc4f-147">[일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서의 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="4bc4f-148">웹 역할에 대해 IIS 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4bc4f-148">Customize IIS for a web role</span></span>
<span data-ttu-id="4bc4f-149">[일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서의 IIS 시작 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="4bc4f-150">확장</span><span class="sxs-lookup"><span data-stu-id="4bc4f-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="4bc4f-151">X 인스턴스 이상 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="4bc4f-152">사용자의 Azure 구독은 사용할 수 있는 코어 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="4bc4f-153">사용 가능한 모든 코어를 사용하는 경우 크기 조정은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="4bc4f-154">예를 들어 100개의 코어 제한이 있으면 클라우드 서비스에 대한 100개의 A1 크기 가상 컴퓨터 인스턴스나 50개의 A2 크기 가상 컴퓨터 인스턴스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="4bc4f-155">네트워킹</span><span class="sxs-lookup"><span data-stu-id="4bc4f-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="4bc4f-156">여러 VIP 클라우드 서비스에서 IP를 예약할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="4bc4f-157">우선, IP를 예약하려고 하는 가상 컴퓨터 인스턴스가 켜져 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="4bc4f-158">다음으로, 스테이징 및 프로덕션 배포 모두에 대해 예약된 IP를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="4bc4f-159">**않습니다** .</span><span class="sxs-lookup"><span data-stu-id="4bc4f-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="4bc4f-160">원격 데스크톱</span><span class="sxs-lookup"><span data-stu-id="4bc4f-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="4bc4f-161">NSG가 있을 때 원격 데스크톱을 어떻게 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="4bc4f-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="4bc4f-162">포트 **3389** 및 **20000**에서 트래픽을 허용하는 규칙을 NSG에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="4bc4f-163">원격 데스크톱은 포트 **3389**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="4bc4f-164">클라우드 서비스 인스턴스에서 부하가 분산되므로 연결할 인스턴스를 직접 제어할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="4bc4f-165">*RemoteForwarder* 및 *RemoteAccess* 에이전트가 RDP 트래픽을 관리하고 클라이언트에서 RDP 쿠키를 전송하고 연결할 개별 인스턴스를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="4bc4f-166">*RemoteForwarder* 및 *RemoteAccess* 에이전트를 사용하려면 포트 **20000***이 열려 있어야 합니다. 이 포트는 NSG가 있으면 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bc4f-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
