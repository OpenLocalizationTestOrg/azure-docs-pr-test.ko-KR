---
title: "Linux 기반 HDInsight-Azure와 aaaScript 액션 개발 | Microsoft Docs"
description: "Toouse Bash toocustomize Linux 기반 HDInsight 클러스터를 스크립트 하는 방법에 대해 알아봅니다. hello 스크립트 동작 hdinsight 기능은 toorun 스크립트 중 또는 클러스터를 만든 후입니다. 스크립트 추가 소프트웨어를 설치 또는 클러스터 구성 설정을 사용 하는 toochange를 수 있습니다."
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
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="c0975-105">HDInsight를 사용하여 스크립트 작업 개발</span><span class="sxs-lookup"><span data-stu-id="c0975-105">Script action development with HDInsight</span></span>

<span data-ttu-id="c0975-106">자세한 내용은 toocustomize를 이용한 적 사용 하 여 HDInsight 클러스터 어떻게 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="c0975-107">스크립트 작업 중 이나 후 클러스터를 만드는 방법을 toocustomize HDInsight은입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0975-108">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c0975-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c0975-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0975-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="c0975-111">스크립트 작업 정의</span><span class="sxs-lookup"><span data-stu-id="c0975-111">What are script actions</span></span>

<span data-ttu-id="c0975-112">스크립트 작업은 Azure hello 클러스터 노드 toomake 구성 변경에서 실행 되는 Bash 스크립트 하거나 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="c0975-113">스크립트 작업을 루트로, 실행 되 고 권한 toohello 클러스터 노드 전체 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="c0975-114">스크립트 동작 메서드를 다음 hello를 통해 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="c0975-115">이 메서드 tooapply 스크립트를 사용 함</span><span class="sxs-lookup"><span data-stu-id="c0975-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="c0975-116">클러스터를 생성하는 동안...</span><span class="sxs-lookup"><span data-stu-id="c0975-116">During cluster creation...</span></span> | <span data-ttu-id="c0975-117">실행 중인 클러스터에서...</span><span class="sxs-lookup"><span data-stu-id="c0975-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="c0975-118">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c0975-118">Azure portal</span></span> |<span data-ttu-id="c0975-119">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-119">✓</span></span> |<span data-ttu-id="c0975-120">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-120">✓</span></span> |
| <span data-ttu-id="c0975-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0975-121">Azure PowerShell</span></span> |<span data-ttu-id="c0975-122">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-122">✓</span></span> |<span data-ttu-id="c0975-123">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-123">✓</span></span> |
| <span data-ttu-id="c0975-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c0975-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="c0975-125">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-125">✓</span></span> |
| <span data-ttu-id="c0975-126">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c0975-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="c0975-127">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-127">✓</span></span> |<span data-ttu-id="c0975-128">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-128">✓</span></span> |
| <span data-ttu-id="c0975-129">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c0975-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="c0975-130">✓</span><span class="sxs-lookup"><span data-stu-id="c0975-130">✓</span></span> |&nbsp; |

