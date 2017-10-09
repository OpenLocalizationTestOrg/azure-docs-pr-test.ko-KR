---
title: "HDInsight-Azure와 액션 개발 aaaScript | Microsoft Docs"
description: "스크립트 동작을 가진 toocustomize Hadoop 클러스터 하는 방법에 대해 알아봅니다. 스크립트 동작 사용된 tooinstall 클러스터에 설치 된 응용 프로그램의 Hadoop 클러스터 또는 toochange hello 구성에서 실행 되는 추가 소프트웨어를 수 있습니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a><span data-ttu-id="4ba69-104">HDInsight Windows 기반 클러스터용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="4ba69-104">Develop Script Action scripts for HDInsight Windows-based clusters</span></span>
<span data-ttu-id="4ba69-105">스크립트 동작 toowrite HDInsight에 대 한 스크립트 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-105">Learn how toowrite Script Action scripts for HDInsight.</span></span> <span data-ttu-id="4ba69-106">스크립트 동작 스크립트 사용에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-106">For information on using Script Action scripts, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="4ba69-107">Linux 기반 HDInsight 클러스터를 용으로 작성 된 동일한 문서의 hello에 대 한 참조 [HDInsight에 대 한 스크립트 작업 개발 스크립트](hdinsight-hadoop-script-actions-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-107">For hello same article written for Linux-based HDInsight clusters, see [Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>



> [!IMPORTANT]
> <span data-ttu-id="4ba69-108">hello 단계에서 Windows 기반 HDInsight 클러스터에 대 한이 문서 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4ba69-109">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="4ba69-110">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4ba69-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="4ba69-112">Linux 기반 클러스터로 스크립트 작업 사용에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발(Linux)](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-112">For information on using script actions with Linux-based clusters, see [Script action development with HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).</span></span>
>
>



<span data-ttu-id="4ba69-113">스크립트 동작 사용된 tooinstall 클러스터에 설치 된 응용 프로그램의 Hadoop 클러스터 또는 toochange hello 구성에서 실행 되는 추가 소프트웨어를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-113">Script Action can be used tooinstall additional software running on a Hadoop cluster or toochange hello configuration of applications installed on a cluster.</span></span> <span data-ttu-id="4ba69-114">스크립트 작업은 HDInsight 클러스터를 구축할 때 hello 클러스터 노드에서 실행 되는 스크립트 및 hello 클러스터의 노드 HDInsight 구성을 완료 한 후 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-114">Script actions are scripts that run on hello cluster nodes when HDInsight clusters are deployed, and they are executed once nodes in hello cluster complete HDInsight configuration.</span></span> <span data-ttu-id="4ba69-115">스크립트 작업을 시스템 관리자 계정 권한으로 실행 되 고 읽기/쓰기 권한 toohello 클러스터 노드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-115">A script action is executed under system admin account privileges and provides full access rights toohello cluster nodes.</span></span> <span data-ttu-id="4ba69-116">각 클러스터는 지정 된 hello 순서로 실행 하는 스크립트 작업 toobe 목록과 함께 제공 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-116">Each cluster can be provided with a list of script actions toobe executed in hello order in which they are specified.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba69-117">Hello 다음과 같은 오류 메시지가 발생 하면:</span><span class="sxs-lookup"><span data-stu-id="4ba69-117">If you experience hello following error message:</span></span>
>
> <span data-ttu-id="4ba69-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello 용어 ' 저장 HDIFile' 인식 되지 않습니다는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-118">System.Management.Automation.CommandNotFoundException; ExceptionMessage : hello term 'Save-HDIFile' is not recognized as hello name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="4ba69-119">Hello hello 이름이 올바른지 확인 하거나 경로 포함 한 경우 해당 hello 경로가 올바른지 확인 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4ba69-119">Check hello spelling of hello name, or if a path was included, verify that hello path is correct and try again.</span></span>
> <span data-ttu-id="4ba69-120">Hello 도우미 메서드를 포함 하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-120">It is because you didn't include hello helper methods.</span></span>  <span data-ttu-id="4ba69-121">[사용자 지정 스크립트에 대한 도우미 메서드](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-121">See [Helper methods for custom scripts](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).</span></span>
>
>

## <a name="sample-scripts"></a><span data-ttu-id="4ba69-122">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4ba69-122">Sample scripts</span></span>
<span data-ttu-id="4ba69-123">Windows 운영 체제에서 HDInsight 클러스터를 만들기 위해 hello 스크립트 작업은 Azure PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-123">For creating HDInsight clusters on Windows operating system, hello Script Action is Azure PowerShell script.</span></span> <span data-ttu-id="4ba69-124">hello 다음 스크립트는 hello 사이트 구성 파일을 구성 하기 위한 예제:</span><span class="sxs-lookup"><span data-stu-id="4ba69-124">hello following script is a sample for configuring hello site configuration files:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

<span data-ttu-id="4ba69-125">hello 스크립트는 4 개의 매개 변수, hello 구성 파일 이름, toomodify, hello 값 tooset, 및 설명을 표시할 hello 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-125">hello script takes four parameters, hello configuration file name, hello property you want toomodify, hello value you want tooset, and a description.</span></span> <span data-ttu-id="4ba69-126">예:</span><span class="sxs-lookup"><span data-stu-id="4ba69-126">For example:</span></span>

    hive-site.xml hive.metastore.client.socket.timeout 90

<span data-ttu-id="4ba69-127">이러한 매개 변수는 hello hive.metastore.client.socket.timeout 값 too90 hello hive-site.xml 파일에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-127">These parameters sets hello hive.metastore.client.socket.timeout value too90 in hello hive-site.xml file.</span></span>  <span data-ttu-id="4ba69-128">hello 기본값은 60 초입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-128">hello default value is 60 seconds.</span></span>

<span data-ttu-id="4ba69-129">이 샘플 스크립트는 [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1)에도 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-129">This sample script can also be found at [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).</span></span>

<span data-ttu-id="4ba69-130">HDInsight은 HDInsight 클러스터에서 여러 스크립트 tooinstall 추가 구성 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-130">HDInsight provides several scripts tooinstall additional components on HDInsight clusters:</span></span>

| <span data-ttu-id="4ba69-131">이름</span><span class="sxs-lookup"><span data-stu-id="4ba69-131">Name</span></span> | <span data-ttu-id="4ba69-132">스크립트</span><span class="sxs-lookup"><span data-stu-id="4ba69-132">Script</span></span> |
| --- | --- |
| <span data-ttu-id="4ba69-133">**Spark 설치**</span><span class="sxs-lookup"><span data-stu-id="4ba69-133">**Install Spark**</span></span> |<span data-ttu-id="4ba69-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="4ba69-134">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="4ba69-135">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-135">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="4ba69-136">**R 설치**</span><span class="sxs-lookup"><span data-stu-id="4ba69-136">**Install R**</span></span> |<span data-ttu-id="4ba69-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="4ba69-137">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="4ba69-138">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-r-scripts]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-138">See [Install and use R on HDInsight clusters][hdinsight-r-scripts].</span></span> |
| <span data-ttu-id="4ba69-139">**Solr 설치**</span><span class="sxs-lookup"><span data-stu-id="4ba69-139">**Install Solr**</span></span> |<span data-ttu-id="4ba69-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="4ba69-140">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="4ba69-141">[HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-141">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="4ba69-142">- **Giraph 설치**</span><span class="sxs-lookup"><span data-stu-id="4ba69-142">- **Install Giraph**</span></span> |<span data-ttu-id="4ba69-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="4ba69-143">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="4ba69-144">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-144">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |

<span data-ttu-id="4ba69-145">스크립트 동작에는 hello HDInsight.NET SDK를 사용 하 여 하거나 hello Azure 포털, Azure PowerShell에서에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-145">Script Action can be deployed from hello Azure portal, Azure PowerShell or by using hello HDInsight .NET SDK.</span></span>  <span data-ttu-id="4ba69-146">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-146">For more information, see [Customize HDInsight clusters using Script Action][hdinsight-cluster-customize].</span></span>

> [!NOTE]
> <span data-ttu-id="4ba69-147">hello 예제 스크립트는 HDInsight 클러스터 버전이 3.1은만 이상 버전에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-147">hello sample scripts work only with HDInsight cluster version 3.1 or above.</span></span> <span data-ttu-id="4ba69-148">HDInsight 클러스터 버전에 대한 자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-148">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="helper-methods-for-custom-scripts"></a><span data-ttu-id="4ba69-149">사용자 지정 스크립트에 대한 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="4ba69-149">Helper methods for custom scripts</span></span>
<span data-ttu-id="4ba69-150">스크립트 작업 도우미 메서드는 사용자 지정 스크립트를 쓰는 동안 사용할 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-150">Script Action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="4ba69-151">에 정의 된 이러한 메서드가 [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), 다음 예제는 hello를 사용 하 여 스크립트에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-151">These methods are defined in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1), and can be included in your scripts using hello following sample:</span></span>

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

