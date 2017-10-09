---
title: "VMware에서 StorSimple 가상 배열 aaaProvision | Microsoft Docs"
description: "StorSimple 가상 배열 배포 시리즈의 두 번째 자습서에는 VMware에서 가상 장치를 프로비전하는 내용이 포함됩니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>StorSimple 가상 배열 배포 - VMware에서 프로비전
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>개요
이 자습서에서는 설명 방법을 tooprovision tooa StorSimple 가상 배열 이상 VMware ESXi 5.5를 실행 하는 호스트 시스템에 연결 합니다. 이 문서에는 Azure 포털 및 Microsoft Azure Government 클라우드 hello toohello 배포를 StorSimple 가상 배열에 적용 됩니다.

관리자 권한 tooprovision 필요 하 고이 정보를 tooa 가상 장치를 연결 합니다. hello 프로 비전 하 고 초기 설치에는 약 10 분 toocomplete를 걸릴 수 있습니다.

## <a name="provisioning-prerequisites"></a>프로비전 필수 조건
필수 구성 요소 tooprovision VMware ESXi 5.5를 실행 하는 호스트 시스템에서 가상 장치 hello 및 위에서 다음과 같습니다.

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 장치 관리자 서비스에 대 한
시작하기 전에 다음 사항을 확인합니다.

