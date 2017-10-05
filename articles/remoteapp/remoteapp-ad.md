---
title: "Azure AD + Azure RemoteApp에 대한 Active Directory 요구 사항 | Microsoft Docs"
description: "Azure RemoteApp과 작동하도록 Active Directory를 설정하는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="f6544-103">Azure AD + Azure RemoteApp에 대한 Active Directory 요구 사항</span><span class="sxs-lookup"><span data-stu-id="f6544-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f6544-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f6544-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f6544-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f6544-106">Azure RemoteApp 하이브리드 컬렉션 또는 AD Connect를 사용하여 페더레이션하려는 클라우드 컬렉션의 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="f6544-107">Azure AD 및 Active Directory 연결</span><span class="sxs-lookup"><span data-stu-id="f6544-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="f6544-108">Azure AD 테넌트와 온-프레미스 Active Directory 환경을 연결하려면 AD Connect를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="f6544-109">[4번 클릭](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) 만으로 두 개의 디렉터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="f6544-110">참고 - 하이브리드 컬렉션에는 디렉터리 동기화가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="f6544-111">“@domain.com”이 일치하는지 확인</span><span class="sxs-lookup"><span data-stu-id="f6544-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="f6544-112">시작하기 전에 온-프레미스 포리스트에 대한 UPN이 Azure AD 도메인의 접미사와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="f6544-113">Azure AD에서 UPN 도메인 접미사를 설정한 후에는 Azure RemoteApp에 로그인하는 모든 사용자가 “user@<the suffix you set up>”로 로그인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="f6544-114">또한 사용자가 동일한 user@suffix 를 사용하여 온-프레미스 도메인에 로그인할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="f6544-115">특정한 경우에는 온-프레미스 사용자를 위해 다른 도메인 접미사를 지정하는 동안 Azure AD에 하나의 도메인 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="f6544-116">이런 경우 사용자는 Azure RemoteApp을 통해 도메인에 가입된 컴퓨터나 리소스에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="f6544-117">예를 들어 AAD에서 UPN 도메인 접미사를 contoso.com으로 설정했지만 일부 온-프레미스/AD 사용자를 @contoso.uk로 로그인하도록 구성한 경우 해당 사용자는 ARA 컬렉션에 제대로 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="f6544-118">로그인을 가능하게 하려면 AAD와 AD의 사용자 UPN이 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="f6544-119">Azure RemoteApp에 대한 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="f6544-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="f6544-120">다음과 같은 온-프레미스 Active Directory 개체도 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="f6544-121">RDSH 끝점을 온-프레미스 도메인에 연결하여 RemoteApp 프로그램에 도메인 리소스에 대한 액세스 권한을 제공할 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="f6544-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="f6544-122">RemoteApp 컴퓨터 개체를 포함할 OU(조직 구성 단위).</span><span class="sxs-lookup"><span data-stu-id="f6544-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="f6544-123">필수는 아니지만 OU를 통해 RemoteApp에 사용할 계정과 정책을 격리시키는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="f6544-124">RemoteApp 컬렉션을 만들 때 이러한 두 개체가 필요하므로 이 단계를 먼저 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6544-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

