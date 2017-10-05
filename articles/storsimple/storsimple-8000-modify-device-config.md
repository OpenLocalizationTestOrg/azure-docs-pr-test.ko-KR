---
title: "StorSimple 8000 시리즈 장치 구성 수정 | Microsoft Docs"
description: "이미 배포된 StorSimple 장치를 다시 구성하기 위해 StorSimple 장치 관리자 서비스를 사용하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 01e1e7447d6951d1b2c89f3b0ef726af9c03fd66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-modify-your-storsimple-device-configuration"></a><span data-ttu-id="5ab68-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 구성 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-103">Use the StorSimple Device Manager service to modify your StorSimple device configuration</span></span>

## <a name="overview"></a><span data-ttu-id="5ab68-104">개요</span><span class="sxs-lookup"><span data-stu-id="5ab68-104">Overview</span></span>

<span data-ttu-id="5ab68-105">**설정** 블레이드의 Azure Portal **장치 설정** 섹션에는 StorSimple 장치 관리자 서비스에서 관리하는 StorSimple 장치에서 다시 구성할 수 있는 모든 장치 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-105">The Azure portal **Device settings** section in the **Settings** blade contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="5ab68-106">이 자습서에서는 **설정** 블레이드를 사용하여 다음 장치 수준의 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-106">This tutorial explains how you can use the **Settings** blade to perform the following device-level tasks:</span></span>

* <span data-ttu-id="5ab68-107">장치 이름 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-107">Modify device friendly name</span></span>
* <span data-ttu-id="5ab68-108">장치 시간 설정 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-108">Modify device time settings</span></span>
* <span data-ttu-id="5ab68-109">보조 DNS 할당</span><span class="sxs-lookup"><span data-stu-id="5ab68-109">Assign a secondary DNS</span></span>
* <span data-ttu-id="5ab68-110">네트워크 인터페이스 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-110">Modify network interfaces</span></span>
* <span data-ttu-id="5ab68-111">IP 교체 또는 재할당</span><span class="sxs-lookup"><span data-stu-id="5ab68-111">Swap or reassign IPs</span></span>

## <a name="modify-device-friendly-name"></a><span data-ttu-id="5ab68-112">장치 이름 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-112">Modify device friendly name</span></span>

<span data-ttu-id="5ab68-113">Azure Portal을 사용하여 장치 이름을 변경하거나 사용자가 원하는 고유한 이름을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-113">You can use the Azure portal to change the device name and assign it a unique friendly name of your choice.</span></span> <span data-ttu-id="5ab68-114">장치의 **일반 설정** 블레이드를 사용하여 장치 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-114">Use the **General settings** blade on your device to modify the device friendly name.</span></span> <span data-ttu-id="5ab68-115">이름은 모든 문자를 사용할 수 있으며 최대 64자 길이로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-115">The friendly name can contain any characters and can be a maximum of 64 characters long.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ab68-116">장치 설정이 완료되기 전에 Azure Portal에서 장치 이름을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-116">You can only modify the device name in the Azure portal before the device setup is complete.</span></span> <span data-ttu-id="5ab68-117">최소 장치 설정이 완료되면 장치 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-117">Once the minimum device setup is complete, you cannot change the device name.</span></span>