* 모든 hello 단계를 완료 [StorSimple 가상 배열에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.
* Hello Azure 포털에서에서 VMware에 대 한 hello 가상 장치 이미지를 다운로드 했습니다. 자세한 내용은 참조 **3 단계: 다운로드 hello 가상 장치 이미지** 의 [StorSimple 가상 배열 가이드에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.

### <a name="for-hello-storsimple-virtual-device"></a>Hello StorSimple 가상 장치에 대 한
가상 장치를 배포하기 전에 다음 사항을 확인해야 합니다.

* Hyper-v를 실행 하는 액세스 tooa 호스트 시스템이 준비 (2008 R2 이상 버전)는 수 사용된 tooa 프로 비전 할 수는 장치입니다.
* hello 호스트 시스템은 수 toodedicate 가상 장치 리소스 tooprovision 다음 hello:

  * 코어 4개 이상
  * RAM 8GB 이상 파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다. 16GB RAM toosupport 2-4 백만 파일이 필요 합니다.
  * 네트워크 인터페이스 하나
  * 시스템 데이터용 가상 디스크 500GB

### <a name="for-hello-network-in-datacenter"></a>Hello 네트워크 데이터 센터에 대 한
시작하기 전에 다음 사항을 확인합니다.

* Hello 네트워킹 요구 사항 toodeploy StorSimple 가상 장치 하 고 hello 요구 사항에 따른 구성 된 hello 데이터 센터 네트워크를 검토 했습니다. 

## <a name="step-by-step-provisioning"></a>단계별 프로비전
tooprovision tooa 가상 장치를 연결 하 고, tooperform hello 단계를 수행 해야 합니다.

1. Hello 호스트 시스템에 충분 한 리소스 toomeet hello 최소 가상 장치 요구 사항에 있는지 확인 합니다.
2. 하이퍼바이저에서 가상 장치를 프로비전합니다.
3. Hello 가상 장치를 시작 하 고 hello IP 주소를 가져옵니다.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>1단계: 호스트 시스템이 최소 가상 장치 요구 사항을 충족하도록 합니다.
가상 장치 toocreate이 필요 합니다.

* VMware ESXi Server 5.5를 실행 하는 액세스 tooa 호스트 시스템 이상.
* 시스템 toomanage hello ESXi 호스트에 VMware vSphere 클라이언트입니다.

  * 코어 4개 이상
  * RAM 8GB 이상 파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다. 16GB RAM toosupport 2-4 백만 파일이 필요 합니다.
  * 하나 이상의 네트워크 인터페이스 연결 toohello 네트워크 라우팅 트래픽 tooInternet 수 있습니다. hello 최소 인터넷 대역폭 hello 장치의 최적의 작업에 대 한 5 Mbps tooallow 이어야 합니다.
  * 데이터용 가상 디스크 500GB

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>2단계: 하이퍼바이저에서 가상 장치를 프로비전합니다.
Hello 단계 tooprovision 프로그램 하이퍼바이저에서 가상 장치를 다음을 수행 합니다.

1. 시스템에 hello 가상 장치 이미지를 복사 합니다. 이 가상 이미지가 hello Azure 포털을 통해 다운로드 합니다.

   1. Hello 최신 이미지 파일을 다운로드 한 있는지 확인 합니다. 이전에 hello 이미지 다운로드 하는 경우 다운로드 다시 tooensure hello 최신 이미지가 포함 되어 있습니다. hello 최신 이미지에는 두 개의 파일 (대신 하나)에 있습니다.
   2. 이 이미지를 사용 하 여 hello 절차의 뒷부분에 나오는 hello 이미지를 복사 했던 hello 위치를 기록해 둡니다.

2. Hello vSphere 클라이언트를 사용 하 여 ESXi 서버 toohello에 로그인 합니다. Toohave 관리자 권한을 toocreate 가상 컴퓨터 필요합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. Hello 왼쪽된 창에 표시 되는 hello 인벤토리 단원의 hello vSphere 클라이언트 hello ESXi 서버를 선택 합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Hello VMDK toohello ESXi 서버를 업로드 합니다. Toohello 이동 **구성** hello 오른쪽 창에서 탭 합니다. **하드웨어** 아래에서 **저장소**를 선택합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. Hello에서 마우스 오른쪽 단추로 창 아래에서 **데이터 저장소**, 선택 hello tooupload hello VMDK를 원하는 데이터 저장소입니다. hello 데이터 저장소는 충분 한 hello OS에 대비한 여유 공간 및 데이터 디스크에 있어야 합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. **데이터 저장소 찾아보기**를 마우스 오른쪽 단추를 클릭하고 선택합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. **데이터 저장소 브라우저** 창이 표시됩니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Hello 도구 모음에서 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) 아이콘 toocreate 새 폴더입니다. Hello 폴더 이름을 지정 하 고는 기록 합니다. 나중에 가상 컴퓨터를 만들 때 이 폴더 이름을 사용합니다(권장 모범 사례). **확인**을 클릭합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. hello hello의 왼쪽된 창에 새 폴더가 hello 표시 **데이터 저장소 브라우저**합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Hello 업로드 아이콘 클릭 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) 선택 **파일 업로드**합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. 탐색 하 고 다운로드 한 toohello VMDK 파일을 가리킵니다. 두 가지 파일이 있습니다. 파일 tooupload를 선택 합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. **열기**를 클릭합니다. hello VMDK 파일 toohello의 hello 업로드 데이터 저장소 시작을 지정 합니다. 파일 tooupload hello에 대 일 분 정도 걸릴 수 있습니다.
13. Hello 업로드가 완료 되 면 hello 파일을 hello 데이터 저장소에서 사용자가 만든 hello 폴더에 나타납니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    이제 두 번째 VMDK 파일 toohello hello 업로드 같은 데이터 저장소입니다.
14. Toohello vSphere 클라이언트 창을 반환 합니다. ESXi 서버를 선택한 상태에서 마우스 오른쪽 단추를 클릭하고 **새 가상 컴퓨터**를 선택합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. **새 가상 컴퓨터 만들기** 창이 나타납니다. Hello에 **구성** 페이지, 선택 hello **사용자 지정** 옵션입니다. **다음**을 누릅니다.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Hello에 **이름 및 위치** 페이지에서 가상 컴퓨터의 hello 이름을 지정 합니다. 이 이름은 8 단계 앞부분에서 지정한 hello 폴더 이름이 (권장된 모범 사례) 일치 해야 합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Hello에 **저장소** 페이지 toouse tooprovision VM를 원하는 데이터 저장소를 선택 합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Hello에 **가상 컴퓨터 버전** 페이지에서 **가상 컴퓨터 버전: 8**합니다. 버전 8 too11 모두 사용할 수 있습니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Hello에 **게스트 운영 체제** 페이지, 선택 hello **게스트 운영 체제** 으로 **Windows**합니다. 에 대 한 **버전**, hello 드롭다운 목록에서 선택 **Microsoft Windows Server 2012 (64 비트)**합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Hello에 **Cpu** 페이지, hello 조정 **가상 소켓 수** 및 **가상 소켓 당 코어 수가** hello를 하므로 **코어의총수**4 (또는 그 이상)가 있습니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Hello에 **메모리** 페이지 8GB 이상의 ram을 지정 합니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Hello에 **네트워크** 페이지 hello 네트워크 인터페이스의 hello 수를 지정 합니다. 최소 요구 사항을 hello는 하나의 네트워크 인터페이스입니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Hello에 **SCSI 컨트롤러** 페이지에서 기본값을 사용한 hello **LSI 논리 SAS 컨트롤러**합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Hello에 **디스크를 선택** 페이지에서 선택 **기존 가상 디스크를 사용 하 여**합니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Hello에 **기존 디스크 선택** 페이지의 **디스크 파일 경로**, 클릭 **찾아보기**합니다. **Browse Datastores** (데이터 저장소 찾아보기) 대화 상자가 열립니다. Toohello 위치 hello VMDK 업로드 위치를 이동 합니다. Hello 두 개의 파일을 처음 업로드 병합 된 hello 데이터 저장소의 파일 하나만 표시 됩니다. Hello 파일을 선택 하 고 클릭 **확인**합니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Hello에 **고급 옵션** 페이지 hello 기본값을 적용 하 고 클릭 **다음**합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Hello에 **준비 tooComplete** 페이지 hello 새 가상 컴퓨터와 관련 된 모든 hello 설정을 검토 합니다. 확인 **완료 되기 전에 hello 가상 컴퓨터 설정을 편집**합니다. **계속**을 클릭합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Hello에 **가상 컴퓨터 속성** 페이지 hello **하드웨어** 탭에서 hello 장치 하드웨어를 찾습니다. **새 하드 디스크**를 선택합니다. **추가**를 클릭합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. **하드웨어 추가** 창이 표시됩니다. Hello에 **장치 유형** 페이지의 **tooadd 원하는 선택 hello 유형의 장치**선택, **하드 디스크**를 클릭 하 고 **다음**합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Hello에 **디스크를 선택** 페이지에서 선택 **새 가상 디스크 만들기**합니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Hello에 **디스크를 만들** 페이지, hello 변경 **디스크 크기** too500 GB (이상). 500GB hello 최소 요구 사항을 상태인 동안 항상 가장 큰 디스크를 제공할 수 있습니다. 참고 확장 하거나 프로 비전 한 번 hello 디스크를 축소할 수 없습니다. 디스크 tooprovision hello 크기에 자세한 내용은 hello hello 크기 조정 섹션을 검토 [모범 사례 문서](storsimple-ova-best-practices.md)합니다. **디스크 프로비전**에서 **씬 프로비전**을 선택합니다. **다음**을 누릅니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Hello에 **고급 옵션** 페이지 hello 기본값을 적용 합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Hello에 **준비 tooComplete** 페이지 hello 디스크 옵션을 검토 합니다. **마침**을 클릭합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Toohello 가상 컴퓨터 속성 페이지를 반환 합니다. 새 하드 디스크 tooyour 가상 컴퓨터에 추가 됩니다. **마침**을 클릭합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Hello 오른쪽 창에서 선택한 가상 컴퓨터와 toohello 이동 **요약** 탭 합니다. 가상 컴퓨터에 대 한 hello 설정을 검토 합니다.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

