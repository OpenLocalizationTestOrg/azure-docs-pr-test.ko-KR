---
title: "aaaInstall Python 및 Azure SDK-hello"
description: "자세한 내용은 방법 azure tooinstall Python 및 hello SDK toouse 합니다."
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
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="01bb3-103">Python 및 hello SDK 설치</span><span class="sxs-lookup"><span data-stu-id="01bb3-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="01bb3-104">Python을 쉽게 tooset를 Windows 켜져 있고, Linux, Mac에 미리 설치 되어 나오는 및 [Windows 용를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="01bb3-105">이 가이드에서는 설치 및 Azure와 함께 사용할 수 있도록 컴퓨터를 설정하는 작업을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="01bb3-106">작업은에 hello Python Azure SDK?</span><span class="sxs-lookup"><span data-stu-id="01bb3-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="01bb3-107">Python 용 Azure SDK hello toodevelop 사용 하면 배포 하 고 Azure에 대 한 Python 응용 프로그램을 관리 하는 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="01bb3-108">특히, Python 용 Azure SDK hello hello 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="01bb3-109">**관리 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="01bb3-109">**Management libraries**.</span></span> <span data-ttu-id="01bb3-110">이러한 클래스 라이브러리는 저장소, 계정, 가상 컴퓨터와 같은 Azure 리소스를 관리하는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="01bb3-111">**런타임 라이브러리**.</span><span class="sxs-lookup"><span data-stu-id="01bb3-111">**Runtime libraries**.</span></span> <span data-ttu-id="01bb3-112">이러한 클래스 라이브러리는 저장소 및 서비스 버스와 같은 Azure 기능에 액세스하는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="01bb3-113">Python 및 어떤 버전 toouse</span><span class="sxs-lookup"><span data-stu-id="01bb3-113">Which Python and which version toouse</span></span>
<span data-ttu-id="01bb3-114">사용할 수 있는 몇 가지의 Python 인터프리터 옵션이 있으며 다음을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="01bb3-115">CPython-hello 표준 및 가장 자주 사용 되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="01bb3-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="01bb3-116">PyPy-규정을 준수 하는 빠른 대체 구현 tooCPython</span><span class="sxs-lookup"><span data-stu-id="01bb3-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="01bb3-117">IronPython - .Net/CLR에서 실행되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="01bb3-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="01bb3-118">Jython-hello Java 가상 컴퓨터에서 실행 되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="01bb3-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="01bb3-119">**CPython** v2.7 또는 v3.3 + 및 PyPy 5.4.0 테스트 되 고 hello Python Azure SDK에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="01bb3-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="01bb3-120">여기서 tooget Python?</span><span class="sxs-lookup"><span data-stu-id="01bb3-120">Where tooget Python?</span></span>
<span data-ttu-id="01bb3-121">여러 가지 방법으로 tooget CPython 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="01bb3-122">[www.python.org][www.python.org]에서 직접</span><span class="sxs-lookup"><span data-stu-id="01bb3-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="01bb3-123">[www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] 또는 [www.activestate.com][www.activestate.com]과 같은 신뢰할 수 있는 배포자로부터</span><span class="sxs-lookup"><span data-stu-id="01bb3-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="01bb3-124">원본에서 빌드</span><span class="sxs-lookup"><span data-stu-id="01bb3-124">Build from source!</span></span>

<span data-ttu-id="01bb3-125">특별히 필요한 경우가 hello 처음 두 가지 옵션 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="01bb3-126">Windows, Linux 및 MacOS에 SDK 설치(클라이언트 라이브러리만 해당)</span><span class="sxs-lookup"><span data-stu-id="01bb3-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="01bb3-127">Python 설치를 이미 있는 경우에 pip tooinstall 기존 Python 2.7 또는 Python 3.3 + 환경에서 모든 hello 클라이언트 라이브러리의 번들을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="01bb3-128">Hello에서 hello 패키지를 다운로드이 [Python 패키지 인덱스] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="01bb3-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="01bb3-129">관리자 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-129">You may need administrator rights:</span></span>

