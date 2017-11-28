---
title: "AD aaaAzure + Azure RemoteApp에 대 한 Active Directory 요구 사항 | Microsoft Docs"
description: "자세한 방법을 tooset Azure RemoteApp과 함께 toowork Active Directory를 구성 합니다."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="9d138-103">Azure AD + Azure RemoteApp에 대한 Active Directory 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9d138-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9d138-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9d138-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9d138-106">Azure RemoteApp 하이브리드 컬렉션 또는 toofederate AD Connect를 사용 하 여 원하는 클라우드 컬렉션 toodo hello 다음을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="9d138-107">Azure AD 및 Active Directory 연결</span><span class="sxs-lookup"><span data-stu-id="9d138-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="9d138-108">Azure AD 테 넌 트를 온-프레미스 Active Directory 환경 tooconnect를 하려는 경우 AD Connect를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="9d138-109">이동할 수만 [4 번의 클릭](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello 두 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="9d138-110">참고 - 하이브리드 컬렉션에는 디렉터리 동기화가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="9d138-111">“@domain.com”이 일치하는지 확인</span><span class="sxs-lookup"><span data-stu-id="9d138-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="9d138-112">시작 하기 전에 해야 Azure AD 도메인에 온-프레미스 포리스트 일치 hello 접미사에 대 한 해당 hello UPN 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="9d138-113">Azure RemoteApp에 로그인 하는 모든 사용자로 로그인은 Azure AD에서 hello UPN 도메인 접미사를 설정한 후 "@ 사용자<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="9d138-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="9d138-114">사용자가 로그인 수 있는지도 hello를 사용 하 여 동일한 있는지 확인 user@suffix hello 온-프레미스 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="9d138-115">일부 경우에 설정할 수 있습니다 한 도메인 이름-에 hello 사용자에 대 한 다른 도메인 접미사를 지정 하는 동안 Azure AD에서</span><span class="sxs-lookup"><span data-stu-id="9d138-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="9d138-116">이 경우 사용자가 수 tooconnect tooany 도메인에 가입 된 컴퓨터 또는 Azure RemoteApp을 통해 리소스 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="9d138-117">예를 들어 contoso.com으로 AAD에서 사용자 UPN 도메인 접미사를 설정 했지만 프레미스/AD에서 일부 사용자가 사용 하 여 구성 된 toolog @contoso.uk, 해당 사용자는 hello ARA 컬렉션에 로그인 할 수 toocorrectly 경우가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="9d138-118">AAD와 AD에서 UPN 해야 하는 사용자가 로그인 toobe 가능한 hello에 대 한 동일 hello "</span><span class="sxs-lookup"><span data-stu-id="9d138-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="9d138-119">Azure RemoteApp에 대한 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="9d138-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="9d138-120">다음 온-프레미스 Active Directory 개체 toocreate hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="9d138-121">서비스 계정 tooprovide toodomain 리소스에 액세스 RDSH 끝점 toohello 온-프레미스 도메인에 가입 하 여 RemoteApp 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="9d138-122">조직 구성 단위 (OU) toocontain RemoteApp 컴퓨터 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="9d138-123">권장 (않음 필요 하지 않음) tooisolate hello 계정과 RemoteApp에 사용할 정책을 하는 OU hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="9d138-124">RemoteApp 컬렉션을 만들 때 필요한 두이 개체 모두 수 있으므로 있는지 toodo 이러한 단계 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d138-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

