---
title: "HDInsight에서 R Server 시작 - Azure | Microsoft Docs"
description: "R Server를 포함하는 HDInsight 클러스터에서 Apache Spark를 만들고 클러스터에 R 스크립트를 제출하는 방법을 알아봅니다."
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
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="6d543-103">HDInsight에서 R 서버 사용 시작</span><span class="sxs-lookup"><span data-stu-id="6d543-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="6d543-104">HDInsight에는 HDInsight 클러스터에 통합되는 R Server 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="6d543-105">이 옵션을 사용하면 R 스크립트에서 Spark 및 MapReduce를 사용하여 분산된 계산을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="6d543-106">이 문서에서는 HDInsight 클러스터에서 R Server를 만든 다음 R 스크립트를 실행하여 분산된 R 계산에 Spark를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6d543-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d543-107">Prerequisites</span></span>

* <span data-ttu-id="6d543-108">**Azure 구독**: 이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="6d543-109">자세한 내용을 보려면 [Microsoft Azure 평가판 받기](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) 문서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="6d543-110">**SSH(보안 셸) 클라이언트**: SSH 클라이언트는 HDInsight 클러스터에 원격으로 연결하여 클러스터에서 직접 명령을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="6d543-111">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="6d543-112">**SSH 키(선택 사항)**: 암호 또는 공개 키를 사용하여 클러스터에 연결할 때 사용되는 SSH 계정을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="6d543-113">암호를 사용하면 작업이 보다 간편하며, 공개/개인 키 쌍을 만들지 않고도 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="6d543-114">하지만 키를 사용하는 것이 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="6d543-115">이 문서의 단계에서는 암호를 사용하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="6d543-116">자동화된 클러스터 생성</span><span class="sxs-lookup"><span data-stu-id="6d543-116">Automated cluster creation</span></span>