<span data-ttu-id="4ba69-152">이 스크립트에 의해 제공 되는 hello 도우미 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-152">Here are hello helper methods that are provided by this script:</span></span>

| <span data-ttu-id="4ba69-153">도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="4ba69-153">Helper method</span></span> | <span data-ttu-id="4ba69-154">설명</span><span class="sxs-lookup"><span data-stu-id="4ba69-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4ba69-155">**Save-HDIFile**</span><span class="sxs-lookup"><span data-stu-id="4ba69-155">**Save-HDIFile**</span></span> |<span data-ttu-id="4ba69-156">Hello Azure VM 노드 할당된 toohello 클러스터와 연결 된 hello 로컬 디스크에서 식별자 URI (Uniform Resource) tooa 위치를 지정 하는 hello에서 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-156">Download a file from hello specified Uniform Resource Identifier (URI) tooa location on hello local disk that is associated with hello Azure VM node assigned toohello cluster.</span></span> |
| <span data-ttu-id="4ba69-157">**Expand-HDIZippedFile**</span><span class="sxs-lookup"><span data-stu-id="4ba69-157">**Expand-HDIZippedFile**</span></span> |<span data-ttu-id="4ba69-158">압축된 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-158">Unzip a zipped file.</span></span> |
| <span data-ttu-id="4ba69-159">**Invoke-HDICmdScript**</span><span class="sxs-lookup"><span data-stu-id="4ba69-159">**Invoke-HDICmdScript**</span></span> |<span data-ttu-id="4ba69-160">cmd.exe에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-160">Run a script from cmd.exe.</span></span> |
| <span data-ttu-id="4ba69-161">**Write-HDILog**</span><span class="sxs-lookup"><span data-stu-id="4ba69-161">**Write-HDILog**</span></span> |<span data-ttu-id="4ba69-162">스크립트 작업에 사용 된 hello 사용자 지정 스크립트에서 출력을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-162">Write output from hello custom script used for a script action.</span></span> |
| <span data-ttu-id="4ba69-163">**Get-Services**</span><span class="sxs-lookup"><span data-stu-id="4ba69-163">**Get-Services**</span></span> |<span data-ttu-id="4ba69-164">Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 서비스의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-164">Get a list of services running on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-165">**Get-Service**</span><span class="sxs-lookup"><span data-stu-id="4ba69-165">**Get-Service**</span></span> |<span data-ttu-id="4ba69-166">입력으로 hello 특정 서비스 이름으로 특정 서비스에 대 한 자세한 정보를 가져올 (서비스 이름, 프로세스 ID, 상태, 등) hello 컴퓨터 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-166">With hello specific service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-167">**Get-HDIServices**</span><span class="sxs-lookup"><span data-stu-id="4ba69-167">**Get-HDIServices**</span></span> |<span data-ttu-id="4ba69-168">Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 HDInsight 서비스의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-168">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-169">**Get-HDIService**</span><span class="sxs-lookup"><span data-stu-id="4ba69-169">**Get-HDIService**</span></span> |<span data-ttu-id="4ba69-170">Hello 특정 HDInsight 서비스 이름으로 입력으로, 특정 서비스에 대 한 자세한 정보를 가져올 (서비스 이름, 프로세스 ID, 상태, 등) hello 컴퓨터 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-170">With hello specific HDInsight service name as input, get detailed information for a specific service (service name, process ID, state, etc.) on hello machine where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-171">**Get-ServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="4ba69-171">**Get-ServicesRunning**</span></span> |<span data-ttu-id="4ba69-172">Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 서비스의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-172">Get a list of services that are running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-173">**Get-ServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="4ba69-173">**Get-ServiceRunning**</span></span> |<span data-ttu-id="4ba69-174">특정 서비스 이름 사용 하 여 실행 중인지 확인 hello 컴퓨터에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-174">Check if a specific service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-175">**Get-HDIServicesRunning**</span><span class="sxs-lookup"><span data-stu-id="4ba69-175">**Get-HDIServicesRunning**</span></span> |<span data-ttu-id="4ba69-176">Hello 컴퓨터에서 실행 중인 hello 스크립트를 실행 하는 HDInsight 서비스의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-176">Get a list of HDInsight services running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-177">**Get-HDIServiceRunning**</span><span class="sxs-lookup"><span data-stu-id="4ba69-177">**Get-HDIServiceRunning**</span></span> |<span data-ttu-id="4ba69-178">경우 특정 HDInsight 서비스 이름 사용 하 여 컴퓨터에서 실행 중인 hello hello 스크립트가 실행 되는 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-178">Check if a specific HDInsight service (by name) is running on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-179">**Get-HDIHadoopVersion**</span><span class="sxs-lookup"><span data-stu-id="4ba69-179">**Get-HDIHadoopVersion**</span></span> |<span data-ttu-id="4ba69-180">Hadoop hello 스크립트를 실행 하는 hello 컴퓨터에 설치 된 hello 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-180">Get hello version of Hadoop installed on hello computer where hello script executes.</span></span> |
| <span data-ttu-id="4ba69-181">**Test-IsHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="4ba69-181">**Test-IsHDIHeadNode**</span></span> |<span data-ttu-id="4ba69-182">헤드 노드 hello 스크립트를 실행 하는 hello 컴퓨터 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-182">Check if hello computer where hello script executes is a head node.</span></span> |
| <span data-ttu-id="4ba69-183">**Test-IsActiveHDIHeadNode**</span><span class="sxs-lookup"><span data-stu-id="4ba69-183">**Test-IsActiveHDIHeadNode**</span></span> |<span data-ttu-id="4ba69-184">Hello 스크립트를 실행 하는 hello 컴퓨터 활성 헤드 노드에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4ba69-184">Check if hello computer where hello script executes is an active head node.</span></span> |
| <span data-ttu-id="4ba69-185">**Test-IsHDIDataNode**</span><span class="sxs-lookup"><span data-stu-id="4ba69-185">**Test-IsHDIDataNode**</span></span> |<span data-ttu-id="4ba69-186">데이터 노드 hello 스크립트를 실행 하는 hello 컴퓨터 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-186">Check if hello computer where hello script executes is a data node.</span></span> |
| <span data-ttu-id="4ba69-187">**Edit-HDIConfigFile**</span><span class="sxs-lookup"><span data-stu-id="4ba69-187">**Edit-HDIConfigFile**</span></span> |<span data-ttu-id="4ba69-188">Hello config 파일 hive-site.xml, 코어 site.xml, hdfs-site.xml, mapred-site.xml, 또는 yarn-site.xml 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-188">Edit hello config files hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml, or yarn-site.xml.</span></span> |

