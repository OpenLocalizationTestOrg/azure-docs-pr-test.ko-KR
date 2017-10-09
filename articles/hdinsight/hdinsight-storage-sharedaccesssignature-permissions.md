---
title: "공유 액세스 서명-Azure HDInsight를 사용 하 여 aaaRestrict 액세스 | Microsoft Docs"
description: "공유 액세스 서명 toorestrict toouse HDInsight toodata Azure 저장소 blob에 저장 된 액세스 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="e6a58-103">Azure 저장소 공유 액세스 서명 toorestrict 액세스 toodata를 사용 하 여 HDInsight의</span><span class="sxs-lookup"><span data-stu-id="e6a58-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="e6a58-104">HDInsight 대 한 모든 권한을 toodata hello 클러스터와 연결 된 hello Azure 저장소 계정에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="e6a58-105">공유 액세스 서명 hello blob 컨테이너 toorestrict 액세스 toohello 데이터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="e6a58-106">예를 들어 tooprovide 읽기 전용 액세스 toohello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="e6a58-107">공유 액세스 서명 (SAS)는 Azure 저장소 계정의 toolimit 액세스 toodata 수 있는 기능.</span><span class="sxs-lookup"><span data-stu-id="e6a58-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="e6a58-108">예를 들어 toodata 읽기 전용 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6a58-109">Apache Ranger를 사용하는 솔루션의 경우 도메인에 가입된 HDInsight를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="e6a58-110">자세한 내용은 참조 hello [도메인에 가입 된 HDInsight 구성](hdinsight-domain-joined-configure.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="e6a58-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="e6a58-111">HDInsight에 대 한 모든 권한을 toohello 기본 저장소 hello 클러스터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="e6a58-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e6a58-112">Requirements</span></span>

* <span data-ttu-id="e6a58-113">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="e6a58-113">An Azure subscription</span></span>
* <span data-ttu-id="e6a58-114">C# 또는 Python.</span><span class="sxs-lookup"><span data-stu-id="e6a58-114">C# or Python.</span></span> <span data-ttu-id="e6a58-115">C# 예제 코드가 Visual Studio 솔루션으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="e6a58-116">Visual Studio는 버전 2013, 2015 또는 2017이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="e6a58-117">Python은 버전 2.7 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="e6a58-118">Linux 기반 HDInsight 클러스터 또는 [Azure PowerShell] [ powershell] -Linux 기반 기존 클러스터를 설정한 경우 Ambari tooadd 공유 액세스 서명을 toohello 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="e6a58-119">그렇지 않은 경우 Azure PowerShell toocreate 클러스터를 사용 하 고 클러스터를 만드는 동안 공유 액세스 서명을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e6a58-120">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e6a58-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a58-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e6a58-122">예를 들어 파일에서 hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="e6a58-123">이 저장소는 다음 항목 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="e6a58-124">HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e6a58-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="e6a58-125">HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Python 스크립트</span><span class="sxs-lookup"><span data-stu-id="e6a58-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="e6a58-126">PowerShell 스크립트는 HDInsight를 만들 수 있는 클러스터 및 toouse hello SAS를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="e6a58-127">공유 액세스 서명</span><span class="sxs-lookup"><span data-stu-id="e6a58-127">Shared Access Signatures</span></span>

<span data-ttu-id="e6a58-128">두 가지 형태의 공유 액세스 서명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="e6a58-129">임시: hello 시작 시간, 만료 시간 및 SAS hello SAS URI에 지정 된 모든 hello에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="e6a58-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="e6a58-130">저장된 액세스 정책: 저장된 액세스 정책은 Blob 컨테이너 같은 리소스 컨테이너에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="e6a58-131">정책에는 하나 이상의 공유 액세스 서명에 대 한 제약 조건을 사용 하는 toomanage 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="e6a58-132">저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 제약 조건을 상속-hello 시작 시간, 만료 시간 및 사용 권한-hello 저장 된 액세스 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="e6a58-133">hello hello 두 형식의 차이 한 가지 주요 시나리오에 대 한 중요: 해지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="e6a58-134">SAS URL을 이므로 모든 사용자에 게 SAS hello 가져옵니다 צ ְ ײ, 요청한 사용자에 관계 없이 toobegin.</span><span class="sxs-lookup"><span data-stu-id="e6a58-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="e6a58-135">SAS를 공개적으로 게시 하는 경우에 hello world의 다른 사용자가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="e6a58-136">분산된 SAS는 다음 네 가지 중 하나에 해당할 때까지 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="e6a58-137">SAS에 도달 하는 hello에 지정 된 만료 시간을 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="e6a58-138">SAS에 도달 하는 hello에서 참조 하는 hello 저장 된 액세스 정책에 지정 된 만료 시간을 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="e6a58-139">hello 다음과 같은 시나리오를 사용 하면 hello 만료 시간에 도달 toobe:</span><span class="sxs-lookup"><span data-stu-id="e6a58-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="e6a58-140">hello 시간 간격이 경과 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="e6a58-141">hello 저장 된 액세스 정책은 수정 된 toohave hello 과거에 만료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="e6a58-142">한 가지 방법은 toorevoke hello SAS는 hello 만료 시간을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="e6a58-143">hello 저장 하는 또 다른 방법은 toorevoke hello SAS SAS 삭제 되 면 hello에서 참조 하는 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="e6a58-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="e6a58-144">동일한 이름, 모든 SAS 토큰에 대 한 hello로 hello 저장 된 액세스 정책을 다시 만드는 경우 hello 이전 정책은 유효 (hello에 hello 만료 시간 SAS을 지나치지 않은) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="e6a58-145">Toorevoke hello SAS를 가져오려는 경우 수 있는지 toouse 다른 이름을 hello 액세스 정책 만료 시간이 hello 나중에 다시 만드는 경우.</span><span class="sxs-lookup"><span data-stu-id="e6a58-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="e6a58-146">사용 하는 toocreate hello SAS hello 계정 키 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="e6a58-147">Hello 키 다시 생성 하면 이전 키 toofail 인증 hello를 사용 하는 모든 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="e6a58-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="e6a58-148">모든 구성 요소 toohello 새 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6a58-149">공유 액세스 서명 URI hello 계정 키 사용 되는 toocreate hello 서명과 사용 하 여 연결 되며 hello (있는 경우) 저장 된 액세스 정책에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="e6a58-150">저장 된 액세스 정책이 없는 지정, hello만 방법은 toorevoke 공유 액세스 서명을 toochange hello 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="e6a58-151">항상 저장된 액세스 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="e6a58-152">저장 된 정책을 사용 하는 경우 서명을 취소 하거나 필요에 따라 hello 만료 날짜를 연장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="e6a58-153">이 문서의 단계 hello 저장 된 액세스 정책을 toogenerate SAS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="e6a58-154">공유 액세스 서명에 대 한 자세한 내용은 참조 하십시오. [hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="e6a58-155">C\#을 사용하여 저장된 정책 및 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="e6a58-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="e6a58-156">Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="e6a58-157">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SASToken** 프로젝트를 마우스 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="e6a58-158">선택 **설정** hello 항목 다음에 대 한 값 추가:</span><span class="sxs-lookup"><span data-stu-id="e6a58-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="e6a58-159">StorageConnectionString: hello 연결 문자열 toocreate 원하는 hello 저장소 계정에 대 한 저장 된 정책 및에 대 한 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="e6a58-160">hello 형식을 해야 `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` 여기서 `myaccount` hello 저장소 계정의 이름입니다 및 `mykey` hello 저장소 계정에 대 한 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="e6a58-161">에 액세스 하려면 toorestrict hello 저장소 계정에서 ContainerName: hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="e6a58-162">SASPolicyName: hello에 대 한 이름 toouse hello 정책 toocreate를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="e6a58-163">FileToUpload: hello 경로 tooa 파일 업로드 toohello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="e6a58-164">Hello 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-164">Run hello project.</span></span> <span data-ttu-id="e6a58-165">다음 텍스트 정보 비슷한 toohello hello SAS 생성 되 면 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="e6a58-166">Hello SAS 정책 토큰이, 저장소 계정 이름과 컨테이너 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="e6a58-167">이러한 값은 hello 저장소 계정이 HDInsight 클러스터와 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="e6a58-168">Python을 사용하여 저장된 정책 및 SAS 만들기</span><span class="sxs-lookup"><span data-stu-id="e6a58-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="e6a58-169">Hello SASToken.py 파일을 열고 hello 다음 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="e6a58-170">정책\_이름: hello에 대 한 이름 toouse hello 정책 toocreate 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="e6a58-171">저장소\_계정\_이름: hello 사용자의 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="e6a58-172">저장소\_계정\_키: hello hello 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="e6a58-173">저장소\_컨테이너\_이름: hello toorestrict에 대 한 액세스를 원하는 hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="e6a58-174">예제\_파일\_경로: hello tooa 파일 경로 업로드 된 toohello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="e6a58-175">Hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-175">Run hello script.</span></span> <span data-ttu-id="e6a58-176">Hello SAS 토큰 비슷한 toohello를 hello 스크립트가 완료 되 면 텍스트를 다음으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="e6a58-177">Hello SAS 정책 토큰이, 저장소 계정 이름과 컨테이너 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="e6a58-178">이러한 값은 hello 저장소 계정이 HDInsight 클러스터와 연결할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="e6a58-179">HDInsight와 hello SAS를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e6a58-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="e6a58-180">HDInsight 클러스터를 만들 때 기본 저장소 계정을 지정해야 하며 필요에 따라 추가 저장소 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="e6a58-181">저장소를 추가 하는 두이 방법 모두에 대 한 모든 권한 toohello 저장소 계정 및 사용 되는 컨테이너 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="e6a58-182">공유 액세스 서명을 toolimit 액세스 tooa 컨테이너 toouse 추가 사용자 지정 항목 toohello **핵심 사이트** hello 클러스터에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="e6a58-183">에 대 한 **Windows 기반** 또는 **Linux 기반** HDInsight 클러스터, PowerShell을 사용 하 여 클러스터를 만드는 동안 hello 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="e6a58-184">에 대 한 **Linux 기반** HDInsight 클러스터를 Ambari를 사용 하 여 클러스터를 만든 후 hello 구성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="e6a58-185">Hello SAS를 사용 하는 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e6a58-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="e6a58-186">사용 하 여 hello SAS hello에 포함 된 HDInsight 클러스터를 만드는 예 `CreateCluster` hello 리포지토리의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="e6a58-187">toouse 설명 해 다음 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="e6a58-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="e6a58-188">열기 hello `CreateCluster\HDInsightSAS.ps1` 텍스트 편집기에서 파일 및 hello 다음 hello 문서의 hello 시작 부분에 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="e6a58-189">예를 들어 변경 `'mycluster'` toohello 이름 toocreate hello 클러스터의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="e6a58-190">저장소 계정 및 SAS 토큰을 만들 때 hello SAS 값 hello 이전 단계에서 hello 값을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="e6a58-191">Hello 값을 변경 되 면 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="e6a58-192">새 Azure PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="e6a58-193">Azure PowerShell에 익숙하지 않거나 설치되지 않은 경우 [Azure PowerShell 설치 및 구성][powershell]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a58-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="e6a58-194">Hello 프롬프트에서 명령을 tooauthenticate tooyour Azure 구독을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="e6a58-195">메시지가 표시 되 면 Azure 구독에 대 한 hello 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="e6a58-196">계정이 여러 Azure 구독과 연결 된 경우 toouse 할 수 있습니다 `Select-AzureRmSubscription` toouse 원하는 tooselect hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="e6a58-197">Hello 프롬프트에서 디렉터리 toohello 변경 `CreateCluster` hello HDInsightSAS.ps1 파일이 포함 된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="e6a58-198">다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e6a58-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="e6a58-199">Hello 스크립트 실행 될 때를 기록 출력 toohello PowerShell 프롬프트를 hello 리소스 그룹 및 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="e6a58-200">Hello HDInsight 클러스터에 대 한 증명된 tooenter hello HTTP 사용자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="e6a58-201">이 계정은 사용 되는 toosecure HTTP/s 액세스 toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="e6a58-202">Linux 기반 클러스터를 만드는 경우 SSH 사용자 계정 이름 및 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="e6a58-203">이 계정은 toohello 클러스터에 사용 되는 tooremotely 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e6a58-204">HTTP/s hello 또는 SSH 사용자 이름 및 암호에 대 한 메시지가 표시 되 면 hello 다음 조건을 충족 하는 암호를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="e6a58-205">길이가 10자 이상이어야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="e6a58-206">숫자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="e6a58-207">영숫자가 아닌 문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="e6a58-208">대문자 또는 소문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="e6a58-209">일반적으로 약 15 분이 스크립트 toocomplete 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="e6a58-210">Hello 스크립트가 오류 없이 완료 되 면 hello 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="e6a58-211">Hello SAS를 사용 하 여 기존 클러스터와</span><span class="sxs-lookup"><span data-stu-id="e6a58-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="e6a58-212">Linux 기반 기존 클러스터를 설정한 경우에 hello SAS toohello을 추가할 수 있습니다 **핵심 사이트** 단계를 수행 하는 hello를 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="e6a58-213">클러스터에 대 한 hello Ambari web UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="e6a58-214">이 페이지에 대 한 hello 주소 https://YOURCLUSTERNAME.azurehdinsight.net 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e6a58-215">대화 상자가 나타나면 인증 hello 관리자 이름 (admin)를 사용 하 여 toohello 클러스터 고 hello 클러스터를 만드는 경우 사용 되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="e6a58-216">Hello hello Ambari web UI의 왼쪽에서 선택 **HDFS** 선택한 후 hello **Configs** hello 중간 hello 페이지의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="e6a58-217">선택 hello **고급** 탭을 선택한 다음 hello를 찾을 때까지 스크롤 **사용자 지정 핵심 사이트** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e6a58-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="e6a58-218">Hello 확장 **사용자 지정 핵심 사이트** 다음 스크롤 toohello 끝 섹션과 선택 hello **속성을 추가 중...**  링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="e6a58-219">Hello에 대 한 값을 사용 하 여 hello 다음 **키** 및 **값** 필드:</span><span class="sxs-lookup"><span data-stu-id="e6a58-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="e6a58-220">**키**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e6a58-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="e6a58-221">**값**: hello 이전에 실행 하는 C#, Python 응용 프로그램에서 반환 된 SAS hello</span><span class="sxs-lookup"><span data-stu-id="e6a58-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="e6a58-222">대체 **CONTAINERNAME** hello C# 또는 SAS 응용 프로그램과 함께 사용 hello 컨테이너 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="e6a58-223">대체 **STORAGEACCOUNTNAME** hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="e6a58-224">Hello 클릭 **추가** toosave이 키 및 값을 단추 클릭 hello **저장** toosave hello에 대 한 구성 변경 내용을 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="e6a58-225">메시지가 표시 되 면 hello 변경 ("추가 SAS 저장소 액세스" 예를 들어)에 대 한 설명을 추가 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="e6a58-226">클릭 **확인** hello 변경을 완료 한 경우.</span><span class="sxs-lookup"><span data-stu-id="e6a58-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e6a58-227">Hello 변경 내용이 적용 되기 전에 몇 가지 서비스를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="e6a58-228">Hello Ambari 웹 UI에서에서 선택 **HDFS** hello hello 왼쪽, 선택한 후 목록에서 **모든 다시 시작** hello에서 **서비스 작업** 드롭 다운 목록 hello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="e6a58-229">메시지가 나타나면 **Turn on maintenance mode**을 선택한 다음 __Conform Restart All"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="e6a58-230">MapReduce2 및 YARN에 대해 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="e6a58-231">Hello 서비스를 다시 시작한 후 각 하나를 선택 하 고 hello에서 유지 관리 모드를 사용 하지 않도록 설정 **서비스 작업** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="e6a58-232">제한된 액세스 테스트</span><span class="sxs-lookup"><span data-stu-id="e6a58-232">Test restricted access</span></span>

<span data-ttu-id="e6a58-233">액세스를 사용 하 여 hello 다음 메서드를 제한 한 tooverify:</span><span class="sxs-lookup"><span data-stu-id="e6a58-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="e6a58-234">에 대 한 **Windows 기반** HDInsight 클러스터를 원격 데스크톱 tooconnect toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="e6a58-235">자세한 내용은 참조 [tooHDInsight RDP를 사용 하 여 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="e6a58-236">연결 되 면 hello를 사용 하 여 **명령줄 Hadoop** hello 데스크톱 tooopen 명령 프롬프트에서 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="e6a58-237">에 대 한 **Linux 기반** HDInsight 클러스터를 SSH tooconnect toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="e6a58-238">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a58-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="e6a58-239">Toohello 클러스터 연결 되 면 다음 단계 tooverify hello SAS 저장소 계정에만 읽기 및 목록 항목을 할 수 있는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="e6a58-240">hello 컨테이너의 toolist hello 내용을 hello hello 프롬프트에서 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="e6a58-241">대체 **SASCONTAINER** hello SAS 저장소 계정에 대해 생성 하는 hello 컨테이너의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="e6a58-242">대체 **SASACCOUNTNAME** hello SAS에 사용 되는 hello 저장소 계정의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="e6a58-243">hello 목록 hello 파일을 업로드 hello 컨테이너와 SAS를 만들 때 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="e6a58-244">사용 하 여 hello 다음 명령은 tooverify hello 파일의 hello 내용을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="e6a58-245">Hello 대체 **SASCONTAINER** 및 **SASACCOUNTNAME** hello 이전 단계에서 설명한 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="e6a58-246">대체 **FILENAME** hello 이전 명령에 표시 된 hello 파일의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="e6a58-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="e6a58-247">이 명령은 hello 파일의 내용을 hello를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="e6a58-248">다음 명령 toodownload hello 파일 toohello 로컬 파일 시스템 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="e6a58-249">이 명령은 다운로드 hello 라는 파일 tooa 로컬 파일 **testfile.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="e6a58-250">사용 하 여 hello 다음 명령은 tooupload hello 로컬 파일 tooa 라는 새 파일 **testupload.txt** hello SAS 저장소에:</span><span class="sxs-lookup"><span data-stu-id="e6a58-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="e6a58-251">텍스트 다음 메시지와 비슷한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="e6a58-252">이 오류는 hello 저장소 위치는 읽기 + 목록만 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="e6a58-253">에 나오는 명령 tooput hello 데이터에 따라 쓰기 가능한 hello 클러스터에 대 한 기본 저장소 hello hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="e6a58-254">이 시간 hello 작업이 성공적으로 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e6a58-255">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e6a58-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="e6a58-256">작업이 취소됨</span><span class="sxs-lookup"><span data-stu-id="e6a58-256">A task was canceled</span></span>

<span data-ttu-id="e6a58-257">**증상**: hello PowerShell 스크립트를 사용 하는 클러스터를 만들 때는 hello 다음과 같은 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="e6a58-258">**원인**: hello 관리자/HTTP 사용자 hello 클러스터에 대 한 또는 (Linux 기반 클러스터)에 대 한 암호를 사용 하는 경우이 오류가 발생할 수 hello SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="e6a58-259">**해결 방법**: hello 다음 조건을 충족 하는 암호를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e6a58-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="e6a58-260">길이가 10자 이상이어야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="e6a58-261">숫자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-261">Must contain at least one digit</span></span>
* <span data-ttu-id="e6a58-262">영숫자가 아닌 문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="e6a58-263">대문자 또는 소문자를 1개 이상 포함해야 함</span><span class="sxs-lookup"><span data-stu-id="e6a58-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6a58-264">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6a58-264">Next steps</span></span>

<span data-ttu-id="e6a58-265">배웠습니다 했으므로 tooadd 액세스가 제한 된 저장소 tooyour HDInsight 클러스터를 클러스터에 데이터와 다른 방법으로 toowork에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6a58-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="e6a58-266">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="e6a58-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e6a58-267">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="e6a58-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e6a58-268">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="e6a58-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
