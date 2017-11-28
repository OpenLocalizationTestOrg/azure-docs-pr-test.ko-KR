---
title: "Azure HDInsight에 R Server 시작 aaaGet | Microsoft Docs"
description: "어떻게 toocreate는 Apache는 R 서버를 포함 하는 HDInsight 클러스터에서을 멤버 알아보고 hello 클러스터에서 R 스크립트를 제출 합니다."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="8a4b7-103">HDInsight에서 R 서버 사용 시작</span><span class="sxs-lookup"><span data-stu-id="8a4b7-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="8a4b7-104">HDInsight는 HDInsight 클러스터에 통합 하는 R Server 옵션 toobe 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="8a4b7-105">이 옵션을 사용 하면 R 스크립트 toouse Spark 및 MapReduce distributed toorun 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="8a4b7-106">이 문서에서는 HDInsight 클러스터와 용 Spark를 사용 하 여 보여 주는 실행 R 스크립트에는 R 서버 toocreate R 계산을 분산 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8a4b7-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8a4b7-107">Prerequisites</span></span>

* <span data-ttu-id="8a4b7-108">**Azure 구독**: 이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="8a4b7-109">이동 toohello 문서 [Get Microsoft Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="8a4b7-110">**SSH (보안 셸) 클라이언트**: 프로그램의 SSH 클라이언트를 사용 하 tooremotely toohello HDInsight 클러스터에 연결 하 고 hello 클러스터에서 직접 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="8a4b7-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="8a4b7-112">**SSH 키 (선택 사항)**: 암호 또는 공개 키 중 하나를 사용 하 여 hello SSH 사용 되는 계정 tooconnect toohello 클러스터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="8a4b7-113">암호를 사용 하 여 보다 쉽게 이며 허용 toocreate 공개/개인 키 쌍을 필요 없이 tooget 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="8a4b7-114">하지만 키를 사용하는 것이 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="8a4b7-115">이 문서에 hello 단계는 암호를 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="8a4b7-116">자동화된 클러스터 생성</span><span class="sxs-lookup"><span data-stu-id="8a4b7-116">Automated cluster creation</span></span>

<span data-ttu-id="8a4b7-117">Azure 리소스 관리자 템플릿, SDK, hello 및 또한 PowerShell을 사용 하 여 HDInsight R 서버 hello 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="8a4b7-118">Azure 리소스 관리 템플릿을 사용 하는 R 서버 toocreate 참조 [R 서버 HDInsight 클러스터를 배포할](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="8a4b7-119">hello.NET SDK를 사용 하 여 R 서버는 toocreate 참조 [hello.NET SDK를 사용 하 여 HDInsight의 Linux 기반 클러스터를 만듭니다.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="8a4b7-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="8a4b7-120">R 서버 toodeploy에 hello 문서를 참조 powershell을 사용 하 여 [HDInsight powershell에 R 서버 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="8a4b7-121">Hello Azure 포털을 사용 하 여 hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8a4b7-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="8a4b7-122">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8a4b7-123">**새로 만들기** -> **인텔리전스 + 분석** -> **HDInsight**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![새 클러스터를 만드는 과정의 이미지](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="8a4b7-125">Hello에 **빨리 만들기** 경험 hello에 hello 클러스터에 대 한 이름을 입력 하십시오 **클러스터 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="8a4b7-126">Hello를 사용 하 여 여러 Azure 구독이 있는 경우 **구독** 항목 tooselect hello 하나 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![클러스터 이름 및 구독 선택](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="8a4b7-128">선택 **형식 클러스터** tooopen hello **클러스터 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="8a4b7-129">Hello에 **클러스터 구성** 블레이드에서 다음 옵션 선택 hello:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="8a4b7-130">**클러스터 유형**: R Server</span><span class="sxs-lookup"><span data-stu-id="8a4b7-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="8a4b7-131">**버전**: R Server tooinstall hello 클러스터에서의 select hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="8a4b7-132">현재 사용 가능한 hello 버전은 ***R 서버 (HDI 3.6) 9.1***합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="8a4b7-133">사용할 수 있는 버전의 R Server hello에 대 한 릴리스 정보는 사용할 수 있는 [여기](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="8a4b7-134">**R 서버에 대 한 R Studio community edition**:이 브라우저 기반 IDE hello 가장자리 노드에 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="8a4b7-135">Toonot 않으려면 hello 확인란의 선택을 취소 한 다음 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="8a4b7-136">Toohave를 선택 하는 경우이 앱 설치, RStudio 서버 로그인이 만들어지면 클러스터에 대 한 포털 응용 프로그램 블레이드에서 발견 된 hello에 액세스 하기 위한 hello URL.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="8a4b7-137">Hello 기본값 hello 다른 옵션을 그대로 사용 하 고 hello를 사용 하 여 **선택** toosave hello 클러스터 유형 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![클러스터 유형 블레이드 스크린샷](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="8a4b7-139">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="8a4b7-140">**SSH 사용자 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="8a4b7-141">SSH가 사용 되는 tooremotely toohello 클러스터 사용 하 여 연결 된 **SSH (보안 셸)** 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="8a4b7-142">이 대화 상자에 나 hello 클러스터 (hello hello 클러스터에 대 한 구성 탭)에서 만들어진 후 hello SSH 사용자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="8a4b7-143">R 서버는 구성 된 tooexpect는 **SSH 사용자 이름이** "remoteuser"입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="8a4b7-144">**다른 사용자 이름을 사용 하는 경우에 hello 클러스터가 생성 된 후 추가 단계를 수행 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8a4b7-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="8a4b7-145">Leave hello 상자에 대 한 검사 **동일한 암호를 사용 하 여 클러스터 로그인으로** toouse **암호** hello 인증 유형으로 공개 키의 사용을 선호 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="8a4b7-146">예를 들어 RTVS, RStudio 또는 데스크톱 다른 IDE로 원격 클라이언트를 통해 hello 클러스터에 공개/개인 키 쌍 tooaccess R Server 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="8a4b7-147">Hello RStudio Server community edition을 설치 하는 경우 toochoose SSH 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="8a4b7-148">공개/개인 키 쌍을 사용 하 여 toocreate의 선택을 취소 **동일한 암호를 사용 하 여 클러스터 로그인으로** 선택한 후 **공개 키** 다음과 같이 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="8a4b7-149">이러한 지침에서는 ssh-keygen을 포함한 Cygwin 또는 이와 동등한 프로그램이 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="8a4b7-150">노트북에 hello 명령 프롬프트에서 공개/개인 키 쌍을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="8a4b7-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="8a4b7-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="8a4b7-152">Hello 프롬프트 tooname 키 파일을 따르고 보안 강화를 위해 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="8a4b7-153">다음 이미지는 hello와 같은 화면이 표시:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-153">Your screen should look something like hello following image:</span></span>

        ![Windows의 SSH 명령줄](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="8a4b7-155">이 명령은 개인 키 파일을 만들고 hello 이름 < 개인 키 파일 >.pub furiosa 및 furiosa.pub 예를 들어 아래에서 공개 키 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH 디렉터리](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="8a4b7-157">Hello 공개 키 파일 (&#42; 그런 다음 지정. pub) 할당 HDI 클러스터 자격 증명 하 고 마지막으로 리소스 그룹 및 지역 및 선택을 확인 하는 경우 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![자격 증명 블레이드](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="8a4b7-159">노트북에 개인 키 파일 hello에 대 한 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="8a4b7-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="8a4b7-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="8a4b7-161">원격 로그인에 대 한 SSH 함께 hello 개인 키 파일을 사용.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="8a4b7-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="8a4b7-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="8a4b7-163">또는 Hadoop Spark의 부품 hello 정의 컨텍스트 R Server에 대 한 hello 클라이언트에서 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="8a4b7-164">Hello 참조 **Hadoop 클라이언트와 Microsoft R Server를 사용 하 여** 에 하위 단원 [Spark에 대 한 계산 컨텍스트를 만들어](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="8a4b7-165">hello 빨리 만들기 toohello를 전환 **저장소** 블레이드 tooselect hello 저장소 계정 설정을 toobe hello hello의 기본 위치에 사용 되는 HDFS 파일 hello 클러스터에서 사용 하는 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="8a4b7-166">새 또는 기존 Azure Storage 계정이나 기존 Data Lake Storage 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="8a4b7-167">기존 저장소 계정을 선택 하 여 선택은 Azure 저장소 계정을 선택 하는 경우 **저장소 계정을 선택** 다음 hello 관련 계정을 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="8a4b7-168">Hello를 사용 하 여 새 계정 만들기 **새로 만들기** hello에 대 한 링크 **저장소 계정을 선택** 섹션.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8a4b7-169">선택 하는 경우 **새로** hello 새 저장소 계정에 대 한 이름을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="8a4b7-170">녹색 확인 표시가 hello 이름이 수락 된 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="8a4b7-171">hello **기본 컨테이너** hello 클러스터의 기본값 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="8a4b7-172">Hello 값으로이 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="8a4b7-173">새 저장소 계정 옵션을 선택한 경우 프롬프트 tooselect **위치** 은 tooselect 제공 되는 영역 toocreate hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![데이터 원본 블레이드](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="8a4b7-175">Hello HDInsight 클러스터의 hello 위치를 설정 hello 기본 데이터 원본에 대 한 hello 위치를 선택 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="8a4b7-176">hello 클러스터와 기본 데이터 원본에에서 있어야 hello 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="8a4b7-177">선택 합니다 ADLS 저장소 계정 toouse hello 및 hello 클러스터를 추가 하려는 경우 기존 데이터 레이크 저장소 toouse, *추가* id tooyour 클러스터 tooallow 액세스 toohello 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="8a4b7-178">이 프로세스에 대한 자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="8a4b7-179">사용 하 여 hello **선택** 단추 toosave hello 데이터 소스 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="8a4b7-180">hello **요약** 블레이드 다음 표시 toovalidate 모든 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="8a4b7-181">변경할 수는 여기에 **클러스터 크기** toomodify hello 클러스터의 서버 수 및는 지정 **스크립트 작업을** toorun 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="8a4b7-182">더 큰 클러스터를 사용 해야 하는 모른다면 hello 기본값인에 hello 작업자 노드 수를 두고 `4`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="8a4b7-183">hello 예상 비용 hello 클러스터의 hello 블레이드 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![클러스터 요약](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="8a4b7-185">필요에 따라 hello 포털을 통해 나중에 클러스터 크기를 조정할 수 있습니다 (**클러스터** -> **설정** -> **배율 클러스터**) tooincrease 또는 hello 작업자 노드 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="8a4b7-186">이 크기를 조정 하는 것은 hello 클러스터 사용에 없는 경우 아래로 유휴 또는 용량 toomeet hello 요구 사항 보다 큰 작업을 추가 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="8a4b7-187">클러스터, hello 데이터 노드 및 hello 가장자리 노드 크기를 조정할 때 염두에서에 몇 가지 요인 tookeep 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="8a4b7-188">hello 성능 Spark에 분산 된 R 서버 분석에 비례 toohello 작업자 노드 수 있으면 hello 데이터가 큽니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="8a4b7-189">R 서버 분석의 hello 성능은 분석 중인 데이터의 hello 크기에 비례 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="8a4b7-190">예:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-190">For example:</span></span>  

     * <span data-ttu-id="8a4b7-191">작은 toomodest 데이터에 대 한 성능이 hello 가장자리 노드에 대 한 로컬 계산 컨텍스트를 분석 하는 경우에 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="8a4b7-192">로컬 hello 및 Spark 계산 컨텍스트는 hello 시나리오에 대 한 자세한 내용은 적합 HDInsight에 R Server에 대 한 계산 컨텍스트 옵션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="8a4b7-193">Toohello 가장자리 노드에 로그인 하 고 R 스크립트 실행 후 실행 hello ScaleR rx 함수를 제외한 모든 <strong>로컬로</strong> hello 가장자리 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="8a4b7-194">따라서 메모리 hello 및 hello 가장자리 노드의 코어 수 적절 하 게 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="8a4b7-195">hello를 사용 하는 경우 R Server HDI에 원격 연산 컨텍스트로 랩톱에서에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="8a4b7-197">사용 하 여 hello **선택** 단추 toosave hello 노드 가격 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="8a4b7-198">**템플릿 및 매개 변수 다운로드**에 대한 링크도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="8a4b7-199">선택한 구성 hello 사용 하 여 클러스터의 사용된 tooautomate hello 생성 될 수 있는이 링크 toodisplay 스크립트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="8a4b7-200">만든 후에 이러한 스크립트 hello 클러스터에 대 한 Azure 포털 항목에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8a4b7-201">일반적으로 약 20 분을 만든 hello 클러스터 toobe에 몇 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="8a4b7-202">Hello 타일 hello 시작 보드를 사용 하거나 hello **알림** hello 페이지 toocheck의 hello 만들기 프로세스에 남아 있는 hello에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="8a4b7-203">TooRStudio 서버 연결</span><span class="sxs-lookup"><span data-stu-id="8a4b7-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="8a4b7-204">설치에서 tooinclude RStudio 서버 community 버전을 선택 했으면 두 가지 방법을 통해 hello RStudio 로그인을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="8a4b7-205">Url toohello 이동 (여기서 **CLUSTERNAME** hello 클러스터를 만든 후의 hello 이름인):</span><span class="sxs-lookup"><span data-stu-id="8a4b7-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="8a4b7-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="8a4b7-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="8a4b7-207">클러스터에 대 한 hello 항목 선택 hello hello Azure 포털에서에서 열기 **R Server 대시보드** 빠른 연결을 선택한 다음 hello **R Studio 대시보드**:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Hello R studio 대시보드 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Hello R studio 대시보드 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="8a4b7-210">사용 되는 hello 방법에 관계 없이 hello 처음으로 로그인 해야 tooauthenticate 두 번 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="8a4b7-211">Hello 첫 번째 인증에 hello 제공 *Admin userid 클러스터* 및 *암호*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="8a4b7-212">Hello 두 번째 프롬프트 hello 제공 *SSH userid* 및 *암호*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="8a4b7-213">후속 로그 기능 하기만 hello *SSH 암호가* 및 *userid*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="8a4b7-214">Toohello R Server 가장자리 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="8a4b7-215">SSH를 사용 하 여 hello 명령을 사용 하 여 hello HDInsight 클러스터의 서버 가장자리 노드 tooR 연결:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="8a4b7-216">Hello를 찾을 수 있습니다 `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello 후 클러스터를 선택 하 여 Azure 포털에서에서 주소 **모든 설정을** -> **앱** -> **은 RServer**.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="8a4b7-217">Hello hello 가장자리 노드에 대 한 SSH 끝점 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Hello 가장자리 노드에 대 한 SSH 끝점 hello의 이미지](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="8a4b7-219">입력 정보 요청된 tooenter 모르는 암호 toosecure을 SSH 사용자 계정을 사용 하는 경우 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="8a4b7-220">공개 키를 사용한 경우 toouse hello `-i` 매개 변수 toospecify hello 일치 하는 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="8a4b7-221">예:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8a4b7-222">자세한 내용은 참조 [tooHDInsight (Hadoop) SSH를 사용 하 여 연결](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="8a4b7-223">연결 된 후 본사에 도착 하면 프롬프트 비슷한 toohello 다음:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="8a4b7-224">여러 동시 사용자 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="8a4b7-225">Hello 가장자리 노드 버전이 실행 되는 hello RStudio 커뮤니티에 대 한 더 많은 사용자를 추가 하 여 여러 동시 사용자가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="8a4b7-226">HDInsight 클러스터를 만들 때 다음과 같이 두 사용자, 즉 HTTP 사용자와 SSH 사용자를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![동시 사용자 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="8a4b7-228">**클러스터 로그인 사용자 이름과**: 사용자가 만든는 HTTP 사용자에 게는 사용 되는 tooprotect hello HDInsight hello HDInsight 게이트웨이 통해 인증 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="8a4b7-229">이 HTTP 사용자는 다른 UI 구성 요소 뿐만 아니라 사용 되는 tooaccess hello Ambari UI, YARN UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="8a4b7-230">**SSH 사용자 이름 보안**: 셸 보안을 통해는 SSH 사용자 tooaccess hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="8a4b7-231">이 사용자는 hello hello 헤드 노드, 작업자 노드 및 가장자리 노드 모두에 대 한 Linux 시스템의에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="8a4b7-232">사용할 수 있도록 보안 셸 tooaccess hello 노드 중 하나가 원격 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="8a4b7-233">HDInsight 유형 클러스터에서 Microsoft R Server hello에 사용 되는 hello R Studio Server 커뮤니티 버전 로그인 메커니즘으로 서 Linux 사용자 이름 및 암호를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="8a4b7-234">토큰 전달은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-234">It does not support passing tokens.</span></span> <span data-ttu-id="8a4b7-235">따라서 toouse R 스튜디오 tooaccess 고 새 클러스터를 만든 경우, 필요한 toolog에 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="8a4b7-236">먼저 hello HDInsight 게이트웨이 통해 HTTP hello 사용자 자격 증명을 사용 하 여 로그인:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![동시 사용자 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="8a4b7-238">SSH 사용자 자격 증명 toolog hello를 사용 하 여 tooRStudio에서.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![동시 사용자 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="8a4b7-240">현재 HDInsight 클러스터를 프로비전할 때 SSH 사용자 계정 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="8a4b7-241">Tooenable 여러 사용자가 tooaccess HDInsight에 대 한 Microsoft R Server를 클러스터 하도록 hello Linux 시스템에서에서 추가 사용자 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="8a4b7-242">RStudio Server 커뮤니티를 hello 클러스터 가장자리 노드에서 실행 되므로 여기에서 몇 가지 단계:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="8a4b7-243">만든 hello SSH 사용자 toolog toohello 가장자리 노드 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="8a4b7-244">에지 노드에 더 많은 Linux 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8a4b7-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="8a4b7-245">Hello 사용자가 만든 RStudio 커뮤니티 버전 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="8a4b7-246">1 단계: toohello 가장자리 노드에서 만든 hello SSH 사용자 toolog 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="8a4b7-247">모든 SSH 도구 (예: Putty)를 다운로드 하 고 hello 기존 SSH 사용자 toolog에서 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="8a4b7-248">제공 하는 hello 지침에 따라 [tooHDInsight (Hadoop) SSH를 사용 하 여 연결](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello 가장자리 노드.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="8a4b7-249">HDInsight 클러스터에서 hello 가장자리 노드 주소가 R 서버에 대 한: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="8a4b7-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="8a4b7-250">2단계: 에지 노드에 더 많은 Linux 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="8a4b7-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="8a4b7-251">사용자 toohello 가장자리 노드 tooadd hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="8a4b7-252">다음 항목을 반환 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-252">You should see hello following items returned:</span></span> 

![동시 사용자 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="8a4b7-254">에 대 한 메시지가 표시 되 면 "현재 Kerberos 암호:", 누르기만 **Enter** tooignore 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="8a4b7-255">hello `-m` 옵션 `useradd` 명령은 hello 시스템에서 RStudio 커뮤니티 버전에 필요한 hello 사용자에 대 한 홈 폴더를 만듦을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="8a4b7-256">사용자가 만든 hello와 3 단계: 사용 RStudio 커뮤니티 버전</span><span class="sxs-lookup"><span data-stu-id="8a4b7-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="8a4b7-257">사용자가 만든 toolog hello를 사용 하 여 tooRStudio에서:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-257">Use hello user created toolog in tooRStudio:</span></span>

![동시 사용자 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="8a4b7-259">RStudio 있음을 나타내도록 hello 새 사용자를 사용 하는 알림 (여기에서는 예를 들어 *sshuser6*) toolog hello 클러스터에서:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![동시 사용자 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="8a4b7-261">Hello 원래 자격 증명을 사용 하 여 로그인 할 수 있습니다 (기본적으로 *sshuser*) 다른 브라우저 창에서 동시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="8a4b7-262">scaleR 함수를 사용하여 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="8a4b7-263">다음 hello 사용 되는 명령 toorun의 예는 작업은:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="8a4b7-264">YARN UI에서 다른 사용자 이름 아래에서 제출 하는 hello 작업이 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![동시 사용자 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="8a4b7-266">또한 해당 hello 새로 추가 된 사용자가 루트 권한을 Linux 시스템에서 필요는 없지만 이러한 않습니다는 hello 동일한 참고 hello 원격 HDFS와 WASB 저장소에 tooall hello 파일에 액세스할 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="8a4b7-267">Hello R 콘솔을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8a4b7-267">Use hello R console</span></span>

1. <span data-ttu-id="8a4b7-268">Hello SSH 세션에서 다음 명령 toostart hello R 콘솔 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="8a4b7-269">유사한 toohello 다음 출력이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="8a4b7-270">R 3.2.2 (2015-08-14)-버전 "화재 안전" Copyright (C) 2015 통계 컴퓨팅 플랫폼에 대 한 R Foundation hello: x86_64-pc-linux-gnu (64 비트)</span><span class="sxs-lookup"><span data-stu-id="8a4b7-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="8a4b7-271">R은 평가판 소프트웨어이며 절대로 어떠한 보증도 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="8a4b7-272">시작 tooredistribute는 특정 조건에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="8a4b7-273">배포에 대한 자세한 내용을 보려면 'license()' 또는 'licence()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="8a4b7-274">자연어가 지원되지만 영어 로캘로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="8a4b7-275">R은 많은 참가자가 함께한 공동 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="8a4b7-276">게시에서 toocite R 또는 R 패키지 하는 방법에 대 한 자세한 내용과 'citation()' 'contributors()'를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="8a4b7-277">일부 데모, 온라인 도움말에 대 한 ' help()' 또는 'help.start()' HTML 브라우저 인터페이스 toohelp에 대 한 'demo()'를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="8a4b7-278">'Q()' tooquit 오른쪽 입력</span><span class="sxs-lookup"><span data-stu-id="8a4b7-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="8a4b7-279">Microsoft R Server 버전 8.0: R Microsoft 패키지의 향상된 배포 Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="8a4b7-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="8a4b7-280">릴리스 정보를 보려면 'readme()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="8a4b7-281">Hello에서 `>` 프롬프트 R 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="8a4b7-282">R 서버 tooeasily를 허용 하는 패키지에 포함 되어 Hadoop으로 상호 작용 하 고 분산 된 계산을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="8a4b7-283">예를 들어 다음 hello HDInsight 클러스터에 대 한 hello 기본 파일 시스템의 명령 tooview hello 루트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="8a4b7-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="8a4b7-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="8a4b7-285">Hello WASB 스타일 주소 지정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="8a4b7-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="8a4b7-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="8a4b7-287">Microsoft R Server 또는 Microsoft R 클라이언트의 원격 인스턴스에서 HDI의 R Server 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="8a4b7-288">Microsoft R Server 또는 데스크톱 또는 랩톱에서 실행 되는 Microsoft R 클라이언트의 원격 인스턴스에서 액세스 toohello HDI Hadoop Spark 계산 컨텍스트를 가능한 tooset 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="8a4b7-289">참조 **Hadoop 클라이언트와 Microsoft R Server를 사용 하 여** hello에 하위 섹션 [Spark에 대 한 계산 컨텍스트를 만드는](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="8a4b7-290">toodo toospecify hello 노트북에 hello RxSpark 계산 컨텍스트를 정의할 때 다음 옵션을 필요한 따라서: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, 및 sshProfileScript 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="8a4b7-291">예:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="8a4b7-292">계산 컨텍스트 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-292">Use a compute context</span></span>

<span data-ttu-id="8a4b7-293">계산 컨텍스트가 있습니다 toocontrol을 계산을 hello HDInsight 클러스터의 hello 노드에 분산 여부 hello 가장자리 노드에서 로컬로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="8a4b7-294">RStudio 서버나 (에 대 한 SSH 세션) hello R 콘솔에서 hello 기본 저장소에 HDInsight에 대 한 코드 tooload 예제 데이터를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="8a4b7-295">다음으로, 보겠습니다 일부 데이터 정보를 만들고 म hello 데이터로 작업할 수 있도록 두 개의 데이터 소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="8a4b7-296">Hello 로컬 계산 컨텍스트를 사용 하 여 hello 데이터에 대해 로지스틱 회귀를 실행 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="8a4b7-297">출력 줄 비슷한 toohello 다음으로 끝나는 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="8a4b7-298">그런 다음 확인해 보겠습니다 hello Spark 컨텍스트를 사용 하 여 동일한 로지스틱 회귀 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="8a4b7-299">hello Spark 컨텍스트 hello hello HDInsight 클러스터의 모든 hello 작업자 노드를 통해 처리를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="8a4b7-300">또한 클러스터 노드에서 MapReduce toodistribute 계산을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="8a4b7-301">계산 컨텍스트에 대한 자세한 내용은 [HDInsight에서 R Server의 Compute 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="8a4b7-302">R 코드 toomultiple 노드 배포</span><span class="sxs-lookup"><span data-stu-id="8a4b7-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="8a4b7-303">R server 쉽게 기존 R 코드를 사용 하 고 수를 사용 하 여 hello 클러스터의 여러 노드에서 실행 `rxExec`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="8a4b7-304">이 함수는 매개 변수 비우기 또는 시뮬레이션을 수행할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="8a4b7-305">hello 다음 코드는 방법의 예로 toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="8a4b7-306">여전히 Spark hello 또는 MapReduce 컨텍스트를 사용 하는 경우이 명령은 값을 반환 hello nodename hello 작업자 노드에 대 한 해당 hello 코드 `(Sys.info()["nodename"])` 에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="8a4b7-307">예를 들어 4 개 노드 클러스터에서 예상 tooreceive toohello 다음과 유사한 출력:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="8a4b7-308">Hive 및 Parquet의 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="8a4b7-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="8a4b7-309">R 서버 9.1에서 제공 되는 기능에는 hello Spark 계산 컨텍스트에서 ScaleR 함수에서 사용 하기 위해 Hive 및 Parquet에 대 한 직접 액세스 toodata를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="8a4b7-310">이러한 기능을 기능을 통해 새 ScaleR 데이터 소스 RxHiveData 및 RxParquetData 라는 Spark 데이터 프레임이 ScaleR에 따라 분석에 직접 Spark SQL tooload 데이터의 사용을 통해 작동 하는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="8a4b7-311">hello 코드 다음 몇 가지 샘플 코드 hello 새 기능을 사용 하는 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="8a4b7-312">이 새 함수에 대 한 추가 정보에 대 한 hello 사용 하 여 R Server에 hello 온라인 도움말을 참조 `?RxHivedata` 및 `?RxParquetData` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="8a4b7-313">Hello 가장자리 노드에 추가 R 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="8a4b7-314">Hello 가장자리 노드에서 tooinstall 추가 R 패키지를 선택 하는 경우 사용할 수 있습니다 `install.packages()` 직접 내에서 R 콘솔 연결된 toohello SSH 통해 노드 가장자리 때 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="8a4b7-315">그러나 hello 클러스터의 작업자 노드 hello에 tooinstall R 패키지를 해야 하는 경우에 스크립트 작업을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="8a4b7-316">스크립트 동작 하는 사용 되는 toomake 구성 변경 내용을 toohello HDInsight 클러스터 또는 tooinstall 추가 같은 소프트웨어를 추가 R 패키지는 Bash 스크립트.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="8a4b7-317">스크립트 동작을 사용 하 여 tooinstall 추가 패키지 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a4b7-318">스크립트 동작 tooinstall 추가 R 패키지를 사용 하 여만 사용할 수 있습니다 hello 클러스터를 만든 후.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="8a4b7-319">Hello 스크립트에서는 R Server 완전히 설치 및 구성 하는 대로 클러스터를 만드는 동안이 절차를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="8a4b7-320">Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터에서 R 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="8a4b7-321">Hello에서 **설정** 블레이드를 **스크립트 동작** 차례로 **새 제출** toosubmit 새 스크립트 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![스크립트 작업 블레이드의 이미지](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="8a4b7-323">Hello에서 **스크립트 동작을 제출** 블레이드에서 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="8a4b7-324">**이름**: 친숙 한 이름을 tooidentify이이 스크립트</span><span class="sxs-lookup"><span data-stu-id="8a4b7-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="8a4b7-325">**Bash 스크립트 URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="8a4b7-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="8a4b7-326">**헤드**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="8a4b7-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="8a4b7-327">**작업자**: **선택**이어야 함</span><span class="sxs-lookup"><span data-stu-id="8a4b7-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="8a4b7-328">**에지 노드**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="8a4b7-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="8a4b7-329">**Zookeeper**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="8a4b7-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="8a4b7-330">**매개 변수**: hello R 패키지 설치 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="8a4b7-331">예를 들어 `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="8a4b7-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="8a4b7-332">**이 스크립트 유지...**: **선택**이어야 함</span><span class="sxs-lookup"><span data-stu-id="8a4b7-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="8a4b7-333">기본적으로 hello Microsoft MRAN 리포지토리의 hello 버전의 설치 된 R Server와 일관 된 스냅숏에서 모든 R 패키지가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="8a4b7-334">최신 버전의 패키지 tooinstall 하려는 경우 다음 위험은 일부의 비 호환성입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="8a4b7-335">그러나이 설치 유형은 수를 지정 하 여 `useCRAN` hello로 hello 패키지의 첫 번째 요소 목록, 예를 들어 `useCRAN bitops, stringr, arules`합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="8a4b7-336">일부 R 패키지에는 추가 Linux 시스템 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="8a4b7-337">편의 위해 우리는 사전 설치 된 hello 상위 100 가장 인기 있는 R 패키지에 필요한 hello 종속성.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="8a4b7-338">그러나 이러한 보다 더 많은 라이브러리를 필요 hello R 패키지를 설치한 경우 다음 여기에 hello 기본 스크립트를 다운로드 하며 단계 tooinstall hello 시스템 라이브러리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="8a4b7-339">업로드 수정 hello 스크립트 tooa 공용 Azure 저장소 컨테이너에에서 blob 하 고 수정 하는 hello 스크립트 tooinstall hello 패키지를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="8a4b7-340">스크립트 작업 개발에 대한 자세한 내용은 [스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![스크립트 작업 추가](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="8a4b7-342">선택 **만들기** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="8a4b7-343">Hello 스크립트가 완료 되 면 hello R 패키지는 모든 작업자 노드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="8a4b7-344">Microsoft R Server 조작화 사용</span><span class="sxs-lookup"><span data-stu-id="8a4b7-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="8a4b7-345">데이터 모델링 완료 되 면 hello 모델 toomake 예측 실제로 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="8a4b7-346">Microsoft R Server 화에 대 한 tooconfigure hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="8a4b7-347">첫째, ssh hello 가장자리 노드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="8a4b7-348">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8a4b7-349">사용 하 여 ssh를 hello 관련 버전 및 sudo hello dotnet dll에 대 한 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="8a4b7-350">Microsoft R Server 9.1의 경우:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="8a4b7-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="8a4b7-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="8a4b7-352">Microsoft R Server 9.0의 경우:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="8a4b7-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="8a4b7-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="8a4b7-354">한 기본 구성 사용 하 여 Microsoft R Server 해결해줍니다 tooconfigure 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="8a4b7-355">[R Server 조작화 구성]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="8a4b7-356">“A.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-356">Select “A.</span></span> <span data-ttu-id="8a4b7-357">One-box(웹 + 계산 노드)”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="8a4b7-358">Hello에 대 한 암호를 입력 **admin** 사용자</span><span class="sxs-lookup"><span data-stu-id="8a4b7-358">Enter a password for hello **admin** user</span></span>

![one-box 조작화](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="8a4b7-360">선택적 단계로 다음과 같이 진단 테스트를 실행하여 진단 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="8a4b7-361">“6.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-361">Select “6.</span></span> <span data-ttu-id="8a4b7-362">진단 테스트 실행”을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="8a4b7-363">“A.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-363">Select “A.</span></span> <span data-ttu-id="8a4b7-364">구성 테스트”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-364">Test configuration”</span></span>
3. <span data-ttu-id="8a4b7-365">이전 구성 단계에서 사용자 이름("admin")과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="8a4b7-366">Confirm Overall Health(전체 상태 확인)이 pass(합격)인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="8a4b7-367">종료 hello 관리 유틸리티</span><span class="sxs-lookup"><span data-stu-id="8a4b7-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="8a4b7-368">SSH를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-368">Exit SSH</span></span>

![조작화에 대한 진단](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="8a4b7-370">**Spark에 웹 서비스를 이용할 때 긴 지연**</span><span class="sxs-lookup"><span data-stu-id="8a4b7-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="8a4b7-371">Spark 계산 컨텍스트에서 mrsdeploy 함수를 사용 하 여 만든 웹 서비스 tooconsume 동안 오래 지연 발생 하면 일부 누락 된 폴더에 tooadd 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="8a4b7-372">hello Spark 응용 프로그램 이라는 tooa 사용자 속해 '*rserve2*' 때마다 mrsdeploy 함수를 사용 하는 웹 서비스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="8a4b7-373">이 문제를 해결 toowork:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="8a4b7-374">이 단계에서 화에 대 한 hello 구성이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="8a4b7-375">사용할 수 있습니다 이제 'hello 'mrsdeploy 가장자리 노드 여 RClient tooconnect toohello 화에 패키지 하 고과 같은 해당 기능을 사용 하 여 시작 [원격 실행](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) 및 [웹 서비스](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="8a4b7-376">설정에 따라 여부 클러스터 가상 네트워크에 여부, tooset SSH 로그인을 통해 포트 전달 터널링을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="8a4b7-377">hello 다음 섹션에서는 어떻게 tooset이이 터널이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="8a4b7-378">가상 네트워크의 RServer 클러스터</span><span class="sxs-lookup"><span data-stu-id="8a4b7-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="8a4b7-379">포트 12800 toohello 가장자리 노드를 통해 트래픽을 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="8a4b7-380">이런 방식으로 hello 가장자리 노드 tooconnect toohello 화 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="8a4b7-381">경우 hello `remoteLogin()` 없습니다 toohello 가장자리 노드를 연결 하지만 SSH toohello 가장자리 노드 수 해야 합니다 tooverify 제대로 또는 하지 hello 규칙 tooallow 트래픽 12800 포트에서 설정 된 여부.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="8a4b7-382">Tooface hello 문제를 계속 진행 하면 SSH를 통해 정방향 터널링 포트를 설정 하 여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="8a4b7-383">Hello 다음 단원을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="8a4b7-384">가상 네트워크에 설정되지 않은 RServer 클러스터</span><span class="sxs-lookup"><span data-stu-id="8a4b7-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="8a4b7-385">클러스터가 VNet에 설정되지 않았거나 VNet을 통한 연결에 문제가 있는 경우 SSH 포트 전달 터널링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="8a4b7-386">Putty에서도 이 터널링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-386">On Putty, you can set it up as well.</span></span>

![Putty ssh 연결](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="8a4b7-388">SSH 세션이 활성 상태인 컴퓨터의 포트 12800 hello 트래픽은 toohello 가장자리 노드 포트 12800 SSH 세션을 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="8a4b7-389">`remoteLogin()` 메서드에서 `127.0.0.1:12800`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="8a4b7-390">이 포트 전달을 통해 toohello 가장자리 노드 화에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="8a4b7-391">Microsoft R Server 해결해줍니다 tooscale HDInsight 작업자 노드에 있는 노드를 계산 하는 방법</span><span class="sxs-lookup"><span data-stu-id="8a4b7-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="8a4b7-392">Hello 작업자 노드를 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="8a4b7-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="8a4b7-393">Microsoft R Server는 현재 Yarn을 통해 관리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="8a4b7-394">Hello 작업자 노드를 서비스 해제 없는 hello Yarn 리소스 관리자의 hello 서버에서 차지 하는 hello 리소스 인식 되지 않습니다 때문에 예상 대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="8a4b7-395">순서 tooavoid이이 경우 권장 hello 계산 노드를 확장 하기 전에 hello 작업자 노드를 서비스 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="8a4b7-396">단계 toodecommissioning 작업자 노드:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="8a4b7-397">Ambari 콘솔 tooHDI 클러스터를 로그인 하 고 "호스트" 탭을 클릭</span><span class="sxs-lookup"><span data-stu-id="8a4b7-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="8a4b7-398">작업자 노드 (toobe 서비스 해제) 선택 "작업"를 클릭 하십시오. > "선택한 호스트" > "호스트" > "ON 유지 관리 모드 설정"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="8a4b7-399">예를 들어 다음 이미지는 hello म wn3 및 wn4 toodecommission을 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![작업자 노드 서비스 해제](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="8a4b7-401">**작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **서비스 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="8a4b7-402">**작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **서비스 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="8a4b7-403">**작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="8a4b7-404">**작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="8a4b7-405">**작업** > **선택한 호스트** > **호스트**를 선택하고 > **모든 구성 요소 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="8a4b7-406">Hello 헤드 노드를 선택 하 고 hello 작업자 노드를 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="8a4b7-407">**작업** > **선택한 호스트** > "**호스트** > **모든 구성 요소 다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="8a4b7-408">서비스 해제된 작업자 노드 각각에 Compute 노드 구성</span><span class="sxs-lookup"><span data-stu-id="8a4b7-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="8a4b7-409">SSH를 서비스 해제된 각 작업자 노드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="8a4b7-410">`dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`을 사용하여 관리 유틸리티를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="8a4b7-411">"1" tooselect 옵션 "구성 R 서버에 대 한 해결해줍니다"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="8a4b7-412">입력 "c" tooselect 옵션 "3.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="8a4b7-413">Compute 노드" 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-413">Compute node".</span></span> <span data-ttu-id="8a4b7-414">그러면 hello 작업자 노드 hello 계산 노드를 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="8a4b7-415">종료 hello 관리 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="8a4b7-416">웹 노드에 계산 노드 세부 정보 추가</span><span class="sxs-lookup"><span data-stu-id="8a4b7-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="8a4b7-417">모든 서비스가 해제 된 작업자 노드 구성 되 면 toorun 계산 노드, hello 가장자리 노드에서 돌아와 hello Microsoft R Server 웹 노드 구성에서 폐기 된 작업자 노드 IP 주소 추가:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="8a4b7-418">Hello 가장자리 노드로 SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="8a4b7-419">`vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="8a4b7-420">Hello "Uri" 섹션을 살펴보고 작업자 노드 IP 및 포트 세부 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![작업자 노드 서비스 해제 명령줄](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="8a4b7-422">문제 해결</span><span class="sxs-lookup"><span data-stu-id="8a4b7-422">Troubleshoot</span></span>

<span data-ttu-id="8a4b7-423">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8a4b7-424">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a4b7-424">Next steps</span></span>

<span data-ttu-id="8a4b7-425">이제 새 HDInsight 클러스터를 사용 하 여 hello R 서버 및 hello 기본 사항 toocreate 대 한 SSH 세션에서 R 콘솔 hello 하는 방법을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4b7-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="8a4b7-426">hello 다음 항목에서는 설명 관리 하 고 HDInsight에 R server 작업의 다른 방법:</span><span class="sxs-lookup"><span data-stu-id="8a4b7-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="8a4b7-427">RStudio 서버 tooHDInsight 추가 (클러스터를 만드는 동안 설치 되지 않은) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="8a4b7-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="8a4b7-428">HDInsight의 R 서버에 대한 Compute 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="8a4b7-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="8a4b7-429">HDInsight에서 R Server의 Azure Storage 옵션</span><span class="sxs-lookup"><span data-stu-id="8a4b7-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