## <a name="best-practices-for-script-development"></a><span data-ttu-id="4ba69-189">스크립트 개발을 위한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="4ba69-189">Best practices for script development</span></span>
<span data-ttu-id="4ba69-190">HDInsight 클러스터에 대 한 사용자 지정 스크립트를 개발할 때 염두에 몇 가지 모범 사례 tookeep 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-190">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* <span data-ttu-id="4ba69-191">Hello Hadoop 버전을 확인</span><span class="sxs-lookup"><span data-stu-id="4ba69-191">Check for hello Hadoop version</span></span>

    <span data-ttu-id="4ba69-192">HDInsight 버전 3.1 (Hadoop 2.4) 이상과 tooinstall 사용자 지정 스크립트 동작 구성 요소를 사용 하 여 클러스터에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-192">Only HDInsight version 3.1 (Hadoop 2.4) and above support using Script Action tooinstall custom components on a cluster.</span></span> <span data-ttu-id="4ba69-193">사용자 지정 스크립트에서 hello를 사용 해야 **Get HDIHadoopVersion** hello 스크립트에서 다른 작업을 수행 합니다. 계속 하기 전에 도우미 메서드 toocheck hello Hadoop 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-193">In your custom script, you must use hello **Get-HDIHadoopVersion** helper method toocheck hello Hadoop version before proceeding with performing other tasks in hello script.</span></span>
