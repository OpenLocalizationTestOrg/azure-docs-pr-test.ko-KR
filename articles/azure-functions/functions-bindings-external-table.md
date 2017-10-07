---
title: "aaaAzure 함수 외부 테이블 바인딩 (미리 보기) | Microsoft Docs"
description: "Azure Functions에서 외부 테이블 바인딩 사용"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="7d4ed-103">Azure Functions 외부 테이블 바인딩(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="7d4ed-104">이 문서에서는 어떻게 toomanipulate 테이블 형식 데이터를 SaaS 공급자 (예: Sharepoint, Dynamics) 기본 제공 바인딩 사용 하는 함수 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="7d4ed-105">Azure Functions는 외부 테이블에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="7d4ed-106">API 연결</span><span class="sxs-lookup"><span data-stu-id="7d4ed-106">API Connections</span></span>

<span data-ttu-id="7d4ed-107">테이블 바인딩 타사 SaaS 공급자와 외부 API 연결 tooauthenticate를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="7d4ed-108">바인딩을 할당할 때 새 API 연결을 만들 하거나 hello 내에서 기존 API 연결을 사용 하 여 동일한 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="7d4ed-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="7d4ed-109">지원되는 API 연결(테이블)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="7d4ed-110">커넥터</span><span class="sxs-lookup"><span data-stu-id="7d4ed-110">Connector</span></span>|<span data-ttu-id="7d4ed-111">트리거</span><span class="sxs-lookup"><span data-stu-id="7d4ed-111">Trigger</span></span>|<span data-ttu-id="7d4ed-112">입력</span><span class="sxs-lookup"><span data-stu-id="7d4ed-112">Input</span></span>|<span data-ttu-id="7d4ed-113">출력</span><span class="sxs-lookup"><span data-stu-id="7d4ed-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="7d4ed-114">DB2</span><span class="sxs-lookup"><span data-stu-id="7d4ed-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="7d4ed-115">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-115">x</span></span>|<span data-ttu-id="7d4ed-116">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-116">x</span></span>
|[<span data-ttu-id="7d4ed-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="7d4ed-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="7d4ed-118">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-118">x</span></span>|<span data-ttu-id="7d4ed-119">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-119">x</span></span>
|[<span data-ttu-id="7d4ed-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="7d4ed-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="7d4ed-121">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-121">x</span></span>|<span data-ttu-id="7d4ed-122">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-122">x</span></span>
|[<span data-ttu-id="7d4ed-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="7d4ed-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="7d4ed-124">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-124">x</span></span>|<span data-ttu-id="7d4ed-125">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-125">x</span></span>
|[<span data-ttu-id="7d4ed-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="7d4ed-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="7d4ed-127">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-127">x</span></span>|<span data-ttu-id="7d4ed-128">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-128">x</span></span>
|[<span data-ttu-id="7d4ed-129">Informix</span><span class="sxs-lookup"><span data-stu-id="7d4ed-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="7d4ed-130">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-130">x</span></span>|<span data-ttu-id="7d4ed-131">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-131">x</span></span>
|[<span data-ttu-id="7d4ed-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="7d4ed-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="7d4ed-133">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-133">x</span></span>|<span data-ttu-id="7d4ed-134">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-134">x</span></span>
|[<span data-ttu-id="7d4ed-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="7d4ed-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="7d4ed-136">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-136">x</span></span>|<span data-ttu-id="7d4ed-137">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-137">x</span></span>
|[<span data-ttu-id="7d4ed-138">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7d4ed-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="7d4ed-139">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-139">x</span></span>|<span data-ttu-id="7d4ed-140">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-140">x</span></span>
|[<span data-ttu-id="7d4ed-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="7d4ed-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="7d4ed-142">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-142">x</span></span>|<span data-ttu-id="7d4ed-143">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-143">x</span></span>
|[<span data-ttu-id="7d4ed-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="7d4ed-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="7d4ed-145">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-145">x</span></span>|<span data-ttu-id="7d4ed-146">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-146">x</span></span>
|[<span data-ttu-id="7d4ed-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d4ed-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="7d4ed-148">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-148">x</span></span>|<span data-ttu-id="7d4ed-149">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-149">x</span></span>
|[<span data-ttu-id="7d4ed-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7d4ed-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="7d4ed-151">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-151">x</span></span>|<span data-ttu-id="7d4ed-152">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-152">x</span></span>
|[<span data-ttu-id="7d4ed-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="7d4ed-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="7d4ed-154">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-154">x</span></span>|<span data-ttu-id="7d4ed-155">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-155">x</span></span>
|<span data-ttu-id="7d4ed-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="7d4ed-156">UserVoice</span></span>||<span data-ttu-id="7d4ed-157">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-157">x</span></span>|<span data-ttu-id="7d4ed-158">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-158">x</span></span>
|<span data-ttu-id="7d4ed-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="7d4ed-159">Zendesk</span></span>||<span data-ttu-id="7d4ed-160">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-160">x</span></span>|<span data-ttu-id="7d4ed-161">x</span><span class="sxs-lookup"><span data-stu-id="7d4ed-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="7d4ed-162">외부 테이블 연결은 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)에서도 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="7d4ed-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="7d4ed-163">API 연결 만들기: 단계별 방법</span><span class="sxs-lookup"><span data-stu-id="7d4ed-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="7d4ed-164">함수 만들기 > 사용자 지정 함수 ![사용자 지정 함수 만들기](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="7d4ed-165">시나리오 `Experimental` > `ExternalTable-CSharp` 템플릿 > 새 `External Table connection` 만들기
![테이블 입력 템플릿 선택](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="7d4ed-166">SaaS 공급자 선택 > 연결 선택/만들기 ![SaaS 연결 구성](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="7d4ed-167">API 연결을 선택 > hello 함수를 만들 ![테이블 함수 만들기](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="7d4ed-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="7d4ed-168">`Integrate` > `External Table` 선택</span><span class="sxs-lookup"><span data-stu-id="7d4ed-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="7d4ed-169">Hello 연결 toouse 대상 테이블을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="7d4ed-170">이러한 설정은 SaaS 공급자마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="7d4ed-171">이 내용은 아래 [데이터 원본 설정](#datasourcesettings)
![테이블 구성](./media/functions-bindings-storage-table/configure-API-connection.jpg)에서 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="7d4ed-172">사용</span><span class="sxs-lookup"><span data-stu-id="7d4ed-172">Usage</span></span>

<span data-ttu-id="7d4ed-173">이 예에서는 Id, LastName 및 FirstName 열과 "Contact" 라는 tooa 테이블을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="7d4ed-174">로그 이름과 성을 hello 및 hello 코드 hello 테이블의 hello 연락처 엔터티를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="7d4ed-175">바인딩</span><span class="sxs-lookup"><span data-stu-id="7d4ed-175">Bindings</span></span>
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
<span data-ttu-id="7d4ed-176">`entityId`는 테이블 바인딩을 위해 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="7d4ed-177">`ConnectionAppSettingsKey`hello API 연결 문자열을 저장 하는 hello 응용 프로그램 설정을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="7d4ed-178">hello 응용 프로그램 설정을 자동으로 생성 됩니다는 API를 추가 하면 UI를 통합 하는 hello에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="7d4ed-179">테이블 형식 커넥터는 데이터 집합을 제공하며 각 데이터 집합은 테이블을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="7d4ed-180">hello hello 기본 데이터 집합 이름은 "default"입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="7d4ed-181">데이터 집합 및 다양 한 SaaS 공급자의 테이블에 대 한 hello 타이틀은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="7d4ed-182">커넥터</span><span class="sxs-lookup"><span data-stu-id="7d4ed-182">Connector</span></span>|<span data-ttu-id="7d4ed-183">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="7d4ed-183">Dataset</span></span>|<span data-ttu-id="7d4ed-184">테이블</span><span class="sxs-lookup"><span data-stu-id="7d4ed-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="7d4ed-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="7d4ed-185">**SharePoint**</span></span>|<span data-ttu-id="7d4ed-186">사이트</span><span class="sxs-lookup"><span data-stu-id="7d4ed-186">Site</span></span>|<span data-ttu-id="7d4ed-187">SharePoint 목록</span><span class="sxs-lookup"><span data-stu-id="7d4ed-187">SharePoint List</span></span>
|<span data-ttu-id="7d4ed-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="7d4ed-188">**SQL**</span></span>|<span data-ttu-id="7d4ed-189">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7d4ed-189">Database</span></span>|<span data-ttu-id="7d4ed-190">테이블</span><span class="sxs-lookup"><span data-stu-id="7d4ed-190">Table</span></span> 
|<span data-ttu-id="7d4ed-191">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="7d4ed-191">**Google Sheet**</span></span>|<span data-ttu-id="7d4ed-192">스프레드시트</span><span class="sxs-lookup"><span data-stu-id="7d4ed-192">Spreadsheet</span></span>|<span data-ttu-id="7d4ed-193">워크시트</span><span class="sxs-lookup"><span data-stu-id="7d4ed-193">Worksheet</span></span> 
|<span data-ttu-id="7d4ed-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="7d4ed-194">**Excel**</span></span>|<span data-ttu-id="7d4ed-195">Excel 파일</span><span class="sxs-lookup"><span data-stu-id="7d4ed-195">Excel file</span></span>|<span data-ttu-id="7d4ed-196">시트</span><span class="sxs-lookup"><span data-stu-id="7d4ed-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="7d4ed-197">C#에서 사용</span><span class="sxs-lookup"><span data-stu-id="7d4ed-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<span data-ttu-id="7d4ed-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## 데이터 원본 설정</span><span class="sxs-lookup"><span data-stu-id="7d4ed-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="7d4ed-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7d4ed-199">SQL Server</span></span>

<span data-ttu-id="7d4ed-200">스크립트 toocreate hello 및 채울 hello Contact 테이블 미만인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="7d4ed-201">dataSetName은 “default”입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-201">dataSetName is “default.”</span></span>

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a><span data-ttu-id="7d4ed-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="7d4ed-202">Google Sheets</span></span>
<span data-ttu-id="7d4ed-203">Google Docs에서 `Contact`라는 워크시트가 있는 스프레드시트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="7d4ed-204">hello 커넥터 hello 스프레드시트 표시 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="7d4ed-205">hello 내부 이름 (굵게) toobe 예를 들어, dataSetName로 사용 해야: `docs.google.com/spreadsheets/d/` ** `1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0` ** hello 열 이름을 추가 `Id`, `LastName`, `FirstName` toohello 먼저 행을 다음에 데이터 채우기 후속 행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="7d4ed-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="7d4ed-206">Salesforce</span></span>
<span data-ttu-id="7d4ed-207">dataSetName은 “default”입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4ed-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d4ed-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d4ed-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
