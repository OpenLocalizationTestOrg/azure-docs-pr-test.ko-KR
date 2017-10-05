---
title: "Azure AD Connect: AD FS(Active Directory Federation Services) 팜에 대한 SSL 인증서 업데이트 | Microsoft 문서"
description: "이 문서에서는 Azure AD Connect를 사용하여 AD FS 팜의 SSL 인증서를 업데이트하는 단계를 자세히 설명합니다."
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
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="3986b-104">AD FS(Active Directory Federation Services) 팜에 대한 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="3986b-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="3986b-105">개요</span><span class="sxs-lookup"><span data-stu-id="3986b-105">Overview</span></span>
<span data-ttu-id="3986b-106">이 문서에서는 Azure AD Connect를 사용하여 AD FS(Active Directory Federation Services) 팜에 대한 SSL 인증서를 업데이트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="3986b-107">선택된 사용자 로그인 방법이 AD FS가 아닌 경우에도 Azure AD Connect 도구를 사용하여 AD FS 팜의 SSL 인증서를 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="3986b-108">간단한 3단계에 따라 모든 페더레이션 및 WAP(웹 응용 프로그램 프록시) 서버 간에 AD FS 팜의 SSL 인증서를 업데이트하는 전체 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![3단계](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="3986b-110">AD FS에서 사용하는 인증서에 대한 자세한 내용은 [AD FS에서 사용하는 인증서 이해](https://technet.microsoft.com/library/cc730660.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3986b-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3986b-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3986b-111">Prerequisites</span></span>

* <span data-ttu-id="3986b-112">**AD FS 팜**: AD FS 팜이 Windows Server 2012 R2 이상을 기반으로 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="3986b-113">**Azure AD Connect**: Azure AD Connect 버전이 1.1.443.0 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="3986b-114">**AD FS SSL 인증서 업데이트** 작업을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![SSL 업데이트 작업](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="3986b-116">1단계: AD FS 팜 정보 제공</span><span class="sxs-lookup"><span data-stu-id="3986b-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="3986b-117">Azure AD Connect는 다음과 같은 방법으로 AD FS 팜에 대한 정보를 자동으로 가져오려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="3986b-118">AD FS(Windows Server 2016 이상)에서 팜 정보 쿼리.</span><span class="sxs-lookup"><span data-stu-id="3986b-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="3986b-119">Azure AD Connect를 통해 로컬에 저장된 이전 실행의 정보 참조.</span><span class="sxs-lookup"><span data-stu-id="3986b-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="3986b-120">표시된 서버 목록은 서버를 추가하거나 제거하여 AD FS 팜의 현재 구성을 반영하도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="3986b-121">서버 정보가 제공되면 바로 Azure AD Connect가 연결 및 현재 SSL 인증서 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![AD FS 서버 정보](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="3986b-123">더 이상 AD FS 팜에 포함되지 않는 서버가 목록에 들어 있으면 **제거**를 클릭하여 AD FS 팜의 서버 목록에서 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![목록의 오프라인 서버](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="3986b-125">Azure AD Connect에서 AD FS 팜에 대한 서버 목록에서 서버를 제거하는 것은 로컬 작업이며 이 작업을 수행하면 Azure AD Connect가 로컬에서 유지 관리하는 AD FS 팜에 대한 정보가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="3986b-126">Azure AD Connect는 변경 내용을 반영하기 위해 AD FS의 구성을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="3986b-127">2단계: 새 SSL 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="3986b-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="3986b-128">AD FS 팜 서버에 대한 정보가 확인된 후 Azure AD Connect는 새 SSL 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="3986b-129">설치를 계속하려면 암호로 보호된 PFX 인증서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL 인증서](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="3986b-131">인증서를 제공하면 Azure AD Connect가 일련의 필수 조건을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="3986b-132">인증서에서 다음 사항을 확인하여 AD FS 팜의 인증서가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="3986b-133">인증서의 주체 이름/주체 대체 이름은 페더레이션 서비스 이름과 같거나 와일드카드 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="3986b-134">인증서가 30일 이상 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="3986b-135">인증서 신뢰 체인이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="3986b-136">인증서가 암호로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="3986b-137">3단계: 업데이트할 서버 선택</span><span class="sxs-lookup"><span data-stu-id="3986b-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="3986b-138">다음 단계에서는 SSL 인증서를 업데이트해야 하는 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="3986b-139">오프라인 상태인 서버는 업데이트 대상으로 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-139">Servers that are offline can't be selected for the update.</span></span>

![업데이트할 서버 선택](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="3986b-141">구성이 완료되면 Azure AD Connect는 업데이트 상태를 나타내는 메시지를 표시하고 AD FS 로그인을 확인하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![구성 완료](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="3986b-143">FAQ</span><span class="sxs-lookup"><span data-stu-id="3986b-143">FAQs</span></span>

* <span data-ttu-id="3986b-144">**새 AD FS SSL 인증서에 대한 인증서의 주체 이름은 무엇이어야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3986b-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="3986b-145">Azure AD Connect는 인증서의 주체 이름/대체 주체 이름에 페더레이션 서비스 이름이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="3986b-146">예를 들어 페더레이션 서비스 이름이 fs.contoso.com이면 주체 이름/대체 주체 이름은 fs.contoso.com이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="3986b-147">와일드 카드 인증서도 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="3986b-148">**WAP 서버 페이지에서 자격 증명이 다시 요청되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="3986b-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="3986b-149">AD FS 서버에 연결하기 위해 제공한 자격 증명에 WAP 서버를 관리할 권한이 없으면 Azure AD Connect는 WAP 서버에 대한 관리자 권한이 포함된 자격 증명을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="3986b-150">**서버가 오프라인으로 표시됩니다. 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="3986b-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="3986b-151">서버가 오프라인 상태이면 Azure AD Connect가 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="3986b-152">서버가 AD FS 팜의 일부이면 서버 연결을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3986b-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="3986b-153">이 문제를 해결한 후 마법사에서 새로 고침 아이콘을 눌러 상태를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="3986b-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="3986b-154">서버가 이전에 팜에 포함되었지만 더 이상 존재하지 않으면 **제거**를 클릭하여 Azure AD Connect가 유지 관리하는 서버 목록에서 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="3986b-155">Azure AD Connect의 목록에서 서버를 제거해도 AD FS 구성 자체는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="3986b-156">Windows Server 2016 이상에서 AD FS를 사용하는 경우 서버는 구성 설정에 남아 있게 되며 다음에 작업이 실행될 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="3986b-157">**새 SSL 인증서를 사용하여 내 팜 서버의 하위 집합을 업데이트할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="3986b-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="3986b-158">예.</span><span class="sxs-lookup"><span data-stu-id="3986b-158">Yes.</span></span> <span data-ttu-id="3986b-159">언제든지 **SSL 인증서 업데이트** 작업을 다시 실행하여 나머지 서버를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="3986b-160">**SSL 인증서 업데이트용 서버 선택** 페이지에서 **SSL 만료 날짜**를 기준으로 서버 목록을 정렬하면 아직 업데이트되지 않은 서버에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="3986b-161">**이전 실행에서 서버를 제거했지만 계속 오프라인 상태로 표시되고 AD FS 서버 페이지에 나열됩니다. 제거한 후에도 오프라인 서버가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="3986b-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="3986b-162">Azure AD Connect의 목록에서 서버를 제거해도 AD FS 구성에서는 서버가 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="3986b-163">Azure AD Connect는 팜에 대한 정보를 얻기 위해 AD FS(Windows Server 2016 이상)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="3986b-164">서버가 AD FS 구성에 남아 있으면 해당 서버는 목록에 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3986b-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3986b-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3986b-165">Next steps</span></span>

- [<span data-ttu-id="3986b-166">Azure AD Connect 및 페더레이션</span><span class="sxs-lookup"><span data-stu-id="3986b-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="3986b-167">Azure AD Connect를 사용하여 Active Directory Federation Services 관리 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3986b-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
