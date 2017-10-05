---
title: "Python 및 SDK 설치 - Azure"
description: "Azure에서 사용할 Python 및 SDK를 설치하는 방법에 대해 알아봅니다."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="29cfc-103">Python 및 SDK 설치</span><span class="sxs-lookup"><span data-stu-id="29cfc-103">Installing Python and the SDK</span></span>
<span data-ttu-id="29cfc-104">Python은 Windows에서 쉽게 설정할 수 있으며 Mac, Linux 및 [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about)에서는 사전 설치되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="29cfc-105">이 가이드에서는 설치 및 Azure와 함께 사용할 수 있도록 컴퓨터를 설정하는 작업을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="29cfc-106">Python Azure SDK에 포함된 내용</span><span class="sxs-lookup"><span data-stu-id="29cfc-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="29cfc-107">Python용 Azure SDK에는 Azure용 Python 응용 프로그램을 개발, 배포 및 관리할 수 있는 구성 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="29cfc-108">구체적으로 말해서 Python용 Azure SDK에는 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="29cfc-109">**관리 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="29cfc-109">**Management libraries**.</span></span> <span data-ttu-id="29cfc-110">이러한 클래스 라이브러리는 저장소, 계정, 가상 컴퓨터와 같은 Azure 리소스를 관리하는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="29cfc-111">**런타임 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="29cfc-111">**Runtime libraries**.</span></span> <span data-ttu-id="29cfc-112">이러한 클래스 라이브러리는 저장소 및 서비스 버스와 같은 Azure 기능에 액세스하는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="29cfc-113">사용할 Python 및 버전</span><span class="sxs-lookup"><span data-stu-id="29cfc-113">Which Python and which version to use</span></span>
<span data-ttu-id="29cfc-114">사용할 수 있는 몇 가지의 Python 인터프리터 옵션이 있으며 다음을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="29cfc-115">CPython - 가장 일반적으로 사용되는 표준 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="29cfc-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="29cfc-116">PyPy - 빠르고 규정을 준수하는 CPython에 대한 대체 구현</span><span class="sxs-lookup"><span data-stu-id="29cfc-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="29cfc-117">IronPython - .Net/CLR에서 실행되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="29cfc-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="29cfc-118">Jython - Java 가상 컴퓨터에서 실행되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="29cfc-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="29cfc-119">**CPython** v2.7 또는 v3.3 이상 및 PyPy 5.4.0은 Python Azure SDK에 대해 테스트 및 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="29cfc-120">Python을 구하는 위치</span><span class="sxs-lookup"><span data-stu-id="29cfc-120">Where to get Python?</span></span>
<span data-ttu-id="29cfc-121">CPython을 구하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="29cfc-122">[www.python.org][www.python.org]에서 직접</span><span class="sxs-lookup"><span data-stu-id="29cfc-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="29cfc-123">[www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] 또는 [www.activestate.com][www.activestate.com]과 같은 신뢰할 수 있는 배포자로부터</span><span class="sxs-lookup"><span data-stu-id="29cfc-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="29cfc-124">원본에서 빌드</span><span class="sxs-lookup"><span data-stu-id="29cfc-124">Build from source!</span></span>

<span data-ttu-id="29cfc-125">구체적인 요구 사항이 없다면 처음 두 가지 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="29cfc-126">Windows, Linux 및 MacOS에 SDK 설치(클라이언트 라이브러리만 해당)</span><span class="sxs-lookup"><span data-stu-id="29cfc-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="29cfc-127">Python이 이미 설치되어 있는 경우 pip를 사용하여 기존 Python 2.7 또는 Python 3.3 + 환경에 모든 클라이언트 라이브러리의 번들을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="29cfc-128">이 경우 [PyPI(Python 패키지 인덱스)][Python Package Index]에서 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="29cfc-129">관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-129">You may need administrator rights:</span></span>

