---
title: "클라우드 서비스 역할 aaaAzure FAQ | Microsoft Docs"
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="cceeb-104">클라우드 서비스 FAQ</span><span class="sxs-lookup"><span data-stu-id="cceeb-104">Cloud Services FAQ</span></span>
<span data-ttu-id="cceeb-105">이 문서는 Microsoft Azure 클라우드 서비스에 대한 일부 자주 묻는 질문을 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="cceeb-106">Hello를 방문할 수도 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) 일반적인 Azure 가격 책정 및 지원 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="cceeb-107">Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="cceeb-108">인증서</span><span class="sxs-lookup"><span data-stu-id="cceeb-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="cceeb-109">어디에 내 인증서를 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cceeb-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="cceeb-110">**내**</span><span class="sxs-lookup"><span data-stu-id="cceeb-110">**My**</span></span>  
  <span data-ttu-id="cceeb-111">개인 키를 포함한 응용 프로그램 인증서(\*.pfx, \*.p12)</span><span class="sxs-lookup"><span data-stu-id="cceeb-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="cceeb-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="cceeb-112">**CA**</span></span>  
  <span data-ttu-id="cceeb-113">모든 중간 인증서를 이 저장소(정책 및 하위 CA)로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="cceeb-114">**루트**</span><span class="sxs-lookup"><span data-stu-id="cceeb-114">**ROOT**</span></span>  
  <span data-ttu-id="cceeb-115">기본 루트 CA 인증서 여기로 이동 해야 하므로 hello 루트 CA 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="cceeb-116">만료된 인증서를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-116">I can't remove expired certificate</span></span>
<span data-ttu-id="cceeb-117">Azure에서는 사용 중인 인증서를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="cceeb-118">Hello 인증서를 사용 하는 tooeither delete hello 배포 또는 다른 또는 갱신 된 인증서로 업데이트 hello 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="cceeb-119">만료된 인증서 삭제</span><span class="sxs-lookup"><span data-stu-id="cceeb-119">Delete an expired certificate</span></span>
<span data-ttu-id="cceeb-120">Hello hello 인증서가 사용 하 여에으로 사용할 수 있습니다 [제거 AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="cceeb-121">확장명이 Windows Azure 서비스 관리라는 인증서가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="cceeb-122">이러한 인증서는 확장 hello 원격 데스크톱 확장 같은 toohello 클라우드 서비스에 추가 될 때마다 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="cceeb-123">이러한 인증서는 암호화 및 해독 hello hello 확장 개인 구성에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="cceeb-124">이러한 인증서가 만료되는 경우 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="cceeb-125">hello 만료 날짜를 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="cceeb-126">삭제한 인증서가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="cceeb-127">대개 Visual Studio와 같은 사용 중인 도구 때문에 계속 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="cceeb-128">인증서를 사용 하는 도구와 다시 연결 될 때마다 다시 업로드 tooAzure 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="cceeb-129">내 인증서가 자꾸 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-129">My certificates keep disappearing</span></span>
<span data-ttu-id="cceeb-130">Hello 가상 컴퓨터 인스턴스를 재활용할 때 모든 로컬 변경 내용이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="cceeb-131">사용 하 여 한 [시작 작업](cloud-services-startup-tasks.md) tooinstall 인증서 toohello 가상 컴퓨터가 각 시간 hello 역할 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="cceeb-132">Hello 포털에서 관리 인증서를 찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="cceeb-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="cceeb-133">[관리 인증서](../azure-api-management-certs.md) 은 hello Azure 클래식 포털에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="cceeb-134">hello 현재 Azure 포털에서 관리 인증서를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="cceeb-135">어떻게 하면 관리 인증서를 사용하지 않도록 설정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cceeb-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="cceeb-136">[관리 인증서](../azure-api-management-certs.md) 는 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="cceeb-137">삭제할 hello Azure 클래식 포털을 통해 수 없도록 할 때 toobe 더 이상 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="cceeb-138">특정 IP 주소에 대한 SSL 인증서를 만들려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="cceeb-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="cceeb-139">Hello의 지시를 hello [인증서 자습서 만들](cloud-services-certs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="cceeb-140">DNS 이름 hello hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="cceeb-141">보안</span><span class="sxs-lookup"><span data-stu-id="cceeb-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="cceeb-142">SSL 3.0 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="cceeb-142">Disable SSL 3.0</span></span>
<span data-ttu-id="cceeb-143">toodisable SSL 3.0 및 TLS 보안 사용이 블로그 게시물에 설명 되어 있는 시작 작업을 만듭니다: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="cceeb-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="cceeb-144">추가 **nosniff** tooyour 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="cceeb-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="cceeb-145">hello MIME 형식이 감지 로부터 tooprevent 클라이언트에 설정을 추가 하면 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="cceeb-146">IIS에서 설정으로도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="cceeb-147">Hello로 사용 하 여 hello 다음 명령은 [일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서.</span><span class="sxs-lookup"><span data-stu-id="cceeb-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="cceeb-148">웹 역할에 대해 IIS 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="cceeb-148">Customize IIS for a web role</span></span>
<span data-ttu-id="cceeb-149">Hello에서 hello IIS 시작 스크립트를 사용 하 여 [일반적인 시작 작업](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) 문서.</span><span class="sxs-lookup"><span data-stu-id="cceeb-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="cceeb-150">확장</span><span class="sxs-lookup"><span data-stu-id="cceeb-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="cceeb-151">X 인스턴스 이상 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="cceeb-152">Azure 구독에 코어를 사용할 수 있습니다 hello 수에 대 한 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="cceeb-153">사용 가능한 모든 hello 코어를 사용한 경우 배율이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="cceeb-154">예를 들어 100개의 코어 제한이 있으면 클라우드 서비스에 대한 100개의 A1 크기 가상 컴퓨터 인스턴스나 50개의 A2 크기 가상 컴퓨터 인스턴스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="cceeb-155">네트워킹</span><span class="sxs-lookup"><span data-stu-id="cceeb-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="cceeb-156">여러 VIP 클라우드 서비스에서 IP를 예약할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="cceeb-157">먼저, tooreserve hello IP를 만들려고 하는 hello 가상 컴퓨터 인스턴스의 켜져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="cceeb-158">둘째, 여기 hello 스테이징 및 프로덕션 배포에 대 한 예약 된 Ip를 사용 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="cceeb-159">**없는** hello 배포를 업그레이드 하는 동안 hello 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="cceeb-160">원격 데스크톱</span><span class="sxs-lookup"><span data-stu-id="cceeb-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="cceeb-161">NSG가 있을 때 원격 데스크톱을 어떻게 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="cceeb-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="cceeb-162">포트에서 트래픽을 허용 하는 NSG 규칙 toohello 추가 **3389** 및 **20000**합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="cceeb-163">원격 데스크톱은 포트 **3389**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="cceeb-164">클라우드 서비스 인스턴스 부하 분산이 되므로 어떤 인스턴스 tooconnect을 직접 제어할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="cceeb-165">hello *RemoteForwarder* 및 *RemoteAccess* 에이전트 RDP 트래픽을 관리 하 고 hello 클라이언트 toosend RDP 쿠키를 허용 및는 개별 인스턴스 tooconnect를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="cceeb-166">hello *RemoteForwarder* 및 *RemoteAccess* 에이전트에 해당 포트 필요 **20000*** 열 수 있는 NSG 있는 경우 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceeb-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
