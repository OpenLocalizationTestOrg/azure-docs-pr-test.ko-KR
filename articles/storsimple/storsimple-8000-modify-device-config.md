---
title: "aaaModify hello StorSimple 8000 시리즈 장치 구성 | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 장치 관리자 서비스 tooreconfigure 이미 배포 된 StorSimple 장치에 설명 합니다."
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
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a><span data-ttu-id="d389c-103">사용 하 여 hello StorSimple 장치 관리자 서비스 toomodify StorSimple 장치 구성</span><span class="sxs-lookup"><span data-stu-id="d389c-103">Use hello StorSimple Device Manager service toomodify your StorSimple device configuration</span></span>

## <a name="overview"></a><span data-ttu-id="d389c-104">개요</span><span class="sxs-lookup"><span data-stu-id="d389c-104">Overview</span></span>

<span data-ttu-id="d389c-105">Azure 포털 hello **장치 설정** hello 섹션인 **설정을** 블레이드는 StorSimple 장치 관리자에서 관리 되는 StorSimple 장치에는 다시 구성할 수 있는 모든 hello 장치 매개 변수가 포함 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-105">hello Azure portal **Device settings** section in hello **Settings** blade contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="d389c-106">이 자습서에서는 hello를 사용 하는 방법에 대해 설명 **설정을** 블레이드 tooperform hello 장치 수준 태스크를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-106">This tutorial explains how you can use hello **Settings** blade tooperform hello following device-level tasks:</span></span>

* <span data-ttu-id="d389c-107">장치 이름 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-107">Modify device friendly name</span></span>
* <span data-ttu-id="d389c-108">장치 시간 설정 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-108">Modify device time settings</span></span>
* <span data-ttu-id="d389c-109">보조 DNS 할당</span><span class="sxs-lookup"><span data-stu-id="d389c-109">Assign a secondary DNS</span></span>
* <span data-ttu-id="d389c-110">네트워크 인터페이스 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-110">Modify network interfaces</span></span>
* <span data-ttu-id="d389c-111">IP 교체 또는 재할당</span><span class="sxs-lookup"><span data-stu-id="d389c-111">Swap or reassign IPs</span></span>

## <a name="modify-device-friendly-name"></a><span data-ttu-id="d389c-112">장치 이름 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-112">Modify device friendly name</span></span>

<span data-ttu-id="d389c-113">Hello Azure 포털 toochange hello 장치 이름을 사용 하 고 원하는 고유한 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-113">You can use hello Azure portal toochange hello device name and assign it a unique friendly name of your choice.</span></span> <span data-ttu-id="d389c-114">사용 하 여 hello **일반 설정** 장치 toomodify hello 장치 친숙 한 이름을 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-114">Use hello **General settings** blade on your device toomodify hello device friendly name.</span></span> <span data-ttu-id="d389c-115">hello 이름 모든 문자를 포함할 수 및 최대 64 자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-115">hello friendly name can contain any characters and can be a maximum of 64 characters long.</span></span>

> [!NOTE] 
> <span data-ttu-id="d389c-116">Hello 장치 설치가 완료 되기 전에 hello Azure 포털에서에서 장치 이름을 hello 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-116">You can only modify hello device name in hello Azure portal before hello device setup is complete.</span></span> <span data-ttu-id="d389c-117">Hello 최소 장치 설정 완료 되 면 hello 장치 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-117">Once hello minimum device setup is complete, you cannot change hello device name.</span></span>

