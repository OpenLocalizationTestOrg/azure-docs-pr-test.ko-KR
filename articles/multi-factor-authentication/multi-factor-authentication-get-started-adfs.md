---
title: "2단계 검증 및 AD FS - Azure MFA | Microsoft Docs"
description: "Azure MFA 및 AD FS 시작 방법을 설명하는 Azure Multi-Factor Authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="3ef54-103">Azure Multi-Factor Authentication 및 Active Directory Federation Services 시작</span><span class="sxs-lookup"><span data-stu-id="3ef54-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="3ef54-104"><center>![클라우드](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="3ef54-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="3ef54-105">조직에서 AD FS를 사용하여 온-프레미스 Active Directory를 Azure Active Directory에 페더레이션한 경우 Azure Multi-Factor Authentication 사용을 위한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="3ef54-106">Azure Multi-Factor Authentication 또는 Active Directory Federation Services를 사용하여 클라우드 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="3ef54-107">Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="3ef54-108">다음 표에서는 리소스 보안 유지를 위해 Azure Multi-Factor Authentication을 사용하는 경우와 AD FS를 사용하는 경우의 확인 환경을 요약해서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="3ef54-109">확인 환경 - 브라우저 기반 앱</span><span class="sxs-lookup"><span data-stu-id="3ef54-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="3ef54-110">확인 환경 - 비 브라우저 기반 앱</span><span class="sxs-lookup"><span data-stu-id="3ef54-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ef54-111">Azure Multi-Factor Authentication을 사용하여 Azure AD 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="3ef54-112">첫 번째 확인 단계는 AD FS를 사용하여 온-프레미스에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="3ef54-113">두 번째 단계는 클라우드 인증을 사용하여 수행되는 휴대폰 기반 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="3ef54-114">Active Directory Federation Services를 사용하여 Azure AD 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="3ef54-115">첫 번째 확인 단계는 AD FS를 사용하여 온-프레미스에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="3ef54-116">두 번째 단계는 클레임을 적용하여 온-프레미스에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="3ef54-117">페더레이션된 사용자의 앱 암호 관련 주의 사항:</span><span class="sxs-lookup"><span data-stu-id="3ef54-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="3ef54-118">앱 암호는 클라우드 인증을 사용하여 확인되므로 페더레이션을 바이패스합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="3ef54-119">앱 암호를 설정할 때 페더레이션이 능동적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="3ef54-120">앱 암호를 사용할 경우 온-프레미스 클라이언트 액세스 제어 설정은 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="3ef54-121">앱 암호에 대한 온-프레미스 인증 로깅 기능이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="3ef54-122">계정 사용 안 함/삭제 설정은 디렉터리 동기화 동안 최대 3시간이 걸리며 클라우드 ID에서 앱 암호의 사용 안 함/삭제가 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef54-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ef54-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ef54-123">Next steps</span></span>
<span data-ttu-id="3ef54-124">Azure Multi-Factor Authentication 또는 AD FS를 통한 Azure Multi-factor Authentication 서버 설정 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ef54-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="3ef54-125">Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="3ef54-126">Windows Server 2012 R2 AD FS와 Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="3ef54-127">AD FS 2.0과 함께 Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="3ef54-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