<span data-ttu-id="6d543-117">Azure Resource Manager 템플릿, SDK 및 PowerShell을 사용하여 HDInsight R 서버 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="6d543-118">Azure Resource Management 템플릿을 사용하여 R Server를 만들려면 [R Server HDInsight 클러스터 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="6d543-119">.NET SDK를 사용하여 R 서버를 만들려면 [.NET SDK를 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="6d543-120">PowerShell을 사용하여 R Server를 배포하려면 [PowerShell을 사용하여 HDInsight에서 R Server 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="6d543-121">Azure Portal을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6d543-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="6d543-122">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6d543-123">**새로 만들기** -> **인텔리전스 + 분석** -> **HDInsight**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![새 클러스터를 만드는 과정의 이미지](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="6d543-125">**빠른 생성** 환경에서 **클러스터 이름** 필드에 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="6d543-126">Azure 구독이 여러 개 있는 경우 **구독** 항목을 사용하여 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![클러스터 이름 및 구독 선택](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="6d543-128">**클러스터 유형**을 선택하여 **클러스터 구성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="6d543-129">**클러스터 구성** 블레이드에서 다음 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="6d543-130">**클러스터 유형**: R Server</span><span class="sxs-lookup"><span data-stu-id="6d543-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="6d543-131">**버전**: 클러스터에 설치할 R Server의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="6d543-132">현재 사용 가능한 버전은 ***R Server 9.1(HDI 3.6)***입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="6d543-133">사용 가능한 R Server 버전의 릴리스 정보는 [여기](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="6d543-134">**R Server용 R Studio Community Edition**: 이 브라우저 기반 IDE는 기본적으로 에지 노드에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="6d543-135">설치하지 않으려면 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="6d543-136">설치를 선택하면 만들어진 클러스터의 포털 응용 프로그램 블레이드에서 RStudio Server 로그인에 액세스하기 위한 URL을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="6d543-137">다른 옵션은 기본값으로 남겨 두고 **선택** 단추를 사용하여 클러스터 유형을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![클러스터 유형 블레이드 스크린샷](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="6d543-139">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="6d543-140">**SSH 사용자 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="6d543-141">SSH는 **SSH(보안 셸)** 클라이언트를 사용하여 클러스터에 원격으로 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="6d543-142">클러스터(클러스터에 대한 [구성] 탭)를 만든 후에 이 대화 상자에서 SSH 사용자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="6d543-143">R Server는 "remoteuser"라는 **SSH 사용자 이름**를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="6d543-144">**다른 사용자 이름을 사용하면 클러스터를 만든 후에 추가 단계를 수행해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6d543-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="6d543-145">공개 키를 사용하려는 경우가 아니면 상자에서 **클러스터 로그인과 동일한 암호 사용**을 선택하여 **암호**를 인증 유형으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="6d543-146">RTVS, RStudio 또는 다른 데스크톱 IDE와 같은 원격 클라이언트를 통해 클러스터에서 R Server에 액세스하려는 경우 공개/개인 키 쌍이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="6d543-147">RStudio Server Community Edition을 설치하려면 SSH 암호를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="6d543-148">공개/개인 키 쌍을 만들고 사용하려면 **클러스터 로그인과 동일한 암호 사용**의 확인을 취소한 다음 **공개 키**를 선택하고 다음과 같이 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="6d543-149">이러한 지침에서는 ssh-keygen을 포함한 Cygwin 또는 이와 동등한 프로그램이 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="6d543-150">랩톱 컴퓨터의 명령 프롬프트에서 공개/개인 키 쌍을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="6d543-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="6d543-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="6d543-152">프롬프트를 따라서 키 파일 이름을 지정하고 보안 강화를 위해 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="6d543-153">화면은 다음 이미지와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-153">Your screen should look something like the following image:</span></span>

        ![Windows의 SSH 명령줄](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="6d543-155">이 명령은 개인 키 파일 및 공개 키 파일을 <private-key-filename>.pub이라는 이름으로 만듭니다(예: furiosa 및 furiosa.pub).</span><span class="sxs-lookup"><span data-stu-id="6d543-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH 디렉터리](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="6d543-157">그러면 HDI 클러스터 자격 증명을 할당할 때 공개 키 파일(&#42;.pub)을 지정하고 리소스 그룹 및 지역을 마지막으로 확인한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![자격 증명 블레이드](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="6d543-159">랩톱의 개인 키 파일에 대한 사용 권한 변경:</span><span class="sxs-lookup"><span data-stu-id="6d543-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="6d543-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="6d543-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="6d543-161">원격 로그인을 위해 SSH와 함께 개인 키 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="6d543-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="6d543-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="6d543-163">또는 클라이언트에서 R Server에 대한 Hadoop Spark 계산 컨텍스트 정의의 일부를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="6d543-164">[Spark에 대한 Compute 컨텍스트 만들기](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)에서 **Hadoop 클라이언트로 Microsoft R Server 사용** 하위 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="6d543-165">빠른 생성은 사용자를 **Storage** 블레이드로 전환하여 클러스터에서 사용하는 HDFS 파일 시스템의 기본 위치에 사용될 저장소 계정 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="6d543-166">새 또는 기존 Azure Storage 계정이나 기존 Data Lake Storage 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="6d543-167">Azure Storage 계정을 선택하면 **저장소 계정 선택**을 선택한 다음 관련 계정을 선택하여 기존 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="6d543-168">**저장소 계정 선택** 섹션에서 **새로 만들기** 링크를 사용하여 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6d543-169">**새로 만들기**를 선택한 경우 새 저장소 계정의 이름을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="6d543-170">이름이 허용되는 경우 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="6d543-171">**기본 컨테이너**는 기본적으로 클러스터 이름으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="6d543-172">이 기본값을 값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-172">Leave this default as the value.</span></span>

      <span data-ttu-id="6d543-173">새 저장소 계정 옵션을 선택한 경우 **위치**를 선택하라는 메시지가 표시되며, 여기서 저장소 계정을 만들 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![데이터 원본 블레이드](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="6d543-175">기본 데이터 원본의 위치를 선택하면 HDInsight 클러스터의 위치도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="6d543-176">클러스터와 기본 데이터 원본은 같은 하위 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="6d543-177">기존 Data Lake Store를 사용하려는 경우 사용할 ADLS 저장소 계정을 선택하고 클러스터에 클러스터 *ADD* ID를 추가하여 저장소에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="6d543-178">이 프로세스에 대한 자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="6d543-179">**선택** 단추를 사용하여 데이터 원본 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="6d543-180">그러면 **요약** 블레이드가 표시되어 모든 설정의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="6d543-181">여기서는 **클러스터 크기**를 변경하여 클러스터에 있는 서버 수를 수정하고 실행하려는 **스크립트 작업**을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="6d543-182">더 큰 클러스터가 필요한 경우가 아니면 작업자 노드 수를 기본값(`4`)으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="6d543-183">클러스터의 예상 비용이 블레이드 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![클러스터 요약](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="6d543-185">필요한 경우 나중에 포털을 통해 다시 클러스터의 크기를 조정하여(**클러스터** -> **설정** -> **클러스터 크기 조정**) 작업자 노드의 수를 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="6d543-186">이와 같이 크기를 조정하면 클러스터를 사용하지 않을 때 유휴 상태로 유지하거나 대규모 작업의 요구에 맞게 용량을 추가하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="6d543-187">클러스터, 데이터 노드 및 에지 노드의 크기를 조정할 때 염두할 몇 가지 요인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="6d543-188">Spark에서 분산된 R 서버 분석의 성능은 데이터가 클 경우 작업자 노드 수에 비례합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="6d543-189">R 서버 분석의 성능은 분석 중인 데이터의 크기에 비례합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="6d543-190">예:</span><span class="sxs-lookup"><span data-stu-id="6d543-190">For example:</span></span>  

     * <span data-ttu-id="6d543-191">작은 데이터부터 보통 크기의 데이터의 경우 성능은 에지 노드의 로컬 계산 컨텍스트에서 분석할 때 가장 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="6d543-192">로컬 및 Spark 계산 컨텍스트가 가장 잘 작동하는 시나리오에 대한 자세한 내용은 HDInsight에서 R Server의 Compute 컨텍스트 옵션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="6d543-193">에지 노드에 로그인하고 R 스크립트를 실행하면 ScaleR rx 함수를 제외한 모든 항목이 에지 노드에서 <strong>로컬로</strong> 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="6d543-194">따라서 에지 노드의 코어 수 및 메모리 크기를 적절하게 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="6d543-195">HDI의 R Server를 랩톱 컴퓨터의 원격 계산 컨텍스트로 사용할 경우에도 동일하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="6d543-197">**선택** 단추를 사용하여 노드 가격 책정 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="6d543-198">**템플릿 및 매개 변수 다운로드**에 대한 링크도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="6d543-199">이 링크를 클릭하면 선택한 구성으로 클러스터의 생성을 자동화하는 데 사용할 수 있는 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="6d543-200">이러한 스크립트는 만들어진 클러스터의 Azure Portal 항목에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d543-201">클러스터를 만드는 데 약간의 시간이 걸리며, 일반적으로 약 20분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="6d543-202">시작 보드에 있는 타일 또는 페이지 왼쪽에 있는 **알림** 항목을 사용하여 생성 프로세스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="6d543-203">RStudio Server에 연결</span><span class="sxs-lookup"><span data-stu-id="6d543-203">Connect to RStudio Server</span></span>

<span data-ttu-id="6d543-204">설치 시 RStudio Server Community Edition을 포함하도록 선택한 경우 별도의 두 가지 방법으로 RStudio 로그인에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="6d543-205">다음 URL로 이동합니다(여기서 **CLUSTERNAME**은 만든 클러스터의 이름임).</span><span class="sxs-lookup"><span data-stu-id="6d543-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="6d543-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="6d543-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="6d543-207">Azure Portal에서 클러스터 항목을 열고 **R Server 대시보드** 빠른 링크를 선택한 다음 **R Studio 대시보드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![R Studio 대시보드에 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![R Studio 대시보드에 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6d543-210">사용한 방법과 관계 없이 처음 로그인할 때는 두 번 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="6d543-211">첫 번째 인증에서 *클러스터 관리자 사용자 ID*와 *암호*를 제공하고,</span><span class="sxs-lookup"><span data-stu-id="6d543-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="6d543-212">두 번째 프롬프트에서 *SSH 사용자 ID*와 *암호*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="6d543-213">후속 로그인에서는 *SSH 사용자 ID*와 *암호*만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="6d543-214">R Server 에지 노드에 연결</span><span class="sxs-lookup"><span data-stu-id="6d543-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="6d543-215">다음 명령으로 SSH를 사용하여 HDInsight 클러스터의 R Server 에지 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="6d543-216">Azure Portal에서 클러스터를 선택한 다음 **모든 설정** -> **앱** -> **RServer**를 차례로 선택하여 `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="6d543-217">그러면 에지 노드에 대한 SSH 끝점 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![에지 노드에 대한 SSH 끝점의 이미지](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="6d543-219">SSH 사용자 계정을 보호하는 암호를 사용한 경우 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="6d543-220">공용 키를 사용하는 경우, `-i` 매개 변수를 사용하고 일치하는 개인 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="6d543-221">예:</span><span class="sxs-lookup"><span data-stu-id="6d543-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6d543-222">자세한 내용은 [SSH를 사용하여 HDInsight(Hadoop)에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="6d543-223">연결되면 다음과 유사한 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="6d543-224">여러 동시 사용자 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="6d543-225">RStudio Community 버전이 실행되는 에지 노드에 대해 더 많은 사용자를 추가하여 여러 동시 사용자를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="6d543-226">HDInsight 클러스터를 만들 때 다음과 같이 두 사용자, 즉 HTTP 사용자와 SSH 사용자를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![동시 사용자 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="6d543-228">**클러스터 로그인 사용자 이름**: 사용자가 만든 HDInsight 클러스터를 보호하는 데 사용되는 HDInsight 게이트웨이를 통해 인증하기 위한 HTTP 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="6d543-229">이 HTTP 사용자는 Ambari UI, YARN UI 및 다른 UI 구성 요소에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="6d543-230">**SSH(보안 셸) 사용자 이름**: 보안 셸을 통해 클러스터에 액세스하는 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="6d543-231">이 사용자는 모든 헤드 노드, 작업자 노드 및 에지 노드에 대한 Linux 시스템의 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="6d543-232">따라서 보안 셸을 사용하여 원격 클러스터의 노드 중 하나에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="6d543-233">HDInsight 유형 클러스터의 Microsoft R Server에 사용되는 R Studio Server Community 버전은 로그인 메커니즘으로 Linux 사용자 이름과 암호만 허용하며,</span><span class="sxs-lookup"><span data-stu-id="6d543-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="6d543-234">토큰 전달은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-234">It does not support passing tokens.</span></span> <span data-ttu-id="6d543-235">따라서 새 클러스터를 만들고 R Studio를 사용하여 액세스하려는 경우 두 번 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="6d543-236">먼저 HDInsight 게이트웨이를 통해 HTTP 사용자 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![동시 사용자 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="6d543-238">그런 다음 SSH 사용자 자격 증명을 사용하여 RStudio에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![동시 사용자 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="6d543-240">현재 HDInsight 클러스터를 프로비전할 때 SSH 사용자 계정 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="6d543-241">따라서 여러 사용자가 HDInsight 클러스터의 Microsoft R Server에 액세스할 수 있게 하려면 Linux 시스템에 추가 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="6d543-242">RStudio Server Community가 클러스터의 에지 노드에서 실행되므로 여기서는 다음과 같은 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="6d543-243">만든 SSH 사용자를 사용하여 에지 노드에 로그인</span><span class="sxs-lookup"><span data-stu-id="6d543-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="6d543-244">에지 노드에 더 많은 Linux 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="6d543-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="6d543-245">만든 사용자를 통해 RStudio Community 버전 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="6d543-246">1단계: 만든 SSH 사용자를 사용하여 에지 노드에 로그인</span><span class="sxs-lookup"><span data-stu-id="6d543-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="6d543-247">SSH 도구(예: Putty)를 다운로드하고 기존 SSH 사용자를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="6d543-248">그런 다음 [SSH를 사용하여 HDInsight(Hadoop)에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)에서 제공된 지침에 따라 에지 노드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="6d543-249">HDInsight 클러스터의 R Server에 대한 에지 노드 주소는 *clustername-ed-ssh.azurehdinsight.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="6d543-250">2단계: 에지 노드에 더 많은 Linux 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="6d543-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="6d543-251">에지 노드에 사용자를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="6d543-252">반환되는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-252">You should see the following items returned:</span></span> 

![동시 사용자 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="6d543-254">"현재 Kerberos 암호:"를 묻는 메시지가 표시될 때 **Enter** 키를 누르기만 하면 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="6d543-255">`useradd` 명령의 `-m` 옵션은 시스템에서 사용자의 홈 폴더를 만듦을 나타내며, 이 폴더는 RStudio Community 버전에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="6d543-256">3단계: 만든 사용자를 통해 RStudio Community 버전 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="6d543-257">만든 사용자를 사용하여 RStudio에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-257">Use the user created to log in to RStudio:</span></span>

![동시 사용자 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="6d543-259">RStudio에서 새 사용자(예: 여기서는 *sshuser6*)를 사용하여 클러스터에 로그인함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![동시 사용자 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="6d543-261">또한 다른 브라우저 창에서 원래 자격 증명(기본적으로 *sshuser*)을 사용하여 동시에 로그인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="6d543-262">scaleR 함수를 사용하여 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="6d543-263">다음은 작업을 실행하는 데 사용되는 명령의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
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

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="6d543-264">제출된 작업은 YARN UI에서 다른 사용자 이름 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![동시 사용자 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="6d543-266">새로 추가된 사용자는 Linux 시스템에서 루트 권한을 가지고 있지 않지만 원격 HDFS 및 WASB 저장소의 모든 파일에 동일한 액세스 권한을 가지고 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="6d543-267">R 콘솔 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-267">Use the R console</span></span>

1. <span data-ttu-id="6d543-268">SSH 세션에서 다음 명령을 사용하여 R 콘솔을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="6d543-269">다음과 비슷한 결과가 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="6d543-270">R 버전 3.2.2(2015-08-14) -- "실행 안전" Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu(64비트)</span><span class="sxs-lookup"><span data-stu-id="6d543-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="6d543-271">R은 평가판 소프트웨어이며 절대로 어떠한 보증도 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="6d543-272">특정 조건에서 재배포는 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="6d543-273">배포에 대한 자세한 내용을 보려면 'license()' 또는 'licence()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="6d543-274">자연어가 지원되지만 영어 로캘로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="6d543-275">R은 많은 참가자가 함께한 공동 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="6d543-276">자세한 내용을 보려면 'contributors()'를 입력하고 게시물에 R 또는 R 패키지를 명시하는 방법을 보려면 'citation()'을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="6d543-277">몇 가지 데모를 보려면 'demo()'를, 온라인 도움말은 'help()'를, HTML 브라우저 인터페이스를 보려면 'help.start()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="6d543-278">R을 끝내려면 'q()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="6d543-279">Microsoft R Server 버전 8.0: R Microsoft 패키지의 향상된 배포 Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="6d543-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="6d543-280">릴리스 정보를 보려면 'readme()'를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="6d543-281">`>` 프롬프트에서 R 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="6d543-282">R 서버에는 Hadoop과 쉽게 상호 작용하고 분산된 계산을 실행할 수 있는 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="6d543-283">예를 들어, 다음 명령을 사용하여 HDInsight 클러스터에 대한 기본 파일 시스템의 루트를 볼 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="6d543-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="6d543-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="6d543-285">WASB 스타일 주소 지정을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="6d543-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="6d543-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="6d543-287">Microsoft R Server 또는 Microsoft R 클라이언트의 원격 인스턴스에서 HDI의 R Server 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="6d543-288">데스크톱 또는 랩톱에서 실행되는 Microsoft R Server 또는 Microsoft R Client의 원격 인스턴스에서 HDI Hadoop Spark 계산 컨텍스트에 대한 액세스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="6d543-289">[Spark에 대한 Compute 컨텍스트 만들기](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)에서 **Hadoop 클라이언트로 Microsoft R Server 사용** 하위 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="6d543-290">이렇게 하려면 랩톱 컴퓨터에서 RxSpark 계산 컨텍스트를 정의할 때 hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches 및 sshProfileScript와 같은 옵션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="6d543-291">예:</span><span class="sxs-lookup"><span data-stu-id="6d543-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="6d543-292">계산 컨텍스트 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-292">Use a compute context</span></span>

<span data-ttu-id="6d543-293">계산 컨텍스트를 사용하여 계산을 이제 노드에서 로컬로 수행할지 여부 또는 HDInsight 클러스터의 노드 간에 분산할지 여부를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="6d543-294">RStudio Server 또는 R 콘솔(SSH 세션)에서 다음 코드를 사용하여 HDInsight의 기본 저장소에 예제 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
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

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="6d543-295">그런 다음 데이터로 작업할 수 있도록 몇 가지 데이터 정보를 만들고 두 개의 데이터 원본을 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="6d543-296">로컬 계산 컨텍스트를 사용하여 데이터에 대해 로지스틱 회귀를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="6d543-297">다음과 유사한 줄로 끝나는 출력이 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-297">You should see output that ends with lines similar to the following:</span></span>

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

4. <span data-ttu-id="6d543-298">이번에는 Spark 컨텍스트를 사용하여 동일한 로지스틱 회귀를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="6d543-299">Spark 컨텍스트는 HDInsight 클러스터의 모든 작업자 노드에서 처리를 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="6d543-300">MapReduce를 사용하여 클러스터 노드 간에 계산을 분산시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="6d543-301">계산 컨텍스트에 대한 자세한 내용은 [HDInsight에서 R Server의 Compute 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="6d543-302">여러 노드에 R 코드 분산</span><span class="sxs-lookup"><span data-stu-id="6d543-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="6d543-303">R Server를 사용하면 손쉽게 기존 R 코드를 가져와 `rxExec`를 통해 클러스터의 여러 노드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="6d543-304">이 함수는 매개 변수 비우기 또는 시뮬레이션을 수행할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="6d543-305">다음 코드는 `rxExec`를 사용하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="6d543-306">Spark 또는 MapReduce 컨텍스트를 계속 사용하는 경우 이 명령에서는 `(Sys.info()["nodename"])` 코드가 실행되는 작업자 노드의 nodename(노드 이름) 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="6d543-307">예를 들어 4개 노드 클러스터에서는 다음과 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="6d543-308">Hive 및 Parquet의 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="6d543-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="6d543-309">R Server 9.1에서 제공되는 새로운 기능을 사용하면 Spark 계산 컨텍스트의 ScaleR 함수에서 Hive 및 Parquet의 데이터에 직접 액세스하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="6d543-310">이러한 기능은 RxHiveData 및 RxParquetData라는 새로운 ScaleR 데이터 소스 함수를 통해 사용할 수 있습니다. 이 함수는 Spark SQL을 사용하여 Spark DataFrame에 데이터를 직접 로드하여 ScaleR을 통해 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="6d543-311">다음 코드는 새 함수를 사용하는 샘플 코드 일부를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-311">The following code provides some sample code on use of the new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="6d543-312">이러한 새 기능의 사용에 대한 자세한 내용은 `?RxHivedata` 및 `?RxParquetData` 명령을 사용하여 R Server의 온라인 도움말을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="6d543-313">에지 노드에 추가 R 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="6d543-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="6d543-314">SSH를 통해 에지 노드에 연결한 경우 에지 노드에 추가 R 패키지를 설치하려면 R 콘솔 내에서 직접 `install.packages()`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="6d543-315">그러나 클러스터의 작업자 노드에 R 패키지를 설치해야 하는 경우에는 스크립트 작업을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="6d543-316">스크립트 동작은 HDInsight 클러스터의 구성을 변경하거나 추가 소프트웨어(예: 추가 R 패키지)를 설치하는 데 사용되는 Bash 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="6d543-317">스크립트 동작을 사용하여 추가 패키지를 설치하려면 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d543-318">추가 R 패키지를 설치하는 데 스크립트 작업을 사용하려는 경우 클러스터가 만들어진 후에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="6d543-319">클러스터를 만드는 동안 이 프로시저를 사용하지 마세요. 스크립트는 완전히 설치되고 구성된 R Server에 의존하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="6d543-320">[Azure Portal](https://portal.azure.com)에서 HDInsight 클러스터의 R Server를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="6d543-321">**설정** 블레이드에서 **스크립트 동작**을 선택한 후 **새로운 항목 제출**을 선택하여 새 스크립트 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![스크립트 작업 블레이드의 이미지](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="6d543-323">**스크립트 동작 제출** 블레이드에서 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="6d543-324">**이름**: 이 스크립트를 식별하는 친숙한 이름</span><span class="sxs-lookup"><span data-stu-id="6d543-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="6d543-325">**Bash 스크립트 URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="6d543-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="6d543-326">**헤드**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="6d543-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="6d543-327">**작업자**: **선택**이어야 함</span><span class="sxs-lookup"><span data-stu-id="6d543-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="6d543-328">**에지 노드**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="6d543-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="6d543-329">**Zookeeper**: **선택 취소**여야 함</span><span class="sxs-lookup"><span data-stu-id="6d543-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="6d543-330">**매개 변수**: 설치할 R 패키지</span><span class="sxs-lookup"><span data-stu-id="6d543-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="6d543-331">예: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="6d543-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="6d543-332">**이 스크립트 유지...**: **선택**이어야 함</span><span class="sxs-lookup"><span data-stu-id="6d543-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="6d543-333">기본적으로 모든 R 패키지는 설치된 R Server의 버전과 일치하는 Microsoft MRAN 리포지토리의 스냅숏에서 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="6d543-334">최신 버전의 패키지를 설치하려는 경우 호환성 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="6d543-335">그러나 이 설치 유형은 패키지 목록의 첫 번째 요소로 `useCRAN`을 지정함으로써 가능합니다(예: `useCRAN bitops, stringr, arules`).</span><span class="sxs-lookup"><span data-stu-id="6d543-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="6d543-336">일부 R 패키지에는 추가 Linux 시스템 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="6d543-337">편의상 가장 인기 있는 상위 100개 R 패키지에서 필요한 종속성을 미리 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="6d543-338">그러나 설치한 R 패키지에 더 많은 라이브러리가 필요한 경우 여기에 사용되는 기본 스크립트를 다운로드하고 시스템 라이브러리를 설치하는 단계를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="6d543-339">그런 다음 수정된 스크립트를 Azure 저장소의 공용 blob 컨테이너에 업로드하고 수정된 스크립트를 사용하여 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="6d543-340">스크립트 작업 개발에 대한 자세한 내용은 [스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![스크립트 작업 추가](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="6d543-342">**만들기**를 선택하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-342">Select **Create** to run the script.</span></span> <span data-ttu-id="6d543-343">스크립트가 완료되면 모든 작업자 노드에서 R 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="6d543-344">Microsoft R Server 조작화 사용</span><span class="sxs-lookup"><span data-stu-id="6d543-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="6d543-345">데이터 모델링이 완료되면 모델 조작화를 수행하여 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="6d543-346">Microsoft R Server 조작화를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="6d543-347">먼저 ssh를 에지 노드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="6d543-348">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6d543-349">SSH를 사용한 후 관련 버전의 디렉터리를 변경하고 sudo를 통해 dotnet dll을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="6d543-350">Microsoft R Server 9.1의 경우:</span><span class="sxs-lookup"><span data-stu-id="6d543-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="6d543-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="6d543-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="6d543-352">Microsoft R Server 9.0의 경우:</span><span class="sxs-lookup"><span data-stu-id="6d543-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="6d543-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="6d543-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="6d543-354">One-box 구성으로 Microsoft R Server 조작화를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="6d543-355">[R Server 조작화 구성]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="6d543-356">“A.</span><span class="sxs-lookup"><span data-stu-id="6d543-356">Select “A.</span></span> <span data-ttu-id="6d543-357">One-box(웹 + 계산 노드)”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="6d543-358">**admin**(관리자) 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-358">Enter a password for the **admin** user</span></span>

![one-box 조작화](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="6d543-360">선택적 단계로 다음과 같이 진단 테스트를 실행하여 진단 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="6d543-361">“6.</span><span class="sxs-lookup"><span data-stu-id="6d543-361">Select “6.</span></span> <span data-ttu-id="6d543-362">진단 테스트 실행”을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="6d543-363">“A.</span><span class="sxs-lookup"><span data-stu-id="6d543-363">Select “A.</span></span> <span data-ttu-id="6d543-364">구성 테스트”를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-364">Test configuration”</span></span>
3. <span data-ttu-id="6d543-365">이전 구성 단계에서 사용자 이름("admin")과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="6d543-366">Confirm Overall Health(전체 상태 확인)이 pass(합격)인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="6d543-367">관리 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="6d543-368">SSH를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-368">Exit SSH</span></span>

![조작화에 대한 진단](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="6d543-370">**Spark에 웹 서비스를 이용할 때 긴 지연**</span><span class="sxs-lookup"><span data-stu-id="6d543-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="6d543-371">Spark 계산 컨텍스트에서 mrsdeploy 함수로 만든 웹 서비스를 이용하려고 할 때 긴 지연이 발생하는 경우 일부 누락된 폴더를 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="6d543-372">Spark 응용 프로그램은 mrsdeploy 함수를 사용하여 웹 서비스에서 호출될 때마다 '*rserve2*'라는 사용자에게 속합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="6d543-373">이 문제를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="6d543-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="6d543-374">이 단계에서 조작화 구성이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="6d543-375">이제 RClient의 'mrsdeploy' 패키지를 사용하여 에지 노드의 조작화에 연결하고 [원격 실행](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) 및 [웹 서비스](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)와 같은 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="6d543-376">클러스터가 가상 네트워크에 설정되어 있는지 여부에 따라 SSH 로그인을 통해 포트 전달 터널링을 설정할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="6d543-377">다음 섹션에서는 이 터널을 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="6d543-378">가상 네트워크의 RServer 클러스터</span><span class="sxs-lookup"><span data-stu-id="6d543-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="6d543-379">12800 포트를 통해 에지 노드로 트래픽을 허용하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="6d543-380">이렇게 하면 에지 노드를 사용하여 조작화 기능에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="6d543-381">`remoteLogin()`이 에지 노드에 연결할 수 없지만 에지 노드로 SSH를 실행할 수 있는 경우 12800 포트에서 트래픽을 허용하는 규칙이 올바르게 설정되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="6d543-382">문제가 계속되면 SSH를 통해 포트 전달 터널링을 설정하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="6d543-383">지침은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="6d543-384">가상 네트워크에 설정되지 않은 RServer 클러스터</span><span class="sxs-lookup"><span data-stu-id="6d543-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="6d543-385">클러스터가 VNet에 설정되지 않았거나 VNet을 통한 연결에 문제가 있는 경우 SSH 포트 전달 터널링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="6d543-386">Putty에서도 이 터널링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-386">On Putty, you can set it up as well.</span></span>

![Putty ssh 연결](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="6d543-388">SSH 세션이 활성화되면 컴퓨터의 12800 포트에서 발생한 트래픽이 SSH 세션을 통해 에지 노드의 12800 포트로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="6d543-389">`remoteLogin()` 메서드에서 `127.0.0.1:12800`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="6d543-390">이렇게 하면 포트 전달을 통해 에지 노드의 조작화에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="6d543-391">HDInsight 작업자 노드에서 Microsoft R Server 조작화 계산 노드를 확장하는 방법</span><span class="sxs-lookup"><span data-stu-id="6d543-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="6d543-392">작업자 노드 서비스 해제</span><span class="sxs-lookup"><span data-stu-id="6d543-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="6d543-393">Microsoft R Server는 현재 Yarn을 통해 관리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="6d543-394">작업자 노드 서비스를 해제하지 않으면 Yarn 리소스 관리자가 서버에서 사용하는 리소스를 인식하지 못하기 때문에 예상대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="6d543-395">이 상황을 피하려면 계산 노드의 크기를 조정하기 전에 작업자 노드의 서비스를 해제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="6d543-396">작업자 노드 서비스를 해제하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="6d543-397">HDI 클러스터의 Ambari 콘솔에 로그인하고 "Hosts" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="6d543-398">서비스를 해제할 작업자 노드를 선택하고 "동작"> "선택한 호스트"> "Hosts"를 차례로 클릭한 다음 "유지 관리 모드 켜기"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="6d543-399">예를 들어 다음 이미지에서는 wn3과 wn4를 선택하여 서비스를 해제했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![작업자 노드 서비스 해제](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="6d543-401">**작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **서비스 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="6d543-402">**작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **서비스 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="6d543-403">**작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="6d543-404">**작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="6d543-405">**작업** > **선택한 호스트** > **호스트**를 선택하고 > **모든 구성 요소 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="6d543-406">작업자 노드를 선택 취소하고 헤드 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="6d543-407">**작업** > **선택한 호스트** > "**호스트** > **모든 구성 요소 다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="6d543-408">서비스 해제된 작업자 노드 각각에 Compute 노드 구성</span><span class="sxs-lookup"><span data-stu-id="6d543-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="6d543-409">SSH를 서비스 해제된 각 작업자 노드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="6d543-410">`dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`을 사용하여 관리 유틸리티를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="6d543-411">"1"을 입력하여 [R Server 조작화 구성] 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="6d543-412">"c"를 입력하여 "C.</span><span class="sxs-lookup"><span data-stu-id="6d543-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="6d543-413">Compute 노드" 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-413">Compute node".</span></span> <span data-ttu-id="6d543-414">그러면 작업자 노드에 계산 노드가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="6d543-415">관리 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="6d543-416">웹 노드에 계산 노드 세부 정보 추가</span><span class="sxs-lookup"><span data-stu-id="6d543-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="6d543-417">서비스가 해제된 모든 작업자 노드에서 계산 노드를 실행하도록 구성한 후에 에지 노드로 돌아가서 Microsoft R Server 웹 노드의 구성에 서비스가 해제된 작업자 노드의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="6d543-418">SSH를 에지 노드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-418">SSH into the edge node.</span></span>
* <span data-ttu-id="6d543-419">`vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="6d543-420">"URI" 섹션을 살펴보고 작업자 노드의 IP 및 포트 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![작업자 노드 서비스 해제 명령줄](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="6d543-422">문제 해결</span><span class="sxs-lookup"><span data-stu-id="6d543-422">Troubleshoot</span></span>

<span data-ttu-id="6d543-423">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d543-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d543-424">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d543-424">Next steps</span></span>

<span data-ttu-id="6d543-425">이제 R Server와 SSH 세션에서 R 콘솔을 사용하는 기본 사항이 포함된 새 HDInsight 클러스터를 만드는 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="6d543-426">다음 항목에서는 HDInsight에 R Server를 관리하고 작업하는 다른 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d543-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="6d543-427">HDInsight에 RStudio Server 추가(클러스터 생성 동안 설치되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="6d543-427">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="6d543-428">HDInsight의 R 서버에 대한 Compute 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="6d543-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="6d543-429">HDInsight에서 R Server의 Azure Storage 옵션</span><span class="sxs-lookup"><span data-stu-id="6d543-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
