---
title: "StorSimple 가상 배열에 대 한 필수 구성 요소 aaaPortal | Microsoft Docs"
description: "첫 번째 자습서 toodeploy StorSimple 가상 배열 hello Azure 포털을 준비가 포함"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>StorSimple 가상 배열 배포-hello Azure 포털 준비

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>개요

이 hello 첫 번째 문서 hello 시리즈의 필요한 배포 자습서 toocompletely hello 리소스 관리자 모델을 사용 하는 iSCSI 서버나 파일 서버와 가상 배열을 배포 합니다. 이 문서는 hello 요구 하는 toocreate에 설명 하 고 실행 하 여 StorSimple 장치 관리자 서비스 이전 tooprovisioning 가상 배열을 구성 합니다. 이 문서는 때도 tooa 배포 필수 구성 검사 목록 및 구성 요소 out 연결합니다.

관리자는 권한이 toocomplete hello 설정 및 구성 프로세스를 필요합니다. 시작 하기 전에 hello 배포 구성 검사 목록 검토 하는 것이 좋습니다. hello 포털 준비 보다 작은 10 분이 걸립니다.

이 문서에 게시 된 hello 정보 toohello hello Azure 포털에서에서 StorSimple 가상 배열 및 Microsoft Azure Government 클라우드 배포를 적용 합니다.

### <a name="get-started"></a>시작
hello 배포 워크플로 hello 포털을 준비 하 고, 가상화 된 환경의 가상 배열 프로 비전, hello 설치 완료 이루어져 있습니다. 파일 서버 또는 iSCSI 서버로 hello StorSimple 가상 배열 배포 시작 tooget, 벡터 리소스 다음 toorefer toohello가 필요 합니다.

#### <a name="deployment-articles"></a>배포 문서

toodeploy StorSimple 가상 배열 toohello 문서 미리 시퀀스를 지정 하는 hello에서는 다음을 참조 하십시오.

