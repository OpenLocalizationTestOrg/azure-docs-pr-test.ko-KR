---
title: "사용 하 여 aaaManaging 장치 hello Azure 포털-미리 보기 | Microsoft Docs"
description: "Toouse Azure 포털 toomanage 장치 hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="62008-103">Azure 포털 hello-미리 보기를 사용 하 여 장치 관리</span><span class="sxs-lookup"><span data-stu-id="62008-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="62008-104">이 기능은 현재 공개 미리 보기로 제공되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-104">This capability currently is in public preview.</span></span> <span data-ttu-id="62008-105">Toorevert 준비 하거나 변경 내용을 모두 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="62008-106">hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory (Azure AD) 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="62008-107">그러나 hello 기능이 일반 공급 되 면 hello 기능의 일부 측면 Azure Active Directory premium 구독에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="62008-108">Azure AD(Active Directory)의 장치 관리를 사용하면 보안 및 규정 준수에 대한 표준을 충족하는 장치에서 사용자 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="62008-109">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="62008-109">This topic:</span></span>

- <span data-ttu-id="62008-110">Hello에 익숙한 것으로 가정 [Azure Active Directory의 toodevice 관리 소개](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="62008-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="62008-111">Azure 포털을 hello를 사용 하 여 장치를 관리 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="62008-112">hello Azure 포털에서에서 장치 toomanage 해야 tooclick **장치** hello에 **관리** hello hello 섹션 **Azure Active Directory** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Intune 장치 관리](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="62008-114">장치 설정 구성</span><span class="sxs-lookup"><span data-stu-id="62008-114">Configure device settings</span></span>

<span data-ttu-id="62008-115">toomanage toobe 필요한 hello Azure 포털을 사용 하 여 장치를 등록 하거나 tooAzure AD 가입 하십시오.</span><span class="sxs-lookup"><span data-stu-id="62008-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="62008-116">관리자로 서 등록 하 고 hello 장치 설정을 구성 하 여 장치를 가입 hello 과정을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Intune 장치 관리](./media/device-management-azure-portal/22.png)


<span data-ttu-id="62008-118">hello 장치 설정 블레이드에서 tooconfigure가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="62008-119">**사용자가 장치 tooAzure AD에 조인할 수 있습니다.** -이 설정 장치 tooAzure AD 가입할 수 있는 tooselect hello 사용자가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="62008-120">hello 기본값은 **모든**합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-120">hello default is **All**.</span></span>

- <span data-ttu-id="62008-121">**Azure AD에 추가 하는 로컬 관리자가 가입 장치** -장치에 대 한 로컬 관리자 권한을 hello 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="62008-122">여기에 추가 하는 사용자가 toohello 추가 *장치 관리자* Azure ad에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="62008-123">Azure AD의 전역 관리자 및 장치 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="62008-124">이 옵션에는 Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 등의 제품을 통해 사용할 수 있는 premium edition 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="62008-125">**Azure ad 사용자가 장치를 등록할 수 있습니다** -tooconfigure 설정을 tooallow 장치 toobe이 Azure AD에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="62008-126">선택 하는 경우 **None**, Azure AD 조인 되지 않은 tooregister 또는 Azure AD 조인 하이브리드 장치 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="62008-127">Office 365용 Microsoft Intune 또는 MDM(모바일 장치 관리)에 등록하려면 먼저 장치를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="62008-128">이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음**은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="62008-129">**Multi-factor Auth toojoin 장치가 필요** -두 번째 인증 단계 자신의 장치 tooAzure AD toojoin 사용자가 필요한 tooprovide 있는지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="62008-130">hello 기본값은 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-130">hello default is **No**.</span></span> <span data-ttu-id="62008-131">그러나 장치를 등록하는 경우 Multi-Factor Authentication을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="62008-132">이 서비스에 대해 multi-factor authentication을 활성화 하기 전에 multi-factor authentication 자신의 장치를 등록 하는 hello 사용자에 대해 구성 된 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="62008-133">다양한 Azure Multi-Factor Authentication 서비스에 대한 자세한 내용은 [Azure Multi-Factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62008-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="62008-134">**최대 장치 수가** -이 설정을 사용 하면 Azure AD에서 사용자가 장치의 tooselect hello 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="62008-135">사용자가이 할당량에 도달 하면 하나까지 수 tooadd 추가 장치 수 없습니다는 또는 이상의 hello 기존 장치가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="62008-136">hello 장치 따옴표는 모든 장치는 Azure AD 조인 또는 현재 등록 된 Azure AD에 대해 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="62008-137">hello 기본값은 **20**합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-137">hello default value is **20**.</span></span>

- <span data-ttu-id="62008-138">**사용자가 장치에서 설정 및 응용 프로그램 데이터를 동기화가** -기본적으로이 설정은 너무**NONE**합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="62008-139">특정 사용자 또는 그룹 중 하나 또는 모두를 선택 하면 해당 Windows 10 장치에서 hello 사용자의 설정 및 응용 프로그램 데이터 toosync 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="62008-140">Windows 10에서 동기화가 작동되는 방식에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62008-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="62008-141">이 옵션에는 Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 등의 제품을 통해 사용할 수 있는 프리미엄 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Intune 장치 관리](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="62008-143">장치 찾기</span><span class="sxs-lookup"><span data-stu-id="62008-143">Locate devices</span></span>

<span data-ttu-id="62008-144">관리자로 서 hello Azure 포털의에서 두 가지 옵션이 있습니다 toolocate 등록 하 고 장치를 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="62008-145">**모든 장치** hello에 **관리** hello 섹션 **장치** 블레이드</span><span class="sxs-lookup"><span data-stu-id="62008-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![모든 장치](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="62008-147">**장치** hello에 **관리** 섹션은 **사용자** 블레이드</span><span class="sxs-lookup"><span data-stu-id="62008-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![모든 장치](./media/device-management-azure-portal/43.png)



<span data-ttu-id="62008-149">두 옵션으로 얻을 수 있습니다 tooa 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="62008-150">필터로 hello 표시 이름을 사용 하 여 장치에 대 한 toosearch가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="62008-151">등록 및 조인된 장치의 자세한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="62008-152">일반 장치 관리 작업을 tooperform 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-152">Enables you tooperform common device management tasks</span></span>
   

![모든 장치](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="62008-154">장치 관리 작업</span><span class="sxs-lookup"><span data-stu-id="62008-154">Device management tasks</span></span>

<span data-ttu-id="62008-155">관리자로 서 관리할 수 있습니다 hello 등록 또는 장치를 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="62008-156">이 섹션에서는 일반 장치 관리 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="62008-157">**Intune 장치 관리** - Intune 관리자인 경우 **Microsoft Intune**으로 표시된 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="62008-158">관리자는 추가 장치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-158">An administrator can see additional device</span></span> 

![Intune 장치 관리](./media/device-management-azure-portal/31.png)


<span data-ttu-id="62008-160">**Azure AD 장치 사용/사용 안 함**</span><span class="sxs-lookup"><span data-stu-id="62008-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="62008-161">tooenable 또는 사용 안 함 장치를 Azure AD에서 toobe 전역 관리자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="62008-162">장치를 사용하지 않도록 설정하면 장치에서 Azure AD 리소스에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="62008-163">눌러 수 toodisable hello 장치 *...*</span><span class="sxs-lookup"><span data-stu-id="62008-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="62008-164">자세한 내용은 hello 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-164">click hello device for additional details.</span></span>

 
![Intune 장치 관리](./media/device-management-azure-portal/33.png)

<span data-ttu-id="62008-166">Hello에 hello 상태를 변경 하는 장치를 사용 하지 않도록 설정 **ENABLED** 열 너무**아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![장치 사용 안 함](./media/device-management-azure-portal/32.png)


<span data-ttu-id="62008-168">**Azure AD 장치를 삭제** -toodelete 장치를 Azure AD에서 toobe 전역 관리자를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="62008-169">장치 삭제:</span><span class="sxs-lookup"><span data-stu-id="62008-169">Deleting a device:</span></span>
 
- <span data-ttu-id="62008-170">장치에서 Azure AD 리소스에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="62008-171">모든 예를 들어 연결 된 toohello 장치 된 세부 사항, Windows 장치에 대 한 BitLocker 키를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="62008-172">복구할 수 없으며, 반드시 필요한 경우가 아니면 권장되지 않는 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="62008-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="62008-173">장치를 다른 관리 기관 (예: Microsoft Intune)에 의해 관리 되는 경우 해당 hello 장치 초기화 / Azure AD에서 hello 장치를 삭제 하기 전에 사용 중지 된에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="62008-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="62008-174">“…”를 선택하여</span><span class="sxs-lookup"><span data-stu-id="62008-174">You can either select “…”</span></span> <span data-ttu-id="62008-175">toodelete hello 장치 또는 추가 세부 정보에 대 한 hello 장치를 클릭</span><span class="sxs-lookup"><span data-stu-id="62008-175">toodelete hello device or click on hello device for additional details</span></span>
 
![장치 삭제](./media/device-management-azure-portal/34.png)


<span data-ttu-id="62008-177">**보거나 장치 ID를 복사** -hello 장치 또는 PowerShell을 사용 하 여 문제를 해결 하는 동안에 장치 ID tooverify hello 장치 ID 세부 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="62008-178">tooaccess hello 복사 옵션을 hello 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-178">tooaccess hello copy option, click hello device.</span></span>

![장치 ID 보기](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="62008-180">**보거나 BitLocker 키를 복사** -관리자가 볼 수 있으며 복사 hello BitLocker 키 toohelp 사용자 toorecover의 암호화 된 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="62008-181">이러한 키는 암호화되고 해당 키가 Azure AD에 저장된 Windows 장치에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="62008-182">Hello 장치의 세부 정보에 액세스할 때이 키를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-182">You can copy these keys when accessing details of hello device.</span></span>
 
![BitLocker 키 보기](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="62008-184">감사 로그</span><span class="sxs-lookup"><span data-stu-id="62008-184">Audit logs</span></span>


<span data-ttu-id="62008-185">hello 장치 활동은 hello 활동 로그를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="62008-186">이 작업 트리거 hello 장치 등록 서비스에서 또는 hello 사용자가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62008-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="62008-187">장치 만들기 및 hello 장치 소유자/사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="62008-188">Toodevice 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62008-188">Changes toodevice settings</span></span>

- <span data-ttu-id="62008-189">장치 삭제 또는 업데이트 등의 장치 작업</span><span class="sxs-lookup"><span data-stu-id="62008-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="62008-190">데이터 감사 하 여 항목 지점 toohello는 **감사 로그** hello에 **활동** hello 섹션 **장치* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![감사 로그](./media/device-management-azure-portal/61.png)


<span data-ttu-id="62008-192">감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62008-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="62008-193">hello 발생의 hello 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="62008-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="62008-194">hello 대상</span><span class="sxs-lookup"><span data-stu-id="62008-194">hello targets</span></span>

- <span data-ttu-id="62008-195">초기자 hello / 행위자 (누가) 활동</span><span class="sxs-lookup"><span data-stu-id="62008-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="62008-196">hello 활동 (작업)</span><span class="sxs-lookup"><span data-stu-id="62008-196">hello activity (what)</span></span>

![감사 로그](./media/device-management-azure-portal/63.png)

<span data-ttu-id="62008-198">클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.</span><span class="sxs-lookup"><span data-stu-id="62008-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![감사 로그](./media/device-management-azure-portal/64.png)


<span data-ttu-id="62008-200">hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 감사 데이터를 보고.</span><span class="sxs-lookup"><span data-stu-id="62008-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="62008-201">범주</span><span class="sxs-lookup"><span data-stu-id="62008-201">Catergory</span></span>
- <span data-ttu-id="62008-202">활동 리소스 종류</span><span class="sxs-lookup"><span data-stu-id="62008-202">Activity resource type</span></span>
- <span data-ttu-id="62008-203">작업</span><span class="sxs-lookup"><span data-stu-id="62008-203">Activity</span></span>
- <span data-ttu-id="62008-204">날짜 범위</span><span class="sxs-lookup"><span data-stu-id="62008-204">Date range</span></span>
- <span data-ttu-id="62008-205">대상</span><span class="sxs-lookup"><span data-stu-id="62008-205">Target</span></span>
- <span data-ttu-id="62008-206">초기자(작업자)</span><span class="sxs-lookup"><span data-stu-id="62008-206">Initiated By (Actor)</span></span>

<span data-ttu-id="62008-207">또한 toohello 필터를 검색할 수 있습니다 특정 항목에 대 한.</span><span class="sxs-lookup"><span data-stu-id="62008-207">In addition toohello filters, you can search for specific entries.</span></span>

![감사 로그](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="62008-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62008-209">Next steps</span></span>

* [<span data-ttu-id="62008-210">Azure Active Directory의 toodevice 관리 소개</span><span class="sxs-lookup"><span data-stu-id="62008-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



