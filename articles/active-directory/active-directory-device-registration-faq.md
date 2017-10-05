---
title: "Azure Active Directory 자동 장치 등록 FAQ| Microsoft Docs"
description: "Azure Active Directory를 사용한 장치 등록과 관련된 FAQ입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="2654a-103">Azure Active Directory 자동 장치 등록 FAQ</span><span class="sxs-lookup"><span data-stu-id="2654a-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="2654a-104">**Q: 최근에 장치를 등록했습니다. Azure Portal에서 내 사용자 정보에 장치가 표시되지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="2654a-105">**A:** 자동 장치 등록이 지정된 도메인 연결 Windows 10 장치가 사용자 정보 아래에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="2654a-106">모든 장치를 표시하려면 PowerShell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="2654a-107">다음 장치만 사용자 정보 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="2654a-108">엔터프라이즈에 조인되지 않은 모든 개인 장치</span><span class="sxs-lookup"><span data-stu-id="2654a-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="2654a-109">모든 비 Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2654a-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="2654a-110">모든 비 Windows 장치</span><span class="sxs-lookup"><span data-stu-id="2654a-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="2654a-111">**Q: Azure Portal에서 Azure Active Directory에 등록된 모든 장치를 볼 수는 없는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="2654a-112">**A:** 현재 방법이 Azure Portal에서 등록된 모든 장치를 볼 수 있는 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="2654a-113">모든 장치를 찾으려면 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="2654a-114">자세한 내용은 [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="2654a-115">**Q: 클라이언트의 장치 등록 상태를 어떻게 알 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="2654a-116">**A:** 장치 등록 상태는 다음에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="2654a-117">장치가 무엇인지</span><span class="sxs-lookup"><span data-stu-id="2654a-117">What the device is</span></span>
- <span data-ttu-id="2654a-118">등록된 방법</span><span class="sxs-lookup"><span data-stu-id="2654a-118">How it was registered</span></span> 
- <span data-ttu-id="2654a-119">관련된 모든 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2654a-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="2654a-120">**Q: Azure Portal에서 또는 Windows PowerShell을 사용하여 삭제한 장치가 여전히 등록된 것으로 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="2654a-121">**A:** 이것은 의도적인 작동입니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-121">**A:** This is by design.</span></span> <span data-ttu-id="2654a-122">장치는 클라우드의 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="2654a-123">장치를 제거하고 다시 등록하려면 장치에서 직접 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="2654a-124">온-프레미스 AD 도메인에 조인된 Windows 10 및 Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="2654a-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="2654a-125">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="2654a-126">`dsregcmd.exe /debug /leave`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="2654a-127">로그아웃했다가 로그인하여 장치를 다시 등록하는 예약된 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="2654a-128">온-프레미스 AD 도메인에 조인된 다른 Windows 플랫폼:</span><span class="sxs-lookup"><span data-stu-id="2654a-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="2654a-129">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="2654a-130">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="2654a-131">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="2654a-132">**Q: Azure Portal에서 중복된 장치 항목이 나타나는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="2654a-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="2654a-133">**A:**</span></span>

-   <span data-ttu-id="2654a-134">Windows 10 및 Windows Server 2016의 경우 같은 장치를 반복해서 조인 해제했다가 다시 조인하면 중복된 항목이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="2654a-135">회사 또는 학교 계정 추가를 사용한 경우 회사 또는 학교 계정 추가를 사용하는 각 Windows 사용자는 장치 이름이 같은 새 장치 레코드를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="2654a-136">자동 등록을 사용하여 온-프레미스 AD 도메인에 조인된 다른 Windows 플랫폼은 장치에 로그인하는 각 도메인 사용자에 대해 장치 이름이 같은 새 장치 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="2654a-137">초기화되었다가 같은 이름으로 다시 설치되고 다시 조인된 AADJ 장치는 장치 이름이 같은 다른 레코드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="2654a-138">**Q: Azure Portal에서 사용하지 않도록 설정한 장치에서 여전히 리소스에 액세스할 수 있는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="2654a-139">**A:** 해지가 적용되는 데는 최대 1시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="2654a-140">분실한 장치의 경우에는 장치를 초기화하여 사용자가 장치에 액세스하지 못하게 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="2654a-141">자세한 내용은 [Intune에서 관리를 위해 장치 등록](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="2654a-142">**Q: 사용자에게 "여기에서 해당 위치로 이동할 수 없습니다." 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="2654a-143">**A:** 특정 장치 상태를 요구하도록 특정 조건부 액세스 규칙을 구성했거나 장치가 조건을 충족하지 않을 경우 사용자가 차단되고 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="2654a-144">규칙을 평가하고 장치가 이 조건을 충족하는지 확인하여 이 메시지가 표시되지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="2654a-145">**Q: Azure Portal에서 사용자 정보에 장치 레코드가 표시되고 클라이언트에 등록된 상태로 표시됩니다. 조건부 액세스를 사용할 수 있게 제대로 설정되어 있는 것인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="2654a-146">**A:** Azure Portal의 장치 레코드(deviceID) 및 상태가 클라이언트와 일치하고 조건부 액세스를 위한 평가 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="2654a-147">자세한 내용은 [Azure Active Directory Device 등록 시작](active-directory-device-registration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="2654a-148">**Q: Azure AD에 조인한 장치에 대해 "사용자 이름 또는 암호가 올바르지 않습니다." 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="2654a-149">**A:** 이 시나리오에 대한 일반적인 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="2654a-150">사용자 자격 증명이 더 이상 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="2654a-151">컴퓨터가 Azure Active Directory와 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="2654a-152">네트워크 연결 문제가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="2654a-153">Azure AD 조인 필수 구성 요소가 충족되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="2654a-154">[Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장](active-directory-azureadjoin-overview.md)에 대한 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="2654a-155">페더레이션 로그인을 수행하려면 페더레이션 서버가 Ws-Trust 활성 끝점을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="2654a-156">**Q: PC를 조인하려고 할 때 "오류가 발생했습니다." 대화 상자가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="2654a-157">**A:** Intune에 Azure Active Directory를 등록했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="2654a-158">자세한 내용은 [Windows 장치 관리 설정](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="2654a-159">**Q: 오류 정보가 표시되지 않더라도 PC 조인 시도가 실패하는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="2654a-160">**A:** 한 가지 가능한 원인은 사용자가 기본 제공 관리자 계정을 사용하여 장치에 로그인했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2654a-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="2654a-161">Azure Active Directory 조인을 사용하여 설치를 완료하기 전에 다른 로컬 계정을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="2654a-162">**Q: 자동 장치 등록의 설치에 대한 지침은 어디에서 찾나요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="2654a-163">**A:** 자세한 지침은 [Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="2654a-164">**Q: 자동 장치 등록에 대한 문제 해결 정보는 어디에서 찾나요?**</span><span class="sxs-lookup"><span data-stu-id="2654a-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="2654a-165">**A:** 문제 해결 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2654a-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="2654a-166">Windows 10 및 Windows Server 2016에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2654a-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="2654a-167">Windows 하위 수준 클라이언트에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2654a-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

