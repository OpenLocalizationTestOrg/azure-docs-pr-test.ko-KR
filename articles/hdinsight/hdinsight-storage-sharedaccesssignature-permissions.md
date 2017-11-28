---
title: "공유 액세스 서명을 사용하여 액세스 제한 - Azure HDInsight | Microsoft Docs"
description: "공유 액세스 서명을 사용하여 Azure 저장소 Blob에 저장된 데이터에 대한 HDInsight 액세스를 제한하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 2e4b1a307fae06c0639d93b9804c6f0f703d5900
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-in-hdinsight"></a><span data-ttu-id="41f85-103">Azure Storage 공유 액세스 서명을 사용하여 HDInsight에서 데이터 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="41f85-103">Use Azure Storage Shared Access Signatures to restrict access to data in HDInsight</span></span>

<span data-ttu-id="41f85-104">HDInsight는 클러스터와 연결된 Azure Storage 계정의 데이터에 대해 모든 액세스 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-104">HDInsight has full access to data in the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="41f85-105">blob 컨테이너에서 공유 액세스 서명을 사용하여 데이터에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-105">You can use Shared Access Signatures on the blob container to restrict access to the data.</span></span> <span data-ttu-id="41f85-106">예를 들어 데이터에 대한 읽기 전용 액세스 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-106">For example, to provide read-only access to the data.</span></span> <span data-ttu-id="41f85-107">공유 액세스 서명(SAS)은 데이터에 대한 액세스를 제한할 수 있는 Azure 저장소 계정의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="41f85-108">예를 들어 데이터에 대한 읽기 전용 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-108">For example, providing read-only access to data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41f85-109">Apache Ranger를 사용하는 솔루션의 경우 도메인에 가입된 HDInsight를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="41f85-110">자세한 내용은 [도메인에 가입된 HDInsight 구성](hdinsight-domain-joined-configure.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-110">For more information, see the [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="41f85-111">HDInsight는 클러스터의 기본 저장소에 대해 모든 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-111">HDInsight must have full access to the default storage for the cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="41f85-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="41f85-112">Requirements</span></span>

* <span data-ttu-id="41f85-113">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="41f85-113">An Azure subscription</span></span>
* <span data-ttu-id="41f85-114">C# 또는 Python.</span><span class="sxs-lookup"><span data-stu-id="41f85-114">C# or Python.</span></span> <span data-ttu-id="41f85-115">C# 예제 코드가 Visual Studio 솔루션으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="41f85-116">Visual Studio는 버전 2013, 2015 또는 2017이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="41f85-117">Python은 버전 2.7 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="41f85-118">Linux 기반 HDInsight 클러스터 또는 [Azure PowerShell][powershell] - 기존 Linux 기반 클러스터가 있는 경우 Ambari를 사용하여 클러스터에 공유 액세스 서명을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="41f85-119">그렇지 않으면 Azure PowerShell을 사용하여 클러스터를 만들고 클러스터를 만들 때 공유 액세스 서명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-119">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="41f85-120">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41f85-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="41f85-122">[https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature)의 예제 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-122">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="41f85-123">이 리포지토리에는 다음 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-123">This repository contains the following items:</span></span>

  * <span data-ttu-id="41f85-124">HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="41f85-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="41f85-125">HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Python 스크립트</span><span class="sxs-lookup"><span data-stu-id="41f85-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="41f85-126">HDInsight 클러스터를 만들고 SAS를 사용하도록 구성할 수 있는 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="41f85-126">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="41f85-127">공유 액세스 서명</span><span class="sxs-lookup"><span data-stu-id="41f85-127">Shared Access Signatures</span></span>

<span data-ttu-id="41f85-128">두 가지 형태의 공유 액세스 서명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="41f85-129">Ad hoc: SAS에 대한 시작 시간, 만료 시간 및 사용 권한이 SAS URI에 모두 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-129">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span>

* <span data-ttu-id="41f85-130">저장된 액세스 정책: 저장된 액세스 정책은 Blob 컨테이너 같은 리소스 컨테이너에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="41f85-131">정책은 하나 이상의 공유 액세스 서명에 대한 제약 조건을 관리하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-131">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="41f85-132">SAS를 공유 액세스 정책과 연결할 경우 SAS는 저장된 액세스 정책에 대해 정의된 제약 조건(시작 시간, 만료 시간 및 사용 권한)을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-132">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="41f85-133">두 형식의 차이점은 주요 시나리오인 해지에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-133">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="41f85-134">SAS는 URL이므로 SAS를 시작하도록 요청한 사용자에 상관없이 SAS를 획득한 모든 사용자가 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-134">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="41f85-135">SAS가 공개적으로 게시된 경우 전 세계의 모든 사용자가 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-135">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="41f85-136">분산된 SAS는 다음 네 가지 중 하나에 해당할 때까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="41f85-137">SAS에 지정된 만료 시간에 도달한 경우</span><span class="sxs-lookup"><span data-stu-id="41f85-137">The expiry time specified on the SAS is reached.</span></span>

2. <span data-ttu-id="41f85-138">SAS에서 참조된 저장된 액세스 정책에 대해 지정된 만료 시간에 도달했습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-138">The expiry time specified on the stored access policy referenced by the SAS is reached.</span></span> <span data-ttu-id="41f85-139">다음과 같은 시나리오에서는 만료 시간에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-139">The following scenarios cause the expiry time to be reached:</span></span>

    * <span data-ttu-id="41f85-140">시간 간격이 경과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-140">The time interval has elapsed.</span></span>
    * <span data-ttu-id="41f85-141">저장된 액세스 정책이 과거 만료 시간을 갖도록 수정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-141">The stored access policy is modified to have an expiry time in the past.</span></span> <span data-ttu-id="41f85-142">SAS를 철회하는 한 가지 방법은 만료 시간을 변경하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-142">Changing the expiry time is one way to revoke the SAS.</span></span>

3. <span data-ttu-id="41f85-143">SAS에서 참조되는 저장된 액세스 정책을 삭제한 경우(SAS를 해지하는 다른 방법).</span><span class="sxs-lookup"><span data-stu-id="41f85-143">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="41f85-144">똑같은 이름을 사용하여 저장된 액세스 정책을 다시 만들면 이전 정책에 대한 모든 SAS 토큰이 다시 유효해집니다(SAS의 만료 시간이 경과하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="41f85-144">If you recreate the stored access policy with the same name, all  SAS tokens for the previous policy are valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="41f85-145">SAS를 해지하기 위해 만료 시간을 미래의 시간으로 지정하여 액세스 정책을 다시 만들 경우 다른 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-145">If you intend to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>

4. <span data-ttu-id="41f85-146">SAS를 만드는 데 사용된 계정 키를 다시 생성한 경우.</span><span class="sxs-lookup"><span data-stu-id="41f85-146">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="41f85-147">키를 다시 생성하면 이전 키를 사용하는 모든 응용 프로그램이 인증에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-147">Regenerating the key causes all applications that use the previous key to fail authentication.</span></span> <span data-ttu-id="41f85-148">모든 구성 요소를 새 키로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-148">Update all components to the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41f85-149">공유 액세스 서명 URI는 서명을 만드는 데 사용된 계정 키 및 저장된 관련 액세스 정책(있는 경우)에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-149">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="41f85-150">저장된 액세스 정책을 지정하지 않는 경우 공유 액세스 서명을 해지하는 방법은 계정 키를 변경하는 것뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-150">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

<span data-ttu-id="41f85-151">항상 저장된 액세스 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="41f85-152">저장된 정책을 사용하는 경우 필요에 따라 서명을 철회하거나 만료 날짜를 연장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-152">When using stored policies, you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="41f85-153">이 문서의 단계에서는 SAS를 생성하는 데 저장된 액세스 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-153">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="41f85-154">공유 액세스 서명에 대한 자세한 내용은 [SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-154">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="41f85-155">C\#을 사용하여 저장된 정책 및 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="41f85-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="41f85-156">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-156">Open the solution in Visual Studio.</span></span>

2. <span data-ttu-id="41f85-157">솔루션 탐색기에서 **SASToken** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-157">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="41f85-158">**설정** 을 선택하고 다음 항목에 대한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-158">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="41f85-159">StorageConnectionString: 저장된 정책 및 SAS를 만들 저장소 계정에 대한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-159">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="41f85-160">형식은 `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey`여야 하며 여기서 `myaccount`는 사용자의 저장소 계정 이름이고 `mykey`는 저장소 계정에 대한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-160">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>

   * <span data-ttu-id="41f85-161">ContainerName: 액세스를 제한할 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-161">ContainerName: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="41f85-162">SASPolicyName: 만들 저장된 정책에 대해 사용할 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-162">SASPolicyName: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="41f85-163">FileToUpload: 컨테이너에 업로드할 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-163">FileToUpload: The path to a file that is uploaded to the container.</span></span>

4. <span data-ttu-id="41f85-164">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-164">Run the project.</span></span> <span data-ttu-id="41f85-165">SAS가 생성되면 다음 텍스트와 유사한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-165">Information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="41f85-166">SAS 정책 토큰, 저장소 계정 이름 및 컨테이너 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-166">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="41f85-167">저장소 계정을 HDInsight 클러스터에 연결할 때 이러한 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-167">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="41f85-168">Python을 사용하여 저장된 정책 및 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="41f85-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="41f85-169">SASToken.py 파일을 열고 다음 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-169">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="41f85-170">policy\_name: 만들 저장된 정책에 대해 사용할 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-170">policy\_name: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="41f85-171">storage\_account\_name: 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-171">storage\_account\_name: The name of your storage account.</span></span>

   * <span data-ttu-id="41f85-172">storage\_account\_key: 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-172">storage\_account\_key: The key for the storage account.</span></span>

   * <span data-ttu-id="41f85-173">storage\_container\_name: 액세스를 제한할 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-173">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="41f85-174">example\_file\_path: 컨테이너에 업로드할 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-174">example\_file\_path: The path to a file that is uploaded to the container.</span></span>

2. <span data-ttu-id="41f85-175">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-175">Run the script.</span></span> <span data-ttu-id="41f85-176">스크립트가 완료되면 다음 텍스트와 유사한 SAS 토큰이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-176">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="41f85-177">SAS 정책 토큰, 저장소 계정 이름 및 컨테이너 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-177">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="41f85-178">저장소 계정을 HDInsight 클러스터에 연결할 때 이러한 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-178">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="41f85-179">HDInsight에 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="41f85-179">Use the SAS with HDInsight</span></span>

<span data-ttu-id="41f85-180">HDInsight 클러스터를 만들 때 기본 저장소 계정을 지정해야 하며 필요에 따라 추가 저장소 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="41f85-181">저장소를 추가하는 이 두 가지 방법 모두에 사용된 저장소 계정 및 컨테이너에 대한 모든 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-181">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="41f85-182">공유 액세스 서명을 사용하여 컨테이너에 대한 액세스를 제한하려면 클러스터에 대한 **core-site** 구성에 사용자 지정 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-182">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="41f85-183">**Windows 기반** 또는 **Linux 기반** HDInsight 클러스터의 경우 PowerShell을 사용하여 클러스터를 만드는 동안 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="41f85-184">**Linux 기반** HDInsight 클러스터의 경우 Ambari를 사용하여 클러스터를 만든 후 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-184">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="41f85-185">SAS를 사용하는 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="41f85-185">Create a cluster that uses the SAS</span></span>

<span data-ttu-id="41f85-186">SAS를 사용하는 HDInsight 클러스터를 만드는 예제는 리포지토리의 `CreateCluster` 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-186">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="41f85-187">이를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-187">To use it, use the following steps:</span></span>

1. <span data-ttu-id="41f85-188">텍스트 편집기에서 `CreateCluster\HDInsightSAS.ps1` 파일을 열고 문서 맨 앞에 있는 다음 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-188">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

    ```powershell
    # Replace 'mycluster' with the name of the cluster to be created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with the name of the group to be created
    $resourceGroupName = 'myresourcegroup'
    # Replace with the Azure data center you want to the cluster to live in
    $location = 'North Europe'
    # Replace with the name of the default storage account to be created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with the name of the SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with the name of the SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with the SAS token generated earlier
    $SASToken = 'sastoken'
    # Set the number of worker nodes in the cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="41f85-189">예를 들어 `'mycluster'` 를 만들려는 클러스터의 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-189">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="41f85-190">SAS 값은 저장소 계정 및 SAS 토큰을 만들 때 이전 단계에서 사용한 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-190">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="41f85-191">값을 변경한 후 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-191">Once you have changed the values, save the file.</span></span>

2. <span data-ttu-id="41f85-192">새 Azure PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="41f85-193">Azure PowerShell에 익숙하지 않거나 설치되지 않은 경우 [Azure PowerShell 설치 및 구성][powershell]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="41f85-194">프롬프트에서 다음 명령을 사용하여 Azure 구독에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-194">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="41f85-195">메시지가 표시되면 Azure 구독 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-195">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="41f85-196">계정이 여러 Azure 구독과 연결되는 경우 `Select-AzureRmSubscription` 을 사용하여 사용할 구독을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-196">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>

4. <span data-ttu-id="41f85-197">프롬프트에서 디렉터리를 HDInsightSAS.ps1 파일이 있는 `CreateCluster` 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-197">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="41f85-198">그런 후 다음 명령을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-198">Then use the following command to run the script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="41f85-199">스크립트를 실행하면 리소스 그룹 및 저장소 계정이 생성되면서 출력이 PowerShell 프롬프트에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-199">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="41f85-200">HDInsight 클러스터에 대한 HTTP 사용자를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-200">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="41f85-201">이 계정은 클러스터에 대한 보안 HTTP/s 액세스를 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-201">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="41f85-202">Linux 기반 클러스터를 만드는 경우 SSH 사용자 계정 이름 및 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="41f85-203">이 계정은 클러스터에 원격으로 로그인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-203">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="41f85-204">HTTP/s 또는 SSH 사용자 이름 및 암호를 묻는 메시지가 나타나면 다음 조건을 충족하는 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-204">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="41f85-205">길이가 10자 이상이어야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="41f85-206">숫자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="41f85-207">영숫자가 아닌 문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="41f85-208">대문자 또는 소문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="41f85-209">이 스크립트를 완료하는 데는 일반적으로 약 15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-209">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="41f85-210">스크립트가 오류 없이 완료되면 클러스터가 만들어진 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-210">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="41f85-211">기존 클러스터에서 SAS 사용</span><span class="sxs-lookup"><span data-stu-id="41f85-211">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="41f85-212">기존 Linux 기반 클러스터가 있는 경우 다음 단계에 따라 **core-site** 구성에 SAS를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-212">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="41f85-213">클러스터에 대한 Ambari 웹 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-213">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="41f85-214">이 페이지의 주소는 https://YOURCLUSTERNAME.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-214">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="41f85-215">메시지가 표시되면 클러스터를 만들 때 사용한 관리자 이름(admin)과 암호를 사용하여 클러스터를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-215">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>

2. <span data-ttu-id="41f85-216">Ambari 웹 UI의 왼쪽에서 **HDFS** 를 선택한 다음 페이지 중간에서 **Configs** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-216">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>

3. <span data-ttu-id="41f85-217">**Advanced** 탭을 선택한 다음 **Custom core-site** 섹션이 나올 때까지 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-217">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>

4. <span data-ttu-id="41f85-218">**Custom core-site** 섹션을 확장한 후 끝까지 스크롤하여 **Add property...** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-218">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="41f85-219">**Key** 및 **Value** 필드에 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-219">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="41f85-220">**키**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="41f85-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="41f85-221">**값**: 이전에 실행한 C# 또는 Python 응용 프로그램에서 반환된 SAS</span><span class="sxs-lookup"><span data-stu-id="41f85-221">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="41f85-222">**CONTAINERNAME** 을 C# 또는 SAS 응용 프로그램에서 사용한 컨테이너 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-222">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="41f85-223">**STORAGEACCOUNTNAME** 을 사용한 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-223">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>

5. <span data-ttu-id="41f85-224">**Add** 단추를 클릭하여 이 키 및 값을 저장한 후 **Save** 단추를 클릭하여 구성 변경을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-224">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="41f85-225">메시지가 나타나면 변경에 대한 설명(예: "SAS 저장소 액세스 추가")을 추가하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-225">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="41f85-226">변경이 완료되었으면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-226">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="41f85-227">변경 내용을 적용하기 전에 여러 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-227">You must restart several services before the change takes effect.</span></span>

6. <span data-ttu-id="41f85-228">Ambari 웹 UI의 왼쪽 목록에서 **HDFS**를 선택한 다음 오른쪽의 **Service Actions** 드롭다운 목록에서 **Restart All**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-228">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="41f85-229">메시지가 나타나면 **Turn on maintenance mode**을 선택한 다음 __Conform Restart All"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="41f85-230">MapReduce2 및 YARN에 대해 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="41f85-231">서비스가 다시 시작된 후 각 서비스를 선택하고 **서비스 작업** 드롭다운에서 유지 관리 모드를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-231">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="41f85-232">제한된 액세스 테스트</span><span class="sxs-lookup"><span data-stu-id="41f85-232">Test restricted access</span></span>

<span data-ttu-id="41f85-233">액세스를 제한을 확인하려면 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-233">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="41f85-234">**Windows 기반** HDInsight 클러스터의 경우 원격 데스크톱을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-234">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="41f85-235">자세한 내용은 [RDP를 사용하여 HDInsight에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-235">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="41f85-236">연결된 후에는 바탕 화면의 **Hadoop 명령줄** 아이콘을 사용하여 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-236">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>

* <span data-ttu-id="41f85-237">**Linux 기반** HDInsight 클러스터의 경우 SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-237">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="41f85-238">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41f85-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="41f85-239">클러스터에 연결되면 다음 단계에 따라 SAS 저장소 계정의 항목에 대한 읽기 및 목록 전용 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-239">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="41f85-240">컨테이너의 콘텐츠를 나열하려면 프롬프트에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-240">To list the contents of the container, use the following command from the prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="41f85-241">**SASCONTAINER** 를 SAS 저장소 계정에 대해 만든 컨테이너의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-241">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="41f85-242">**SASACCOUNTNAME**을 SAS에 사용된 저장소 계정의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-242">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS.</span></span>

    <span data-ttu-id="41f85-243">목록에는 컨테이너와 SAS를 만들 때 업로드된 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-243">The list includes the file uploaded when the container and SAS were created.</span></span>

2. <span data-ttu-id="41f85-244">다음 명령을 사용하여 파일의 내용을 읽을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-244">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="41f85-245">이전 단계처럼 **SASCONTAINER** 및 **SASACCOUNTNAME**을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-245">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="41f85-246">**FILENAME** 을 이전 명령에 표시된 파일 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-246">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="41f85-247">이 명령은 파일 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-247">This command lists the contents of the file.</span></span>

3. <span data-ttu-id="41f85-248">다음 명령을 사용하여 파일을 로컬 파일 시스템에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-248">Use the following command to download the file to the local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="41f85-249">이 명령은 파일을 **testfile.txt**라는 로컬 파일에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-249">This command downloads the file to a local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="41f85-250">다음 명령을 사용하여 로컬 파일을 SAS 저장소의 새 **testupload.txt** 파일에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-250">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="41f85-251">다음 텍스트와 유사한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-251">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="41f85-252">저장소 위치가 읽기 + 목록 전용이므로 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-252">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="41f85-253">다음 명령을 사용하여 쓰기 가능한 클러스터의 기본 저장소에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-253">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="41f85-254">이때 작업이 성공적으로 완료되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-254">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="41f85-255">문제 해결</span><span class="sxs-lookup"><span data-stu-id="41f85-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="41f85-256">작업이 취소됨</span><span class="sxs-lookup"><span data-stu-id="41f85-256">A task was canceled</span></span>

<span data-ttu-id="41f85-257">**증상**: PowerShell 스크립트를 사용하여 클러스터를 만들 때 다음과 같은 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-257">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="41f85-258">**원인**: 클러스터의 admin/HTTP 사용자 또는 Linux 기반 클러스터인 경우 SSH 사용자에 대해 암호를 사용하는 경우 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-258">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="41f85-259">**해결 방법**: 다음 조건을 충족하는 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-259">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="41f85-260">길이가 10자 이상이어야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="41f85-261">숫자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-261">Must contain at least one digit</span></span>
* <span data-ttu-id="41f85-262">영숫자가 아닌 문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="41f85-263">대문자 또는 소문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="41f85-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="41f85-264">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41f85-264">Next steps</span></span>

<span data-ttu-id="41f85-265">이제 HDInsight 클러스터에 액세스가 제한된 저장소를 추가하는 방법을 배웠으므로 클러스터에서 데이터에 대해 작업하는 다른 방법에 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="41f85-265">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="41f85-266">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="41f85-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="41f85-267">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="41f85-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="41f85-268">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="41f85-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
