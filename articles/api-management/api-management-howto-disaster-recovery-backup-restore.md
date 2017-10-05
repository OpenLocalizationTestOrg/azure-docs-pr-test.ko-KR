---
title: "Azure API Management에서 백업 및 복원을 사용하여 재해 복구 구현 | Microsoft Docs"
description: "Azure API 관리에서 백업 및 복원을 사용하여 재해 복구를 수행하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="6145b-103">Azure API 관리에서 서비스 백업 및 복원을 사용하여 재해 복구를 구현하는 방법</span><span class="sxs-lookup"><span data-stu-id="6145b-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="6145b-104">Azure API 관리를 통해 API를 게시 및 관리하면 기존에는 직접 디자인, 구현 및 관리해야 했던 대부분의 내결함성 및 인프라 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="6145b-105">Azure 플랫폼은 매우 적은 비용으로 상당한 잠재적 오류를 완화합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="6145b-106">API 관리 서비스를 호스트하는 지역에 영향을 주는 가용성 문제로부터 서비스를 복구하려면 언제든지 다른 지역에서 서비스를 다시 구축할 준비가 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="6145b-107">가용성 목표와 복구 시간 목표에 따라서는 하나 이상의 지역에서 백업 서비스를 예약하고 해당 구성과 콘텐츠를 활성 서비스와 동기화 상태로 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="6145b-108">서비스 백업 및 복원 기능은 재해 복구 전략을 구현하는 데 필요한 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="6145b-109">이 가이드에서는 Azure 리소스 관리자 요청을 인증하는 방법과 API 관리 서비스 인스턴스를 백업 및 복원하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="6145b-110">재해 복구를 위한 API 관리 서비스 인스턴스를 백업 및 복원하는 프로세스는 스테이징과 같은 시나리오에 대한 API 관리 서비스 인스턴스를 복제하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="6145b-111">각 백업은 30일 후 만료되니 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="6145b-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="6145b-112">30일의 만료 기간이 만료된 후 백업을 복원하려고 하면 `Cannot restore: backup expired` 메시지와 함께 복원이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="6145b-113">Azure 리소스 관리자 요청 인증</span><span class="sxs-lookup"><span data-stu-id="6145b-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6145b-114">백업 및 복원을 위한 REST API는 Azure 리소스 관리자를 사용하며 API 관리 엔터티를 관리하기 위한 REST API와는 다른 인증 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="6145b-115">이 섹션의 단계에는 Azure 리소스 관리자 요청을 인증하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="6145b-116">자세한 내용은 [Azure 리소스 관리자 요청 인증](http://msdn.microsoft.com/library/azure/dn790557.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6145b-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="6145b-117">Azure 리소스 관리자를 사용하여 리소스에서 수행하는 모든 작업은 다음 단계를 사용하여 Azure Active Directory에서 인증되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="6145b-118">응용 프로그램을 Azure Active Directory 테넌트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="6145b-119">추가한 응용 프로그램에 대한 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="6145b-120">Azure 리소스 관리자에 대한 요청을 인증하기 위한 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="6145b-121">첫 번째 단계는 Azure Active Directory 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="6145b-122">API 관리 서비스 인스턴스를 포함하는 구독을 사용하여 [Azure 클래식 포털](http://manage.windowsazure.com/) 에 로그인하고 기본 Azure Active Directory에 대한 **응용 프로그램** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="6145b-123">Azure Active Directory 기본 디렉토리에 사용자의 계정이 표시되지 않는 경우, 계정에 필요한 사용 권한을 부여하려면 Azure 구독의 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6145b-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Azure Active Directory 응용 프로그램 만들기][api-management-add-aad-application]

<span data-ttu-id="6145b-125">**추가**, **조직에서 개발 중인 응용 프로그램 추가**를 선택하고 **네이티브 클라이언트 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="6145b-126">설명하는 이름을 입력하고 다음 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="6145b-127">**리디렉션 URI**로 `http://resources`와 같은 자리 표시자 URL을 입력하고, 필수 필드지만 값은 나중에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="6145b-128">응용 프로그램을 저장하려면 이 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-128">Click the check box to save the application.</span></span>

