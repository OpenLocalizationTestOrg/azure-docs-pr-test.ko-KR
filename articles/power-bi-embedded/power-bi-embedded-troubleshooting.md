---
title: "aaaMicrosoft 포함 된 Power BI 미리 보기 문제 해결"
description: "Microsoft Power BI Embedded 미리 보기 문제 해결"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="1c29a-103">Microsoft Power BI Embedded 미리 보기 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1c29a-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="1c29a-104">이 문서는 방법에 대 한 대답을 제공 tootroubleshoot **Power BI 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c29a-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="1c29a-105">SQL Server 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="1c29a-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="1c29a-106">SQL Server 연결 문자열 tooset toofollow 특정 형식 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c29a-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="1c29a-107">SQL Server에 대한 연결 문자열의 예는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c29a-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="1c29a-108">SQL Server 연결 문자열에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="1c29a-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="1c29a-109">SQL Server 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="1c29a-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="1c29a-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="1c29a-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="1c29a-111">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="1c29a-111">Setting credentials</span></span>
<span data-ttu-id="1c29a-112">개발 또는 사용자 이름 및 암호와 같은 스테이징 환경에 대 한 자격 증명이 있는 hello 경우에는 프로덕션 솔루션 일치 하는 tooupdate 자격 증명을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c29a-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c29a-113">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1c29a-113">See Also</span></span>
* [<span data-ttu-id="1c29a-114">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="1c29a-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="1c29a-115">Power BI Embedded란</span><span class="sxs-lookup"><span data-stu-id="1c29a-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

