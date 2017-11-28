---
title: "Azure AD Connect: 장치 쓰기 저장 사용 | Microsoft Docs"
description: "이 세부 정보를 어떻게 문서 Azure AD Connect를 사용 하 여 tooenable 장치 쓰기 저장"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a><span data-ttu-id="5d934-103">Azure AD Connect: 장치 쓰기 저장 사용</span><span class="sxs-lookup"><span data-stu-id="5d934-103">Azure AD Connect: Enabling device writeback</span></span>
> [!NOTE]
> <span data-ttu-id="5d934-104">구독 tooAzure AD Premium 장치 쓰기 저장에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-104">A subscription tooAzure AD Premium is required for device writeback.</span></span>
> 
> 

<span data-ttu-id="5d934-105">hello 설명서에서는 Azure AD Connect에서 tooenable hello 장치 쓰기 저장 기능 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-105">hello following documentation provides information on how tooenable hello device writeback feature in Azure AD Connect.</span></span> <span data-ttu-id="5d934-106">장치 쓰기 저장은 hello 다음 시나리오에서에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-106">Device Writeback is used in hello following scenarios:</span></span>

* <span data-ttu-id="5d934-107">장치 tooADFS에 따라 조건부 액세스를 사용 하도록 설정 (2012 R2 이상) 보호 된 응용 프로그램 (신뢰 당사자 트러스트).</span><span class="sxs-lookup"><span data-stu-id="5d934-107">Enable conditional access based on devices tooADFS (2012 R2 or higher) protected applications (relying party trusts).</span></span>

