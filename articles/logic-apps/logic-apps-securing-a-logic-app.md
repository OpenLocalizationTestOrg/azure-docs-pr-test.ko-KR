---
title: "Azure Logic Apps에 대한 액세스 보호 | Microsoft Docs"
description: "Azure Logic Apps에서 워크플로와 함께 사용되는 트리거, 입력 및 출력, 작업 매개 변수 및 서비스에 대한 액세스를 보호하기 위한 보안을 추가합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="3807c-103">논리 앱에 대한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="3807c-103">Secure access to your logic apps</span></span>

<span data-ttu-id="3807c-104">논리 앱을 보호하는 데 사용할 수 있는 많은 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="3807c-105">논리 앱(HTTP 요청 트리거)을 트리거하는 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="3807c-106">논리 앱을 관리, 편집 또는 읽기 위한 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="3807c-107">실행에 대한 입력 및 출력의 콘텐츠에 대한 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="3807c-108">워크플로에서 작업 내에서 매개 변수 또는 입력 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="3807c-109">워크플로에서 요청을 수신하는 서비스에 대한 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="3807c-110">트리거에 대한 보안 액세스</span><span class="sxs-lookup"><span data-stu-id="3807c-110">Secure access to trigger</span></span>

<span data-ttu-id="3807c-111">HTTP 요청([요청](../connectors/connectors-native-reqres.md) 또는 [WebHook](../connectors/connectors-native-webhook.md))을 발생시키는 논리 앱으로 작업하는 경우, 인증된 클라이언트만 논리 앱을 발생시킬 수 있도록 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="3807c-112">논리 앱에 대한 모든 요청은 SSL을 통해 암호화되고 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="3807c-113">공유 액세스 서명</span><span class="sxs-lookup"><span data-stu-id="3807c-113">Shared Access Signature</span></span>

<span data-ttu-id="3807c-114">논리 앱에 대한 모든 요청 끝점은 URL의 일부로서 [SAS(공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md))를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="3807c-115">각 URL은 `sp`, `sv` 및 `sig` 쿼리 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="3807c-116">권한은 `sp`에 의해 지정되고 허용된 HTTP 메서드에 해당하며, `sv`는 생성하는 데 사용된 버전이며, `sig`는 트리거하는 액세스를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="3807c-117">서명은 모든 URL 경로 및 속성에 관한 암호 키를 포함한 SHA256 알고리즘을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="3807c-118">비밀 키 암호는 절대 노출되거나 공개되지 않으며 논리 앱의 일부로서 암호화되고 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="3807c-119">논리 앱은 암호 키로 만들어진 유효한 서명을 포함하는 트리거에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="3807c-120">액세스 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="3807c-120">Regenerate access keys</span></span>

