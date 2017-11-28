---
title: "Active Directory 자동 장치 등록 FAQ aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="11015-103">Azure Active Directory 자동 장치 등록 FAQ</span><span class="sxs-lookup"><span data-stu-id="11015-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="11015-104">**Q: 저는 최근에 hello 장치를 등록합니다. Hello 장치 hello Azure 포털에서에서 내 사용자 정보에서 볼 수 없는 이유**</span><span class="sxs-lookup"><span data-stu-id="11015-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="11015-105">**A:** 자동 장치 등록 된 도메인에 가입 하는 Windows 10 장치 hello 사용자 정보에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="11015-106">모든 장치 toouse PowerShell toosee 필요.</span><span class="sxs-lookup"><span data-stu-id="11015-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="11015-107">만 hello 다음 장치 아래에 나열 됩니다 hello 사용자 정보:</span><span class="sxs-lookup"><span data-stu-id="11015-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="11015-108">엔터프라이즈에 조인되지 않은 모든 개인 장치</span><span class="sxs-lookup"><span data-stu-id="11015-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="11015-109">모든 비 Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="11015-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="11015-110">모든 비 Windows 장치</span><span class="sxs-lookup"><span data-stu-id="11015-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="11015-111">**Q: 이유를 볼 수 없습니다 hello Azure 포털에서에서 Azure Active Directory에 등록 하는 모든 hello 장치?**</span><span class="sxs-lookup"><span data-stu-id="11015-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="11015-112">**A:** 현재,이 방법은 toosee 없습니다 등록 된 모든 장치 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="11015-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="11015-113">Azure PowerShell toofind 모든 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="11015-114">자세한 내용은 참조 hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11015-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="11015-115">**Q: 어떻게 hello 클라이언트의 어떤 hello 장치 등록 상태를 알 수 있습니까 됩니다?**</span><span class="sxs-lookup"><span data-stu-id="11015-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="11015-116">**A:** hello 장치 등록 상태에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="11015-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="11015-117">어떤 hello 장치가</span><span class="sxs-lookup"><span data-stu-id="11015-117">What hello device is</span></span>
- <span data-ttu-id="11015-118">등록된 방법</span><span class="sxs-lookup"><span data-stu-id="11015-118">How it was registered</span></span> 
- <span data-ttu-id="11015-119">Tooit을 관련 하는 모든 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="11015-120">**Q: 이유는 삭제 하려면 장치에 hello Azure 포털 또는 Windows PowerShell을 사용 하 여 여전히 나열 등록?**</span><span class="sxs-lookup"><span data-stu-id="11015-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="11015-121">**A:** 이것은 의도적인 작동입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-121">**A:** This is by design.</span></span> <span data-ttu-id="11015-122">hello 장치 액세스 tooresources hello 클라우드에서 없을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="11015-123">Tooremove hello 장치를 다시 등록 하는 경우 수동 작업이 toobe hello 장치에 대해 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="11015-124">온-프레미스 AD 도메인에 조인된 Windows 10 및 Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="11015-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="11015-125">관리자 권한으로 hello 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="11015-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="11015-126">`dsregcmd.exe /debug /leave`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="11015-127">로그 아웃 하 고 다시 hello 장치를 등록 하는 tootrigger hello 예약 된 작업에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="11015-128">온-프레미스 AD 도메인에 조인된 다른 Windows 플랫폼:</span><span class="sxs-lookup"><span data-stu-id="11015-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="11015-129">관리자 권한으로 hello 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="11015-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="11015-130">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="11015-131">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="11015-132">**Q: Azure Portal에서 중복된 장치 항목이 나타나는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="11015-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="11015-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="11015-133">**A:**</span></span>

