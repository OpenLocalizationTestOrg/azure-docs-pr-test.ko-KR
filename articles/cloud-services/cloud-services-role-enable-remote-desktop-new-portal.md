---
title: "Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용 | Microsoft Docs"
description: "원격 데스크톱 연결을 허용하기 위해 Azure 클라우드 서비스 응용 프로그램을 구성하는 방법"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="10ce1-103">Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="10ce1-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10ce1-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="10ce1-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="10ce1-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="10ce1-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="10ce1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10ce1-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="10ce1-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10ce1-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="10ce1-108">원격 데스크톱을 사용하면 Azure에서 실행 중인 역할의 데스크톱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="10ce1-109">원격 데스크톱 연결을 사용하여 응용 프로그램 실행 중에 응용 프로그램 문제를 진단하고 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="10ce1-110">서비스 정의에 원격 데스크톱 모듈을 포함하여 개발 중에 원격 데스크톱 연결을 사용하도록 설정하거나 원격 데스크톱 확장을 통해 원격 데스크톱을 사용 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="10ce1-111">권장되는 방법은 원격 데스크톱 확장을 사용하는 것입니다. 이 방법을 사용하면 응용 프로그램이 배포된 후에도 응용 프로그램을 다시 배포할 필요 없이 원격 데스크톱을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="10ce1-112">Azure Portal에서 원격 데스크톱 구성</span><span class="sxs-lookup"><span data-stu-id="10ce1-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="10ce1-113">Azure Portal에서는 응용 프로그램이 배포된 후에도 원격 데스크톱을 사용 가능하게 설정할 수 있도록 원격 데스크톱 확장 접근 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="10ce1-114">클라우드 서비스의 **원격 데스크톱** 블레이드에서 원격 데스크톱을 사용하도록 설정하거나 가상 컴퓨터에 연결하는 데 사용되는 로컬 관리자 계정, 인증에 사용되는 인증서를 변경하고 만료 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="10ce1-115">**클라우드 서비스**, 클라우드 서비스의 이름, **원격 데스크톱**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="10ce1-117">개별 역할 또는 모든 역할 중 어떤 범주에 대해 원격 데스크톱을 사용하도록 설정할지 선택한 후 전환기의 값을 **Enabled**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="10ce1-118">사용자 이름, 암호, 만료 및 인증서에 대한 필수 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="10ce1-120">처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="10ce1-121">다시 부팅되지 않도록 하려면 암호를 암호화하는 데 사용되는 인증서가 역할에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="10ce1-122">다시 시작되지 않도록 하려면 [클라우드 서비스에 대 한 인증서를 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 하고 이 대화 상자로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="10ce1-123">**역할**에서 업데이트할 역할을 선택하거나 모든 역할을 선택하려면 **모두**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="10ce1-124">구성 업데이트를 마치면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="10ce1-125">역할 인스턴스가 연결을 수신할 준비가 되기까지 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="10ce1-126">원격으로 역할 인스턴스 액세스</span><span class="sxs-lookup"><span data-stu-id="10ce1-126">Remote into role instances</span></span>
<span data-ttu-id="10ce1-127">역할에 대해 원격 데스크톱이 사용 가능하게 설정되면 Azure Portal에서 직접 연결을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="10ce1-128">**인스턴스**를 클릭하여 **인스턴스** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="10ce1-129">원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="10ce1-130">**연결**을 클릭하여 역할 인스턴스에 대한 RDP 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="10ce1-132">**열기**를 클릭한 후 **연결**을 클릭하여 원격 데스크톱 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="10ce1-133">클라우드 서비스가 NSG 뒤에 있는 경우 포트 **3389** 및 **20000**의 트래픽을 허용하는 규칙을 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="10ce1-134">원격 데스크톱은 포트 **3389**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="10ce1-135">클라우드 서비스 인스턴스에서 부하가 분산되므로 연결할 인스턴스를 직접 제어할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="10ce1-136">*RemoteForwarder* 및 *RemoteAccess* 에이전트가 RDP 트래픽을 관리하고 클라이언트에서 RDP 쿠키를 전송하고 연결할 개별 인스턴스를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="10ce1-137">*RemoteForwarder* 및 *RemoteAccess* 에이전트를 사용하려면 포트 **20000***이 열려 있어야 합니다. 이 포트는 NSG가 있으면 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10ce1-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="10ce1-138">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="10ce1-138">Additional resources</span></span>

<span data-ttu-id="10ce1-139">[Cloud Services를 구성하는 방법](cloud-services-how-to-configure.md)
[Cloud Services FAQ - 원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="10ce1-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
