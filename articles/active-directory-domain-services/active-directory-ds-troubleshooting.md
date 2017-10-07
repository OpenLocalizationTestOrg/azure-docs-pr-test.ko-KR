---
title: "Azure Active Directory Domain Services: 문제 해결 가이드 | Microsoft Docs"
description: "Azure AD 도메인 서비스에 대한 문제 해결 가이드"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a><span data-ttu-id="a8f2d-103">Azure AD Domain Services - 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="a8f2d-103">Azure AD Domain Services - Troubleshooting guide</span></span>
<span data-ttu-id="a8f2d-104">이 문서는 Azure AD(Active Directory) 도메인 서비스를 설치하거나 관리할 때 발생할 수 있는 문제에 대한 문제 해결 힌트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span></span>

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a><span data-ttu-id="a8f2d-105">Azure AD 디렉터리에 대해 Azure AD Domain Services를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span></span>
<span data-ttu-id="a8f2d-106">Tooenable 디렉터리에 대 한 Azure AD 도메인 서비스를 시도 하 고 실패 하거나 가져옵니다 때 오류를 해결 하는이 섹션 사용 하면 뒤로 too'Disabled 설정/해제 '.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-106">This section helps you troubleshoot errors when you try tooenable Azure AD Domain Services for your directory and it fails or gets toggled back too'Disabled'.</span></span>

<span data-ttu-id="a8f2d-107">Hello toohello 오류 메시지가 발생 하면 해당 하는 문제 해결 단계를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-107">Pick hello troubleshooting steps that correspond toohello error message you encounter.</span></span>