<span data-ttu-id="5d934-108">이 방법은 보안을 강화 하 고 tooapplications에 액세스 하는 보증 tootrusted 장치에만 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-108">This provides additional security and assurance that access tooapplications is granted only tootrusted devices.</span></span> <span data-ttu-id="5d934-109">조건부 액세스에 대한 자세한 내용은 [조건부 액세스로 위험 관리](../active-directory-conditional-access.md) 및 [Azure Active Directory Device Registration을 사용하여 온-프레미스 조건부 액세스 설정](../active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d934-109">For more information on conditional access, see [Managing Risk with Conditional Access](../active-directory-conditional-access.md) and [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

> [!IMPORTANT]
> <li><span data-ttu-id="5d934-110">장치는 hello 사용자로 포리스트 동일 hello에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-110">Devices must be located in hello same forest as hello users.</span></span> <span data-ttu-id="5d934-111">장치 다시 작성 해야 tooa 단일 포리스트, 이후이 기능은 사용자의 다중 포리스트 배포를 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-111">Since devices must be written back tooa single forest, this feature does not currently support a deployment with multiple user forests.</span></span></li>
> <li><span data-ttu-id="5d934-112">Toohello 온-프레미스 Active Directory 포리스트에 하나의 장치 등록 구성 개체를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-112">Only one device registration configuration object can be added toohello on-premises Active Directory forest.</span></span> <span data-ttu-id="5d934-113">이 기능은 토폴로지 여기서 hello 온-프레미스 Active Directory에서 동기화 된 toomultiple Azure AD 디렉터리와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-113">This feature is not compatible with a topology where hello on-premises Active Directory is synchronized toomultiple Azure AD directories.</span></span></li>> 

## <a name="part-1-install-azure-ad-connect"></a><span data-ttu-id="5d934-114">1부: Azure AD Connect 설치</span><span class="sxs-lookup"><span data-stu-id="5d934-114">Part 1: Install Azure AD Connect</span></span>
1. <span data-ttu-id="5d934-115">사용자 지정 또는 Express 설정을 사용하여 Azure AD Connect를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-115">Install Azure AD Connect using Custom or Express settings.</span></span> <span data-ttu-id="5d934-116">모든 사용자 및 장치 쓰기 저장을 활성화 하기 전에 동기화 그룹으로 toostart를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-116">Microsoft recommends toostart with all users and groups successfully synchronized before you enable device writeback.</span></span>

## <a name="part-2-prepare-active-directory"></a><span data-ttu-id="5d934-117">2부: Active Directory 준비</span><span class="sxs-lookup"><span data-stu-id="5d934-117">Part 2: Prepare Active Directory</span></span>
<span data-ttu-id="5d934-118">장치 쓰기 저장을 사용 하기 위한 단계 tooprepare 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-118">Use hello following steps tooprepare for using device writeback.</span></span>

1. <span data-ttu-id="5d934-119">Azure AD Connect가 설치 되어 있는 hello 컴퓨터에서 관리자 모드에서 PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-119">From hello machine where Azure AD Connect is installed, launch PowerShell in elevated mode.</span></span>
2. <span data-ttu-id="5d934-120">Hello Active Directory PowerShell 모듈 설치 되지 않은 경우 다음 명령을 hello를 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-120">If hello Active Directory PowerShell module is NOT installed, install it using hello following command:</span></span>
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. <span data-ttu-id="5d934-121">Hello Azure Active Directory PowerShell 모듈 설치 되지 않은 경우 다운로드 하 고 설치 원본 [Azure Active Directory에 대 한 Windows PowerShell 모듈 (64 비트 버전)](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-121">If hello Azure Active Directory PowerShell module is NOT installed, then download and install it from [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span> <span data-ttu-id="5d934-122">이 구성 요소는 hello 로그인 도우미를 Azure AD Connect와 함께 설치 되는 종속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-122">This component has a dependency on hello sign-in assistant, which is installed with Azure AD Connect.</span></span>
4. <span data-ttu-id="5d934-123">엔터프라이즈 관리자 자격 증명으로 hello 다음 명령을 실행 하 고 PowerShell을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-123">With enterprise admin credentials, run hello following commands and then exit PowerShell.</span></span>
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

<span data-ttu-id="5d934-124">엔터프라이즈 관리자 자격 증명 필요 되므로 필요한 변경 내용을 toohello 구성 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-124">Enterprise admin credentials are required since changes toohello configuration namespace are needed.</span></span> <span data-ttu-id="5d934-125">도메인 관리자의 사용 권한으로는 부족합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-125">A domain admin will not have enough permissions.</span></span>

![장치 쓰기 저장 사용을 위한 Powershell](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

<span data-ttu-id="5d934-127">설명:</span><span class="sxs-lookup"><span data-stu-id="5d934-127">Description:</span></span>

* <span data-ttu-id="5d934-128">존재하지 않는 경우 CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn]에서 새 컨테이너 및 개체를 생성하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-128">If they do not exist already, creates and configures new containers and objects under CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span></span>
* <span data-ttu-id="5d934-129">존재하지 않는 경우 CN=RegisteredDevices,[domain-dn]에서 새 컨테이너 및 개체를 생성하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-129">If they do not exist already, creates and configures new containers and objects under CN=RegisteredDevices,[domain-dn].</span></span> <span data-ttu-id="5d934-130">이 컨테이너에서 장치 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-130">Device objects will be created in this container.</span></span>
* <span data-ttu-id="5d934-131">Active Directory의 장치를 toomanage hello Azure AD 커넥터 계정에 필요한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-131">Sets necessary permissions on hello Azure AD Connector account, toomanage devices on your Active Directory.</span></span>
* <span data-ttu-id="5d934-132">여러 포리스트에 Azure AD Connect 설치 하는 경우에 toorun 하나의 포리스트에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-132">Only needs toorun on one forest, even if Azure AD Connect is being installed on multiple forests.</span></span>

<span data-ttu-id="5d934-133">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5d934-133">Parameters:</span></span>

* <span data-ttu-id="5d934-134">DomainName: 장치 개체를 만드는 Active Directory 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-134">DomainName: Active Directory Domain where device objects will be created.</span></span> <span data-ttu-id="5d934-135">참고: 지정된 Active Directory 포리스트에 대한 모든 장치는 단일 도메인에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-135">Note: All devices for a given Active Directory forest will be created in a single domain.</span></span>
* <span data-ttu-id="5d934-136">Hello 디렉터리에 Azure AD Connect toomanage 개체에 의해 사용 될 AdConnectorAccount: Active Directory 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-136">AdConnectorAccount: Active Directory account that will be used by Azure AD Connect toomanage objects in hello directory.</span></span> <span data-ttu-id="5d934-137">Azure AD Connect 동기화 tooconnect tooAD에서 사용 하는 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-137">This is hello account used by Azure AD Connect sync tooconnect tooAD.</span></span> <span data-ttu-id="5d934-138">Express 설정을 사용 하 여를 설치한 경우 MSOL_ 접두사로 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-138">If you installed using express settings, it is hello account prefixed with MSOL_.</span></span>

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a><span data-ttu-id="5d934-139">3부: Azure AD Connect에서 장치 쓰기 저장 사용</span><span class="sxs-lookup"><span data-stu-id="5d934-139">Part 3: Enable device writeback in Azure AD Connect</span></span>
<span data-ttu-id="5d934-140">Azure AD Connect에서 tooenable 장치 쓰기 저장 프로시저를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-140">Use hello following procedure tooenable device writeback in Azure AD Connect.</span></span>

1. <span data-ttu-id="5d934-141">Hello 설치 마법사를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-141">Run hello installation wizard again.</span></span> <span data-ttu-id="5d934-142">선택 **동기화 옵션을 사용자 지정** 페이지 hello 추가 작업에서 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-142">Select **customize synchronization options** from hello Additional Tasks page and click **Next**.</span></span>
   <span data-ttu-id="5d934-143">![사용자 지정 설치 사용자 지정 동기화 옵션](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-143">![Custom Install customize synchronization options](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span></span>
2. <span data-ttu-id="5d934-144">Hello 선택적 기능 페이지에 장치 쓰기 저장은 더 이상 회색입니다. 경우 hello Azure AD Connect 준비 단계 완료 되지 않은 점에 유의 하십시오 hello 선택적 기능 페이지에 장치 쓰기 저장으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-144">In hello Optional Features page, device writeback will no longer be grayed out. Please note that if hello Azure AD Connect prep steps are not completed device writeback will be grayed out in hello Optional features page.</span></span> <span data-ttu-id="5d934-145">장치 쓰기 저장에 대 한 hello 확인란을 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-145">Check hello box for device writeback and click **next**.</span></span> <span data-ttu-id="5d934-146">Hello 확인란은 여전히 사용 하지 않도록 설정 하는 경우 참조 hello [문제 해결 섹션](#the-writeback-checkbox-is-still-disabled)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-146">If hello checkbox is still disabled, see hello [troubleshooting section](#the-writeback-checkbox-is-still-disabled).</span></span>
   <span data-ttu-id="5d934-147">![사용자 지정 설치 장치 쓰기 저장 선택적 기능](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-147">![Custom install Device Writeback optional features](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span></span>
3. <span data-ttu-id="5d934-148">Hello 쓰기 저장 페이지에서 제공 하는 hello 도메인 hello 기본 장치 쓰기 저장 포리스트도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-148">On hello writeback page, you will see hello supplied domain as hello default Device writeback forest.</span></span>
   <span data-ttu-id="5d934-149">![사용자 지정 설치 장치 쓰기 저장 대상 포리스트](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-149">![Custom Install device writeback target forest](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span></span>
4. <span data-ttu-id="5d934-150">추가 구성 변경 없이 마법사 hello hello 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-150">Complete hello installation of hello Wizard with no additional configuration changes.</span></span> <span data-ttu-id="5d934-151">필요한 경우 너무 참조[Azure AD Connect의 사용자 지정 설치 합니다.](active-directory-aadconnect-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="5d934-151">If needed, refer too[Custom installation of Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)</span></span>

## <a name="enable-conditional-access"></a><span data-ttu-id="5d934-152">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="5d934-152">Enable conditional access</span></span>
<span data-ttu-id="5d934-153">이 시나리오에서 사용할 수 있는 자세한 지침 tooenable [Azure Active Directory Device Registration을 사용 하 여 온-프레미스 조건부 액세스 설정](../active-directory-conditional-access-automatic-device-registration-setup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-153">Detailed instructions tooenable this scenario are available within [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

## <a name="verify-devices-are-synchronized-tooactive-directory"></a><span data-ttu-id="5d934-154">장치는 동기화 된 tooActive 디렉터리를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d934-154">Verify Devices are synchronized tooActive Directory</span></span>
<span data-ttu-id="5d934-155">장치 쓰기 저장은 이제 제대로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-155">Device writeback should now be working properly.</span></span> <span data-ttu-id="5d934-156">장치 개체 toobe 쓰기 저장 tooAD too3 시간까지 걸릴 수 있으므로 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-156">Be aware that it can take up too3 hours for device objects toobe written-back tooAD.</span></span>  <span data-ttu-id="5d934-157">장치를 적절 하 게 동기화 되 고 tooverify hello 동기화 규칙을 완료 한 후 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-157">tooverify that your devices are being synced properly, do hello following after hello sync rules complete:</span></span>

1. <span data-ttu-id="5d934-158">Active Directory 관리 센터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-158">Launch Active Directory Administrative Center.</span></span>
2. <span data-ttu-id="5d934-159">Hello 페더레이션된 되 고 도메인 내에서 RegisteredDevices를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-159">Expand RegisteredDevices, within hello Domain that is being federated.</span></span>
   <span data-ttu-id="5d934-160">![Active Directory 관리 센터 등록 장치](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-160">![Active Directory Admin Center Registered Devices](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span></span>
3. <span data-ttu-id="5d934-161">현재 등록된 장치가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-161">Current registered devices will be listed there.</span></span>
   <span data-ttu-id="5d934-162">![Active Directory 관리 센터 등록 장치 목록](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-162">![Active Directory Admin Center Registered Devices List](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d934-163">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5d934-163">Troubleshooting</span></span>
### <a name="hello-writeback-checkbox-is-still-disabled"></a><span data-ttu-id="5d934-164">hello 쓰기 저장 확인란은 여전히 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-164">hello writeback checkbox is still disabled</span></span>
<span data-ttu-id="5d934-165">Hello 확인란 위의 hello 단계를 수행한 경우에 장치 쓰기 저장을 해제에 대 한 hello 하는 경우 다음 단계는 안내해 마법사 hello 상자를 사용 하기 전에 어떤 hello 설치를 통해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-165">If hello checkbox for device writeback is not enabled even though you have followed hello steps above, hello following steps will guide you through what hello installation wizard is verifying before hello box is enabled.</span></span>

<span data-ttu-id="5d934-166">먼저 첫 번째로</span><span class="sxs-lookup"><span data-stu-id="5d934-166">First things first:</span></span>

* <span data-ttu-id="5d934-167">하나 이상의 포리스트에 Windows Server 2012R2가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-167">Make sure at least one forest has Windows Server 2012R2.</span></span> <span data-ttu-id="5d934-168">hello 장치 개체 유형 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-168">hello device object type must be present.</span></span>
* <span data-ttu-id="5d934-169">Hello 설치 마법사가 이미 실행 한 다음 변경 내용을 발견 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-169">If hello installation wizard is already running, then any changes will not be detected.</span></span> <span data-ttu-id="5d934-170">이 경우 hello 설치 마법사를 완료 하 고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-170">In this case, complete hello installation wizard and run it again.</span></span>
* <span data-ttu-id="5d934-171">Hello 초기화 스크립트에서 제공 하는 hello 계정 실제로 hello 올바른 사용자 hello Active Directory Connector에서 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-171">Make sure hello account you provide in hello initialization script is actually hello correct user used by hello Active Directory Connector.</span></span> <span data-ttu-id="5d934-172">tooverify이를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-172">tooverify this, follow these steps:</span></span>
  * <span data-ttu-id="5d934-173">Hello 시작 메뉴에서 열고 **동기화 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-173">From hello start menu, open **Synchronization Service**.</span></span>
  * <span data-ttu-id="5d934-174">열기 hello **커넥터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-174">Open hello **Connectors** tab.</span></span>
  * <span data-ttu-id="5d934-175">Active Directory 도메인 서비스 형식과 hello 커넥터를 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-175">Find hello Connector with type Active Directory Domain Services and select it.</span></span>
  * <span data-ttu-id="5d934-176">**작업** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-176">Under **Actions**, select **Properties**.</span></span>
  * <span data-ttu-id="5d934-177">너무 이동**tooActive Directory 포리스트에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-177">Go too**Connect tooActive Directory Forest**.</span></span> <span data-ttu-id="5d934-178">이 화면 일치 hello ् य ा ख toohello 스크립트에 지정 된 해당 hello 도메인과 사용자 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-178">Verify that hello domain and user name specified on this screen match hello account provided toohello script.</span></span>
    <span data-ttu-id="5d934-179">![동기화 서비스 관리자의 커넥터 계정](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span><span class="sxs-lookup"><span data-stu-id="5d934-179">![Connector account in Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span></span>

<span data-ttu-id="5d934-180">Active Directory의 구성 확인:</span><span class="sxs-lookup"><span data-stu-id="5d934-180">Verify configuration in Active Directory:</span></span>

* <span data-ttu-id="5d934-181">Device Registration Service hello 위치 아래에 있는 해당 hello 확인 (CN DeviceRegistrationService, CN = 장치 등록 서비스, CN = = 장치 등록 구성, CN = Services, CN = Configuration) 구성 명명 컨텍스트 내에서.</span><span class="sxs-lookup"><span data-stu-id="5d934-181">Verify that hello Device Registration Service is located in hello location below (CN=DeviceRegistrationService,CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration) under configuration naming context.</span></span>

![문제 해결, 구성 네임스페이스의 DeviceRegistrationService](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* <span data-ttu-id="5d934-183">Hello 구성 네임 스페이스를 검색 하 여 구성 개체가 하나씩만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-183">Verify there is only one configuration object by searching hello configuration namespace.</span></span> <span data-ttu-id="5d934-184">가 둘 이상의 hello 중복을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-184">If there is more than one, delete hello duplicate.</span></span>

![문제를 해결 하며, hello 중복 개체에 대 한 검색](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* <span data-ttu-id="5d934-186">Hello 장치 등록 서비스 개체에 hello 특성 게스트가 DeviceLocation 있고 값이 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-186">On hello Device Registration Service object, make sure hello attribute msDS-DeviceLocation is present and has a value.</span></span> <span data-ttu-id="5d934-187">조회는 hello objectType 게스트가 DeviceContainer과 함께 사용할이 위치 하 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d934-187">Lookup this location and make sure it is present with hello objectType msDS-DeviceContainer.</span></span>

![문제 해결, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![문제 해결, RegisteredDevices 개체 클래스](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* <span data-ttu-id="5d934-190">Active Directory Connector 필수 사용 권한이 hello 이전 단계에서 발견 하는 hello 등록 된 장치 컨테이너에서 hello 사용 하는 hello 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-190">Verify hello account used by hello Active Directory Connector has required permissions on hello Registered Devices container found by hello previous step.</span></span> <span data-ttu-id="5d934-191">다음은이 컨테이너에서 hello 예상 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-191">This is hello expected permissions on this container:</span></span>

![문제 해결, 컨테이너에 대한 권한 확인](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* <span data-ttu-id="5d934-193">Hello Active Directory 계정에 대 한 권한이 hello CN 확인 = 장치 등록 구성, CN = Services, CN = 구성 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-193">Verify hello Active Directory account has permissions on hello CN=Device Registration Configuration,CN=Services,CN=Configuration object.</span></span>

![문제 해결, 장치 등록 구성에 대한 권한 확인](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a><span data-ttu-id="5d934-195">추가 정보</span><span class="sxs-lookup"><span data-stu-id="5d934-195">Additional Information</span></span>
* [<span data-ttu-id="5d934-196">조건부 액세스를 사용한 위험 관리</span><span class="sxs-lookup"><span data-stu-id="5d934-196">Managing Risk With Conditional Access</span></span>](../active-directory-conditional-access.md)
* [<span data-ttu-id="5d934-197">Azure Active Directory Device Registration을 사용하여 온-프레미스 조건부 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="5d934-197">Setting up On-premises Conditional Access using Azure Active Directory Device Registration</span></span>](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a><span data-ttu-id="5d934-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d934-198">Next steps</span></span>
<span data-ttu-id="5d934-199">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5d934-199">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

