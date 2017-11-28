---
title: "Linux 기반 HDInsight-Azure의 Hadoop을 사용 하기 위한 aaaTips | Microsoft Docs"
description: "Linux 기반 HDInsight (Hadoop) 클러스터에서 Azure 클라우드 hello 실행 중인 Linux 친숙 한 환경에서 사용 하기 위한 구현 팁을 가져옵니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a><span data-ttu-id="47d58-103">Linux에서 HDInsight 사용에 관한 정보</span><span class="sxs-lookup"><span data-stu-id="47d58-103">Information about using HDInsight on Linux</span></span>

<span data-ttu-id="47d58-104">Azure HDInsight 클러스터 hello Azure 클라우드에에서 실행 되는 친숙 한 Linux 환경에서 Hadoop을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in hello Azure cloud.</span></span> <span data-ttu-id="47d58-105">대부분의 작업에 대해 Linux 설치에서 모든 다른 Hadoop으로 정확하게 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span></span> <span data-ttu-id="47d58-106">이 문서를 알고 있어야 하는 특정 차이점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-106">This document calls out specific differences that you should be aware of.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47d58-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47d58-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47d58-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="47d58-109">Prerequisites</span></span>

<span data-ttu-id="47d58-110">대부분이 문서의 단계 hello hello 다음 toobe 시스템에 설치 해야 할 수 있는 유틸리티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-110">Many of hello steps in this document use hello following utilities, which may need toobe installed on your system.</span></span>

