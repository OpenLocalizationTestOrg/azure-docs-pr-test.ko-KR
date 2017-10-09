---
title: "HDInsight에서 Hadoop aaaSubmit 작업 | Microsoft Docs"
description: "Hadoop toosubmit tooAzure HDInsight Hadoop 작업 하는 방법에 대해 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 50430b96-2329-4775-9713-19c5795b775f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6c3acde744e8e384088a6cd56e4273c001c0c9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="81465-103">HDInsight에서 Hadoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="81465-103">Submit Hadoop jobs in HDInsight</span></span>

<span data-ttu-id="81465-104">.NET SDK, Curl 및 Azure PowerShell을 사용하여 Hadoop 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81465-104">You can submit Hadoop jobs using .NET SDK, Curl, and Azure PowerShell:</span></span>

- <span data-ttu-id="81465-105">.NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="81465-105">Use .NET SDK</span></span>

  - [<span data-ttu-id="81465-106">비대화형 인증 .NET 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="81465-106">Create non-interactive authentication .NET applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)
  - [<span data-ttu-id="81465-107">HDInsight .NET SDK를 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="81465-107">Run Hive queries using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
  - [<span data-ttu-id="81465-108">HDInsight에서 Hadoop에 대 한 hello.NET SDK를 사용 하 여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-108">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
  - [<span data-ttu-id="81465-109">HDInsight에서 Hadoop용 .NET SDK를 사용하여 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-109">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
  - [<span data-ttu-id="81465-110">HDInsight .NET SDK를 사용하여 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-110">Run MapReduce jobs using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-mapreduce-dotnet-sdk.md)

- <span data-ttu-id="81465-111">CURL</span><span class="sxs-lookup"><span data-stu-id="81465-111">CURL</span></span>

  - [<span data-ttu-id="81465-112">Curl을 사용하여 HDInsight에서 Hadoop으로 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="81465-112">Run Hive queries with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-hive-curl.md)
  - [<span data-ttu-id="81465-113">Curl을 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-113">Run Pig jobs with Hadoop on HDInsight by using Curl</span></span>](hdinsight-hadoop-use-pig-curl.md)
  - [<span data-ttu-id="81465-114">Curl을 사용하여 HDInsight에서 Hadoop으로 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-114">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-sqoop-curl.md)
  - [<span data-ttu-id="81465-115">Curl을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-115">Run MapReduce jobs with Hadoop on HDInsight using Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)

- <span data-ttu-id="81465-116">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81465-116">PowerShell</span></span>

  - [<span data-ttu-id="81465-117">PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="81465-117">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
  - [<span data-ttu-id="81465-118">PowerShell을 사용하여 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-118">Run Pig jobs using PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md)
  - [<span data-ttu-id="81465-119">HDInsight에서 Hadoop과 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="81465-119">Use Sqoop with Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)
  - [<span data-ttu-id="81465-120">PowerShell을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="81465-120">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md)

## <a name="see-also"></a><span data-ttu-id="81465-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="81465-121">See also</span></span>

- [<span data-ttu-id="81465-122">Azure HDInsight 설명서</span><span class="sxs-lookup"><span data-stu-id="81465-122">Azure HDInsight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)