가상 컴퓨터가 프로비전되어 있습니다. hello 다음 단계 toopower이이 컴퓨터에 이며 hello IP 주소를 가져옵니다.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>3 단계: hello 가상 장치 시작 및 hello IP 가져오기
가상 장치 hello 단계 toostart 다음을 수행 하 고 tooit를 연결 합니다.

#### <a name="toostart-hello-virtual-device"></a>toostart hello 가상 장치
1. Hello 가상 장치를 시작 합니다. Hello 왼쪽된 창에서 hello vSphere Configuration Manager에서에서 장치를 선택 하 고 toobring hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다. **전원**을 선택한 후 **전원 켜기**를 선택합니다. 이렇게 하면 가상 컴퓨터의 전원이 켜집니다. Hello 아래쪽에서 hello 상태를 볼 수 **최근 작업** hello vSphere 클라이언트의 창.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. hello 설정 작업은 몇 분 toocomplete를 소요 됩니다. Hello 장치가 실행 되 면 이동 toohello **콘솔** 탭 합니다. Ctrl + Alt + Delete toolog을 toohello 장치에 보냅니다. 또는 지점 hello 콘솔 창에 hello 커서 수 있으며 Ctrl + Alt + Insert 키를 누릅니다. hello 기본 사용자가 *StorSimpleAdmin* hello 기본 암호는 및 *Password1*합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. 보안상의 이유로 hello 처음 로그온 할 때 hello 장치 관리자 암호가 만료 됩니다. 입력 정보 요청된 toochange hello 암호 됩니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. 8자 이상을 포함하는 암호를 입력합니다. hello 암호 3 4 가지 항목 중 이러한 요구 사항 포함 해야 합니다: 대문자, 소문자, 숫자 및 특수 문자. Hello 암호 tooconfirm 다시 입력 것입니다. 알려 hello 암호가 변경 되었습니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Hello 암호를 성공적으로 변경 한 후 hello 가상 장치를 다시 부팅 될 수 있습니다. Hello 재부팅 toocomplete 될 때까지 기다립니다. hello 장치의 Windows PowerShell 콘솔 hello 진행률 표시줄을 함께 표시 될 수 있습니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. 6-8단계는 DHCP 환경이 아닌 곳에서 부팅하는 경우에만 적용됩니다. DHCP 환경에 있는 다음 이러한 단계를 생략 하 고 toostep 9를 이동 합니다. 비 DHCP 환경에서 장치를 부팅 하는 경우 다음 화면 hello를 표시 됩니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   다음으로 hello 네트워크를 구성 합니다.
7. 사용 하 여 hello `Get-HcsIpAddress` 명령 toolist hello 네트워크 인터페이스가 가상 장치에서 사용 하도록 설정 합니다. 장치에 사용 하도록 설정 하는 단일 네트워크 인터페이스, hello 기본 이름이 할당 toothis 인터페이스 인지 `Ethernet`합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. 사용 하 여 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 네트워크입니다. 아래에 예가 나와 있습니다.

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Hello 초기 설치가 완료 된 후 hello 장치에 부팅 hello 장치 배너 텍스트를 표시 됩니다. Hello IP 주소와 hello 배너 텍스트 toomanage hello 장치에 표시 된 hello URL의 적어 둡니다. 이 IP 주소 tooconnect toohello 웹 가상 장치 하 고 전체 hello 로컬 설치 및 등록의 UI를 사용 합니다.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (선택 사항) 정부 클라우드 hello에 장치를 배포 하는 경우에이 단계를 수행 합니다. 장치에서 이제 hello 미국 연방 정보 FIPS (Processing Standard) 모드를 하면 있습니다. hello FIPS 140 표준은 hello 중요 한 데이터 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인 하는 암호화 알고리즘을 정의 합니다.

    1. tooenable hello FIPS 모드에서는 hello 다음 cmdlet을 실행 합니다.

        `Enable-HcsFIPSMode`
    2. 암호화 유효성 검사 hello 내용이 적용 되도록 hello FIPS 모드를 활성화 한 후에 장치를 다시 부팅 합니다.

       > [!NOTE]
       > 장치에서 FIPS 모드를 사용 또는 사용하지 않도록 설정할 수 있습니다. FIPS 및 비 FIPS 모드 사이 교대로 반복 되 hello 장치가 지원 되지 않습니다.
       >
       >

장치 hello 최소 구성 요구를 충족 하지 않으면 hello 배너 텍스트 (아래 참조)에 오류가 표시 됩니다. 적절 한 리소스 toomeet hello 최소 요구 사항을 갖도록 toomodify hello 장치 구성을 해야 합니다. 그런 다음 다시 시작 하 고 toohello 장치를 연결할 수 있습니다. toohello 최소 구성 요구 사항을 참조 [1 단계: hello 호스트 시스템이 최소 가상 장치 요구 사항을 충족 하는지 확인](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)합니다.

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Hello 로컬 웹 UI를 사용 하 여 hello 초기 구성 중 다른 오류가 발생 하면 다음 워크플로가 toohello를 참조 하십시오.

* 진단 테스트를 너무 실행[웹 UI 설정 문제 해결](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)합니다.
* [로그 패키지를 생성하고 로그 파일을 살펴봅니다](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>다음 단계
* [StorSimple 가상 배열을 파일 서버로 설정](storsimple-virtual-array-deploy3-fs-setup.md)
* [StorSimple 가상 배열을 iSCSI 서버로 설정](storsimple-virtual-array-deploy3-iscsi-setup.md)
