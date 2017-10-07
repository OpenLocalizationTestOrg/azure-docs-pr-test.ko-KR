---
title: "Jupyter/IPython 노트북 aaaCreate | Microsoft Docs"
description: "Toodeploy hello Jupyter/IPython 전자 필기장 Linux 가상 컴퓨터에서 Azure의 hello 리소스 관리자 배포 모델을 사용 하 여 만든 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="3dad9-103">Azure에서 Azure VM 만들기, Jupyter 설치 및 Jupyter Notebook 실행</span><span class="sxs-lookup"><span data-stu-id="3dad9-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="3dad9-104">hello [Jupyter 프로젝트](http://jupyter.org), 이전의 hello [IPython 프로젝트](http://ipython.org), 용 도구의 컬렉션을 제공 hello 만들기로 코드 실행을 결합 하는 강력한 대화형 셸을 사용 하 여 과학적 컴퓨팅 라이브 계산 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="3dad9-105">이러한 노트북 파일에는 임의 텍스트, 수식, 입력 코드, 결과, 그래픽, 비디오를 비롯하여 최신 웹 브라우저에서 표시할 수 있는 기타 모든 미디어가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="3dad9-106">절대적으로 새 tooPython 하 고 toolearn 원하는 재미, 대화형 환경 또는 일부 심각한 병렬/기술적 컴퓨팅, Jupyter 노트북 hello 최선의 선택은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="3dad9-107">![스크린 샷](./media/jupyter-notebook/ipy-notebook-spectral.png) 사운드 녹음의를 사용 하 여 SciPy, Matplotlib 패키지 tooanalyze hello 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="3dad9-108">Jupyter 두 가지 방법: Azure 노트북 또는 사용자 지정 배포</span><span class="sxs-lookup"><span data-stu-id="3dad9-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="3dad9-109">도 사용할 수 있는 서비스를 제공 하는 azure[Jupyter 사용을 즉시 시작 ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="3dad9-110">Hello Azure 노트북 서비스를 사용 하 여 얻을 수 있습니다 쉽게 액세스 tooJupyter 웹에 액세스할 수 있는 인터페이스 모든 hello 전원을 python 및 많은 해당 라이브러리를 사용 하 여 확장 가능한 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="3dad9-111">Hello 설치는 hello 서비스에 의해를 처리 하므로 사용자 관리 및 hello 사용자가 구성에 대 한 hello 필요 없이 이러한 리소스를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="3dad9-112">Hello 노트북 서비스 시나리오에 대해 작동 하지 않을 경우이 문서는 보여 주는 방법을 toodeploy hello Jupyter 노트북 Microsoft Azure에서 Linux 가상 컴퓨터 (Vm)를 사용 하 여 계속 tooread 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3dad9-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="3dad9-113">Azure에서 VM 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="3dad9-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="3dad9-114">hello 첫 번째 단계는 toocreate Azure에서 실행 되는 가상 컴퓨터 (VM).</span><span class="sxs-lookup"><span data-stu-id="3dad9-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="3dad9-115">이 VM hello 클라우드에서 전체 운영 체제 이며 hello Jupyter 노트북 실행에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="3dad9-116">Azure 가상 컴퓨터, Linux 및 Windows를 실행할 수 있는 이며 Jupyter 두 유형의 가상 컴퓨터에 설치 하는 hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="3dad9-117">Linux VM을 만들고 Jupyter에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="3dad9-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="3dad9-118">제공 된 hello 지침에 따라 [여기] [ portal-vm-linux] toocreate hello의 가상 컴퓨터 *Ubuntu* 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="3dad9-119">이 자습서에서는 Ubuntu Server 14.04 LTS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="3dad9-120">사용자 이름 hello에서는 *azureuser*합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="3dad9-121">Hello 가상 컴퓨터를 배포한 후 hello 네트워크 보안 그룹에 대 한 보안 규칙을 tooopen이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="3dad9-122">Hello Azure 포털에서에서 이동 너무**네트워크 보안 그룹** 및 hello 보안 그룹이 해당 tooyour VM에 대 한 열기 hello 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="3dad9-123">다음 설정을 hello로 tooadd 인바운드 보안 규칙 필요: **TCP** hello 프로토콜에 대 한  **\***  hello 소스 (공용) 포트에 대 한 및 **9999** 에 대 한 hello (개인) 대상 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![스크린샷](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="3dad9-125">네트워크 보안 그룹에서 클릭 **네트워크 인터페이스** 및 참고 hello **공용 IP 주소** hello 다음 단계에서 필요한 tooconnect tooyour VM 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="3dad9-126">Hello VM에 필요한 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-126">Install required software on hello VM</span></span>
<span data-ttu-id="3dad9-127">toorun hello 우리의 VM에서 Jupyter 노트북, Jupyter과 해당 종속성을 설치 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="3dad9-128">Ssh를 사용 하 여 tooyour linux vm을 연결 하 고 hello 사용자 이름/암호 쌍을 만들 때 선택한 vm hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="3dad9-129">이 자습서에서는 PuTTY를 사용하고 Windows에서 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="3dad9-130">Ubuntu에 Jupyter 설치</span><span class="sxs-lookup"><span data-stu-id="3dad9-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="3dad9-131">Anaconda, 인기 있는 데이터 과학 python 배포는에서 제공 하는 hello 링크 중 하나를 사용 하 여 설치 [Continuum Analytics](https://www.continuum.io/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="3dad9-132">Hello이 문서의 문서를 작성할 당시 아래 링크 hello hello toodate 버전을 가장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="3dad9-133">Linux용 Anaconda 설치</span><span class="sxs-lookup"><span data-stu-id="3dad9-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="3dad9-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="3dad9-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="3dad9-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="3dad9-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="3dad9-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="3dad9-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="3dad9-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="3dad9-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3dad9-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="3dad9-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="3dad9-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="3dad9-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="3dad9-140">Ubuntu에 Anaconda3 2.3.0 64비트 설치</span><span class="sxs-lookup"><span data-stu-id="3dad9-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="3dad9-141">예로 Ubuntu에 Anaconda를 설치하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![스크린샷](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="3dad9-143">Jupyter 구성 및 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="3dad9-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="3dad9-144">설치한 후 tootake 순간 toosetup hello 구성 파일에 필요한 Jupyter 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="3dad9-145">Jupyter 구성 문제를 발생 하는 경우는 것이 유용한 toolook hello에 [Jupyter 노트북 서버를 실행 하는 데는 설명서](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="3dad9-146">다음에서는 `cd` toohello 디렉터리 toocreate 우리의 SSL 인증서를 프로 파일링 하 고 hello 프로필 구성 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="3dad9-147">Linux에서 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="3dad9-148">명령 toocreate hello SSL 인증서 (Linux 및 Windows)를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="3dad9-149">참고는 이후 생성 자체 서명 된 SSL 인증서를 toohello 노트북을 연결할 때 브라우저에서 보안 경고를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="3dad9-150">장기 프로덕션 용도로 toouse 조직과 연결 된 제대로 서명 된 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="3dad9-151">이 데모의 hello 범위를 벗어나 인증서 관리 이므로 지금은 tooa 자체 서명 된 인증서 대해서만 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="3dad9-152">또한 toousing 인증서도 제공 해야 암호 tooprotect 전자 필기장을 무단된으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="3dad9-153">보안상의 이유로 Jupyter 암호를 사용의 구성 파일에 암호화 된 암호 tooencrypt 필요 하므로 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="3dad9-154">IPython 제공 유틸리티 toodo. 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="3dad9-155">이 사용자를 입력 한 암호와 확인, 고 hello 암호 다음 인쇄 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="3dad9-156">단계 다음에 나오는 hello에 대 한이 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="3dad9-157">다음으로 hello 프로필의 구성 파일을 편집 합니다는 `jupyter_notebook_config.py` hello 디렉터리에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="3dad9-158">이 파일이 존재 하지 않을 수 있습니다-참고 hello 그럴 경우 새로 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="3dad9-159">이 파일에는 여러 필드가 포함되어 있으며 기본적으로 모든 필드는 주석 처리되어 있습니다.  원하는 대로의 텍스트 편집기로이 파일을 열 수 있습니다 다음 콘텐츠 이상 hello에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="3dad9-160">**Hello 이전 단계의 hello sha1 가진 hello 구성에 있는지 tooreplace hello c.NotebookApp.password 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="3dad9-161">Jupyter 노트북 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="3dad9-162">이 시점에서 준비 toostart hello Jupyter 노트북 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="3dad9-163">toodo이 이동 toohello 디렉터리 toostore 전자 필기장에 원하는 하 고 다음 명령을 hello로 hello Jupyter 노트북 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="3dad9-164">이제 해야 수 수 tooaccess hello 주소에서 Jupyter 노트북 `https://[PUBLIC-IP-ADDRESS]:9999`합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="3dad9-165">전자 필기장을 처음 사용할 때 암호 hello 로그인 페이지를 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="3dad9-166">에 로그인 되 고 있습니다 "Jupyter 노트북 대시보드" hello 모든 전자 필기장 작업에 대 한 제어 센터인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="3dad9-167">이 페이지에서 새 노트북을 만들고 기존 노트북을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-167">From this page you can create new notebooks and open existing ones.</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="3dad9-169">Hello Jupyter 노트북을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3dad9-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="3dad9-170">Hello를 누르면 **새로** 단추, 시작 페이지를 수행 하는 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="3dad9-172">hello 영역으로 표시는 `In []:` hello 입력된 영역 프롬프트는 여기서 모든 유효한 Python 코드를 입력할 수 있습니다 및에 도달 하면 실행 될 `Shift-Enter` 하거나 hello "재생" 아이콘 (hello 오른쪽 방향 삼각형 hello 도구 모음에서)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="3dad9-173">강력한 패러다임: 다양한 미디어를 지원하는 라이브 컴퓨팅 문서</span><span class="sxs-lookup"><span data-stu-id="3dad9-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="3dad9-174">자체 hello 노트북에에서 있기 때문에 몇 가지 방법 모두의 혼합 매우 자연 tooanyone Python 및 워드 프로세서 사용 경험이 있어야: Python 코드 블록을 실행할 수 있지만 너무 "코드"에서 셀의 hello 스타일을 변경 하 여 정보 및 기타 텍스트를 유지할 수도 있습니다 "Ma rkdown "hello 드롭다운 메뉴를 사용 하 여 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="3dad9-175">Jupyter는 컴퓨팅 및 다양한 미디어(텍스트, 그래픽, 비디오 및 최신 웹 브라우저에서 표시할 수 있는 모든 것)의 결합을 허용하므로 워드 프로세서보다 훨씬 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="3dad9-176">텍스트, 코드, 동영상 및 더 많은 것을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-176">You can mix, text, code, videos and more!</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="3dad9-178">있고 과학 및 기술 컴퓨팅, 다음 스크린 샷에서 hello에 Python의 많은 뛰어난 라이브러리의 전원이 hello 간단한 계산을 수행할 수 있는 한 환경에서 모든을 복잡 한 네트워크 분석으로 쉽게 동일 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="3dad9-179">이러한 패러다임 hello 최신 웹의 hello 전원 라이브 계산와 혼합의 다양 한 비즈니스 가능성이 제공 하 고 hello 클라우드;에 가장 적합 hello 노트북을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="3dad9-180">예비는 계산 잠깐 보관 함 toorecord로 문제에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="3dad9-181">tooshare 하드 카피 형식 (HTML, PDF) 또는 '라이브' 계산 폼에 동료와 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="3dad9-182">toodistribute 및 학생 hello 실제 코드를 시험해 볼 즉시 수 있으므로 계산을 포함 하는 현재 라이브 교육 자료에는 수정 하 고 다시 대화형으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="3dad9-183">hello 연구 결과에 즉시 재현 될 수 있는 방식으로 제공 하는 "실행 파일 논문" tooprovide 유효성을 검사 하 고 다른 사용자가 확장.</span><span class="sxs-lookup"><span data-stu-id="3dad9-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="3dad9-184">공동 컴퓨팅 플랫폼으로 서: 여러 사용자가 로그인 할 수 toothe 동일 노트북 서버 tooshare 라이브 계산 세션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="3dad9-185">Toohello IPython 소스 코드를 이동 하는 경우 [리포지토리][repository], 노트북 예제를 다운로드 하 고 다음 사용해 자신의 Azure Jupyter vm 수와 전체 디렉터리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="3dad9-186">Hello 다운로드 `.ipynb` 파일 hello에서 사이트 및 전자 필기장 Azure VM의 hello 대시보드에 업로드 (또는 hello VM에 직접 다운로드할).</span><span class="sxs-lookup"><span data-stu-id="3dad9-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="3dad9-187">결론</span><span class="sxs-lookup"><span data-stu-id="3dad9-187">Conclusion</span></span>
<span data-ttu-id="3dad9-188">hello Jupyter 노트북 대화형으로 Azure에서 Python 생태계 hello의 hello 전원에 액세스 하기 위한 강력한 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="3dad9-189">이 인터페이스는 간단한 Python 탐색 및 학습, 데이터 분석 및 시각화, 시뮬레이션, 병렬 컴퓨팅 등 다양한 사용 사례를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="3dad9-190">hello 결과 노트북 문서 hello 계산을 수행 되 고 다른 Jupyter 사용자와 공유할 수 있는 완전 한 레코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="3dad9-191">Azure에서 클라우드 배포에 가장 적합 하지만 hello Jupyter 노트북 로컬 응용 프로그램으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="3dad9-192">Jupyter의 hello 핵심 기능을 통해 Visual Studio 내에서 사용할 수는는 [Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="3dad9-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="3dad9-193">PTVS는 Microsoft의 무료 오픈 소스 플러그 인으로, IntelliSense, 디버깅, 프로파일링, 병렬 컴퓨팅 통합 등 고급 편집기 기능을 포함하는 고급 Python 개발 환경으로 Visual Studio를 전환해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dad9-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3dad9-194">Next steps</span></span>
<span data-ttu-id="3dad9-195">자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3dad9-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
