---
title: "Azure HDInsight aaaUse SSH 터널링 tooaccess | Microsoft Docs"
description: "Toouse SSH 터널 toosecurely Linux 기반 HDInsight 노드에 호스팅되는 웹 리소스를 탐색 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="6279c-103">SSH 터널링 tooaccess Ambari web UI, JobHistory, NameNode, Oozie, 및 기타 웹 Ui 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6279c-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="6279c-104">Hello 인터넷을 통해 액세스 tooAmbari 웹 UI를 제공 하는 Linux 기반 HDInsight 클러스터에 있지만 hello UI의 일부 기능은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="6279c-105">예를 들어 hello 웹 UI Ambari를 통해 표시 되는 다른 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="6279c-106">Hello Ambari web UI의 전체 기능에 대 한 SSH 터널 toohello 클러스터 헤드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="6279c-107">SSH 터널을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="6279c-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="6279c-108">SSH 터널을 통해 여러 hello 메뉴 Ambari에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="6279c-109">이러한 메뉴는 작업자 노드 등의 다른 노드 유형에서 실행되는 웹 사이트 및 서비스에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="6279c-110">종종 이러한 웹 사이트를 보호 하지 않는, 인터넷 hello에 안전 하 게 보호 toodirectly 노출 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="6279c-111">다음 웹 ui를 만들 hello SSH 터널이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="6279c-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="6279c-112">JobHistory</span></span>
* <span data-ttu-id="6279c-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="6279c-113">NameNode</span></span>
* <span data-ttu-id="6279c-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="6279c-114">Thread Stacks</span></span>
* <span data-ttu-id="6279c-115">Oozie web UI</span><span class="sxs-lookup"><span data-stu-id="6279c-115">Oozie web UI</span></span>
* <span data-ttu-id="6279c-116">HBase Master and Logs UI</span><span class="sxs-lookup"><span data-stu-id="6279c-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="6279c-117">스크립트 동작 toocustomize 클러스터를 사용 하면 모든 서비스 또는 웹 UI를 노출 하는 설치 하는 유틸리티 SSH 터널이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="6279c-118">예를 들어를 설치한 경우 색상 스크립트 작업을 사용 하 여 SSH 터널 tooaccess hello 색상 웹 UI를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6279c-119">가상 네트워크를 통해 직접 액세스 tooHDInsight를 설정한 경우에 toouse SSH 터널을 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="6279c-120">가상 네트워크를 통해 HDInsight에 직접 액세스의 예로, 참조 hello [HDInsight 연결 tooyour 온-프레미스 네트워크](connect-on-premises-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6279c-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="6279c-121">SSH 터널이란</span><span class="sxs-lookup"><span data-stu-id="6279c-121">What is an SSH tunnel</span></span>

<span data-ttu-id="6279c-122">[SSH 터널링 secure](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) tooa 포트 로컬 워크스테이션에서 전송 된 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="6279c-123">hello 트래픽은 SSH 연결 tooyour HDInsight 클러스터 헤드 노드를 통해 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="6279c-124">hello 요청 hello 헤드 노드에서 발생 하는 경우 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="6279c-125">hello 응답 hello 터널 tooyour 워크스테이션을 통해 다시 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6279c-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6279c-126">Prerequisites</span></span>

* <span data-ttu-id="6279c-127">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="6279c-127">An SSH client.</span></span> <span data-ttu-id="6279c-128">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6279c-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="6279c-129">일 수 있는 웹 브라우저 toouse SOCKS5 프록시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6279c-130">Windows에서 기본 제공 하는 hello SOCKS 프록시 지원 SOCKS5, 지원 하지 않습니다 및 hello이이 문서의 단계에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="6279c-131">hello 다음 브라우저 Windows 프록시 설정에 의존 하 고 하지 않을 현재이 문서의 단계 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="6279c-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="6279c-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="6279c-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="6279c-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6279c-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="6279c-134">Google Chrome hello Windows 프록시 설정에도 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="6279c-135">그러나 SOCKS5를 지원하는 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="6279c-136">[FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="6279c-137"><a name="usessh"></a>SSH 명령 hello를 사용 하 여 터널을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="6279c-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="6279c-138">사용 하 여 hello 다음 명령은 toocreate hello를 사용 하 여 SSH 터널이 `ssh` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="6279c-139">대체 **USERNAME** HDInsight 클러스터와 바꾸기에 대 한 SSH 사용자 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="6279c-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="6279c-140">이 명령은 SSH를 통해 트래픽을 toolocal 포트 9876 toohello 클러스터 라우팅하는 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="6279c-141">hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-141">hello options are:</span></span>

* <span data-ttu-id="6279c-142">**D 9876** -hello hello 터널을 통해 트래픽을 라우팅하는 로컬 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="6279c-143">**C** - 웹 트래픽은 대부분 텍스트이므로 모든 데이터 압축</span><span class="sxs-lookup"><span data-stu-id="6279c-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="6279c-144">**2** -force SSH tootry 프로토콜 버전 2만 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="6279c-145">**q** - 자동 모드</span><span class="sxs-lookup"><span data-stu-id="6279c-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="6279c-146">**T** - 포트 전달 후 허위 tty 할당 비활성화</span><span class="sxs-lookup"><span data-stu-id="6279c-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6279c-147">**n** - 포트 전달 후 STDIN 읽지 않음</span><span class="sxs-lookup"><span data-stu-id="6279c-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6279c-148">**N** - 포트 전달 후 원격 명령 실행 안 함</span><span class="sxs-lookup"><span data-stu-id="6279c-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6279c-149">**f** -hello 백그라운드에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="6279c-150">Hello 명령이 완료 된 후 hello 로컬 컴퓨터에서 보낸 트래픽은 tooport 9876 라우트된 toohello 클러스터 헤드 노드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="6279c-151"><a name="useputty"></a>PuTTY를 사용하여 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="6279c-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="6279c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty)는 Windows용 그래픽 SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="6279c-153">다음 단계 toocreate PuTTY를 사용 하 여 SSH 터널이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="6279c-154">PuTTY를 열고 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="6279c-155">PuTTY를 잘 모르는 경우 참조 hello [설명서 (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html) PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="6279c-156">Hello에 **범주** 섹션 toohello hello 대화의 왼쪽, 확장 **연결**를 확장 하 고 **SSH**를 선택한 후 **터널**합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="6279c-157">Hello hello에 다음 정보를 제공 **SSH에 대 한 옵션 포트 전달** 형식:</span><span class="sxs-lookup"><span data-stu-id="6279c-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="6279c-158">**원본 포트** -hello tooforward 한다고 hello 클라이언트에는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="6279c-159">예를 들면 **9876**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-159">For example, **9876**.</span></span>

   * <span data-ttu-id="6279c-160">**대상** -hello hello Linux 기반 HDInsight 클러스터에 대 한 SSH 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6279c-161">예를 들면 **mycluster-ssh.azurehdinsight.net**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="6279c-162">**Dynamic** - 동적 SOCKS 프록시 라우팅을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![터널링 옵션 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="6279c-164">클릭 **추가** tooadd hello 설정 하 고 클릭 **열려** tooopen SSH 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="6279c-165">대화 상자가 나타나면 toohello 서버에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="6279c-166">브라우저에서 사용 하 여 hello 터널</span><span class="sxs-lookup"><span data-stu-id="6279c-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6279c-167">hello이 섹션 사용 하 여 hello Mozilla FireFox 브라우저에에서 단계를 모든 플랫폼에서 hello를 동일한 프록시 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="6279c-168">Google Chrome 등 다른 최신 브라우저 FoxyProxy toowork hello 터널와 같은 확장을 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="6279c-169">Hello 브라우저 toouse 구성 **localhost** 및 때 사용 하는 hello 포트도 hello 터널 만들기는 **SOCKS v5** 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="6279c-170">Hello Firefox 설정의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="6279c-171">9876 보다 다른 포트를 사용 하는 경우 사용 하는 hello 포트 toohello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![Firefox 설정 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="6279c-173">선택 하면 **원격 DNS** hello HDInsight 클러스터를 사용 하 여 DNS 도메인 이름 () 요청을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="6279c-174">이 설정은 hello hello 클러스터의 헤드 노드를 사용 하 여 DNS를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="6279c-175">와 같은 사이트를 방문 하 여 hello 터널 작동 확인 [http://www.whatismyip.com/](http://www.whatismyip.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="6279c-176">hello IP 하나를 사용할지 hello Microsoft Azure 데이터 센터에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="6279c-177">Ambari 웹 UI 통해 확인</span><span class="sxs-lookup"><span data-stu-id="6279c-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="6279c-178">Hello 클러스터, 설정 되 면 다음 단계 tooverify hello Ambari Web에서에서 웹 서비스 Ui를 액세스할 수 있도록 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="6279c-179">브라우저에서 toohttp://headnodehost:8080을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="6279c-180">hello `headnodehost` 주소 hello 터널 toohello 클러스터 통해 전송 되 고 toohello 헤드 노드에 Ambari에서 실행 되는 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="6279c-181">메시지가 표시 되 면 클러스터에 대 한 hello 관리자 사용자 이름 (admin) 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="6279c-182">메시지가 표시 되는 두 번째로 hello Ambari web UI 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="6279c-183">이 경우 hello 정보를 다시 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6279c-184">Hello http://headnodehost:8080 주소 tooconnect toohello 클러스터를 사용할 때는 hello 터널을 통해 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="6279c-185">통신은 HTTPS가 아닌 hello SSH 터널을 사용 하 여 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="6279c-186">HTTPS를 사용 하 여 인터넷 hello, https://CLUSTERNAME.azurehdinsight.net를 사용 하 여 넘는 tooconnect 여기서 **CLUSTERNAME** hello hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="6279c-187">Hello Ambari 웹 UI에서에서 HDFS hello hello 페이지의 hello 왼쪽 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![HDFS가 선택된 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="6279c-189">Hello HDFS 서비스 정보 표시 되 면 선택 **빠른 링크**합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="6279c-190">Hello 클러스터 헤드 노드 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="6279c-191">Hello 헤드 노드 중 하나를 선택한 다음 선택 **NameNode UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Hello 빠른 링크 메뉴를 사용 하 여 이미지 확장](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="6279c-193">__빠른 링크__를 선택하면 대기 표시기가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="6279c-194">인터넷 연결 속도가 느린 경우 이러한 상태가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="6279c-195">에 대 한 hello 서버에서 받은 hello 데이터 toobe 2 분 정도 기다린 후 hello 목록을 다시 시도.</span><span class="sxs-lookup"><span data-stu-id="6279c-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="6279c-196">일부 항목에 hello **빠른 링크** 메뉴 hello 화면 오른쪽 hello 여 잘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="6279c-197">이 경우 마우스를 사용 하 여 hello 메뉴를 확장 하 고 hello 오른쪽 화살표 키 tooscroll hello 화면 toohello 오른쪽 toosee hello 나머지 hello 메뉴를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="6279c-198">다음 이미지는 페이지와 유사한 toohello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-198">A page similar toohello following image is displayed:</span></span>

    ![Hello NameNode UI의 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="6279c-200">이 페이지에 대 한 hello URL 확인 비슷해야 너무**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="6279c-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="6279c-201">이 URI hello 정규화 된 도메인의 내부 이름 (FQDN) hello 노드를 사용 하 고만 액세스할 수는 SSH 터널을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6279c-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6279c-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6279c-202">Next steps</span></span>

<span data-ttu-id="6279c-203">Toocreate 및 SSH 터널을 사용 하 여 참조 문서를 다른 방법으로 toouse Ambari 다음 hello 배웠습니다 했으므로:</span><span class="sxs-lookup"><span data-stu-id="6279c-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="6279c-204">Ambari를 사용하여 HDInsight 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="6279c-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="6279c-205">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6279c-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

