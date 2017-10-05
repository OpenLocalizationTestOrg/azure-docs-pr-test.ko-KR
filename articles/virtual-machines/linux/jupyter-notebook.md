---
title: "Jupyter/IPython Notebook 만들기 | Microsoft Docs"
description: "Azure의 리소스 관리자 배포 모델을 사용하여 만든 Linux 가상 컴퓨터에 Jupyter/IPython Notebook을 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="7adec-103">Azure에서 Azure VM 만들기, Jupyter 설치 및 Jupyter Notebook 실행</span><span class="sxs-lookup"><span data-stu-id="7adec-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="7adec-104">[IPython 프로젝트](http://ipython.org) 이전의 [Jupyter 프로젝트](http://jupyter.org)는 라이브 계산 문서의 생성을 사용하여 코드 실행을 결합하는 강력한 대화형 셸을 사용하여 과학적 계산용 도구의 컬렉션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="7adec-105">이러한 노트북 파일에는 임의 텍스트, 수식, 입력 코드, 결과, 그래픽, 비디오를 비롯하여 최신 웹 브라우저에서 표시할 수 있는 기타 모든 미디어가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="7adec-106">Python을 처음 접하며 재미있는 대화형 환경에서 이를 배우려는 경우든, 병렬/기술 컴퓨팅에 대해 상당한 조예가 있는 경우든 Jupyter Notebook을 사용하면 많은 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="7adec-107">![스크린샷](./media/jupyter-notebook/ipy-notebook-spectral.png) SciPy 및 Matplotlib 패키지를 사용하여 소리 녹음의 구조를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="7adec-108">Jupyter 두 가지 방법: Azure 노트북 또는 사용자 지정 배포</span><span class="sxs-lookup"><span data-stu-id="7adec-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="7adec-109">Azure는 [Jupyter를 사용하여 즉시 시작 ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)하는데 사용할 수 있는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="7adec-110">Azure 노트북 서비스를 사용하면 Python과 많은 라이브러리를 완벽하게 활용할 수 있는, 확장 가능한 컴퓨팅 리소스에 대한 Jupyter의 웹 기반 인터페이스에 대한 액세스를 쉽게 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="7adec-111">설치는 서비스에 의해 처리되므로 사용자는 사용자에 의한 관리 및 구성에 대한 필요 없이 이러한 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="7adec-112">노트북 서비스가 시나리오에 대해 작동하지 않는 경우 Linux 가상 컴퓨터(VM)를 사용하여 Microsoft Azure의 Jupyter Notebook을 배포하는 방법을 보여 주는 이 문서를 계속해서 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="7adec-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="7adec-113">Azure에서 VM 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="7adec-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="7adec-114">첫 번째 단계는 Azure에서 실행되는 VM(가상 컴퓨터)을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="7adec-115">이 VM은 클라우드에서 작동하는 완벽한 운영 체제이며 Jupyter Notebook을 실행하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="7adec-116">Azure는 Linux 및 Windows 가상 컴퓨터를 모두 실행할 수 있으므로, 두 가지 유형의 가상 컴퓨터에서 Jupyter를 설치하는 과정에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="7adec-117">Linux VM을 만들고 Jupyter에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="7adec-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="7adec-118">[여기][portal-vm-linux]에 나와 있는 지침에 따라 *Ubuntu* 배포의 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="7adec-119">이 자습서에서는 Ubuntu Server 14.04 LTS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="7adec-120">사용자 이름은 *azureuser*라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="7adec-121">가상 컴퓨터가 배포한 후 네트워크 보안 그룹의 보안 규칙을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="7adec-122">Azure Portal에서 **네트워크 보안 그룹**으로 이동하고 VM에 해당하는 보안 그룹에 대한 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="7adec-123">프로토콜에 대한 **TCP**, 원본(공용) 포트에 대한**\*** 및 대상(개인) 포트에 대한 **9999** 설정을 사용하여 인바운드 보안 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![스크린샷](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="7adec-125">네트워크 보안 그룹에 있는 동안 **네트워크 인터페이스**를 클릭하고 다음 단계에서 VM에 연결하는데 필요하므로 **공용 IP 주소**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="7adec-126">VM에 필수 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="7adec-126">Install required software on the VM</span></span>
<span data-ttu-id="7adec-127">VM에서 Jupyter Notebook을 실행하려면 먼저 Jupyter 및 종속성을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="7adec-128">vm을 만들 때 선택한 ssh 및 사용자 이름/암호 쌍을 사용하여 linux vm에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="7adec-129">이 자습서에서는 PuTTY를 사용하고 Windows에서 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="7adec-130">Ubuntu에 Jupyter 설치</span><span class="sxs-lookup"><span data-stu-id="7adec-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="7adec-131">[지속성 분석](https://www.continuum.io/downloads)에서 제공된 링크 중 하나를 사용하여 인기 있는 데이터 과학 python 배포인 Anaconda를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="7adec-132">이 문서를 작성할 당시 아래 링크는 가장 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="7adec-133">Linux용 Anaconda 설치</span><span class="sxs-lookup"><span data-stu-id="7adec-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="7adec-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="7adec-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="7adec-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="7adec-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="7adec-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="7adec-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="7adec-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="7adec-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="7adec-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="7adec-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="7adec-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32비트</href>
    </span><span class="sxs-lookup"><span data-stu-id="7adec-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="7adec-140">Ubuntu에 Anaconda3 2.3.0 64비트 설치</span><span class="sxs-lookup"><span data-stu-id="7adec-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="7adec-141">예로 Ubuntu에 Anaconda를 설치하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![스크린샷](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="7adec-143">Jupyter 구성 및 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="7adec-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="7adec-144">설치한 후 Jupyter에 대한 구성 파일을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="7adec-145">Jupyter 구성 문제가 발생하는 경우 [노트북 서버 실행에 대한 Jupyter 설명서](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)를 보면 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="7adec-146">그런 다음 프로필 디렉터리로 변경하여( `cd` ) SSL 인증서를 만들고 프로필 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="7adec-147">Linux에서는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="7adec-148">다음 명령을 사용하여 SSL 인증서를 만듭니다(Linux 및 Windows).</span><span class="sxs-lookup"><span data-stu-id="7adec-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="7adec-149">자체 서명된 SSL 인증서를 만들고 있으므로 노트북에 연결할 때 브라우저에서 보안 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="7adec-150">장기 프로덕션용으로는 조직과 연결된 적절히 서명된 인증서를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="7adec-151">이 데모에서는 인증서 관리를 다루지 않으므로 지금은 자체 서명된 인증서만을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="7adec-152">인증서를 사용할 뿐만 아니라, 권한이 없는 사용자로부터 노트북을 보호하기 위해 암호도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="7adec-153">보안상의 이유로 Jupyter는 구성 파일에서 암호화된 암호를 사용하므로, 먼저 암호를 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="7adec-154">IPython에서 암호화할 수 있는 유틸리티를 제공하므로 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="7adec-155">암호 및 암호 확인을 위한 프롬프트가 표시된 후 암호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="7adec-156">다음 단계를 위해 암호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="7adec-157">다음으로, 프로필 구성 파일을 편집합니다. 사용자가 있는 디렉터리의 `jupyter_notebook_config.py` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="7adec-158">이 파일이 존재하지 않을 수 있습니다. 이 경우 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="7adec-159">이 파일에는 여러 필드가 포함되어 있으며 기본적으로 모든 필드는 주석 처리되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="7adec-160">원하는 텍스트 편집기로 이 파일을 열 수 있으며, 다음과 같은 내용이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="7adec-161">**구성에 있는 c.NotebookApp.password를 이전 단계의 sha1로 대체해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="7adec-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="7adec-162">Jupyter Notebook 실행</span><span class="sxs-lookup"><span data-stu-id="7adec-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="7adec-163">이제 Jupyter Notebook을 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="7adec-164">이렇게 하려면 노트북을 저장할 디렉터리로 이동한 후 다음 명령을 사용하여 Jupyter Notebook 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="7adec-165">이제 주소 `https://[PUBLIC-IP-ADDRESS]:9999`의 Jupyter Notebook에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="7adec-166">노트북에 처음 액세스하는 경우 로그인 페이지에서 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="7adec-167">로그인한 후에는 모든 노트북 작업에 대한 제어 센터인 "Jupyter Notebook 대시보드"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="7adec-168">이 페이지에서 새 노트북을 만들고 기존 노트북을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-168">From this page you can create new notebooks and open existing ones.</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="7adec-170">Jupyter Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="7adec-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="7adec-171">**New** 단추를 클릭하는 경우 다음과 같은 여는 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-171">If you click the **New** button, you will see the following opening page.</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="7adec-173">`In []:` 프롬프트로 표시되는 이 영역은 입력 영역이며, 여기서 유효한 Python 코드를 입력할 수 있고 `Shift-Enter`를 누르거나 "Play" 아이콘(도구 모음의 오른쪽을 가리키는 삼각형)을 클릭하면 코드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="7adec-174">강력한 패러다임: 다양한 미디어를 지원하는 라이브 컴퓨팅 문서</span><span class="sxs-lookup"><span data-stu-id="7adec-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="7adec-175">노트북은 Python과 워드 프로세서가 결합된 방식이므로 노트북 자체는 Python 및 워드 프로세서를 사용해 본 적이 있는 사람들에게는 매우 자연스럽게 느껴집니다. Python 코드 블록을 실행할 수 있지만 도구 모음의 드롭다운 메뉴를 사용하여 "Code"에서 "Markdown"으로 셀 스타일을 변경해서 메모 및 기타 텍스트를 유지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="7adec-176">Jupyter는 컴퓨팅 및 다양한 미디어(텍스트, 그래픽, 비디오 및 최신 웹 브라우저에서 표시할 수 있는 모든 것)의 결합을 허용하므로 워드 프로세서보다 훨씬 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="7adec-177">텍스트, 코드, 동영상 및 더 많은 것을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-177">You can mix, text, code, videos and more!</span></span>

![스크린샷](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="7adec-179">또한 Python에서 지원하는 여러 가지 탁월한 과학 및 기술 컴퓨팅용 라이브러리 덕분에 다음 스크린샷과 같이 단일 환경에서 단순한 계산뿐만 아니라 복잡한 네트워크 분석도 간편하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="7adec-180">최신 웹 기능과 라이브 컴퓨팅을 결합한 이 패러다임은 많은 가능성을 제공하며, 클라우드에 이상적으로 적합하므로 Notebook을 다음과 같이 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="7adec-181">컴퓨팅 스크래치패드로 사용하여 문제에 대한 예비 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="7adec-182">'라이브' 컴퓨팅 형식이나 하드카피 형식(HTML, PDF)으로 결과를 동료와 공유하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="7adec-183">학생들이 실제 코드로 즉시 실험해 보고 수정하고 대화형으로 다시 실행할 수 있도록 계산이 포함된 라이브 교육 교재를 배포하고 표시하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="7adec-184">다른 사람이 즉시 재현하고 유효성을 검사하고 확장할 수 있는 방식으로, 연구 결과를 나타내는 "실행 가능한 백서"를 제공하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="7adec-185">협업 컴퓨팅을 위한 플랫폼으로 사용할 수 있습니다. 즉, 여러 사용자가 동일한 노트북 서버에 로그인하여 라이브 컴퓨팅 세션을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="7adec-186">IPython 소스 코드 [리포지토리][repository]로 이동하면 Notebook 예제가 있는 전체 디렉터리를 볼 수 있습니다. 여기서 예제를 다운로드하여 Azure Jupyter VM에서 실험해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="7adec-187">사이트에서 `.ipynb` 파일을 다운로드하고 노트북 Azure VM의 대시보드에 업로드(또는 VM으로 직접 다운로드)하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="7adec-188">결론</span><span class="sxs-lookup"><span data-stu-id="7adec-188">Conclusion</span></span>
<span data-ttu-id="7adec-189">Jupyter Notebook은 Azure에서 Python 에코시스템의 기능에 대화형으로 액세스할 수 있는 강력한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="7adec-190">이 인터페이스는 간단한 Python 탐색 및 학습, 데이터 분석 및 시각화, 시뮬레이션, 병렬 컴퓨팅 등 다양한 사용 사례를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="7adec-191">결과적으로 생성된 Notebook 문서에는 작업을 수행한 후 다른 Jupyter 사용자와 공유할 수 있는 전체 컴퓨팅 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="7adec-192">Jupyter Notebook은 로컬 응용 프로그램으로 사용할 수 있지만 Azure의 클라우드 배포에 이상적으로 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="7adec-193">또한 Jupyter의 핵심 기능은 PTVS([Python Tools for Visual Studio][Python Tools for Visual Studio])를 통해 Visual Studio 내에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="7adec-194">PTVS는 Microsoft의 무료 오픈 소스 플러그 인으로, IntelliSense, 디버깅, 프로파일링, 병렬 컴퓨팅 통합 등 고급 편집기 기능을 포함하는 고급 Python 개발 환경으로 Visual Studio를 전환해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7adec-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7adec-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7adec-195">Next steps</span></span>
<span data-ttu-id="7adec-196">자세한 내용은 [Python 개발자 센터](/develop/python/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7adec-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
