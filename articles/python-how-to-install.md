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
# <a name="installing-python-and-hello-sdk"></a>Python 및 hello SDK 설치
Python을 쉽게 tooset를 Windows 켜져 있고, Linux, Mac에 미리 설치 되어 나오는 및 [Windows 용를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about)합니다. 이 가이드에서는 설치 및 Azure와 함께 사용할 수 있도록 컴퓨터를 설정하는 작업을 단계별로 안내합니다.

## <a name="whats-in-hello-python-azure-sdk"></a>작업은에 hello Python Azure SDK?
Python 용 Azure SDK hello toodevelop 사용 하면 배포 하 고 Azure에 대 한 Python 응용 프로그램을 관리 하는 구성 요소를 포함 합니다. 특히, Python 용 Azure SDK hello hello 다음이 포함 됩니다.

* **관리 라이브러리**. 이러한 클래스 라이브러리는 저장소, 계정, 가상 컴퓨터와 같은 Azure 리소스를 관리하는 인터페이스를 제공합니다.
* **런타임 라이브러리**. 이러한 클래스 라이브러리는 저장소 및 서비스 버스와 같은 Azure 기능에 액세스하는 인터페이스를 제공합니다.

## <a name="which-python-and-which-version-toouse"></a>Python 및 어떤 버전 toouse
사용할 수 있는 몇 가지의 Python 인터프리터 옵션이 있으며 다음을 예로 들 수 있습니다.

* CPython-hello 표준 및 가장 자주 사용 되는 Python 인터프리터
* PyPy-규정을 준수 하는 빠른 대체 구현 tooCPython
* IronPython - .Net/CLR에서 실행되는 Python 인터프리터
* Jython-hello Java 가상 컴퓨터에서 실행 되는 Python 인터프리터

**CPython** v2.7 또는 v3.3 + 및 PyPy 5.4.0 테스트 되 고 hello Python Azure SDK에 대 한 지원.

## <a name="where-tooget-python"></a>여기서 tooget Python?
여러 가지 방법으로 tooget CPython 가지가 있습니다.

* [www.python.org][www.python.org]에서 직접
* [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] 또는 [www.activestate.com][www.activestate.com]과 같은 신뢰할 수 있는 배포자로부터
* 원본에서 빌드

특별히 필요한 경우가 hello 처음 두 가지 옵션 권장 합니다.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Windows, Linux 및 MacOS에 SDK 설치(클라이언트 라이브러리만 해당)
Python 설치를 이미 있는 경우에 pip tooinstall 기존 Python 2.7 또는 Python 3.3 + 환경에서 모든 hello 클라이언트 라이브러리의 번들을 사용할 수 있습니다. Hello에서 hello 패키지를 다운로드이 [Python 패키지 인덱스] [ Python Package Index] (PyPI).

관리자 권한이 필요할 수 있습니다.

* Linux와 MacOS 등 hello를 사용 하 여 `sudo` 명령: `sudo pip install azure-mgmt-compute`합니다.
* Windows: 관리자로 PowerShell/명령 프롬프트를 엽니다.

각 Azure 서비스에 대한 각 라이브러리를 개별적으로 설치할 수 있습니다.

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Hello를 사용 하 여 미리 보기 패키지를 설치할 수 있습니다 `--pre` 플래그:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Hello를 사용 하 여 한 줄에 Azure 라이브러리의 집합을 설치할 수도 있습니다 `azure` 메타 패키지입니다. 이 메타 패키지의 모든 패키지를 아직 안정적으로 게시 됩니다. 이후 hello `azure` 메타 패키지는 아직 미리 보기 상태입니다.
그러나 코드 품질/완결성 관점에서 hello 코어 패키지 간주할 수 "안정적인"이 이번에

* 가능한 빠른 시간 내에 다른 언어와 동기화되어 공식적으로 레이블 표시될 예정입니다.
  그때까지는 더 이상의 주요 변경 내용은 계획에 없습니다.

Toouse hello 필요 미리 보기 버전 이므로 `--pre` 플래그:

```console
   $ pip install --pre azure
```

또는 직접

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>추가 패키지 가져오기
hello [Python 패키지 인덱스] [ Python Package Index] (PyPI)에 Python 라이브러리의 풍부한 선택 합니다.  대부분의 웹 개발 tooTechnical에서 다양 한 시나리오에 대 한 비트 흥미로운 hello 이미 해야 tooinstall는 배포판을 선택한 경우 컴퓨팅입니다.

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
[Python Tools for Visual Studio][Python Tools for Visual Studio](PTVS)는 VS를 완전한 Python IDE로 전환하는 Microsoft의 무료/OSS 플러그 인입니다.

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

