---
title: "Azure HDInsight에 R server RStudio aaaInstall | Microsoft Docs"
description: "어떻게 tooinstall HDInsight에 R server RStudio 합니다."
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="c2d97-103">HDInsight의 R Server를 사용하여 RStudio 설치</span><span class="sxs-lookup"><span data-stu-id="c2d97-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="c2d97-104">이 문서에서는 tooinstall 커뮤니티 (무료) 버전의 hello 하는 방법을 설명 [RStudio 서버](https://www.rstudio.com/products/rstudio-server/) hello 가장자리 노드는 사용자 지정 스크립트를 사용 하는 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="c2d97-105">RStudio Server는 원격 클라이언트에서 사용할 브라우저 기반 IDE를 제공하며 Linux에서 널리 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="c2d97-106">오늘날 다음을 포함해 R에 사용 가능한 여러 IDE(통합된 개발 환경)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="c2d97-107">Microsoft용 [Visual Studio용 R 도구](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)(RTVS)</span><span class="sxs-lookup"><span data-stu-id="c2d97-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="c2d97-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="c2d97-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="c2d97-109">Walware의 Eclipse 기반 [StatET](http://www.walware.de/goto/statet)</span><span class="sxs-lookup"><span data-stu-id="c2d97-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="c2d97-110">HDInsight 클러스터의 hello 가장자리 노드에서 RStudio 서버를 설치할 hello 장점은 제공 하는 전체 IDE 환경을 hello 개발 및 R 스크립트의 실행에 대 한 R server hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="c2d97-111">이 구성은 hello R 콘솔의 기본 사용 보다 훨씬 더 생산적 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="c2d97-112">이 문서에서 설명 하는 hello 절차는 클러스터를 프로 비전 할 때 tooinstall RStudio 서버 community 버전을 선택 하지 않은 경우 해당만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="c2d97-113">프로 비전에서 추가한 경우 hello에서 클릭 것 tooaccess 다음 **R Server 대시보드** hello 클러스터에 대 한 다음 hello에서 Azure 포털 항목에서에서 타일 **R Studio 서버** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="c2d97-114">Hello 설치 지침을 따라야 RStudio 서버의 toouse 상업적으로 사용이 허가 된 hello Pro 버전을 원하는 경우 [RStudio 서버](https://www.rstudio.com/products/rstudio/download-server/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="c2d97-115">R가 설치 hello를 사용 하 여 HDInsight 클러스터를 사용 하는 경우 [설치 R 스크립트 작업](hdinsight-hadoop-r-scripts-linux.md),이 문서의 단계 hello 작동 하지 것입니다는 R 서버 hello HDInsight 클러스터에 필요한 대로 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="c2d97-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c2d97-116">Prerequisites</span></span>

* <span data-ttu-id="c2d97-117">R 서버가 설치된 Azure HDInsight 클러스터.</span><span class="sxs-lookup"><span data-stu-id="c2d97-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="c2d97-118">자세한 내용은 [HDInsight 클러스터에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2d97-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="c2d97-119">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="c2d97-119">An SSH client.</span></span> <span data-ttu-id="c2d97-120">Macintosh OS X, Linux 및 Unix 배포에 대 한 hello `ssh` 명령은 hello 운영 체제와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="c2d97-121">Windows의 경우 권장 [Cygwin](http://www.redhat.com/services/custom/cygwin/) hello로 [OpenSSH 옵션](https://www.youtube.com/watch?v=CwYSvvGaiWU), 또는 [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="c2d97-122">사용자 지정 스크립트를 사용 하 여 hello 클러스터에 RStudio를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="c2d97-123">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-123">Here are hello steps:</span></span>

1. <span data-ttu-id="c2d97-124">Hello 클러스터의 hello 가장자리 노드를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="c2d97-125">R server는 HDInsight 클러스터에 대 한 다음은 헤드 노드 및 가장자리 노드 hello 명명 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="c2d97-126">헤드 노드: `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="c2d97-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="c2d97-127">에지 노드: `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="c2d97-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="c2d97-128">1 단계에서 제공 하는 hello 명명 패턴을 사용 하 여 hello 클러스터의 hello 가장자리 노드로 SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="c2d97-129">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2d97-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c2d97-130">연결 되 면 hello 클러스터 상의 루트 사용자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="c2d97-131">Hello SSH 세션에서 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="c2d97-132">사용자 지정 스크립트 tooinstall hello RStudio를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="c2d97-133">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="c2d97-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="c2d97-134">Hello 사용자 지정 스크립트 파일에 대 한 hello 권한을 변경 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="c2d97-135">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="c2d97-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="c2d97-136">R server는 HDInsight 클러스터를 만드는 동안 SSH 암호를 사용 하는 경우이 단계를 건너뛰고 toohello 다음 계속 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="c2d97-137">SSH 키 대신 toocreate hello 클러스터를 사용한 경우 SSH 사용자에 대 한 암호를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="c2d97-138">TooRStudio 연결할 때이 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="c2d97-139">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="c2d97-140">**현재 Kerberos 암호**를 묻는 메시지가 표시되면 **Enter** 키를 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="c2d97-141">`USERNAME` 을(를) HDInsight 클러스터에 대한 SSH 사용자로 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="c2d97-142">암호를 성공적으로 설정 hello 메시지의 뒤에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="c2d97-143">Hello SSH 세션을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="c2d97-144">매핑 SSH 터널 toohello 클러스터를 만드는 `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello HDInsight 클러스터에서 toohello 클라이언트 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="c2d97-145">새 브라우저 세션을 열기 전에 SSH 터널을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="c2d97-146">Linux 클라이언트 또는 사용 하 여 Windows 클라이언트에서 [Cygwin](http://www.redhat.com/services/custom/cygwin/)터미널 세션을 열고 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c2d97-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="c2d97-147">대체 **USERNAME** HDInsight 클러스터와 바꾸기에 대 한 SSH 사용자 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="c2d97-148">`-i id_rsa_key`를 추가하여 암호가 이닌 SSH 키를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="c2d97-149">PuTTY와 Windows 클라이언트를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="c2d97-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="c2d97-150">PuTTY를 열고 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="c2d97-151">Hello에 **범주** 섹션 toohello hello 대화의 왼쪽, 확장 **연결**를 확장 하 고 **SSH**를 선택한 후 **터널**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="c2d97-152">Hello hello에 다음 정보를 제공 **SSH에 대 한 옵션 포트 전달** 형식:</span><span class="sxs-lookup"><span data-stu-id="c2d97-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="c2d97-153">**원본 포트** -hello tooforward 한다고 hello 클라이언트에는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="c2d97-154">예를 들면 **8787**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-154">For example, **8787**.</span></span>
        * <span data-ttu-id="c2d97-155">**대상** -hello 해야 하는 대상 매핑된 toohello 로컬 클라이언트 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="c2d97-156">예를 들면 **localhost:8787**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="c2d97-157">![SSH 터널 만들기](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH 터널 만들기")</span><span class="sxs-lookup"><span data-stu-id="c2d97-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="c2d97-158">클릭 **추가** tooadd hello 설정 하 고 클릭 **열려** tooopen SSH 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="c2d97-159">대화 상자가 나타나면 toohello 서버 tooestablish SSH 세션을 사용 하도록 설정한 hello 터널이 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="c2d97-160">웹 브라우저를 열고 hello hello 포트 hello 터널에 대 한 입력에 따라 url을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="c2d97-161">입력 정보 요청된 tooenter hello SSH 사용자 이름 및 암호 tooconnect toohello 클러스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="c2d97-162">SSH 키를 사용 하는 hello 클러스터를 만드는 동안 경우 5 단계에서 만든 hello 암호를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="c2d97-163">![Studio tooR 연결](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "SSH 터널을 만들어")</span><span class="sxs-lookup"><span data-stu-id="c2d97-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="c2d97-164">tootest hello RStudio 설치 성공 여부, hello 클러스터에서 R 기반 Spark 및 MapReduce 작업을 실행 하는 테스트 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="c2d97-165">RStudio, toodownload hello 테스트 스크립트 toorun toohello SSH 콘솔 돌아가서 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="c2d97-166">R이 설치된 Hadoop 클러스터를 만든 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="c2d97-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="c2d97-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="c2d97-168">R이 설치된 Spark 클러스터를 만든 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="c2d97-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="c2d97-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="c2d97-170">RStudio, 다운로드 한 스크립트를 테스트 하는 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="c2d97-171">Hello 파일 tooopen hello 파일의 hello 내용을 선택 하 고 클릭 한 다음를 두 번 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="c2d97-172">Hello에 hello 출력이 **콘솔** 창:</span><span class="sxs-lookup"><span data-stu-id="c2d97-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="c2d97-173">![Hello 설치 테스트](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "hello 설치 테스트")</span><span class="sxs-lookup"><span data-stu-id="c2d97-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="c2d97-174">또 다른 옵션 tootype 것 `source(testhdi.r)` 또는 `source(testhdi_spark.r)` tooexecute hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d97-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2d97-175">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c2d97-175">See also</span></span>

* [<span data-ttu-id="c2d97-176">HDInsight 클러스터의 R 서버에 대한 계산 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="c2d97-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="c2d97-177">HDInsight에서 R Server의 Azure Storage 옵션</span><span class="sxs-lookup"><span data-stu-id="c2d97-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