<span data-ttu-id="c0975-131">이러한 메서드 tooapply 스크립트 동작을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="c0975-132"><a name="bestPracticeScripting"></a>스크립트 개발을 위한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="c0975-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="c0975-133">HDInsight 클러스터에 대 한 사용자 지정 스크립트를 개발할 때 염두에 몇 가지 모범 사례 tookeep 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="c0975-134">Hello Hadoop 버전 대상</span><span class="sxs-lookup"><span data-stu-id="c0975-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="c0975-135">대상 hello OS 버전</span><span class="sxs-lookup"><span data-stu-id="c0975-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="c0975-136">안정적인 tooscript 리소스 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="c0975-137">사전 컴파일한 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="c0975-138">Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인</span><span class="sxs-lookup"><span data-stu-id="c0975-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="c0975-139">Hello 클러스터 아키텍처의 고가용성을 보장</span><span class="sxs-lookup"><span data-stu-id="c0975-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="c0975-140">Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="c0975-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="c0975-141">쓰기 정보 tooSTDOUT 및 STDERR</span><span class="sxs-lookup"><span data-stu-id="c0975-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="c0975-142">줄 끝을 LF인 파일을 ASCII로 저장</span><span class="sxs-lookup"><span data-stu-id="c0975-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="c0975-143">일시적인 오류 다시 시도 논리 toorecover를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c0975-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="c0975-144">스크립트 동작 60 분 내에 완료 되어야 하거나 hello 프로세스가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="c0975-145">노드 프로 비전 시 hello 스크립트는 다른 설치 및 구성 프로세스와 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="c0975-146">CPU 시간 또는 네트워크 대역폭 등의 리소스에 대 한 경합은 hello 스크립트 tootake 긴 toofinish 개발 환경에서 사용 하지 않고 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="c0975-147"><a name="bPS1"></a>Hello Hadoop 버전 대상</span><span class="sxs-lookup"><span data-stu-id="c0975-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="c0975-148">HDInsight의 서로 다른 버전에는 설치된 Hadoop 서비스 및 구성 요소의 서로 다른 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="c0975-149">스크립트는 특정 버전의 서비스 또는 구성 요소에는 하는 경우에 hello 필수 구성 요소를 포함 하는 HDInsight의 hello 버전과 hello 스크립트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="c0975-150">자세한 내용은 HDInsight에 포함 된 구성 요소 버전에 hello를 사용 하 여 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c0975-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="c0975-151"><a name="bps10"></a>대상 hello OS 버전</span><span class="sxs-lookup"><span data-stu-id="c0975-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="c0975-152">Linux 기반 HDInsight hello Ubuntu Linux 배포판을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="c0975-153">HDInsight는 버전이 다르면 다른 버전의 Ubuntu에 의존하는데 이는 스크립트 동작 방식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="c0975-154">예를 들어 HDInsight 3.4 이전 버전은 Upstart를 사용하는 Ubuntu 버전을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="c0975-155">버전 3.5는 Systemd를 사용하는 Ubuntu 16.04를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="c0975-156">스크립트 둘 다와 함께 toowork 작성 해야 하므로 다양 한 명령이 Systemd와 Upstart 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="c0975-157">HDInsight 3.4 및 3.5 간의 또 다른 중요 한 차이점은 `JAVA_HOME` tooJava 8 가리키게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="c0975-158">사용 하 여 hello OS 버전을 확인 하면 `lsb_release`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="c0975-159">hello 다음 코드에서는 방법을 toodetermine 경우 hello 스크립트 Ubuntu 14 또는 16에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="c0975-160">이러한 조각은 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에 포함 된 hello 전체 스크립트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="c0975-161">HDInsight에서 사용 되는 Ubuntu hello 버전에서는 참조 hello [HDInsight 구성 요소 버전](hdinsight-component-versioning.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c0975-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="c0975-162">toounderstand hello와의 차이점 Systemd Upstart, 참조 [Upstart 사용자에 대 한 Systemd](https://wiki.ubuntu.com/SystemdForUpstartUsers)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="c0975-163"><a name="bPS2"></a>안정적인 tooscript 리소스 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="c0975-164">hello 스크립트와 관련 된 리소스가 유지 되어야 hello 수명의 hello 클러스터 전체에서 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="c0975-165">이러한 리소스를 새 노드를 작업 크기 조정 하는 동안 toohello 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="c0975-166">hello 가장 좋은 방법은 toodownload 이며 구독에는 Azure 저장소 계정에 모든 항목을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0975-167">사용 된 hello 저장소 계정에는 다른 저장소 계정에 hello 클러스터 또는 공용, 읽기 전용 컨테이너에 대 한 되는 hello 기본 저장소 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="c0975-168">Microsoft에서 제공 하는 hello 예제 hello에 저장 됩니다는 예를 들어 [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="c0975-169">이 hello HDInsight 팀에서 유지 관리 하는 공용, 읽기 전용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="c0975-170"><a name="bPS4"></a>사전 컴파일한 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="c0975-171">tooreduce hello 하나 toorun hello 스크립트 시간, 소스 코드에서 리소스를 컴파일 하는 작업을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="c0975-172">예를 들어 리소스 선컴파일하도록 하 고 hello에 Azure 저장소 계정 blob 보관해 HDInsight와 동일한 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="c0975-173"><a name="bPS3"></a>Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인</span><span class="sxs-lookup"><span data-stu-id="c0975-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="c0975-174">스크립트는 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-174">Scripts must be idempotent.</span></span> <span data-ttu-id="c0975-175">반환 해야 하는 경우 hello 스크립트가 여러 번 실행 되 면 hello 클러스터 toohello 될 때마다 동일한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="c0975-176">예를 들어 구성 파일을 수정하는 스크립트는 여러 번 실행하는 경우 중복 항목을 추가해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="c0975-177"><a name="bPS5"></a>Hello 클러스터 아키텍처의 고가용성을 보장</span><span class="sxs-lookup"><span data-stu-id="c0975-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="c0975-178">Linux 기반 HDInsight 클러스터 hello 클러스터 내에서 활성화 되어 있는 두 개의 헤드 노드를 제공 하 고 두 노드 모두에서 스크립트 동작 실행.</span><span class="sxs-lookup"><span data-stu-id="c0975-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="c0975-179">설치 하는 hello 구성 요소에 예상 되는 헤드 노드를 하나만 있으면 두 헤드 노드에서 hello 구성 요소를 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c0975-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0975-180">서비스 HDInsight의 일부로 제공 되는 디자인 된 toofail 통해 hello 두 헤드 노드 사이의 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="c0975-181">이 기능은 toocustom 구성 요소가 스크립트 동작을 통해 설치 된 연장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="c0975-182">사용자 지정 구성 요소에 대한 고가용성이 필요한 경우 사용자 고유의 장애 조치 메커니즘을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="c0975-183"><a name="bPS6"></a>Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="c0975-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="c0975-184">Hello 클러스터에 설치 하는 구성 요소는 Hadoop 분산 파일 시스템 (HDFS) 저장소를 사용 하는 기본 구성을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="c0975-185">HDInsight은 hello 기본 저장소로 Azure 저장소 서비스 또는 데이터 레이크 저장소 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="c0975-186">둘 다 hello 클러스터를 삭제할 경우에 데이터를 유지 하는 HDFS 호환 되는 파일 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="c0975-187">WASB 또는 HDFS 대신 ADL toouse 설치 tooconfigure 구성 요소를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="c0975-188">대부분의 작업에 대 한 toospecify hello 파일 시스템이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="c0975-189">예를 들어 hello 다음 hello 로컬 파일 시스템 toocluster 저장소에서 hello giraph examples.jar 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="c0975-190">이 예제에서는 hello `hdfs` 명령은 hello 기본 저장소 클러스터에 투명 하 게 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="c0975-191">일부 작업에 대 한 toospecify hello URI를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="c0975-192">예를 들어 Data Lake Store에 대해 `adl:///example/jars`를 또는 Azure Storage에 대해 `wasb:///example/jars`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="c0975-193"><a name="bPS7"></a>쓰기 정보 tooSTDOUT 및 STDERR</span><span class="sxs-lookup"><span data-stu-id="c0975-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="c0975-194">HDInsight은 스크립트 출력을 쓸된 tooSTDOUT 및 STDERR를 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="c0975-195">Hello Ambari web UI를 사용 하 여이 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="c0975-196">Ambari은 hello 클러스터를 성공적으로 만들 경우 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="c0975-197">클러스터 만들기 및 만들기 실패 하는 동안 스크립트 작업을 사용 하는 경우 참조 문제 해결 섹션 hello [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) 로깅되는 정보에 액세스 하는 다른 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="c0975-198">유틸리티 및 설치 패키지를 대부분 이미 쓸 정보 tooSTDOUT 및 STDERR를 되었지만 tooadd 추가 로깅을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="c0975-199">toosend 텍스트 tooSTDOUT 사용 `echo`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="c0975-200">예:</span><span class="sxs-lookup"><span data-stu-id="c0975-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="c0975-201">기본적으로 `echo` 보냅니다 hello 문자열 tooSTDOUT 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="c0975-202">toodirect 것 tooSTDERR, 추가 `>&2` 전에 `echo`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="c0975-203">예:</span><span class="sxs-lookup"><span data-stu-id="c0975-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="c0975-204">이 tooSTDOUT tooSTDERR (2)를 대신 기록 된 정보를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="c0975-205">IO 리디렉션에 대한 자세한 내용은 [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0975-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="c0975-206">스크립트 동작에서 기록된 정보 보기에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="c0975-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="c0975-207"><a name="bps8"></a> 줄 끝을 LF인 파일을 ASCII로 저장</span><span class="sxs-lookup"><span data-stu-id="c0975-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="c0975-208">Bash 스크립트는 LF에서 종료한 줄을 사용하여 ASCII 형식으로 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="c0975-209">파일 또는 u t F-8로 저장 된 CRLF hello 줄 끝으로 사용한 다음 오류가 hello로 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="c0975-210"><a name="bps9"></a>일시적인 오류 다시 시도 논리 toorecover를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c0975-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="c0975-211">파일을 다운로드할 때 인터넷 hello apt get 또는 통해 데이터를 전송 하는 다른 작업을 사용 하 여 패키지를 설치, hello 동작 tootransient 네트워킹 오류로 인해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="c0975-212">예를 들어 hello 원격 리소스와 통신 하는 tooa 백업 노드를 통해 실패의 hello 프로세스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="c0975-213">toomake 스크립트 탄력적인 tootransient 오류를 재시도 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="c0975-214">hello 함수 다음 tooimplement 다시 시도 하는 논리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="c0975-215">세 번 실패 하기 전에 hello 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-215">It retries hello operation three times before failing.</span></span>

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

<span data-ttu-id="c0975-216">hello 다음 예제에 나와 방법을 toouse이이 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="c0975-217"><a name="helpermethods"></a>사용자 지정 스크립트에 대한 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="c0975-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="c0975-218">스크립트 작업 도우미 메서드는 사용자 지정 스크립트를 쓰는 동안 사용할 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="c0975-219">이러한 메서드는 [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) 스크립트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="c0975-220">Hello toodownload를 수행 하 고 스크립트의 일부로 사용:</span><span class="sxs-lookup"><span data-stu-id="c0975-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="c0975-221">다음 스크립트에 사용할 수 있는 도우미 hello:</span><span class="sxs-lookup"><span data-stu-id="c0975-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="c0975-222">도우미 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-222">Helper usage</span></span> | <span data-ttu-id="c0975-223">설명</span><span class="sxs-lookup"><span data-stu-id="c0975-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="c0975-224">Hello 소스 URI toohello 지정 된 파일 경로에서 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="c0975-225">기본적으로 기존 파일을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="c0975-226">Tar 파일 추출 (사용 하 여 `-xf`) toohello 대상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="c0975-227">클러스터 헤드 노드에서 실행한 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="c0975-228">Hello 현재 노드 (작업자) 데이터 노드인 경우 1; 반환 그렇지 않으면 0입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="c0975-229">노드 (명명 된 workernode0) 1; 반환 hello 현재 노드가 hello 첫 번째 데이터 (작업자) 이면 그렇지 않으면 0입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="c0975-230">Hello 클러스터의 hello headnodes의 hello 정규화 된 도메인 이름을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="c0975-231">이름은 쉼표로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-231">Names are comma delimited.</span></span> <span data-ttu-id="c0975-232">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="c0975-233">기본 헤드 노드에 hello의 hello 정규화 된 도메인 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="c0975-234">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="c0975-235">Hello 보조 헤드 노드에의 hello 정규화 된 도메인 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="c0975-236">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="c0975-237">기본 헤드 노드에 hello의 hello 숫자 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="c0975-238">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="c0975-239">Hello 보조 헤드 노드에의 hello 숫자 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="c0975-240">빈 문자열이 오류에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="c0975-241"><a name="commonusage"></a>일반적인 사용 패턴</span><span class="sxs-lookup"><span data-stu-id="c0975-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="c0975-242">이 섹션에서 사용자 고유의 사용자 지정 스크립트를 작성 하는 동안에 실행 될 수 있는 hello 일반적인 사용 패턴을 구현 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="c0975-243">Tooa 스크립트 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="c0975-243">Passing parameters tooa script</span></span>

<span data-ttu-id="c0975-244">경우에 따라 스크립트에 매개 변수가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="c0975-245">예를 들어 hello Ambari REST API를 사용 하는 경우 hello 클러스터에 대 한 hello 관리자 암호를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="c0975-246">Toohello 스크립트에 전달 된 매개 변수 라고 *위치 매개 변수*, 너무 할당 된`$1` hello 첫 번째 매개 변수에 대 한 `$2` 두 번째 및 하므로 on hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="c0975-247">`$0`hello 스크립트 자체의 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="c0975-248">Toohello 스크립트 매개 변수로 전달 된 값을 작은따옴표 (')으로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="c0975-249">이렇게 하면 값이 전달 되는 hello 리터럴로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="c0975-250">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="c0975-250">Setting environment variables</span></span>

<span data-ttu-id="c0975-251">환경 변수를 설정 hello 문 다음에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="c0975-252">여기서 VARIABLENAME는 hello hello 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="c0975-253">tooaccess hello 변수를 사용 하 여 `$VARIABLENAME`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="c0975-254">예를 들어 tooassign 라는 암호 환경 변수로 위치 매개 변수에서 제공 하는 값, 문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="c0975-255">후속 액세스 toohello 정보를 유도할 수 `$PASSWORD`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="c0975-256">Hello 스크립트 내에서 설정한 환경 변수가 hello 스크립트의 hello 범위 내 에서만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="c0975-257">경우에 따라 hello 스크립트가 완료 된 후 지속 되는 tooadd 시스템 수준 환경 변수를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="c0975-258">tooadd 시스템 수준 환경 변수는 hello 변수를 너무 추가`/etc/environment`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="c0975-259">Hello 문 다음의 추가 예를 들어 `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="c0975-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="c0975-260">Hello 사용자 지정 스크립트를 저장할 toolocations 액세스</span><span class="sxs-lookup"><span data-stu-id="c0975-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="c0975-261">사용 되는 스크립트 toocustomize 클러스터 toobe hello 다음 위치 중 하나에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="c0975-262">__Azure 저장소 계정__ hello 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="c0975-263">__추가 저장소 계정__ hello 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="c0975-264">__공개적으로 읽을 수 있는 URI__</span><span class="sxs-lookup"><span data-stu-id="c0975-264">A __publicly readable URI__.</span></span> <span data-ttu-id="c0975-265">예를 들어 한 URL toodata OneDrive, Dropbox, 또는 서비스를 호스트 하는 다른 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="c0975-266">__Azure 데이터 레이크 저장소 계정__ hello HDInsight 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="c0975-267">HDInsight와 함께 Azure Data Lake Store를 사용하는 방법에 대한 자세한 내용은 [Data Lake Store를 사용하여 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0975-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0975-268">hello 서비스 보안 주체 HDInsight 사용 하 여 tooaccess Data Lake 저장소에 대 한 읽기 액세스 toohello 스크립트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="c0975-269">또한 hello 스크립트에 의해 사용 되는 리소스 공개적으로 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="c0975-270">Hello Azure 네트워크 내에서 둘 다로 신속 하 게 액세스할을 제공 hello 파일을 Azure 저장소 계정 또는 Azure 데이터 레이크 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="c0975-271">hello URI 사용 하는 형식 tooreference hello 스크립트 사용 중인 hello 서비스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="c0975-272">Hello HDInsight 클러스터와 연결 된 저장소 계정에 대해 사용 하 여 `wasb://` 또는 `wasbs://`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="c0975-273">공개적으로 읽을 수 있는 URI의 경우 `http://` 또는 `https://`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="c0975-274">Data Lake Store의 경우 `adl://`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="c0975-275">Hello 운영 체제 버전 확인</span><span class="sxs-lookup"><span data-stu-id="c0975-275">Checking hello operating system version</span></span>

<span data-ttu-id="c0975-276">HDInsight의 다른 버전들은 Ubuntu의 특정 버전에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="c0975-277">스크립트에서 확인해야 하는 OS 버전 간의 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="c0975-278">예를 들어 tooinstall Ubuntu의 제한은 toohello 버전이 있는 이진 파일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="c0975-279">toocheck hello OS 버전을 사용 하 여 `lsb_release`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="c0975-280">예를 들어 다음 스크립트는 hello hello OS 버전에 따라 tooreference 특정 tar 파일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

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

## <span data-ttu-id="c0975-281"><a name="deployScript"></a>스크립트 작업 배포를 위한 검사 목록</span><span class="sxs-lookup"><span data-stu-id="c0975-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="c0975-282">이러한 스크립트 toodeploy를 준비할 때 했습니다 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="c0975-283">Hello 배포 하는 동안 hello 클러스터 노드에서 액세스할 수 있는 위치에서 사용자 지정 스크립트를 포함 하는 hello 파일을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="c0975-284">예를 들어 hello hello 클러스터에 대 한 기본 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="c0975-285">공개적으로 읽을 수 있는 호스팅 서비스에 파일을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="c0975-286">Hello 스크립트 강력한 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="c0975-287">이 통해 hello 스크립트 toobe 여러 번 실행 hello에 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="c0975-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="c0975-288">임시 파일 디렉터리 /tmp tookeep hello 사용 하 여 hello 스크립트에 의해 사용 되는 파일을 다운로드 하 여 다음 스크립트를 실행 한 후를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="c0975-289">운영 체제 수준을 설정 또는 Hadoop 서비스 구성 파일 변경 되 면 toorestart HDInsight 서비스 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="c0975-290"><a name="runScriptAction"></a>어떻게 toorun 스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="c0975-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="c0975-291">메서드를 다음 hello를 사용 하 여 스크립트 작업 toocustomize HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="c0975-292">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c0975-292">Azure portal</span></span>
* <span data-ttu-id="c0975-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0975-293">Azure PowerShell</span></span>
* <span data-ttu-id="c0975-294">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="c0975-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="c0975-295">hello HDInsight.NET SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="c0975-296">각 메서드를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [toouse 작업을 스크립팅 하는 방법을](hdinsight-hadoop-customize-cluster-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="c0975-297"><a name="sampleScripts"></a>사용자 지정 스크립트 샘플</span><span class="sxs-lookup"><span data-stu-id="c0975-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="c0975-298">Microsoft은 HDInsight 클러스터에서 예제 스크립트 tooinstall 구성 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="c0975-299">자세한 예제 스크립트 동작에 대 한 링크를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c0975-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="c0975-300">HDInsight에서 Hue 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="c0975-301">HDInsight 클러스터에 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="c0975-302">HDInsight 클러스터에 Giraph 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="c0975-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="c0975-303">HDInsight 클러스터에 Mono 설치 또는 업그레이드</span><span class="sxs-lookup"><span data-stu-id="c0975-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="c0975-304">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c0975-304">Troubleshooting</span></span>

<span data-ttu-id="c0975-305">hello 다음은 오류가 개발한 스크립트를 사용 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="c0975-306">**오류**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="c0975-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="c0975-307">때로는 `syntax error: unexpected end of file`이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="c0975-308">*원인*: 스크립트에서 줄 hello CRLF 끝나야 하는 경우이 오류는 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="c0975-309">Unix 시스템 hello 줄 끝 LF만 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="c0975-310">이 문제가 가장 자주 발생 hello 스크립트는 Windows 환경에 대해 작성 되어 CRLF은 Windows에서 많은 텍스트 편집기를 종료 하는 일반적인 선으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="c0975-311">*해결 방법*: 텍스트 편집기에서 옵션이 면 hello 줄 끝에 대 한 Unix 형식 또는 LF 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="c0975-312">Hello 나오는 Unix 시스템 toochange hello CRLF tooan LF에 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="c0975-313">hello 다음 명령은 동일 대략 hello CRLF 줄 끝 tooLF를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="c0975-314">시스템에서 사용할 수 있는 hello 유틸리티에 따라 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="c0975-315">명령</span><span class="sxs-lookup"><span data-stu-id="c0975-315">Command</span></span> | <span data-ttu-id="c0975-316">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c0975-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="c0975-317">원본 파일 hello와 함께 백업 됩니다는 합니다. BAK 확장</span><span class="sxs-lookup"><span data-stu-id="c0975-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="c0975-318">OUTFILE은 끝이 LF인 버전만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="c0975-319">Hello 파일을 직접 수정</span><span class="sxs-lookup"><span data-stu-id="c0975-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="c0975-320">OUTFILE은 끝이 LF인 버전만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="c0975-321">**오류**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="c0975-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="c0975-322">*원인*: 경우이 오류가 발생 hello 스크립트는 바이트 순서 표시가 (BOM) u t F-8로 저장 되었다는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="c0975-323">*해결 방법*: hello 파일 ASCII로 또는 BOM 없이 u t F-8로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="c0975-324">Hello hello BOM 없이 파일은 Linux 또는 Unix 시스템 toocreate에서 다음 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="c0975-325">대체 `INFILE` hello 파일에 BOM hello 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="c0975-326">`OUTFILE`hello BOM 없이 hello 스크립트가 들어 있는 새 파일 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="c0975-327"><a name="seeAlso"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0975-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="c0975-328">너무 방법에 대해 알아봅니다[HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="c0975-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="c0975-329">사용 하 여 hello [HDInsight.NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx) toolearn HDInsight를 관리 하는.NET 응용 프로그램을 만드는 방법에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="c0975-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="c0975-330">사용 하 여 hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn toouse REST tooperform 관리 작업에서 HDInsight 클러스터 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c0975-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