* <span data-ttu-id="4ba69-194">안정적인 tooscript 리소스 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-194">Provide stable links tooscript resources</span></span>

    <span data-ttu-id="4ba69-195">사용자가 확인 해야 모든 hello 스크립트와 클러스터의 hello 사용자 지정에 사용 되는 다른 아티팩트 계속 hello 클러스터의 hello 수명 주기 동안 사용할 수 및 이러한 파일의 hello 버전 hello 기간에 대 한 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-195">Users should make sure that all hello scripts and other artifacts used in hello customization of a cluster remain available throughout hello lifetime of hello cluster and that hello versions of these files do not change for hello duration.</span></span> <span data-ttu-id="4ba69-196">이러한 리소스는 hello hello 클러스터 노드를 이미지로 다시 설치 해야 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-196">These resources are required if hello reimaging of nodes in hello cluster is required.</span></span> <span data-ttu-id="4ba69-197">hello 가장 좋은 방법은 toodownload 이며 사용자 정의 컨트롤 hello 저장소 계정에 모든 항목을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-197">hello best practice is toodownload and archive everything in a Storage account that hello user controls.</span></span> <span data-ttu-id="4ba69-198">이 hello 기본 저장소 계정 또는 사용자 지정 된 클러스터에 대 한 배포의 hello 타임에 지정한 hello 추가 되는 저장소 계정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-198">This can be hello default Storage account or any of hello additional Storage accounts specified at hello time of deployment for a customized cluster.</span></span>
    <span data-ttu-id="4ba69-199">Hello에서 Spark와 R 사용자 지정 클러스터 샘플 hello 설명서의 예를 들어 기능이 되었습니다 hello 리소스의 로컬 복사본을이 저장소 계정을 제공: https://hdiconfigactions.blob.core.windows.net/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-199">In hello Spark and R customized cluster samples provided in hello documentation, for example, we have made a local copy of hello resources in this Storage account: https://hdiconfigactions.blob.core.windows.net/.</span></span>
* <span data-ttu-id="4ba69-200">Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인</span><span class="sxs-lookup"><span data-stu-id="4ba69-200">Ensure that hello cluster customization script is idempotent</span></span>

    <span data-ttu-id="4ba69-201">Hello 클러스터 수명 동안 HDInsight 클러스터의 노드 hello를 이미지로 다시 설치를 예상 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-201">You must expect that hello nodes of an HDInsight cluster is reimaged during hello cluster lifetime.</span></span> <span data-ttu-id="4ba69-202">클러스터를 이미지로 다시 설치할 때마다 hello 클러스터 사용자 지정 스크립트가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-202">hello cluster customization script is run whenever a cluster is reimaged.</span></span> <span data-ttu-id="4ba69-203">이 스크립트를 이미지로 다시 설치 시 hello 스크립트 해당 hello 클러스터 상태에 있었던 경우 hello 클러스터 처음부터 처음으로 hello에 대 한 hello 스크립트 실행 한 후에 사용자 지정 된 동일한 toohello 반환 확인 해야 하는 hello 의미에서 설계 된 toobe idempotent 있어야 합니다. 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-203">This script must be designed toobe idempotent in hello sense that upon reimaging, hello script should ensure that hello cluster is returned toohello same customized state that it was in just after hello script ran for hello first time when hello cluster was initially created.</span></span> <span data-ttu-id="4ba69-204">예를 들어 사용자 지정 스크립트에 D:\AppLocation에서 응용 프로그램을 설치 하는 경우 첫 번째 실행 한 다음, 이미지로 다시 설치 시 각 후속 실행 시 hello 스크립트 hello 응용 프로그램 hello 다른를 계속 하기 전에 D:\AppLocation 위치에 있는지 여부를 확인 해야 hello 스크립트의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-204">For example, if a custom script installed an application at D:\AppLocation on its first run, then on each subsequent run, upon reimaging, hello script should check whether hello application exists at hello D:\AppLocation location before proceeding with other steps in hello script.</span></span>
* <span data-ttu-id="4ba69-205">Hello 최적의 위치에 사용자 지정 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-205">Install custom components in hello optimal location</span></span>

    <span data-ttu-id="4ba69-206">클러스터 노드를 이미지로 다시 설치 되 면 hello C:\ 리소스 드라이브 및 D:\ 드라이브 수를 다시 포맷, 데이터 및 해당 드라이브에 설치 하는 응용 프로그램의 hello 손실.</span><span class="sxs-lookup"><span data-stu-id="4ba69-206">When cluster nodes are reimaged, hello C:\ resource drive and D:\ system drive can be reformatted, resulting in hello loss of data and applications that had been installed on those drives.</span></span> <span data-ttu-id="4ba69-207">또한 hello 클러스터의 일부인 Azure 가상 컴퓨터 (VM) 노드는 작동이 중단 되며 새 노드도 대체 됩니다 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-207">This could also happen if an Azure virtual machine (VM) node that is part of hello cluster goes down and is replaced by a new node.</span></span> <span data-ttu-id="4ba69-208">Hello 클러스터에서 hello C:\apps 위치 또는 hello D:\ 드라이브에 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-208">You can install components on hello D:\ drive or in hello C:\apps location on hello cluster.</span></span> <span data-ttu-id="4ba69-209">Hello C:\ 드라이브에서 다른 위치에 모두 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-209">All other locations on hello C:\ drive are reserved.</span></span> <span data-ttu-id="4ba69-210">Hello 응용 프로그램 또는 라이브러리 놓이는 위치 toobe hello 클러스터 사용자 지정 스크립트에 설치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-210">Specify hello location where applications or libraries are toobe installed in hello cluster customization script.</span></span>
