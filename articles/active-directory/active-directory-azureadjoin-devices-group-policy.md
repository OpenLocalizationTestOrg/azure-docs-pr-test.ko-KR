---
title: "Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결 | Microsoft Docs"
description: "관리자가 기업 네트워크에 도메인이 가입되도록 장치를 활성화하는 그룹 정책을 구성할 수 있는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="2c83b-103">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="2c83b-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="2c83b-104">도메인 가입은 조직에서 15년이 넘도록 작업하기 위해 장치를 연결해 온 일반적인 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="2c83b-105">사용자가 Windows Server Active Directory(Active Directory) 회사 또는 학교 계정을 사용하여 장치에 로그인할 수 있도록 설정했으며 IT에서 이러한 장치를 완전히 관리할 수 있도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="2c83b-106">조직에서는 일반적으로 사용자에 게 장치를 프로비전하는 이미징 메서드에 의존하고 이를 관리하는 데 System Center 구성 관리자(SCCM) 또는 그룹 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="2c83b-107">Windows 10에서 도메인 가입을 사용하면 장치를 Azure AD(Azure Active Directory)에 연결했을 때 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="2c83b-108">어디에서나 Azure AD 리소스에 SSO(single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="2c83b-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="2c83b-109">회사 또는 학교 계정을 사용하여 엔터프라이즈 Windows 스토어에 액세스(Microsoft 계정 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="2c83b-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="2c83b-110">회사 또는 학교 계정을 사용하여 장치 간 사용자 설정의 엔터프라이즈 규격 로밍(Microsoft 계정 필요 없음)</span><span class="sxs-lookup"><span data-stu-id="2c83b-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="2c83b-111">비즈니스용 Windows Hello 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 인증 및 손쉬운 로그인</span><span class="sxs-lookup"><span data-stu-id="2c83b-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="2c83b-112">조직 장치의 그룹 정책 설정을 준수하는 장치 액세스 할 수 있도록 제한하는 기능</span><span class="sxs-lookup"><span data-stu-id="2c83b-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c83b-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2c83b-113">Prerequisites</span></span>
<span data-ttu-id="2c83b-114">도메인 가입이 계속 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-114">Domain join continues to be useful.</span></span> <span data-ttu-id="2c83b-115">그러나 SSO에 대한 Azure AD 혜택을 얻고 회사 또는 학교 계정으로 설정을 로밍하고 회사 또는 학교 계정으로 Windows 스토어에 액세스하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="2c83b-116">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2c83b-116">Azure AD subscription</span></span>
* <span data-ttu-id="2c83b-117">Azure AD에 온-프레미스 디렉터리를 확장하는 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2c83b-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="2c83b-118">Azure AD에 도메인 가입 장치를 연결하도록 설정한 정책</span><span class="sxs-lookup"><span data-stu-id="2c83b-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="2c83b-119">장치에 Windows 10 빌드(빌드 10551 또는 이후 버전)</span><span class="sxs-lookup"><span data-stu-id="2c83b-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="2c83b-120">또한 비즈니스용 Windows Hello 및 Windows Hello를 사용하도록 하려면 다음과 같은 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="2c83b-121">사용자 인증서를 발급하기 위한 **PKI(공개 키 인프라)**가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="2c83b-122">**System Center Configuration Manager 현재 분기** - 1606 이상 버전을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="2c83b-123">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c83b-123">For more information, see:</span></span> 
    - [<span data-ttu-id="2c83b-124">System Center Configuration Manager용 설명서</span><span class="sxs-lookup"><span data-stu-id="2c83b-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="2c83b-125">System Center Configuration Manager 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="2c83b-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="2c83b-126">System Center Configuration Manager의 비즈니스용 Windows Hello 설정</span><span class="sxs-lookup"><span data-stu-id="2c83b-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="2c83b-127">PKI 배포 요구 사항에 대한 대안으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="2c83b-128">Windows Server 2016 Active Directory 도메인 서비스와 몇 가지 도메인 컨트롤러를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="2c83b-129">조건부 액세스를 활성화하려면 추가 배포 없이 ‘도메인 가입된’ 장치에 대한 액세스를 허용하는 그룹 정책 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="2c83b-130">장치의 규정 준수에 따른 액세스 제어를 관리하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c83b-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="2c83b-131">비즈니스용 Windows Hello 시나리오에 대한 System Center Configuration Manager 현재 분기(1606 이상)</span><span class="sxs-lookup"><span data-stu-id="2c83b-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="2c83b-132">배포 지침</span><span class="sxs-lookup"><span data-stu-id="2c83b-132">Deployment instructions</span></span>

<span data-ttu-id="2c83b-133">배포하려면 [Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-conditional-access-automatic-device-registration-setup.md)에 나와 있는 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2c83b-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="2c83b-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c83b-134">Next step</span></span>
* [<span data-ttu-id="2c83b-135">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c83b-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="2c83b-136">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="2c83b-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2c83b-137">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="2c83b-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="2c83b-138">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="2c83b-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="2c83b-139">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="2c83b-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

