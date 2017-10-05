---
title: "하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결 | Microsoft Docs"
description: "하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결"
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 715fca79e488ae3759926181c244a42026f4a554
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="5c241-103">하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c241-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="5c241-104">이 항목은 다음 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-104">This topic is applicable only to the following devices:</span></span> 

- <span data-ttu-id="5c241-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="5c241-105">Windows 7</span></span> 
- <span data-ttu-id="5c241-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5c241-106">Windows 8.1</span></span> 
- <span data-ttu-id="5c241-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="5c241-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="5c241-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5c241-108">Windows Server 2012</span></span> 
- <span data-ttu-id="5c241-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5c241-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="5c241-110">Windows 10 또는 Windows Server 2016의 경우 [Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-current.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c241-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="5c241-111">이 항목에서는 다음 시나리오를 지원하도록 [장치에 조인된 하이브리드 Azure Active Directory를 구성](device-management-hybrid-azuread-joined-devices-setup.md)했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="5c241-112">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="5c241-112">Device-based conditional access</span></span>

- [<span data-ttu-id="5c241-113">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="5c241-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="5c241-114">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="5c241-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="5c241-115">이 항목에서는 잠재적인 문제를 해결하는 방법에 대한 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-115">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  

<span data-ttu-id="5c241-116">**알아야 할 사항:**</span><span class="sxs-lookup"><span data-stu-id="5c241-116">**What you should know:**</span></span> 

- <span data-ttu-id="5c241-117">사용자당 최대 장치 수는 장치 중심입니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-117">The maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="5c241-118">예를 들어 *jdoe* 및 *jharnett*가 장치에 로그인하는 경우 **사용자** 정보 탭에 각각에 대해 별도 등록(DeviceID)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span></span>  

- <span data-ttu-id="5c241-119">초기 등록 / 장치 조인은 로그온 또는 잠금 / 잠금 해제 시 시도를 수행하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-119">The initial registration / join of devices is configured to perform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="5c241-120">작업 스케줄러 작업에 의해 트리거되는 5분 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="5c241-121">운영 체제의 다시 설치나 수동 등록 취소 및 다시 등록이 수행되면 Azure AD에서 새 등록이 생성될 수 있으며 Azure Portal의 사용자 정보 탭에 여러 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-121">A reinstall of the operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="5c241-122">1단계: 등록 상태 검색</span><span class="sxs-lookup"><span data-stu-id="5c241-122">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="5c241-123">**장치 등록 상태를 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="5c241-123">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="5c241-124">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-124">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="5c241-125">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="5c241-126">이 명령을 실행하면 조인 상태에 대한 자세한 세부 정보를 제공하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-126">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a><span data-ttu-id="5c241-128">2단계: 하이브리드 Azure AD 조인 상태 평가</span><span class="sxs-lookup"><span data-stu-id="5c241-128">Step 2: Evaluate the hybrid Azure AD join status</span></span> 

<span data-ttu-id="5c241-129">하이브리드 Azure AD 조인이 실패하는 경우 이 대화 상자에는 발생한 문제에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-129">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span></span>

<span data-ttu-id="5c241-130">**가장 일반적인 문제는 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="5c241-130">**The most common issues are:**</span></span>

- <span data-ttu-id="5c241-131">잘못 구성된 AD FS 또는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c241-131">A misconfigured AD FS or Azure AD</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="5c241-133">도메인 사용자로 로그온되지 않음</span><span class="sxs-lookup"><span data-stu-id="5c241-133">You are not signed on as a domain user</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="5c241-135">할당량에 도달함</span><span class="sxs-lookup"><span data-stu-id="5c241-135">A quota has been reached</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="5c241-137">서비스가 응답하지 않음</span><span class="sxs-lookup"><span data-stu-id="5c241-137">The service is not responding</span></span> 

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="5c241-139">**Applications and Services Log\Microsoft-Workplace Join**의 이벤트 로그에서 상태 정보를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-139">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="5c241-140">**실패한 하이브리드 Azure AD 조인에 대한 가장 일반적인 원인은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="5c241-140">**The most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="5c241-141">컴퓨터가 조직의 내부 네트워크에 있지 않거나 온-프레미스 AD 도메인 컨트롤러에 연결되지 않은 VPN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-141">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="5c241-142">로컬 컴퓨터 계정으로 컴퓨터에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-142">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="5c241-143">서비스 구성 문제:</span><span class="sxs-lookup"><span data-stu-id="5c241-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="5c241-144">페더레이션 서버가 **WIAORMULTIAUTHN**을 지원하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-144">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="5c241-145">컴퓨터가 속한 AD 포리스트의 Azure AD에서 확인된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-145">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="5c241-146">장치 제한에 도달했습니다.</span><span class="sxs-lookup"><span data-stu-id="5c241-146">A user has reached the limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c241-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c241-147">Next steps</span></span>

<span data-ttu-id="5c241-148">질문은 [장치 관리 FAQ](device-management-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c241-148">For questions, see the [device management FAQ](device-management-faq.md)</span></span>  
