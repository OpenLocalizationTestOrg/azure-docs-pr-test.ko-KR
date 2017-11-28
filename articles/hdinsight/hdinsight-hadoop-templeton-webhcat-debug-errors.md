---
title: "Azure HDInsight에서 aaaUnderstand 및 해결 WebHCat 오류 | Microsoft Docs"
description: "HDInsight에 WebHCat에 의해 tooabout 일반적인 오류를 반환 하는 방법 및 방법에 대해 알아봅니다 tooresolve 해당 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="1559c-103">HDInsight WebHCat에서 받은 오류 이해 및 해결</span><span class="sxs-lookup"><span data-stu-id="1559c-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="1559c-104">Tooresolve WebHCat HDInsight를 사용 하는 시기와 방법을 받은 오류에 대 한 자세한 내용은 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="1559c-105">WebHCat는 Visual Studio 용 Azure PowerShell 및 hello 데이터 레이크 도구와 같은 클라이언트 도구에서 내부적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="1559c-106">WebHCat이란?</span><span class="sxs-lookup"><span data-stu-id="1559c-106">What is WebHCat</span></span>

<span data-ttu-id="1559c-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat)은 [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog)용 REST API, Hadoop용 테이블 및 저장소 관리 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="1559c-108">WebHCat HDInsight 클러스터를 기본적으로 사용 하며 다양 한 도구 toosubmit 작업에서 사용 됩니다, 그리고 toohello 클러스터 로그인 하지 않고 등 작업 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="1559c-109">구성 수정</span><span class="sxs-lookup"><span data-stu-id="1559c-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1559c-110">이 문서에 나열 된 hello 오류 구성된 최대값을 초과 했기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="1559c-111">Hello 해결 단계에 언급 한 값을 변경할 수 있습니다 때 hello tooperform hello 변경 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="1559c-112">에 대 한 **Windows** 클러스터: 클러스터를 만드는 동안 스크립트 동작 tooconfigure hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="1559c-113">자세한 내용은 [스크립트 동작 개발](hdinsight-hadoop-script-actions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1559c-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="1559c-114">에 대 한 **Linux** 클러스터: (웹 또는 REST API) 사용 하 여 Ambari toomodify hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="1559c-115">자세한 내용은 [Ambari를 사용하여 HDInsight 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="1559c-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1559c-116">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1559c-117">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1559c-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="1559c-118">기본 구성</span><span class="sxs-lookup"><span data-stu-id="1559c-118">Default configuration</span></span>

<span data-ttu-id="1559c-119">다음 기본 값에는 hello 초과 된 경우 WebHCat 성능이 저하 될 하거나 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="1559c-120">설정</span><span class="sxs-lookup"><span data-stu-id="1559c-120">Setting</span></span> | <span data-ttu-id="1559c-121">기능</span><span class="sxs-lookup"><span data-stu-id="1559c-121">What it does</span></span> | <span data-ttu-id="1559c-122">기본값</span><span class="sxs-lookup"><span data-stu-id="1559c-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1559c-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="1559c-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="1559c-124">최대 동시에 활성화 될 수 있는 작업 수를 hello (보류 중 또는 실행)</span><span class="sxs-lookup"><span data-stu-id="1559c-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="1559c-125">10000</span><span class="sxs-lookup"><span data-stu-id="1559c-125">10,000</span></span> |
| <span data-ttu-id="1559c-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="1559c-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="1559c-127">hello 최대 동시에 제공 될 수 있습니다. 있는 요청 수</span><span class="sxs-lookup"><span data-stu-id="1559c-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="1559c-128">20</span><span class="sxs-lookup"><span data-stu-id="1559c-128">20</span></span> |
| <span data-ttu-id="1559c-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="1559c-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="1559c-130">작업 기록 하는 일 수 hello 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="1559c-131">7 일</span><span class="sxs-lookup"><span data-stu-id="1559c-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="1559c-132">너무 많은 요청</span><span class="sxs-lookup"><span data-stu-id="1559c-132">Too many requests</span></span>

<span data-ttu-id="1559c-133">**HTTP 상태 코드**: 429</span><span class="sxs-lookup"><span data-stu-id="1559c-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="1559c-134">원인</span><span class="sxs-lookup"><span data-stu-id="1559c-134">Cause</span></span> | <span data-ttu-id="1559c-135">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1559c-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="1559c-136">기본값인 20 분 당 WebHCat 통해 저장 된 hello 최대 동시 요청을 지났습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="1559c-137">사용자 작업 tooensure 하지 제출 보다 최대 동시 요청 수가 hello 또는 않는 수정 하 여 hello 동시 요청 한도 늘릴 줄일 `templeton.exec.max-procs`합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="1559c-138">자세한 내용은 [구성 수정](#modifying-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1559c-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="1559c-139">서버 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="1559c-139">Server unavailable</span></span>

