---
title: "Microsoft Power BI Embedded 미리 보기 문제 해결"
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
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="7894e-103">Microsoft Power BI Embedded 미리 보기 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7894e-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="7894e-104">이 문서에서는 **Power BI Embedded** 문제를 해결하는 방법에 대한 답변을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7894e-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="7894e-105">SQL Server 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="7894e-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="7894e-106">SQL Server 연결 문자열을 설정하려면 특정 형식을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7894e-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="7894e-107">SQL Server에 대한 연결 문자열의 예는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7894e-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="7894e-108">SQL Server 연결 문자열에 대해 자세히 알아보려면 다음 문서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7894e-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="7894e-109">SQL Server 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7894e-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="7894e-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="7894e-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="7894e-111">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="7894e-111">Setting credentials</span></span>
<span data-ttu-id="7894e-112">사용자 이름 및 암호와 같은 개발 또는 스테이징 환경에 대한 자격 증명이 있는 경우 프로덕션 솔루션과 일치하는 자격 증명을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7894e-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="7894e-113">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7894e-113">See Also</span></span>
* [<span data-ttu-id="7894e-114">샘플 시작</span><span class="sxs-lookup"><span data-stu-id="7894e-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="7894e-115">Power BI Embedded란</span><span class="sxs-lookup"><span data-stu-id="7894e-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

