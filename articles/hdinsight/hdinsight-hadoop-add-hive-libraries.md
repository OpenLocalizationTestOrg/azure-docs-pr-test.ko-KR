---
title: "HDInsight 클러스터를 만드는 동안 Hive 라이브러리 추가 - Azure | Microsoft Docs"
description: "클러스터를 만드는 동안 HDInsight 클러스터에 Hive 라이브러리(jar 파일)를 추가하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="f254e-103">HDInsight 클러스터를 만들 때 사용자 지정 Hive 라이브러리에 추가</span><span class="sxs-lookup"><span data-stu-id="f254e-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="f254e-104">HDInsight에서 Hive와 함께 자주 사용하는 라이브러리가 있는 경우 이 문서는 클러스터를 만드는 동안 스크립트 작업을 사용하여 라이브러리를 사전 로드하는 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="f254e-105">이 문서의 단계를 사용하여 추가된 라이브러리는 Hive에서 전역적으로 사용 가능합니다. 로드하는 데 [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli)을 사용하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="f254e-106">작동 방법</span><span class="sxs-lookup"><span data-stu-id="f254e-106">How it works</span></span>

<span data-ttu-id="f254e-107">클러스터를 만들 때 생성된 클러스터 노드에서 스크립트를 실행하는 스크립트 작업을 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="f254e-108">이 문서의 스크립트는 단일 매개 변수를 수락하며 이는 미리 로드된 라이브러리(jar 파일로 저장됨)가 포함되는 WASB 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="f254e-109">클러스터를 만들 때 스크립트는 파일을 열거하고 헤드 및 작업자 노드의 `/usr/lib/customhivelibs/` 디렉터리에 복사한 다음 `core-site.xml` 파일의 `hive.aux.jars.path` 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="f254e-110">또한 Linux 기반 클러스터에서 파일의 위치로 `hive-env.sh` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="f254e-111">이 문서의 스크립트 작업을 사용하여 다음과 같은 시나리오에서 라이브러리를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="f254e-112">**Linux 기반 HDInsight** - Hive 클라이언트, **WebHCat** 및 **HiveServer2**를 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f254e-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="f254e-113">**Windows 기반 HDInsight** - Hive 클라이언트 및 **WebHCat**을 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f254e-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="f254e-114">스크립트</span><span class="sxs-lookup"><span data-stu-id="f254e-114">The script</span></span>

<span data-ttu-id="f254e-115">**스크립트 위치**</span><span class="sxs-lookup"><span data-stu-id="f254e-115">**Script location**</span></span>

<span data-ttu-id="f254e-116">**Linux 기반 클러스터**의 경우: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="f254e-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="f254e-117">**Windows 기반 클러스터**의 경우: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="f254e-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f254e-118">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f254e-119">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f254e-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="f254e-120">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="f254e-120">**Requirements**</span></span>

* <span data-ttu-id="f254e-121">스크립트는 **헤드 노드** 및 **작업자 노드** 모두에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="f254e-122">설치하려는 jar을 **단일 컨테이너**의 Azure Blob Storage에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="f254e-123">만드는 동안 jar 파일의 라이브러리를 포함하는 저장소 계정을 HDInsight 클러스터에 **연결해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="f254e-124">기본 저장소 계정이거나 __선택적 구성__을 통해 추가된 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="f254e-125">컨테이너에 대한 WASB 경로를 스크립트 작업에 대한 매개 변수로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="f254e-126">예를 들어 jar이 **mystorage** 저장소 계정의 **libs** 컨테이너에 저장되는 경우 매개 변수는 **wasb://libs@mystorage.blob.core.windows.net/**입니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f254e-127">이 문서는 이미 저장소 계정, Blob 컨테이너를 만들고 거기에 파일을 업로드했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="f254e-128">저장소 계정을 만들지 않은 경우 [Azure Portal](https://portal.azure.com)을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f254e-129">[Azure 저장소 탐색기](http://storageexplorer.com/)와 같은 유틸리티를 사용하여 계정에 컨테이너를 만들고 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="f254e-130">스크립트를 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f254e-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="f254e-131">다음 단계는 Linux 기반 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f254e-132">Windows 기반 클러스터를 만들려면 클러스터를 만들 때 **Windows**를 클러스터 OS로 선택하고 bash 스크립트 대신 Windows(PowerShell) 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="f254e-133">또한 이 스크립트를 사용하여 클러스터를 만드는 데 Azure PowerShell 또는 HDInsight.NET SDK를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="f254e-134">이 방법을 사용하는 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f254e-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="f254e-135">[Linux에서 HDInsight 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md)의 단계를 사용하여 클러스터 프로비전을 시작하는 한편 프로비전을 완료하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="f254e-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="f254e-136">**선택적 구성** 블레이드에서 **스크립트 동작**을 선택하고 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="f254e-137">**이름**: 스크립트 동작의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="f254e-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="f254e-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="f254e-139">**HEAD**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="f254e-140">**WORKER**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="f254e-141">**ZOOKEEPER**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="f254e-142">**매개 변수**: jar을 포함하는 컨테이너 및 저장소 계정에 WASB 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="f254e-143">예를 들어 **wasb://libs@mystorage.blob.core.windows.net/**입니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="f254e-144">**스크립트 동작**의 아래 쪽에서 **선택** 단추를 사용하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="f254e-145">**선택적 구성** 블레이드에서 **연결된 저장소 계정**을 선택하고 **저장소 키 추가** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="f254e-146">jar을 포함하는 저장소 계정을 선택한 다음 **선택** 단추를 사용하여 설정을 저장하고 **선택적 구성** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="f254e-147">**선택적 구성** 블레이드 아래쪽의 **선택** 단추를 사용하여 선택적 구성 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="f254e-148">[Linux에서 HDInsight 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 계속 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="f254e-149">클러스터 생성이 완료되면 `ADD JAR` 문을 사용하지 않고도 Hive에서 이 스크립트를 통해 추가된 jar을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f254e-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f254e-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f254e-150">Next steps</span></span>

<span data-ttu-id="f254e-151">Hive로 작업하는 방법에 대한 자세한 내용은 [HDInsight로 Hive 사용](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="f254e-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
