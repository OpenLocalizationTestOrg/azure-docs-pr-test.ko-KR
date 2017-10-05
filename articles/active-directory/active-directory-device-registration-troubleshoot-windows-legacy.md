---
title: "Windows 하위 수준 클라이언트에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결 | Microsoft Docs"
description: "Windows 하위 수준 클라이언트에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결"
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="457fc-103">Windows 하위 수준 클라이언트에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="457fc-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="457fc-104">이 항목은 다음 클라이언트에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="457fc-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="457fc-105">Windows 7</span></span> 
- <span data-ttu-id="457fc-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="457fc-106">Windows 8.1</span></span> 
- <span data-ttu-id="457fc-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="457fc-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="457fc-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="457fc-108">Windows Server 2012</span></span> 
- <span data-ttu-id="457fc-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="457fc-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="457fc-110">Windows 10 또는 Windows Server 2016의 경우 [Windows 10 및 Windows Server 2016에 대한 Azure AD 도메인 조인 컴퓨터의 자동 등록 문제 해결](active-directory-device-registration-troubleshoot-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="457fc-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="457fc-111">이 항목에서는 [Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-device-registration-get-started.md)에 설명된 대로 도메인 조인 장치의 자동 등록을 구성했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="457fc-112">이 항목에서는 잠재적인 문제를 해결하는 방법에 대한 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="457fc-113">성공적인 결과를 얻기 위해 알아두어야 할 사항:</span><span class="sxs-lookup"><span data-stu-id="457fc-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="457fc-114">Azure AD에서 이러한 클라이언트는 사용자/장치 기준으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="457fc-115">예제: jdoe 및 jharnett이 이 장치에 로그인하는 경우 사용자 정보 탭에 해당 사용자에 대해 별도 등록(DeviceID)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="457fc-116">이러한 클라이언트의 등록은 기본적으로 로그온 또는 잠금/잠금 해제 시 시도되도록 구성되어 있으며 작업 스케줄러 작업을 사용하여 5분 지연된 후에 트리거되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="457fc-117">운영 체제의 다시 설치나 수동 등록 취소 및 다시 등록이 수행되면 Azure AD에서 새 등록이 생성될 수 있으며 Azure Portal의 사용자 정보 탭에 여러 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="457fc-118">1단계: 등록 상태 검색</span><span class="sxs-lookup"><span data-stu-id="457fc-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="457fc-119">**장치 등록 상태를 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="457fc-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="457fc-120">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="457fc-121">`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="457fc-122">이 명령을 실행하면 조인 상태에 대한 자세한 세부 정보를 제공하는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="457fc-124">2단계: 등록 상태 평가</span><span class="sxs-lookup"><span data-stu-id="457fc-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="457fc-125">조인이 실패하는 경우 이 대화 상자에는 발생한 문제에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="457fc-126">**가장 일반적인 문제는 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="457fc-126">**The most common issues are:**</span></span>

- <span data-ttu-id="457fc-127">잘못 구성된 AD FS 또는 Azure AD</span><span class="sxs-lookup"><span data-stu-id="457fc-127">A misconfigured AD FS or Azure AD</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="457fc-129">도메인 사용자로 로그온되지 않음</span><span class="sxs-lookup"><span data-stu-id="457fc-129">You are not signed on as a domain user</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="457fc-131">할당량에 도달함</span><span class="sxs-lookup"><span data-stu-id="457fc-131">A quota has been reached</span></span>

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="457fc-133">서비스가 응답하지 않음</span><span class="sxs-lookup"><span data-stu-id="457fc-133">The service is not responding</span></span> 

    ![Windows에 대한 작업 공간 연결](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="457fc-135">**Applications and Services Log\Microsoft-Workplace Join**의 이벤트 로그에서 상태 정보를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="457fc-136">**실패한 등록에 대한 가장 일반적인 원인은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="457fc-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="457fc-137">컴퓨터가 조직의 내부 네트워크에 있지 않거나 온-프레미스 AD 도메인 컨트롤러에 연결되지 않은 VPN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="457fc-138">로컬 컴퓨터 계정으로 컴퓨터에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="457fc-139">서비스 구성 문제:</span><span class="sxs-lookup"><span data-stu-id="457fc-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="457fc-140">페더레이션 서버가 **WIAORMULTIAUTHN**을 지원하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="457fc-141">컴퓨터가 속한 AD 포리스트의 Azure AD에서 확인된 도메인 이름을 가리키는 서비스 연결 지점 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="457fc-142">장치 제한에 도달했습니다.</span><span class="sxs-lookup"><span data-stu-id="457fc-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="457fc-143">Azure Active Directory 장치 등록 시작을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="457fc-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="457fc-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="457fc-144">Next steps</span></span>

<span data-ttu-id="457fc-145">자세한 내용은 [자동 장치 등록 FAQ](active-directory-device-registration-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="457fc-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