![일반 설정의 장치 이름](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

<span data-ttu-id="5ab68-119">StorSimple 장치 관리자 서비스에 연결된 StorSimple 장치에는 기본 이름이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-119">A StorSimple device that is connected to the StorSimple Device Manager service is assigned a default name.</span></span> <span data-ttu-id="5ab68-120">기본 이름에는 일반적으로 장치의 일련 번호가 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-120">The default name typically reflects the serial number of the device.</span></span> <span data-ttu-id="5ab68-121">예를 들어, 기본 장치 이름은 8600-SHX0991003G44HT와 같이 다음을 나타내는 15자 길이의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-121">For example, a default device name that is 15 characters long, such as 8600-SHX0991003G44HT, indicates the following:</span></span>

* <span data-ttu-id="5ab68-122">**8600** – 장치 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-122">**8600**  – Indicates the device model.</span></span>
* <span data-ttu-id="5ab68-123">**SHX** – 제조 사이트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-123">**SHX** – Indicates the manufacturing site.</span></span>
* <span data-ttu-id="5ab68-124">**0991003** - 특정 제품을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-124">**0991003** - Indicates a specific product.</span></span>
* <span data-ttu-id="5ab68-125">**G44HT**- 마지막 5자리 숫자는 고유한 일련 번호를 만들도록 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-125">**G44HT**- The last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="5ab68-126">순차적인 집합이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-126">This might not be a sequential set.</span></span>

## <a name="modify-device-description"></a><span data-ttu-id="5ab68-127">장치 설명 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-127">Modify device description</span></span>

<span data-ttu-id="5ab68-128">장치의 **일반 설정** 블레이드를 사용하여 장치 설명을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-128">Use the **General settings** blade on your device to modify the device description.</span></span>

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

<span data-ttu-id="5ab68-130">일반적으로 장치 설명은 장치의 소유자 및 물리적 위치를 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-130">A device description usually helps identify the owner and the physical location of the device.</span></span> <span data-ttu-id="5ab68-131">설명 필드에는 256자 미만의 문자가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-131">The description field must contain fewer than 256 characters.</span></span>

## <a name="modify-time-settings"></a><span data-ttu-id="5ab68-132">시간 설정 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-132">Modify time settings</span></span>

<span data-ttu-id="5ab68-133">장치는 클라우드 저장소 서비스 공급자를 사용하여 인증하기 위해 시간을 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-133">Your device must synchronize time in order to authenticate with your cloud storage service provider.</span></span> <span data-ttu-id="5ab68-134">장치의 **일반 설정** 블레이드를 사용하여 장치 시간 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-134">Use the **General settings** blade on your device to modify the device time settings.</span></span>

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 <span data-ttu-id="5ab68-136">드롭다운 목록에서 표준 시간대를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-136">Select your time zone from the drop-down list.</span></span> <span data-ttu-id="5ab68-137">최대 두 개의 NTP(Network Time Protocol) 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-137">You can specify up to two Network Time Protocol (NTP) servers:</span></span>

 - <span data-ttu-id="5ab68-138">**기본 NTP 서버** - 이 구성은 필수 항목이며 장치를 구성하기 위해 StorSimple용 Windows PowerShell을 사용할 때 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-138">**Primary NTP server** -  The configuration is required and is specified when you use Windows PowerShell for StorSimple to configure your device.</span></span> <span data-ttu-id="5ab68-139">기본 Windows 서버 **time.windows.com** 을 NTP 서버로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-139">You can specify the default Windows Server **time.windows.com** as your NTP server.</span></span> <span data-ttu-id="5ab68-140">Azure Portal을 통해 기본 NTP 서버 구성을 볼 수 있지만, 변경하려면 Windows PowerShell 인터페이스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-140">You can view the primary NTP server configuration through the Azure portal, but you must use the Windows PowerShell interface to change it.</span></span> <span data-ttu-id="5ab68-141">`Set-HcsNTPClientServerAddress` cmdlet을 사용하여 장치의 기본 NTP 서버를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-141">Use the `Set-HcsNTPClientServerAddress` cmdlet to modify the Primary NTP server of your device.</span></span> <span data-ttu-id="5ab68-142">자세한 내용은 [Set-HcsNTPClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet의 구문으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-142">For more information, go to synxtax for [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

- <span data-ttu-id="5ab68-143">**보조 NTP 서버** - 이 구성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-143">**Secondary NTP server** - The configuration is optional.</span></span> <span data-ttu-id="5ab68-144">포털을 사용하여 보조 NTP 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-144">You can use the portal to configure a secondary NTP server.</span></span>

<span data-ttu-id="5ab68-145">NTP 서버 구성 시 네트워크에서 NTP 트래픽이 데이터 센터에서 인터넷으로 전달되도록 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-145">When configuring the NTP server, ensure that your network allows the NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="5ab68-146">공용 NTP 서버를 지정하는 경우, NTP 트래픽이 외부 네트워크 간에 여행할 수 있도록 네트워크 방화벽 및 기타 보안 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-146">When specifying a public NTP server, you must make sure that your network firewalls and other security devices are configured to allow NTP traffic to travel to and from the outside network.</span></span> <span data-ttu-id="5ab68-147">양방향 NTP 트래픽이 허용되지 않는 경우 내부 NTP 서버(Windows 도메인 컨트롤러가 이 기능을 제공)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-147">If bidirectional NTP traffic is not permitted, you must use an internal NTP server (a Windows domain controller provides this function).</span></span> <span data-ttu-id="5ab68-148">장치가 시간을 동기화할 수 없는 경우 클라우드 저장소 공급자와 통신하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-148">If your device cannot synchronize time, it may not be able to communicate with your cloud storage provider.</span></span>

<span data-ttu-id="5ab68-149">공용 NTP 서버의 목록을 보려면 [NTP 서버 웹](http://support.ntp.org/bin/view/Servers/WebHome)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="5ab68-149">To see a list of public NTP servers, go to the [NTP Servers Web](http://support.ntp.org/bin/view/Servers/WebHome).</span></span>

### <a name="what-happens-if-the-device-is-deployed-in-a-different-time-zone"></a><span data-ttu-id="5ab68-150">장치를 다른 표준 시간대에 배포하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="5ab68-150">What happens if the device is deployed in a different time zone?</span></span>

<span data-ttu-id="5ab68-151">장치를 다른 표준 시간대에 배포하는 경우 장치 표준 시간대가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-151">If the device is deployed in a different time zone, the device time zone will change.</span></span> <span data-ttu-id="5ab68-152">장치 표준 시간대를 사용하는 모든 백업 정책이 있는 백업 정책이 새 표준 시간대에 따라 자동으로 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-152">Given that all the backup policies use the device time zone, the backup policies will automatically adjust in accordance with the new time zone.</span></span> <span data-ttu-id="5ab68-153">사용자 개입이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-153">No user intervention is required.</span></span>

## <a name="modify-dns-settings"></a><span data-ttu-id="5ab68-154">DNS 설정 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-154">Modify DNS settings</span></span>

<span data-ttu-id="5ab68-155">DNS 서버는 장치가 클라우드 저장소 서비스 공급자와 통신하려고 할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-155">A DNS server is used when your device attempts to communicate with your cloud storage service provider.</span></span> <span data-ttu-id="5ab68-156">장치의 **네트워크 설정** 블레이드를 사용하여 구성된 DNS 설정을 보고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-156">Use the **Network settings** blade on your device to view and modify the configured DNS settings.</span></span> 

![네트워크 설정에서 DNS 설정](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

<span data-ttu-id="5ab68-158">고가용성을 위해 초기 장치를 배포하는 동안 기본 및 보조 DNS 서버를 모두 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-158">For high availability, you are required to configure both the primary and the secondary DNS servers during the initial device deployment.</span></span>

<span data-ttu-id="5ab68-159">**기본 DNS 서버** - 먼저 StorSimple용 Windows PowerShell을 사용하여 초기 설정 중에 기본 DNS 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-159">**Primary DNS server** - You use the Windows PowerShell for StorSimple to first specify the Primary DNS server during the initial setup.</span></span> <span data-ttu-id="5ab68-160">Windows PowerShell 인터페이스를 통해서만 기본 DNS 서버를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-160">You can reconfigure the primary DNS server only via the Windows PowerShell interface.</span></span> <span data-ttu-id="5ab68-161">`Set-HcsDNSClientServerAddress` cmdlet을 사용하여 장치의 기본 DNS 서버를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-161">Use the `Set-HcsDNSClientServerAddress` cmdlet to modify the primary DNS server of your device.</span></span> <span data-ttu-id="5ab68-162">자세한 내용은 [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet의 구문으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-162">For more information, go to synxtax for [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

<span data-ttu-id="5ab68-163">**보조 DNS 서버** - 보조 DNS 서버를 수정하려면 장치의 Windows PowerShell 인터페이스에서 `Set-HcsDNSClientServerAddress` cmdlet 또는 Azure Portal에서 StorSimple 장치의 **네트워크 설정** 블레이드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-163">**Secondary DNS server** - To modify the secondary DNS server, use the `Set-HcsDNSClientServerAddress` cmdlet in the Windows PowerShell interface of the device or **Network settings** blade of your StorSimple device in the Azure portal.</span></span>

<span data-ttu-id="5ab68-164">Azure Portal에서 보조 DNS 서버를 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-164">To modify the secondary DNS server in Azure portal, perform the following steps.</span></span>

1. <span data-ttu-id="5ab68-165">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-165">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="5ab68-166">장치 목록에서 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-166">From the list of devices, select and click your device.</span></span>

2. <span data-ttu-id="5ab68-167">**설정** 블레이드에서 **장치 설정 > 네트워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-167">In the **Settings** blade, go to **Device settings > Network**.</span></span> <span data-ttu-id="5ab68-168">그러면 **네트워크 설정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-168">This opens up the **Network settings** blade.</span></span> <span data-ttu-id="5ab68-169">**DNS 설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-169">Click **DNS settings** tile.</span></span> <span data-ttu-id="5ab68-170">보조 DNS 서버 IP 주소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-170">Modify the secondary DNS server IP address.</span></span>

    ![보조 DNS 서버 IP 주소 수정](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. <span data-ttu-id="5ab68-172">명령 모음에서 **저장**을 클릭하고 확인하라는 메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-172">From the command bar, click **Save** and when prompted for confirmation, click **OK**.</span></span>

    ![변경 내용 저장 및 확인](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a><span data-ttu-id="5ab68-174">네트워크 인터페이스 수정</span><span class="sxs-lookup"><span data-stu-id="5ab68-174">Modify network interfaces</span></span>

<span data-ttu-id="5ab68-175">장치에는 6개의 장치 네트워크 인터페이스가 있으며, 그 중 4개는 1GbE, 2개는 10GbE입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-175">Your device has six device network interfaces, four of which are 1 GbE and two of which are 10 GbE.</span></span> <span data-ttu-id="5ab68-176">이러한 인터페이스는 DATA 0부터 DATA 5로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-176">These interfaces are labeled as DATA 0 – DATA 5.</span></span> <span data-ttu-id="5ab68-177">DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 네트워크 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-177">DATA 0, DATA 1, DATA 4, and DATA 5 are 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE network interfaces.</span></span>

<span data-ttu-id="5ab68-178">**네트워크 설정** 블레이드를 사용하여 사용할 각 인터페이스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-178">Use the **Network settings** blade to configure each of the interfaces to be used.</span></span>

![네트워크 설정을 통해 네트워크 인터페이스 구성](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

<span data-ttu-id="5ab68-180">고가용성을 위해 장치에 둘 이상의 iSCSI 인터페이스 및 두 개의 클라우드 지원 인터페이스가 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-180">To ensure high availability, we recommend that you have at least two iSCSI interfaces and two cloud-enabled interfaces on your device.</span></span> <span data-ttu-id="5ab68-181">권장 사항이지만 사용하지 않는 인터페이스를 사용하지 않도록 설정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-181">We recommend but do not require that unused interfaces be disabled.</span></span>

<span data-ttu-id="5ab68-182">각 네트워크 인터페이스의 경우 다음 매개 변수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-182">For each network interface, the following parameters are displayed:</span></span>

* <span data-ttu-id="5ab68-183">**속도** – 사용자가 구성할 수 있는 매개 변수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-183">**Speed** – Not a user-configurable parameter.</span></span> <span data-ttu-id="5ab68-184">DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-184">DATA 0, DATA 1, DATA 4, and DATA 5 are always 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE interfaces.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5ab68-185">속도 및 이중 교환 패턴은 항상 자동으로 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-185">Speed and duplex are always auto-negotiated.</span></span> <span data-ttu-id="5ab68-186">Jumbo 프레임이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-186">Jumbo frames are not supported.</span></span>
  
* <span data-ttu-id="5ab68-187">**인터페이스 상태** – 인터페이스를 설정하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-187">**Interface state** – An interface can be enabled or disabled.</span></span> <span data-ttu-id="5ab68-188">설정 경우 장치가 인터페이스를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-188">If enabled, the device will attempt to use the interface.</span></span> <span data-ttu-id="5ab68-189">네트워크에 연결 및 사용되는 해당 인터페이스만 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-189">We recommend that only those interfaces that are connected to the network and used be enabled.</span></span> <span data-ttu-id="5ab68-190">사용하지 않는 모든 인터페이스는 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-190">Disable any interfaces that you are not using.</span></span>
* <span data-ttu-id="5ab68-191">**인터페이스 유형** – 이 매개 변수를 사용하면 클라우드 저장소 트래픽에서 iSCSI 트래픽을 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-191">**Interface type** – This parameter allows you to isolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="5ab68-192">이 매개 변수는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-192">This parameter can be one of the following:</span></span>
  
  * <span data-ttu-id="5ab68-193">**클라우드 사용** – 사용하도록 설정하면 장치가 클라우드와 통신하는 데 이 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-193">**Cloud enabled** – when enabled, the device will use this interface to communicate with the cloud.</span></span>
  * <span data-ttu-id="5ab68-194">**iSCSI 사용** – 사용하도록 설정하면 장치가 iSCSI 호스트와 통신하는 데 이 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-194">**iSCSI enabled** – when enabled, the device will use this interface to communicate with the iSCSI host.</span></span>
    
    <span data-ttu-id="5ab68-195">클라우드 저장소 트래픽에서 iSCSI 트래픽을 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-195">We recommend that you isolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="5ab68-196">또한 호스트가 장치와 동일한 서브넷 내에 있는 경우, 게이트웨이를 할당할 필요가 없습니다. 하지만 호스트가 장치와 다른 서브넷에 있는 경우, 게이트웨이를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-196">Also note if your host is within the same subnet as your device, you do not need to assign a gateway; however, if your host is in a different subnet than your device, you will need to assign a gateway.</span></span>
* <span data-ttu-id="5ab68-197">**IP 주소** – 네트워크 인터페이스를 구성할 때 VIP(가상 IP)를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-197">**IP address** – When you configure any of the network interfaces, you must configure a virtual IP (VIP).</span></span> <span data-ttu-id="5ab68-198">IPv4나 IPv6 또는 둘 다가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-198">This can be IPv4 or IPv6 or both.</span></span> <span data-ttu-id="5ab68-199">IPv4 및 IPv6 주소 모음이 모두 장치 네트워크 인터페이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-199">Both the IPv4 and IPv6 address families are supported for the device network interfaces.</span></span> <span data-ttu-id="5ab68-200">IPv4를 사용하는 경우 십진수 표기법으로 32비트 IP 주소(*xxx.xxx.xxx.xxx*)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-200">When using IPv4, specify a 32-bit IP address (*xxx.xxx.xxx.xxx*) in dot-decimal notation.</span></span> <span data-ttu-id="5ab68-201">IPv6를 사용하는 경우 4자리 접두사를 제공하면 해당 접두사를 기반으로 사용자의 장치 네트워크 인터페이스에 대해 128비트 주소가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-201">When using IPv6, simply supply a 4-digit prefix, and a 128-bit address will be generated automatically for your device network interface based on that prefix.</span></span>
* <span data-ttu-id="5ab68-202">**서브넷** – 서브넷 마스크를 참조하고 Widnows PowerShell 인터페이스를 통해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-202">**Subnet** – This refers to the subnet mask and is configured via the Windows PowerShell interface.</span></span>
* <span data-ttu-id="5ab68-203">**게이트웨이** – 동일한 IP 주소 공간(서브넷) 내에 있지 않은 노드와 통신하려고 할 때 이 인터페이스가 사용하는 기본 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-203">**Gateway** – This is the default gateway that should be used by this interface when it attempts to communicate with nodes that are not within the same IP address space (subnet).</span></span> <span data-ttu-id="5ab68-204">기본 게이트웨이는 서브넷 마스크를 통해 결정된 대로 인터페이스 IP 주소와 동일한 주소 공간(서브넷)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-204">The default gateway must be in the same address space (subnet) as the interface IP address, as determined by the subnet mask.</span></span>
* <span data-ttu-id="5ab68-205">**고정 IP 주소** - 이 필드는 DATA 0 인터페이스를 구성하는 동안에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-205">**Fixed IP address** – This field is available only while you configure the DATA 0 interface.</span></span> <span data-ttu-id="5ab68-206">업데이트 또는 장치 문제 해결과 같은 작업의 경우 장치 컨트롤러에 직접 연결해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-206">For operations such as updates or troubleshooting the device, you may need to connect directly to the device controller.</span></span> <span data-ttu-id="5ab68-207">고정 IP 주소는 장치에서 활성 및 수동 컨트롤러에 모두 액세스하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-207">The fixed IP address can be used to access both the active and the passive controller on your device.</span></span>

> [!NOTE]
> * <span data-ttu-id="5ab68-208">작업을 제대로 수행하려면 각 장치 인터페이스가 연결된 각 스위치에서 인터페이스 속도 및 이중을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-208">To ensure proper operation, verify the interface speed and duplex on the switch that each device interface is connected to.</span></span> <span data-ttu-id="5ab68-209">스위치 인터페이스는 기가비트 이더넷(1000Mbps)과 협상하거나 이에 대해 구성되며 전이중입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-209">Switch interfaces should either negotiate with or be configured for Gigabit Ethernet (1000 Mbps) and be full-duplex.</span></span> <span data-ttu-id="5ab68-210">더 느린 속도 또는 반이중에서의 인터페이스 운영은 성능 문제를 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-210">Interfaces operating at slower speeds or in half-duplex will result in performance issues.</span></span>
> * <span data-ttu-id="5ab68-211">중단 및 가동 중지를 최소화하려면 장치의 iSCSI 네트워크 인터페이스가 연결될 각각의 스위치 포트에서 포트패스트를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-211">To minimize disruptions and downtime, we recommend that you enable portfast on each of the switch ports that the iSCSI network interface of your device will be connecting to.</span></span> <span data-ttu-id="5ab68-212">이렇게 하면 장애 조치 시 네트워크 연결을 신속하게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-212">This will ensure that network connectivity can be established quickly in the event of a failover.</span></span>

### <a name="configure-data-0"></a><span data-ttu-id="5ab68-213">DATA 0 구성</span><span class="sxs-lookup"><span data-stu-id="5ab68-213">Configure DATA 0</span></span>

<span data-ttu-id="5ab68-214">DATA 0은 기본적으로 클라우드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-214">DATA 0 is cloud-enabled by default.</span></span> <span data-ttu-id="5ab68-215">DATA 0을 구성할 때 고정된 두 IP 주소를 각 컨트롤러마다 하나씩 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-215">When configuring DATA 0, you are also required to configure two fixed IP addresses, one for each controller.</span></span> <span data-ttu-id="5ab68-216">이러한 고정 IP 주소는 장치 컨트롤러에 직접 액세스하는 데 사용할 수 있으며 장치에서 업데이트를 설치하거나 문제 해결을 목적으로 컨트롤러에 액세스할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-216">These fixed IP addresses can be used to access the device controllers directly and are useful when you install updates on the device or when you access the controllers for the purpose of troubleshooting.</span></span>

<span data-ttu-id="5ab68-217">DATA 0 설정 블레이드를 통해 고정된 IP 컨트롤러를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-217">You can reconfigure the fixed IP controllers via the DATA 0 settings blade.</span></span>

![네트워크 인터페이스 구성 - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> <span data-ttu-id="5ab68-219">컨트롤러의 고정 IP 주소는 장치에 대한 업데이트를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-219">The fixed IP addresses for the controller are used for servicing the updates to the device.</span></span> <span data-ttu-id="5ab68-220">따라서 고정 IP는 라우팅 가능하고 인터넷에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-220">Therefore, the fixed IPs must be routable and able to connect to the Internet.</span></span>

### <a name="configure-data-1---data-5"></a><span data-ttu-id="5ab68-221">DATA 1~DATA 5 구성</span><span class="sxs-lookup"><span data-stu-id="5ab68-221">Configure DATA 1 - DATA 5</span></span>

<span data-ttu-id="5ab68-222">DATA 1~DATA 5 네트워크 인터페이스의 경우 다음 스크린샷에 표시된 대로 모든 네트워크 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-222">For DATA 1 - DATA 5 network interfaces, you can configure all the network settings as shown in the following screenshot:</span></span>

![네트워크 인터페이스 구성 DATA 1~DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a><span data-ttu-id="5ab68-224">IP 교체 또는 재할당</span><span class="sxs-lookup"><span data-stu-id="5ab68-224">Swap or reassign IPs</span></span>

<span data-ttu-id="5ab68-225">현재, 컨트롤러의 모든 네트워크 인터페이스에 사용 중인 VIP가 할당된 경우(해당 네트워크 내의 동일한 장치 또는 다른 장치를 통해) 해당 컨트롤러는 장애 조치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-225">Currently, if any network interface on the controller is assigned a VIP that is in use (by the same device or another device in the network), then the controller will fail over.</span></span> <span data-ttu-id="5ab68-226">장치 네트워크 인터페이스의 VIP를 교환하거나 다시 할당하는 경우 중복 IP 상황을 만들 수 있는 만큼 적절한 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-226">If you swap or reassign VIPs for a device network interface, you must follow a proper procedure as you could create a duplicate IP situation.</span></span>

<span data-ttu-id="5ab68-227">다음 단계를 수행하여 네트워크 인터페이스에 대한 VIP를 교체하거나 재할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-227">Perform the following steps to swap or reassign the VIPs for any of the network interfaces:</span></span>

#### <a name="to-reassign-ips"></a><span data-ttu-id="5ab68-228">IP 재할당</span><span class="sxs-lookup"><span data-stu-id="5ab68-228">To reassign IPs</span></span>

1. <span data-ttu-id="5ab68-229">두 인터페이스에 대한 IP 주소 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-229">Clear the IP address for both interfaces.</span></span>
2. <span data-ttu-id="5ab68-230">IP 주소 선택을 취소한 후 해당 인터페이스에 새 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-230">After the IP addresses are cleared, assign the new IP addresses to the respective interfaces.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ab68-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ab68-231">Next steps</span></span>

* <span data-ttu-id="5ab68-232">[StorSimple 장치에 대해 MPIO를 구성](storsimple-8000-configure-mpio-windows-server.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-232">Learn how to [configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span>
* <span data-ttu-id="5ab68-233">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ab68-233">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