<span data-ttu-id="3807c-121">REST API 또는 Azure Portal을 통해 언제든지 새 보안 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="3807c-122">이전 키를 사용하여 이전에 생성된 모든 현재 URL은 무효화되고 논리 앱을 실행하는 데 권한이 더 이상 부여되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="3807c-123">Azure Portal에서 논리 앱을 열어 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="3807c-124">**설정** 아래에 있는 **액세스 키** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="3807c-125">다시 생성할 키를 선택하고 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="3807c-126">다시 생성한 후 검색한 URL은 새 액세스 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="3807c-127">만료 날짜가 있는 콜백 URL 만들기</span><span class="sxs-lookup"><span data-stu-id="3807c-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="3807c-128">다른 상대방과 URL을 공유하는 경우 필요에 따라 특정 키와 만료 날짜로 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="3807c-129">그러면 원활하게 키를 배포하거나 특정 시간대에 앱 실행 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="3807c-130">다음과 같이 [논리 앱 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers)를 통해 URL의 만료 날짜를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="3807c-131">본문에서는 속성 `NotAfter`를 `NotAfter` 날짜 및 시간까지만 유효한 콜백 URL을 반환하는 JSON 날짜 문자열로서 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="3807c-132">기본 또는 보조 비밀 키로 URL 만들기</span><span class="sxs-lookup"><span data-stu-id="3807c-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="3807c-133">요청 기반 트리거에 대한 콜백 URL을 생성하거나 나열하면, URL을 서명하기 위해 사용할 키를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="3807c-134">다음과 같이 [논리 앱 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers)을 통해 특정 키로 서명된 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="3807c-135">본문에서는 속성 `KeyType`을 `Primary` 또는 `Secondary`로서 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="3807c-136">이는 지정된 보안 키로 서명된 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="3807c-137">받는 IP 주소 제한</span><span class="sxs-lookup"><span data-stu-id="3807c-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="3807c-138">공유 액세스 서명 외에도 특정 클라이언트의 논리 앱 호출만 제한하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="3807c-139">예를 들어 Azure API Management를 통해 끝점을 관리하는 경우 API Management 인스턴스 IP 주소에서 요청이 들어오면 요청을 수락하도록 논리 앱을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="3807c-140">이 설정은 논리 앱 설정 내에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="3807c-141">Azure Portal에서 IP 주소 제한을 추가하려는 논리 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="3807c-142">**설정** 아래에 있는 **액세스 제어 구성** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="3807c-143">트리거에 의해 허용되는 IP 주소 범위 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="3807c-144">유효한 IP 범위 형식은 `192.168.1.1/255`입니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="3807c-145">논리 앱을 중첩된 논리 앱으로서 실행하려는 경우 **다른 논리 앱만** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="3807c-146">이 옵션은 빈 배열을 리소스에 작성할 수 있으며, 이는 서비스 자체(부모 논리 앱)의 호출만 성공적으로 실행된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="3807c-147">요청 트리거가 있는 논리 앱은 IP에 관계 없이 REST API/Management `/triggers/{triggerName}/run`을 통해 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="3807c-148">이 시나리오에는 Azure REST API에 대한 인증이 필요하며 모든 이벤트는 Azure Audit Log에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="3807c-149">그에 따라 액세스 제어 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="3807c-150">리소스 정의에서 IP 범위 설정</span><span class="sxs-lookup"><span data-stu-id="3807c-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="3807c-151">배포를 자동화하기 위해 [배포 템플릿](logic-apps-create-deploy-template.md)을 사용하는 경우 리소스 템플릿에서 IP 범위 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="3807c-152">Azure Active Directory, OAuth 또는 기타 보안 추가</span><span class="sxs-lookup"><span data-stu-id="3807c-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="3807c-153">논리 앱을 기반으로 권한 부여 프로토콜을 추가하기 위해 [Azure API Management](https://azure.microsoft.com/services/api-management/)에서는 논리 앱을 API로 노출하는 기능을 사용하여 모든 끝점에 대한 다양한 모니터링, 보안, 정책 및 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="3807c-154">Azure API Management는 Azure Active Directory, 인증서, OAuth 또는 기타 보안 표준을 사용할 수 있는 논리 앱에 대한 공용 또는 개인 끝점을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="3807c-155">요청을 받으면 Azure API Management는 해당 요청을 논리 앱에 전달합니다(필요한 모든 변환 또는 진행 중인 제한 수행).</span><span class="sxs-lookup"><span data-stu-id="3807c-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="3807c-156">API Management에서만 논리 앱이 트리거되도록 논리 앱에서 받는 IP 범위 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="3807c-157">논리 앱을 관리하거나 편집하기 위한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="3807c-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="3807c-158">특정 사용자 또는 그룹만 리소스에서 작업을 수행할 수 있도록 논리 앱에서 관리 작업을 위한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="3807c-159">논리 앱은 Azure [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md) 기능을 사용하고 동일한 도구로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="3807c-160">또한 구독 구성원들에게 할당할 수 있는 몇 가지 기본 제공 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="3807c-161">**논리 앱 참가자** - 논리 앱을 보고, 편집하고 업데이트하기 위한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="3807c-162">리소스를 제거하거나 관리 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="3807c-163">**논리 앱 연산자** - 논리 앱과 실행 기록을 보고 활성화/비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="3807c-164">정의를 편집하거나 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="3807c-165">[Azure 리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md)을 사용하여 논리 앱을 변경하거나 삭제하지 않도록 방지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="3807c-166">이 기능은 프로덕션 리소스가 변경되거나 삭제되는 것을 방지하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="3807c-167">실행 기록 콘텐츠에 대한 보안 액세스</span><span class="sxs-lookup"><span data-stu-id="3807c-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="3807c-168">이전 실행에서 특정 IP 주소 범위까지 입력 또는 출력 콘텐츠에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="3807c-169">워크플로 실행 내에 있는 모든 데이터는 전송 중 그리고 미사용 시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="3807c-170">실행 기록을 호출하면 서비스가 요청을 인증하고 요청 및 응답 입출력에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="3807c-171">지정된 IP 주소 범위에서 콘텐츠를 보기 위한 요청만 콘텐츠를 반환하도록 하여 이 링크를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="3807c-172">추가 액세스 제어를 위해 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="3807c-173">누구도 입/출력에 액세스할 수 없도록 `0.0.0.0`과 같이 IP 주소를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="3807c-174">관리자 권한을 가진 사용자만 이러한 제한을 제거하여 워크플로 콘텐츠에 'Just-In-Time' 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="3807c-175">Azure Portal의 리소스 설정 내에서 이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="3807c-176">Azure Portal에서 IP 주소 제한을 추가하려는 논리 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="3807c-177">**설정** 아래에 있는 **액세스 제어 구성** 메뉴 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="3807c-178">콘텐츠에 액세스하기 위해 IP 주소 범위 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="3807c-179">리소스 정의에서 IP 범위 설정</span><span class="sxs-lookup"><span data-stu-id="3807c-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="3807c-180">배포를 자동화하기 위해 [배포 템플릿](logic-apps-create-deploy-template.md)을 사용하는 경우 리소스 템플릿에서 IP 범위 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="3807c-181">워크플로 내에서 매개 변수 및 입력 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="3807c-182">환경에 배포하기 위해 워크플로 정의의 몇 가지 측면을 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="3807c-183">또한 일부 매개 변수는 워크플로 편집 시 표시하지 않으려는 보안 매개 변수일 수 있습니다. 예를 들어, HTTP 작업의 [Azure Active Directory 인증](../connectors/connectors-native-http.md#authentication)에 대한 클라이언트 ID 및 클라이언트 암호 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="3807c-184">매개 변수 및 보안 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="3807c-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="3807c-185">런타임 시 리소스 매개 변수의 값에 액세스하기 위해 [워크플로 정의 언어](http://aka.ms/logicappsdocs)는 `@parameters()` 연산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="3807c-186">또한 [리소스 배포 템플릿에서 매개 변수를 지정](../azure-resource-manager/resource-group-authoring-templates.md#parameters)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="3807c-187">하지만 매개 변수 형식을 `securestring`로 지정하면 해당 매개 변수는 리소스 정의의 나머지를 반환하지 않고 배포 후에 리소스를 확인하여 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="3807c-188">요청의 머리글이나 본문에 매개 변수를 사용하는 경우 해당 매개 변수에서는 실행 기록과 나가는 HTTP 요청에 액세스하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="3807c-189">해당하는 콘텐츠 액세스 정책을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="3807c-190">권한 부여 헤더는 입력 또는 출력을 통해 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="3807c-191">여기에서 암호를 사용하는 경우 암호를 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="3807c-192">암호가 있는 리소스 배포 템플릿</span><span class="sxs-lookup"><span data-stu-id="3807c-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="3807c-193">다음 예제에서는 런타임 시 `secret`의 보안 매개 변수를 참조하는 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="3807c-194">별도 매개 변수 파일에서 `secret`에 대한 환경 값을 지정하거나 [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md)를 사용하여 배포 시 암호를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="3807c-195">워크플로에서 요청을 수신하는 서비스에 대한 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="3807c-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="3807c-196">논리 앱이 액세스해야 하는 모든 끝점을 보호하는 데는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="3807c-197">아웃바운드 요청에 대한 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3807c-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="3807c-198">HTTP, HTTP + Swagger(개방형 API) 또는 웹후크 동작으로 작업할 경우 전송되는 요청에 인증을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="3807c-199">추가할 수 있는 인증으로는 기본 인증, 인증서 인증 또는 Azure Active Directory 인증이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="3807c-200">이 인증을 구성하는 방법에 대한 자세한 내용은 [이 문서에서](../connectors/connectors-native-http.md#authentication) 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="3807c-201">논리 앱 IP 주소에 대한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="3807c-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="3807c-202">논리 앱의 모든 호출은 영역당 특정 IP 주소 집합에서 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="3807c-203">지정된 IP 주소의 요청만 수락하도록 필터링을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="3807c-204">해당 IP 주소의 목록은 [논리 앱 제한 및 구성](logic-apps-limits-and-config.md#configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3807c-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="3807c-205">온-프레미스 연결</span><span class="sxs-lookup"><span data-stu-id="3807c-205">On-premises connectivity</span></span>

<span data-ttu-id="3807c-206">논리 앱은 여러 서비스를 통합하여 안전하고 신뢰할 수 있는 온-프레미스 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="3807c-207">온-프레미스 데이터 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="3807c-207">On-premises data gateway</span></span>

<span data-ttu-id="3807c-208">논리 앱의 많은 관리형 커넥터는 파일 시스템, SQL, SharePoint, DB2 등의 온-프레미스 시스템에 보안 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="3807c-209">게이트웨이는 Azure Service Bus를 통해 암호화된 채널의 온-프레미스 원본에서 데이터를 릴레이합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="3807c-210">보안으로 시작하는 모든 트래픽은 게이트웨이 에이전트에서 트래픽을 아웃바운드합니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="3807c-211">[데이터 게이트웨이 작동 원리](logic-apps-gateway-install.md#gateway-cloud-service)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="3807c-212">Azure API 관리</span><span class="sxs-lookup"><span data-stu-id="3807c-212">Azure API Management</span></span>

<span data-ttu-id="3807c-213">[Azure API Management](https://azure.microsoft.com/services/api-management/)에는 보안 프록시를 위한 사이트 간 VPN 및 ExpressRoute 통합과 온-프레미스 시스템에 대한 통신 등 온-프레미스 연결 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="3807c-214">Logic App Designer에서 워크플로 내의 Azure API Management에서 노출되는 API를 빠르게 선택하여 온-프레미스 시스템에 빠르게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="3807c-215">Azure App Services의 하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="3807c-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="3807c-216">온-프레미스 통신을 위해 Azure API와 Web Apps용 온-프레미스 하이브리드 연결 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="3807c-217">하이브리드 연결 및 구성 방법에 대한 자세한 내용은 [이 문서에서](../app-service-web/web-sites-hybrid-connection-get-started.md) 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3807c-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3807c-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3807c-218">Next steps</span></span>
[<span data-ttu-id="3807c-219">배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="3807c-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="3807c-220">예외 처리</span><span class="sxs-lookup"><span data-stu-id="3807c-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="3807c-221">논리 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="3807c-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="3807c-222">논리 앱 오류 진단 및 문제</span><span class="sxs-lookup"><span data-stu-id="3807c-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