* <span data-ttu-id="4ba69-211">Hello 클러스터 아키텍처의 고가용성을 보장</span><span class="sxs-lookup"><span data-stu-id="4ba69-211">Ensure high availability of hello cluster architecture</span></span>

    <span data-ttu-id="4ba69-212">HDInsight는 액티브-패시브 아키텍처 고가용성을 위해, 헤드 노드는 어느 한 헤드 노드는 활성 모드 (hello HDInsight 서비스 실행)이 고 다른 hello에서 (어떤 HDInsight에서 서비스가 실행 되지 않는) 대기 모드에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-212">HDInsight has an active-passive architecture for high availability, in which one head node is in active mode (where hello HDInsight services are running) and hello other head node is in standby mode (in which HDInsight services are not running).</span></span> <span data-ttu-id="4ba69-213">HDInsight 서비스는 중단 되는 경우 활성 노드와 수동 모드를 전환 하는 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="4ba69-213">hello nodes switch active and passive modes if HDInsight services are interrupted.</span></span> <span data-ttu-id="4ba69-214">고가용성을 위해 두 헤드 노드에 사용 되는 tooinstall 서비스 스크립트 동작을 사용 하는 경우 해당 hello HDInsight 장애 조치 메커니즘 않습니다 수 tooautomatically 장애가 사용자 설치 서비스를 대신 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-214">If a script action is used tooinstall services on both head nodes for high availability, note that hello HDInsight failover mechanism is not able tooautomatically fail over these user-installed services.</span></span> <span data-ttu-id="4ba69-215">따라서 사용자 설치 서비스를 HDInsight 헤드 노드에 항상 사용 가능한 예상된 toobe 액티브-패시브 모드에 있는 경우 장애 조치 메커니즘이 자신의 하거나 액티브-액티브 모드로 설정 해야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-215">So user-installed services on HDInsight head nodes that are expected toobe highly available must either have their own failover mechanism if in active-passive mode or be in active-active mode.</span></span>

    <span data-ttu-id="4ba69-216">Hello 헤드 노드 역할 hello에 값으로 지정 하는 경우 헤드 노드 모두에서 실행 되는 HDInsight 스크립트 동작 명령 *ClusterRoleCollection* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-216">An HDInsight Script Action command runs on both head nodes when hello head-node role is specified as a value in hello *ClusterRoleCollection* parameter.</span></span> <span data-ttu-id="4ba69-217">따라서 사용자 지정 스크립트를 설계할 때는 스크립트에서 이 설정을 인식하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-217">So when you design a custom script, make sure that your script is aware of this setup.</span></span> <span data-ttu-id="4ba69-218">여기서 hello 동일한 서비스 설치 되 고 hello 헤드 노드 모두에서 시작 하 고 서로 경쟁 결국 문제를 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="4ba69-218">You should not run into problems where hello same services are installed and started on both of hello head nodes and they end up competing with each other.</span></span> <span data-ttu-id="4ba69-219">또한, 주의 이미지로 다시 설치 하는 동안 데이터는 손실 되므로 스크립트 동작을 통해 설치 된 소프트웨어는 toobe 탄력적인 toosuch 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-219">Also, be aware that data is lost during reimaging, so software installed via Script Action has toobe resilient toosuch events.</span></span> <span data-ttu-id="4ba69-220">응용 프로그램 디자인 된 toowork 여러 노드 간에 분산 되는 항상 사용 가능한 데이터를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-220">Applications should be designed toowork with highly available data that is distributed across many nodes.</span></span> <span data-ttu-id="4ba69-221">클러스터의 노드 hello의 1/5로 수 이미지로 다시 설치할 수 hello에 참고 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-221">Note that as many as 1/5 of hello nodes in a cluster can be reimaged at hello same time.</span></span>
* <span data-ttu-id="4ba69-222">Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="4ba69-222">Configure hello custom components toouse Azure Blob storage</span></span>

    <span data-ttu-id="4ba69-223">hello 클러스터 노드에 설치 하는 hello 사용자 지정 구성 요소는 기본 구성 toouse Hadoop 분산 파일 시스템 (HDFS) 저장소에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-223">hello custom components that you install on hello cluster nodes might have a default configuration toouse Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="4ba69-224">Hello 구성 toouse Azure Blob 저장소를 대신 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-224">You should change hello configuration toouse Azure Blob storage instead.</span></span> <span data-ttu-id="4ba69-225">클러스터에 이미지로 다시 설치 hello HDFS 파일 시스템 포맷 가져옵니다 하 고 저장 된 모든 데이터는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-225">On a cluster reimage, hello HDFS file system gets formatted and you would lose any data that is stored there.</span></span> <span data-ttu-id="4ba69-226">대신 Azure Blob Storage를 사용하면 데이터가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-226">Using Azure Blob storage instead ensures that your data is retained.</span></span>