* <span data-ttu-id="47d58-111">[cURL](https://curl.haxx.se/) -웹 기반 서비스와 toocommunicate 사용</span><span class="sxs-lookup"><span data-stu-id="47d58-111">[cURL](https://curl.haxx.se/) - used toocommunicate with web-based services</span></span>
* <span data-ttu-id="47d58-112">[jq](https://stedolan.github.io/jq/) -tooparse JSON 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-112">[jq](https://stedolan.github.io/jq/) - used tooparse JSON documents</span></span>
* <span data-ttu-id="47d58-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (미리 보기)-tooremotely 사용 되는 Azure 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="47d58-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used tooremotely manage Azure services</span></span>

## <a name="users"></a><span data-ttu-id="47d58-114">사용자</span><span class="sxs-lookup"><span data-stu-id="47d58-114">Users</span></span>

<span data-ttu-id="47d58-115">[도메인에 가입](hdinsight-domain-joined-introduction.md)되어 있지 않으면 HDInsight를 **단일 사용자** 시스템으로 간주하기 때문에</span><span class="sxs-lookup"><span data-stu-id="47d58-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span></span> <span data-ttu-id="47d58-116">Hello 클러스터 관리자의 권한 가진 단일 SSH 사용자 계정을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-116">A single SSH user account is created with hello cluster, with administrator level permissions.</span></span> <span data-ttu-id="47d58-117">추가 SSH 계정을 만들 수 있지만 관리자 액세스 toohello 클러스터도 가집니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-117">Additional SSH accounts can be created, but they also have administrator access toohello cluster.</span></span>

<span data-ttu-id="47d58-118">도메인 가입 HDInsight에서는 여러 사용자와 세분화된 권한 및 역할 설정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span></span> <span data-ttu-id="47d58-119">자세한 내용은 [도메인 가입 HDInsight 클러스터 구성](hdinsight-domain-joined-manage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="domain-names"></a><span data-ttu-id="47d58-120">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="47d58-120">Domain names</span></span>

<span data-ttu-id="47d58-121">hello 정규화 된 도메인 이름 (FQDN) toouse toohello 클러스터 hello은 인터넷에서 연결할 때  **&lt;clustername >. azurehdinsight.net** 또는 SSH에만 해당) (용  **&lt;clustername-ssh >. azurehdinsight.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-121">hello fully qualified domain name (FQDN) toouse when connecting toohello cluster from hello internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span></span>

<span data-ttu-id="47d58-122">내부적으로 hello 클러스터의 각 노드 이름이 지정 된 클러스터 구성 중에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-122">Internally, each node in hello cluster has a name that is assigned during cluster configuration.</span></span> <span data-ttu-id="47d58-123">toofind hello 클러스터 이름 참조 hello **호스트** hello Ambari 웹 UI에는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-123">toofind hello cluster names, see hello **Hosts** page on hello Ambari Web UI.</span></span> <span data-ttu-id="47d58-124">또한 hello tooreturn hello Ambari REST API에서에서 호스트를 목록은 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-124">You can also use hello following tooreturn a list of hosts from hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

<span data-ttu-id="47d58-125">대체 **암호** hello 관리자 계정의 hello 암호로 및 **CLUSTERNAME** 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-125">Replace **PASSWORD** with hello password of hello admin account, and **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="47d58-126">이 명령은 hello 클러스터에서 hello 호스트의 목록을 포함 하는 JSON 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-126">This command returns a JSON document that contains a list of hello hosts in hello cluster.</span></span> <span data-ttu-id="47d58-127">사용 되는 tooextract hello Jq `host_name` 각 호스트에 대 한 요소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-127">Jq is used tooextract hello `host_name` element value for each host.</span></span>

<span data-ttu-id="47d58-128">특정 서비스에 대 한 hello 노드의 toofind hello 이름을 해야 할 경우에 해당 구성 요소에 대 한 Ambari를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-128">If you need toofind hello name of hello node for a specific service, you can query Ambari for that component.</span></span> <span data-ttu-id="47d58-129">예를 들어 hello HDFS 이름 노드에 대 한 toofind hello 호스트 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-129">For example, toofind hello hosts for hello HDFS name node, use hello following command:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

<span data-ttu-id="47d58-130">이 명령은 hello 서비스를 설명 하는 JSON 문서를 반환 하 고 다음 jq 추출만 hello `host_name` hello 호스트에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-130">This command returns a JSON document describing hello service, and then jq pulls out only hello `host_name` value for hello hosts.</span></span>

## <a name="remote-access-tooservices"></a><span data-ttu-id="47d58-131">원격 액세스 tooservices</span><span class="sxs-lookup"><span data-stu-id="47d58-131">Remote access tooservices</span></span>

* <span data-ttu-id="47d58-132">**Ambari(웹)** - https://&lt;clustername>.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="47d58-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span></span>

    <span data-ttu-id="47d58-133">Hello 클러스터 관리자 사용자와 암호를 사용 하 여 인증 하 고 tooAmbari 로그인.</span><span class="sxs-lookup"><span data-stu-id="47d58-133">Authenticate by using hello cluster administrator user and password, and then log in tooAmbari.</span></span>

    <span data-ttu-id="47d58-134">인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-134">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="47d58-135">일부의 hello 웹 Ui 내부 도메인 이름을 사용 하 여 Ambari 액세스 노드를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-135">Some of hello web UIs available through Ambari access nodes using an internal domain name.</span></span> <span data-ttu-id="47d58-136">내부 도메인 이름을 통해 공개적으로 액세스할 수 없는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-136">Internal domain names are not publicly accessible over hello internet.</span></span> <span data-ttu-id="47d58-137">Hello 인터넷을 통해 tooaccess 일부 기능을 시도할 때 "서버를 찾을 수 없습니다." 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-137">You may receive "server not found" errors when trying tooaccess some features over hello Internet.</span></span>
    >
    > <span data-ttu-id="47d58-138">toouse hello hello Ambari web UI의 전체 기능 SSH 터널 tooproxy 웹 트래픽 toohello 클러스터 헤드 노드 사용.</span><span class="sxs-lookup"><span data-stu-id="47d58-138">toouse hello full functionality of hello Ambari web UI, use an SSH tunnel tooproxy web traffic toohello cluster head node.</span></span> <span data-ttu-id="47d58-139">참조 [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 Ui](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="47d58-139">See [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

* <span data-ttu-id="47d58-140">**Ambari(REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span><span class="sxs-lookup"><span data-stu-id="47d58-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d58-141">Hello 클러스터 관리자가 사용자 및 암호를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-141">Authenticate by using hello cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="47d58-142">인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-142">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

* <span data-ttu-id="47d58-143">**WebHCat(Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span><span class="sxs-lookup"><span data-stu-id="47d58-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d58-144">Hello 클러스터 관리자가 사용자 및 암호를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-144">Authenticate by using hello cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="47d58-145">인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-145">Authentication is plaintext - always use HTTPS toohelp ensure that hello connection is secure.</span></span>

* <span data-ttu-id="47d58-146">**SSH** - &lt;clustername >-ssh.azurehdinsight.net(포트 22 또는 23).</span><span class="sxs-lookup"><span data-stu-id="47d58-146">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span></span> <span data-ttu-id="47d58-147">22 포트가 사용 되는 tooconnect toohello 기본 헤드 노드에, 23는 보조 사용 되는 tooconnect toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-147">Port 22 is used tooconnect toohello primary headnode, while 23 is used tooconnect toohello secondary.</span></span> <span data-ttu-id="47d58-148">Hello 헤드 노드에 대 한 자세한 내용은 참조 하십시오. [HDInsight에서 Hadoop의 가용성 및 안정성 클러스터](hdinsight-high-availability-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-148">For more information on hello head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="47d58-149">클라이언트 컴퓨터에서 SSH를 통해 hello 클러스터 헤드 노드만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-149">You can only access hello cluster head nodes through SSH from a client machine.</span></span> <span data-ttu-id="47d58-150">연결 되 면 hello 작업자 노드는 헤드 노드에에서 SSH를 사용 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-150">Once connected, you can then access hello worker nodes by using SSH from a headnode.</span></span>

## <a name="file-locations"></a><span data-ttu-id="47d58-151">파일 위치</span><span class="sxs-lookup"><span data-stu-id="47d58-151">File locations</span></span>

<span data-ttu-id="47d58-152">Hadoop 관련 파일에 대 한 hello 클러스터 노드에서 있습니다 `/usr/hdp`합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-152">Hadoop-related files can be found on hello cluster nodes at `/usr/hdp`.</span></span> <span data-ttu-id="47d58-153">이 디렉터리에 하위 디렉터리를 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-153">This directory contains hello following subdirectories:</span></span>

* <span data-ttu-id="47d58-154">**2.2.4.9-1**: hello 디렉터리 이름이 hello 버전의 hello Hortonworks Data Platform HDInsight에서 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-154">**2.2.4.9-1**: hello directory name is hello version of hello Hortonworks Data Platform used by HDInsight.</span></span> <span data-ttu-id="47d58-155">클러스터에 hello 번호 hello 여기에 나열 된 하나 보다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-155">hello number on your cluster may be different than hello one listed here.</span></span>
* <span data-ttu-id="47d58-156">**현재**:이 디렉터리에 hello 아래 링크 toosubdirectories **2.2.4.9-1** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-156">**current**: This directory contains links toosubdirectories under hello **2.2.4.9-1** directory.</span></span> <span data-ttu-id="47d58-157">이 디렉터리가 tooremember hello 버전 번호가 없는 있도록 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-157">This directory exists so that you don't have tooremember hello version number.</span></span>

<span data-ttu-id="47d58-158">예제 데이터 및 JAR 파일은 `/example` 및 `/HdiSamples`의 HDFS(Hadoop 분산 파일 시스템)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-158">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span></span>

## <a name="hdfs-azure-storage-and-data-lake-store"></a><span data-ttu-id="47d58-159">HDFS, Azure Storage 및 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47d58-159">HDFS, Azure Storage, and Data Lake Store</span></span>

<span data-ttu-id="47d58-160">대부분의 Hadoop 배포에서 HDFS hello 클러스터의 hello 컴퓨터에서 로컬 저장소에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-160">In most Hadoop distributions, HDFS is backed by local storage on hello machines in hello cluster.</span></span> <span data-ttu-id="47d58-161">계산 리소스에 대해 시간당 또는 분당 비용이 부과되는 클라우드 기반 솔루션의 경우 로컬 저장소를 사용하면 비용이 많이 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-161">Using local storage can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span></span>

<span data-ttu-id="47d58-162">HDInsight은 hello 기본 저장소로 Azure 저장소에서 blob 또는 Azure 데이터 레이크 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-162">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as hello default store.</span></span> <span data-ttu-id="47d58-163">이러한 서비스 혜택을 따라 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-163">These services provide hello following benefits:</span></span>

* <span data-ttu-id="47d58-164">저렴한 장기 저장소</span><span class="sxs-lookup"><span data-stu-id="47d58-164">Cheap long-term storage</span></span>
* <span data-ttu-id="47d58-165">웹 사이트, 파일 업로드/다운로드 유틸리티, 다양한 언어 SDK 및 웹 브라우저와 같은 외부 서비스에 액세스할 수 있음</span><span class="sxs-lookup"><span data-stu-id="47d58-165">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span></span>

> [!WARNING]
> <span data-ttu-id="47d58-166">HDInsight는 __범용__ Azure Storage 계정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-166">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="47d58-167">Hello 현재 지원 하지 않는 __Blob 저장소__ 계정 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-167">It does not currently support hello __Blob storage__ account type.</span></span>

<span data-ttu-id="47d58-168">각 blob (또는 HDInsight 관점에서 파일) 으로만 too195 GB를 이동할 수 있지만 Azure 저장소 계정이 too4.75 TB 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-168">An Azure Storage account can hold up too4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up too195 GB.</span></span> <span data-ttu-id="47d58-169">Azure 데이터 레이크 저장소 동적으로 늘릴 수 toohold trillions의 파일을 개별 파일로 페타바이트 보다 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-169">Azure Data Lake Store can grow dynamically toohold trillions of files, with individual files greater than a petabyte.</span></span> <span data-ttu-id="47d58-170">자세한 내용은 [Blob 이해](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 및 [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-170">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span>

<span data-ttu-id="47d58-171">Azure 저장소 서비스 또는 데이터 레이크 저장소 중 하나를 사용할 때 않아도 toodo HDInsight tooaccess hello 데이터에서 특별 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-171">When using either Azure Storage or Data Lake Store, you don't have toodo anything special from HDInsight tooaccess hello data.</span></span> <span data-ttu-id="47d58-172">다음 명령을 hello hello에 파일을 나열 하는 예를 들어 `/example/data` 데이터 레이크 저장소 또는 Azure 저장소에 저장 되어 있는지 여부에 관계 없이 폴더:</span><span class="sxs-lookup"><span data-stu-id="47d58-172">For example, hello following command lists files in hello `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span></span>

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a><span data-ttu-id="47d58-173">URI 및 구성표</span><span class="sxs-lookup"><span data-stu-id="47d58-173">URI and scheme</span></span>

<span data-ttu-id="47d58-174">일부 명령은 해야 toospecify hello 구성표 hello URI의 일환으로 파일에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="47d58-174">Some commands may require you toospecify hello scheme as part of hello URI when accessing a file.</span></span> <span data-ttu-id="47d58-175">예를 들어 hello 스톰 HDFS 구성 하려면 toospecify hello 구성표 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-175">For example, hello Storm-HDFS component requires you toospecify hello scheme.</span></span> <span data-ttu-id="47d58-176">기본이 아닌 저장소 ("추가" 저장소 toohello 클러스터로 추가 된 저장소)를 사용 하는 경우에 hello URI의 일부로 항상 hello 체계를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-176">When using non-default storage (storage added as "additional" storage toohello cluster), you must always use hello scheme as part of hello URI.</span></span>

<span data-ttu-id="47d58-177">사용 하는 경우 __Azure 저장소__, hello URI 체계를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-177">When using __Azure Storage__, use one of hello following URI schemes:</span></span>

* <span data-ttu-id="47d58-178">`wasb:///`: 암호화되지 않은 통신을 사용하여 기본 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-178">`wasb:///`: Access default storage using unencrypted communication.</span></span>

* <span data-ttu-id="47d58-179">`wasbs:///`: 암호화된 통신을 사용하여 기본 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-179">`wasbs:///`: Access default storage using encrypted communication.</span></span>  <span data-ttu-id="47d58-180">hello wasbs 구성표는 HDInsight 버전 3.6부터 에서만에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-180">hello wasbs scheme is supported only from HDInsight version 3.6 onwards.</span></span>

* <span data-ttu-id="47d58-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: 기본이 아닌 저장소 계정과 통신할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span></span> <span data-ttu-id="47d58-182">예를 들어 추가 저장소 계정이 있거나 공개적으로 액세스할 수 있는 저장소 계정에 저장된 데이터에 액세스하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-182">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span></span>

<span data-ttu-id="47d58-183">사용 하는 경우 __데이터 레이크 저장소__, hello URI 체계를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-183">When using __Data Lake Store__, use one of hello following URI schemes:</span></span>

* <span data-ttu-id="47d58-184">`adl:///`: Hello 클러스터에 대 한 hello 기본 데이터 레이크 저장소에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-184">`adl:///`: Access hello default Data Lake Store for hello cluster.</span></span>

* <span data-ttu-id="47d58-185">`adl://<storage-name>.azuredatalakestore.net/`: 기본이 아닌 Data Lake Store와 통신할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-185">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store.</span></span> <span data-ttu-id="47d58-186">HDInsight 클러스터의 hello 루트 디렉터리 외부에 있는 tooaccess 데이터도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-186">Also used tooaccess data outside hello root directory of your HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47d58-187">HDInsight에 대 한 hello 기본 저장소로 데이터 레이크 저장소를 사용할 경우 HDInsight 저장소의 hello 루트로 hello 저장소 toouse 내의 경로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-187">When using Data Lake Store as hello default store for HDInsight, you must specify a path within hello store toouse as hello root of HDInsight storage.</span></span> <span data-ttu-id="47d58-188">hello 기본 경로 `/clusters/<cluster-name>/`합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-188">hello default path is `/clusters/<cluster-name>/`.</span></span>
>
> <span data-ttu-id="47d58-189">사용 하는 경우 `/` 또는 `adl:///` tooaccess 데이터만 액세스할 수 있습니다 hello 루트에 저장 된 데이터 (예를 들어 `/clusters/<cluster-name>/`) hello 클러스터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-189">When using `/` or `adl:///` tooaccess data, you can only access data stored in hello root (for example, `/clusters/<cluster-name>/`) of hello cluster.</span></span> <span data-ttu-id="47d58-190">hello를 사용 하 여 hello 저장소에서 아무 곳 이나 tooaccess 데이터 `adl://<storage-name>.azuredatalakestore.net/` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-190">tooaccess data anywhere in hello store, use hello `adl://<storage-name>.azuredatalakestore.net/` format.</span></span>

### <a name="what-storage-is-hello-cluster-using"></a><span data-ttu-id="47d58-191">저장소는 hello 사용 하 여 클러스터</span><span class="sxs-lookup"><span data-stu-id="47d58-191">What storage is hello cluster using</span></span>

<span data-ttu-id="47d58-192">Hello 클러스터에 대 한 Ambari tooretrieve hello 기본 저장소 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-192">You can use Ambari tooretrieve hello default storage configuration for hello cluster.</span></span> <span data-ttu-id="47d58-193">사용 하 여 hello 다음 tooretrieve HDFS 구성 정보 curl을 사용 하 여 명령을 사용 하 여 필터링 [jq](https://stedolan.github.io/jq/):</span><span class="sxs-lookup"><span data-stu-id="47d58-193">Use hello following command tooretrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span></span>

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> <span data-ttu-id="47d58-194">첫 번째 적용 된 구성을 toohello 서버 hello를 반환 합니다. (`service_config_version=1`),이 정보를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-194">This returns hello first configuration applied toohello server (`service_config_version=1`), which contains this information.</span></span> <span data-ttu-id="47d58-195">Toolist toofind hello 최신 구성 버전을 모두 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-195">You may need toolist all configuration versions toofind hello latest one.</span></span>

<span data-ttu-id="47d58-196">이 명령은 다음 Uri 값 비슷한 toohello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-196">This command returns a value similar toohello following URIs:</span></span>

* <span data-ttu-id="47d58-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` - Azure Storage 계정을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="47d58-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span></span>

    <span data-ttu-id="47d58-198">hello 계정 이름은 hello Azure 저장소 계정 이름을 hello를 hello 컨테이너 이름을 hello blob 컨테이너는 hello 클러스터 저장소의 hello 루트는 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-198">hello account name is hello name of hello Azure Storage account, while hello container name is hello blob container that is hello root of hello cluster storage.</span></span>

* <span data-ttu-id="47d58-199">`adl://home` - Azure Data Lake Store를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="47d58-199">`adl://home` if using Azure Data Lake Store.</span></span> <span data-ttu-id="47d58-200">tooget hello Data Lake 저장소 이름 REST 호출 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-200">tooget hello Data Lake Store name, use hello following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    <span data-ttu-id="47d58-201">이 명령은 호스트 이름 뒤에 나오는 hello 반환: `<data-lake-store-account-name>.azuredatalakestore.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-201">This command returns hello following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span></span>

    <span data-ttu-id="47d58-202">HDInsight 사용 하 여 hello REST 호출 다음에 대 한 hello 루트는 hello 저장소 내의 tooget hello 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="47d58-202">tooget hello directory within hello store that is hello root for HDInsight, use hello following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    <span data-ttu-id="47d58-203">이 명령은 경로 경로 비슷한 toohello 반환: `/clusters/<hdinsight-cluster-name>/`합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-203">This command returns a path similar toohello following path: `/clusters/<hdinsight-cluster-name>/`.</span></span>

<span data-ttu-id="47d58-204">Azure 포털 hello를 사용 하 여 단계를 수행 하는 hello를 사용 하 여 hello 저장소 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-204">You can also find hello storage information using hello Azure portal by using hello following steps:</span></span>

1. <span data-ttu-id="47d58-205">Hello에 [Azure 포털](https://portal.azure.com/)를 HDInsight 클러스터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-205">In hello [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="47d58-206">Hello에서 **속성** 섹션에서 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-206">From hello **Properties** section, select **Storage Accounts**.</span></span> <span data-ttu-id="47d58-207">hello 클러스터에 대 한 hello 저장소 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-207">hello storage information for hello cluster is displayed.</span></span>

### <a name="how-do-i-access-files-from-outside-hdinsight"></a><span data-ttu-id="47d58-208">HDInsight 외부에서 파일에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="47d58-208">How do I access files from outside HDInsight</span></span>

<span data-ttu-id="47d58-209">외부 hello HDInsight 클러스터에서 tooaccess 데이터는 다양 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-209">There are a various ways tooaccess data from outside hello HDInsight cluster.</span></span> <span data-ttu-id="47d58-210">hello 다음은 몇 가지 링크 tooutilities 및 데이터와 함께 사용 되는 toowork 일 수 있는 Sdk입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-210">hello following are a few links tooutilities and SDKs that can be used toowork with your data:</span></span>

<span data-ttu-id="47d58-211">사용 하는 경우 __Azure 저장소__, 데이터에 액세스할 수 있도록 하는 방법에 대 한 링크를 따라 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-211">If using __Azure Storage__, see hello following links for ways that you can access your data:</span></span>

* <span data-ttu-id="47d58-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Azure로 작업하기 위한 명령줄 인터페이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span></span> <span data-ttu-id="47d58-213">를 설치한 후 hello를 사용 하 여 `az storage` 저장소 사용에 대 한 도움말 명령을 또는 `az storage blob` blob 관련 명령에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-213">After installing, use hello `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span></span>
* <span data-ttu-id="47d58-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): Azure 저장소의 Blob 작업을 위한 python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span></span>
* <span data-ttu-id="47d58-215">다양한 SDK:</span><span class="sxs-lookup"><span data-stu-id="47d58-215">Various SDKs:</span></span>

    * [<span data-ttu-id="47d58-216">Java</span><span class="sxs-lookup"><span data-stu-id="47d58-216">Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
    * [<span data-ttu-id="47d58-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="47d58-217">Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
    * [<span data-ttu-id="47d58-218">PHP</span><span class="sxs-lookup"><span data-stu-id="47d58-218">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
    * [<span data-ttu-id="47d58-219">Python</span><span class="sxs-lookup"><span data-stu-id="47d58-219">Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
    * [<span data-ttu-id="47d58-220">Ruby</span><span class="sxs-lookup"><span data-stu-id="47d58-220">Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)
    * [<span data-ttu-id="47d58-221">.NET</span><span class="sxs-lookup"><span data-stu-id="47d58-221">.NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
    * [<span data-ttu-id="47d58-222">저장소 REST API</span><span class="sxs-lookup"><span data-stu-id="47d58-222">Storage REST API</span></span>](https://msdn.microsoft.com/library/azure/dd135733.aspx)

<span data-ttu-id="47d58-223">사용 하는 경우 __Azure 데이터 레이크 저장소__, 데이터에 액세스할 수 있도록 하는 방법에 대 한 링크를 따라 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-223">If using __Azure Data Lake Store__, see hello following links for ways that you can access your data:</span></span>

* [<span data-ttu-id="47d58-224">웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="47d58-224">Web browser</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* [<span data-ttu-id="47d58-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47d58-225">PowerShell</span></span>](../data-lake-store/data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="47d58-226">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47d58-226">Azure CLI 2.0</span></span>](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [<span data-ttu-id="47d58-227">WebHDFS REST API</span><span class="sxs-lookup"><span data-stu-id="47d58-227">WebHDFS REST API</span></span>](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="47d58-228">Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47d58-228">Data Lake Tools for Visual Studio</span></span>](https://www.microsoft.com/download/details.aspx?id=49504)
* [<span data-ttu-id="47d58-229">.NET</span><span class="sxs-lookup"><span data-stu-id="47d58-229">.NET</span></span>](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="47d58-230">Java</span><span class="sxs-lookup"><span data-stu-id="47d58-230">Java</span></span>](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="47d58-231">Python</span><span class="sxs-lookup"><span data-stu-id="47d58-231">Python</span></span>](../data-lake-store/data-lake-store-get-started-python.md)

## <span data-ttu-id="47d58-232"><a name="scaling"></a>클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="47d58-232"><a name="scaling"></a>Scaling your cluster</span></span>

<span data-ttu-id="47d58-233">기능을 확장 하는 hello 클러스터에서는 클러스터에 의해 사용 되는 데이터 노드 수가 변경 hello toodynamically 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-233">hello cluster scaling feature allows you toodynamically change hello number of data nodes used by a cluster.</span></span> <span data-ttu-id="47d58-234">클러스터에서 다른 작업 또는 프로세스가 실행되는 동안 크기 조정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-234">You can perform scaling operations while other jobs or processes are running on a cluster.</span></span>

<span data-ttu-id="47d58-235">hello 다른 클러스터 종류는 다음과 같이 확장 하 여 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-235">hello different cluster types are affected by scaling as follows:</span></span>

* <span data-ttu-id="47d58-236">**Hadoop**: hello 클러스터에서 hello 서비스의 일부 hello 클러스터의 노드 수를 줄일 때는 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-236">**Hadoop**: When scaling down hello number of nodes in a cluster, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="47d58-237">실행 중이거나 toofail hello hello 크기 조정 작업이 완료 될 때 보류 중인 작업을 크기 조정 작업이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-237">Scaling operations can cause jobs running or pending toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="47d58-238">Hello 작업이 완료 되 면 hello 작업을 다시 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-238">You can resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="47d58-239">**HBase**: 지역 서버 hello 크기 조정 작업이 완료 된 후 몇 분 안에 자동으로 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-239">**HBase**: Regional servers are automatically balanced within a few minutes after completion of hello scaling operation.</span></span> <span data-ttu-id="47d58-240">toomanually 균형 지역 서버 hello 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-240">toomanually balance regional servers, use hello following steps:</span></span>

    1. <span data-ttu-id="47d58-241">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-241">Connect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="47d58-242">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-242">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    2. <span data-ttu-id="47d58-243">Hello 다음 toostart hello HBase 셸을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-243">Use hello following toostart hello HBase shell:</span></span>

            hbase shell

    3. <span data-ttu-id="47d58-244">HBase 셸 hello 로드 되 면 다음 toomanually 균형 hello 지역 서버 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-244">Once hello HBase shell has loaded, use hello following toomanually balance hello regional servers:</span></span>

            balancer

* <span data-ttu-id="47d58-245">**Storm**: 크기 조정 작업을 수행한 후 실행 중인 모든 Storm 토폴로지 균형을 다시 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-245">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span></span> <span data-ttu-id="47d58-246">균형 조정 hello 새 hello 클러스터의 노드 수에 따라 hello 토폴로지 tooreadjust 병렬 처리 수준 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-246">Rebalancing allows hello topology tooreadjust parallelism settings based on hello new number of nodes in hello cluster.</span></span> <span data-ttu-id="47d58-247">toorebalance 토폴로지, 실행 hello 다음 옵션 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-247">toorebalance running topologies, use one of hello following options:</span></span>

    * <span data-ttu-id="47d58-248">**SSH**: toohello 서버 연결 및 사용 하 여 hello 다음 명령은 toorebalance 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="47d58-248">**SSH**: Connect toohello server and use hello following command toorebalance a topology:</span></span>

            storm rebalance TOPOLOGYNAME

        <span data-ttu-id="47d58-249">원래 hello 토폴로지에서 제공 하는 매개 변수 toooverride hello 병렬 처리 수준 힌트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-249">You can also specify parameters toooverride hello parallelism hints originally provided by hello topology.</span></span> <span data-ttu-id="47d58-250">예를 들어 `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` 다시 구성 합니다. hello 토폴로지 too5 작업자 프로세스, hello 배출구 파랑 구성 요소에 대 한 3 executor 및 hello 노란색 볼트 구성 요소에 대 한 단일 한 10 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-250">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures hello topology too5 worker processes, 3 executors for hello blue-spout component, and 10 executors for hello yellow-bolt component.</span></span>

    * <span data-ttu-id="47d58-251">**Storm UI**: 사용 하 여 hello 다음 단계 toorebalance hello 스톰 UI를 사용 하는 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-251">**Storm UI**: Use hello following steps toorebalance a topology using hello Storm UI.</span></span>

        1. <span data-ttu-id="47d58-252">열기 **https://CLUSTERNAME.azurehdinsight.net/stormui** 여기서 CLUSTERNAME은 hello 이름 Storm 클러스터의 웹 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-252">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is hello name of your Storm cluster.</span></span> <span data-ttu-id="47d58-253">메시지가 표시 되 면 hello HDInsight 클러스터 (관리) 관리자 이름과 hello 클러스터를 만들 때 지정한 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-253">If prompted, enter hello HDInsight cluster administrator (admin) name and password you specified when creating hello cluster.</span></span>
        2. <span data-ttu-id="47d58-254">Toorebalance, 원하는 선택한 다음 하면 hello hello 토폴로지를 선택 **균형을 다시 조정할** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-254">Select hello topology you wish toorebalance, then select hello **Rebalance** button.</span></span> <span data-ttu-id="47d58-255">Hello를 리 밸런스 작업이 수행 되기 전에 hello 지연 시간을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-255">Enter hello delay before hello rebalance operation is performed.</span></span>

<span data-ttu-id="47d58-256">HDInsight 클러스터 크기 조정에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-256">For specific information on scaling your HDInsight cluster, see:</span></span>

* [<span data-ttu-id="47d58-257">Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-257">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="47d58-258">Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="47d58-258">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a><span data-ttu-id="47d58-259">Hue(또는 다른 Hadoop 구성 요소)를 어떻게 설치합니까?</span><span class="sxs-lookup"><span data-stu-id="47d58-259">How do I install Hue (or other Hadoop component)?</span></span>

<span data-ttu-id="47d58-260">HDInsight는 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-260">HDInsight is a managed service.</span></span> <span data-ttu-id="47d58-261">Azure에서 hello 클러스터 문제를 발견 하면 hello 노드 실패를 삭제 하 고 노드 tooreplace를 만들 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-261">If Azure detects a problem with hello cluster, it may delete hello failing node and create a node tooreplace it.</span></span> <span data-ttu-id="47d58-262">Hello 클러스터에서 작업을 수동으로 설치 하면이 작업이 수행 될 때 보관 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-262">If you manually install things on hello cluster, they are not persisted when this operation occurs.</span></span> <span data-ttu-id="47d58-263">대신 [HDInsight 스크립트 동작](hdinsight-hadoop-customize-cluster.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-263">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="47d58-264">스크립트 동작 변경 내용에 따라 사용 되는 toomake hello 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-264">A script action can be used toomake hello following changes:</span></span>

* <span data-ttu-id="47d58-265">Spark 또는 Hue와 같은 서비스 또는 웹 사이트를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-265">Install and configure a service or web site such as Spark or Hue.</span></span>
* <span data-ttu-id="47d58-266">설치 및 구성 하려면 hello 클러스터의 여러 노드에 구성을 변경 해야 하는 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="47d58-266">Install and configure a component that requires configuration changes on multiple nodes in hello cluster.</span></span> <span data-ttu-id="47d58-267">예를 들어 필수 환경 변수, 로깅 디렉터리 만들기 또는 구성 파일 만들기입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-267">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span></span>

<span data-ttu-id="47d58-268">스크립트 동작은 Bash 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-268">Script Actions are Bash scripts.</span></span> <span data-ttu-id="47d58-269">hello 스크립트 클러스터 프로 비전 중에 실행 사용된 tooinstall과 가능 hello 클러스터에서 추가 구성 요소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-269">hello scripts run during cluster provisioning, and can be used tooinstall and configure additional components on hello cluster.</span></span> <span data-ttu-id="47d58-270">예제 스크립트는 다음과 같은 구성 요소가 hello를 설치 하기 위한 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-270">Example scripts are provided for installing hello following components:</span></span>

* [<span data-ttu-id="47d58-271">Hue</span><span class="sxs-lookup"><span data-stu-id="47d58-271">Hue</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="47d58-272">Giraph</span><span class="sxs-lookup"><span data-stu-id="47d58-272">Giraph</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="47d58-273">Solr</span><span class="sxs-lookup"><span data-stu-id="47d58-273">Solr</span></span>](hdinsight-hadoop-solr-install-linux.md)

<span data-ttu-id="47d58-274">사용자 고유의 스크립트 작업 개발에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47d58-274">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

### <a name="jar-files"></a><span data-ttu-id="47d58-275">Jar 파일</span><span class="sxs-lookup"><span data-stu-id="47d58-275">Jar files</span></span>

<span data-ttu-id="47d58-276">일부 Hadoop 기술은 MapReduce 작업의 일부로 사용되거나 Pig 또는 Hive 내부에서 사용되는 함수를 포함하는 자체 포함된 jar 파일에 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-276">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span></span> <span data-ttu-id="47d58-277">이러한 스크립트 동작을 사용 하 여 설치할 수 있습니다, 종종 모든 설치에 필요 하지 않습니다 및 수 업로드 된 toohello 클러스터 프로 비전 한 후 있으며 직접 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-277">While these can be installed using Script Actions, they often don't require any setup and can be uploaded toohello cluster after provisioning and used directly.</span></span> <span data-ttu-id="47d58-278">후에 유지 되는 toomake 있는지 hello 구성 요소에는 hello 클러스터의 이미지로 다시 설치 합니다 (WASB 또는 ADL) 클러스터에 대 한 hello jar 파일 hello 기본 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-278">If you want toomake sure hello component survives reimaging of hello cluster, you can store hello jar file in hello default storage for your cluster (WASB or ADL).</span></span>

<span data-ttu-id="47d58-279">예를 들어, toouse 최신 버전의 hello [DataFu](http://datafu.incubator.apache.org/), hello 프로젝트를 포함 하는 jar를 다운로드 하 고 toohello HDInsight 클러스터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-279">For example, if you want toouse hello latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing hello project and upload it toohello HDInsight cluster.</span></span> <span data-ttu-id="47d58-280">다음 방법에 hello DataFu 설명서에 따라 toouse에서 Pig 또는 Hive 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-280">Then follow hello DataFu documentation on how toouse it from Pig or Hive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47d58-281">일부 구성 요소를 독립 실행형 jar 파일 HDInsight에 함께 제공 되 있지만 hello 경로에 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-281">Some components that are standalone jar files are provided with HDInsight, but are not in hello path.</span></span> <span data-ttu-id="47d58-282">특정 구성 요소에 대 한 원하는 경우에 클러스터에에 대 한 hello 따라 toosearch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-282">If you are looking for a specific component, you can use hello follow toosearch for it on your cluster:</span></span>
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> <span data-ttu-id="47d58-283">이 명령은 모든 일치 하는 jar 파일의 hello 경로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-283">This command returns hello path of any matching jar files.</span></span>

<span data-ttu-id="47d58-284">toouse 다른 버전의 구성 요소를 업로드 hello 버전 및 작업에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-284">toouse a different version of a component, upload hello version you need and use it in your jobs.</span></span>

> [!WARNING]
> <span data-ttu-id="47d58-285">Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원 하 고 Microsoft 지원 tooisolate 도와 관련된 toothese 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-285">Components provided with hello HDInsight cluster are fully supported and Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="47d58-286">사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-286">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="47d58-287">이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47d58-287">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="47d58-288">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. 또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="47d58-288">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d58-289">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47d58-289">Next steps</span></span>

* [<span data-ttu-id="47d58-290">Windows 기반 HDInsight tooLinux 기반에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="47d58-290">Migrate from Windows-based HDInsight tooLinux-based</span></span>](hdinsight-migrate-from-windows-to-linux.md)
* [<span data-ttu-id="47d58-291">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="47d58-291">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="47d58-292">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="47d58-292">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="47d58-293">HDInsight에서 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="47d58-293">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