-   <span data-ttu-id="11015-134">Windows 10 및 Windows Server 2016, toounjoin 시도 반복된 하 고 다시 가입 하는 경우 동일한 장치 hello에 대 한 중복 된 항목이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="11015-135">추가 회사 또는 학교 계정을 사용 하는 각 windows 사용자 hello로 새 장치 레코드를 만들어집니다 추가 회사 또는 학교 계정을 사용한 경우 동일한 장치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="11015-136">다른 Windows 플랫폼에는 온-프레미스 AD 도메인에 가입 된 자동 등록을 사용 하 여 hello와 새 장치 레코드가 만들어집니다 각 도메인 사용자가 hello 장치에 로그온에 대 한 동일한 장치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="11015-137">초기화 된, AADJ 컴퓨터를 다시 설치 하 고 다시 조인 된 hello 동일한 이름, hello 사용 하 여 다른 레코드로 표시 됩니다 동일한 장치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="11015-138">**Q: 액세스 이유는 사용자 여전히 리소스 hello Azure 포털에서에서 비활성화 하는 장치에서?**</span><span class="sxs-lookup"><span data-stu-id="11015-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="11015-139">**A:** 적용 revoke toobe tooan 시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="11015-140">손실 된 장치에 대 한 사용자가 hello 장치에 액세스할 수 없다고 hello 장치 tooensure 초기화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="11015-141">자세한 내용은 [Intune에서 관리를 위해 장치 등록](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11015-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="11015-142">**Q: 사용자에게 "여기에서 해당 위치로 이동할 수 없습니다." 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="11015-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="11015-143">**A:** 사용자가 차단 되 고이 메시지가 특정 조건부 액세스 규칙 toorequire 특정 장치 상태를 구성 하는 경우 hello 장치 hello 조건을 충족 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="11015-144">Hello 규칙을 평가 하 고 해당 hello 장치를 확인 하십시오 수 toomeet hello 조건 tooavoid이이 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="11015-145">**Q: hello 장치 레코드 hello Azure 포털에서에서 사용자 정보 hello에서 참조 하 고 hello 클라이언트에 등록 된 hello 상태를 볼 수 있습니다. 조건부 액세스를 사용할 수 있게 제대로 설정되어 있는 것인가요?**</span><span class="sxs-lookup"><span data-stu-id="11015-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="11015-146">**A:** hello 장치 기록 (deviceID) 및 Azure 포털 hello에 대 한 상태가 hello 클라이언트와 일치 하 고 조건부 액세스에 대 한 평가 조건을 만족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="11015-147">자세한 내용은 [Azure Active Directory Device 등록 시작](active-directory-device-registration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11015-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="11015-148">**Q: 왜 "사용자 이름 또는 암호가 올바르지 않습니다." 메시지가 장치에 대 한 I에 막 합류 tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="11015-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="11015-149">**A:** 이 시나리오에 대한 일반적인 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="11015-150">사용자 자격 증명이 더 이상 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="11015-151">컴퓨터가 없습니다 toocommunicate Azure Active Directory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="11015-152">네트워크 연결 문제가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="11015-153">hello Azure AD Join 필수 조건은 충족 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="11015-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="11015-154">에 대 한 hello 단계를 따랐는지 확인 하십시오 [기능 tooWindows 10 장치의 Azure Active Directory Join을 통해 클라우드 확장](active-directory-azureadjoin-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="11015-155">페더레이션된 로그인에는 페더레이션 서버 toosupport WS-트러스트 활성 끝점이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11015-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="11015-156">**Q: 표시 되는 이유 hello "Oops... 오류가 발생 했습니다!" 내 PC를 가입시 키 려 할 때 대화 마십시오?**</span><span class="sxs-lookup"><span data-stu-id="11015-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="11015-157">**A:** Intune에 Azure Active Directory를 등록했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="11015-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="11015-158">자세한 내용은 [Windows 장치 관리 설정](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11015-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="11015-159">**PC의 경우 오류 정보 받지 않는 경우 하지만 실패 시도 toojoin 내 q 했습니까?**</span><span class="sxs-lookup"><span data-stu-id="11015-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="11015-160">**A:** toohello 장치 hello 기본 제공 관리자 계정을 사용 하 여 해당 hello 사용자가 로그인 한 가지 가능한 원인은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11015-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="11015-161">Azure Active Directory Join toocomplete hello 설치 프로그램을 사용 하기 전에 다른 로컬 계정을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="11015-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="11015-162">**Q: 자동 장치 등록의 hello 설치에 대 한 지침을 어디서 찾을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="11015-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="11015-163">**A:** 자세한 지침을 참조 하십시오. [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="11015-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="11015-164">**Q: 어디에 있습니까 문제 해결 hello 자동 장치 등록에 대 한 내용은?**</span><span class="sxs-lookup"><span data-stu-id="11015-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="11015-165">**A:** 문제 해결 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11015-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="11015-166">가입 된 컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="11015-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="11015-167">Windows 하위 클라이언트에 대 한 컴퓨터 tooAzure AD 가입 된 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="11015-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