* <span data-ttu-id="01bb3-130">Linux와 MacOS 등 hello를 사용 하 여 `sudo` 명령: `sudo pip install azure-mgmt-compute`합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="01bb3-131">Windows: 관리자로 PowerShell/명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="01bb3-132">각 Azure 서비스에 대한 각 라이브러리를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="01bb3-133">Hello를 사용 하 여 미리 보기 패키지를 설치할 수 있습니다 `--pre` 플래그:</span><span class="sxs-lookup"><span data-stu-id="01bb3-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="01bb3-134">Hello를 사용 하 여 한 줄에 Azure 라이브러리의 집합을 설치할 수도 있습니다 `azure` 메타 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="01bb3-135">이 메타 패키지의 모든 패키지를 아직 안정적으로 게시 됩니다. 이후 hello `azure` 메타 패키지는 아직 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="01bb3-136">그러나 코드 품질/완결성 관점에서 hello 코어 패키지 간주할 수 "안정적인"이 이번에</span><span class="sxs-lookup"><span data-stu-id="01bb3-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="01bb3-137">가능한 빠른 시간 내에 다른 언어와 동기화되어 공식적으로 레이블 표시될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="01bb3-138">그때까지는 더 이상의 주요 변경 내용은 계획에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="01bb3-139">Toouse hello 필요 미리 보기 버전 이므로 `--pre` 플래그:</span><span class="sxs-lookup"><span data-stu-id="01bb3-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="01bb3-140">또는 직접</span><span class="sxs-lookup"><span data-stu-id="01bb3-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="01bb3-141">추가 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="01bb3-141">Getting More Packages</span></span>
<span data-ttu-id="01bb3-142">hello [Python 패키지 인덱스] [ Python Package Index] (PyPI)에 Python 라이브러리의 풍부한 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="01bb3-143">대부분의 웹 개발 tooTechnical에서 다양 한 시나리오에 대 한 비트 흥미로운 hello 이미 해야 tooinstall는 배포판을 선택한 경우 컴퓨팅입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="01bb3-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01bb3-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="01bb3-145">[Python Tools for Visual Studio][Python Tools for Visual Studio](PTVS)는 VS를 완전한 Python IDE로 전환하는 Microsoft의 무료/OSS 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="01bb3-147">PTVS는 선택 사항이지만 Python 및 웹 프로젝트/솔루션 지원, 디버깅, 프로파일링, 대화형 창, 템플릿 편집 및 Intellisense를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="01bb3-148">PTVS을 사용 하면 쉽게 toodeploy tooMicrosoft Azure 배포에 대 한 지원과 함께 너무[클라우드 서비스](cloud-services/cloud-services-python-ptvs.md) 및 [웹 사이트](app-service-web/web-sites-python-ptvs-django-mysql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="01bb3-149">PTVS는 기존 Visual Studio 2013, 2015 또는 2017 설치와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="01bb3-150">설명서, 다운로드 및 토론에 대한 자세한 내용은 [Python Tools for Visual Studio]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01bb3-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="01bb3-151">Linux 및 MacOS용 Python Azure 시나리오</span><span class="sxs-lookup"><span data-stu-id="01bb3-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="01bb3-152">Linux 또는 MacOS의 경우 지원되는 주요 Azure 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="01bb3-153">Python 용 hello 클라이언트 라이브러리를 사용 하 여 Azure 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="01bb3-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="01bb3-154">Linux VM에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="01bb3-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="01bb3-155">개발 하 고 tooAzure 웹 사이트 게시 Git를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="01bb3-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="01bb3-156">hello 첫 번째 시나리오를 활용 하는 hello의 Azure PaaS 기능와 같은 tooauthor 풍부한 웹 앱을 사용 하면 [blob 저장소](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [큐 저장소](storage/queues/storage-python-how-to-use-queue-storage.md), [테이블 저장소](cosmos-db/table-storage-how-to-use-python.md) hello Azure REST Api에 대 한 Pythonic 래퍼를 통해 등입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="01bb3-157">이 기능은 Windows, Mac 및 Linux에서 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="01bb3-158">또한 로컬 개발 컴퓨터 또는 Azure에서 실행되는 Linux VM에서 이러한 클라이언트 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="01bb3-159">Hello VM 시나리오의 경우 단순히 (Ubuntu, CentOS, Suse) 선택한 Linux VM을 시작 했으며 어떤 점이 좋은지 실행/관리</span><span class="sxs-lookup"><span data-stu-id="01bb3-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="01bb3-160">예를 들어, 실행할 수 있습니다 [IPython] [ IPython] REPL/노트북 Linux/Windows/Mac 컴퓨터와 브라우저 tooa Linux 또는 Windows 다중 프로세서 VM 실행 중에 Azure에서 IPython 엔진 hello 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="01bb3-161">방법에 대 한 Linux VM을 tooset 참조 hello [는 Linux 가상 컴퓨터 실행을 만들](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="01bb3-162">Git 배포를 사용 하 여 Python 웹 응용 프로그램을 개발 하 고 운영 체제에서 tooan Azure 웹 사이트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="01bb3-163">리포지토리 tooAzure 푸시할 때 자동으로 가상 환경을 만듭니다 및 pip 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="01bb3-164">개발 및 Azure 웹 사이트를 게시에 대 한 자세한 내용은 참조에 대 한 hello 자습서 [Django로 웹 사이트를 만드는](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle로 웹 사이트를 만드는](app-service-web/web-sites-python-create-deploy-bottle-app.md), 및 [로 웹 사이트 만들기 플라스](app-service-web/web-sites-python-create-deploy-flask-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01bb3-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="01bb3-165">WSGI 규격 프레임워크 사용에 대한 일반적인 정보는 [Azure Websites를 사용하여 Python 구성](app-service-web/web-sites-python-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01bb3-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="01bb3-166">추가 소프트웨어 및 리소스</span><span class="sxs-lookup"><span data-stu-id="01bb3-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="01bb3-167">Python ReadTheDocs용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="01bb3-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="01bb3-168">Python GitHub용 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="01bb3-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="01bb3-169">공식 Python용 Azure 샘플</span><span class="sxs-lookup"><span data-stu-id="01bb3-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="01bb3-170">[지속성 분석 Python 배포][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="01bb3-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="01bb3-171">[Enthought Python 배포][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="01bb3-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="01bb3-172">[ActiveState Python 배포][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="01bb3-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="01bb3-173">[SciPy - Scientific Python 라이브러리 제품군][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="01bb3-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="01bb3-174">[NumPy - Python의 숫자 라이브러리][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="01bb3-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="01bb3-175">[Django 프로젝트 - 완성도 높은 웹 프레임워크/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="01bb3-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="01bb3-176">[IPython - Python용 고급 REPL/Notebook][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="01bb3-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="01bb3-177">[GitHub의 Python Tools for Visual Studio][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="01bb3-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="01bb3-178">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="01bb3-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