## <a name="common-usage-patterns"></a><span data-ttu-id="4ba69-227">일반적인 사용 패턴</span><span class="sxs-lookup"><span data-stu-id="4ba69-227">Common usage patterns</span></span>
<span data-ttu-id="4ba69-228">이 섹션에서 사용자 고유의 사용자 지정 스크립트를 작성 하는 동안에 실행 될 수 있는 hello 일반적인 사용 패턴을 구현 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-228">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="configure-environment-variables"></a><span data-ttu-id="4ba69-229">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="4ba69-229">Configure environment variables</span></span>
<span data-ttu-id="4ba69-230">종종 스크립트 작업 개발 중 이며 보이면 hello tooset 환경 변수를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-230">Often in script action development, you feel hello need tooset environment variables.</span></span> <span data-ttu-id="4ba69-231">예를 들어 가장 가능성이 높은 시나리오는 이진 외부 사이트에서 다운로드 하 고 hello 클러스터에 설치 위치는 설치 된 tooyour 'PATH' 환경 변수의 hello 위치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-231">For instance, a most likely scenario is when you download a binary from an external site, install it on hello cluster, and add hello location of where it is installed tooyour ‘PATH’ environment variable.</span></span> <span data-ttu-id="4ba69-232">다음 코드 조각 hello tooset 환경 변수에서 사용자 지정 스크립트를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-232">hello following snippet shows you how tooset environment variables in hello custom script.</span></span>

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

<span data-ttu-id="4ba69-233">Hello 환경 변수를 설정 하는이 문을 **MDS_RUNNER_CUSTOM_CLUSTER** toohello 값 'true' 및 집합 hello이 변수 toobe 전체 컴퓨터의 범위.</span><span class="sxs-lookup"><span data-stu-id="4ba69-233">This statement sets hello environment variable **MDS_RUNNER_CUSTOM_CLUSTER** toohello value 'true' and also sets hello scope of this variable toobe machine-wide.</span></span> <span data-ttu-id="4ba69-234">시간에 반드시 환경 변수 hello 적절 한 범위-컴퓨터 또는 사용자에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-234">At times it is important that environment variables are set at hello appropriate scope – machine or user.</span></span> <span data-ttu-id="4ba69-235">환경 변수 설정에 대한 자세한 내용은 [여기][1]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-235">Refer [here][1] for more information on setting environment variables.</span></span>

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="4ba69-236">Hello 사용자 지정 스크립트를 저장할 toolocations 액세스</span><span class="sxs-lookup"><span data-stu-id="4ba69-236">Access toolocations where hello custom scripts are stored</span></span>
<span data-ttu-id="4ba69-237">사용 되는 스크립트 toocustomize 클러스터 요구 tooeither hello 클러스터에 대 한 hello 기본 저장소 계정 또는 다른 저장소 계정에 읽기 전용 컨테이너를 공용 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-237">Scripts used toocustomize a cluster needs tooeither be in hello default storage account for hello cluster or in a public read-only container on any other storage account.</span></span> <span data-ttu-id="4ba69-238">공개적으로 액세스할 수 있는 toobe 작업이 필요한 스크립트 리소스의 다른 위치 액세스 하는 경우 (적어도 공개 읽기 전용).</span><span class="sxs-lookup"><span data-stu-id="4ba69-238">If your script accesses resources located elsewhere these need toobe in a publicly accessible (at least public read-only).</span></span> <span data-ttu-id="4ba69-239">예를 들어 tooaccess 파일을 원하는 하 고 hello SaveFile HDI 명령을 사용 하 여 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-239">For instance you might want tooaccess a file and save it using hello SaveFile-HDI command.</span></span>

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

<span data-ttu-id="4ba69-240">이 예제에서는 해당 hello 컨테이너 'somecontainer' 저장소 계정 'somestorageaccount'에 공개적으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-240">In this example, you must ensure that hello container 'somecontainer' in storage account 'somestorageaccount' is publicly accessible.</span></span> <span data-ttu-id="4ba69-241">그렇지 않으면 hello 스크립트 ' 찾을 수 없음 ' 예외를 throw 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-241">Otherwise, hello script throws a ‘Not Found’ exception and fail.</span></span>

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a><span data-ttu-id="4ba69-242">추가 AzureRmHDInsightScriptAction toohello cmdlet 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="4ba69-242">Pass parameters toohello Add-AzureRmHDInsightScriptAction cmdlet</span></span>
<span data-ttu-id="4ba69-243">toopass 여러 매개 변수 추가 AzureRmHDInsightScriptAction toohello cmdlet hello 스크립트에 대 한 tooformat hello 문자열 값 toocontain 모든 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-243">toopass multiple parameters toohello Add-AzureRmHDInsightScriptAction cmdlet, you need tooformat hello string value toocontain all parameters for hello script.</span></span> <span data-ttu-id="4ba69-244">예:</span><span class="sxs-lookup"><span data-stu-id="4ba69-244">For example:</span></span>

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

