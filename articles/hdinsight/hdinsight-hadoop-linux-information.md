---
title: "Linux 기반 HDInsight에서 Hadoop 사용 팁 - Azure | Microsoft Docs"
description: "Azure 클라우드에서 실행되는 친숙한 Linux 환경에서 Linux 기반 HDInsight(Hadoop) 클러스터를 사용하기 위한 구현 팁을 제공합니다."
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
ms.openlocfilehash: 8c6ff4a6b8617cda9b12be060c7c7bed62cb3f44
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a><span data-ttu-id="de574-103">Linux에서 HDInsight 사용에 관한 정보</span><span class="sxs-lookup"><span data-stu-id="de574-103">Information about using HDInsight on Linux</span></span>

<span data-ttu-id="de574-104">Azure HDInsight 클러스터는 Azure 클라우드에서 실행되는 친숙한 Linux 환경에서 Hadoop을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-104">Azure HDInsight clusters provide Hadoop on a familiar Linux environment, running in the Azure cloud.</span></span> <span data-ttu-id="de574-105">대부분의 작업에 대해 Linux 설치에서 모든 다른 Hadoop으로 정확하게 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-105">For most things, it should work exactly as any other Hadoop-on-Linux installation.</span></span> <span data-ttu-id="de574-106">이 문서를 알고 있어야 하는 특정 차이점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-106">This document calls out specific differences that you should be aware of.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de574-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="de574-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de574-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="de574-109">Prerequisites</span></span>

<span data-ttu-id="de574-110">이 문서의 단계 대부분은 많은 시스템에 설치해야 할 수 있는 다음과 같은 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-110">Many of the steps in this document use the following utilities, which may need to be installed on your system.</span></span>