| <span data-ttu-id="a8f2d-108">**오류 메시지**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-108">**Error Message**</span></span> | <span data-ttu-id="a8f2d-109">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-109">**Resolution**</span></span> |
| --- |:--- |
| <span data-ttu-id="a8f2d-110">*hello 이름 contoso100.com 이미이 네트워크에서 사용 중입니다. 사용하지 않는 이름을 지정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-110">*hello name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span> |[<span data-ttu-id="a8f2d-111">Hello 가상 네트워크의 도메인 이름 충돌</span><span class="sxs-lookup"><span data-stu-id="a8f2d-111">Domain name conflict in hello virtual network</span></span>](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| <span data-ttu-id="a8f2d-112">*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 서비스에는 적절 한 사용 권한이 toohello 응용 프로그램 'Azure AD 도메인 서비스 Sync' 라는 없습니다. 'Azure AD 도메인 서비스 Sync'를 호출 하는 hello 응용 프로그램을 삭제 하 고 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-112">*Domain Services could not be enabled in this Azure AD tenant. hello service does not have adequate permissions toohello application called 'Azure AD Domain Services Sync'. Delete hello application called 'Azure AD Domain Services Sync' and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="a8f2d-113">도메인 서비스에 적절 한 사용 권한이 toohello Azure AD 도메인 서비스 동기화 응용 프로그램이 없는</span><span class="sxs-lookup"><span data-stu-id="a8f2d-113">Domain Services does not have adequate permissions toohello Azure AD Domain Services Sync application</span></span>](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| <span data-ttu-id="a8f2d-114">*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 도메인 서비스에서 Azure AD 테 넌 트 응용 프로그램을 hello 가지 않습니다 권한 tooenable 도메인 서비스를 필요 합니다. 응용 프로그램 식별자 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello와 hello 응용 프로그램을 삭제 한 후 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-114">*Domain Services could not be enabled in this Azure AD tenant. hello Domain Services application in your Azure AD tenant does not have hello required permissions tooenable Domain Services. Delete hello application with hello application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="a8f2d-115">테 넌 트에 도메인 서비스 응용 프로그램 hello 제대로 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-115">hello Domain Services application is not configured properly in your tenant</span></span>](active-directory-ds-troubleshooting.md#invalid-configuration) |
| <span data-ttu-id="a8f2d-116">*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello Microsoft Azure AD 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다. 응용 프로그램 식별자 00000002-0000-0000-c000-000000000000 hello와 hello 응용 프로그램을 사용 하도록 설정 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-116">*Domain Services could not be enabled in this Azure AD tenant. hello Microsoft Azure AD application is disabled in your Azure AD tenant. Enable hello application with hello application identifier 00000002-0000-0000-c000-000000000000 and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="a8f2d-117">hello Microsoft Graph 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-117">hello Microsoft Graph application is disabled in your Azure AD tenant</span></span>](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a><span data-ttu-id="a8f2d-118">도메인 이름 충돌</span><span class="sxs-lookup"><span data-stu-id="a8f2d-118">Domain Name conflict</span></span>
<span data-ttu-id="a8f2d-119">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-119">**Error message:**</span></span>

<span data-ttu-id="a8f2d-120">*hello 이름 contoso100.com 이미이 네트워크에서 사용 중입니다. 사용하지 않는 이름을 지정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-120">*hello name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span>

<span data-ttu-id="a8f2d-121">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-121">**Remediation:**</span></span>

<span data-ttu-id="a8f2d-122">Hello로 기존 도메인 가졌는지 확인 동일한 도메인 이름을 해당 가상 네트워크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-122">Ensure that you do not have an existing domain with hello same domain name available on that virtual network.</span></span> <span data-ttu-id="a8f2d-123">예를 들어 hello 선택한 가상 네트워크에서 이미 사용할 수 있는 ' contoso.com' 이라는 도메인을 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-123">For instance, assume you have a domain called 'contoso.com' already available on hello selected virtual network.</span></span> <span data-ttu-id="a8f2d-124">나중 tooenable hello로 사용 되는 Azure AD 도메인 서비스는 관리 되는 도메인을 시도 하면 해당 가상 네트워크에 동일한 도메인 이름 (즉, ' contoso.com').</span><span class="sxs-lookup"><span data-stu-id="a8f2d-124">Later, you try tooenable an Azure AD Domain Services managed domain with hello same domain name (that is, 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="a8f2d-125">Tooenable Azure AD 도메인 서비스는 동안 오류가 발생 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-125">You encounter a failure when trying tooenable Azure AD Domain Services.</span></span>

<span data-ttu-id="a8f2d-126">이 오류는 해당 가상 네트워크에서 도메인 이름 hello에 대 한 tooname 충돌 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-126">This failure is due tooname conflicts for hello domain name on that virtual network.</span></span> <span data-ttu-id="a8f2d-127">이 경우 Azure AD 도메인 서비스는 관리 되는 도메인을 다른 이름 tooset를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-127">In this situation, you must use a different name tooset up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="a8f2d-128">또는 기존 도메인 hello를 프로 비전 해제할 수 있으며 tooenable Azure AD 도메인 서비스를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-128">Alternately, you can de-provision hello existing domain and then proceed tooenable Azure AD Domain Services.</span></span>

### <a name="inadequate-permissions"></a><span data-ttu-id="a8f2d-129">부적절한 권한</span><span class="sxs-lookup"><span data-stu-id="a8f2d-129">Inadequate permissions</span></span>
<span data-ttu-id="a8f2d-130">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-130">**Error message:**</span></span>

<span data-ttu-id="a8f2d-131">*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 서비스에는 적절 한 사용 권한이 toohello 응용 프로그램 'Azure AD 도메인 서비스 Sync' 라는 없습니다. 'Azure AD 도메인 서비스 Sync'를 호출 하는 hello 응용 프로그램을 삭제 하 고 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-131">*Domain Services could not be enabled in this Azure AD tenant. hello service does not have adequate permissions toohello application called 'Azure AD Domain Services Sync'. Delete hello application called 'Azure AD Domain Services Sync' and then try tooenable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="a8f2d-132">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-132">**Remediation:**</span></span>

<span data-ttu-id="a8f2d-133">Azure AD 디렉터리에서 'Azure AD 도메인 서비스 Sync' hello 이름의 응용 프로그램인 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-133">Check toosee if there is an application with hello name 'Azure AD Domain Services Sync' in your Azure AD directory.</span></span> <span data-ttu-id="a8f2d-134">이 응용 프로그램이 있으면 삭제한 다음 Azure AD Domain Services를 사용하도록 다시 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="a8f2d-135">수행 hello 단계 toocheck hello 응용 프로그램 및 toodelete hello 있는지에 대 한 다음, hello 응용 프로그램이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="a8f2d-135">Perform hello following steps toocheck for hello presence of hello application and toodelete it, if hello application exists:</span></span>

1. <span data-ttu-id="a8f2d-136">Toohello 이동 **Azure 클래식 포털** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="a8f2d-136">Navigate toohello **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span></span>
2. <span data-ttu-id="a8f2d-137">선택 hello **Active Directory** hello 왼쪽된 창에서 노드.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-137">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="a8f2d-138">Azure AD 도메인 서비스 선택 hello Azure AD 테 넌 트 (디렉터리) tooenable 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-138">Select hello Azure AD tenant (directory) for which you would like tooenable Azure AD Domain Services.</span></span>
4. <span data-ttu-id="a8f2d-139">Toohello 이동 **응용 프로그램** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-139">Navigate toohello **Applications** tab.</span></span>
5. <span data-ttu-id="a8f2d-140">선택 hello **회사가 보유 한 응용 프로그램** hello 드롭다운에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-140">Select hello **Applications my company owns** option in hello dropdown.</span></span>
6. <span data-ttu-id="a8f2d-141">**Azure AD Domain Services 동기화**라는 응용 프로그램이 있는지 확인합니다. Hello 응용 프로그램에서 볼 수 있으면 계속 toodelete 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-141">Check for an application called **Azure AD Domain Services Sync**. If hello application exists, proceed toodelete it.</span></span>
7. <span data-ttu-id="a8f2d-142">Hello 응용 프로그램을 삭제 한 후 tooenable Azure AD 도메인 서비스를 다시 한 번 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-142">Once you have deleted hello application, try tooenable Azure AD Domain Services once again.</span></span>

### <a name="invalid-configuration"></a><span data-ttu-id="a8f2d-143">유효하지 않은 구성</span><span class="sxs-lookup"><span data-stu-id="a8f2d-143">Invalid configuration</span></span>
<span data-ttu-id="a8f2d-144">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-144">**Error message:**</span></span>

<span data-ttu-id="a8f2d-145">*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 도메인 서비스에서 Azure AD 테 넌 트 응용 프로그램을 hello 가지 않습니다 권한 tooenable 도메인 서비스를 필요 합니다. 응용 프로그램 식별자 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello와 hello 응용 프로그램을 삭제 한 후 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.*</span><span class="sxs-lookup"><span data-stu-id="a8f2d-145">*Domain Services could not be enabled in this Azure AD tenant. hello Domain Services application in your Azure AD tenant does not have hello required permissions tooenable Domain Services. Delete hello application with hello application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try tooenable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="a8f2d-146">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-146">**Remediation:**</span></span>

<span data-ttu-id="a8f2d-147">(D87dcbc6-a371-462e-88e3-28ad15ec4e64의 응용 프로그램 식별자)를 가진 ' AzureActiveDirectoryDomainControllerServices' hello 이름의 응용 프로그램이 Azure AD 디렉터리에 있는 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-147">Check toosee if you have an application with hello name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span></span> <span data-ttu-id="a8f2d-148">이 응용 프로그램이 있으면 하 고 다시 활성화 한 다음 Azure AD 도메인 서비스 toodelete 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-148">If this application exists, you need toodelete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="a8f2d-149">다음 PowerShell 스크립트 toofind hello 응용 프로그램 hello를 사용 하 여 삭제.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-149">Use hello following PowerShell script toofind hello application and delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f2d-150">이 스크립트는 **Azure AD PowerShell 버전 2** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-150">This script uses **Azure AD PowerShell version 2** cmdlets.</span></span> <span data-ttu-id="a8f2d-151">모든 사용 가능한 cmdlet 및 toodownload hello 모듈의 전체 목록에 대 한 읽기 hello [azure Ad PowerShell 참조 설명서](https://msdn.microsoft.com/library/azure/mt757189.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-151">For a full list of all available cmdlets and toodownload hello module, read hello [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span></span>
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a><span data-ttu-id="a8f2d-152">Microsoft Graph 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="a8f2d-152">Microsoft Graph disabled</span></span>
<span data-ttu-id="a8f2d-153">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-153">**Error message:**</span></span>

<span data-ttu-id="a8f2d-154">이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-154">Domain Services could not be enabled in this Azure AD tenant.</span></span> <span data-ttu-id="a8f2d-155">hello Microsoft Azure AD 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-155">hello Microsoft Azure AD application is disabled in your Azure AD tenant.</span></span> <span data-ttu-id="a8f2d-156">응용 프로그램 식별자 00000002-0000-0000-c000-000000000000 hello와 hello 응용 프로그램을 사용 하도록 설정 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-156">Enable hello application with hello application identifier 00000002-0000-0000-c000-000000000000 and then try tooenable Domain Services for your Azure AD tenant.</span></span>

<span data-ttu-id="a8f2d-157">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="a8f2d-157">**Remediation:**</span></span>

<span data-ttu-id="a8f2d-158">Hello 식별자 00000002-0000-0000-c000-000000000000으로 응용 프로그램을 사용 하지 않도록 설정한 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-158">Check toosee if you have disabled an application with hello identifier 00000002-0000-0000-c000-000000000000.</span></span> <span data-ttu-id="a8f2d-159">이 응용 프로그램은 Microsoft Azure AD 응용 프로그램 hello 고 Graph API 액세스 tooyour Azure AD 테 넌 트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-159">This application is hello Microsoft Azure AD application and provides Graph API access tooyour Azure AD tenant.</span></span> <span data-ttu-id="a8f2d-160">Azure AD 도메인 서비스에 Azure AD 테 넌 트 tooyour 관리 되는이 응용 프로그램 활성화 toobe toosynchronize 필요한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-160">Azure AD Domain Services needs this application toobe enabled toosynchronize your Azure AD tenant tooyour managed domain.</span></span>

<span data-ttu-id="a8f2d-161">tooresolve이이 오류를이 응용 프로그램을 사용 하도록 설정 하 고 다음 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-161">tooresolve this error, enable this application and then try tooenable Domain Services for your Azure AD tenant.</span></span>

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="a8f2d-162">사용자가 없습니다 toosign toohello 관리 되는 Azure AD 도메인 서비스 도메인에서</span><span class="sxs-lookup"><span data-stu-id="a8f2d-162">Users are unable toosign in toohello Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="a8f2d-163">하나 이상의 사용자가 Azure AD 테 넌 트에 없습니다 toosign toohello 새로 만든 관리 되는 도메인의 인 hello 문제 해결 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-163">If one or more users in your Azure AD tenant are unable toosign in toohello newly created managed domain, perform hello following troubleshooting steps:</span></span>

* <span data-ttu-id="a8f2d-164">**로그인 UPN 형식을 사용 하 여:** toosign hello UPN 형식을 사용 하 여 시도 하세요 (예를 들어 'joeuser@contoso.com') hello SAMAccountName 형식 ('CONTOSO\joeuser') 대신.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-164">**Sign-in using UPN format:** Try toosign in using hello UPN format (for example, 'joeuser@contoso.com') instead of hello SAMAccountName format ('CONTOSO\joeuser').</span></span> <span data-ttu-id="a8f2d-165">SAMAccountName hello hello 관리 되는 도메인에 있는 다른 사용자와 동일한 hello은 너무 긴 UPN 접두사를 가진 되었거나 사용자에 대해 자동으로 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-165">hello SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is hello same as another user on hello managed domain.</span></span> <span data-ttu-id="a8f2d-166">hello UPN 형식 toobe Azure AD 테 넌 트 내에서 고유 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-166">hello UPN format is guaranteed toobe unique within an Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f2d-167">Toohello Azure AD 도메인 서비스에 대 한 관리 되는 도메인에서 UPN 형식 toosign hello를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-167">We recommend using hello UPN format toosign in toohello Azure AD Domain Services managed domain.</span></span>
>
>

* <span data-ttu-id="a8f2d-168">갖추어야 할 [암호 동기화를 사용 하도록 설정](active-directory-ds-getting-started-password-sync.md) hello 시작 가이드에 설명 된 hello 단계에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-168">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with hello steps outlined in hello Getting Started guide.</span></span>
* <span data-ttu-id="a8f2d-169">**외부 계정:** hello 영향을 받는 사용자 계정을 hello Azure AD 테 넌 트에 외부 계정이 아닌지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-169">**External accounts:** Ensure that hello affected user account is not an external account in hello Azure AD tenant.</span></span> <span data-ttu-id="a8f2d-170">외부 계정의 예는 Microsoft 계정(예: 'joe@live.com') 또는 외부 Azure AD 디렉터리에서 사용자 계정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-170">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span></span> <span data-ttu-id="a8f2d-171">Azure AD 도메인 서비스에 이러한 사용자 계정에 대 한 자격 증명이 없기 때문에 이러한 사용자 toohello 관리 되는 도메인에 서명할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-171">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in toohello managed domain.</span></span>
* <span data-ttu-id="a8f2d-172">**계정 동기화:** hello 영향을 받는 사용자 계정이 온-프레미스 디렉터리에서 동기화를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-172">**Synced accounts:** If hello affected user accounts are synchronized from an on-premises directory, verify that:</span></span>

  * <span data-ttu-id="a8f2d-173">배포 했거나 toohello 업데이트 [최신 버전의 Azure AD Connect 권장](https://www.microsoft.com/en-us/download/details.aspx?id=47594)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-173">You have deployed or updated toohello [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span></span>
  * <span data-ttu-id="a8f2d-174">Azure AD Connect를 너무 구성한[전체 동기화를 수행](active-directory-ds-getting-started-password-sync.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-174">You have configured Azure AD Connect too[perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span></span>
  * <span data-ttu-id="a8f2d-175">디렉터리의 hello 크기에 따라 수는 사용자 계정에 대 한 시간이 걸릴 하 고 해시 toobe Azure AD 도메인 서비스에서 사용할 수 있는 자격 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-175">Depending on hello size of your directory, it may take a while for user accounts and credential hashes toobe available in Azure AD Domain Services.</span></span> <span data-ttu-id="a8f2d-176">인증 (hello의 크기에 따라 몇 시간 tooa 일 또는 큰 디렉터리에 대 한 두 디렉터리-)을 다시 시도 하기 전에 충분 한 시간 동안 대기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-176">Ensure you wait long enough before retrying authentication (depending on hello size of your directory - a few hours tooa day or two for large directories).</span></span>
  * <span data-ttu-id="a8f2d-177">Hello 이전 단계를 확인 한 후 hello 문제가 지속 되 면 hello Microsoft Azure AD Sync Service를 다시 시작 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-177">If hello issue persists after verifying hello preceding steps, try restarting hello Microsoft Azure AD Sync Service.</span></span> <span data-ttu-id="a8f2d-178">동기화 시스템에서 명령 프롬프트를 시작 하 고 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-178">From your sync machine, launch a command prompt and execute hello following commands:</span></span>

    1. <span data-ttu-id="a8f2d-179">net stop 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="a8f2d-179">net stop 'Microsoft Azure AD Sync'</span></span>
    2. <span data-ttu-id="a8f2d-180">net start 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="a8f2d-180">net start 'Microsoft Azure AD Sync'</span></span>
* <span data-ttu-id="a8f2d-181">**클라우드 전용 계정을**: hello 영향을 받는 사용자 계정을 클라우드 전용 사용자 계정이 확인 Azure AD 도메인 서비스를 사용 하도록 설정한 후 해당 hello 사용자가 자신의 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-181">**Cloud-only accounts**: If hello affected user account is a cloud-only user account, ensure that hello user has changed their password after you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="a8f2d-182">이 단계를 수행 하면 hello 자격 증명 생성 된 Azure AD 도메인 서비스 toobe 필요한 해시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-182">This step causes hello credential hashes required for Azure AD Domain Services toobe generated.</span></span>

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a><span data-ttu-id="a8f2d-183">Azure AD 테넌트에서는 제거되지만 관리되는 도메인에서는 제거되지 않는 사용자</span><span class="sxs-lookup"><span data-stu-id="a8f2d-183">Users removed from your Azure AD tenant are not removed from your managed domain</span></span>
<span data-ttu-id="a8f2d-184">Azure AD에서는 사용자 개체를 실수로 삭제하지 못하도록 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-184">Azure AD protects you from accidental deletion of user objects.</span></span> <span data-ttu-id="a8f2d-185">Azure AD 테 넌 트 로부터 사용자 계정을 삭제 하면 hello 해당 하는 사용자 개체는 이동된 toohello 휴지통을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-185">When you delete a user account from your Azure AD tenant, hello corresponding user object is moved toohello Recycle Bin.</span></span> <span data-ttu-id="a8f2d-186">이 삭제 작업은 동기화 된 tooyour 관리 되는 도메인을 하면 hello 사용 안 함을 표시 하는 사용자 계정 toobe에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-186">When this delete operation is synchronized tooyour managed domain, it causes hello corresponding user account toobe marked disabled.</span></span> <span data-ttu-id="a8f2d-187">이 기능을 사용 하면 복구 하거나 나중에 hello 사용자 계정 삭제 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-187">This feature helps you recover or undelete hello user account later.</span></span>

<span data-ttu-id="a8f2d-188">hello hello에 남아 있는 관리 되는 도메인의 상태를 사용 하지 않도록 설정 하는 사용자 계정, 가진 사용자 계정을 다시 만드는 경우에 hello Azure AD 디렉터리에서 동일한 UPN입니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-188">hello user account remains in hello disabled state in your managed domain, even if you re-create a user account with hello same UPN in your Azure AD directory.</span></span> <span data-ttu-id="a8f2d-189">tooforce 필요한 관리 되는 도메인에서 tooremove hello 사용자 계정에 Azure AD 테 넌 트에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-189">tooremove hello user account from your managed domain, you need tooforce delete it from your Azure AD tenant.</span></span>

<span data-ttu-id="a8f2d-190">tooremove hello 사용자 계정을 통해 관리 되는 도메인에서 완벽 하 게 Azure AD 테 넌 트에서 hello 사용자를 영구적으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-190">tooremove hello user account fully from your managed domain, delete hello user permanently from your Azure AD tenant.</span></span> <span data-ttu-id="a8f2d-191">Hello Remove-msoluser PowerShell cmdlet을 사용 하 여 hello로 '-RemoveFromRecycleBin' 옵션을이에 설명 된 대로 [MSDN 문서](https://msdn.microsoft.com/library/azure/dn194132.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-191">Use hello Remove-MsolUser PowerShell cmdlet with hello '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span></span>

## <a name="contact-us"></a><span data-ttu-id="a8f2d-192">문의처</span><span class="sxs-lookup"><span data-stu-id="a8f2d-192">Contact Us</span></span>
<span data-ttu-id="a8f2d-193">너무 hello Azure Active Directory 도메인 서비스 제품 팀에 문의[의견 공유 또는 지원을 위해](active-directory-ds-contact-us.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8f2d-193">Contact hello Azure Active Directory Domain Services product team too[share feedback or for support](active-directory-ds-contact-us.md).</span></span>
