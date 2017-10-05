---
title: "SSH 터널링을 사용하여 Azure HDInsight에 액세스 | Microsoft Docs"
description: "SSH 터널을 사용하여 Linux 기반 HDInsight 노드에 호스팅되는 웹 리소스를 안전하게 검색하는 방법에 알아봅니다."
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="f5d7e-103">SSH 터널링을 사용하여 Ambari 웹 UI, JobHistory, NameNode, Oozie 및 기타 웹 UI에 액세스</span><span class="sxs-lookup"><span data-stu-id="f5d7e-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="f5d7e-104">Linux 기반 HDInsight 클러스터는 인터넷을 통해 Ambari 웹 UI에 대한 액세스를 제공하지만 일부 UI의 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="f5d7e-105">예를 들면 Ambari를 통해 노출되는 다른 서비스에 대한 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="f5d7e-106">Ambari 웹 UI의 모든 기능의 경우 SSH 터널을 클러스터 헤드에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="f5d7e-107">SSH 터널을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="f5d7e-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="f5d7e-108">Ambari의 일부 메뉴만 SSH 터널을 통해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="f5d7e-109">이러한 메뉴는 작업자 노드 등의 다른 노드 유형에서 실행되는 웹 사이트 및 서비스에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="f5d7e-110">종종 이러한 웹사이트는 보안이 유지되지 않으므로 인터넷에 직접 노출하는 것은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="f5d7e-111">다음 웹 UI에는 SSH 터널이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="f5d7e-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="f5d7e-112">JobHistory</span></span>
* <span data-ttu-id="f5d7e-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="f5d7e-113">NameNode</span></span>
* <span data-ttu-id="f5d7e-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="f5d7e-114">Thread Stacks</span></span>
* <span data-ttu-id="f5d7e-115">Oozie web UI</span><span class="sxs-lookup"><span data-stu-id="f5d7e-115">Oozie web UI</span></span>
* <span data-ttu-id="f5d7e-116">HBase Master and Logs UI</span><span class="sxs-lookup"><span data-stu-id="f5d7e-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="f5d7e-117">클러스터를 사용자 지정하는 스크립트 작업을 사용하는 경우 웹 UI를 노출하는 설치하는 모든 서비스 또는 유틸리티는 SSH 터널이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="f5d7e-118">예를 들어 스크립트 작업을 사용하여 Hue를 설치하는 경우 SSH 터널을 사용하여 Hue 웹 UI에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5d7e-119">가상 네트워크를 통해 HDInsight에 대한 직접 액세스가 있는 경우 SSH 터널을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="f5d7e-120">가상 네트워크를 통해 HDInsight에 직접 액세스하는 예는 [온-프레미스 네트워크에 HDInsight 연결](connect-on-premises-network.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="f5d7e-121">SSH 터널이란</span><span class="sxs-lookup"><span data-stu-id="f5d7e-121">What is an SSH tunnel</span></span>

<span data-ttu-id="f5d7e-122">[Secure Shell(SSH) 터널링](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling)은 로컬 워크스테이션의 포트로 전송된 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="f5d7e-123">이 트래픽은 SSH 연결을 통해 HDInsight 클러스터 헤드 노드로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="f5d7e-124">해당 요청은 마치 헤드 노드에서 시작된 것처럼 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="f5d7e-125">그러면 응답은 워크스테이션에 대한 터널을 통해 다시 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5d7e-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f5d7e-126">Prerequisites</span></span>

* <span data-ttu-id="f5d7e-127">SSH 클라이언트.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-127">An SSH client.</span></span> <span data-ttu-id="f5d7e-128">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="f5d7e-129">SOCKS5 프록시를 사용하도록 구성할 수 있는 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f5d7e-130">Windows에 기본 제공된 SOCKS 프록시 지원은 SOCKS5를 지원하지 않고 이 문서의 단계에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="f5d7e-131">다음 브라우저는 Windows 프록시 설정에 의존하고 현재 이 문서의 단계에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="f5d7e-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="f5d7e-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="f5d7e-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="f5d7e-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="f5d7e-134">Google Chrome도 Windows 프록시 설정에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="f5d7e-135">그러나 SOCKS5를 지원하는 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="f5d7e-136">[FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="f5d7e-137"><a name="usessh"></a>SSH 명령을 사용하여 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="f5d7e-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="f5d7e-138">`ssh` 명령을 사용하여 SSH 터널을 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="f5d7e-139">**USERNAME**을 HDInsight 클러스터에 대한 SSH 사용자로 바꾸고 **CLUSTERNAME**을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="f5d7e-140">이 명령은 로컬 포트 9876에서 SSH를 통해 클러스터에 트래픽을 라우팅하는 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="f5d7e-141">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-141">The options are:</span></span>

* <span data-ttu-id="f5d7e-142">**D 9876** - 터널을 통해 트래픽을 라우팅하는 로컬 포트</span><span class="sxs-lookup"><span data-stu-id="f5d7e-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="f5d7e-143">**C** - 웹 트래픽은 대부분 텍스트이므로 모든 데이터 압축</span><span class="sxs-lookup"><span data-stu-id="f5d7e-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="f5d7e-144">**2** - SSH가 프로토콜 버전 2만 시도하도록 강요</span><span class="sxs-lookup"><span data-stu-id="f5d7e-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="f5d7e-145">**q** - 자동 모드</span><span class="sxs-lookup"><span data-stu-id="f5d7e-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="f5d7e-146">**T** - 포트 전달 후 허위 tty 할당 비활성화</span><span class="sxs-lookup"><span data-stu-id="f5d7e-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="f5d7e-147">**n** - 포트 전달 후 STDIN 읽지 않음</span><span class="sxs-lookup"><span data-stu-id="f5d7e-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="f5d7e-148">**N** - 포트 전달 후 원격 명령 실행 안 함</span><span class="sxs-lookup"><span data-stu-id="f5d7e-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="f5d7e-149">**f** - 백그라운드에서 실행</span><span class="sxs-lookup"><span data-stu-id="f5d7e-149">**f** - Run in the background.</span></span>

<span data-ttu-id="f5d7e-150">명령이 완료되면 로컬 컴퓨터에서 9876 포트로 전송되는 트래픽이 클러스터 헤드 노드로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="f5d7e-151"><a name="useputty"></a>PuTTY를 사용하여 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="f5d7e-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="f5d7e-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty)는 Windows용 그래픽 SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="f5d7e-153">PuTTY를 사용하여 SSH 터널을 만들려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="f5d7e-154">PuTTY를 열고 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="f5d7e-155">PuTTY에 대해 잘 모르는 경우 [PuTTY 설명서(영문)(http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="f5d7e-156">대화 상자의 왼쪽에 있는 **Category** 섹션에서 **Connection**, **SSH**를 차례로 확장한 다음 **Tunnels**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="f5d7e-157">**Options controlling SSH port forwarding** 양식에 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="f5d7e-158">**Source port** - 전달하려는 클라이언트의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="f5d7e-159">예를 들면 **9876**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-159">For example, **9876**.</span></span>

   * <span data-ttu-id="f5d7e-160">**Destination** - Linux 기반 HDInsight 클러스터의 SSH 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f5d7e-161">예를 들면 **mycluster-ssh.azurehdinsight.net**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="f5d7e-162">**Dynamic** - 동적 SOCKS 프록시 라우팅을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![터널링 옵션 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="f5d7e-164">**Add**를 클릭하여 설정을 추가한 다음 **Open**을 클릭하여 SSH 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="f5d7e-165">메시지가 표시되면 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="f5d7e-166">브라우저에서 터널 사용</span><span class="sxs-lookup"><span data-stu-id="f5d7e-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5d7e-167">이 섹션의 단계에서는 Mozilla FireFox 브라우저를 사용합니다. 이 브라우저는 모든 플랫폼에서 동일한 프록시 설정을 제공하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="f5d7e-168">Google Chrome 등의 다른 최신 브라우저에는 터널에서 작동하기 위해 FoxyProxy 등의 확장이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="f5d7e-169">**localhost**와 **SOCKS v5** 프록시로 터널을 만들 때 사용한 포트를 사용하도록 브라우저를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="f5d7e-170">Firefox 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="f5d7e-171">9876이 아닌 다른 포트를 사용한 경우 포트를 사용한 포트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![Firefox 설정 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="f5d7e-173">**Remote DNS**를 선택하면 HDInsight 클러스터를 통해 DNS(Domain Name System) 요청이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="f5d7e-174">이 설정은 클러스터의 헤드 노드를 사용하여 DNS를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="f5d7e-175">[http://www.whatismyip.com/](http://www.whatismyip.com/)과 같은 사이트를 방문하여 터널이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="f5d7e-176">반환된 IP는 Microsoft Azure 데이터 센터에서 사용하는 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="f5d7e-177">Ambari 웹 UI 통해 확인</span><span class="sxs-lookup"><span data-stu-id="f5d7e-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="f5d7e-178">클러스터를 설정한 후에 Ambari 웹에서 서비스 웹 UI에 액세스할 수 있는지 확인하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="f5d7e-179">브라우저에서 http://headnodehost:8080 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="f5d7e-180">`headnodehost` 주소는 터널을 통해 클러스터로 전송되며 Ambari가 실행 중인 헤드 노드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="f5d7e-181">메시지가 표시되면 클러스터의 관리자 사용자 이름(관리자) 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="f5d7e-182">Ambari 웹 UI에서 두 번째로 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="f5d7e-183">이러한 경우 정보를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f5d7e-184">http://headnodehost:8080 주소를 사용하여 클러스터에 연결할 경우 터널을 통해 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="f5d7e-185">통신 보안은 HTTPS가 아닌 SSH 터널을 사용하여 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="f5d7e-186">HTTPS를 사용하여 인터넷을 통해 연결하려면 https://CLUSTERNAME.azurehdinsight.net을 사용합니다. 여기서 **CLUSTERNAME**은 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="f5d7e-187">Ambari 웹 UI에서 페이지의 왼쪽 목록에서 HDFS를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![HDFS가 선택된 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="f5d7e-189">HDFS 서비스 정보가 표시되면 **빠른 링크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="f5d7e-190">클러스터 헤드 노드 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="f5d7e-191">헤드 노드 중 하나를 선택한 다음 **NameNode UI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![확장된 빠른 링크 메뉴의 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="f5d7e-193">__빠른 링크__를 선택하면 대기 표시기가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="f5d7e-194">인터넷 연결 속도가 느린 경우 이러한 상태가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="f5d7e-195">데이터를 서버에서 받을 때까지 기다렸다가 목록을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="f5d7e-196">**빠른 링크** 메뉴의 일부 항목이 화면 오른쪽에서 잘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="f5d7e-197">그럴 경우 마우스를 사용하여 메뉴를 확장한 다음 오른쪽 화살표 키를 사용하여 메뉴의 나머지 부분을 볼 수 있도록 오른쪽으로 화면을 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="f5d7e-198">다음 이미지와 유사한 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-198">A page similar to the following image is displayed:</span></span>

    ![NameNode UI의 이미지](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="f5d7e-200">이 페이지의 URL에 유의하세요. **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="f5d7e-201">이 URI는 노드의 내부 FQDN(정규화된 도메인 이름)을 사용하며 SSH 터널을 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5d7e-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5d7e-202">Next steps</span></span>

<span data-ttu-id="f5d7e-203">SSH 터널을 만들고 사용하는 방법을 배웠으므로 다음 문서에서 Ambari를 사용하는 다른 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="f5d7e-204">Ambari를 사용하여 HDInsight 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="f5d7e-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="f5d7e-205">HDInsight에서의 SSH 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5d7e-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

