---
title: "백업 및 복원 Azure API 관리에서 사용 하 여 aaaImplement 재해 복구 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 백업 및 Azure API 관리에서 tooperform 재해 복구를 복원 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="16c94-103">Tooimplement 재해 복구를 사용 하 여 백업 서비스 및 Azure API 관리에서 복원 방법</span><span class="sxs-lookup"><span data-stu-id="16c94-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="16c94-104">Toopublish를 선택 하 고 있는 toodesign, 구현 및 관리 해야 하는 많은 오류 내결함성 및 인프라 기능을 수행 하는 Azure API 관리를 통해 Api 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="16c94-105">Azure 플랫폼 hello 늘어나 hello 비용의 일부분에 발생할 수 있는 오류를 완화합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="16c94-106">여기서 API 관리 서비스는 hello 지역에 영향을 주는 가용성 문제 로부터 toorecover 호스트 하면 언제 든 지 준비 tooreconstitute 다른 지역에 서비스 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="16c94-107">가용성 목표와 복구 시간 목표에 따라 수도 tooreserve 백업 서비스 하나 이상의 영역에 있으며 구성 및 콘텐츠 hello 활성 서비스와 동기화 toomaintain를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="16c94-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="16c94-108">hello 서비스 백업 및 복원 기능은 재해 복구 전략을 구현 하기 위한 hello 필요한 문서 블록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="16c94-109">이 가이드에서는 Azure 리소스 관리자 tooauthenticate 요청 방법 등에 toobackup 및 API 관리 서비스 인스턴스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="16c94-110">API 관리 서비스 인스턴스를 준비 하는 등의 시나리오에 대 한 복제를 위한 백업 및 재해 복구에 대 한 API 관리 서비스 인스턴스 복원에 대 한 hello 프로세스를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="16c94-111">각 백업은 30일 후 만료되니 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="16c94-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="16c94-112">와 hello 복원이 실패 합니다 hello 30 일 만료 기간이 만료 된 후 toorestore 백업을 시도 하면는 `Cannot restore: backup expired` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="16c94-113">Azure 리소스 관리자 요청 인증</span><span class="sxs-lookup"><span data-stu-id="16c94-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="16c94-114">hello REST API 백업 및 복원에 대 한 Azure 리소스 관리자를 사용 하 여 및에 서로 다른 인증 메커니즘이 API 관리 엔터티를 관리 하기 위한 REST Api를 hello 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="16c94-115">이 섹션의 단계 hello tooauthenticate Azure 리소스 관리자 요청 하는 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="16c94-116">자세한 내용은 [Azure 리소스 관리자 요청 인증](http://msdn.microsoft.com/library/azure/dn790557.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c94-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="16c94-117">모든 사용자가 hello Azure 리소스 관리자를 사용 하 여 리소스에서 수행 하는 hello 작업 단계를 수행 하는 hello를 사용 하 여 Azure Active Directory와 인증 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="16c94-118">응용 프로그램 toohello Azure Active Directory 테 넌 트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="16c94-119">사용자가 추가한 hello 응용 프로그램에 대 한 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="16c94-120">리소스 관리자 요청 tooAzure를 인증 하기 위한 hello 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="16c94-121">hello 첫 번째 단계는 toocreate Azure Active Directory 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="16c94-122">Hello에 로그인 [Azure 클래식 포털](http://manage.windowsazure.com/) API 관리 서비스를 포함 하는 hello 구독을 사용 하 여 인스턴스 및 toohello 이동 **응용 프로그램** 기본 Azure Active Directory에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="16c94-123">Hello Azure Active Directory 기본 디렉터리 표시 tooyour 계정이 아닌 경우 hello Azure 구독 toogrant hello의 연락처 hello 관리자 tooyour 계정 사용 권한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Azure Active Directory 응용 프로그램 만들기][api-management-add-aad-application]

<span data-ttu-id="16c94-125">**추가**, **조직에서 개발 중인 응용 프로그램 추가**를 선택하고 **네이티브 클라이언트 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="16c94-126">설명이 포함 된 이름을 입력 하 고 hello 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="16c94-127">같은 자리 표시자 URL을 입력 `http://resources` hello에 대 한 **리디렉션 URI**처럼 필수 필드 이지만 hello 값은 나중에 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="16c94-128">Hello 확인란 toosave hello 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="16c94-129">Hello 응용 프로그램을 저장 한 후 클릭 **구성**, toohello 아래로 스크롤하여 **tooother 응용 프로그램 사용 권한** 섹션을 클릭 하 여 **응용 프로그램을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![권한 추가][api-management-aad-permissions-add]