* <span data-ttu-id="de574-111">[cURL](https://curl.haxx.se/) - 웹 기반 서비스와 통신하는 데 사용됩니다</span><span class="sxs-lookup"><span data-stu-id="de574-111">[cURL](https://curl.haxx.se/) - used to communicate with web-based services</span></span>
* <span data-ttu-id="de574-112">[jq](https://stedolan.github.io/jq/) -JSON 문서를 구문 분석하는 데 사용됩니다</span><span class="sxs-lookup"><span data-stu-id="de574-112">[jq](https://stedolan.github.io/jq/) - used to parse JSON documents</span></span>
* <span data-ttu-id="de574-113">[Azure CLI 2.0(미리 보기)](https://docs.microsoft.com/cli/azure/install-az-cli2) - Azure 서비스를 원격으로 관리 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-113">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (preview) - used to remotely manage Azure services</span></span>

## <a name="users"></a><span data-ttu-id="de574-114">사용자</span><span class="sxs-lookup"><span data-stu-id="de574-114">Users</span></span>

<span data-ttu-id="de574-115">[도메인에 가입](hdinsight-domain-joined-introduction.md)되어 있지 않으면 HDInsight를 **단일 사용자** 시스템으로 간주하기 때문에</span><span class="sxs-lookup"><span data-stu-id="de574-115">Unless [domain-joined](hdinsight-domain-joined-introduction.md), HDInsight should be considered a **single-user** system.</span></span> <span data-ttu-id="de574-116">관리자 수준 권한으로 하나의 SSH 사용자 계정이 클러스터와 함께 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="de574-116">A single SSH user account is created with the cluster, with administrator level permissions.</span></span> <span data-ttu-id="de574-117">추가 SSH 계정을 만들 수는 있지만 클러스터에 대한 관리자 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-117">Additional SSH accounts can be created, but they also have administrator access to the cluster.</span></span>

<span data-ttu-id="de574-118">도메인 가입 HDInsight에서는 여러 사용자와 세분화된 권한 및 역할 설정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-118">Domain-joined HDInsight supports multiple users and more granular permission and role settings.</span></span> <span data-ttu-id="de574-119">자세한 내용은 [도메인 가입 HDInsight 클러스터 구성](hdinsight-domain-joined-manage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-119">For more information, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="domain-names"></a><span data-ttu-id="de574-120">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="de574-120">Domain names</span></span>

<span data-ttu-id="de574-121">인터넷에서 클러스터에 연결할 때 사용할 FQDN(정규화된 도메인 이름)은 **&lt;clustername>.azurehdinsight.net** 또는 **&lt;clustername-ssh>.azurehdinsight.net**(SSH인 경우만)입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-121">The fully qualified domain name (FQDN) to use when connecting to the cluster from the internet is **&lt;clustername>.azurehdinsight.net** or (for SSH only) **&lt;clustername-ssh>.azurehdinsight.net**.</span></span>

<span data-ttu-id="de574-122">내부적으로 클러스터의 각 노드 이름은 클러스터 구성 중에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-122">Internally, each node in the cluster has a name that is assigned during cluster configuration.</span></span> <span data-ttu-id="de574-123">클러스터 이름을 찾으려면 Ambari 웹 UI의 **호스트** 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-123">To find the cluster names, see the **Hosts** page on the Ambari Web UI.</span></span> <span data-ttu-id="de574-124">다음을 사용하여 Ambari REST API에서 호스트 목록을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-124">You can also use the following to return a list of hosts from the Ambari REST API:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

<span data-ttu-id="de574-125">**PASSWORD**는 관리 계정의 암호로 바꾸고 **CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de574-125">Replace **PASSWORD** with the password of the admin account, and **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="de574-126">이 명령은 클러스터의 호스트 목록을 포함하는 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-126">This command returns a JSON document that contains a list of the hosts in the cluster.</span></span> <span data-ttu-id="de574-127">Jq는 각 호스트에 대한 `host_name` 요소 값을 추출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-127">Jq is used to extract the `host_name` element value for each host.</span></span>

<span data-ttu-id="de574-128">특정 서비스에 대한 노드의 이름을 찾으려면 해당 구성 요소에 대해 Ambari를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-128">If you need to find the name of the node for a specific service, you can query Ambari for that component.</span></span> <span data-ttu-id="de574-129">예를 들어 HDFS 이름 노드에 대한 호스트를 찾으려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-129">For example, to find the hosts for the HDFS name node, use the following command:</span></span>

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

<span data-ttu-id="de574-130">이 명령은 서비스를 설명하는 JSON 문서를 반환한 다음 jq에서 호스트에 대한 `host_name` 값만 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-130">This command returns a JSON document describing the service, and then jq pulls out only the `host_name` value for the hosts.</span></span>

## <a name="remote-access-to-services"></a><span data-ttu-id="de574-131">서비스에 대한 원격 액세스</span><span class="sxs-lookup"><span data-stu-id="de574-131">Remote access to services</span></span>

* <span data-ttu-id="de574-132">**Ambari(웹)** - https://&lt;clustername>.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="de574-132">**Ambari (web)** - https://&lt;clustername>.azurehdinsight.net</span></span>

    <span data-ttu-id="de574-133">클러스터 관리자 계정 및 암호를 사용하여 인증하고 Ambari에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-133">Authenticate by using the cluster administrator user and password, and then log in to Ambari.</span></span>

    <span data-ttu-id="de574-134">인증은 일반 텍스트입니다. 항상 HTTPS를 사용하여 연결의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-134">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="de574-135">일부 웹 UI는 내부 도메인 이름을 사용하여 Ambari 액세스 일부를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-135">Some of the web UIs available through Ambari access nodes using an internal domain name.</span></span> <span data-ttu-id="de574-136">내부 도메인 이름은 인터넷을 통해 공개적으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-136">Internal domain names are not publicly accessible over the internet.</span></span> <span data-ttu-id="de574-137">인터넷을 통해 일부 기능에 액세스하려고 하면 "서버를 찾을 수 없음" 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-137">You may receive "server not found" errors when trying to access some features over the Internet.</span></span>
    >
    > <span data-ttu-id="de574-138">Ambari 웹 UI의 모든 기능을 사용하려면 프록시 웹 트래픽에 대한 SSH 터널을 클러스터 헤드 노드에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-138">To use the full functionality of the Ambari web UI, use an SSH tunnel to proxy web traffic to the cluster head node.</span></span> <span data-ttu-id="de574-139">[SSH 터널링을 사용하여 Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie 및 기타 웹 UI에 액세스](hdinsight-linux-ambari-ssh-tunnel.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-139">See [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

* <span data-ttu-id="de574-140">**Ambari(REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span><span class="sxs-lookup"><span data-stu-id="de574-140">**Ambari (REST)** - https://&lt;clustername>.azurehdinsight.net/ambari</span></span>

    > [!NOTE]
    > <span data-ttu-id="de574-141">클러스터 관리자 계정 및 암호를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-141">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="de574-142">인증은 일반 텍스트입니다. 항상 HTTPS를 사용하여 연결의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-142">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="de574-143">**WebHCat(Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span><span class="sxs-lookup"><span data-stu-id="de574-143">**WebHCat (Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton</span></span>

    > [!NOTE]
    > <span data-ttu-id="de574-144">클러스터 관리자 계정 및 암호를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-144">Authenticate by using the cluster administrator user and password.</span></span>
    >
    > <span data-ttu-id="de574-145">인증은 일반 텍스트입니다. 항상 HTTPS를 사용하여 연결의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-145">Authentication is plaintext - always use HTTPS to help ensure that the connection is secure.</span></span>

* <span data-ttu-id="de574-146">**SSH** - &lt;clustername >-ssh.azurehdinsight.net(포트 22 또는 23).</span><span class="sxs-lookup"><span data-stu-id="de574-146">**SSH** - &lt;clustername>-ssh.azurehdinsight.net on port 22 or 23.</span></span> <span data-ttu-id="de574-147">포트 22는 기본 헤드 노드에 연결하는 데 사용되는 반면 포트 23은 보조 헤드 노드에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-147">Port 22 is used to connect to the primary headnode, while 23 is used to connect to the secondary.</span></span> <span data-ttu-id="de574-148">헤드 노드에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터의 가용성 및 안정성](hdinsight-high-availability-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-148">For more information on the head nodes, see [Availability and reliability of Hadoop clusters in HDInsight](hdinsight-high-availability-linux.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="de574-149">클라이언트 컴퓨터에서 SSH를 통해 클러스터 헤드 노드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-149">You can only access the cluster head nodes through SSH from a client machine.</span></span> <span data-ttu-id="de574-150">연결한 후 헤드 노드에서 SSH를 사용하여 작업자 노드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-150">Once connected, you can then access the worker nodes by using SSH from a headnode.</span></span>

## <a name="file-locations"></a><span data-ttu-id="de574-151">파일 위치</span><span class="sxs-lookup"><span data-stu-id="de574-151">File locations</span></span>

<span data-ttu-id="de574-152">Hadoop 관련 파일은 `/usr/hdp`의 클러스터 노드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-152">Hadoop-related files can be found on the cluster nodes at `/usr/hdp`.</span></span> <span data-ttu-id="de574-153">이 디렉터리에는 다음과 같은 하위 디렉터리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-153">This directory contains the following subdirectories:</span></span>

* <span data-ttu-id="de574-154">**2.2.4.9-1**: 디렉터리 이름은 HDInsight에서 사용되는 Hortonworks Data Platform의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-154">**2.2.4.9-1**: The directory name is the version of the Hortonworks Data Platform used by HDInsight.</span></span> <span data-ttu-id="de574-155">클러스터에 있는 숫자는 여기에 나열된 것과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-155">The number on your cluster may be different than the one listed here.</span></span>
* <span data-ttu-id="de574-156">**current**: **2.2.4.9-1** 디렉터리 아래의 하위 디렉터리에 대한 링크를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-156">**current**: This directory contains links to subdirectories under the **2.2.4.9-1** directory.</span></span> <span data-ttu-id="de574-157">이 디렉터리가 있으므로 버전 번호를 기억할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-157">This directory exists so that you don't have to remember the version number.</span></span>

<span data-ttu-id="de574-158">예제 데이터 및 JAR 파일은 `/example` 및 `/HdiSamples`의 HDFS(Hadoop 분산 파일 시스템)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-158">Example data and JAR files can be found on Hadoop Distributed File System at `/example` and `/HdiSamples`</span></span>

## <a name="hdfs-azure-storage-and-data-lake-store"></a><span data-ttu-id="de574-159">HDFS, Azure Storage 및 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="de574-159">HDFS, Azure Storage, and Data Lake Store</span></span>

<span data-ttu-id="de574-160">대부분의 Hadoop 배포판에서 HDFS는 클러스터의 컴퓨터에서 로컬 저장소에 의해 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="de574-160">In most Hadoop distributions, HDFS is backed by local storage on the machines in the cluster.</span></span> <span data-ttu-id="de574-161">계산 리소스에 대해 시간당 또는 분당 비용이 부과되는 클라우드 기반 솔루션의 경우 로컬 저장소를 사용하면 비용이 많이 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-161">Using local storage can be costly for a cloud-based solution where you are charged hourly or by minute for compute resources.</span></span>

<span data-ttu-id="de574-162">HDInsight는 Azure Storage 또는 Azure Data Lake Store의 Blob을 기본 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-162">HDInsight uses either blobs in Azure Storage or Azure Data Lake Store as the default store.</span></span> <span data-ttu-id="de574-163">이러한 서비스는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-163">These services provide the following benefits:</span></span>

* <span data-ttu-id="de574-164">저렴한 장기 저장소</span><span class="sxs-lookup"><span data-stu-id="de574-164">Cheap long-term storage</span></span>
* <span data-ttu-id="de574-165">웹 사이트, 파일 업로드/다운로드 유틸리티, 다양한 언어 SDK 및 웹 브라우저와 같은 외부 서비스에 액세스할 수 있음</span><span class="sxs-lookup"><span data-stu-id="de574-165">Accessibility from external services such as websites, file upload/download utilities, various language SDKs, and web browsers</span></span>

> [!WARNING]
> <span data-ttu-id="de574-166">HDInsight는 __범용__ Azure Storage 계정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-166">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="de574-167">현재 __Blob 저장소__ 계정 유형은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-167">It does not currently support the __Blob storage__ account type.</span></span>

<span data-ttu-id="de574-168">Azure Storage 계정은 최대 4.75TB까지 저장할 수 있지만 개별 Blob(또는 HDInsight 관점 기준 파일)은 최대 195GB까지만 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-168">An Azure Storage account can hold up to 4.75 TB, though individual blobs (or files from an HDInsight perspective) can only go up to 195 GB.</span></span> <span data-ttu-id="de574-169">Azure Data Lake Store는 페타바이트 이상의 개별 파일을 수조 개 포함하도록 동적으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-169">Azure Data Lake Store can grow dynamically to hold trillions of files, with individual files greater than a petabyte.</span></span> <span data-ttu-id="de574-170">자세한 내용은 [Blob 이해](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 및 [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-170">For more information, see [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) and [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span>

<span data-ttu-id="de574-171">Azure Storage 또는 Data Lake Store를 사용하는 경우 HDInsight에서 데이터에 액세스하기 위해 특별한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-171">When using either Azure Storage or Data Lake Store, you don't have to do anything special from HDInsight to access the data.</span></span> <span data-ttu-id="de574-172">예를 들어 Azure Storage 또는 Data Lake Store 중 어느 것에 저장되어 있든지 다음 명령은 `/example/data` 폴더에 있는 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-172">For example, the following command lists files in the `/example/data` folder regardless of whether it is stored on Azure Storage or Data Lake Store:</span></span>

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a><span data-ttu-id="de574-173">URI 및 구성표</span><span class="sxs-lookup"><span data-stu-id="de574-173">URI and scheme</span></span>

<span data-ttu-id="de574-174">일부 명령에서는 파일에 액세스할 때 URI의 일부로 구성표를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-174">Some commands may require you to specify the scheme as part of the URI when accessing a file.</span></span> <span data-ttu-id="de574-175">예를 들어 Storm-HDFS 구성 요소를 사용하려면 구성표를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-175">For example, the Storm-HDFS component requires you to specify the scheme.</span></span> <span data-ttu-id="de574-176">기본값이 아닌 저장소(클러스터에 "추가" 저장소로 추가된 저장소)를 사용할 때는 항상 URI의 일부로 구성표를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-176">When using non-default storage (storage added as "additional" storage to the cluster), you must always use the scheme as part of the URI.</span></span>

<span data-ttu-id="de574-177">__Azure Storage__를 사용하는 경우 다음 URI 체계 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-177">When using __Azure Storage__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="de574-178">`wasb:///`: 암호화되지 않은 통신을 사용하여 기본 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-178">`wasb:///`: Access default storage using unencrypted communication.</span></span>

* <span data-ttu-id="de574-179">`wasbs:///`: 암호화된 통신을 사용하여 기본 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-179">`wasbs:///`: Access default storage using encrypted communication.</span></span>  <span data-ttu-id="de574-180">wasbs 구성표는 HDInsight 버전 3.6 이상에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-180">The wasbs scheme is supported only from HDInsight version 3.6 onwards.</span></span>

* <span data-ttu-id="de574-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: 기본이 아닌 저장소 계정과 통신할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-181">`wasb://<container-name>@<account-name>.blob.core.windows.net/`: Used when communicating with a non-default storage account.</span></span> <span data-ttu-id="de574-182">예를 들어 추가 저장소 계정이 있거나 공개적으로 액세스할 수 있는 저장소 계정에 저장된 데이터에 액세스하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-182">For example, when you have an additional storage account or when accessing data stored in a publicly accessible storage account.</span></span>

<span data-ttu-id="de574-183">__Data Lake Store__를 사용하는 경우 다음 URI 체계 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-183">When using __Data Lake Store__, use one of the following URI schemes:</span></span>

* <span data-ttu-id="de574-184">`adl:///`: 클러스터의 기본 Data Lake Store에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-184">`adl:///`: Access the default Data Lake Store for the cluster.</span></span>

* <span data-ttu-id="de574-185">`adl://<storage-name>.azuredatalakestore.net/`: 기본이 아닌 Data Lake Store와 통신할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-185">`adl://<storage-name>.azuredatalakestore.net/`: Used when communicating with a non-default Data Lake Store.</span></span> <span data-ttu-id="de574-186">HDInsight 클러스터의 루트 디렉터리 외부 데이터에 액세스하는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-186">Also used to access data outside the root directory of your HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de574-187">HDInsight의 기본 저장소로 Data Lake Store를 사용하는 경우 HDInsight 저장소의 루트로 사용할 저장소 내의 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-187">When using Data Lake Store as the default store for HDInsight, you must specify a path within the store to use as the root of HDInsight storage.</span></span> <span data-ttu-id="de574-188">기본 경로는 `/clusters/<cluster-name>/`입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-188">The default path is `/clusters/<cluster-name>/`.</span></span>
>
> <span data-ttu-id="de574-189">`/` 또는 `adl:///`을 사용하여 데이터에 액세스하는 경우 클러스터의 루트(예: `/clusters/<cluster-name>/`)에 저장된 데이터에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-189">When using `/` or `adl:///` to access data, you can only access data stored in the root (for example, `/clusters/<cluster-name>/`) of the cluster.</span></span> <span data-ttu-id="de574-190">저장소의 모든 위치에 있는 데이터에 액세스하려면 `adl://<storage-name>.azuredatalakestore.net/` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-190">To access data anywhere in the store, use the `adl://<storage-name>.azuredatalakestore.net/` format.</span></span>

### <a name="what-storage-is-the-cluster-using"></a><span data-ttu-id="de574-191">클러스터에서 사용하는 저장소</span><span class="sxs-lookup"><span data-stu-id="de574-191">What storage is the cluster using</span></span>

<span data-ttu-id="de574-192">Ambari를 사용하면 클러스터에 대한 기본 저장소 구성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-192">You can use Ambari to retrieve the default storage configuration for the cluster.</span></span> <span data-ttu-id="de574-193">curl을 사용하여 HDFS 구성 정보를 검색하도록 다음 명령을 사용하고 [jq](https://stedolan.github.io/jq/)를 사용하여 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-193">Use the following command to retrieve HDFS configuration information using curl, and filter it using [jq](https://stedolan.github.io/jq/):</span></span>

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> <span data-ttu-id="de574-194">이렇게 하면 해당 정보가 있는 서버(`service_config_version=1`)에 적용된 첫 번째 구성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-194">This returns the first configuration applied to the server (`service_config_version=1`), which contains this information.</span></span> <span data-ttu-id="de574-195">최신 버전을 찾기 위해 모든 구성 버전을 나열해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-195">You may need to list all configuration versions to find the latest one.</span></span>

<span data-ttu-id="de574-196">이 명령은 다음 URI와 유사한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-196">This command returns a value similar to the following URIs:</span></span>

* <span data-ttu-id="de574-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` - Azure Storage 계정을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="de574-197">`wasb://<container-name>@<account-name>.blob.core.windows.net` if using an Azure Storage account.</span></span>

    <span data-ttu-id="de574-198">계정 이름은 Azure Storage 계정의 이름이고, 컨테이너 이름은 클러스터 저장소의 루트인 Blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-198">The account name is the name of the Azure Storage account, while the container name is the blob container that is the root of the cluster storage.</span></span>

* <span data-ttu-id="de574-199">`adl://home` - Azure Data Lake Store를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="de574-199">`adl://home` if using Azure Data Lake Store.</span></span> <span data-ttu-id="de574-200">Data Lake Store 이름을 가져오려면 다음 REST 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-200">To get the Data Lake Store name, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    <span data-ttu-id="de574-201">이 명령은 `<data-lake-store-account-name>.azuredatalakestore.net` 호스트 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-201">This command returns the following host name: `<data-lake-store-account-name>.azuredatalakestore.net`.</span></span>

    <span data-ttu-id="de574-202">저장소 내에서 HDInsight의 루트 디렉터리를 가져오려면 다음 REST 호출을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-202">To get the directory within the store that is the root for HDInsight, use the following REST call:</span></span>

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    <span data-ttu-id="de574-203">이 명령은 `/clusters/<hdinsight-cluster-name>/`과 비슷한 경로를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-203">This command returns a path similar to the following path: `/clusters/<hdinsight-cluster-name>/`.</span></span>

<span data-ttu-id="de574-204">또한 다음 단계를 사용하여 Azure Portal에서 저장소 정보를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-204">You can also find the storage information using the Azure portal by using the following steps:</span></span>

1. <span data-ttu-id="de574-205">[Azure Portal](https://portal.azure.com/)에서 HDInsight 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-205">In the [Azure portal](https://portal.azure.com/), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="de574-206">**속성** 섹션에서 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-206">From the **Properties** section, select **Storage Accounts**.</span></span> <span data-ttu-id="de574-207">클러스터에 대한 저장소 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-207">The storage information for the cluster is displayed.</span></span>

### <a name="how-do-i-access-files-from-outside-hdinsight"></a><span data-ttu-id="de574-208">HDInsight 외부에서 파일에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="de574-208">How do I access files from outside HDInsight</span></span>

<span data-ttu-id="de574-209">HDInsight 클러스터 외부에서 데이터에 액세스하는 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-209">There are a various ways to access data from outside the HDInsight cluster.</span></span> <span data-ttu-id="de574-210">다음은 데이터 작업에 사용할 수 있는 유틸리티 및 SDK에 대한 몇 가지 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-210">The following are a few links to utilities and SDKs that can be used to work with your data:</span></span>

<span data-ttu-id="de574-211">__Azure Storage__를 사용하는 경우 다음 링크를 참조하여 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-211">If using __Azure Storage__, see the following links for ways that you can access your data:</span></span>

* <span data-ttu-id="de574-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Azure로 작업하기 위한 명령줄 인터페이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-212">[Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Command-Line interface commands for working with Azure.</span></span> <span data-ttu-id="de574-213">설치 후 저장소 사용에 대한 도움말은 `az storage`를 참조하고 Blob 관련 명령에 대한 도움말은 `az storage blob`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-213">After installing, use the `az storage` command for help on using storage, or `az storage blob` for blob-specific commands.</span></span>
* <span data-ttu-id="de574-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): Azure 저장소의 Blob 작업을 위한 python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-214">[blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): A python script for working with blobs in Azure Storage.</span></span>
* <span data-ttu-id="de574-215">다양한 SDK:</span><span class="sxs-lookup"><span data-stu-id="de574-215">Various SDKs:</span></span>

    * [<span data-ttu-id="de574-216">Java</span><span class="sxs-lookup"><span data-stu-id="de574-216">Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
    * [<span data-ttu-id="de574-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="de574-217">Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
    * [<span data-ttu-id="de574-218">PHP</span><span class="sxs-lookup"><span data-stu-id="de574-218">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
    * [<span data-ttu-id="de574-219">Python</span><span class="sxs-lookup"><span data-stu-id="de574-219">Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
    * [<span data-ttu-id="de574-220">Ruby</span><span class="sxs-lookup"><span data-stu-id="de574-220">Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)
    * [<span data-ttu-id="de574-221">.NET</span><span class="sxs-lookup"><span data-stu-id="de574-221">.NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
    * [<span data-ttu-id="de574-222">저장소 REST API</span><span class="sxs-lookup"><span data-stu-id="de574-222">Storage REST API</span></span>](https://msdn.microsoft.com/library/azure/dd135733.aspx)

<span data-ttu-id="de574-223">__Azure Data Lake Store__를 사용하는 경우 다음 링크를 참조하여 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-223">If using __Azure Data Lake Store__, see the following links for ways that you can access your data:</span></span>

* [<span data-ttu-id="de574-224">웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="de574-224">Web browser</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* [<span data-ttu-id="de574-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de574-225">PowerShell</span></span>](../data-lake-store/data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="de574-226">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de574-226">Azure CLI 2.0</span></span>](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [<span data-ttu-id="de574-227">WebHDFS REST API</span><span class="sxs-lookup"><span data-stu-id="de574-227">WebHDFS REST API</span></span>](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [<span data-ttu-id="de574-228">Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de574-228">Data Lake Tools for Visual Studio</span></span>](https://www.microsoft.com/download/details.aspx?id=49504)
* [<span data-ttu-id="de574-229">.NET</span><span class="sxs-lookup"><span data-stu-id="de574-229">.NET</span></span>](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="de574-230">Java</span><span class="sxs-lookup"><span data-stu-id="de574-230">Java</span></span>](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="de574-231">Python</span><span class="sxs-lookup"><span data-stu-id="de574-231">Python</span></span>](../data-lake-store/data-lake-store-get-started-python.md)

## <span data-ttu-id="de574-232"><a name="scaling"></a>클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="de574-232"><a name="scaling"></a>Scaling your cluster</span></span>

<span data-ttu-id="de574-233">클러스터 크기 조정 기능을 사용하면 클러스터에서 사용하는 데이터 노드 수를 동적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-233">The cluster scaling feature allows you to dynamically change the number of data nodes used by a cluster.</span></span> <span data-ttu-id="de574-234">클러스터에서 다른 작업 또는 프로세스가 실행되는 동안 크기 조정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-234">You can perform scaling operations while other jobs or processes are running on a cluster.</span></span>

<span data-ttu-id="de574-235">다른 클러스터 종류는 다음과 같이 크기 조정에 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-235">The different cluster types are affected by scaling as follows:</span></span>

* <span data-ttu-id="de574-236">**Hadoop**: 클러스터의 노드 수를 줄이면 클러스터 서비스 중 일부가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-236">**Hadoop**: When scaling down the number of nodes in a cluster, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="de574-237">크기 조정 작업을 수행하면 작업이 실행 중이거나 보류 중 상태가 되므로 크기 조정 작업이 완료되지 못하고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-237">Scaling operations can cause jobs running or pending to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="de574-238">작업이 완료되면 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-238">You can resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="de574-239">**HBase**: 지역 서버는 크기 조정 작업을 완료한 후 몇 분 안에 자동으로 균형을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="de574-239">**HBase**: Regional servers are automatically balanced within a few minutes after completion of the scaling operation.</span></span> <span data-ttu-id="de574-240">지역 서버를 수동으로 조정하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-240">To manually balance regional servers, use the following steps:</span></span>

    1. <span data-ttu-id="de574-241">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-241">Connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="de574-242">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-242">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    2. <span data-ttu-id="de574-243">다음을 사용하여 HBase 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-243">Use the following to start the HBase shell:</span></span>

            hbase shell

    3. <span data-ttu-id="de574-244">HBase 셸이 로드되면 다음을 사용하여 지역 서버를 수동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-244">Once the HBase shell has loaded, use the following to manually balance the regional servers:</span></span>

            balancer

* <span data-ttu-id="de574-245">**Storm**: 크기 조정 작업을 수행한 후 실행 중인 모든 Storm 토폴로지 균형을 다시 맞추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-245">**Storm**: You should rebalance any running Storm topologies after a scaling operation has been performed.</span></span> <span data-ttu-id="de574-246">균형을 다시 조정하면 토폴로지를 새 클러스터의 노드 수에 따라 병렬 처리 설정을 다시 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-246">Rebalancing allows the topology to readjust parallelism settings based on the new number of nodes in the cluster.</span></span> <span data-ttu-id="de574-247">실행 중인 토폴로지의 균형을 다시 조정하려면 다음 옵션 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-247">To rebalance running topologies, use one of the following options:</span></span>

    * <span data-ttu-id="de574-248">**SSH**: 서버에 연결하고 다음 명령을 사용하여 토폴로지 균형을 다시 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="de574-248">**SSH**: Connect to the server and use the following command to rebalance a topology:</span></span>

            storm rebalance TOPOLOGYNAME

        <span data-ttu-id="de574-249">매개 변수를 지정하여 원래 토폴로지로 제공된 병렬 처리 힌트를 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-249">You can also specify parameters to override the parallelism hints originally provided by the topology.</span></span> <span data-ttu-id="de574-250">예를 들어 `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10`은 토폴로지를 5개 작업자 프로세스, 파란색 spout 구성 요소를 3개 실행자 및 노란색 bolt 구성 요소를 10개 실행자로 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-250">For example, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigures the topology to 5 worker processes, 3 executors for the blue-spout component, and 10 executors for the yellow-bolt component.</span></span>

    * <span data-ttu-id="de574-251">**Storm UI**: Storm UI를 사용하여 토폴로지 균형을 다시 맞추려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-251">**Storm UI**: Use the following steps to rebalance a topology using the Storm UI.</span></span>

        1. <span data-ttu-id="de574-252">웹 브라우저에서 **https://CLUSTERNAME.azurehdinsight.net/stormui**를 엽니다. 여기서 CLUSTERNAME은 Storm 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-252">Open **https://CLUSTERNAME.azurehdinsight.net/stormui** in your web browser, where CLUSTERNAME is the name of your Storm cluster.</span></span> <span data-ttu-id="de574-253">메시지가 표시되면 클러스터를 만들 때 지정한 HDInsight 클러스터 관리자(관리자) 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-253">If prompted, enter the HDInsight cluster administrator (admin) name and password you specified when creating the cluster.</span></span>
        2. <span data-ttu-id="de574-254">균형을 다시 맞추려는 토폴로지를 선택한 다음 **균형 다시 맞추기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-254">Select the topology you wish to rebalance, then select the **Rebalance** button.</span></span> <span data-ttu-id="de574-255">균형 재조정 작업이 수행되기 전에 지연 시간을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-255">Enter the delay before the rebalance operation is performed.</span></span>

<span data-ttu-id="de574-256">HDInsight 클러스터 크기 조정에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-256">For specific information on scaling your HDInsight cluster, see:</span></span>

* [<span data-ttu-id="de574-257">Azure Portal을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="de574-257">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="de574-258">Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="de574-258">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a><span data-ttu-id="de574-259">Hue(또는 다른 Hadoop 구성 요소)를 어떻게 설치합니까?</span><span class="sxs-lookup"><span data-stu-id="de574-259">How do I install Hue (or other Hadoop component)?</span></span>

<span data-ttu-id="de574-260">HDInsight는 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-260">HDInsight is a managed service.</span></span> <span data-ttu-id="de574-261">Azure에서 클러스터와 관련된 문제를 발견하면 실패한 노드를 삭제하고 이 노드를 대체할 노드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-261">If Azure detects a problem with the cluster, it may delete the failing node and create a node to replace it.</span></span> <span data-ttu-id="de574-262">클러스터에 Hue(또는 다른 Hadoop 구성 요소)를 수동으로 설치하는 경우 이 작업이 수행될 때 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-262">If you manually install things on the cluster, they are not persisted when this operation occurs.</span></span> <span data-ttu-id="de574-263">대신 [HDInsight 스크립트 동작](hdinsight-hadoop-customize-cluster.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-263">Instead, use [HDInsight Script Actions](hdinsight-hadoop-customize-cluster.md).</span></span> <span data-ttu-id="de574-264">스크립트 동작을 사용하여 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-264">A script action can be used to make the following changes:</span></span>

* <span data-ttu-id="de574-265">Spark 또는 Hue와 같은 서비스 또는 웹 사이트를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-265">Install and configure a service or web site such as Spark or Hue.</span></span>
* <span data-ttu-id="de574-266">클러스터의 여러 노드에 대한 구성을 변경할 필요가 있는 구성 요소를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-266">Install and configure a component that requires configuration changes on multiple nodes in the cluster.</span></span> <span data-ttu-id="de574-267">예를 들어 필수 환경 변수, 로깅 디렉터리 만들기 또는 구성 파일 만들기입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-267">For example, a required environment variable, creating of a logging directory, or creation of a configuration file.</span></span>

<span data-ttu-id="de574-268">스크립트 동작은 Bash 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="de574-268">Script Actions are Bash scripts.</span></span> <span data-ttu-id="de574-269">스크립트는 클러스터를 프로비전하는 동안 실행되며, 클러스터에 추가 구성 요소를 설치 및 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-269">The scripts run during cluster provisioning, and can be used to install and configure additional components on the cluster.</span></span> <span data-ttu-id="de574-270">다음 구성 요소를 설치하기 위한 예제 스크립트가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-270">Example scripts are provided for installing the following components:</span></span>

* [<span data-ttu-id="de574-271">Hue</span><span class="sxs-lookup"><span data-stu-id="de574-271">Hue</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="de574-272">Giraph</span><span class="sxs-lookup"><span data-stu-id="de574-272">Giraph</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="de574-273">Solr</span><span class="sxs-lookup"><span data-stu-id="de574-273">Solr</span></span>](hdinsight-hadoop-solr-install-linux.md)

<span data-ttu-id="de574-274">사용자 고유의 스크립트 작업 개발에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de574-274">For information on developing your own Script Actions, see [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

### <a name="jar-files"></a><span data-ttu-id="de574-275">Jar 파일</span><span class="sxs-lookup"><span data-stu-id="de574-275">Jar files</span></span>

<span data-ttu-id="de574-276">일부 Hadoop 기술은 MapReduce 작업의 일부로 사용되거나 Pig 또는 Hive 내부에서 사용되는 함수를 포함하는 자체 포함된 jar 파일에 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-276">Some Hadoop technologies are provided in self-contained jar files that contain functions used as part of a MapReduce job, or from inside Pig or Hive.</span></span> <span data-ttu-id="de574-277">[스크립트 동작]을 사용하여 설치할 수도 있지만 종종 설치할 필요 없이 프로비전한 후에 클러스터에 업로드하여 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-277">While these can be installed using Script Actions, they often don't require any setup and can be uploaded to the cluster after provisioning and used directly.</span></span> <span data-ttu-id="de574-278">구성 요소에서 클러스터를 다시 이미징하여 유지할 수 있도록 하려면 클러스터의 기본 저장소(WASB 또는 ADL)에 jar 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-278">If you want to make sure the component survives reimaging of the cluster, you can store the jar file in the default storage for your cluster (WASB or ADL).</span></span>

<span data-ttu-id="de574-279">예를 들어 [DataFu](http://datafu.incubator.apache.org/)의 최신 버전을 사용하려는 경우 프로젝트가 포함된 jar을 다운로드하고 HDInsight 클러스터에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-279">For example, if you want to use the latest version of [DataFu](http://datafu.incubator.apache.org/), you can download a jar containing the project and upload it to the HDInsight cluster.</span></span> <span data-ttu-id="de574-280">그런 다음 Pig 또는 Hive를 사용하는 방법에 대한 DataFu 설명서를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-280">Then follow the DataFu documentation on how to use it from Pig or Hive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de574-281">독립 실행형 jar 파일인 구성 요소 일부는 HDInsight와 함께 제공되지만 경로에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-281">Some components that are standalone jar files are provided with HDInsight, but are not in the path.</span></span> <span data-ttu-id="de574-282">특정 구성 요소를 찾으려면 다음을 사용하여 클러스터에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-282">If you are looking for a specific component, you can use the follow to search for it on your cluster:</span></span>
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> <span data-ttu-id="de574-283">이 명령은 일치하는 jar 파일의 경로를 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-283">This command returns the path of any matching jar files.</span></span>

<span data-ttu-id="de574-284">다른 버전의 구성 요소를 사용하려면 필요한 버전을 업로드한 후 작업에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de574-284">To use a different version of a component, upload the version you need and use it in your jobs.</span></span>

> [!WARNING]
> <span data-ttu-id="de574-285">HDInsight 클러스터와 함께 제공되는 구성 요소는 완벽하게 지원되며 Microsoft 지원은 이러한 구성 요소와 관련된 문제를 격리하고 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de574-285">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="de574-286">사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-286">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="de574-287">지원을 통해 문제를 해결하거나 해당 기술에 대한 전문 지식이 있는, 오픈 소스 기술에 대해 사용 가능한 채널에 참여하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-287">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="de574-288">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de574-288">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="de574-289">또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="de574-289">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de574-290">다음 단계</span><span class="sxs-lookup"><span data-stu-id="de574-290">Next steps</span></span>

* [<span data-ttu-id="de574-291">Windows 기반 HDInsight에서 Linux 기반 HDInsight로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="de574-291">Migrate from Windows-based HDInsight to Linux-based</span></span>](hdinsight-migrate-from-windows-to-linux.md)
* [<span data-ttu-id="de574-292">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="de574-292">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="de574-293">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="de574-293">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="de574-294">HDInsight에서 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="de574-294">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
