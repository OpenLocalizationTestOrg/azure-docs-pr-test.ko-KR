---
title: "Azure Blob 컨테이너, SQL Server 및 Hive 테이블에서 데이터 샘플링 | Microsoft Docs"
description: "다양한 Azure 환경에 저장된 데이터를 탐색하는 방법"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="36dab-103"><a name="heading"></a>Azure blob 컨테이너, SQL Server 및 Hive 테이블의 데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="36dab-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="36dab-104">이 문서는 세 가지 다른 Azure 위치 중 하나에 저장된 데이터를 샘플링하는 방법을 설명하는 토픽에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="36dab-105">**Azure blob 컨테이너 데이터** 는 프로그래밍 방식으로 다운로드한 다음 샘플 Python 코드로 샘플링함으로써 샘플링됩니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="36dab-106">**SQL Server 데이터** 는 SQL 및 Python 프로그래밍 언어를 모두 사용하여 샘플링됩니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="36dab-107">**Hive 테이블 데이터** 는 Hive 쿼리를 사용하여 샘플링됩니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="36dab-108">다음의 **메뉴** 는 이러한 각 Azure Storage 환경에서 데이터를 샘플링하는 방법을 설명하는 토픽에 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="36dab-109">이 샘플 작업은 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="36dab-110">**데이터를 샘플링하는 이유**</span><span class="sxs-lookup"><span data-stu-id="36dab-110">**Why sample data?**</span></span>

<span data-ttu-id="36dab-111">분석할 데이터 집합이 큰 경우 일반적으로 데이터를 다운 샘플링하여 작지만 전형적이고 관리하기 쉬운 크기로 줄이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="36dab-112">그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="36dab-113">Cortana 분석 프로세스에서는 데이터 처리 기능 및 기계 학습 모델의 빠른 프로토타입 제작을 지원하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="36dab-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

