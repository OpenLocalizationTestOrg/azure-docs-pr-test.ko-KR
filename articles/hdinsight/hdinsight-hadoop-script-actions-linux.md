---
title: "Linux 기반 HDInsight를 사용하여 스크립트 작업 개발 - Azure | Microsoft Docs"
description: "Bash 스크립트를 사용하여 Linux 기반 HDInsight 클러스터를 사용자 지정하는 방법을 알아봅니다. HDInsight의 스크립트 작업 기능을 사용하면 클러스터를 생성하는 동안 또는 생성한 후에 스크립트를 실행할 수 있습니다. 클러스터 구성 설정을 변경하거나 추가 소프트웨어를 설치하는 데 스크립트를 사용할 수 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="2ba24-105">HDInsight를 사용하여 스크립트 작업 개발</span><span class="sxs-lookup"><span data-stu-id="2ba24-105">Script action development with HDInsight</span></span>

<span data-ttu-id="2ba24-106">Bash 스크립트를 사용하여 HDInsight 클러스터를 사용자 지정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="2ba24-107">스크립트 작업은 클러스터를 만드는 동안 또는 만든 후에 HDInsight를 사용자 지정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ba24-108">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2ba24-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2ba24-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="2ba24-111">스크립트 작업 정의</span><span class="sxs-lookup"><span data-stu-id="2ba24-111">What are script actions</span></span>

<span data-ttu-id="2ba24-112">스크립트 작업은 Azure가 구성을 변경하거나 소프트웨어를 설치하기 위해 클러스터 노드에서 실행하는 Bash 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="2ba24-113">스크립트 작업은 루트로 실행되며 클러스터 노드에 대한 모든 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="2ba24-114">스크립트 작업은 다음 방법을 통해 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="2ba24-115">이 방법을 사용하여 스크립트를 적용...</span><span class="sxs-lookup"><span data-stu-id="2ba24-115">Use this method to apply a script...</span></span> | <span data-ttu-id="2ba24-116">클러스터를 생성하는 동안...</span><span class="sxs-lookup"><span data-stu-id="2ba24-116">During cluster creation...</span></span> | <span data-ttu-id="2ba24-117">실행 중인 클러스터에서...</span><span class="sxs-lookup"><span data-stu-id="2ba24-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="2ba24-118">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2ba24-118">Azure portal</span></span> |<span data-ttu-id="2ba24-119">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-119">✓</span></span> |<span data-ttu-id="2ba24-120">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-120">✓</span></span> |
| <span data-ttu-id="2ba24-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ba24-121">Azure PowerShell</span></span> |<span data-ttu-id="2ba24-122">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-122">✓</span></span> |<span data-ttu-id="2ba24-123">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-123">✓</span></span> |
| <span data-ttu-id="2ba24-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2ba24-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="2ba24-125">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-125">✓</span></span> |
| <span data-ttu-id="2ba24-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2ba24-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="2ba24-127">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-127">✓</span></span> |<span data-ttu-id="2ba24-128">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-128">✓</span></span> |
| <span data-ttu-id="2ba24-129">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="2ba24-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="2ba24-130">✓</span><span class="sxs-lookup"><span data-stu-id="2ba24-130">✓</span></span> |&nbsp; |

