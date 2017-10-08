---
title: "클러스터 만들기-Azure HDInsight 중 aaaAdd 하이브 라이브러리 | Microsoft Docs"
description: "어떻게 tooadd 하이브 라이브러리 (jar 파일), tooan HDInsight는 클러스터를 만드는 동안을 클러스터에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="c442f-103">HDInsight 클러스터를 만들 때 사용자 지정 Hive 라이브러리에 추가</span><span class="sxs-lookup"><span data-stu-id="c442f-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="c442f-104">HDInsight의 Hive와 자주 사용 하는 라이브러리를 사용 하도록 설정한 경우이 문서 스크립트 동작 toopre 부하 hello 라이브러리를 사용 하 여 클러스터 생성 중에 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="c442f-105">Hello 단계를 사용 하 여이 문서에 추가 된 전체적으로 사용할 수 있는지 확인 하이브에-없습니다 필요 toouse [JAR 추가](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c442f-106">작동 방법</span><span class="sxs-lookup"><span data-stu-id="c442f-106">How it works</span></span>

<span data-ttu-id="c442f-107">클러스터를 만들 때 생성 되는 동안 hello 클러스터 노드에서 스크립트를 실행 하는 스크립트 작업을 필요에 따라 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="c442f-108">이 문서에 hello 스크립트는 미리 로드 하는 hello (jar 파일으로 저장 됨) 라이브러리 toobe 포함 WASB 위치 단일 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="c442f-109">클러스터를 만드는 동안 hello 스크립트 hello 파일을 열거, toohello 복사 `/usr/lib/customhivelibs/` 작업자 노드 및 헤드 노드에서 디렉터리에 추가 toohello `hive.aux.jars.path` hello에 대 한 속성 `core-site.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="c442f-110">Linux 기반 클러스터에서 업데이트 hello `hive-env.sh` hello 파일의 hello 위치와 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="c442f-111">이 문서의 hello 스크립트 동작을 사용 하 여에서는 hello 라이브러리 hello 다음 시나리오에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="c442f-112">**Linux 기반 HDInsight** -하이브 클라이언트 hello를 사용 하는 경우 **WebHCat**, 및 **HiveServer2**합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="c442f-113">**Windows 기반 HDInsight** -hello 하이브 클라이언트를 사용 하는 경우 및 **WebHCat**합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="c442f-114">hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="c442f-114">hello script</span></span>

<span data-ttu-id="c442f-115">**스크립트 위치**</span><span class="sxs-lookup"><span data-stu-id="c442f-115">**Script location**</span></span>

<span data-ttu-id="c442f-116">**Linux 기반 클러스터**의 경우: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="c442f-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="c442f-117">**Windows 기반 클러스터**의 경우: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="c442f-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c442f-118">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c442f-119">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c442f-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c442f-120">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="c442f-120">**Requirements**</span></span>

* <span data-ttu-id="c442f-121">hello 스크립트 적용된 tooboth hello 여야 **헤드 노드** 및 **작업자 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="c442f-122">tooinstall Azure Blob 저장소에 저장 해야 하는 것이 원하는 jar hello는 **단일 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="c442f-123">jar 파일의 hello 라이브러리가 포함 된 hello 저장소 계정 **해야** 연결된 toohello HDInsight 클러스터를 만드는 동안 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="c442f-124">Hello 기본 저장소 계정 이어야 또는 계정을 통해 추가 된 __선택적 구성__합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="c442f-125">매개 변수 toohello 스크립트 동작으로 hello WASB 경로 toohello 컨테이너를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="c442f-126">Jar 라는 컨테이너에 저장 된 경우 hello에 예를 들어 **libs** 라는 저장소 계정에서 **mystorage**, hello 매개 변수를 지정할  **wasb://libs@mystorage.blob.core.windows.net/** 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c442f-127">이 문서에서는 저장소 계정, blob 컨테이너 및 업로드 된 hello 파일 tooit 만들 이미 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="c442f-128">저장소 계정을 만들지 않은 경우 그렇게 할 수 있습니다 hello를 통해 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c442f-129">사용할 수 있습니다는 유틸리티와 같은 [Azure 저장소 탐색기](http://storageexplorer.com/) toocreate hello 계정 및 업로드에서 컨테이너 tooit 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="c442f-130">Hello 스크립트를 사용 하 여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c442f-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="c442f-131">단계를 수행 하는 hello Linux 기반 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c442f-132">Windows 기반 클러스터 toocreate 선택 **Windows** hello 클러스터를 만들 때 hello로 운영 체제를 클러스터링 하 고 hello Windows (PowerShell) 스크립트를 사용 하 여 hello bash 스크립트 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="c442f-133">Azure PowerShell 또는 hello HDInsight.NET SDK toocreate이이 스크립트를 사용 하는 클러스터를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="c442f-134">이 방법을 사용하는 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c442f-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="c442f-135">hello 단계를 사용 하 여 클러스터를 프로 비전 시작 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md), 하지만 프로 비전을 완료 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="c442f-136">Hello에 **옵션 구성** 블레이드를 **스크립트 동작**, hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="c442f-137">**이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="c442f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="c442f-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="c442f-139">**HEAD**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="c442f-140">**WORKER**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="c442f-141">**ZOOKEEPER**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="c442f-142">**매개 변수**: hello WASB 주소 toohello 컨테이너와 저장소 계정 hello jar 포함 된 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="c442f-143">예를 들어 **wasb://libs@mystorage.blob.core.windows.net/**입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="c442f-144">Hello hello 맨 아래에 **스크립트 동작**, hello를 사용 하 여 **선택** 단추 toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="c442f-145">Hello에 **옵션 구성** 블레이드를 **연결 된 저장소 계정** 및 선택 hello **저장소 키를 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="c442f-146">Hello jar를 포함 하는 hello 저장소 계정을 선택 하 고 다음 hello를 사용 하 여 **선택** 단추 toosave 설정 및 반환 hello **선택적 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="c442f-147">사용 하 여 hello **선택** hello 아래쪽 hello의 단추 **선택적 구성** 블레이드 toosave hello 선택적 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="c442f-148">에 설명 된 대로 hello 클러스터를 프로 비전 계속 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c442f-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="c442f-149">클러스터 만들기가 완료 되 면 수 toouse hello jar toouse hello 필요 없이 하이브에서이 스크립트를 통해 추가 된 됩니다 `ADD JAR` 문.</span><span class="sxs-lookup"><span data-stu-id="c442f-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c442f-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c442f-150">Next steps</span></span>

<span data-ttu-id="c442f-151">Hive로 작업하는 방법에 대한 자세한 내용은 [HDInsight로 Hive 사용](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="c442f-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
