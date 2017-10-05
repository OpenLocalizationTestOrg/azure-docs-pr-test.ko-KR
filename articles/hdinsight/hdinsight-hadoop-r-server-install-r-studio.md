---
title: "HDInsight의 R Server를 사용하여 RStudio 설치 - Azure | Microsoft Docs"
description: "HDInsight에서 R Server를 사용하여 RStudio를 설치하는 방법입니다."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="be08c-103">HDInsight의 R Server를 사용하여 RStudio 설치</span><span class="sxs-lookup"><span data-stu-id="be08c-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="be08c-104">이 문서에서는 사용자 지정 스크립트를 사용하여 클러스터의 에지 노드에 [RStudio Server](https://www.rstudio.com/products/rstudio-server/)의 커뮤니티(무료) 버전을 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="be08c-105">RStudio Server는 원격 클라이언트에서 사용할 브라우저 기반 IDE를 제공하며 Linux에서 널리 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="be08c-106">오늘날 다음을 포함해 R에 사용 가능한 여러 IDE(통합된 개발 환경)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="be08c-107">Microsoft용 [Visual Studio용 R 도구](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)(RTVS)</span><span class="sxs-lookup"><span data-stu-id="be08c-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="be08c-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="be08c-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="be08c-109">Walware의 Eclipse 기반 [StatET](http://www.walware.de/goto/statet)</span><span class="sxs-lookup"><span data-stu-id="be08c-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="be08c-110">RStudio Server를 HDInsight 클러스터의 에지 노드에 설치하는 이점은 클러스터의 R Server를 사용하여 R 스크립트를 개발 및 실행할 수 있는 완벽한 IDE 환경이 제공한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="be08c-111">이 구성은 R 콘솔의 기본 용도보다 상당히 생산성이 높을 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="be08c-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="be08c-112">이 문서에서 설명하는 절차는 클러스터를 프로비전할 때 RStudio Server 커뮤니티 에디션을 설치하도록 선택하지 않은 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="be08c-113">프로비전 중에 추가한 경우 클러스터의 Azure Portal 항목에서 **R Server 대시보드** 타일을 클릭한 다음 **R Studio Server** 타일을 클릭하여 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="be08c-114">상업적으로 사용이 허가된 Pro 버전의 RStudio 서버를 사용하려면 [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/)에서 제공하는 설치 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="be08c-115">[R 스크립트 작업 설치](hdinsight-hadoop-r-scripts-linux.md)를 사용하여 R이 설치된 HDInsight 클러스터를 사용하는 경우 HDInsight 클러스터의 R Server가 필요하므로 이 단계의 단계가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="be08c-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="be08c-116">Prerequisites</span></span>

* <span data-ttu-id="be08c-117">R 서버가 설치된 Azure HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="be08c-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="be08c-118">자세한 내용은 [HDInsight 클러스터에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="be08c-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="be08c-119">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="be08c-119">An SSH client.</span></span> <span data-ttu-id="be08c-120">Linux 및 Unix 배포 또는 Macintosh OS X의 경우 `ssh` 명령은 운영 체제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="be08c-121">Windows의 경우 [OpenSSH 옵션](https://www.youtube.com/watch?v=CwYSvvGaiWU) 또는 [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)와 함께 [Cygwin](http://www.redhat.com/services/custom/cygwin/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="be08c-122">사용자 지정 스크립트를 사용하여 클러스터에 RStudio 설치</span><span class="sxs-lookup"><span data-stu-id="be08c-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="be08c-123">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-123">Here are the steps:</span></span>

1. <span data-ttu-id="be08c-124">클러스터의 에지 노드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="be08c-125">R 서버가 설치된 HDInsight 클러스터의 경우 헤드 노드와 에지 노드에 대한 명명 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="be08c-126">헤드 노드: `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="be08c-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="be08c-127">에지 노드: `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="be08c-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="be08c-128">1단계에 제공된 명명 패턴을 사용하여 클러스터의 에지 노드로 SSH를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="be08c-129">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="be08c-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="be08c-130">연결이 완료되면 클러스터의 루트 사용자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="be08c-131">SSH 세션에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="be08c-132">사용자 지정 스크립트를 다운로드하여 RStudio를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="be08c-133">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="be08c-134">사용자 지정 스크립트 파일에 대한 권한을 변경하고 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="be08c-135">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="be08c-136">R 서버가 설치된 HDInsight 클러스터를 만드는 동안 SSH 암호를 사용한 경우 이 단계를 건너뛰고 다음 단계로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="be08c-137">그렇지 않고 SSH 키를 사용하여 클러스터를 만든 경우 SSH 사용자에 대한 암호를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="be08c-138">RStudio에 연결할 때 이 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="be08c-139">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="be08c-140">**현재 Kerberos 암호**를 묻는 메시지가 표시되면 **Enter** 키를 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="be08c-141">`USERNAME` 을(를) HDInsight 클러스터에 대한 SSH 사용자로 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="be08c-142">암호가 성공적으로 설정된 경우 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="be08c-143">SSH 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="be08c-144">HDInsight 클러스터에서 `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` 을 클라이언트 컴퓨터에 매핑하여 클러스터에 대한 SSH 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="be08c-145">새 브라우저 세션을 열기 전에 SSH 터널을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="be08c-146">[Cygwin](http://www.redhat.com/services/custom/cygwin/)을 사용하는 Linux 클라이언트 또는 Windows 클라이언트에서 터미널 세션을 열고 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="be08c-147">**USERNAME**을 HDInsight 클러스터에 대한 SSH 사용자로 바꾸고 **CLUSTERNAME**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="be08c-148">`-i id_rsa_key`를 추가하여 암호가 이닌 SSH 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="be08c-149">PuTTY와 Windows 클라이언트를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="be08c-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="be08c-150">PuTTY를 열고 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="be08c-151">대화 상자의 왼쪽에 있는 **Category** 섹션에서 **Connection**, **SSH**를 차례로 확장한 다음 **Tunnels**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="be08c-152">**Options controlling SSH port forwarding** 양식에 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="be08c-153">**Source port** - 전달하려는 클라이언트의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="be08c-154">예를 들면 **8787**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-154">For example, **8787**.</span></span>
        * <span data-ttu-id="be08c-155">**Destination** - 로컬 클라이언트 컴퓨터에 매핑해야 하는 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="be08c-156">예를 들면 **localhost:8787**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="be08c-157">![SSH 터널 만들기](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH 터널 만들기")</span><span class="sxs-lookup"><span data-stu-id="be08c-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="be08c-158">**Add**를 클릭하여 설정을 추가한 다음 **Open**을 클릭하여 SSH 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="be08c-159">메시지가 표시되면 서버에 로그인하여 SSH 세션을 설정하고 터널을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="be08c-160">웹 브라우저를 열고 터널에 대해 입력한 포트에 따라 다음 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="be08c-161">클러스터에 연결할 SSH 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="be08c-162">클러스터를 만드는 동안 SSH 키를 사용한 경우 5단계에서 만든 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="be08c-163">![R 스튜디오에 연결](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "R 스튜디오에 연결")</span><span class="sxs-lookup"><span data-stu-id="be08c-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="be08c-164">RStudio 설치의 성공 여부를 테스트하려면 클러스터에서 R 기반 MapReduce 및 Spark 작업을 실행하는 테스트 스크립트를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="be08c-165">RStudio에서 실행할 테스트 스크립트를 다운로드하려면 SSH 콘솔로 돌아가 다음 명령을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="be08c-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="be08c-166">R이 설치된 Hadoop 클러스터를 만든 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="be08c-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="be08c-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="be08c-168">R이 설치된 Spark 클러스터를 만든 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="be08c-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="be08c-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="be08c-170">RStudio에 다운로드한 테스트 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="be08c-171">파일을 두 번 클릭하여 열고 파일의 내용을 선택한 다음 **Run**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="be08c-172">**Console** 창에 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="be08c-173">![설치 테스트](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "설치 테스트")</span><span class="sxs-lookup"><span data-stu-id="be08c-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="be08c-174">또 다른 옵션은 `source(testhdi.r)` 또는 `source(testhdi_spark.r)`을(를) 입력하여 스크립트를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be08c-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="be08c-175">참고 항목</span><span class="sxs-lookup"><span data-stu-id="be08c-175">See also</span></span>

* [<span data-ttu-id="be08c-176">HDInsight 클러스터의 R 서버에 대한 계산 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="be08c-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="be08c-177">HDInsight에서 R Server의 Azure Storage 옵션</span><span class="sxs-lookup"><span data-stu-id="be08c-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

