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
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Azure에서 Azure VM 만들기, Jupyter 설치 및 Jupyter Notebook 실행
hello [Jupyter 프로젝트](http://jupyter.org), 이전의 hello [IPython 프로젝트](http://ipython.org), 용 도구의 컬렉션을 제공 hello 만들기로 코드 실행을 결합 하는 강력한 대화형 셸을 사용 하 여 과학적 컴퓨팅 라이브 계산 문서입니다. 이러한 노트북 파일에는 임의 텍스트, 수식, 입력 코드, 결과, 그래픽, 비디오를 비롯하여 최신 웹 브라우저에서 표시할 수 있는 기타 모든 미디어가 포함될 수 있습니다. 절대적으로 새 tooPython 하 고 toolearn 원하는 재미, 대화형 환경 또는 일부 심각한 병렬/기술적 컴퓨팅, Jupyter 노트북 hello 최선의 선택은 것입니다.

![스크린 샷](./media/jupyter-notebook/ipy-notebook-spectral.png) 사운드 녹음의를 사용 하 여 SciPy, Matplotlib 패키지 tooanalyze hello 구조입니다.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Jupyter 두 가지 방법: Azure 노트북 또는 사용자 지정 배포
도 사용할 수 있는 서비스를 제공 하는 azure[Jupyter 사용을 즉시 시작 ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)합니다.  Hello Azure 노트북 서비스를 사용 하 여 얻을 수 있습니다 쉽게 액세스 tooJupyter 웹에 액세스할 수 있는 인터페이스 모든 hello 전원을 python 및 많은 해당 라이브러리를 사용 하 여 확장 가능한 컴퓨팅 리소스입니다.  Hello 설치는 hello 서비스에 의해를 처리 하므로 사용자 관리 및 hello 사용자가 구성에 대 한 hello 필요 없이 이러한 리소스를 액세스할 수 있습니다.

Hello 노트북 서비스 시나리오에 대해 작동 하지 않을 경우이 문서는 보여 주는 방법을 toodeploy hello Jupyter 노트북 Microsoft Azure에서 Linux 가상 컴퓨터 (Vm)를 사용 하 여 계속 tooread 하십시오.

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Azure에서 VM 만들기 및 구성
hello 첫 번째 단계는 toocreate Azure에서 실행 되는 가상 컴퓨터 (VM).
이 VM hello 클라우드에서 전체 운영 체제 이며 hello Jupyter 노트북 실행에 사용 됩니다. Azure 가상 컴퓨터, Linux 및 Windows를 실행할 수 있는 이며 Jupyter 두 유형의 가상 컴퓨터에 설치 하는 hello 설명 합니다.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Linux VM을 만들고 Jupyter에 대한 포트 열기
제공 된 hello 지침에 따라 [여기] [ portal-vm-linux] toocreate hello의 가상 컴퓨터 *Ubuntu* 배포 합니다. 이 자습서에서는 Ubuntu Server 14.04 LTS를 사용합니다. 사용자 이름 hello에서는 *azureuser*합니다.

Hello 가상 컴퓨터를 배포한 후 hello 네트워크 보안 그룹에 대 한 보안 규칙을 tooopen이 필요 합니다.  Hello Azure 포털에서에서 이동 너무**네트워크 보안 그룹** 및 hello 보안 그룹이 해당 tooyour VM에 대 한 열기 hello 탭 합니다. 다음 설정을 hello로 tooadd 인바운드 보안 규칙 필요: **TCP** hello 프로토콜에 대 한  **\***  hello 소스 (공용) 포트에 대 한 및 **9999** 에 대 한 hello (개인) 대상 포트입니다.

![스크린샷](./media/jupyter-notebook/azure-add-endpoint.png)

네트워크 보안 그룹에서 클릭 **네트워크 인터페이스** 및 참고 hello **공용 IP 주소** hello 다음 단계에서 필요한 tooconnect tooyour VM 있을 것입니다.

## <a name="install-required-software-on-hello-vm"></a>Hello VM에 필요한 소프트웨어를 설치 합니다.
toorun hello 우리의 VM에서 Jupyter 노트북, Jupyter과 해당 종속성을 설치 해야 했습니다. Ssh를 사용 하 여 tooyour linux vm을 연결 하 고 hello 사용자 이름/암호 쌍을 만들 때 선택한 vm hello 합니다. 이 자습서에서는 PuTTY를 사용하고 Windows에서 연결합니다.

### <a name="installing-jupyter-on-ubuntu"></a>Ubuntu에 Jupyter 설치
Anaconda, 인기 있는 데이터 과학 python 배포는에서 제공 하는 hello 링크 중 하나를 사용 하 여 설치 [Continuum Analytics](https://www.continuum.io/downloads)합니다.  Hello이 문서의 문서를 작성할 당시 아래 링크 hello hello toodate 버전을 가장 됩니다.

#### <a name="anaconda-installs-for-linux"></a>Linux용 Anaconda 설치
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64비트</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64비트</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32비트</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32비트</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Ubuntu에 Anaconda3 2.3.0 64비트 설치
예로 Ubuntu에 Anaconda를 설치하는 방법입니다.

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

### <a name="configuring-jupyter-and-using-ssl"></a>Jupyter 구성 및 SSL 사용
설치한 후 tootake 순간 toosetup hello 구성 파일에 필요한 Jupyter 합니다. Jupyter 구성 문제를 발생 하는 경우는 것이 유용한 toolook hello에 [Jupyter 노트북 서버를 실행 하는 데는 설명서](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)합니다.

다음에서는 `cd` toohello 디렉터리 toocreate 우리의 SSL 인증서를 프로 파일링 하 고 hello 프로필 구성 파일을 편집 합니다.

Linux에서 다음 명령을 hello를 사용 합니다.

    cd ~/.jupyter

명령 toocreate hello SSL 인증서 (Linux 및 Windows)를 수행 하는 hello를 사용 합니다.

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

참고는 이후 생성 자체 서명 된 SSL 인증서를 toohello 노트북을 연결할 때 브라우저에서 보안 경고를 제공 합니다.  장기 프로덕션 용도로 toouse 조직과 연결 된 제대로 서명 된 인증서를 사용 합니다.  이 데모의 hello 범위를 벗어나 인증서 관리 이므로 지금은 tooa 자체 서명 된 인증서 대해서만 했습니다.

또한 toousing 인증서도 제공 해야 암호 tooprotect 전자 필기장을 무단된으로 사용 합니다.  보안상의 이유로 Jupyter 암호를 사용의 구성 파일에 암호화 된 암호 tooencrypt 필요 하므로 먼저 합니다.  IPython 제공 유틸리티 toodo. 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

이 사용자를 입력 한 암호와 확인, 고 hello 암호 다음 인쇄 됩니다. 단계 다음에 나오는 hello에 대 한이 note 합니다.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

다음으로 hello 프로필의 구성 파일을 편집 합니다는 `jupyter_notebook_config.py` hello 디렉터리에 있는 파일입니다.  이 파일이 존재 하지 않을 수 있습니다-참고 hello 그럴 경우 새로 만들 것입니다.  이 파일에는 여러 필드가 포함되어 있으며 기본적으로 모든 필드는 주석 처리되어 있습니다.  원하는 대로의 텍스트 편집기로이 파일을 열 수 있습니다 다음 콘텐츠 이상 hello에 확인 해야 합니다. **Hello 이전 단계의 hello sha1 가진 hello 구성에 있는지 tooreplace hello c.NotebookApp.password 수**합니다.

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

### <a name="run-hello-jupyter-notebook"></a>Jupyter 노트북 hello를 실행 합니다.
이 시점에서 준비 toostart hello Jupyter 노트북 있습니다. toodo이 이동 toohello 디렉터리 toostore 전자 필기장에 원하는 하 고 다음 명령을 hello로 hello Jupyter 노트북 서버를 시작 합니다.

    /anaconda3/bin/jupyter-notebook

이제 해야 수 수 tooaccess hello 주소에서 Jupyter 노트북 `https://[PUBLIC-IP-ADDRESS]:9999`합니다.

전자 필기장을 처음 사용할 때 암호 hello 로그인 페이지를 요구 합니다. 에 로그인 되 고 있습니다 "Jupyter 노트북 대시보드" hello 모든 전자 필기장 작업에 대 한 제어 센터인 합니다.  이 페이지에서 새 노트북을 만들고 기존 노트북을 열 수 있습니다.

![스크린샷](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Hello Jupyter 노트북을 사용 하 여
Hello를 누르면 **새로** 단추, 시작 페이지를 수행 하는 hello 표시 됩니다.

![스크린샷](./media/jupyter-notebook/jupyter-untitled-notebook.png)

hello 영역으로 표시는 `In []:` hello 입력된 영역 프롬프트는 여기서 모든 유효한 Python 코드를 입력할 수 있습니다 및에 도달 하면 실행 될 `Shift-Enter` 하거나 hello "재생" 아이콘 (hello 오른쪽 방향 삼각형 hello 도구 모음에서)를 클릭 합니다.

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>강력한 패러다임: 다양한 미디어를 지원하는 라이브 컴퓨팅 문서
자체 hello 노트북에에서 있기 때문에 몇 가지 방법 모두의 혼합 매우 자연 tooanyone Python 및 워드 프로세서 사용 경험이 있어야: Python 코드 블록을 실행할 수 있지만 너무 "코드"에서 셀의 hello 스타일을 변경 하 여 정보 및 기타 텍스트를 유지할 수도 있습니다 "Ma rkdown "hello 드롭다운 메뉴를 사용 하 여 도구 모음에서 합니다.

Jupyter는 컴퓨팅 및 다양한 미디어(텍스트, 그래픽, 비디오 및 최신 웹 브라우저에서 표시할 수 있는 모든 것)의 결합을 허용하므로 워드 프로세서보다 훨씬 많은 기능을 제공합니다. 텍스트, 코드, 동영상 및 더 많은 것을 혼합할 수 있습니다.

![스크린샷](./media/jupyter-notebook/jupyter-editing-experience.png)

있고 과학 및 기술 컴퓨팅, 다음 스크린 샷에서 hello에 Python의 많은 뛰어난 라이브러리의 전원이 hello 간단한 계산을 수행할 수 있는 한 환경에서 모든을 복잡 한 네트워크 분석으로 쉽게 동일 hello로 합니다.

이러한 패러다임 hello 최신 웹의 hello 전원 라이브 계산와 혼합의 다양 한 비즈니스 가능성이 제공 하 고 hello 클라우드;에 가장 적합 hello 노트북을 사용할 수 있습니다.

* 예비는 계산 잠깐 보관 함 toorecord로 문제에 작동 합니다.
* tooshare 하드 카피 형식 (HTML, PDF) 또는 '라이브' 계산 폼에 동료와 결과입니다.
* toodistribute 및 학생 hello 실제 코드를 시험해 볼 즉시 수 있으므로 계산을 포함 하는 현재 라이브 교육 자료에는 수정 하 고 다시 대화형으로 실행 합니다.
* hello 연구 결과에 즉시 재현 될 수 있는 방식으로 제공 하는 "실행 파일 논문" tooprovide 유효성을 검사 하 고 다른 사용자가 확장.
* 공동 컴퓨팅 플랫폼으로 서: 여러 사용자가 로그인 할 수 toothe 동일 노트북 서버 tooshare 라이브 계산 세션을 합니다.

Toohello IPython 소스 코드를 이동 하는 경우 [리포지토리][repository], 노트북 예제를 다운로드 하 고 다음 사용해 자신의 Azure Jupyter vm 수와 전체 디렉터리를 찾을 수 있습니다.  Hello 다운로드 `.ipynb` 파일 hello에서 사이트 및 전자 필기장 Azure VM의 hello 대시보드에 업로드 (또는 hello VM에 직접 다운로드할).

## <a name="conclusion"></a>결론
hello Jupyter 노트북 대화형으로 Azure에서 Python 생태계 hello의 hello 전원에 액세스 하기 위한 강력한 인터페이스를 제공 합니다.  이 인터페이스는 간단한 Python 탐색 및 학습, 데이터 분석 및 시각화, 시뮬레이션, 병렬 컴퓨팅 등 다양한 사용 사례를 처리합니다. hello 결과 노트북 문서 hello 계산을 수행 되 고 다른 Jupyter 사용자와 공유할 수 있는 완전 한 레코드를 포함 합니다.  Azure에서 클라우드 배포에 가장 적합 하지만 hello Jupyter 노트북 로컬 응용 프로그램으로 사용할 수 있습니다.

Jupyter의 hello 핵심 기능을 통해 Visual Studio 내에서 사용할 수는는 [Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS는 Microsoft의 무료 오픈 소스 플러그 인으로, IntelliSense, 디버깅, 프로파일링, 병렬 컴퓨팅 통합 등 고급 편집기 기능을 포함하는 고급 Python 개발 환경으로 Visual Studio를 전환해 줍니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
