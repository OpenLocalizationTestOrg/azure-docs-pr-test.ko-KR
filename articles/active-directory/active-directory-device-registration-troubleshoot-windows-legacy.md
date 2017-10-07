---
title: "aaaTroubleshooting hello 자동 등록 Azure AD 도메인의 Windows 하위 클라이언트에 대 한 컴퓨터를 가입 | Microsoft Docs"
description: "Windows 하위 클라이언트에 대 한 연결 컴퓨터를 Azure AD 도메인의 hello 자동 등록 문제를 해결 합니다."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="d9523-103">Windows 하위 클라이언트에 대 한 컴퓨터 tooAzure AD 가입 된 도메인의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d9523-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="d9523-104">이 항목은 클라이언트에 따라 적용 가능한 유일한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="d9523-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d9523-105">Windows 7</span></span> 
- <span data-ttu-id="d9523-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d9523-106">Windows 8.1</span></span> 
- <span data-ttu-id="d9523-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d9523-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="d9523-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d9523-108">Windows Server 2012</span></span> 
- <span data-ttu-id="d9523-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d9523-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="d9523-110">Windows 10 또는 Windows Server 2016에 대 한 참조 [컴퓨터 tooAzure AD – Windows 10 및 Windows Server 2016에 가입 된 도메인의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="d9523-111">이 항목에서는 구성 자동 등록의 도메인에 가입 된 장치에서 설명한 대로 설명 된 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-device-registration-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="d9523-112">이 항목에서는 문제 해결 방법을 tooresolve 잠재적 문제에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="d9523-113">성공적인 결과 대 한 일부의 toonote:</span><span class="sxs-lookup"><span data-stu-id="d9523-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="d9523-114">Azure AD에서 이러한 클라이언트는 사용자/장치 기준으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="d9523-115">예를 들어: jdoe 및 jharnett toothis 장치 로그인을 별도 등록 (DeviceID) hello 사용자 정보 탭에서 해당 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="d9523-116">이러한 클라이언트 hello 초기 등록 로그온 또는 잠금/잠금해제에 구성 된 tootry 이며는이 트리거될 작업 스케줄러 작업을 사용 하 여 5 분 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="d9523-117">Hello 운영 체제 또는 수동 등록 취소 및 다시 등록의 다시 설치 하 고 Azure AD에 새 등록을 만들 수 있습니다 Azure 포털 여러 항목 hello의 hello 사용자 정보 탭 아래에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="d9523-118">1 단계: hello 등록 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="d9523-119">**tooverify hello 등록 상태:**</span><span class="sxs-lookup"><span data-stu-id="d9523-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="d9523-120">관리자 권한으로 명령 프롬프트를 열고 hello</span><span class="sxs-lookup"><span data-stu-id="d9523-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="d9523-121">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="d9523-122">이 명령은 hello 조인 상태에 대 한 자세한 정보를 제공 하는 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="d9523-124">2 단계: hello 등록 상태를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="d9523-125">Hello 조인 성공 하지 못한 경우 hello 대화 상자에는 발생 한 hello 문제에 대 한 세부 정보와 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="d9523-126">**hello 가장 일반적인 사항은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="d9523-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="d9523-127">잘못 구성된 AD FS 또는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9523-127">A misconfigured AD FS or Azure AD</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="d9523-129">도메인 사용자로 로그온되지 않음</span><span class="sxs-lookup"><span data-stu-id="d9523-129">You are not signed on as a domain user</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="d9523-131">할당량에 도달함</span><span class="sxs-lookup"><span data-stu-id="d9523-131">A quota has been reached</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="d9523-133">hello 서비스가 응답 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-133">hello service is not responding</span></span> 

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="d9523-135">Hello 이벤트 로그에 hello 상태 정보를 찾을 수도 **응용 프로그램 및 서비스 Log\Microsoft 작업 공간 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="d9523-136">**실패 한 등록에 대 한 hello 가장 일반적인 원인은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="d9523-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="d9523-137">컴퓨터가 켜져 hello 조직의 내부 네트워크 또는 VPN 연결 tooan 없이 온-프레미스 AD 도메인 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="d9523-138">로컬 컴퓨터 계정 사용 하 여 tooyour 컴퓨터에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="d9523-139">서비스 구성 문제:</span><span class="sxs-lookup"><span data-stu-id="d9523-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="d9523-140">hello 페더레이션 서버가 있는 상태 구성된 toosupport **WIAORMULTIAUTHN**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="d9523-141">Azure AD에서 hello 컴퓨터 속한 hello AD 포리스트에 tooyour 확인 된 도메인 이름을 가리키는 서비스 연결 지점 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="d9523-142">사용자 장치 hello 제한에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d9523-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="d9523-143">Azure Active Directory 장치 등록 시작을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9523-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9523-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9523-144">Next steps</span></span>

<span data-ttu-id="d9523-145">자세한 내용은 참조 hello [자동 장치 등록 FAQ](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d9523-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
