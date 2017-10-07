---
title: "Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결 aaaEnable | Microsoft Docs"
description: "어떻게 tooconfigure azure 클라우드 서비스 응용 프로그램 tooallow 원격 데스크톱 연결"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="81127-103">Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="81127-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81127-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="81127-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="81127-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="81127-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="81127-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81127-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="81127-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="81127-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="81127-108">원격 데스크톱 사용 하면 Azure에서 실행 중인 역할의 tooaccess hello 데스크톱 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="81127-109">원격 데스크톱 연결 tootroubleshoot를 사용할 수 있으며 실행 되는 동안 응용 프로그램 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="81127-110">서비스 정의에 hello 원격 데스크톱 모듈을 포함 하 여 개발 하는 동안 원격 데스크톱 연결 사용자 역할에 사용할 수 또는 원격 데스크톱 확장 hello 통해 원격 데스크톱 tooenable를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="81127-111">hello 선호 되는 방법은 toouse hello 원격 데스크톱 확장 hello tooredeploy 응용 프로그램 필요 없이 배포 된 후에 원격 데스크톱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="81127-112">Hello Azure 포털에서에서 원격 데스크톱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="81127-113">Azure 포털 hello hello 원격 데스크톱 확장 방법을 사용 하 여 hello 응용 프로그램을 배포 후에 원격 데스크톱을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="81127-114">hello **원격 데스크톱** 클라우드 서비스에 대 한 블레이드 tooenable 원격 데스크톱을 사용 하면, tooconnect toohello 가상 컴퓨터를 사용 하는 변경 hello 로컬 관리자 계정, hello 인증서 인증에 사용 하 고 hello 설정 만료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="81127-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="81127-115">클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="81127-117">선택한 모든 역할 또는 개별 역할에 대 한 원격 데스크톱 tooenable 원하는 여부 후 hello 전환기의 hello 값도 변경**Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="81127-118">사용자 이름, 암호, 만료, 및 인증서에 대 한 hello 필수 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="81127-120">처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="81127-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="81127-121">다시 부팅 hello 인증서 사용 되는 tooencrypt hello 암호 tooprevent hello 역할에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="81127-122">tooprevent 다시 시작을 [hello 클라우드 서비스에 대 한 인증서 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 다음 toothis 대화를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="81127-123">**역할**선택, 선택 하거나 tooupdate hello 역할 **모든** 모든 역할에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="81127-124">구성 업데이트를 마치면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="81127-125">사용자의 역할 인스턴스가 준비 tooreceive 연결 하기 전에 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="81127-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="81127-126">원격으로 역할 인스턴스 액세스</span><span class="sxs-lookup"><span data-stu-id="81127-126">Remote into role instances</span></span>
<span data-ttu-id="81127-127">Hello 역할에 원격 데스크톱 활성화 되 면 hello Azure 포털에서 직접 연결을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="81127-128">클릭 **인스턴스** tooopen hello **인스턴스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81127-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="81127-129">원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="81127-130">클릭 **연결** toodownload는 RDP hello 역할 인스턴스에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="81127-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="81127-132">클릭 **열려** 차례로 **연결** toostart hello 원격 데스크톱 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="81127-133">클라우드 서비스 NSG 뒤 대기 중임을 하는 경우에 포트에서 트래픽을 허용 하는 toocreate 규칙을 할 수 있습니다 **3389** 및 **20000**합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="81127-134">원격 데스크톱은 포트 **3389**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="81127-135">클라우드 서비스 인스턴스 부하 분산이 되므로 어떤 인스턴스 tooconnect을 직접 제어할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="81127-136">hello *RemoteForwarder* 및 *RemoteAccess* 에이전트 RDP 트래픽을 관리 하 고 hello 클라이언트 toosend RDP 쿠키를 허용 및는 개별 인스턴스 tooconnect를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81127-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="81127-137">hello *RemoteForwarder* 및 *RemoteAccess* 에이전트에 해당 포트 필요 **20000*** 열 수 있는 NSG 있는 경우 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81127-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81127-138">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="81127-138">Additional resources</span></span>

<span data-ttu-id="81127-139">[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="81127-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