![일반 설정의 장치 이름](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

<span data-ttu-id="d389c-119">StorSimple 장치에 연결 된 toohello StorSimple 장치 관리자 서비스는 기본 이름이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-119">A StorSimple device that is connected toohello StorSimple Device Manager service is assigned a default name.</span></span> <span data-ttu-id="d389c-120">hello 기본 이름은 일반적으로 hello hello 장치 일련 번호를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-120">hello default name typically reflects hello serial number of hello device.</span></span> <span data-ttu-id="d389c-121">예를 들어, 기본 장치 이름이 15 자, 8600-SHX0991003G44HT 같은 hello 다음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-121">For example, a default device name that is 15 characters long, such as 8600-SHX0991003G44HT, indicates hello following:</span></span>

* <span data-ttu-id="d389c-122">**8600** – hello 장치 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-122">**8600**  – Indicates hello device model.</span></span>
* <span data-ttu-id="d389c-123">**SHX** – hello 제조 사이트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-123">**SHX** – Indicates hello manufacturing site.</span></span>
* <span data-ttu-id="d389c-124">**0991003** - 특정 제품을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-124">**0991003** - Indicates a specific product.</span></span>
* <span data-ttu-id="d389c-125">**G44HT**-hello 마지막 5 자리는 고유한 일련 번호가 증가 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-125">**G44HT**- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="d389c-126">순차적인 집합이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-126">This might not be a sequential set.</span></span>

## <a name="modify-device-description"></a><span data-ttu-id="d389c-127">장치 설명 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-127">Modify device description</span></span>

<span data-ttu-id="d389c-128">사용 하 여 hello **일반 설정** 장치 toomodify hello 장치 설명에 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-128">Use hello **General settings** blade on your device toomodify hello device description.</span></span>

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

<span data-ttu-id="d389c-130">일반적으로 장치 설명을 통해 hello 소유자 및 hello hello 장치의 물리적 위치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-130">A device description usually helps identify hello owner and hello physical location of hello device.</span></span> <span data-ttu-id="d389c-131">hello 설명 필드에는 256 자 미만을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-131">hello description field must contain fewer than 256 characters.</span></span>

## <a name="modify-time-settings"></a><span data-ttu-id="d389c-132">시간 설정 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-132">Modify time settings</span></span>

<span data-ttu-id="d389c-133">장치는 클라우드 저장소 서비스 공급자와 순서 tooauthenticate에서 경과한 시간을 동기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-133">Your device must synchronize time in order tooauthenticate with your cloud storage service provider.</span></span> <span data-ttu-id="d389c-134">사용 하 여 hello **일반 설정** 블레이드 장치 toomodify hello 장치 시간 설정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-134">Use hello **General settings** blade on your device toomodify hello device time settings.</span></span>

![일반 설정의 장치 설명](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 <span data-ttu-id="d389c-136">Hello 드롭 다운 목록에서 표준 시간대를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-136">Select your time zone from hello drop-down list.</span></span> <span data-ttu-id="d389c-137">Tootwo 시간이 NTP (Network Protocol) 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-137">You can specify up tootwo Network Time Protocol (NTP) servers:</span></span>

 - <span data-ttu-id="d389c-138">**기본 NTP 서버** -hello 구성이 필수 이기에 사용 하면 Windows PowerShell StorSimple tooconfigure 장치 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-138">**Primary NTP server** -  hello configuration is required and is specified when you use Windows PowerShell for StorSimple tooconfigure your device.</span></span> <span data-ttu-id="d389c-139">Hello 기본 Windows 서버를 지정할 수 있습니다 **time.windows.com** NTP 서버와 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-139">You can specify hello default Windows Server **time.windows.com** as your NTP server.</span></span> <span data-ttu-id="d389c-140">Hello 주 NTP 서버 구성은 hello Azure 포털을 통해 볼 수는 있지만 Windows PowerShell 인터페이스 toochange hello를 사용 해야 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-140">You can view hello primary NTP server configuration through hello Azure portal, but you must use hello Windows PowerShell interface toochange it.</span></span> <span data-ttu-id="d389c-141">사용 하 여 hello `Set-HcsNTPClientServerAddress` 장치의 cmdlet toomodify hello 기본 NTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-141">Use hello `Set-HcsNTPClientServerAddress` cmdlet toomodify hello Primary NTP server of your device.</span></span> <span data-ttu-id="d389c-142">자세한 내용은 [Set-hcsntpclientserveraddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet에 대 한 toosynxtax를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-142">For more information, go toosynxtax for [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

- <span data-ttu-id="d389c-143">**보조 NTP 서버** -hello 구성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-143">**Secondary NTP server** - hello configuration is optional.</span></span> <span data-ttu-id="d389c-144">Hello 포털 tooconfigure 보조 NTP 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-144">You can use hello portal tooconfigure a secondary NTP server.</span></span>

<span data-ttu-id="d389c-145">Hello NTP 서버를 구성할 때 네트워크 사용자 데이터 센터 toohello 인터넷에서에서 NTP 트래픽이 toopass hello 허용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-145">When configuring hello NTP server, ensure that your network allows hello NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="d389c-146">공용 NTP 서버를 지정할 때는 네트워크 방화벽 및 기타 보안 장치가 구성된 tooallow hello 네트워크 외부에서 NTP 트래픽이 tootravel tooand가 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-146">When specifying a public NTP server, you must make sure that your network firewalls and other security devices are configured tooallow NTP traffic tootravel tooand from hello outside network.</span></span> <span data-ttu-id="d389c-147">양방향 NTP 트래픽이 허용되지 않는 경우 내부 NTP 서버(Windows 도메인 컨트롤러가 이 기능을 제공)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-147">If bidirectional NTP traffic is not permitted, you must use an internal NTP server (a Windows domain controller provides this function).</span></span> <span data-ttu-id="d389c-148">장치 시간을 동기화 할 수 없습니다, 클라우드 저장소 공급자와 수 toocommunicate 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-148">If your device cannot synchronize time, it may not be able toocommunicate with your cloud storage provider.</span></span>

<span data-ttu-id="d389c-149">공용 NTP 서버를 이동 toohello 목록이 toosee [NTP 서버 웹](http://support.ntp.org/bin/view/Servers/WebHome)합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-149">toosee a list of public NTP servers, go toohello [NTP Servers Web](http://support.ntp.org/bin/view/Servers/WebHome).</span></span>

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a><span data-ttu-id="d389c-150">Hello 장치는 다른 표준 시간대에 배포 하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="d389c-150">What happens if hello device is deployed in a different time zone?</span></span>

<span data-ttu-id="d389c-151">Hello 장치가 다른 표준 시간대에 배포 하는 경우에 hello 장치 표준 시간대 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-151">If hello device is deployed in a different time zone, hello device time zone will change.</span></span> <span data-ttu-id="d389c-152">Hello 장치 표준 시간대를 사용 하는 모든 hello 백업 정책, 있다고 가정 hello 백업 정책 hello 새 표준 시간대에 따라 자동으로 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-152">Given that all hello backup policies use hello device time zone, hello backup policies will automatically adjust in accordance with hello new time zone.</span></span> <span data-ttu-id="d389c-153">사용자 개입이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-153">No user intervention is required.</span></span>

## <a name="modify-dns-settings"></a><span data-ttu-id="d389c-154">DNS 설정 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-154">Modify DNS settings</span></span>

<span data-ttu-id="d389c-155">DNS 서버는 장치가 클라우드 저장소 서비스 공급자와 toocommunicate을 시도할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-155">A DNS server is used when your device attempts toocommunicate with your cloud storage service provider.</span></span> <span data-ttu-id="d389c-156">사용 하 여 hello **네트워크 설정** 블레이드 장치 tooview에서 DNS 설정을 구성 하는 hello 하 고 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-156">Use hello **Network settings** blade on your device tooview and modify hello configured DNS settings.</span></span> 

![네트워크 설정에서 DNS 설정](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

<span data-ttu-id="d389c-158">고가용성을 위해 필요한 tooconfigure 기본 두 hello 하 고 hello 초기 장치 배포 하는 동안 보조 DNS 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-158">For high availability, you are required tooconfigure both hello primary and hello secondary DNS servers during hello initial device deployment.</span></span>

<span data-ttu-id="d389c-159">**기본 DNS 서버** -Windows PowerShell hello를 사용 하 여 StorSimple toofirst hello 초기 설치 작업 동안 hello 주 DNS 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-159">**Primary DNS server** - You use hello Windows PowerShell for StorSimple toofirst specify hello Primary DNS server during hello initial setup.</span></span> <span data-ttu-id="d389c-160">Hello Windows PowerShell 인터페이스를 통해서만 hello 주 DNS 서버를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-160">You can reconfigure hello primary DNS server only via hello Windows PowerShell interface.</span></span> <span data-ttu-id="d389c-161">사용 하 여 hello `Set-HcsDNSClientServerAddress` 장치의 cmdlet toomodify hello 주 DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-161">Use hello `Set-HcsDNSClientServerAddress` cmdlet toomodify hello primary DNS server of your device.</span></span> <span data-ttu-id="d389c-162">에 대 한 자세한 내용은 이동 toosynxtax [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d389c-162">For more information, go toosynxtax for [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

<span data-ttu-id="d389c-163">**보조 DNS 서버** -toomodify hello 보조 DNS 서버를 사용 하 여 hello `Set-HcsDNSClientServerAddress` hello 장치의 hello Windows PowerShell 인터페이스에서 cmdlet 또는 **네트워크 설정** hello Azure StorSimple 장치의의 블레이드 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-163">**Secondary DNS server** - toomodify hello secondary DNS server, use hello `Set-HcsDNSClientServerAddress` cmdlet in hello Windows PowerShell interface of hello device or **Network settings** blade of your StorSimple device in hello Azure portal.</span></span>

<span data-ttu-id="d389c-164">Azure 포털에서 toomodify hello 보조 DNS 서버 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-164">toomodify hello secondary DNS server in Azure portal, perform hello following steps.</span></span>

1. <span data-ttu-id="d389c-165">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-165">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="d389c-166">Hello 장치 목록에서 선택 하 고 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-166">From hello list of devices, select and click your device.</span></span>

2. <span data-ttu-id="d389c-167">Hello에 **설정** 블레이드에서 너무 이동**장치 설정 > 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-167">In hello **Settings** blade, go too**Device settings > Network**.</span></span> <span data-ttu-id="d389c-168">Hello를 열어서이 **네트워크 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-168">This opens up hello **Network settings** blade.</span></span> <span data-ttu-id="d389c-169">**DNS 설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-169">Click **DNS settings** tile.</span></span> <span data-ttu-id="d389c-170">Hello 보조 DNS 서버 IP 주소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-170">Modify hello secondary DNS server IP address.</span></span>

    ![보조 DNS 서버 IP 주소 수정](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. <span data-ttu-id="d389c-172">Hello 명령 모음에서 클릭 **저장** 확인 메시지가 나타나면 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-172">From hello command bar, click **Save** and when prompted for confirmation, click **OK**.</span></span>

    ![변경 내용 저장 및 확인](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a><span data-ttu-id="d389c-174">네트워크 인터페이스 수정</span><span class="sxs-lookup"><span data-stu-id="d389c-174">Modify network interfaces</span></span>

<span data-ttu-id="d389c-175">장치에는 6개의 장치 네트워크 인터페이스가 있으며, 그 중 4개는 1GbE, 2개는 10GbE입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-175">Your device has six device network interfaces, four of which are 1 GbE and two of which are 10 GbE.</span></span> <span data-ttu-id="d389c-176">이러한 인터페이스는 DATA 0부터 DATA 5로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-176">These interfaces are labeled as DATA 0 – DATA 5.</span></span> <span data-ttu-id="d389c-177">DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 네트워크 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-177">DATA 0, DATA 1, DATA 4, and DATA 5 are 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE network interfaces.</span></span>

<span data-ttu-id="d389c-178">사용 하 여 hello **네트워크 설정** 블레이드 tooconfigure 각의 hello toobe 사용 되는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-178">Use hello **Network settings** blade tooconfigure each of hello interfaces toobe used.</span></span>

![네트워크 설정을 통해 네트워크 인터페이스 구성](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

<span data-ttu-id="d389c-180">tooensure 고가용성을 두 개 이상의 iSCSI 인터페이스 및 클라우드 지원 인터페이스를 두 개의 장치에 있는 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-180">tooensure high availability, we recommend that you have at least two iSCSI interfaces and two cloud-enabled interfaces on your device.</span></span> <span data-ttu-id="d389c-181">권장 사항이지만 사용하지 않는 인터페이스를 사용하지 않도록 설정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-181">We recommend but do not require that unused interfaces be disabled.</span></span>

<span data-ttu-id="d389c-182">각 네트워크 인터페이스에 대 한 매개 변수 뒤 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-182">For each network interface, hello following parameters are displayed:</span></span>

* <span data-ttu-id="d389c-183">**속도** – 사용자가 구성할 수 있는 매개 변수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-183">**Speed** – Not a user-configurable parameter.</span></span> <span data-ttu-id="d389c-184">DATA 0, DATA 1, DATA 4 및 DATA 5는 1GbE인 반면, DATA 2 및 DATA 3은 10GbE 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-184">DATA 0, DATA 1, DATA 4, and DATA 5 are always 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE interfaces.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d389c-185">속도 및 이중 교환 패턴은 항상 자동으로 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-185">Speed and duplex are always auto-negotiated.</span></span> <span data-ttu-id="d389c-186">Jumbo 프레임이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-186">Jumbo frames are not supported.</span></span>
  
* <span data-ttu-id="d389c-187">**인터페이스 상태** – 인터페이스를 설정하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-187">**Interface state** – An interface can be enabled or disabled.</span></span> <span data-ttu-id="d389c-188">사용 하도록 설정 하는 경우 hello 장치 toouse hello 인터페이스를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-188">If enabled, hello device will attempt toouse hello interface.</span></span> <span data-ttu-id="d389c-189">연결 된 toohello 네트워크 고 사용 하는 인터페이스에만 사용할 수 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-189">We recommend that only those interfaces that are connected toohello network and used be enabled.</span></span> <span data-ttu-id="d389c-190">사용하지 않는 모든 인터페이스는 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-190">Disable any interfaces that you are not using.</span></span>
* <span data-ttu-id="d389c-191">**인터페이스 형식** –이 매개 변수는 클라우드 저장소 트래픽에서 iSCSI 트래픽을 tooisolate 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-191">**Interface type** – This parameter allows you tooisolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="d389c-192">이 매개 변수는 hello 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-192">This parameter can be one of hello following:</span></span>
  
  * <span data-ttu-id="d389c-193">**클라우드 사용** -사용 하도록 설정 하면 hello 장치 hello 클라우드와 인터페이스 toocommunicate이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-193">**Cloud enabled** – when enabled, hello device will use this interface toocommunicate with hello cloud.</span></span>
  * <span data-ttu-id="d389c-194">**iSCSI 사용** – hello 장치에서 hello iSCSI 호스트와이 인터페이스 toocommunicate 사용할 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-194">**iSCSI enabled** – when enabled, hello device will use this interface toocommunicate with hello iSCSI host.</span></span>
    
    <span data-ttu-id="d389c-195">클라우드 저장소 트래픽에서 iSCSI 트래픽을 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-195">We recommend that you isolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="d389c-196">또한 참고 경우 호스트 hello 내에서 동일한 서브넷을 장치로 않아도 tooassign 게이트웨이; 그러나 호스트 장치는 다른 서브넷에 있으면 게이트웨이 tooassign을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-196">Also note if your host is within hello same subnet as your device, you do not need tooassign a gateway; however, if your host is in a different subnet than your device, you will need tooassign a gateway.</span></span>
* <span data-ttu-id="d389c-197">**IP 주소** – hello 네트워크 인터페이스 중 하나를 구성 하는 경우 가상 IP (VIP)를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-197">**IP address** – When you configure any of hello network interfaces, you must configure a virtual IP (VIP).</span></span> <span data-ttu-id="d389c-198">IPv4나 IPv6 또는 둘 다가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-198">This can be IPv4 or IPv6 or both.</span></span> <span data-ttu-id="d389c-199">Hello 개의 장치 네트워크 인터페이스가 hello IPv4 및 IPv6 주소 모음이 모두 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-199">Both hello IPv4 and IPv6 address families are supported for hello device network interfaces.</span></span> <span data-ttu-id="d389c-200">IPv4를 사용하는 경우 십진수 표기법으로 32비트 IP 주소(*xxx.xxx.xxx.xxx*)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-200">When using IPv4, specify a 32-bit IP address (*xxx.xxx.xxx.xxx*) in dot-decimal notation.</span></span> <span data-ttu-id="d389c-201">IPv6를 사용하는 경우 4자리 접두사를 제공하면 해당 접두사를 기반으로 사용자의 장치 네트워크 인터페이스에 대해 128비트 주소가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-201">When using IPv6, simply supply a 4-digit prefix, and a 128-bit address will be generated automatically for your device network interface based on that prefix.</span></span>
* <span data-ttu-id="d389c-202">**서브넷** –이 toohello 서브넷 마스크를 나타내며 hello Windows PowerShell 인터페이스를 통해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-202">**Subnet** – This refers toohello subnet mask and is configured via hello Windows PowerShell interface.</span></span>
* <span data-ttu-id="d389c-203">**게이트웨이** –이 hello에 있지 않은 노드와 toocommunicate을 시도할 때이 인터페이스에서 사용 해야 하는 hello 기본 게이트웨이 동일한 IP 주소 공간 (서브넷).</span><span class="sxs-lookup"><span data-stu-id="d389c-203">**Gateway** – This is hello default gateway that should be used by this interface when it attempts toocommunicate with nodes that are not within hello same IP address space (subnet).</span></span> <span data-ttu-id="d389c-204">hello 기본 게이트웨이 있어야 hello에 같은 주소 공간 (서브넷) hello 인터페이스 IP 주소로 hello 서브넷 마스크를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-204">hello default gateway must be in hello same address space (subnet) as hello interface IP address, as determined by hello subnet mask.</span></span>
* <span data-ttu-id="d389c-205">**고정 IP 주소** –이 필드는 DATA 0 hello를 구성 하는 동안에 사용할 수 있는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-205">**Fixed IP address** – This field is available only while you configure hello DATA 0 interface.</span></span> <span data-ttu-id="d389c-206">Tooconnect 업데이트나 hello 장치 문제 해결 등의 작업을 할 수 있습니다 직접 toohello 장치 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-206">For operations such as updates or troubleshooting hello device, you may need tooconnect directly toohello device controller.</span></span> <span data-ttu-id="d389c-207">고정 IP 주소는 hello 사용된 tooaccess 수 활성 hello와 장치에서 hello 수동 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-207">hello fixed IP address can be used tooaccess both hello active and hello passive controller on your device.</span></span>

> [!NOTE]
> * <span data-ttu-id="d389c-208">tooensure 적절 한 작업이 hello 인터페이스 속도 이중 hello 스위치에 연결 된 각 장치 인터페이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-208">tooensure proper operation, verify hello interface speed and duplex on hello switch that each device interface is connected to.</span></span> <span data-ttu-id="d389c-209">스위치 인터페이스는 기가비트 이더넷(1000Mbps)과 협상하거나 이에 대해 구성되며 전이중입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-209">Switch interfaces should either negotiate with or be configured for Gigabit Ethernet (1000 Mbps) and be full-duplex.</span></span> <span data-ttu-id="d389c-210">더 느린 속도 또는 반이중에서의 인터페이스 운영은 성능 문제를 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-210">Interfaces operating at slower speeds or in half-duplex will result in performance issues.</span></span>
> * <span data-ttu-id="d389c-211">toominimize 작업 중단과 가동 중지 시간에는 각각 hello 장치의 iSCSI 네트워크 인터페이스 포트에 연결 하는 hello 스위치에서 portfast를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-211">toominimize disruptions and downtime, we recommend that you enable portfast on each of hello switch ports that hello iSCSI network interface of your device will be connecting to.</span></span> <span data-ttu-id="d389c-212">이렇게 하면 장애 조치의 hello 이벤트에서 네트워크 연결을 신속 하 게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-212">This will ensure that network connectivity can be established quickly in hello event of a failover.</span></span>

### <a name="configure-data-0"></a><span data-ttu-id="d389c-213">DATA 0 구성</span><span class="sxs-lookup"><span data-stu-id="d389c-213">Configure DATA 0</span></span>

<span data-ttu-id="d389c-214">DATA 0은 기본적으로 클라우드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-214">DATA 0 is cloud-enabled by default.</span></span> <span data-ttu-id="d389c-215">데이터 0을 구성할 때 인 필수 tooconfigure 두 개의 고정된 IP 주소를 각 컨트롤러에 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-215">When configuring DATA 0, you are also required tooconfigure two fixed IP addresses, one for each controller.</span></span> <span data-ttu-id="d389c-216">고정 IP 주소 이러한 직접 사용 하는 tooaccess hello 장치 컨트롤러를 수 있습니다 및는 hello 장치 또는 문제 해결을 위한 hello 목적 hello 컨트롤러를 액세스 하는 경우에 업데이트를 설치 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-216">These fixed IP addresses can be used tooaccess hello device controllers directly and are useful when you install updates on hello device or when you access hello controllers for hello purpose of troubleshooting.</span></span>

<span data-ttu-id="d389c-217">데이터 0 설정 블레이드에서 hello 통해 IP 컨트롤러 고정 hello를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-217">You can reconfigure hello fixed IP controllers via hello DATA 0 settings blade.</span></span>

![네트워크 인터페이스 구성 - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> <span data-ttu-id="d389c-219">고정 IP 주소 hello 컨트롤러에 대 한 hello hello 업데이트 toohello 장치를 서비스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-219">hello fixed IP addresses for hello controller are used for servicing hello updates toohello device.</span></span> <span data-ttu-id="d389c-220">따라서 hello 고정 Ip는 라우팅 가능 하 고 수 tooconnect toohello 인터넷 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-220">Therefore, hello fixed IPs must be routable and able tooconnect toohello Internet.</span></span>

### <a name="configure-data-1---data-5"></a><span data-ttu-id="d389c-221">DATA 1~DATA 5 구성</span><span class="sxs-lookup"><span data-stu-id="d389c-221">Configure DATA 1 - DATA 5</span></span>

<span data-ttu-id="d389c-222">1-DATA 5 네트워크 인터페이스가 데이터에 대 한 hello 스크린 샷 뒤에 표시 된 대로 모든 hello 네트워크 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-222">For DATA 1 - DATA 5 network interfaces, you can configure all hello network settings as shown in hello following screenshot:</span></span>

![네트워크 인터페이스 구성 DATA 1~DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a><span data-ttu-id="d389c-224">IP 교체 또는 재할당</span><span class="sxs-lookup"><span data-stu-id="d389c-224">Swap or reassign IPs</span></span>

<span data-ttu-id="d389c-225">현재, 네트워크 인터페이스에 hello 컨트롤러 할당 된 사용 중인 VIP (hello 하 여 같은 장치 또는 hello 네트워크의 다른 장치), hello 컨트롤러 장애 조치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-225">Currently, if any network interface on hello controller is assigned a VIP that is in use (by hello same device or another device in hello network), then hello controller will fail over.</span></span> <span data-ttu-id="d389c-226">장치 네트워크 인터페이스의 VIP를 교환하거나 다시 할당하는 경우 중복 IP 상황을 만들 수 있는 만큼 적절한 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-226">If you swap or reassign VIPs for a device network interface, you must follow a proper procedure as you could create a duplicate IP situation.</span></span>

<span data-ttu-id="d389c-227">다음 단계 tooswap hello 수행 또는 hello 네트워크 인터페이스에 대 한 hello Vip 재할당:</span><span class="sxs-lookup"><span data-stu-id="d389c-227">Perform hello following steps tooswap or reassign hello VIPs for any of hello network interfaces:</span></span>

#### <a name="tooreassign-ips"></a><span data-ttu-id="d389c-228">tooreassign Ip</span><span class="sxs-lookup"><span data-stu-id="d389c-228">tooreassign IPs</span></span>

1. <span data-ttu-id="d389c-229">두 인터페이스에 대 한 지우기 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-229">Clear hello IP address for both interfaces.</span></span>
2. <span data-ttu-id="d389c-230">Hello IP 주소를 지운 후 개별 인터페이스 toohello hello 새 IP 주소 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-230">After hello IP addresses are cleared, assign hello new IP addresses toohello respective interfaces.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d389c-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d389c-231">Next steps</span></span>

* <span data-ttu-id="d389c-232">너무 방법에 대해 알아봅니다[StorSimple 장치에 대 한 MPIO 구성](storsimple-8000-configure-mpio-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-232">Learn how too[configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span>
* <span data-ttu-id="d389c-233">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d389c-233">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