PTVS는 선택 사항이지만 Python 및 웹 프로젝트/솔루션 지원, 디버깅, 프로파일링, 대화형 창, 템플릿 편집 및 Intellisense를 제공합니다.

PTVS을 사용 하면 쉽게 toodeploy tooMicrosoft Azure 배포에 대 한 지원과 함께 너무[클라우드 서비스](cloud-services/cloud-services-python-ptvs.md) 및 [웹 사이트](app-service-web/web-sites-python-ptvs-django-mysql.md)합니다.

PTVS는 기존 Visual Studio 2013, 2015 또는 2017 설치와 작동합니다.  설명서, 다운로드 및 토론에 대한 자세한 내용은 [Python Tools for Visual Studio]를 참조하세요.  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Linux 및 MacOS용 Python Azure 시나리오
Linux 또는 MacOS의 경우 지원되는 주요 Azure 시나리오는 다음과 같습니다.

1. Python 용 hello 클라이언트 라이브러리를 사용 하 여 Azure 서비스 사용
2. Linux VM에서 앱 실행
3. 개발 하 고 tooAzure 웹 사이트 게시 Git를 사용 하 여

hello 첫 번째 시나리오를 활용 하는 hello의 Azure PaaS 기능와 같은 tooauthor 풍부한 웹 앱을 사용 하면 [blob 저장소](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [큐 저장소](storage/queues/storage-python-how-to-use-queue-storage.md), [테이블 저장소](cosmos-db/table-storage-how-to-use-python.md) hello Azure REST Api에 대 한 Pythonic 래퍼를 통해 등입니다. 이 기능은 Windows, Mac 및 Linux에서 동일하게 작동합니다.  또한 로컬 개발 컴퓨터 또는 Azure에서 실행되는 Linux VM에서 이러한 클라이언트 라이브러리를 사용할 수 있습니다.

Hello VM 시나리오의 경우 단순히 (Ubuntu, CentOS, Suse) 선택한 Linux VM을 시작 했으며 어떤 점이 좋은지 실행/관리  예를 들어, 실행할 수 있습니다 [IPython] [ IPython] REPL/노트북 Linux/Windows/Mac 컴퓨터와 브라우저 tooa Linux 또는 Windows 다중 프로세서 VM 실행 중에 Azure에서 IPython 엔진 hello 지점입니다.

방법에 대 한 Linux VM을 tooset 참조 hello [는 Linux 가상 컴퓨터 실행을 만들](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 자습서입니다.

Git 배포를 사용 하 여 Python 웹 응용 프로그램을 개발 하 고 운영 체제에서 tooan Azure 웹 사이트를 게시할 수 있습니다.  리포지토리 tooAzure 푸시할 때 자동으로 가상 환경을 만듭니다 및 pip 필요한 패키지를 설치 합니다.

개발 및 Azure 웹 사이트를 게시에 대 한 자세한 내용은 참조에 대 한 hello 자습서 [Django로 웹 사이트를 만드는](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle로 웹 사이트를 만드는](app-service-web/web-sites-python-create-deploy-bottle-app.md), 및 [로 웹 사이트 만들기 플라스](app-service-web/web-sites-python-create-deploy-flask-app.md)합니다. WSGI 규격 프레임워크 사용에 대한 일반적인 정보는 [Azure Websites를 사용하여 Python 구성](app-service-web/web-sites-python-configure.md)을 참조하세요.

## <a name="additional-software-and-resources"></a>추가 소프트웨어 및 리소스
* [Python ReadTheDocs용 Azure SDK](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Python GitHub용 Azure SDK](https://github.com/Azure/azure-sdk-for-python)
* [공식 Python용 Azure 샘플](https://azure.microsoft.com/documentation/samples/?platform=python)
* [지속성 분석 Python 배포][Continuum Analytics Python Distribution]
* [Enthought Python 배포][Enthought Python Distribution]
* [ActiveState Python 배포][ActiveState Python Distribution]
* [SciPy - Scientific Python 라이브러리 제품군][SciPy - A suite of Scientific Python libraries]
* [NumPy - Python의 숫자 라이브러리][NumPy - A numerics library for Python]
* [Django 프로젝트 - 완성도 높은 웹 프레임워크/CMS][Django Project - A mature web framework/CMS]
* [IPython - Python용 고급 REPL/Notebook][IPython - an advanced REPL/Notebook for Python]
* [GitHub의 Python Tools for Visual Studio][Python Tools for Visual Studio on GitHub]
* [Python 개발자 센터](/develop/python/)

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
