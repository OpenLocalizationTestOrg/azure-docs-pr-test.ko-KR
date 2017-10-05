---
title: "Azure Cloud Shell(미리 보기) 기능 | Microsoft Docs"
description: "Azure Cloud Shell의 기능 개요"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="c387b-103">Azure Cloud Shell에 대한 기능 및 도구</span><span class="sxs-lookup"><span data-stu-id="c387b-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="c387b-104">Azure Cloud Shell은 Azure 리소스를 관리 및 개발하기 위한 브라우저 기반 셸 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="c387b-105">Cloud Shell은 컴퓨터의 직접 설치, 버전 관리 및 유지 관리에 대한 오버헤드 없이 Azure 리소스 관리를 위한 브라우저에서 액세스할 수 있는 미리 구성된 셸 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="c387b-106">Cloud Shell은 요청별로 컴퓨터를 프로비전하므로 결과적으로 컴퓨터 상태는 세션 간에 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="c387b-107">Cloud Shell은 대화형 세션용으로 빌드되었기 때문에 셸은 셸 비활성 시간 20분 후 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="c387b-108">Cloud Shell의 Bash</span><span class="sxs-lookup"><span data-stu-id="c387b-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="c387b-109">도구</span><span class="sxs-lookup"><span data-stu-id="c387b-109">Tools</span></span>
|<span data-ttu-id="c387b-110">Category</span><span class="sxs-lookup"><span data-stu-id="c387b-110">Category</span></span>   |<span data-ttu-id="c387b-111">이름</span><span class="sxs-lookup"><span data-stu-id="c387b-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="c387b-112">Linux 셸 인터프리터</span><span class="sxs-lookup"><span data-stu-id="c387b-112">Linux shell interpreter</span></span>|<span data-ttu-id="c387b-113">Bash</span><span class="sxs-lookup"><span data-stu-id="c387b-113">Bash</span></span><br> <span data-ttu-id="c387b-114">sh</span><span class="sxs-lookup"><span data-stu-id="c387b-114">sh</span></span>               |
|<span data-ttu-id="c387b-115">Azure 도구</span><span class="sxs-lookup"><span data-stu-id="c387b-115">Azure tools</span></span>            |<span data-ttu-id="c387b-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) 및 [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="c387b-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="c387b-117">AZCopy</span><span class="sxs-lookup"><span data-stu-id="c387b-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="c387b-118">배치 Shipyard</span><span class="sxs-lookup"><span data-stu-id="c387b-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="c387b-119">텍스트 편집기</span><span class="sxs-lookup"><span data-stu-id="c387b-119">Text editors</span></span>           |<span data-ttu-id="c387b-120">vim</span><span class="sxs-lookup"><span data-stu-id="c387b-120">vim</span></span><br> <span data-ttu-id="c387b-121">nano</span><span class="sxs-lookup"><span data-stu-id="c387b-121">nano</span></span><br> <span data-ttu-id="c387b-122">emacs</span><span class="sxs-lookup"><span data-stu-id="c387b-122">emacs</span></span>       |
|<span data-ttu-id="c387b-123">소스 제어</span><span class="sxs-lookup"><span data-stu-id="c387b-123">Source control</span></span>         |<span data-ttu-id="c387b-124">git</span><span class="sxs-lookup"><span data-stu-id="c387b-124">git</span></span>                    |
|<span data-ttu-id="c387b-125">빌드 도구</span><span class="sxs-lookup"><span data-stu-id="c387b-125">Build tools</span></span>            |<span data-ttu-id="c387b-126">make</span><span class="sxs-lookup"><span data-stu-id="c387b-126">make</span></span><br> <span data-ttu-id="c387b-127">maven</span><span class="sxs-lookup"><span data-stu-id="c387b-127">maven</span></span><br> <span data-ttu-id="c387b-128">npm</span><span class="sxs-lookup"><span data-stu-id="c387b-128">npm</span></span><br> <span data-ttu-id="c387b-129">pip</span><span class="sxs-lookup"><span data-stu-id="c387b-129">pip</span></span>         |
|<span data-ttu-id="c387b-130">컨테이너</span><span class="sxs-lookup"><span data-stu-id="c387b-130">Containers</span></span>             |<span data-ttu-id="c387b-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="c387b-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="c387b-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="c387b-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="c387b-133">초안</span><span class="sxs-lookup"><span data-stu-id="c387b-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="c387b-134">DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="c387b-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="c387b-135">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c387b-135">Databases</span></span>              |<span data-ttu-id="c387b-136">MySQL 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c387b-136">MySQL client</span></span><br> <span data-ttu-id="c387b-137">PostgreSql 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c387b-137">PostgreSql client</span></span><br> [<span data-ttu-id="c387b-138">sqlcmd 유틸리티</span><span class="sxs-lookup"><span data-stu-id="c387b-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="c387b-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="c387b-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="c387b-140">기타</span><span class="sxs-lookup"><span data-stu-id="c387b-140">Other</span></span>                  |<span data-ttu-id="c387b-141">iPython 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c387b-141">iPython Client</span></span><br> [<span data-ttu-id="c387b-142">Cloud Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="c387b-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="c387b-143">언어 지원</span><span class="sxs-lookup"><span data-stu-id="c387b-143">Language support</span></span>
|<span data-ttu-id="c387b-144">language</span><span class="sxs-lookup"><span data-stu-id="c387b-144">Language</span></span>   |<span data-ttu-id="c387b-145">버전</span><span class="sxs-lookup"><span data-stu-id="c387b-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="c387b-146">.NET</span><span class="sxs-lookup"><span data-stu-id="c387b-146">.NET</span></span>       |<span data-ttu-id="c387b-147">1.01</span><span class="sxs-lookup"><span data-stu-id="c387b-147">1.01</span></span>       |
|<span data-ttu-id="c387b-148">Go</span><span class="sxs-lookup"><span data-stu-id="c387b-148">Go</span></span>         |<span data-ttu-id="c387b-149">1.7</span><span class="sxs-lookup"><span data-stu-id="c387b-149">1.7</span></span>        |
|<span data-ttu-id="c387b-150">자바</span><span class="sxs-lookup"><span data-stu-id="c387b-150">Java</span></span>       |<span data-ttu-id="c387b-151">1.8</span><span class="sxs-lookup"><span data-stu-id="c387b-151">1.8</span></span>        |
|<span data-ttu-id="c387b-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="c387b-152">Node.js</span></span>    |<span data-ttu-id="c387b-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="c387b-153">6.9.4</span></span>      |
|<span data-ttu-id="c387b-154">파이썬</span><span class="sxs-lookup"><span data-stu-id="c387b-154">Python</span></span>     |<span data-ttu-id="c387b-155">2.7 및 3.5(기본값)</span><span class="sxs-lookup"><span data-stu-id="c387b-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="c387b-156">안전한 자동 인증</span><span class="sxs-lookup"><span data-stu-id="c387b-156">Secure automatic authentication</span></span>
<span data-ttu-id="c387b-157">Cloud Shell은 Azure CLI 2.0에 대한 계정 액세스를 안전하고 자동으로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="c387b-158">Azure 파일 지속성</span><span class="sxs-lookup"><span data-stu-id="c387b-158">Azure Files persistence</span></span>
<span data-ttu-id="c387b-159">Cloud Shell은 임시 컴퓨터를 사용하여 요청별로 할당되므로 $Home 외부에 있는 파일 및 컴퓨터 상태는 세션 간에 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="c387b-160">세션 간에 파일을 유지하기 위해 Cloud Shell에서는 처음 시작할 때 Azure 파일 공유 연결을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="c387b-161">작업이 완료되면 Cloud Shell은 이후의 모든 세션에 대해 저장소를 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="c387b-162">Azure 파일 공유를 Cloud Shell에 연결하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c387b-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="c387b-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c387b-163">Next steps</span></span>
[<span data-ttu-id="c387b-164">Cloud Shell 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="c387b-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="c387b-165">
[Azure CLI 2.0에 대한 자세한 정보](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="c387b-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>