<span data-ttu-id="4ba69-245">또는</span><span class="sxs-lookup"><span data-stu-id="4ba69-245">or</span></span>

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a><span data-ttu-id="4ba69-246">실패한 클러스터 배포에 대한 예외 발생</span><span class="sxs-lookup"><span data-stu-id="4ba69-246">Throw exception for failed cluster deployment</span></span>
<span data-ttu-id="4ba69-247">Tooget hello 팩트의 정확 하 게 알림이 표시 하려는 경우 클러스터 사용자 지정 예상 대로 실패을 중요 한 toothrow 예외로 hello 클러스터 만들기 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-247">If you want tooget accurately notified of hello fact that cluster customization did not succeed as expected, it is important toothrow an exception and fail hello cluster creation.</span></span> <span data-ttu-id="4ba69-248">예를 들어,이 특성이 있으면 tooprocess 파일을 사용할 수도 있으며 hello 파일이 존재 하지 않습니다 hello 오류 사례를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-248">For instance, you might want tooprocess a file if it exists and handle hello error case where hello file does not exist.</span></span> <span data-ttu-id="4ba69-249">이렇게 하면 hello 스크립트 정상적으로 종료 하 고 hello hello 클러스터 상태가 올바르게 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-249">This would ensure that hello script exits gracefully and hello state of hello cluster is correctly known.</span></span> <span data-ttu-id="4ba69-250">hello 다음 조각은 방법의 예로 tooachieve이:</span><span class="sxs-lookup"><span data-stu-id="4ba69-250">hello following snippet gives an example of how tooachieve this:</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

<span data-ttu-id="4ba69-251">이 코드 조각에서 hello 파일 존재 하지 않는 경우 hello 스크립트 hello 오류 메시지를 인쇄 후 정상적으로 실제로 종료 하 고 hello 클러스터에 클러스터 사용자 지정 프로세스를 완료 "했습니다" 것으로 가정 하는 실행 중인 상태에 도달 하면 있는 tooa 상태를 저하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-251">In this snippet, if hello file did not exist, it would lead tooa state where hello script actually exits gracefully after printing hello error message, and hello cluster reaches running state assuming it "successfully" completed cluster customization process.</span></span> <span data-ttu-id="4ba69-252">Toobe hello 팩트의 정확 하 게 알림이 표시 하려는 경우 해당 클러스터 사용자 지정 항목 기본적으로 완료 하지 못했습니다 된 누락 된 파일로 인해 예상 대로 더 적절 한 toothrow 예외는 hello 클러스터 사용자 지정 단계에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-252">If you want toobe accurately notified of hello fact that cluster customization essentially did not succeed as expected because of a missing file, it is more appropriate toothrow an exception and fail hello cluster customization step.</span></span> <span data-ttu-id="4ba69-253">tooachieve이 샘플 코드 조각은 대신 다음 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-253">tooachieve this you must use hello following sample code snippet instead.</span></span>

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a><span data-ttu-id="4ba69-254">스크립트 작업 배포를 위한 검사 목록</span><span class="sxs-lookup"><span data-stu-id="4ba69-254">Checklist for deploying a script action</span></span>
<span data-ttu-id="4ba69-255">이러한 스크립트 toodeploy를 준비할 때 했습니다 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-255">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

1. <span data-ttu-id="4ba69-256">Hello 배포 하는 동안 hello 클러스터 노드에서 액세스할 수 있는 위치에서 사용자 지정 스크립트를 포함 하는 hello 파일을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-256">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="4ba69-257">이 hello 기본 또는 클러스터 배포 또는 다른 공개적으로 액세스할 수 있는 저장소 컨테이너의 hello 시 지정 하는 추가 저장소 계정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-257">This can be any of hello default or additional Storage accounts specified at hello time of cluster deployment, or any other publicly accessible storage container.</span></span>
2. <span data-ttu-id="4ba69-258">스크립트 toomake 보내지게를 실행 하 고 있는지에 대 한 검사를 추가 하 여 hello 스크립트 hello에 여러 번 실행 될 수 있도록 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="4ba69-258">Add checks into scripts toomake sure that they execute idempotently, so that hello script can be executed multiple times on hello same node.</span></span>
3. <span data-ttu-id="4ba69-259">사용 하 여 hello **Write-output** STDERR 뿐만 아니라 Azure PowerShell cmdlet tooprint tooSTDOUT 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-259">Use hello **Write-Output** Azure PowerShell cmdlet tooprint tooSTDOUT as well as STDERR.</span></span> <span data-ttu-id="4ba69-260">**Write-Host**를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4ba69-260">Do not use **Write-Host**.</span></span>
4. <span data-ttu-id="4ba69-261">$Env 같은 임시 파일 폴더를 사용 하 여: 임시 tookeep hello 스크립트에서 사용 하는 다운로드 한 파일 hello 및 다음 스크립트를 실행 한 후를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-261">Use a temporary file folder, such as $env:TEMP, tookeep hello downloaded file used by hello scripts and then clean them up after scripts have executed.</span></span>
5. <span data-ttu-id="4ba69-262">D:\ 또는 C:\apps에만 사용자 지정 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-262">Install custom software only at D:\ or C:\apps.</span></span> <span data-ttu-id="4ba69-263">Hello c: 드라이브에서 다른 위치에는 예약 되어으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-263">Other locations on hello C: drive should not be used as they are reserved.</span></span> <span data-ttu-id="4ba69-264">Note hello C:\apps 폴더 외부 hello c: 드라이브에 파일을 설치 hello 노드의 reimages 하는 동안 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-264">Note that installing files on hello C: drive outside of hello C:\apps folder may result in setup failures during reimages of hello node.</span></span>
6. <span data-ttu-id="4ba69-265">Hello 이벤트의 운영 체제 수준을 설정 또는 Hadoop 서비스 구성 파일 변경 된 경우에 hello 스크립트에서 설정 하는 hello 환경 변수와 같은 모든 운영 체제 수준 설정을 선택할 수 없도록 toorestart HDInsight 서비스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-265">In hello event that OS-level settings or Hadoop service configuration files were changed, you may want toorestart HDInsight services so that they can pick up any OS-level settings, such as hello environment variables set in hello scripts.</span></span>