<span data-ttu-id="2ba24-131">이러한 방법을 사용하여 스크립트 작업을 적용하는 데 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="2ba24-132"><a name="bestPracticeScripting"></a>스크립트 개발을 위한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="2ba24-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="2ba24-133">HDInsight 클러스터용으로 사용자 지정 스크립트를 개발할 때 유의해야 하는 몇 가지 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="2ba24-134">Hadoop 버전 대상</span><span class="sxs-lookup"><span data-stu-id="2ba24-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="2ba24-135">OS 버전 대상</span><span class="sxs-lookup"><span data-stu-id="2ba24-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="2ba24-136">스크립트 리소스에 대한 안정적인 링크 제공</span><span class="sxs-lookup"><span data-stu-id="2ba24-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="2ba24-137">사전 컴파일한 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="2ba24-138">클러스터 사용자 지정 스크립트가 멱등원인지 확인</span><span class="sxs-lookup"><span data-stu-id="2ba24-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="2ba24-139">클러스터 아키텍처의 고가용성 확인</span><span class="sxs-lookup"><span data-stu-id="2ba24-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="2ba24-140">Azure Blob 저장소를 사용하도록 사용자 지정 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="2ba24-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="2ba24-141">STDOUT 및 STDERR에 정보 쓰기</span><span class="sxs-lookup"><span data-stu-id="2ba24-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="2ba24-142">줄 끝을 LF인 파일을 ASCII로 저장</span><span class="sxs-lookup"><span data-stu-id="2ba24-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="2ba24-143">다시 시도 논리를 사용하여 일시적 오류에서 복구</span><span class="sxs-lookup"><span data-stu-id="2ba24-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="2ba24-144">스크립트 작업은 60분 이내에 완료하지 않으면 프로세스에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="2ba24-145">노드 프로비전 중에는 스크립트가 다른 설정 및 구성 프로세스와 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="2ba24-146">CPU 시간 또는 네트워크 대역폭 등의 리소스에 대한 경합으로 인해 스크립트 실행이 개발 환경에서보다 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="2ba24-147"><a name="bPS1"></a>Hadoop 버전 대상</span><span class="sxs-lookup"><span data-stu-id="2ba24-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="2ba24-148">HDInsight의 서로 다른 버전에는 설치된 Hadoop 서비스 및 구성 요소의 서로 다른 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="2ba24-149">스크립트가 특정 버전의 서비스 또는 구성 요소를 기대하는 경우 필수 구성 요소를 포함하는 HDInsight의 버전으로 스크립트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="2ba24-150">[HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서를 사용하여 HDInsight가 포함된 구성 요소 버전에 대한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="2ba24-151"><a name="bps10"></a> OS 버전 대상</span><span class="sxs-lookup"><span data-stu-id="2ba24-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="2ba24-152">Linux 기반 HDInsight는 Ubuntu Linux 배포를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="2ba24-153">HDInsight는 버전이 다르면 다른 버전의 Ubuntu에 의존하는데 이는 스크립트 동작 방식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="2ba24-154">예를 들어 HDInsight 3.4 이전 버전은 Upstart를 사용하는 Ubuntu 버전을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="2ba24-155">버전 3.5는 Systemd를 사용하는 Ubuntu 16.04를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="2ba24-156">Systemd 및 Upstart는 다른 명령에 의존하기 때문에 이를 사용하여 작업하기 위해 스크립트가 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="2ba24-157">HDInsight 3.4와 3.5 간의 또 다른 중요한 차이는 현재 `JAVA_HOME`이 Java 8을 가리킨다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="2ba24-158">`lsb_release`를 사용하여 OS 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="2ba24-159">다음 코드는 Ubuntu 14 또는 16에서 스크립트가 실행되고 있는지 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="2ba24-160">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에서 이러한 코드 조각을 포함하는 전체 스크립트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="2ba24-161">HDInsight에서 사용되는 Ubuntu 버전은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="2ba24-162">Systemd와 Upstart 간의 차이점을 이해하려면 [Upstart 사용자에 대한 Systemd](https://wiki.ubuntu.com/SystemdForUpstartUsers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="2ba24-163"><a name="bPS2"></a>스크립트 리소스에 대한 안정적인 링크 제공</span><span class="sxs-lookup"><span data-stu-id="2ba24-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="2ba24-164">스크립트 및 연결된 리소스는 클러스터의 수명 내내 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="2ba24-165">이러한 리소스는 크기 조정 작업 중 새 노드가 클러스터에 추가되는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="2ba24-166">구독의 Azure Storage 계정에 모든 것을 다운로드하고 보관하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ba24-167">사용된 저장소 계정은 클러스터의 기본 저장소 계정 또는 다른 모든 저장소 계정의 공용 읽기 전용 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="2ba24-168">예를 들어 Microsoft에서 제공하는 샘플은 저장소 계정인 [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) 에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="2ba24-169">HDInsight 팀에서 유지 관리하는 공용, 읽기 전용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="2ba24-170"><a name="bPS4"></a>사전 컴파일한 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="2ba24-171">스크립트 실행 시간을 줄이려면 소스 코드로부터 리소스를 컴파일하는 작업은 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="2ba24-172">예를 들어 리소스를 미리 컴파일하고 HDInsight와 동일한 데이터 센터에서 Azure Storage 계정 Blob에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="2ba24-173"><a name="bPS3"></a>클러스터 사용자 지정 스크립트가 멱등원인지 확인</span><span class="sxs-lookup"><span data-stu-id="2ba24-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="2ba24-174">스크립트는 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-174">Scripts must be idempotent.</span></span> <span data-ttu-id="2ba24-175">스크립트를 여러 번 실행하는 경우 매번 동일한 상태로 클러스터를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="2ba24-176">예를 들어 구성 파일을 수정하는 스크립트는 여러 번 실행하는 경우 중복 항목을 추가해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="2ba24-177"><a name="bPS5"></a>클러스터 아키텍처의 고가용성 확인</span><span class="sxs-lookup"><span data-stu-id="2ba24-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="2ba24-178">Linux 기반 HDInsight 클러스터는 클러스터 내에서 활성화 되는 두 헤드 노드를 제공하며 스크립트 작업은 두 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="2ba24-179">설치하는 구성 요소가 하나의 헤드 노드만 예상하는 경우 두 헤드 노드에 구성 요소를 설치하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2ba24-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ba24-180">HDInsight의 일부로 제공되는 서비스는 두 헤드 노드 간에 필요에 따라 장애 조치하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="2ba24-181">이 기능은 스크립트 작업을 통해 설치된 구성 요소를 사용자 지정하도록 확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="2ba24-182">사용자 지정 구성 요소에 대한 고가용성이 필요한 경우 사용자 고유의 장애 조치 메커니즘을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="2ba24-183"><a name="bPS6"></a>Azure Blob 저장소를 사용하도록 사용자 지정 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="2ba24-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="2ba24-184">클러스터에 설치하는 구성 요소에는 HDFS(Hadoop 분산 파일 시스템) 저장소를 사용하기 위한 기본 구성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="2ba24-185">HDInsight는 Azure Storage 또는 Data Lake Store를 기본 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="2ba24-186">클러스터가 삭제되는 경우에도 데이터가 지속되는 HDFS 호환 가능 파일 시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="2ba24-187">설치하는 구성 요소가 HDFS 대신 WASB 또는 ADL을 사용하도록 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="2ba24-188">대부분의 작업의 경우 파일 시스템을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="2ba24-189">예를 들어 다음은 giraph-examples.jar 파일을 로컬 파일 시스템에서 클러스터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="2ba24-190">이 예제에서 `hdfs` 명령은 기본 클러스터 저장소를 투명하게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="2ba24-191">일부 작업의 경우 URI를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="2ba24-192">예를 들어 Data Lake Store에 대해 `adl:///example/jars`를 또는 Azure Storage에 대해 `wasb:///example/jars`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="2ba24-193"><a name="bPS7"></a>STDOUT 및 STDERR에 정보 쓰기</span><span class="sxs-lookup"><span data-stu-id="2ba24-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="2ba24-194">HDInsight는 STDOUT 및 STDERR로 작성된 스크립트 출력을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="2ba24-195">Ambari 웹 UI를 사용하여 이 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="2ba24-196">Ambari는 클러스터를 정상적으로 만든 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="2ba24-197">클러스터를 만드는 동안 스크립트 작업을 사용하며 만들기에 실패하는 경우 문제 해결 섹션 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) 에서 로깅된 정보에 액세스하는 다른 방법을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="2ba24-198">대부분의 유틸리티 및 설치 패키지는 STDOUT 및 STDERR에 정보를 쓰지만 추가 로깅을 추가하려 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="2ba24-199">텍스트를 STDOUT에 보내려면 `echo`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="2ba24-200">예:</span><span class="sxs-lookup"><span data-stu-id="2ba24-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="2ba24-201">기본적으로 `echo`는 STDOUT에 문자열을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="2ba24-202">STDERR에 전달하려면 `echo` 앞에 `>&2`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="2ba24-203">예:</span><span class="sxs-lookup"><span data-stu-id="2ba24-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="2ba24-204">이는 STDOUT에 작성된 정보를 STDERR(2)로 대신 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="2ba24-205">IO 리디렉션에 대한 자세한 내용은 [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="2ba24-206">스크립트 동작에서 기록된 정보 보기에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="2ba24-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="2ba24-207"><a name="bps8"></a> 줄 끝을 LF인 파일을 ASCII로 저장</span><span class="sxs-lookup"><span data-stu-id="2ba24-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="2ba24-208">Bash 스크립트는 LF에서 종료한 줄을 사용하여 ASCII 형식으로 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="2ba24-209">UTF-8로 저장되거나 줄 끝으로 CRLF를 사용하는 파일은 다음 오류와 함께 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="2ba24-210"><a name="bps9"></a> 다시 시도 논리를 사용하여 일시적 오류에서 복구</span><span class="sxs-lookup"><span data-stu-id="2ba24-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="2ba24-211">파일을 다운로드할 때 apt-get 또는 인터넷을 통해 데이터를 전송하는 기타 작업을 사용하여 패키지를 설치하면 일시적인 네트워킹 오류로 인해 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="2ba24-212">예를 들어 통신하는 원격 리소스가 백업 노드로의 장애 조치(failover) 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="2ba24-213">스크립트를 일시적인 오류에 대해 탄력적으로 만들려면 다시 시도 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="2ba24-214">다음 함수는 재시도 논리를 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="2ba24-215">실패하기 전에 작업을 세 번 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-215">It retries the operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="2ba24-216">다음 예제에서는 이 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="2ba24-217"><a name="helpermethods"></a>사용자 지정 스크립트에 대한 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="2ba24-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="2ba24-218">스크립트 작업 도우미 메서드는 사용자 지정 스크립트를 쓰는 동안 사용할 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="2ba24-219">이러한 메서드는 [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) 스크립트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="2ba24-220">다음을 사용하여 다운로드하고 스크립트의 일부로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="2ba24-221">스크립트에서 사용하기 위해 다음 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="2ba24-222">도우미 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-222">Helper usage</span></span> | <span data-ttu-id="2ba24-223">설명</span><span class="sxs-lookup"><span data-stu-id="2ba24-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="2ba24-224">원본 URI에서 지정된 파일 경로로 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="2ba24-225">기본적으로 기존 파일을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="2ba24-226">(`-xf`를 사용하여) 대상 디렉터리에 tar 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="2ba24-227">클러스터 헤드 노드에서 실행한 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="2ba24-228">현재 노드가 데이터(작업자) 노드인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="2ba24-229">현재 노드가 첫 번째 데이터(작업자) 노드(workernode0이라는 이름)인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="2ba24-230">클러스터에서 헤드 노드의 정규화된 도메인 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="2ba24-231">이름은 쉼표로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-231">Names are comma delimited.</span></span> <span data-ttu-id="2ba24-232">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="2ba24-233">기본 헤드 노드의 정규화된 도메인 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="2ba24-234">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="2ba24-235">보조 헤드 노드의 정규화된 도메인 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="2ba24-236">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="2ba24-237">기본 헤드 노드의 숫자 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="2ba24-238">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="2ba24-239">보조 헤드 노드의 숫자 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="2ba24-240">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="2ba24-241"><a name="commonusage"></a>일반적인 사용 패턴</span><span class="sxs-lookup"><span data-stu-id="2ba24-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="2ba24-242">이 섹션에서는 사용자 고유의 사용자 지정 스크립트를 작성하는 동안 실행할 수 있는 일반적인 사용 패턴 중 일부를 구현하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="2ba24-243">스크립트에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="2ba24-243">Passing parameters to a script</span></span>

<span data-ttu-id="2ba24-244">경우에 따라 스크립트에 매개 변수가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="2ba24-245">예를 들어 Ambari REST API를 사용하는 경우 클러스터에 대한 관리자 암호가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="2ba24-246">스크립트에 전달된 매개 변수는 *위치 매개 변수*로 알려져 있으며 첫 번째 매개 변수의 경우 `$1`, 두 번째는 `$2` 등에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="2ba24-247">`$0` 는 스크립트 자체의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="2ba24-248">매개 변수로 스크립트에 전달되는 값은 작은따옴표(')로 묶여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="2ba24-249">이렇게 하면 전달된 값이 리터럴로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="2ba24-250">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="2ba24-250">Setting environment variables</span></span>

<span data-ttu-id="2ba24-251">환경 변수의 설정은 다음 문으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="2ba24-252">여기서 VARIABLENAME은 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="2ba24-253">변수에 액세스하려면 `$VARIABLENAME`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="2ba24-254">예를 들어 위치 매개 변수에서 제공하는 값을 PASSWORD라는 환경 변수로 할당하려면 다음 문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="2ba24-255">이후 정보에 액세스하려면 `$PASSWORD`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="2ba24-256">스크립트 내에서 설정된 환경 변수는 스크립트의 범위 내에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="2ba24-257">경우에 따라 스크립트가 완료된 후에 유지되는 시스템 수준 환경 변수를 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="2ba24-258">시스템 수준 환경 변수를 추가하려면 `/etc/environment`에 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="2ba24-259">예를 들어 다음 문은 `HADOOP_CONF_DIR`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="2ba24-260">사용자 지정 스크립트가 저장된 위치 액세스</span><span class="sxs-lookup"><span data-stu-id="2ba24-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="2ba24-261">클러스터를 사용자 지정하는 데 사용되는 스크립트는 다음 위치 중 하나에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="2ba24-262">클러스터와 연결된 __Azure Storage 계정__</span><span class="sxs-lookup"><span data-stu-id="2ba24-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="2ba24-263">클러스터와 연결된 __추가 저장소 계정__</span><span class="sxs-lookup"><span data-stu-id="2ba24-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="2ba24-264">__공개적으로 읽을 수 있는 URI__</span><span class="sxs-lookup"><span data-stu-id="2ba24-264">A __publicly readable URI__.</span></span> <span data-ttu-id="2ba24-265">예를 들어 OneDrive, Dropbox 또는 다른 파일 호스팅 서비스에 저장된 데이터에 대한 URL</span><span class="sxs-lookup"><span data-stu-id="2ba24-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="2ba24-266">HDInsight 클러스터와 연결된 __Azure Data Lake Store 계정__</span><span class="sxs-lookup"><span data-stu-id="2ba24-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="2ba24-267">HDInsight와 함께 Azure Data Lake Store를 사용하는 방법에 대한 자세한 내용은 [Data Lake Store를 사용하여 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2ba24-268">HDInsight에서 Data Lake Store에 액세스하는 데 사용하는 서비스 주체에는 스크립트에 대한 읽기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="2ba24-269">스크립트에서 사용되는 리소스는 공개적으로도 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="2ba24-270">Azure Storage 계정 또는 Azure Data Lake Store에서 파일을 저장하면 Azure 네트워크 내에서 두 가지 모두 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="2ba24-271">스크립트를 참조하는 데 사용되는 URI 형식은 사용 중인 서비스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="2ba24-272">HDInsight 클러스터와 연결된 저장소 계정의 경우 `wasb://` 또는 `wasbs://`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="2ba24-273">공개적으로 읽을 수 있는 URI의 경우 `http://` 또는 `https://`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="2ba24-274">Data Lake Store의 경우 `adl://`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="2ba24-275">운영 체제 버전 검사</span><span class="sxs-lookup"><span data-stu-id="2ba24-275">Checking the operating system version</span></span>

<span data-ttu-id="2ba24-276">HDInsight의 다른 버전들은 Ubuntu의 특정 버전에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="2ba24-277">스크립트에서 확인해야 하는 OS 버전 간의 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="2ba24-278">예를 들어 Ubuntu의 버전에 연결된 이진 파일을 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="2ba24-279">OS 버전을 확인하려면 `lsb_release`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="2ba24-280">예를 들어, 다음 스크립트에서 OS 버전에 따라 특정 tar 파일을 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="2ba24-281"><a name="deployScript"></a>스크립트 작업 배포를 위한 검사 목록</span><span class="sxs-lookup"><span data-stu-id="2ba24-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="2ba24-282">이러한 스크립트 배포를 준비할 때 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="2ba24-283">사용자 지정 스크립트가 포함된 파일을 배포 중 클러스터 노드에서 액세스할 수 있는 위치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="2ba24-284">예를 들어 클러스터의 기본 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="2ba24-285">공개적으로 읽을 수 있는 호스팅 서비스에 파일을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="2ba24-286">스크립트가 멱등원인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-286">Verify that the script is impotent.</span></span> <span data-ttu-id="2ba24-287">이렇게 하면 스크립트가 동일한 노드에서 여러 번 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="2ba24-288">임시 파일 디렉터리 /tmp를 사용하여 스크립트에서 사용되는 다운로드된 파일을 보관하고 스크립트가 실행된 후 이 파일을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="2ba24-289">OS 수준 설정 또는 Hadoop 서비스 구성 파일이 변경되면 HDInsight 서비스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="2ba24-290"><a name="runScriptAction"></a>스크립트 작업을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="2ba24-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="2ba24-291">스크립트 작업을 사용하여 다음 메서드를 사용하여 HDInsight 클러스터를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="2ba24-292">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2ba24-292">Azure portal</span></span>
* <span data-ttu-id="2ba24-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ba24-293">Azure PowerShell</span></span>
* <span data-ttu-id="2ba24-294">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="2ba24-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="2ba24-295">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2ba24-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="2ba24-296">각 메서드 사용에 대한 자세한 내용은 [스크립트 작업을 사용하는 방법](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="2ba24-297"><a name="sampleScripts"></a>사용자 지정 스크립트 샘플</span><span class="sxs-lookup"><span data-stu-id="2ba24-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="2ba24-298">Microsoft에서는 HDInsight 클러스터에 구성 요소를 설치하는 샘플 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="2ba24-299">더 많은 예제 스크립트 작업은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ba24-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="2ba24-300">HDInsight에서 Hue 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="2ba24-301">HDInsight 클러스터에 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="2ba24-302">HDInsight 클러스터에 Giraph 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="2ba24-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="2ba24-303">HDInsight 클러스터에 Mono 설치 또는 업그레이드</span><span class="sxs-lookup"><span data-stu-id="2ba24-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="2ba24-304">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2ba24-304">Troubleshooting</span></span>

<span data-ttu-id="2ba24-305">다음은 개발한 스크립트를 사용할 때 발생할 수 있는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="2ba24-306">**오류**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="2ba24-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="2ba24-307">때로는 `syntax error: unexpected end of file`이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="2ba24-308">*원인*:이 오류는 스크립트에서 줄이 CRLF로 끝날 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="2ba24-309">Unix 시스템은 줄 끝에 LF이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="2ba24-310">스크립트가 Windows 환경에서 작성된 경우 CRLF은 Windows의 많은 텍스트 편집기에서 줄 끝에 흔하게 쓰이기 때문에 이 문제가 가장 자주 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="2ba24-311">*해상도*: 텍스트 편집기에서 옵션인 경우 줄 끝에 LF 또는 Unix 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="2ba24-312">또한 Unix 시스템에서 다음 명령을 사용하여 CRLF는 LF로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="2ba24-313">다음 명령은 CRLF 줄 끝을 LF으로 변경해야 하는 것과 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="2ba24-314">시스템에서 사용할 수 있는 유틸리티에 따라 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="2ba24-315">명령</span><span class="sxs-lookup"><span data-stu-id="2ba24-315">Command</span></span> | <span data-ttu-id="2ba24-316">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2ba24-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="2ba24-317">원본 파일이 .BAK 확장으로 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="2ba24-318">OUTFILE은 끝이 LF인 버전만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="2ba24-319">파일을 직접 수정</span><span class="sxs-lookup"><span data-stu-id="2ba24-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="2ba24-320">OUTFILE은 끝이 LF인 버전만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="2ba24-321">**오류**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="2ba24-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="2ba24-322">*원인*: 스크립트가 바이트 순서 표시(BOM)를 사용하여 UTF-8로 저장될 때 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="2ba24-323">*해상도*: ASCII로 또는 BOM을 사용하지 않고 UTF-8로 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="2ba24-324">Linux 또는 Unix 시스템에서 다음 명령을 사용하여 BOM을 사용하지 않고 파일을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="2ba24-325">`INFILE`을 BOM을 포함하는 파일로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="2ba24-326">`OUTFILE`은 BOM을 사용하지 않고 스크립트를 포함하는 새 파일 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="2ba24-327"><a name="seeAlso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ba24-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="2ba24-328">[스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="2ba24-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="2ba24-329">[HDInsight.NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx) 를 사용하여 HDInsight를 관리하는 .NET 응용 프로그램을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="2ba24-330">[HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) 를 사용하여 REST를 통해 HDInsight 클러스터에서 관리 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ba24-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
