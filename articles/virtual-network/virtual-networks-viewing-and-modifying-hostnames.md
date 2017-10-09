---
title: "aaaViewing 호스트 이름이 수정 | Microsoft Docs"
description: "Azure 가상 컴퓨터에 대 한 tooview 및 변경 hostnames 웹 방식 및 이름 확인에 대 한 작업자 역할"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="7ef54-103">호스트 이름 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="7ef54-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="7ef54-104">호스트 이름으로 참조 되는 역할 인스턴스 toobe tooallow, 각 역할에 대 한 hello 서비스 구성 파일에서 hello 호스트 이름에 대 한 hello 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-104">tooallow your role instances toobe referenced by host name, you must set hello value for hello host name in hello service configuration file for each role.</span></span> <span data-ttu-id="7ef54-105">Hello 필요한 호스트 이름 toohello를 추가 하 여 그렇게 **vmName** hello 특성 **역할** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-105">You do that by adding hello desired host name toohello **vmName** attribute of hello **Role** element.</span></span> <span data-ttu-id="7ef54-106">값의 hello hello **vmName** 특성은 각 역할 인스턴스의 호스트 이름 hello에 대 한 기준으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-106">hello value of hello **vmName** attribute is used as a base for hello host name of each role instance.</span></span> <span data-ttu-id="7ef54-107">예를 들어 경우 **vmName** 은 *webrole* 해당 역할의 인스턴스가 hello 인스턴스의 호스트 이름을 hello 됩니다 *webrole0*, *webrole1* , 및 *webrole2*합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-107">For example, if **vmName** is *webrole* and there are three instances of that role, hello host names of hello instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="7ef54-108">가상 컴퓨터에 대 한 호스트 이름을 hello hello 가상 컴퓨터 이름에 따라 채워집니다. 때문에 toospecify hello 구성 파일에서 가상 컴퓨터에 대 한 호스트 이름을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-108">You do not need toospecify a host name for virtual machines in hello configuration file, because hello host name for a virtual machine is populated based on hello virtual machine name.</span></span> <span data-ttu-id="7ef54-109">Microsoft Azure 서비스 구성에 대한 자세한 내용은 [Azure 서비스 구성 스키마(.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="7ef54-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="7ef54-110">호스트 이름 보기</span><span class="sxs-lookup"><span data-stu-id="7ef54-110">Viewing hostnames</span></span>
<span data-ttu-id="7ef54-111">아래의 hello 도구 중 하나를 사용 하 여 클라우드 서비스에서 가상 컴퓨터와 역할 인스턴스 hello 호스트 이름을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-111">You can view hello host names of virtual machines and role instances in a cloud service by using any of hello tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7ef54-112">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7ef54-112">Azure Portal</span></span>
<span data-ttu-id="7ef54-113">Hello를 사용할 수 있습니다 [Azure 포털](http://portal.azure.com) hello 개요 블레이드에 가상 컴퓨터에 가상 컴퓨터에 대 한 tooview hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-113">You can use hello [Azure portal](http://portal.azure.com) tooview hello host names for virtual machines on hello overview blade for a virtual machine.</span></span> <span data-ttu-id="7ef54-114">에 대 한 값을 표시 하는 hello 블레이드 있음을 명심 **이름** 및 **호스트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-114">Keep in mind that hello blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="7ef54-115">Hello 호스트 이름 변경 동일 hello 처음 경우도 있지만 hello hello 가상 컴퓨터나 역할 인스턴스 이름을 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-115">Although they are initially hello same, changing hello host name will not change hello name of hello virtual machine or role instance.</span></span>

<span data-ttu-id="7ef54-116">Hello Azure 포털에서에서 역할 인스턴스를 볼 수도 있습니다 하지만 클라우드 서비스의 hello 인스턴스를 나열 하는 경우 hello 호스트 이름이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-116">Role instances can also be viewed in hello Azure portal, but when you list hello instances in a cloud service, hello host name is not displayed.</span></span> <span data-ttu-id="7ef54-117">각 인스턴스의 이름을 표시 하지만 해당 이름 hello 호스트 이름을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-117">You will see a name for each instance, but that name does not represent hello host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="7ef54-118">서비스 구성 파일</span><span class="sxs-lookup"><span data-stu-id="7ef54-118">Service configuration file</span></span>
<span data-ttu-id="7ef54-119">Hello에서 배포 된 서비스에 대 한 hello 서비스 구성 파일을 다운로드할 수 있습니다 **구성** 블레이드 hello Azure 포털의에서 hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-119">You can download hello service configuration file for a deployed service from hello **Configure** blade of hello service in hello Azure portal.</span></span> <span data-ttu-id="7ef54-120">Hello에 대 한 확인할 수 있습니다 **vmName** hello에 대 한 특성 **역할 이름** 요소 toosee hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-120">You can then look for hello **vmName** attribute for hello **Role name** element toosee hello host name.</span></span> <span data-ttu-id="7ef54-121">각 역할 인스턴스의 호스트 이름 hello에 대 한이 호스트 이름은 기본으로 사용 됩니다 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-121">Keep in mind that this host name is used as a base for hello host name of each role instance.</span></span> <span data-ttu-id="7ef54-122">예를 들어 경우 **vmName** 은 *webrole* 해당 역할의 인스턴스가 hello 인스턴스의 호스트 이름을 hello 됩니다 *webrole0*, *webrole1* , 및 *webrole2*합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-122">For example, if **vmName** is *webrole* and there are three instances of that role, hello host names of hello instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="7ef54-123">원격 데스크톱</span><span class="sxs-lookup"><span data-stu-id="7ef54-123">Remote Desktop</span></span>
<span data-ttu-id="7ef54-124">원격 데스크톱 (Windows), Windows PowerShell 원격 (Windows) 또는 SSH (Linux / Windows) 연결 tooyour 가상 컴퓨터나 역할 인스턴스를 활성화 한 후에 다양 한 방법으로 활성 원격 데스크톱 연결에서 hello 호스트 이름을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections tooyour virtual machines or role instances, you can view hello host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="7ef54-125">Hello 명령 프롬프트 또는 SSH 터미널에 호스트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-125">Type hostname at hello command prompt or SSH terminal.</span></span>
* <span data-ttu-id="7ef54-126">Ipconfig를 입력/hello 명령에 모든 메시지 (Windows에만 해당)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-126">Type ipconfig /all at hello command prompt (Windows only).</span></span>
* <span data-ttu-id="7ef54-127">Hello 시스템 뷰 hello 컴퓨터 이름 설정 (Windows에만 해당).</span><span class="sxs-lookup"><span data-stu-id="7ef54-127">View hello computer name in hello system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="7ef54-128">Azure 서비스 관리 REST API</span><span class="sxs-lookup"><span data-stu-id="7ef54-128">Azure Service Management REST API</span></span>
<span data-ttu-id="7ef54-129">REST 클라이언트에서 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="7ef54-130">Azure 포털 클라이언트 인증서 tooconnect toohello 가졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-130">Ensure that you have a client certificate tooconnect toohello Azure portal.</span></span> <span data-ttu-id="7ef54-131">에 제공 된 hello 단계를 수행 하는 클라이언트 인증서를 tooobtain [하는 방법: 다운로드 및 게시 설정 가져오기 및 구독 정보](https://msdn.microsoft.com/library/dn385850.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-131">tooobtain a client certificate, follow hello steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="7ef54-132">값이 2013-11-01인 x-ms-version 헤더 항목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="7ef54-133">형식에 따라 hello에 요청을 보내고: https://management.core.windows.net/\<subscrition id\>/서비스/hostedservices/\<서비스 이름\>? 포함 세부 = true</span><span class="sxs-lookup"><span data-stu-id="7ef54-133">Send a request in hello following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="7ef54-134">Hello에 대 한 확인 **HostName** 요소 각각에 대해 **RoleInstance** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-134">Look for hello **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="7ef54-135">Hello를 확인 하 여 hello REST 호출 응답에서에서 클라우드 서비스에 대 한 hello 내부 도메인 접미사를 볼 수도 있습니다 **InternalDnsSuffix** 요소인 ipconfig를 실행 하 여/모두 (Windows), 원격 데스크톱 세션에서 명령 프롬프트에서에서 또는 또는 SSH 터미널 (Linux)에서 실행 중인 cat /etc/resolv.conf 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-135">You can also view hello internal domain suffix for your cloud service from hello REST call response by checking hello **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="7ef54-136">호스트 이름 수정</span><span class="sxs-lookup"><span data-stu-id="7ef54-136">Modifying a hostname</span></span>
<span data-ttu-id="7ef54-137">수정 된 서비스 구성 파일을 업로드 하거나 원격 데스크톱 세션에서 hello 컴퓨터 바꾸면 역할 인스턴스 또는 가상 컴퓨터에 대 한 hello 호스트 이름을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef54-137">You can modify hello host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming hello computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef54-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ef54-138">Next steps</span></span>
[<span data-ttu-id="7ef54-139">이름 확인(DNS)</span><span class="sxs-lookup"><span data-stu-id="7ef54-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="7ef54-140">Azure 서비스 구성 스키마(.cscfg)</span><span class="sxs-lookup"><span data-stu-id="7ef54-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="7ef54-141">Azure 가상 네트워크 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="7ef54-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="7ef54-142">네트워크 구성 파일을 사용하여 DNS 설정 지정</span><span class="sxs-lookup"><span data-stu-id="7ef54-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

