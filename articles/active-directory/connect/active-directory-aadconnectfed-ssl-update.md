---
title: "Azure AD Connect: Active Directory Federation Services (AD FS) 팜에 대 한 hello SSL 인증서를 업데이트 | Microsoft Docs"
description: "이 문서 정보 hello 단계 tooupdate hello SSL 인증서의 Azure AD Connect를 사용 하 여 AD FS 팜 합니다."
services: active-directory
keywords: "azure ad connect, adfs ssl 업데이트, adfs 인증서 업데이트, adfs 인증서 변경, 새 adfs 인증서, adfs 인증서, adfs ssl 인증서 업데이트, ssl 인증서 adfs 업데이트, adfs ssl 인증서 구성, adfs, ssl, 인증서, adfs 서비스 통신 인증서, 페더레이션 업데이트, 페더레이션 구성, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="1bff8-104">Active Directory Federation Services (AD FS) 팜에 대 한 hello SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="1bff8-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="1bff8-105">개요</span><span class="sxs-lookup"><span data-stu-id="1bff8-105">Overview</span></span>
<span data-ttu-id="1bff8-106">이 문서에서는 Active Directory Federation Services (AD FS) 팜에 대 한 Azure AD Connect tooupdate hello SSL 인증서를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="1bff8-107">경우에 hello 사용자 로그인 방법 선택 된 AD FS hello AD FS 팜에 대 한 hello Azure AD Connect 도구 tooeasily 업데이트 hello SSL 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="1bff8-108">모든 페더레이션 및 3 단계에 따라 간단한 응용 프로그램 프록시 WAP (웹) 서버에서 hello AD FS 팜에 대 한 SSL 인증서를 업데이트 하는 hello 전체 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![3단계](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="1bff8-110">AD FS에서 사용 되는 인증서에 대해 자세히 toolearn 참조 [AD FS에서 사용 하는 인증서 이해](https://technet.microsoft.com/library/cc730660.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bff8-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1bff8-111">Prerequisites</span></span>

* <span data-ttu-id="1bff8-112">**AD FS 팜**: AD FS 팜이 Windows Server 2012 R2 이상을 기반으로 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="1bff8-113">**Azure AD Connect**: 해당 hello를 확인 합니다. Azure AD Connect의 버전이 1.1.443.0 이상.</span><span class="sxs-lookup"><span data-stu-id="1bff8-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="1bff8-114">Hello 작업을 사용 합니다 **업데이트 AD FS SSL 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![SSL 업데이트 작업](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="1bff8-116">1단계: AD FS 팜 정보 제공</span><span class="sxs-lookup"><span data-stu-id="1bff8-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="1bff8-117">Azure AD Connect hello AD FS 팜에 대 한 tooobtain 정보를 자동으로 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="1bff8-118">AD FS (Windows Server 2016 이상)에서 hello 팜 정보를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="1bff8-119">Hello 정보를 참조 하 여 Azure AD Connect에 로컬로 저장 되는 이전 실행에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="1bff8-120">Hello 목록을 추가 하거나 hello 서버 tooreflect hello의 현재 구성을 hello AD FS 팜 제거 하 여 표시 되는 서버를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="1bff8-121">Hello 서버 정보를 제공 하는 즉시 Azure AD Connect hello 연결 및 현재 SSL 인증서 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![AD FS 서버 정보](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="1bff8-123">Hello 목록에 더 이상 hello AD FS 팜에 속하지 않는 서버 있으면 클릭 **제거** AD FS 팜의 서버 hello 목록에서 toodelete hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![목록의 오프라인 서버](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="1bff8-125">Hello 목록에서 서버를 제거 합니다. 서버는 AD FS에 대 한 Azure AD Connect의 팜에 로컬 작업으로 업데이트 hello Azure AD Connect를 로컬로 유지 관리 하는 AD FS 팜 hello에 대 한 정보.</span><span class="sxs-lookup"><span data-stu-id="1bff8-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="1bff8-126">Azure AD Connect에는 AD FS tooreflect hello 변경 시 hello 구성을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="1bff8-127">2단계: 새 SSL 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="1bff8-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="1bff8-128">AD FS 팜 서버에 대 한 hello 정보를 확인 한 후에 Azure AD Connect hello 새 SSL 인증서를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="1bff8-129">암호로 보호 된 PFX 인증서 toocontinue hello 설치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![SSL 인증서](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="1bff8-131">Hello 인증서를 입력 한 후 Azure AD Connect가 일련의 필수 구성 요소를 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="1bff8-132">Hello AD FS 팜에 대 한 인증서를 hello hello 인증서 tooensure 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="1bff8-133">hello hello 인증서에 대 한 주체 대체 이름/제목 이름은 hello 페더레이션 서비스 이름으로 같은 hello 또는 와일드 카드 인증서.</span><span class="sxs-lookup"><span data-stu-id="1bff8-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="1bff8-134">hello 인증서는 30 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="1bff8-135">hello 인증서 신뢰 체인 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="1bff8-136">hello 인증서가 암호로 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="1bff8-137">3 단계: hello 업데이트에 대 한 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="1bff8-138">Hello 다음 단계에서 toohave hello SSL 인증서를 업데이트 해야 하는 hello 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="1bff8-139">Hello 업데이트에 대 한 오프 라인 상태인 서버를 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-139">Servers that are offline can't be selected for hello update.</span></span>

![서버 선택 tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="1bff8-141">Hello 구성을 완료 한 후 Azure AD Connect hello 업데이트의 hello 상태를 표시 하는 옵션 tooverify hello AD FS 로그인 제공 하는 hello 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![구성 완료](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="1bff8-143">FAQ</span><span class="sxs-lookup"><span data-stu-id="1bff8-143">FAQs</span></span>

* <span data-ttu-id="1bff8-144">**Hello 새 AD FS SSL 인증서에 대 한 hello 인증서의 주체 이름은 hello 해야 하는지?**</span><span class="sxs-lookup"><span data-stu-id="1bff8-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="1bff8-145">Azure AD Connect hello 인증서의 주체 이름/대체 주체 이름 hello hello 페더레이션 서비스 이름이 포함 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="1bff8-146">예를 들어, 페더레이션 서비스 이름이 fs.contoso.com 이면 hello 주체 이름/대체 주체 이름 fs.contoso.com 이어야 합니다.  와일드 카드 인증서도 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="1bff8-147">**Am I 요청 이유 자격 증명에 대 한 다시 hello WAP 서버 페이지에서?**</span><span class="sxs-lookup"><span data-stu-id="1bff8-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="1bff8-148">Hello tooAD FS 서버를 연결 하기 위해 제공 된 자격 증명도 hello 권한 toomanage hello WAP 서버에 없을 경우 Azure AD Connect hello WAP 서버에 대 한 관리 권한이 있는 자격 증명을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="1bff8-149">**hello 서버는 오프 라인으로 표시 됩니다. 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="1bff8-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="1bff8-150">Azure AD Connect hello 서버가 오프 라인인 경우 모든 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="1bff8-151">Hello 서버가 AD FS 팜 hello의 일부 이면 hello 연결 toohello 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="1bff8-152">Hello 문제를 해결 한 후 hello 마법사에서 hello 새로 고침 아이콘 tooupdate hello 상태 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="1bff8-153">Hello 서버에서 일부 hello의 팜 이전 하지만 이제 더 이상 존재 하지를 누르고 **제거** toodelete hello Azure AD에 연결 하는 서버 목록에서 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="1bff8-154">Azure AD Connect의 hello 목록에서 제거 hello 서버 hello AD FS 구성 자체를 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="1bff8-155">AD FS Windows Server 2016 이상 버전에서는 hello 구성 설정에 남아 있는 hello 서버 사용 중이 고 표시 될 경우 다시 hello 다음 번 hello 작업이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="1bff8-156">**Hello 새 SSL 인증서로 내 팜 서버의 하위 집합을 업데이트할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="1bff8-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="1bff8-157">예.</span><span class="sxs-lookup"><span data-stu-id="1bff8-157">Yes.</span></span> <span data-ttu-id="1bff8-158">Hello 작업을 항상 실행할 수 있습니다 **업데이트 SSL 인증서** tooupdate hello 다시 남아 있는 서버.</span><span class="sxs-lookup"><span data-stu-id="1bff8-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="1bff8-159">Hello에 **SSL에 대 한 서버 선택 인증서 업데이트** 페이지에서 서버 hello 목록에서 정렬할 수 있습니다 **SSL 만료 날짜** tooeasily 액세스 hello 서버에 아직 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="1bff8-160">**Hello hello 이전에 실행 서버를 제거 했지만 아니지 여전히 되 고 오프 라인 고 나열 된 것으로 hello AD FS 서버 페이지에 있습니다. 제거 했지만 후에 오프 라인 서버 아직 중지 되지 않은 hello를 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="1bff8-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="1bff8-161">Azure AD Connect의 hello 목록에서 제거 hello 서버 hello AD FS 구성에서에서 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="1bff8-162">Azure AD Connect hello 팜에 대 한 모든 정보에 대 한 AD FS (Windows Server 2016 이상이)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="1bff8-163">Hello 서버 hello AD FS 구성에에서 여전히 있는 경우 다시 hello 목록에에서 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bff8-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1bff8-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1bff8-164">Next steps</span></span>

- [<span data-ttu-id="1bff8-165">Azure AD Connect 및 페더레이션</span><span class="sxs-lookup"><span data-stu-id="1bff8-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="1bff8-166">Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1bff8-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