<span data-ttu-id="6145b-129">응용 프로그램이 저장되면, **구성**을 클릭하고 **다른 응용 프로그램에 권한 추가** 섹션을 아래로 스크롤하고 **응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![권한 추가][api-management-aad-permissions-add]

<span data-ttu-id="6145b-131">**Windows** **Azure Service Management API**를 선택하고 이 확인란을 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![권한 추가][api-management-aad-permissions]

<span data-ttu-id="6145b-133">새로 추가된 **Windows****Azure Service Management API** 응용 프로그램 확인란 옆의 **위임된 권한**을 클릭하고 **Azure 서비스 관리 액세스(미리 보기)**의 상자를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![권한 추가][api-management-aad-delegated-permissions]

<span data-ttu-id="6145b-135">백업 및 복원을 생성하는 API를 호출하기 전에 토큰을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="6145b-136">다음 예제는 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget 패키지를 사용하여 토큰을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="6145b-137">다음 지침을 사용하여 `{tentand id}`, `{application id}` 및 `{redirect uri}`을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="6145b-138">`{tenant id}` 를 방금 만든 Azure Active Directory 응용 프로그램의 테넌트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="6145b-139">**끝점 보기**를 클릭하여 ID에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-139">You can access the id by clicking **View endpoints**.</span></span>

![끝점][api-management-aad-default-directory]

![끝점][api-management-endpoint]

<span data-ttu-id="6145b-142">Azure Active Directory 응용 프로그램의 **구성** 탭의 **리디렉션 Uri** 섹션에서 **클라이언트 ID** 및 URL을 사용하여 `{application id}` 및 `{redirect uri}`를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![리소스][api-management-aad-resources]

<span data-ttu-id="6145b-144">값이 지정되면 코드 예제에서는 다음 예와 유사한 토큰을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![위임][api-management-arm-token]

<span data-ttu-id="6145b-146">다음 섹션에서 설명하는 백업 및 복원 작업을 호출하기 전에, REST 호출에 대한 권한 부여 요청 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="6145b-147"><a name="step1"> </a>API Management 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="6145b-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="6145b-148">API Management 서비스를 백업하려면 다음 HTTP 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="6145b-149">설명:</span><span class="sxs-lookup"><span data-stu-id="6145b-149">where:</span></span>

* <span data-ttu-id="6145b-150">`subscriptionId` - 백업할 API 관리 서비스를 포함하는 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="6145b-151">`resourceGroupName` - 'Api-Default-{service-region}' 형식의 문자열입니다. 여기서 `service-region`은 백업할 API 관리 서비스가 호스트되는 Azure 지역(예: `North-Central-US`)을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="6145b-152">`serviceName` - 백업을 만드는 API 관리 서비스를 만들 때 지정하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="6145b-153">`api-version` - `2014-02-14`(으)로 대체</span><span class="sxs-lookup"><span data-stu-id="6145b-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="6145b-154">요청 본문에서 대상 Azure 저장소 계정 이름, 액세스 키, Blob 컨테이너 이름 및 백업 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="6145b-155">`Content-Type` 요청 헤더의 값을 `application/json`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="6145b-156">백업은 오랫동안 실행되는 작업으로, 완료되려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="6145b-157">요청이 정상적으로 실행되어 백업 프로세스가 시작되면 `Location` 헤더가 포함된 `202 Accepted` 응답 상태 코드를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="6145b-158">`Location` 헤더에서 URL에 대한 'GET' 요청을 수행하면 작업 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="6145b-159">백업이 진행 중인 동안에는 '202 수락됨' 상태 코드가 계속 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="6145b-160">응답 코드가 `200 OK` 이면 백업 작업이 정상적으로 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="6145b-161">백업 요청을 수행할 때는 다음의 제약 조건을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6145b-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="6145b-162">요청 본문에 지정된 **Container**가 **있어야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="6145b-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="6145b-163">백업이 진행 중인 동안에는 SKU 업그레이드/다운그레이드, 도메인 이름 변경 등의 **서비스 관리 작업을 수행하면 안 됩니다** .</span><span class="sxs-lookup"><span data-stu-id="6145b-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="6145b-164">백업 복원은 생성 시점부터 **30일 동안만 보장**됩니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="6145b-165">분석 보고서를 만드는 데 사용되는 **사용 현황 데이터**는 백업에 **포함되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="6145b-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="6145b-166">[Azure API Management REST API][Azure API Management REST API] 를 사용하여 분석 보고서를 주기적으로 검색한 다음 안전하게 보관하세요.</span><span class="sxs-lookup"><span data-stu-id="6145b-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="6145b-167">서비스 백업을 수행하는 빈도는 복구 지점 목표에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="6145b-168">영향을 최소화하려면 정기 백업을 구현함과 동시에 API 관리 서비스에 대한 중요 변경을 수행한 후 요청 시 백업도 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="6145b-169">백업 작업이 진행되는 동안 API, 정책, 개발자 포털 모양 등의 서비스 구성을 **변경**하는 경우 **해당 내용이 백업에 포함되지 않아 손실될 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6145b-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="6145b-170"><a name="step2"> </a>API 관리 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="6145b-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="6145b-171">이전에 만든 백업에서 API 관리 서비스를 복원하려면 다음 HTTP 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="6145b-172">설명:</span><span class="sxs-lookup"><span data-stu-id="6145b-172">where:</span></span>