<span data-ttu-id="1559c-140">**HTTP 상태 코드**: 503</span><span class="sxs-lookup"><span data-stu-id="1559c-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="1559c-141">원인</span><span class="sxs-lookup"><span data-stu-id="1559c-141">Cause</span></span> | <span data-ttu-id="1559c-142">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1559c-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="1559c-143">이 상태 코드는 일반적으로 hello 기본 및 보조 간 장애 조치 하는 동안 발생 hello 클러스터 헤드 노드에</span><span class="sxs-lookup"><span data-stu-id="1559c-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="1559c-144">2 분 동안 기다린 후 hello 작업을 다시 시도</span><span class="sxs-lookup"><span data-stu-id="1559c-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="1559c-145">잘못된 요청 콘텐츠: 작업을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="1559c-146">**HTTP 상태 코드**: 400</span><span class="sxs-lookup"><span data-stu-id="1559c-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="1559c-147">원인</span><span class="sxs-lookup"><span data-stu-id="1559c-147">Cause</span></span> | <span data-ttu-id="1559c-148">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1559c-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="1559c-149">작업 세부 정보를 정리 된 hello 작업 기록에서 수행 되는 클리너</span><span class="sxs-lookup"><span data-stu-id="1559c-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="1559c-150">작업 기록에 대 한 hello 기본 보존 기간 7 일입니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="1559c-151">hello 기본 보존 기간을 수정 하 여 변경할 수 있습니다 `mapreduce.jobhistory.max-age-ms`합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="1559c-152">자세한 내용은 [구성 수정](#modifying-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1559c-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="1559c-153">장애 조치 tooa 인해 작업이 중단 되었고</span><span class="sxs-lookup"><span data-stu-id="1559c-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="1559c-154">Tootwo 분을에 대 한 작업 제출을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1559c-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="1559c-155">잘못된 작업 ID가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-155">An Invalid job id was used</span></span> |<span data-ttu-id="1559c-156">작업 id hello 올바른지 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="1559c-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="1559c-157">나쁜 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="1559c-157">Bad gateway</span></span>

<span data-ttu-id="1559c-158">**HTTP 상태 코드**: 502</span><span class="sxs-lookup"><span data-stu-id="1559c-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="1559c-159">원인</span><span class="sxs-lookup"><span data-stu-id="1559c-159">Cause</span></span> | <span data-ttu-id="1559c-160">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1559c-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="1559c-161">내부 가비지 수집이 hello WebHCat 프로세스 내에서 발생</span><span class="sxs-lookup"><span data-stu-id="1559c-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="1559c-162">가비지 컬렉션 toofinish 기다리거나 hello WebHCat 서비스를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="1559c-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="1559c-163">Hello ResourceManager 서비스의에서 응답을 기다리는 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="1559c-164">활성 응용 프로그램 수가 hello hello 구성 된 최대 (10, 000 기본값)이 되 면이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="1559c-165">현재 작업 toocomplete 실행 또는 수정 하 여 hello 동시 작업 한도 늘릴 `yarn.scheduler.capacity.maximum-applications`합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="1559c-166">자세한 내용은 참조 hello [수정 구성](#modifying-configuration) 섹션.</span><span class="sxs-lookup"><span data-stu-id="1559c-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="1559c-167">Tooretrieve hello 통해 모든 작업을 시도 [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) 호출 하는 동안 `Fields` 너무 설정`*`</span><span class="sxs-lookup"><span data-stu-id="1559c-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="1559c-168">*모든* 작업 세부 정보를 검색하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="1559c-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="1559c-169">대신 사용 하 여 `jobid` 만 특정 작업 id 보다 큰 작업에 대 한 tooretrieve 세부 정보입니다. 또는 `Fields`를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1559c-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="1559c-170">헤드 노드에 장애 조치 중 다운 hello WebHCat 서비스는</span><span class="sxs-lookup"><span data-stu-id="1559c-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="1559c-171">2 분 동안 기다렸다가 hello 작업을 다시 시도</span><span class="sxs-lookup"><span data-stu-id="1559c-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="1559c-172">WebHCat을 통해 전송되는 500개 이상의 보류 중인 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="1559c-173">더 많은 작업을 제출하기 전에 현재 보류 중인 작업이 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="1559c-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
