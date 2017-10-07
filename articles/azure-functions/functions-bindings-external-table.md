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
# <a name="azure-functions-external-table-binding-preview"></a>Azure Functions 외부 테이블 바인딩(미리 보기)
이 문서에서는 어떻게 toomanipulate 테이블 형식 데이터를 SaaS 공급자 (예: Sharepoint, Dynamics) 기본 제공 바인딩 사용 하는 함수 내에 있습니다. Azure Functions는 외부 테이블에 대한 입력 및 출력 바인딩을 지원합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>API 연결

테이블 바인딩 타사 SaaS 공급자와 외부 API 연결 tooauthenticate를 활용합니다. 

바인딩을 할당할 때 새 API 연결을 만들 하거나 hello 내에서 기존 API 연결을 사용 하 여 동일한 리소스 그룹

### <a name="supported-api-connections-tables"></a>지원되는 API 연결(테이블)

|커넥터|트리거|입력|출력|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 for Operations](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google Sheets](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 for Financials](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle 데이터베이스](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> 외부 테이블 연결은 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)에서도 사용할 수 있습니다

### <a name="creating-an-api-connection-step-by-step"></a>API 연결 만들기: 단계별 방법

1. 함수 만들기 > 사용자 지정 함수 ![사용자 지정 함수 만들기](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. 시나리오 `Experimental` > `ExternalTable-CSharp` 템플릿 > 새 `External Table connection` 만들기
![테이블 입력 템플릿 선택](./media/functions-bindings-storage-table/create-template-table.jpg)
1. SaaS 공급자 선택 > 연결 선택/만들기 ![SaaS 연결 구성](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. API 연결을 선택 > hello 함수를 만들 ![테이블 함수 만들기](./media/functions-bindings-storage-table/table-template-options.jpg)
1. `Integrate` > `External Table` 선택
    1. Hello 연결 toouse 대상 테이블을 구성 합니다. 이러한 설정은 SaaS 공급자마다 다릅니다. 이 내용은 아래 [데이터 원본 설정](#datasourcesettings)
![테이블 구성](./media/functions-bindings-storage-table/configure-API-connection.jpg)에서 간략히 설명합니다.

## <a name="usage"></a>사용

이 예에서는 Id, LastName 및 FirstName 열과 "Contact" 라는 tooa 테이블을 연결 합니다. 로그 이름과 성을 hello 및 hello 코드 hello 테이블의 hello 연락처 엔터티를 나열 합니다.

### <a name="bindings"></a>바인딩
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
`entityId`는 테이블 바인딩을 위해 비어 있어야 합니다.

`ConnectionAppSettingsKey`hello API 연결 문자열을 저장 하는 hello 응용 프로그램 설정을 식별 합니다. hello 응용 프로그램 설정을 자동으로 생성 됩니다는 API를 추가 하면 UI를 통합 하는 hello에 연결 합니다.

테이블 형식 커넥터는 데이터 집합을 제공하며 각 데이터 집합은 테이블을 포함합니다. hello hello 기본 데이터 집합 이름은 "default"입니다. 데이터 집합 및 다양 한 SaaS 공급자의 테이블에 대 한 hello 타이틀은 다음과 같습니다.

|커넥터|데이터 집합|테이블|
|:-----|:---|:---| 
|**SharePoint**|사이트|SharePoint 목록
|**SQL**|데이터베이스|테이블 
|**Google Sheet**|스프레드시트|워크시트 
|**Excel**|Excel 파일|시트 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>C#에서 사용 #

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

<!--
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
## 데이터 원본 설정

### <a name="sql-server"></a>SQL Server

스크립트 toocreate hello 및 채울 hello Contact 테이블 미만인 합니다. dataSetName은 “default”입니다.

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

### <a name="google-sheets"></a>Google Sheets
Google Docs에서 `Contact`라는 워크시트가 있는 스프레드시트를 만듭니다. hello 커넥터 hello 스프레드시트 표시 이름을 사용할 수 없습니다. hello 내부 이름 (굵게) toobe 예를 들어, dataSetName로 사용 해야: `docs.google.com/spreadsheets/d/` ** `1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0` ** hello 열 이름을 추가 `Id`, `LastName`, `FirstName` toohello 먼저 행을 다음에 데이터 채우기 후속 행 수입니다.

### <a name="salesforce"></a>Salesforce
dataSetName은 “default”입니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