<span data-ttu-id="16c94-131">선택 **Windows** **Azure 서비스 관리 API** hello 확인란 tooadd hello 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![권한 추가][api-management-aad-permissions]

<span data-ttu-id="16c94-133">클릭 **위임 된 권한** 새로 추가 된 hello 옆에 있는 **Windows** **Azure 서비스 관리 API** 응용 프로그램에 대 한 확인란 hello **Azure 액세스 서비스 관리 (미리 보기)**를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![권한 추가][api-management-aad-delegated-permissions]

<span data-ttu-id="16c94-135">이전 tooinvoking hello를 생성 하는 Api hello 백업 및 복원에 필요한 tooget 토큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="16c94-136">hello 다음 예제에서는 hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget 패키지 tooretrieve hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="16c94-137">대체 `{tentand id}`, `{application id}`, 및 `{redirect uri}` 지침을 진행 하는 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="16c94-138">대체 `{tenant id}` hello 방금 만든 Azure Active Directory 응용 프로그램의 hello 테 넌 트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="16c94-139">클릭 하 여 hello id에 액세스할 수 있습니다 **끝점 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-139">You can access hello id by clicking **View endpoints**.</span></span>

![끝점][api-management-aad-default-directory]

![끝점][api-management-endpoint]

<span data-ttu-id="16c94-142">대체 `{application id}` 및 `{redirect uri}` hello를 사용 하 여 **클라이언트 Id** hello에서 URL을 hello 및 **리디렉션 Uri** 섹션에서 Azure Active Directory 응용 프로그램의 **구성**  탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![리소스][api-management-aad-resources]

<span data-ttu-id="16c94-144">Hello 값이 지정 되어 되 면 hello 코드 예제에서는 다음 예제에서는 토큰 비슷한 toohello를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![위임][api-management-arm-token]

<span data-ttu-id="16c94-146">호출 hello 백업 및 복원 hello 다음 섹션에서에서 설명 하는 작업을 하기 전에 REST 호출에 대 한 hello 권한 부여 요청 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="16c94-147"><a name="step1"> </a>API Management 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="16c94-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="16c94-148">HTTP 요청을 수행 하는 API 관리 서비스 문제 hello tooback:</span><span class="sxs-lookup"><span data-stu-id="16c94-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="16c94-149">설명:</span><span class="sxs-lookup"><span data-stu-id="16c94-149">where:</span></span>

* <span data-ttu-id="16c94-150">`subscriptionId`-toobackup 넣을 hello API 관리 서비스를 포함 하는 hello 구독의 id</span><span class="sxs-lookup"><span data-stu-id="16c94-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="16c94-151">`resourceGroupName`-hello 'Api 기본-{서비스 영역을 (를)' 형태의 문자열로 여기서 `service-region` 예를 들어 hello Azure 지역 hello toobackup 고치려는 API 관리 서비스의 호스팅 위치를 식별`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="16c94-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="16c94-152">`serviceName`-hello hello 해당 생성 시 지정 된 백업 하는 API 관리 서비스의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="16c94-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="16c94-153">`api-version` - `2014-02-14`(으)로 대체</span><span class="sxs-lookup"><span data-stu-id="16c94-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="16c94-154">Hello hello 요청 본문을 hello 대상 Azure 저장소 계정 이름, 액세스 키, blob 컨테이너 이름 및 백업 이름 지정:</span><span class="sxs-lookup"><span data-stu-id="16c94-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="16c94-155">Hello의 hello 값 설정 `Content-Type` 요청 헤더에 너무`application/json`합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="16c94-156">백업은 여러 분 toocomplete 걸리는 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="16c94-157">Hello 요청이 성공 하 고 hello 백업 프로세스가 시작 된 경우 받을 수는 `202 Accepted` 와 응답 상태 코드는 `Location` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="16c94-158">'GET' hello에 toohello URL을 요청 확인 `Location` 헤더 toofind hello 작업의 hello 상태 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="16c94-159">Hello 백업 진행 중인 동안 tooreceive 202 수락 상태 코드는 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="16c94-160">응답 코드가 `200 OK` hello 백업 작업이 성공적으로 완료를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="16c94-161">백업 요청을 수행할 때는 제약 조건이 다음 hello를 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="16c94-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="16c94-162">**컨테이너** hello 요청 본문에 지정 된 **있어야**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="16c94-163">백업이 진행 중인 동안에는 SKU 업그레이드/다운그레이드, 도메인 이름 변경 등의 **서비스 관리 작업을 수행하면 안 됩니다** .</span><span class="sxs-lookup"><span data-stu-id="16c94-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="16c94-164">복원는 **30 일에 대해서만 백업 정해진** hello 순간 만들기 이후 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="16c94-165">**사용 현황 데이터** 분석 보고서를 만드는 데 사용 되는 **포함 되어 있지 않으면** hello 백업에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="16c94-166">사용 하 여 [Azure API 관리 REST API] [ Azure API Management REST API] tooperiodically 보관을 위한 분석 보고서를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="16c94-167">hello 주파수 서비스 백업을 수행 된 복구 지점 목표에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="16c94-168">것이 좋습니다 정기 백업 미 실시 구현으로 요청 시 백업 후 중요 한 toominimize tooyour API 관리 서비스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="16c94-169">**변경 내용을** 만들어 놓은 toohello 서비스 구성 (예:: Api, 정책, 개발자 포털 모양) 백업 작업 동안 진행 중인 **hello 백업에 포함 될 수 있습니다 및 손실 될 됩니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="16c94-170"><a name="step2"> </a>API 관리 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="16c94-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="16c94-171">toorestore 이전에 만든된 백업에서 API 관리 서비스는 hello 다음 HTTP 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="16c94-172">설명:</span><span class="sxs-lookup"><span data-stu-id="16c94-172">where:</span></span>

