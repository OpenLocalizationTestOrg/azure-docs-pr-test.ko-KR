---
title: "Azure 로그 분석에서 aaaPython 스크립트 tooretrieve 데이터 | Microsoft Docs"
description: "hello 로그 분석 로그 검색 API는 REST API 클라이언트 로그 분석 작업 영역에서 tooretrieve 데이터를 수 있습니다.  이 문서에서는 hello 로그 검색 API를 사용 하는 샘플 Python 스크립트를 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: bwren
ms.openlocfilehash: a45693b04cd388301b859e7186ca671786d0229e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a><span data-ttu-id="6ef63-104">Python 스크립트로 Log Analytics에서 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="6ef63-104">Retrieve data from Log Analytics with a Python script</span></span>
<span data-ttu-id="6ef63-105">hello [로그 분석 로그 검색 API](log-analytics-log-search-api.md) tooretrieve 데이터 로그 분석 작업 영역에서 모든 REST API 클라이언트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-105">hello [Log Analytics Log Search API](log-analytics-log-search-api.md) allows any REST API client tooretrieve data from a Log Analytics workspace.</span></span>  <span data-ttu-id="6ef63-106">이 문서에서는 hello 로그 분석 로그 검색 API를 사용 하는 샘플 Python 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-106">This article presents a sample Python script that uses hello Log Analytics Log Search API.</span></span>  

## <a name="authentication"></a><span data-ttu-id="6ef63-107">인증</span><span class="sxs-lookup"><span data-stu-id="6ef63-107">Authentication</span></span>
<span data-ttu-id="6ef63-108">이 스크립트는 Azure Active Directory tooauthenticate toohello 작업 영역에서 서비스 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-108">This script uses a service principal in Azure Active Directory tooauthenticate toohello workspace.</span></span>  <span data-ttu-id="6ef63-109">서비스 사용자는 클라이언트 허용 hello 서비스 응용 프로그램 toorequest hello 클라이언트 hello 계정 이름이 없는 경우에 계정을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-109">Service principals allow a client application toorequest that hello service authenticate an account even if hello client does not have hello account name.</span></span> <span data-ttu-id="6ef63-110">Hello에서이 프로세스를 사용 하 여 서비스 사용자를이 스크립트를 실행 하기 전에 만들어야 [포털 toocreate를 사용 하 여 Azure Active Directory 응용 프로그램 및 서비스 사용자 리소스에 액세스할 수 있는](../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-110">Before running this script, you must create a service principal using hello process at [Use portal toocreate an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>  <span data-ttu-id="6ef63-111">Tooprovide hello 응용 프로그램 ID, 테 넌 트 ID 및 인증 키 toohello 스크립트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-111">You'll need tooprovide hello Application ID, Tenant ID, and Authentication Key toohello script.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ef63-112">때 있습니다 [Azure 자동화 계정 만들기](../automation/automation-create-standalone-account.md), 서비스 사용자 만들어집니다 즉 적합 한 toouse이이 스크립트와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-112">When you [create an Azure Automation account](../automation/automation-create-standalone-account.md), a service principal is created that is suitable toouse with this script.</span></span>  <span data-ttu-id="6ef63-113">Azure 자동화에서 만든 서비스 사용자를 이미 있는 경우 수 toouse 있어야 너무 할 수 있지만 새 대시보드를 만드는 대신 해당[인증 키를 만들고](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) 이미 되어 있지 않을 경우.</span><span class="sxs-lookup"><span data-stu-id="6ef63-113">If you already have a service principal created by Azure Automation then you should be able toouse it instead of creating a new one, although you may need too[create an authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) if it doesn't already have one.</span></span>

## <a name="script"></a><span data-ttu-id="6ef63-114">스크립트</span><span class="sxs-lookup"><span data-stu-id="6ef63-114">Script</span></span>
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these tooyour requirements.
query = "Type=Event"
end_time = datetime.datetime.utcnow()
start_time = end_time - datetime.timedelta(hours=24)
num_results = 100  # If not provided, a default of 10 results will be used.

# IDs for authentication.  Fill in values for your service principal.
subscription_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
tenant_id = 'xxxxxxxx-xxxx-xxxx-xxx-xxxxxxxxxxxx'
application_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx'
application_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

# URLs for authentication
authentication_endpoint = 'https://login.microsoftonline.com/'
resource  = 'https://management.core.windows.net/'

# Get access token
context = adal.AuthenticationContext('https://login.microsoftonline.com/' + tenant_id)
token_response = context.acquire_token_with_client_credentials('https://management.core.windows.net/', application_id, application_key)
access_token = token_response.get('accessToken')

# Add token tooheader
headers = {
    "Authorization": 'Bearer ' + access_token,
    "Content-Type":'application/json'
}

# URLs for retrieving data
uri_base = 'https://management.azure.com'
uri_api = 'api-version=2015-11-01-preview'
uri_subscription = 'https://management.azure.com/subscriptions/' + subscription_id
uri_resourcegroup = uri_subscription + '/resourcegroups/'+ resource_group
uri_workspace = uri_resourcegroup + '/providers/Microsoft.OperationalInsights/workspaces/' + workspace
uri_search = uri_workspace + '/search'

# Build search parameters from query details
search_params = {
        "query": query,
        "top": num_results,
        "start": start_time.strftime('%Y-%m-%dT%H:%M:%S'),
        "end": end_time.strftime('%Y-%m-%dT%H:%M:%S')
        }

# Build URL and send post request
uri = uri_search + '?' + uri_api
response = requests.post(uri,json=search_params,headers=headers)

# Response of 200 if successful
if response.status_code == 200:

    # Parse hello response tooget hello ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL tooget search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse hello response tooget hello status
        data = response.json()
        status = data["__metadata"]["Status"]

else:

    # Request failed
    print (response.status_code)
    response.raise_for_status()

print ("Total records:" + str(data["__metadata"]["total"]))
print ("Returned top:" + str(data["__metadata"]["top"]))
pprint (data["value"])
```
## <a name="next-steps"></a><span data-ttu-id="6ef63-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ef63-115">Next steps</span></span>
- <span data-ttu-id="6ef63-116">Hello에 대 한 자세한 [로그 분석 로그 검색 API](log-analytics-log-search-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef63-116">Learn more about hello [Log Analytics Log Search API](log-analytics-log-search-api.md).</span></span>