* <span data-ttu-id="29cfc-130">Linux 및 MacOS, 다음 `sudo` 명령을 사용합니다. `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="29cfc-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="29cfc-131">Windows: 관리자로 PowerShell/명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="29cfc-132">각 Azure 서비스에 대한 각 라이브러리를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="29cfc-133">미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="29cfc-134">`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="29cfc-135">이 메타패키지에서 일부 패키지는 아직 안정적으로 게시되지 않으므로 `azure` 메타패키지는 아직 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="29cfc-136">하지만 코어 패키지는 코드 품질/완전성 관점에서 현재 "안정적"으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="29cfc-137">가능한 빠른 시간 내에 다른 언어와 동기화되어 공식적으로 레이블 표시될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="29cfc-138">그때까지는 더 이상의 주요 변경 내용은 계획에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="29cfc-139">미리 보기 릴리스 상태이므로 `--pre` 플래그를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="29cfc-140">또는 직접</span><span class="sxs-lookup"><span data-stu-id="29cfc-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="29cfc-141">추가 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="29cfc-141">Getting More Packages</span></span>
<span data-ttu-id="29cfc-142">PyPI([Python 패키지 인덱스][Python Package Index])에서 다양한 Python 라이브러리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="29cfc-143">Distro를 설치하도록 선택했다면 웹 개발 및 기술 컴퓨팅을 포함한 다양한 시나리오에 맞는 거의 모든 흥미로운 기능을 이미 갖추었습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="29cfc-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29cfc-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="29cfc-145">[Python Tools for Visual Studio][Python Tools for Visual Studio](PTVS)는 VS를 완전한 Python IDE로 전환하는 Microsoft의 무료/OSS 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="29cfc-147">PTVS는 선택 사항이지만 Python 및 웹 프로젝트/솔루션 지원, 디버깅, 프로파일링, 대화형 창, 템플릿 편집 및 Intellisense를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="29cfc-148">또한 PTVS를 사용하면 [Cloud Services](cloud-services/cloud-services-python-ptvs.md) 및 [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md) 배포 지원과 함께 Microsoft Azure에 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="29cfc-149">PTVS는 기존 Visual Studio 2013, 2015 또는 2017 설치와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="29cfc-150">설명서, 다운로드 및 토론에 대한 자세한 내용은 [Python Tools for Visual Studio]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29cfc-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="29cfc-151">Linux 및 MacOS용 Python Azure 시나리오</span><span class="sxs-lookup"><span data-stu-id="29cfc-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="29cfc-152">Linux 또는 MacOS의 경우 지원되는 주요 Azure 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="29cfc-153">Python용 클라이언트 라이브러리를 사용하여 Azure 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="29cfc-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="29cfc-154">Linux VM에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="29cfc-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="29cfc-155">Git를 사용하여 개발 및 Azure 웹 사이트에 게시</span><span class="sxs-lookup"><span data-stu-id="29cfc-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="29cfc-156">첫 번째 시나리오에서는 Azure REST API용 Python 래퍼를 통해 [Blob 저장소](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [큐 저장소](storage/queues/storage-python-how-to-use-queue-storage.md), [테이블 저장소](cosmos-db/table-storage-how-to-use-python.md) 등의 Azure PaaS 기능을 활용하는 풍부한 기능의 웹앱을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="29cfc-157">이 기능은 Windows, Mac 및 Linux에서 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="29cfc-158">또한 로컬 개발 컴퓨터 또는 Azure에서 실행되는 Linux VM에서 이러한 클라이언트 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="29cfc-159">VM 시나리오의 경우, 원하는 Linux VM(Ubuntu, CentOS, SUSE)을 시작한 후 원하는 대로 실행하고 관리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="29cfc-160">예를 들어 Windows/Mac/Linux 컴퓨터에서 [IPython][IPython] REPL/notebook을 실행하고 Azure에서 IPython Engine을 실행하는 Linux 또는 Windows 다중 프로세싱 VM으로 브라우저를 가리키면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="29cfc-161">Linux VM을 설정하는 방법에 대한 자세한 내용은 [Linux를 실행하는 가상 컴퓨터 만들기](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="29cfc-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="29cfc-162">Git 배포를 사용하여 Python 웹 응용 프로그램을 개발하고 모든 운영 체제에서 Azure 웹 사이트에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="29cfc-163">Azure에 리포지토리를 푸시할 때 가상 환경이 자동으로 만들어지고 PIP가 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="29cfc-164">Azure Websites 개발 및 게시에 대한 자세한 내용은 [Django를 사용하여 Websites 만들기](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle을 사용하여 Websites 만들기](app-service-web/web-sites-python-create-deploy-bottle-app.md) 및 [Flask를 사용하여 Websites 만들기](app-service-web/web-sites-python-create-deploy-flask-app.md)에 대한 자습서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="29cfc-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="29cfc-165">WSGI 규격 프레임워크 사용에 대한 일반적인 정보는 [Azure Websites를 사용하여 Python 구성](app-service-web/web-sites-python-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29cfc-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="29cfc-166">추가 소프트웨어 및 리소스</span><span class="sxs-lookup"><span data-stu-id="29cfc-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="29cfc-167">Python ReadTheDocs용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="29cfc-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="29cfc-168">Python GitHub용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="29cfc-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="29cfc-169">공식 Python용 Azure 샘플</span><span class="sxs-lookup"><span data-stu-id="29cfc-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="29cfc-170">[지속성 분석 Python 배포][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="29cfc-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="29cfc-171">[Enthought Python 배포][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="29cfc-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="29cfc-172">[ActiveState Python 배포][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="29cfc-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="29cfc-173">[SciPy - Scientific Python 라이브러리 제품군][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="29cfc-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="29cfc-174">[NumPy - Python의 숫자 라이브러리][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="29cfc-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="29cfc-175">[Django 프로젝트 - 완성도 높은 웹 프레임워크/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="29cfc-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="29cfc-176">[IPython - Python용 고급 REPL/Notebook][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="29cfc-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="29cfc-177">[GitHub의 Python Tools for Visual Studio][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="29cfc-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="29cfc-178">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="29cfc-178">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