## <a name="debug-custom-scripts"></a><span data-ttu-id="4ba69-266">사용자 지정 스크립트 디버그</span><span class="sxs-lookup"><span data-stu-id="4ba69-266">Debug custom scripts</span></span>
<span data-ttu-id="4ba69-267">hello 스크립트 오류 로그는 생성 시 hello 클러스터에 대해 지정한 hello 기본 저장소 계정에서 다른 출력과 함께 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-267">hello script error logs are stored, along with other output, in hello default Storage account that you specified for hello cluster at its creation.</span></span> <span data-ttu-id="4ba69-268">hello 로그 테이블에 저장 됩니다는 hello 이름의 *u < \cluster-name-fragment >< \time-stamp > setuplog*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-268">hello logs are stored in a table with hello name *u<\cluster-name-fragment><\time-stamp>setuplog*.</span></span> <span data-ttu-id="4ba69-269">이들은 hello 노드 (작업자 노드 및 헤드 노드)는 hello에 스크립트 hello 클러스터에서 실행 된 모든 레코드가 있는 집계 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-269">These are aggregated logs that have records from all of hello nodes (head node and worker nodes) on which hello script runs in hello cluster.</span></span>
<span data-ttu-id="4ba69-270">Visual Studio 용 HDInsight 도구는 쉽게 toocheck hello 로그는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-270">An easy way toocheck hello logs is toouse HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="4ba69-271">Hello 도구를 설치 하기 위한 참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="4ba69-271">For installing hello tools, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)</span></span>

<span data-ttu-id="4ba69-272">**Visual Studio를 사용 하 여 toocheck hello 로그**</span><span class="sxs-lookup"><span data-stu-id="4ba69-272">**toocheck hello log using Visual Studio**</span></span>

1. <span data-ttu-id="4ba69-273">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-273">Open Visual Studio.</span></span>
2. <span data-ttu-id="4ba69-274">**보기**를 클릭하고 **서버 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-274">Click **View**, and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="4ba69-275">"Azure" 단추로 클릭 하 고, 연결을 너무 클릭**Microsoft Azure 구독**, 한 다음 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-275">Right-click "Azure", click Connect too**Microsoft Azure Subscriptions**, and then enter your credentials.</span></span>
4. <span data-ttu-id="4ba69-276">확장 **저장소**, hello 기본 파일 시스템으로 사용 하는 hello Azure 저장소 계정, **테이블**, hello 테이블 이름을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-276">Expand **Storage**, expand hello Azure storage account used as hello default file system, expand **Tables**, and then double-click hello table name.</span></span>

<span data-ttu-id="4ba69-277">클러스터 노드 toosee hello에도 원격 수 STDOUT 및 STDERR에 대 한 사용자 지정 스크립트를 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-277">You can also remote into hello cluster nodes toosee both STDOUT and STDERR for custom scripts.</span></span> <span data-ttu-id="4ba69-278">hello 각 노드의 로그만 특정 toothat 노드 되며 로그인 **C:\HDInsightLogs\DeploymentAgent.log**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-278">hello logs on each node are specific only toothat node and are logged into **C:\HDInsightLogs\DeploymentAgent.log**.</span></span> <span data-ttu-id="4ba69-279">이러한 로그 파일 hello 사용자 지정 스크립트의 모든 출력을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-279">These log files record all outputs from hello custom script.</span></span> <span data-ttu-id="4ba69-280">Spark 스크립트 작업에 대한 예제 로그 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-280">An example log snippet for a Spark script action looks like this:</span></span>

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


<span data-ttu-id="4ba69-281">이 로그에이 명확한 경우 hello Spark 스크립트 동작이 hello HEADNODE0 이라는 VM에서 실행 되 고 예외가 hello 실행 하는 동안 throw 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-281">In this log, it is clear that hello Spark script action has been executed on hello VM named HEADNODE0 and that no exceptions were thrown during hello execution.</span></span>

<span data-ttu-id="4ba69-282">실행 오류가 발생 하는 hello 이벤트에서 것을 설명 하는 hello 출력이 로그 파일에도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-282">In hello event that an execution failure occurs, hello output describing it is also contained in this log file.</span></span> <span data-ttu-id="4ba69-283">이러한 로그에 제공 된 hello 정보 발생할 수 있는 스크립트 문제 디버깅에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba69-283">hello information provided in these logs should be helpful in debugging script problems that may arise.</span></span>

## <a name="see-also"></a><span data-ttu-id="4ba69-284">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4ba69-284">See also</span></span>
* <span data-ttu-id="4ba69-285">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-cluster-customize]</span><span class="sxs-lookup"><span data-stu-id="4ba69-285">[Customize HDInsight clusters using Script Action][hdinsight-cluster-customize]</span></span>
* <span data-ttu-id="4ba69-286">[HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="4ba69-286">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="4ba69-287">[HDInsight 클러스터에서 R 설치 및 사용][hdinsight-r-scripts]</span><span class="sxs-lookup"><span data-stu-id="4ba69-287">[Install and use R on HDInsight clusters][hdinsight-r-scripts]</span></span>
* <span data-ttu-id="4ba69-288">[HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)</span><span class="sxs-lookup"><span data-stu-id="4ba69-288">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="4ba69-289">[HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)</span><span class="sxs-lookup"><span data-stu-id="4ba69-289">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
