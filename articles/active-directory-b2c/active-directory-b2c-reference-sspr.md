---
title: "Azure Active Directory B2C: 셀프 서비스 암호 재설정 | Microsoft Docs"
description: "Azure Active Directory B2C에 소비자에 대 한 tooset 셀프 서비스 암호를 다시 설정 하는 방법을 보여 주는 항목"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="3d78a-103">Azure Active Directory B2C: 소비자를 위해 셀프 서비스 암호 재설정 설정</span><span class="sxs-lookup"><span data-stu-id="3d78a-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="3d78a-104">Hello로 셀프 서비스 암호 재설정 기능, 소비자 (로컬 계정에 등록 한)가 자체적으로 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="3d78a-105">특히 응용 프로그램에 수백만 정기적으로 사용 하는 소비자의 경우 지원 담당자의 부담을 hello 상당히 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="3d78a-106">현재 검증된 전자 메일 주소를 지원 복구 방법으로 사용하여 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="3d78a-107">추가 복구 방법 (예: 확인 된 전화 번호, 보안 질문, 등) hello 미래에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="3d78a-108">이 문서 적용 tooself 서비스 암호 재설정 로그인 정책 hello 축을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="3d78a-109">완전히 사용자 지정 가능한 암호 재설정 정책이 앱에서 호출되어야 하는 경우 [이 문서](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d78a-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="3d78a-110">기본적으로 디렉터리는 셀프 서비스 암호 재설정을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="3d78a-111">사용 하 여 hello 단계 tooturn 다음 그에:</span><span class="sxs-lookup"><span data-stu-id="3d78a-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="3d78a-112">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 구독 관리자 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="3d78a-113">이 hello 회사 또는 학교 계정 또는 같은 Microsoft 계정을 사용 하 여 toocreate 디렉터리 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="3d78a-114">Hello 왼쪽에 표시 되는 hello 탐색 모음의 toohello Active Directory 확장을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="3d78a-115">Hello에서 디렉터리 찾기 **디렉터리** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="3d78a-116">Hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="3d78a-117">Toohello 아래로 스크롤하여 **사용자 암호 재설정 정책** 섹션, 토글 hello **암호 재설정을 위해 사용할 수 있는 사용자** 옵션**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="3d78a-118">해당 hello 확인 **대체 전자 메일 주소** 그대로 둡니다; 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![셀프 서비스 암호 재설정](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="3d78a-120">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="3d78a-121">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="3d78a-121">You're done!</span></span>

<span data-ttu-id="3d78a-122">tootest에 로컬 계정이 id 공급자로 모든 로그인 정책에서 사용 하 여 hello "지금 실행" 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="3d78a-123">Hello 로컬 계정 로그인 페이지 (입력할 수 있는 전자 메일 주소 및 암호 또는 사용자 이름 및 암호)를 클릭 하 여 **계정에 액세스할 수 있습니까?** tooverify hello 소비자 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="3d78a-124">hello 셀프 서비스 암호 재설정 페이지 사용자 지정 하는 hello를 사용 하 여 [회사 브랜딩 기능](../active-directory/active-directory-add-company-branding.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d78a-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