| **#** | **단계** | **이 작업을 수행합니다…** | **그리고 이러한 문서를 사용합니다.** |
| --- | --- | --- | --- |
| 1. |**Azure 포털 hello 설정** |만들기 및 실행 하 여 StorSimple 장치 관리자 서비스 이전 tooprovisioning StorSimple 가상 배열 구성. |[Hello 포털 준비](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**가상 배열 hello를 프로 비전** |Hyper-v에 대 한 프로 비전 하 고 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2에서 Hyper-v를 실행 중인 호스트 시스템에서 StorSimple 가상 배열 tooa를 연결 합니다. <br></br> <br></br> VMware에 대 한 프로 비전 및 tooa StorSimple 가상 배열 이상 VMware ESXi 5.5를 실행 하는 호스트 시스템에 연결 합니다.<br></br> |[Hyper-V에서 가상 배열 프로비전](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [VMware에서 가상 배열 프로비전](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**가상 배열 hello 설정** |파일 서버에 대 한 초기 설치를 수행 하 고 StorSimple 파일 서버를 등록 hello 장치 설치를 완료 합니다. 그런 다음 SMB 공유를 프로비전할 수 있습니다. <br></br> <br></br> ISCSI 서버에 대 한 초기 설치를 수행 하 고 StorSimple iSCSI 서버를 등록 hello 장치 설치를 완료 합니다. 그런 다음 iSCSI 볼륨을 프로비전할 수 있습니다. |[파일 서버로 가상 배열 설정](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[iSCSI 서버로 가상 배열 설정](storsimple-virtual-array-deploy3-iscsi-setup.md) |

이제 tooset hello Azure 포털을 시작할 수 있습니다.

## <a name="configuration-checklist"></a>구성 검사 목록

hello 필요한 정보를 toocollect StorSimple 가상 배열에 hello 소프트웨어를 구성 하기 전에 hello 구성 검사 목록에 설명 합니다. 이 정보를 사용 하면 시간 미리 약식 hello 프로세스의 사용자 환경에서 hello StorSimple 장치 배포를 준비 합니다. StorSimple 가상 배열 하는 파일 서버 또는 iSCSI 서버로 배포 되었는지 여부에 따라 필요 하면 다음 검사 목록을 hello 합니다.

* Hello 다운로드 [StorSimple 가상 배열 파일 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf)합니다.
* Hello 다운로드 [StorSimple 가상 배열 iSCSI 서버 구성 검사 목록](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf)합니다.

## <a name="prerequisites"></a>필수 조건

여기에 StorSimple 장치 관리자 서비스, StorSimple 가상 배열 및 hello 데이터 센터 네트워크 hello 구성 필수 구성 요소를 찾을 있습니다.

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 장치 관리자 서비스에 대 한

시작하기 전에 다음 사항을 확인합니다.

* 액세스 자격 증명이 있는 Microsoft 계정이 있습니다.
* 액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.
* 사용자의 Microsoft Azure 구독을 StorSimple 장치 관리자 서비스에 사용할 수 있습니다.

### <a name="for-hello-storsimple-virtual-array"></a>StorSimple 가상 배열 hello에 대 한

가상 배열을 배포하기 전에 다음 사항을 확인해야 합니다.

* 이상 버전에서 Windows Server 2008 R2 Hyper-v를 실행 하는 액세스 tooa 호스트 시스템이 준비 또는 VMware (ESXi 5.5) tooa 사용된 될 수 있는 장치를 프로 비전 합니다.
* hello 호스트 시스템은 수 toodedicate 가상 배열 리소스 tooprovision 다음 hello:
  
  * 코어 4개 이상
  * RAM 8GB 이상 파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 파일을 지원 합니다. 16GB RAM toosupport 2-4 백만 파일이 필요 합니다.
  * 네트워크 인터페이스 하나
  * 시스템 데이터용 가상 디스크 500GB

### <a name="for-hello-datacenter-network"></a>Hello 데이터 센터 네트워크에 대 한

시작하기 전에 다음 사항을 확인합니다.

* 데이터 센터에서 hello 네트워크 hello StorSimple 장치의 네트워킹 요구 사항을 기준으로 구성 됩니다. 자세한 내용은 참조 hello [StorSimple 가상 배열 시스템 요구 사항](storsimple-ova-system-requirements.md)합니다.
* StorSimple 가상 배열에는 전용 5Mbps 인터넷 대역폭(또는 그 이상)을 항상 사용할 수 있습니다. 이 대역폭은 다른 응용 프로그램과 공유하면 안됩니다.

## <a name="step-by-step-preparation"></a>단계별 준비

Hello StorSimple 장치 관리자 서비스에 대 한 단계별 지침 tooprepare 다음 hello 귀하의 포털을 사용 합니다.

## <a name="step-1-create-a-new-service"></a>1단계: 새 서비스 만들기

Hello StorSimple 장치 관리자 서비스의 단일 인스턴스에 여러 개의 StorSimple 가상 배열을 관리할 수 있습니다. Hello 단계 toocreate hello StorSimple 장치 관리자 서비스의 인스턴스를 다음을 수행 합니다. 가상 배열에서는 기존 StorSimple 장치 관리자 서비스 toomanage을 설정한 경우이 단계를 건너뜁니다 고 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Toocreate 할 서비스와 저장소 계정의 hello 자동 생성을 설정 하지 않은 경우 저장소 계정을 하나 이상 후 서비스를 성공적으로 만들었습니다.
> 
> * 저장소 계정을 자동으로 만들 하지 않은 경우 너무 이동[hello 서비스에 대 한 새 저장소 계정 구성](#optional-step-configure-a-new-storage-account-for-the-service) 자세한 지침에 대 한 합니다.
> * 저장소 계정의 hello 자동 생성을 사용 하도록 설정한 경우 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>2 단계: hello 서비스 등록 키 가져오기

Hello StorSimple 장치 관리자 서비스가 실행 되 고, tooget hello 서비스 등록 키가 필요 합니다. 이 키가 사용 되는 tooregister를 hello 서비스와 StorSimple 장치를 연결 합니다.

Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/)합니다.

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> hello 서비스 등록 키를 사용 하는 tooregister 모든 hello tooregister StorSimple 장치 관리자 서비스에 문의 해야 하는 StorSimple 장치 관리자 장치.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>3 단계: hello 가상 배열 이미지 다운로드

Hello 서비스 등록 키를 사용 하는 다음 toodownload hello 적절 한 가상 배열 이미지 tooprovision 가상 배열 호스트 시스템에서 필요 합니다. hello 가상 배열 이미지는 특정 운영 체제 및 hello hello Azure 포털의에서 빠른 시작 페이지에서 다운로드할 수 있습니다.

> [!IMPORTANT]
> hello StorSimple 가상 배열에서 실행 중인 hello 소프트웨어 hello StorSimple 장치 관리자 서비스와만 사용할 수 있습니다.
> 
> 

Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/)합니다.

#### <a name="tooget-hello-virtual-array-image"></a>tooget hello 가상 배열 이미지

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다. 
2. Hello Azure 포털에서에서 클릭 **찾아보기 > StorSimple 장치 관리자**합니다.
3. 기존 StorSimple 장치 관리자 서비스를 선택합니다. Hello에 **StorSimple 장치 관리자** 블레이드에서 클릭 **빠른 시작**합니다. 
4. Hello 링크 해당 toohello 이미지 hello Microsoft 다운로드 센터에서에서 toodownload 한다는 것을 클릭 합니다. hello 이미지 파일은 약 4.8 g B입니다.
   
   * Windows Server 2012 이상의 Hyper-V용 VHDX
   * Windows Server 2008 R2 이상의 Hyper-V용 VHD
   * VMWare ESXi 5.5 이상용 VMDK
5. 다운로드 하 고 hello 파일 tooa 로컬 드라이브를 한 노트는 hello 압축 푼된 파일의 압축을 풉니다.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>선택적 단계: hello 서비스에 대 한 새 저장소 계정 구성

이 단계는 선택 사항이 며 서비스와 저장소 계정의 hello 자동 만들기를 활성화 하지 않은 경우에 수행 해야 합니다.

Toocreate Azure 저장소 계정을 다른 지역에 필요한 경우 참조 [어떻게 toocreate 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계별 지침.

Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://ms.portal.azure.com/) hello StorSimple 장치 관리자 서비스 페이지 tooadd 기존 Microsoft Azure 저장소 계정에 있습니다.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독

1. Tooyour 장치 관리자 서비스를 찾아 두 번 클릭 합니다. Hello 열립니다 **개요** 블레이드입니다.
2. 선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션.
3. **추가**를 클릭합니다.
4. Hello에 **저장소 계정 추가** 블레이드에서 다음 hello지 않습니다.
   
    1. **구독**에 **현재**를 선택합니다.
   
    2. Azure 저장소 계정의 hello 이름을 제공 합니다.
   
    3. 선택 **사용** toocreate StorSimple 장치 및 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다. 사설 클라우드 내에서 작동하는 경우에만 **사용 안 함**을 선택합니다.
   
    4. **추가**를 클릭합니다. Hello 저장소 계정이 정상적으로 만들어지면 알림이 표시 됩니다.<br></br>
   
     ![기존 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>다음 단계

hello 다음 단계는 tooprovision StorSimple 가상 배열에 대 한 가상 컴퓨터. 호스트 운영 체제에 따라 참조 hello에 필요한 세부 정보:

* [Hyper-V에서 StorSimple 가상 배열 프로비전](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [VMware에서 StorSimple 가상 배열 프로비전](storsimple-virtual-array-deploy2-provision-vmware.md)