* <span data-ttu-id="16c94-173">`subscriptionId`-으로 백업을 복원 하는 hello API 관리 서비스를 포함 하는 hello 구독의 id</span><span class="sxs-lookup"><span data-stu-id="16c94-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="16c94-174">`resourceGroupName`-hello 'Api 기본-{서비스 영역을 (를)' 형태의 문자열로 여기서 `service-region` 예를 들어 hello Azure 지역 hello에 백업을 복원 하는 API 관리 서비스의 호스팅 위치를 식별`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="16c94-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="16c94-175">`serviceName`-hello hello 해당 생성 시에 복원 되 고 서비스를 지정 하는 API 관리의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="16c94-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="16c94-176">`api-version` - `2014-02-14`(으)로 대체</span><span class="sxs-lookup"><span data-stu-id="16c94-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="16c94-177">Hello hello 요청 본문을 Azure 저장소 계정 이름, 액세스 키, blob 컨테이너 이름 및 백업 이름, 즉 hello 백업 파일 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="16c94-178">Hello의 hello 값 설정 `Content-Type` 요청 헤더에 너무`application/json`합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="16c94-179">복원은은 too30 또는 더 많은 분 toocomplete 차지 하는 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="16c94-180">Hello 요청이 성공 하 고 hello 복원 프로세스가 시작 된 경우 받을 수는 `202 Accepted` 와 응답 상태 코드는 `Location` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="16c94-181">'GET' hello에 toohello URL을 요청 확인 `Location` 헤더 toofind hello 작업의 hello 상태 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="16c94-182">Hello 복원이 진행 중인 동안 tooreceive '202 수락 됨' 상태 코드는 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="16c94-183">응답 코드가 `200 OK` hello 복원 작업이 성공적으로 완료를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16c94-184">**hello SKU** hello 서비스를 복원 중인 **일치 해야** hello hello의 SKU가 복원 되는 서비스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="16c94-185">**변경 내용을** 만들어 놓은 toohello 서비스 구성 (예:: Api, 정책, 개발자 포털 모양) 복원 작업 동안 진행 중인 **덮어쓰게**합니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="16c94-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16c94-186">Next steps</span></span>
<span data-ttu-id="16c94-187">Microsoft 블로그 hello 백업/복원 프로세스의 서로 다른 두 연습에 대 한 다음 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="16c94-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="16c94-188">Azure API 관리 계정 복제</span><span class="sxs-lookup"><span data-stu-id="16c94-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="16c94-189">그녀의 기여도 toothis 아티클의 tooGisela 감사 드립니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="16c94-190">Azure API 관리: 백업 및 복원 구성</span><span class="sxs-lookup"><span data-stu-id="16c94-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="16c94-191">자세한 Stuart 별로 hello 접근 방식을 hello 공식 지침에 맞지 않는 하지만 매우 흥미로운 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="16c94-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
