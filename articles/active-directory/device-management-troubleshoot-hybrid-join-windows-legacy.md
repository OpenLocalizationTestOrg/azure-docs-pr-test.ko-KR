---
title: "aaaTroubleshooting 하이브리드 Azure Active Directory 가입 하위 수준 장치 | Microsoft Docs"
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
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="deac6-103">하위 수준 장치에 조인된 하이브리드 Azure Active Directory 문제 해결</span><span class="sxs-lookup"><span data-stu-id="deac6-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="deac6-104">이 항목은 적용 가능한 유일한 toohello 다음 장치:</span><span class="sxs-lookup"><span data-stu-id="deac6-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="deac6-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="deac6-105">Windows 7</span></span> 
- <span data-ttu-id="deac6-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="deac6-106">Windows 8.1</span></span> 
- <span data-ttu-id="deac6-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="deac6-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="deac6-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="deac6-108">Windows Server 2012</span></span> 
- <span data-ttu-id="deac6-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="deac6-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="deac6-110">Windows 10 또는 Windows Server 2016의 경우 [Windows 10 및 Windows Server 2016 장치에 조인된 하이브리드 Azure Active Directory 문제 해결](device-management-troubleshoot-hybrid-join-windows-current.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="deac6-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="deac6-111">이 항목에서는 있다고 가정 [구성 된 하이브리드 Azure Active Directory 가입 장치](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello 다음 시나리오:</span><span class="sxs-lookup"><span data-stu-id="deac6-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="deac6-112">장치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="deac6-112">Device-based conditional access</span></span>

- [<span data-ttu-id="deac6-113">엔터프라이즈 설정 로밍</span><span class="sxs-lookup"><span data-stu-id="deac6-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="deac6-114">비즈니스용 Windows Hello</span><span class="sxs-lookup"><span data-stu-id="deac6-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="deac6-115">이 항목에서는 문제 해결 방법을 tooresolve 잠재적 문제에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="deac6-116">**알아야 할 사항:**</span><span class="sxs-lookup"><span data-stu-id="deac6-116">**What you should know:**</span></span> 

- <span data-ttu-id="deac6-117">사용자 당 장치의 hello 최대 수는 장치 중심입니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="deac6-118">예를 들어 경우 *jdoe* 및 *jharnett* 로그인 tooa 장치 별도 등록 (DeviceID) hello에서 각각의 대해 만들어집니다 **사용자** 정보 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="deac6-119">초기 등록 hello / 참가 장치 시도 하는 구성 된 tooperform 로그온 또는 잠금 / 잠금 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="deac6-120">작업 스케줄러 작업에 의해 트리거되는 5분 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="deac6-121">Hello 운영 체제 또는 수동 다시 설치 여러 항목의 hello 사용자 정보 탭 아래에 결과 hello Azure 포털 및 등록 취소 하 고 다시 등록 Azure AD에 새 등록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="deac6-122">1 단계: hello 등록 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="deac6-123">**tooverify hello 등록 상태:**</span><span class="sxs-lookup"><span data-stu-id="deac6-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="deac6-124">관리자 권한으로 명령 프롬프트를 열고 hello</span><span class="sxs-lookup"><span data-stu-id="deac6-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="deac6-125">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="deac6-126">이 명령은 hello 조인 상태에 대 한 자세한 정보를 제공 하는 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="deac6-128">2 단계: hello 하이브리드 Azure AD 조인 상태를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="deac6-129">Hello 하이브리드 Azure AD 조인 성공 하지 못한 경우 hello 대화 상자에는 발생 한 hello 문제에 대 한 세부 정보와 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="deac6-130">**hello 가장 일반적인 사항은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="deac6-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="deac6-131">잘못 구성된 AD FS 또는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="deac6-131">A misconfigured AD FS or Azure AD</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="deac6-133">도메인 사용자로 로그온되지 않음</span><span class="sxs-lookup"><span data-stu-id="deac6-133">You are not signed on as a domain user</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="deac6-135">할당량에 도달함</span><span class="sxs-lookup"><span data-stu-id="deac6-135">A quota has been reached</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="deac6-137">hello 서비스가 응답 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-137">hello service is not responding</span></span> 

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="deac6-139">Hello 이벤트 로그에 hello 상태 정보를 찾을 수도 **응용 프로그램 및 서비스 Log\Microsoft 작업 공간 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="deac6-140">**실패 한 하이브리드 Azure AD 조인에 대 한 hello 가장 일반적인 원인은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="deac6-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="deac6-141">컴퓨터가 켜져 hello 조직의 내부 네트워크 또는 VPN 연결 tooan 없이 온-프레미스 AD 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="deac6-142">로컬 컴퓨터 계정 사용 하 여 tooyour 컴퓨터에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="deac6-143">서비스 구성 문제:</span><span class="sxs-lookup"><span data-stu-id="deac6-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="deac6-144">hello 페더레이션 서버가 있는 상태 구성된 toosupport **WIAORMULTIAUTHN**합니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="deac6-145">Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="deac6-146">사용자 장치 hello 제한에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="deac6-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="deac6-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="deac6-147">Next steps</span></span>

<span data-ttu-id="deac6-148">질문에 대 한 참조 hello [장치 관리 FAQ](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="deac6-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
