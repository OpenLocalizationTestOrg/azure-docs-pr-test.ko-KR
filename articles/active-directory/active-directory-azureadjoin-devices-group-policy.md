---
title: "Windows 10 용 aaaConnect 도메인에 가입 된 장치 tooAzure AD 환경을 | Microsoft Docs"
description: "관리자가 그룹 정책 tooenable 장치 toobe toohello 도메인에 가입 된 엔터프라이즈 네트워크를 구성할 수는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="8f428-103">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="8f428-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="8f428-104">도메인 가입 hello 전통적인 방법 조직 마지막 15 년 등 hello에 대 한 작업에 대 한 장치 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="8f428-105">Windows Server Active Directory (Active Directory) 작업을 사용 하 여 사용자가 toosign tootheir 장치에서 활성화 있는 또는 학교 계정 및 허용 된 IT toofully 이러한 장치를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="8f428-106">조직은 일반적으로 tooprovision 장치 toousers 메서드가 imaging에 의존 하 고 일반적으로 toomanage SCCM System Center Configuration Manager () 또는 그룹 정책을 사용 하 여 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="8f428-107">도메인 가입 Windows 10의 이점 장치 tooAzure Active Directory (Azure AD)에 연결한 후에 수행 하는 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="8f428-108">Single sign on (SSO) tooAzure AD 리소스 어디에서 든</span><span class="sxs-lookup"><span data-stu-id="8f428-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="8f428-109">작업을 사용 하 여 toohello enterprise Windows 스토어에 액세스 하거나 학교 계정 (Microsoft 계정이 필요)</span><span class="sxs-lookup"><span data-stu-id="8f428-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="8f428-110">회사 또는 학교 계정을 사용하여 장치 간 사용자 설정의 엔터프라이즈 규격 로밍(Microsoft 계정 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="8f428-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="8f428-111">비즈니스용 Windows Hello 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 인증 및 손쉬운 로그인</span><span class="sxs-lookup"><span data-stu-id="8f428-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="8f428-112">기능 toorestrict 조직 장치 그룹 정책 설정을 준수 하는 toodevices만 액세스</span><span class="sxs-lookup"><span data-stu-id="8f428-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f428-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8f428-113">Prerequisites</span></span>
<span data-ttu-id="8f428-114">도메인 가입 계속 toobe 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="8f428-115">그러나 tooget hello Azure AD 혜택 sso를 사용 하 여 설정의 로밍 직장 또는 학교 계정을, 및 tooWindows 저장소 작업을 사용 하 여 액세스할 이나 학교 계정을, hello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="8f428-116">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="8f428-116">Azure AD subscription</span></span>
* <span data-ttu-id="8f428-117">Azure AD Connect tooextend hello 온-프레미스 디렉터리 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="8f428-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="8f428-118">도메인에 가입 된 장치 tooAzure tooconnect AD 설정 정책</span><span class="sxs-lookup"><span data-stu-id="8f428-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="8f428-119">장치에 Windows 10 빌드(빌드 10551 또는 이후 버전)</span><span class="sxs-lookup"><span data-stu-id="8f428-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="8f428-120">비즈니스 사용자와 Windows Hello Windows Hello tooenable 코드도 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="8f428-121">사용자 인증서를 발급하기 위한 **PKI(공개 키 인프라)**가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="8f428-122">**System Center Configuration Manager 현재 분기** -1606 이상 더 좋은 tooinstall 버전이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="8f428-123">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f428-123">For more information, see:</span></span> 
    - [<span data-ttu-id="8f428-124">System Center Configuration Manager용 설명서</span><span class="sxs-lookup"><span data-stu-id="8f428-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="8f428-125">System Center Configuration Manager 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="8f428-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="8f428-126">System Center Configuration Manager의 비즈니스용 Windows Hello 설정</span><span class="sxs-lookup"><span data-stu-id="8f428-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="8f428-127">대체 toohello PKI 배포 요구 사항으로 할 수 있는 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="8f428-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="8f428-128">Windows Server 2016 Active Directory 도메인 서비스와 몇 가지 도메인 컨트롤러를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="8f428-129">조건부 액세스는 tooenable 없는 추가 배포와 toodomain에 가입 된 장치 액세스를 허용 하는 그룹 정책 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="8f428-130">hello 장치의 준수를 기반으로 toomanage 액세스 제어를 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="8f428-131">비즈니스용 Windows Hello 시나리오에 대한 System Center Configuration Manager 현재 분기(1606 이상)</span><span class="sxs-lookup"><span data-stu-id="8f428-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="8f428-132">배포 지침</span><span class="sxs-lookup"><span data-stu-id="8f428-132">Deployment instructions</span></span>

<span data-ttu-id="8f428-133">toodeploy에 나열 된 hello 단계를 수행 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="8f428-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="8f428-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f428-134">Next step</span></span>
* [<span data-ttu-id="8f428-135">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="8f428-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="8f428-136">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f428-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="8f428-137">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="8f428-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="8f428-138">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="8f428-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="8f428-139">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="8f428-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

