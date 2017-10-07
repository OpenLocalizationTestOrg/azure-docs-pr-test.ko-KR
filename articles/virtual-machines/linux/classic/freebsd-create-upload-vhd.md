---
title: "aaaCreate 및 업로드 FreeBSD VM 이미지 | Microsoft Docs"
description: "Toocreate 알아보고 hello FreeBSD 운영 체제 toocreate Azure 가상 컴퓨터를 포함 하는 가상 하드 디스크 (VHD)를 업로드 합니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>만들기 및 업로드 FreeBSD VHD tooAzure
이 문서에서는 어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello FreeBSD 운영 체제입니다. 를 업로드 한 후에 사용자 고유의 이미지 toocreate Azure에서 가상 컴퓨터 (VM)으로 사용할 수 있습니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Hello 리소스 관리자 모델을 사용 하 여 VHD를 업로드 하는 방법에 대 한 내용은 [여기](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="prerequisites"></a>필수 조건
이 문서에서는 다음 항목 hello 있다고 가정 합니다.

* **Azure 구독**- 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다. MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요. 그렇지 않은 경우 너무 방법을 알아보려면[무료 평가판 계정을 만들](https://azure.microsoft.com/pricing/free-trial/)합니다.  
* **Azure PowerShell 도구**-hello Azure PowerShell 모듈을 설치 해야 하 고 toouse Azure 구독을 구성 합니다. toodownload hello 모듈 참조 [Azure 다운로드](https://azure.microsoft.com/downloads/)합니다. 에 대해 설명 하는 자습서는 어떻게 tooinstall 구성 및 여기 hello 모듈을 사용할 수 있습니다. 사용 하 여 hello [Azure 다운로드](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD입니다.
* **.Vhd 파일에 설치 된 FreeBSD 운영 체제**tooa 가상 하드 디스크-는 FreeBSD 운영 체제에서 지원 되는 설치 합니다. 여러 도구 toocreate.vhd 파일을 포함 합니다. 예를 들어 Hyper-v toocreate hello.vhd 파일 등 가상화 솔루션을 사용 하 고 hello 운영 체제를 설치할 수 있습니다. Tooinstall 및 Hyper-v를 사용 하 여 참조 하는 방법에 대 한 지침은 [Hyper-v 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)합니다.

> [!NOTE]
> Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다. Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 cmdlet hello 수 [convert vhd](https://technet.microsoft.com/library/hh848454.aspx)합니다. 또한는 [방법에 대 한 MSDN에서 자습서 toouse hyper-v FreeBSD](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)합니다.
>
>

이 태스크는 다섯 단계를 수행 하는 hello를 포함 합니다.

## <a name="step-1-prepare-hello-image-for-upload"></a>1 단계: 업로드에 대 한 hello 이미지 준비
Hello FreeBSD 운영 체제를 설치한 hello 가상 컴퓨터에서 다음 절차를 수행 하는 hello를 완료 합니다.

1. DHCP를 활성화합니다.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. SSH를 활성화합니다.

    해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다. FreeBSD 디스크에서 설치 후에는 기본적으로 사용하도록 설정되어 있습니다. 
3. 직렬 콘솔을 설치합니다.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. sudo를 설치합니다.

    Azure의 hello 루트 계정이 비활성화 되었습니다. 즉, tooutilize sudo 상승 된 권한으로는 권한 없는 사용자 toorun 명령에서 필요 합니다.

        # pkg install sudo
   
5. Azure 에이전트에 대한 필수 조건.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Azure 에이전트를 설치합니다.

    hello hello Azure 에이전트의 최신 릴리스에 항상에 있습니다 [github](https://github.com/Azure/WALinuxAgent/releases)합니다. 버전 2.0.10 hello + FreeBSD & 10.1, 버전과 10 hello 2.1.4 + (2.2. x 포함) 정식으로 지 원하는 FreeBSD 10.2 및 이상 릴리스를 공식적으로 지원 합니다.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    2.0의 경우 2.0.16을 예로 사용하겠습니다.

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    2.1의 경우 2.1.4를 예로 사용하겠습니다.

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Azure 에이전트를 설치한 후 실행 하는 것이 좋습니다 tooverify 됩니다.
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Hello 시스템을 프로 비전 해제 합니다.

    프로 비전 해제 하 고 확인 시스템 tooclean hello 다시 프로 비전에 대 한 적합 한 것입니다. hello 다음 명령은 삭제 hello 마지막 프로 비전 된 사용자 계정과 연결 된 hello 데이터:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    이제 VM을 종료할 수 있습니다.

## <a name="step-2-create-a-storage-account-in-azure"></a>2단계: Azure에서 저장소 계정 만들기
사용 되는 toocreate 가상 컴퓨터를 사용할 수 있도록 해야 Azure tooupload.vhd 파일의에서 저장소 계정. Hello Azure 클래식 포털 toocreate 저장소 계정 사용할 수 있습니다.

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 명령 모음에서 선택 **새로**합니다.
3. **데이터 서비스** > **저장소** > **빠른 생성**을 선택합니다.

    ![저장소 계정 빠른 생성](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Hello 필드를 다음과 같이 입력 합니다.

   * Hello에 **URL** 필드 hello 저장소 계정 URL에 하위 도메인 이름 toouse를 입력 합니다. hello 항목 3 ~ 24 숫자 및 소문자에서 포함할 수 있습니다. 이 이름은 사용 되는 tooaddress Azure Blob 저장소, Azure 큐 저장소 또는 Azure 테이블 저장소 리소스 hello 구독에 대 한 hello URL에서 hello 호스트 이름이 됩니다.
   * Hello에 **위치/선호도 그룹** 드롭 다운 메뉴에서 선택 hello **위치 또는 선호도 그룹** hello 저장소 계정에 대 한 합니다. 선호도 그룹 hello에 클라우드 서비스 및 저장소를 배치 하면 동일한 데이터 센터입니다.
   * Hello에 **복제** 필드, 결정 여부 toouse **지리적 중복** hello 저장소 계정에 대 한 복제 합니다. 지역에서 복제는 기본적으로 설정되어 있습니다. 이 옵션에 데이터 tooa 보조 위치에 없는 비용 tooyou 복제, hello 기본 위치의 저장소 장애 toothat 위치 하는 경우 오류가 발생 한 조치를 발생 합니다. hello 보조 위치는 자동으로 할당 됩니다 및 변경할 수 없습니다. 기한 toolegal 요구 사항 또는 조직 구성 정책에 클라우드 기반 저장소의 hello 위치 보다 자세히 제어 해야 할 경우 지리적 복제를 해제할 수 있습니다. 그러나 수는 나중에 지리적 복제를 설정 하는 경우 청구 됩니다 일회성 데이터 전송 요금이 tooreplicate 기존 데이터 toohello 보조 위치입니다. 지역에서 복제를 사용하지 않는 저장소 서비스는 할인하여 제공됩니다. 저장소 계정의 지역에서 복제를 관리하는 방법에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/common/storage-redundancy.md)에서 확인할 수 있습니다.

     ![저장소 계정 세부 정보 입력](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. **저장소 계정 만들기**를 선택합니다. hello 계정 아래에 **저장소**합니다.

    ![저장소 계정을 성공적으로 만들었음](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. 다음으로 업로드된 .vhd 파일의 컨테이너를 만듭니다. Hello 저장소 계정 이름을 선택한 다음 선택 **컨테이너**합니다.

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. **컨테이너 만들기**를 선택합니다.

    ![저장소 계정 세부 정보](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. Hello에 **이름** 필드 컨테이너에 대 한 이름을 입력 합니다. 그런 다음, hello **액세스** 드롭 다운 메뉴에서 원하는 액세스 정책의 형식입니다.

    ![컨테이너 이름](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > 기본적으로 hello 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다. tooallow 공용 읽기 액세스 권한을 toohello blob을 hello 컨테이너 하지만 하지 toohello 컨테이너 속성과 메타 데이터를 사용 하 여 hello **공용 Blob** 옵션입니다. hello 컨테이너 및 blob를 사용 하 여 hello tooallow 전체 공용 읽기 권한 **공용 컨테이너** 옵션입니다.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>3 단계: hello 연결 tooAzure 준비
.Vhd 파일을 업로드 하려면 먼저 컴퓨터와 Azure 구독 간에 tooestablish 보안 연결이 필요 합니다. Hello Azure Active Directory (Azure AD) 메서드를 사용 하거나 인증서 메서드 toodo hello 것입니다.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Azure AD hello 메서드 tooupload.vhd 파일을 사용 하 여
1. Azure PowerShell 콘솔을 열고 hello 합니다.
2. Hello 다음 명령을 입력 합니다.  
    `Add-AzureAccount`

    이 명령은 직장 또는 학교 계정으로 로그인할 수 있는 로그인 창을 엽니다.

    ![PowerShell 창](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure를 인증 하 고 hello 자격 증명 정보를 저장 합니다. Hello 창이 닫힙니다.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Hello 인증서 메서드 tooupload.vhd 파일을 사용 하 여
1. Azure PowerShell 콘솔을 열고 hello 합니다.
2. 입력: `Get-AzurePublishSettingsFile`
3. 브라우저 창이 열리고 toodownload hello.publishsettings 제출 하 라는 메시지를 표시 합니다. 이 파일에는 Azure 구독에 대한 정보와 인증서가 포함되어 있습니다.

    ![브라우저 다운로드 페이지](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Hello.publishsettings 파일을 저장 합니다.
5. 형식: `Import-AzurePublishSettingsFile <PathToFile>`여기서 `<PathToFile>` hello toohello.publishsettings 파일 전체 경로입니다.

   자세한 내용은 [Azure Cmdlets 시작](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)을 참조하세요.

   설치 하 고 PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="step-4-upload-hello-vhd-file"></a>4 단계: hello.vhd 파일 업로드
Hello.vhd 파일을 업로드 하는 경우 Blob 저장소 내의 아무 곳 이나 배치할 수 있습니다. 다음은 몇 가지 용어 hello 파일을 업로드할 때 사용 합니다.

* **BlobStorageURL** 2 단계에서에서 만든 hello 저장소 계정에 대 한 hello URL입니다.
* **YourImagesFolder** 은 Blob 저장소 내의 컨테이너 hello toostore 이미지입니다.
* **VHDName** hello Azure 클래식 포털 tooidentify hello 가상 하드 디스크에 표시 되는 hello 레이블입니다.
* **PathToVHDFile** hello 전체 경로 및 hello.vhd 파일의 이름입니다.

Hello 이전 단계에서 사용한 hello Azure PowerShell 창에서 다음을 입력 합니다.

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>5 단계: hello 업로드 한.vhd 파일로 VM 만들기
Hello.vhd 파일을 업로드 한 후에 구독에 연결 되며이 사용자 지정 이미지와 가상 컴퓨터를 만들 수 있는 사용자 지정 이미지의 이미지 toohello 목록으로 추가할 수 있습니다.

1. Hello 이전 단계에서 사용한 hello Azure PowerShell 창에서 다음을 입력 합니다.

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Linux를 사용 하 여 hello OS 유형으로. 현재 Azure PowerShell 버전 hello "Linux" 또는 "Windows" 매개 변수로 허용합니다.
   >
   >
2. Hello를 선택 하면 hello 새 이미지를 나열 된 hello 이전 단계를 완료 한 후 **이미지** hello Azure 클래식 포털에 탭 합니다.  

    ![이미지 선택](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Hello 갤러리에서 가상 컴퓨터를 만듭니다. 이제 **내 이미지**에서 이 새 이미지를 사용할 수 있습니다.
4. Hello 새 이미지를 선택 합니다. 다음으로 hello 메시지 tooset 호스트 이름, 암호, SSH 키를 통해 이동 합니다.

    ![사용자 지정 이미지](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Hello를 프로 비전을 완료 한 후에 Azure에서 실행 중인 FreeBSD VM 표시 됩니다.

    ![Azure의 FreeBSD 이미지](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