* <span data-ttu-id="6145b-173">`subscriptionId` - 백업을 복원할 API 관리 서비스를 포함하는 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="6145b-174">`resourceGroupName` - 'Api-Default-{service-region}' 형식의 문자열입니다. 여기서 `service-region`은 백업을 복원할 API 관리 서비스가 호스트되는 Azure 지역(예: `North-Central-US`)을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="6145b-175">`serviceName` - 백업을 복원할 API 관리 서비스를 만들 때 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="6145b-176">`api-version` - `2014-02-14`(으)로 대체</span><span class="sxs-lookup"><span data-stu-id="6145b-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="6145b-177">요청 본문에서 백업 파일 위치(Azure 저장소 계정 이름, 액세스 키, Blob 컨테이너 이름 및 백업 이름)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="6145b-178">`Content-Type` 요청 헤더의 값을 `application/json`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="6145b-179">복원은 오랫동안 실행되는 작업으로, 완료되려면 30분 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="6145b-180">요청이 정상적으로 실행되어 복원 프로세스가 시작되면 `Location` 헤더가 포함된 `202 Accepted` 응답 상태 코드를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="6145b-181">`Location` 헤더에서 URL에 대한 'GET' 요청을 수행하면 작업 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="6145b-182">복원이 진행 중인 동안에는 '202 수락됨' 상태 코드가 계속 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="6145b-183">응답 코드가 `200 OK` 이면 복원 작업이 정상적으로 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6145b-184">백업을 복원할 서비스의 **SKU**는 복원하려는 백업된 서비스의 SKU와 **일치**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="6145b-185">복원 작업이 진행되는 동안 API, 정책, 개발자 포털 모양 등의 서비스 구성에 적용된 **변경 내용**을 **덮어쓸 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6145b-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6145b-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6145b-186">Next steps</span></span>
<span data-ttu-id="6145b-187">백업/복원 프로세스의 서로 다른 두 연습에 대한 다음 Microsoft 블로그를 체크아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="6145b-188">Azure API 관리 계정 복제</span><span class="sxs-lookup"><span data-stu-id="6145b-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="6145b-189">이 문서를 작성 하는 데 도움을 주신 Gisela에게 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="6145b-190">Azure API 관리: 백업 및 복원 구성</span><span class="sxs-lookup"><span data-stu-id="6145b-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="6145b-191">Stuart에서 구체화된 접근 방식은 공식 지침과 일치하지 않지만 매우 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="6145b-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
