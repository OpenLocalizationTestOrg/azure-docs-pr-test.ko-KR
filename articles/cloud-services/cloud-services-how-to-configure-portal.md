---
title: "클라우드 서비스를 구성하는 방법(포털) | Microsoft Docs"
description: "Azure에서 Cloud Services를 구성하는 방법에 대해 알아봅니다. 또한 클라우드 서비스 구성을 업데이트하고 역할 인스턴스에 대한 원격 액세스를 구성하는 방법도 알아봅니다. 이 예제는 Azure Portal을 사용합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="aae03-105">Cloud Services를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="aae03-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aae03-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aae03-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="aae03-107">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="aae03-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="aae03-108">Azure Portal에서 클라우드 서비스에 가장 일반적으로 사용되는 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="aae03-109">또는 구성 파일을 직접 업데이트하려는 경우 업데이트할 서비스 구성 파일을 다운로드한 후 업데이트된 파일을 업로드하고 구성 변경 내용으로 클라우드 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="aae03-110">어느 방법이든 모든 역할 인스턴스에 구성 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="aae03-111">클라우드 서비스 역할의 인스턴스 또는 이에 대한 원격 데스크톱을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="aae03-112">Azure는 각 역할에 둘 이상의 역할 인스턴스가 있는 경우에만 구성 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="aae03-113">이에 따라, 가상 컴퓨터 하나는 클라이언트 요청을 처리하고 다른 하나는 업데이트를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="aae03-114">자세한 내용은 [Service Level Agreements(서비스 수준 약정)](https://azure.microsoft.com/support/legal/sla/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aae03-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="aae03-115">클라우드 서비스 변경</span><span class="sxs-lookup"><span data-stu-id="aae03-115">Change a cloud service</span></span>
<span data-ttu-id="aae03-116">[Azure Portal](https://portal.azure.com/)을 연 후 클라우드 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="aae03-117">여기에서 여러 항목을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-117">From here, you manage many aspects of it.</span></span>

![설정 페이지](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="aae03-119">**설정** 또는 **모든 설정** 링크를 클릭하면 **설정** 블레이드가 열리며 여기에서 **속성** 및 **구성**을 변경하고 **인증서**를 관리하며 **경고 규칙**을 설정하고 이 클라우드 서비스에 액세스하는 **사용자**를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Azure 클라우드 서비스 설정 블레이드](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="aae03-121">게스트 OS 버전 관리</span><span class="sxs-lookup"><span data-stu-id="aae03-121">Manage Guest OS version</span></span>

<span data-ttu-id="aae03-122">기본적으로 Azure는 Windows Server 2016 같은 게스트 OS를 서비스 구성(.cscfg)에 지정한 OS 제품군 내에서 지원되는 최신 이미지로 주기적으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="aae03-123">특정 OS 버전을 대상으로 해야 하는 경우 **구성** 블레이드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![OS 버전 설정](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="aae03-125">특정 OS 버전을 선택하면 자동 OS 업데이트가 사용되지 않도록 설정되며 패치는 사용자가 책임지고 진행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="aae03-126">즉, 역할 인스턴스가 업데이트를 수신하도록 해야 합니다. 그러지 않으면 응용 프로그램이 보안 취약점에 노출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="aae03-127">모니터링</span><span class="sxs-lookup"><span data-stu-id="aae03-127">Monitoring</span></span>
<span data-ttu-id="aae03-128">클라우드 서비스에 경고를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="aae03-129">**설정** > **경고 규칙** > **경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="aae03-130">여기에서 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-130">From here, you can setup an alert.</span></span> <span data-ttu-id="aae03-131">**메트릭** 드롭다운 상자에서 다음 데이터 형식에 대한 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="aae03-132">디스크 읽기</span><span class="sxs-lookup"><span data-stu-id="aae03-132">Disk read</span></span>
* <span data-ttu-id="aae03-133">디스크 쓰기</span><span class="sxs-lookup"><span data-stu-id="aae03-133">Disk write</span></span>
* <span data-ttu-id="aae03-134">네트워크 입력</span><span class="sxs-lookup"><span data-stu-id="aae03-134">Network in</span></span>
* <span data-ttu-id="aae03-135">네트워크 출력</span><span class="sxs-lookup"><span data-stu-id="aae03-135">Network out</span></span>
* <span data-ttu-id="aae03-136">CPU 비율</span><span class="sxs-lookup"><span data-stu-id="aae03-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="aae03-137">메트릭 타일에서 모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="aae03-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="aae03-138">**설정** > **경고 규칙**을 사용하는 대신 **클라우드 서비스** 블레이드의 **모니터링** 섹션에서 메트릭 타일 중 하나를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![클라우드 서비스 모니터링](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="aae03-140">여기에서 타일에 사용되는 차트를 사용자 지정하거나 경고 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="aae03-141">다시 부팅, 이미지로 다시 설치 또는 원격 데스크톱</span><span class="sxs-lookup"><span data-stu-id="aae03-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="aae03-142">지금은 **Azure Portal**을 사용하여 원격 데스크톱을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="aae03-143">그러나 [Azure 클래식 포털](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) 또는 [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)를 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="aae03-144">먼저 클라우드 서비스 인스턴스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-144">First, click on the cloud service instance.</span></span>

![클라우드 서비스 인스턴스](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="aae03-146">열리는 블레이드에서 원격 데스크톱 연결을 시작하고 인스턴스를 원격으로 다시 부팅하거나 인스턴스를 원격으로 이미지로 다시 설치(새 이미지로 시작)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![클라우드 서비스 인스턴스 단추](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="aae03-148">.cscfg 다시 구성</span><span class="sxs-lookup"><span data-stu-id="aae03-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="aae03-149">[서비스 구성(cscfg)](cloud-services-model-and-package.md#cscfg) 파일을 통해 클라우드 서비스를 다시 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="aae03-150">먼저 .cscfg 파일을 다운로드하고 수정한 후 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="aae03-151">**설정** 아이콘 또는 **모든 설정** 링크를 클릭하여 **설정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![설정 페이지](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="aae03-153">**구성** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-153">Click on the **Configuration** item.</span></span>

    ![구성 블레이드](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="aae03-155">**다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-155">Click on the **Download** button.</span></span>

    ![다운로드](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="aae03-157">서비스 구성 파일을 업데이트한 후 구성 업데이트를 업로드하고 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![업로드](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="aae03-159">.cscfg 파일을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aae03-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aae03-160">Next steps</span></span>
* <span data-ttu-id="aae03-161">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy-portal.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="aae03-162">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aae03-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="aae03-163">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aae03-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="aae03-164">[SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="aae03-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
