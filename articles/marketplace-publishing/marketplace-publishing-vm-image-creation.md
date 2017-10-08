---
title: "Azure 마켓플레이스 hello에 대 한 가상 컴퓨터 이미지 aaaCreating | Microsoft Docs"
description: "어떻게 toocreate 가상 컴퓨터 이미지 hello Azure Marketplace에 대 한 다른 사용자에 대 한 toopurchase 대 한 자세한 설명입니다."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>가이드 toocreate hello Azure Marketplace에 대 한 가상 컴퓨터 이미지
이 문서에서는 **2 단계**, hello 가상 하드 디스크 (Vhd)가 Azure 마켓플레이스 toohello 배포한를 준비 하는 것을 안내 합니다. Vhd 프로그램 SKU의 hello 기초가 됩니다. hello 프로세스는 Windows 기반 또는 Linux 기반 SKU를 제공 하 고 있는지 여부에 따라 달라 집니다. 이 문서에서는 두 시나리오를 모두 다룹니다. 이 프로세스는 [계정 만들기 및 등록][link-acct-creation]과 함께 병렬로 수행할 수 있습니다.

## <a name="1-define-offers-and-skus"></a>1. 제품 및 SKU 정의
이 섹션에서는 toodefine hello 행사와 관련 된 각각의 Sku를 설명 합니다.

제품의 Sku의 "부모" tooall입니다. 제품을 여러 개 보유할 수 있습니다. Toostructure를 결정 하는 방법은 해당 제공 tooyou를입니다. 제안을 toostaging 푸시됩니다와 Sku를 모두 푸시됩니다. Hello URL에 표시 될 있으므로 SKU 식별자를를 신중 하 게 고려:

* Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}
* Azure Preview 포털: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}  

SKU에는 VM 이미지에 대 한 hello 상용 이름입니다. VM 이미지에는 운영 체제 디스크 하나와 0개 이상의 데이터 디스크가 포함되어 있습니다. 가상 컴퓨터에 대 한 전체 저장소 프로필 기본적으로 hello 이며 디스크당 VHD 하나가 필요합니다. 빈 데이터 디스크에 만든 VHD toobe가 필요 합니다.

사용 하는 운영 체제에 관계 없이 hello 최소 개수의 hello SKU에 필요한 데이터 디스크를 추가 합니다. 고객 배포의 hello 시간에 있는 이미지의 일부 디스크를 제거할 수 없습니다 있지만 항상 디스크 추가할 수 중 이나 개발 후가 필요 합니다.

> [!IMPORTANT]
> **새 이미지 버전에서 디스크 수를 변경하지 마세요.** Hello 이미지에 데이터 디스크를 다시 구성 해야 하는 경우 새로운 SKU를 정의 합니다. 다른 디스크 개수로 새 이미지 버전 게시 주요 hello ARM 템플릿 및 기타 시나리오를 통해 솔루션의 자동 크기 조정, 자동 배포의 경우에 새 이미지 버전에 따라 새 배포의 hello 잠재력을 갖게 됩니다.
>
>

### <a name="11-add-an-offer"></a>1.1 제품 추가
1. Toohello 로그인 [게시 포털] [ link-pubportal] 판매자 계정을 사용 하 여 합니다.
2. 선택 hello **가상 컴퓨터** hello 게시 포털을 탭 합니다. Hello 메시지 표시 입력 필드에 제품 이름을 입력 합니다. hello 제공 이름은 일반적으로 hello 이름에 hello 제품이 나 서비스 toosell hello Azure Marketplace에서에서 계획 합니다.
3. **만들기**를 선택합니다.

### <a name="12-define-a-sku"></a>1.2 SKU 정의
제공 하는 서비스를 추가한 후 toodefine 필요 하 고 프로그램 Sku를 식별 합니다. 게시자는 제품을 여러 개 보유할 수 있으며 각 제품에는 그 아래 여러 개의 SKU를 포함할 수 있습니다. 제안을 toostaging 푸시됩니다와 Sku를 모두 푸시됩니다.

1. **SKU를 추가합니다.** hello SKU hello URL에 사용 되는 식별자가 필요 합니다. hello 식별자 게시 프로필 내에서 고유 해야 하지만 다른 게시자와 식별 충돌의 위험이 없습니다.

   > [!NOTE]
   > hello에서 제공 하 고 SKU 식별자 hello Marketplace에에서 hello 제공 URL에 표시 됩니다.
   >
   >
2. **SKU에 대한 요약 설명을 추가합니다.** 요약 설명이 표시 toocustomers 않으므로으로 설정 해야 쉽게 읽을 수 있습니다. 이 정보는 hello "푸시 tooStaging" 단계까지 잠긴 toobe가 필요 하지 않습니다. 그때 까지는 무료 tooedit는 것입니다.
3. Windows 기반 Sku를 사용 하는 경우의 권장 링크 hello tooacquire hello 버전의 Windows Server를 승인 합니다.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Azure 호환 VHD 만들기(Linux 기반)
이 섹션 hello Azure Marketplace에 대 한 Linux 기반 VM 이미지를 만들기 위한 최선의 방법에 중점을 둡니다. 단계별 연습은 toohello 설명서 참조: [만들어 포함 된 가상 하드 디스크를 업로드 하는 hello Linux 운영 체제](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Azure 호환 VHD 만들기(Windows 기반)
이 섹션으로 hello Azure Marketplace에 대 한 Windows Server에 기반 하는 SKU hello 단계 toocreate 집중 합니다.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>기본 Vhd를 수정 하는 hello를 사용 하 고 있는지 확인 합니다. 3.1
VM 이미지에 대 한 hello 운영 체제 VHD Windows Server 또는 SQL Server에 포함 된 Azure 승인 기본 이미지를 기반으로 해야 합니다.

toobegin, hello hello에 있는 이미지를 다음 중 하나에서 VM을 만들 [Microsoft Azure 포털][link-azure-portal]:

* Windows Server([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])

Hello 게시 포털 hello SKU 페이지 아래에서 이러한 링크를 찾을 수도 있습니다.

> [!TIP]
> Hello 현재 Azure 포털 또는 PowerShell을 사용 하는 경우 2014 년 9 월 8 일에 게시 된 및 이후 버전의 Windows Server 이미지 승인 됩니다.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Windows 기반 VM 만들기
Hello Microsoft Azure 포털에서 몇 가지 간단한 단계만 거치면에서 승인 된 기본 이미지에 따라 VM을 만들 수 있습니다. hello 다음은 hello 프로세스의 개요입니다.

1. Hello 기본 이미지 페이지에서 선택 **가상 컴퓨터 만들기** toobe toohello 새 전송 [Microsoft Azure 포털][link-azure-portal]합니다.

    ![drawing][img-acom-1]
2. Microsoft 계정 hello로 toohello 포털 및 Azure 구독 toouse hello에 대 한 암호를 로그인 합니다.
3. 선택한 hello 기본 이미지를 사용 하 여 hello 프롬프트 toocreate VM을 따릅니다. Tooprovide 호스트 이름 (hello 컴퓨터의 이름), (관리자 권한으로 등록 됨) 사용자 이름 및 암호에 필요한 VM hello 합니다.

    ![drawing][img-portal-vm-create]
4. Hello VM toodeploy의 hello 크기를 선택 합니다.

    a.    Toodevelop hello VHD 온-프레미스를 계획 하는 경우에 hello 크기 중요 하지 않습니다. Hello 중 하나를 사용 하는 것이 좋습니다. 더 작은 Vm입니다.

    b.    Azure의 hello 이미지 toodevelop 하려는 경우에 hello 중 하나를 사용 하 여 hello 선택한 이미지에 대 한 VM 크기를 권장 하는 것이 좋습니다.

    c.    가격 책정 정보에 대 한 참조 toohello **가격 책정 계층을 권장** hello 포털에 표시 되는 선택기입니다. Hello hello 게시자에서 제공 하는 세 가지 권장된 크기를 제공 합니다. (이 경우 hello 게시자는 Microsoft입니다.)

    ![drawing][img-portal-vm-size]
5. 속성을 설정합니다.

    a.    빠른 배포를 위해 그대로 두면 hello 아래의 hello 속성에 대 한 기본값 **옵션 구성** 및 **리소스 그룹**합니다.

    b.    아래 **저장소 계정**, hello 저장소 계정 운영 체제는 hello에서 VHD를 저장할 필요에 따라 선택할 수 있습니다.

    c.    아래 **리소스 그룹**, 필요에 따라 어떤 tooplace에 VM을 hello hello 논리 그룹을 선택할 수 있습니다.
6. 선택 hello **위치** 배포:

    a.    Toodevelop hello VHD 온-프레미스 하려는 경우 hello 위치 hello 이미지 tooAzure 나중에 업로드할 때문에 중요 하지 않습니다.

    b.    Azure의 hello 이미지 toodevelop 하려는 경우 hello 처음부터 hello 미국 기반 Microsoft Azure 지역 중 하나를 사용 하는 것이 좋습니다. 인증에 대 한 이미지를 제출 하면 Microsoft에서 사용자 대신 수행 하는 hello VHD 복사 프로세스 속도가 향상 됩니다.

    ![drawing][img-portal-vm-location]
7. **만들기**를 클릭합니다. hello VM toodeploy를 시작합니다. 분 안에 문자열 성공적인 배포를가지고 있으며 사용자 SKU에 대 한 toocreate hello 이미지를 시작할 수 있습니다.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 개발 hello 클라우드에서 VHD
프로토콜 RDP (원격 데스크톱)를 사용 하 여 hello 클라우드에서 VHD를 개발 하는 것이 좋습니다. Hello 사용자 이름 및 암호를 구축 하는 동안 지정 tooRDP를 연결 합니다.

> [!IMPORTANT]
> 온-프레미스에서 VHD를 개발하는 경우(권장되지 않음) [온-프레미스에 가상 컴퓨터 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)를 참조하세요. VHD 다운로드 hello 클라우드 개발 하는 경우에 필요 하지 않습니다.
>
>

**Hello를 사용 하 여 RDP를 통해 연결 [Microsoft Azure 포털][link-azure-portal]**

1. **찾아보기** > **VM**을 선택합니다.
2. hello 가상 컴퓨터 블레이드를 엽니다. 해당 hello와 tooconnect 원하는 VM 실행 되 고 다음 배포 된 Vm의 hello 목록에서 선택 확인 합니다.
3. 선택한 VM으로 hello를 설명 하는 블레이드에서 엽니다. Hello 위쪽 클릭 **연결**합니다.
4. 입력 정보 요청된 tooenter hello 사용자 이름 및 암호 프로 비전 중에 지정 된 경우

**PowerShell을 사용하여 RDP를 통해 연결**

원격 데스크톱 파일 tooa 로컬 컴퓨터, toodownload hello를 사용 하 여 [Get-azureremotedesktopfile cmdlet][link-technet-2]합니다. toouse이이 cmdlet을 순서, tooknow hello hello 서비스의 이름과 hello VM의 이름이 필요 합니다. Hello에서 hello VM을 만든 경우 [Microsoft Azure 포털][link-azure-portal], VM 속성에서이 정보를 찾을 수 있습니다.

1. Hello Microsoft Azure 포털에서 선택 **찾아보기** > **Vm**합니다.
2. hello 가상 컴퓨터 블레이드를 엽니다. Hello 배포 된 VM을 선택 합니다.
3. 선택한 VM으로 hello를 설명 하는 블레이드에서 엽니다.
4. **속성**을 클릭합니다.
5. hello hello 도메인 이름의 첫 부분에는 hello 서비스 이름입니다. hello 호스트 이름은 hello VM 이름이입니다.

    ![drawing][img-portal-vm-rdp]
6. 만든 hello VM toohello 관리자의 로컬 데스크톱에 대 한 hello cmdlet toodownload hello RDP 파일은 다음과 같습니다.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Hello 문서에서 RDP에 대 한 자세한 내용은 MSDN에서 확인할 수 있습니다 [RDP 또는 SSH를 사용 하 여 Azure VM tooan 연결](http://msdn.microsoft.com/library/azure/dn535788.aspx)합니다.

**VM 구성 및 SKU 만들기**

Hello 운영 체제 VHD를 다운로드 한 후 HyperV를 사용 하 고 사용자 SKU 만드는 VM toobegin를 구성 합니다. 자세한 단계는 hello TechNet 링크에서 찾을 수 있습니다: [HyperV 설치 및 구성의 VM](http://technet.microsoft.com/library/hh846766.aspx)합니다.

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 hello 올바른 VHD 크기 선택
VM 이미지의 hello Windows 운영 체제 VHD 128 GB 고정 형식 VHD로 만들어야 합니다.  

Hello 실제 크기는 128GB 보다 작거나, VHD hello 스파스 있어야 합니다. 제공 된 기본 Windows 및 SQL Server 이미지 hello 이러한 요구 사항을 이미 충족, 따라서 hello 얻을 VHD의 hello hello 또는 형식 크기를 변경 하지 마십시오.  

데이터 디스크는 1TB이하여야 합니다. Hello 디스크 크기를 결정할 때는 고객 수 없는 크기가 조정 된다는 Vhd 이미지 내에서 배포의 hello 시 기억해 야 합니다. 데이터 디스크 VHD는 고정 형식 VHD로 작성되어야 합니다. 또한 스파스여야 합니다. 데이터 디스크는 비어 있거나 데이터를 포함할 수 있습니다.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 hello 최신 Windows 패치를 설치 합니다.
hello 기본 이미지에 포함 되어 hello 최신 패치를 tootheir 게시 날짜입니다. Hello 운영 체제 만든 VHD를 게시 하기 전에 Windows 업데이트 실행 되 고 모든 hello 최신 위험 및 중요 한 보안 업데이트가 설치 되었는지 확인 합니다.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 필요 시 추가 구성 수행 및 작업 예약
추가 구성이 필요 하며, 경우에 실행 시작 toomake에 모든 변경 내용이 최종 toohello VM을 배포한 후 예약된 된 작업을 사용 하 여 하는 것이 좋습니다.

* 것이 모범 사례 toohave hello 작업 실행이 완료 되 자체를 삭제 합니다.
* 구성 없이 tooexist 항상 표시할 수 있는 두 개의 드라이브 hello 가지 때문에 C 또는 D 드라이브 이외의 드라이브에 사용 해야 합니다. C 드라이브 hello 운영 체제 디스크가 고 D 드라이브 hello 임시 로컬 디스크.

### <a name="37-generalize-hello-image"></a>3.7 hello 이미지를 일반화 합니다.
Azure 마켓플레이스 hello에서 모든 이미지는 일반적인 방법으로 다시 사용할 수 있는 이어야 합니다. 즉, VHD hello 운영 체제를 일반화 해야 합니다.

* Windows hello 이미지 "sysprepped" 수 있어야 하 고 구성이 hello를 지원 하지 않는 **sysprep** 명령입니다.
* Hello hello 디렉터리 windir%\System32\Sysprep에서 다음 명령을 실행할 수 있습니다.

        sysprep.exe /generalize /oobe /shutdown

  다음 MSDN 문서 hello의 단계에서 toosysprep hello 운영 시스템을 제공 하는 방법에 대 한 지침: [만들기 및 업로드 Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. VHD에서 VM 배포
(Hello 일반화 된 운영 체제 VHD와 0 개 이상의 데이터 디스크 Vhd) Vhd를 업로드 한 후 tooan Azure 저장소 계정 수에 등록 하면 사용자 VM 이미지입니다. 그런 다음 해당 이미지를 테스트할 수 있습니다. 운영 체제 VHD을 일반화 하기 때문에 배포할 수 없다는 직접 VM hello hello VHD URL을 제공 하 여 참고 합니다.

toolearn VM 이미지에 대 한 자세한 검토 hello 다음 블로그 게시물:

* [VM 이미지](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM 이미지 PowerShell 방법](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Azure에서 VM 이미지 정보](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Hello 필요한 도구, PowerShell 및 Azure CLI 설정
* [어떻게 toosetup PowerShell](/powershell/azure/overview)
* [어떻게 toosetup Azure CLI](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 사용자 VM 이미지 만들기
#### <a name="capture-vm"></a>VM 캡처
Azure PowerShell/API/CLI를 사용 하 여 VM hello 캡처에 대 한 지침은 아래 제공 된 hello 링크를 참조 하십시오.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>이미지 일반화
Azure PowerShell/API/CLI를 사용 하 여 VM hello 캡처에 대 한 지침은 아래 제공 된 hello 링크를 참조 하십시오.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure CLI](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 사용자 VM 이미지에서 VM 배포
사용자 VM 이미지에서 VM toodeploy hello 현재 사용할 수 있습니다 [Azure 포털](https://manage.windowsazure.com) 또는 PowerShell입니다.

**Hello 현재 Azure 포털에서 VM 배포**

1. 너무 이동**새로** > **계산** > **가상 컴퓨터** > **갤러리에서**합니다.

    ![drawing][img-manage-vm-new]
2. 너무 이동**내 이미지**을 다음 선택 hello 어떤 toodeploy에서 VM 이미지는 VM 및:

   1. 사용량 기준 과금 주의 기울여야 toowhich 이미지 때문에 선택 hello **내 이미지** 보기는 운영 체제 이미지와 VM 이미지를 모두 나열 합니다.
   2. Hello 디스크 수를 보면 hello 대부분 VM 이미지의 둘 이상의 디스크가 있어야 하기 때문에 어떤 유형의 이미지를 배포 하는 확인할 수 있습니다. 그러나 여전히 가능한 toohave 그러면는 단일 운영 체제 디스크가 하나만 있는 VM 이미지는 **디스크 수가** too1를 설정 합니다.

      ![drawing][img-manage-vm-select]
3. Hello VM 만들기 마법사를 수행 하 고 hello VM 이름, VM 크기, 위치, 사용자 이름 및 암호를 지정 합니다.

**PowerShell에서 VM 배포**

toodeploy hello에서 큰 VM 일반화 방금 만든 VM 이미지를 hello 다음 cmdlet을 사용할 수 있습니다.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> 추가적인 도움이 필요하면 [VHD를 만드는 동안 발생하는 일반적인 문제 해결]을 참조하세요.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. VM 이미지에 대한 인증받기
Azure 마켓플레이스 hello에 대 한 VM 이미지를 준비 hello 다음 단계에는 toohave 인증 된 것입니다.

Hello 확인 결과 toohello 업로드 Vhd가 있는 Azure 컨테이너 추가 제안을, SKU, 정의 하 고, 제출 하는 VM 이미지 인증에 대 한,이 프로세스는 특별 한 인증 도구를 실행 포함 됩니다.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 다운로드 하 여 Azure 인증에 대 한 hello 인증 테스트 도구 실행
hello 인증 도구는 사용자 VM 이미지에서 사용자를 프로 비전 하는 실행 중인 VM에서 실행, VM 이미지 hello tooensure Microsoft Azure와 호환 됩니다. Hello 지침과 VHD를 준비 하는 방법에 대 한 요구 사항을 충족 하는지 확인 합니다. hello 도구의 hello 출력 요청 인증 하는 동안 hello 게시 포털에 업로드 해야 하는 호환성 보고서를 됩니다.

Windows와 Linux Vm의 경우와 hello 인증 도구를 사용할 수 있습니다. PowerShell 통해 tooWindows 기반 Vm에 연결 하 고 SSH.Net 통해 tooLinux Vm을 연결 합니다.

1. 먼저, hello에 hello 인증 도구를 다운로드 [Microsoft 다운로드 사이트][link-msft-download]합니다.
2. Hello 인증 도구를 열고 클릭 다음 hello **새 테스트 시작** 단추입니다.
3. Hello에서 **테스트 정보** 화면 hello 테스트 실행에 대 한 이름을 입력 합니다.
4. Linux VM인지 Windows VM인지 여부를 선택합니다. 선택한 있는 따라 hello 후속 옵션을 선택 합니다.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Hello 인증 도구 tooa Linux VM 이미지를 연결 합니다.**
1. SSH 인증 모드 선택 hello: 암호 또는 키 파일입니다.
2. 암호 기반 인증을 사용 하는 경우 hello 도메인 이름 (DNS System) 이름, 사용자 이름 및 암호를 입력 합니다.
3. 인증 키 파일을 사용 하는 경우 hello DNS 이름, 사용자 이름 및 개인 키 위치를 입력 합니다.

   ![Linux VM 이미지의 암호 인증][img-cert-vm-pswd-lnx]

   ![Linux VM 이미지의 키 파일 인증][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Hello 인증 도구 tooa Windows 기반 VM 이미지를 연결 합니다.**
1. 정규화 된 hello VM DNS 이름 (예를 들어 MyVMName.Cloudapp.net)을 입력 합니다.
2. Hello 사용자 이름 및 암호를 입력 합니다.

   ![Windows VM 이미지의 암호 인증][img-cert-vm-pswd-win]

Linux 또는 Windows 기반 VM 이미지에 대 한 hello 적절 한 옵션을 선택한 후 선택 **연결 테스트** SSH.Net 또는 PowerShell에 테스트용으로 유효한 연결이 있는지 tooensure 합니다. 연결 된 후에 선택 **다음** toostart hello 테스트 합니다.

Hello 테스트가 완료 되 면 각 테스트 요소에 대 한 hello 결과 (성공/실패/경고) 받게 됩니다.

![Linux VM 이미지에 대한 테스트 사례][img-cert-vm-test-lnx]

![Windows VM 이미지에 대한 테스트 사례][img-cert-vm-test-win]

Hello 테스트 중 하나라도 실패할 경우 이미지는 보증 되지 않습니다. 이 경우 hello 요구 사항을 검토 하 고 필요한 변경을 수행 합니다.

테스트를 자동화 하는 hello 후 추가 입력이 tooprovide 설문지 화면을 통해 VM 이미지에 묻습니다.  Hello 질문을 완료 한 후 선택 **다음**합니다.

![인증 도구 질문서][img-cert-vm-questionnaire]

![인증 도구 질문서][img-cert-vm-questionnaire-2]

Hello 질문을 완료 한 후에 hello Linux VM 이미지에 대 한 SSH 액세스 정보 같은 추가 정보 및 모든 실패 한 평가 대 한 설명을 제공할 수 있습니다. Hello 테스트 결과 다운로드 하 고 실행 하는 hello 테스트 사례에 대 한 파일 추가 tooyour 답변 toohello 설문지 로그인 수입니다. Hello에 hello 결과 저장 Vhd와 동일한 컨테이너입니다.

![인증 테스트 결과 저장][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 VM 이미지에 대 한 hello 공유 액세스 서명 URI 가져오기
게시 프로세스는 hello, 하는 동안 hello 만든 프로그램 SKU에 대 한 Vhd의 tooeach 이어지는 hello uniform resource identifier (Uri)를 지정 합니다. Microsoft은 hello 인증 프로세스 중 액세스 toothese Vhd 필요합니다. 따라서 각 VHD에 대 한 공유 액세스 서명 URI toocreate 필요. 이 hello에 입력 해야 하는 URI는 **이미지** hello 게시 포털에서에서 탭 합니다.

hello 공유 액세스 서명 URI 생성 toohello 요구 사항 준수 해야 합니다.

* VHD에 대한 공유 액세스 서명 URI를 생성할 때 나열 및 읽기 권한이면 충분합니다. 쓰기 또는 삭제 권한을 제공하지 마세요.
* 액세스에 대 한 hello 기간 hello 공유 액세스 서명 URI를 만들 때 최소 3 주 이어야 합니다.
* UTC 시간, hello 현재 날짜를 전날 선택 hello에 대 한 toosafeguard 합니다. 예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.

SAS URL이 될 수 있습니다 여러 방법으로 tooshare VHD에 대해 생성 된 Azure Marketplace 합니다.
다음 3 권장된 도구 hello 됩니다.

1.  Azure Storage 탐색기
2.  Microsoft Storage Explorer
3.  Azure CLI

**Azure Storage Explorer(Windows 사용자에 대해 권장됨)**

다음은 Azure 저장소 탐색기를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계

1. CodePlex에서 [Azure Storage Explorer 6 미리 보기 3](https://azurestorageexplorer.codeplex.com/)을 다운로드합니다. 너무 이동[Azure 저장소 탐색기 6 미리 보기](https://azurestorageexplorer.codeplex.com/) 클릭 **"다운로드"**합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)을 다운로드하고 압축을 푼 후에 설치합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. 설치 된 후 hello 응용 프로그램을 엽니다.
4. **계정 추가**를 클릭합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Hello 저장소 계정 이름, 저장소 계정 키 및 저장소 끝점 도메인을 지정 합니다. Azure 포털에서 VHD를 유지 한 있는 Azure 구독에서 hello 저장소 계정입니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Azure 저장소 탐색기 연결 tooyour 특정 저장소 계정을 보여 주는 hello 저장소 계정 내에서 포함 된 모든 hello 시작 됩니다. Hello 운영 체제 디스크 VHD 파일 (또한 데이터 디스크 시나리오에 적용할 수 있는 경우)를 복사 했던 hello 컨테이너를 선택 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Hello blob 컨테이너를 선택한 후 Azure 저장소 탐색기는 hello 컨테이너 내에서 표시 된 hello 파일을 시작 합니다. 제출 된 toobe 필요한 hello 이미지 파일 (.vhd)를 선택 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Hello 컨테이너에서 hello.vhd 파일을 선택한 다음 클릭 hello **보안** 탭 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  Hello에 **Blob 컨테이너 보안** 대화 상자, hello에서 leave hello 기본값 **액세스 수준을** 탭을 클릭 한 다음 **공유 액세스 서명** 탭 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Toogenerate hello.vhd 이미지에 대 한 공유 액세스 서명 URI 아래 hello 단계를 수행 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **액세스를 허용:** toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다. 예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.

    b. **에 대 한 액세스가 허용:** hello 후 3 주 이상 된 날짜를 선택 **에서 액세스를 허용** 날짜입니다.

    c. **허용 된 작업:** 선택 hello **목록** 및 **읽기** 사용 권한.

    d. .Vhd 파일 올바르게를 선택한 경우에 프로그램 파일이 나타납니다 **Blob 이름 tooaccess** 확장.vhd를 합니다.

    e. **서명 생성**을 클릭합니다.

    f. **생성 된 공유 액세스 서명 URI이이 컨테이너의**, 위에 강조 표시 된 대로 다음 hello에 대 한 확인:

       - 이미지 파일 이름 있는지 확인 하 고 **".vhd"** hello URI에 있습니다.
       - Hello 서명의 hello 끝에 있는지 확인 하는 **"rl ="** 나타납니다. 이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.
       - Hello 서명의 중간 되는지 확인 **"sr = c"** 나타납니다. 컨테이너 수준 액세스 권한이 있는지 보여 줍니다.

11. 생성 된 hello tooensure 공유 액세스 서명 URI works, 클릭 **브라우저에서 테스트**합니다. 그 hello 다운로드 프로세스를 시작 해야 합니다.

12. Hello 공유 액세스 서명 URI를 복사 합니다. 이 hello 게시 포털에 hello URI toopaste입니다.

13. Hello SKU의에서 각 VHD에 대 한 6-10 단계를 반복 합니다.

**Microsoft Azure Storage Explorer(Windows/MAC/Linux)**

다음은 Microsoft Azure 저장소 탐색기를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계

1.  [http://storageexplorer.com/](http://storageexplorer.com/) 웹 사이트에서 Microsoft Azure Storage Explorer를 다운로드합니다. 너무 이동[Microsoft Azure 저장소 탐색기](http://storageexplorer.com/releasenotes.html) 클릭 **"Windows 용 다운로드"**합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  설치 된 후 hello 응용 프로그램을 엽니다.

3.  **계정 추가**를 클릭합니다.

4.  Tooyour 계정에 로그인 하 여 Microsoft Azure 저장소 탐색기 tooyour 구독 구성

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Toostorage 계정을 이동 하 고 hello 컨테이너를 선택 합니다.

6.  **"공유 액세스 서명 가져오기"**를 마우스 오른쪽 단추로 클릭의 hello 사용 하 여 **컨테이너**

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  다음에 따른 업데이트 시작 시간, 만료 시간 및 사용 권한

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **시작 시간:** toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다. 예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.

    b.  **만료 시간:** hello 후 3 주 이상 된 날짜를 선택 **시작 시간** 날짜입니다.

    c.  **사용 권한:** 선택 hello **목록** 및 **읽기** 사용 권한

8.  컨테이너 공유 액세스 서명 URI를 복사합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    컨테이너 수준에 대 한 생성 된 SAS URL 이며 이제 내부에 tooadd VHD 이름이 필요 합니다.

    컨테이너 수준 SAS URL의 형식:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    아래와 같이 SAS URL에 hello 컨테이너 이름 뒤에 오는 VHD 이름 삽입`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    예제:

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    VHD SAS URL이 됩니다 TestRGVM201631920152.vhd는 hello VHD 이름`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - 이미지 파일 이름 있는지 확인 하 고 **".vhd"** hello URI에 있습니다.
    - Hello 서명의 중간 되는지 확인 **"sp = rl"** 나타납니다. 이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.
    - Hello 서명의 중간 되는지 확인 **"sr = c"** 나타납니다. 컨테이너 수준 액세스 권한이 있는지 보여 줍니다.

9.  생성 된 공유 액세스 서명 URI works hello tooensure 브라우저에서 테스트 합니다. Hello 다운로드 프로세스를 시작 해야

10. Hello 공유 액세스 서명 URI를 복사 합니다. 이 hello 게시 포털에 hello URI toopaste입니다.

11. Hello SKU의에서 각 VHD에 대 한 이러한 단계를 반복 합니다.

**Azure CLI(Windows가 아닌 연속 통합에 권장됨)**

다음은 Azure CLI를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계

1.  Microsoft Azure CLI를 [여기](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)에서 다운로드합니다. **[Windows](http://aka.ms/webpi-azure-cli)** 및 **[MAC OS](http://aka.ms/mac-azure-cli)**에 대한 다양한 링크를 찾을 수도 있습니다.

2.  다운로드되면 설치하세요.

3.  다음 코드를 사용하여 PowerShell 파일을 만들고 로컬에 저장합니다.

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Hello 다음 업데이트에서 매개 변수 위에

    a. **`<StorageAccountName>`**: 저장소 계정 이름을 제공합니다.

    b. **`<Storage Account Key>`**: 저장소 계정 키를 제공합니다.

    c. **`<Permission Start Date>`**: toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다. 예를 들어 hello 현재 날짜가 2016 년 10 월 26 일 경우 값은 여야 2016 년 10 월 25 일

    d. **`<Permission End Date>`**: Hello 후 3 주까지 이상 되는 날짜를 선택 합니다. **시작 날짜**합니다. 값은 **2016/11/02**이어야 합니다.

    다음은 적절 한 매개 변수를 업데이트 한 후 hello 예제 코드

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  "관리자 권한으로 실행" 모드로 Powershell 편집기를 열고 3단계에서 파일을 엽니다.

5.  실행된 hello 스크립트와 해당 컨테이너 수준 액세스에 대 한 SAS URL을 hello 제공 합니다.

    다음과 같은 hello SAS 서명 및 복사 강조 표시 하는 hello-메모장에서의 hello 출력 됩니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  컨테이너 수준 SAS URL을 이제 얻게 됩니다 및 그 안에 tooadd VHD 이름이 필요 합니다.

    컨테이너 수준 SAS URL #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  아래 표시 된 대로 SAS URL에 hello 컨테이너 이름 뒤에 오는 VHD 이름 삽입`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    예제:

    VHD SAS URL이 됩니다 TestRGVM201631920152.vhd는 hello VHD 이름

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - 이미지 파일 이름 및 ".vhd" hello URI에에서 있는지 확인 합니다.
    -   Hello 서명의 중간에 있는지 확인 하는 "sp = rl" 나타납니다. 이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.
    -   Hello 서명의 중간에 있는지 확인 하는 "s r c =" 나타납니다. 컨테이너 수준 액세스 권한이 있는지 보여 줍니다.

8.  생성 된 공유 액세스 서명 URI works hello tooensure 브라우저에서 테스트 합니다. Hello 다운로드 프로세스를 시작 해야

9.  Hello 공유 액세스 서명 URI를 복사 합니다. 이 hello 게시 포털에 hello URI toopaste입니다.

10. Hello SKU의에서 각 VHD에 대 한 이러한 단계를 반복 합니다.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 hello VM 이미지에 대 한 정보를 제공 하 고 hello 게시 포털에서에서 인증 요청
제안 및 SKU를 만든 후 해당 SKU와 연결 된 hello 이미지 세부 정보를 입력 해야 합니다.

1. Toohello 이동 [게시 포털][link-pubportal], 한 다음 판매자 계정으로 로그인 합니다.
2. 선택 hello **VM 이미지** 탭 합니다.
3. hello hello 페이지 위쪽에 나열 된 hello 식별자가 실제로 hello 제품 식별자 및 hello SKU 식별자가 아닌 합니다.
4. Hello 아래의 hello 속성을 채울 **Sku** 섹션.
5. 아래 **운영 체제 제품군**, hello 운영 체제 VHD와 연결 된 hello 운영 체제 유형을 클릭 합니다.
6. Hello에 **운영 체제** hello 운영 체제를 설명 합니다. 운영 체제 제품군, 유형, 버전, 업데이트 등과 같은 형식을 고려하세요. 예를 들어 "Windows Server Datacenter 2014 R2"를 고려합니다.
7. 가상 컴퓨터 크기를 권장 toosix를 선택 합니다. 이들은 toopurchase 결정 하 고 사용자 이미지를 배포할 때 hello 가격 책정 계층 블레이드 hello Azure 포털에에서 표시 된 toohello 고객을 방해 하는 권장 사항입니다. **이들은 권장 사항일 뿐입니다. hello 고객 수 tooselect 이미지에 지정 된 hello 디스크를 제공 하는 모든 VM 크기입니다.**
8. Hello 버전을 입력 합니다. hello 버전 필드에 의미 체계의 버전 tooidentify hello 제품과 해당 업데이트가 캡슐화합니다.
   * 버전은 hello x.y.z 형식이 며, X, Y 및 Z는 정수 형식 이어야 합니다.
   * 다른 SKU에서 이미지는 다른 주 버전과 부 버전을 가질 수 있습니다.
   * SKU에서 버전 hello 패치 버전 (Z x.y.z 형식이 며에서)를 늘리는 증분 변경만 여야 합니다.
9. Hello에 **OS VHD URL** 상자 hello 운영 체제 VHD에 대 한 URI를 만들 hello 공유 액세스 서명을 입력 합니다.
10. 이 SKU와 연결 된 데이터 디스크에 있는 경우 hello 논리 단위 번호 (LUN) toowhich 배포 시 탑재이 데이터 디스크 toobe 원하는 선택 합니다.
11. Hello에 **LUN X VHD URL** 상자 hello 첫 번째 데이터 VHD에 대 한 URI를 만들 hello 공유 액세스 서명을 입력 합니다.

    ![drawing](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>일반적인 SAS URL 문제 및 해결

|문제|오류 메시지|해결|문서 링크|
|---|---|---|---|
|이미지 복사 중 오류 - "?"가 SAS URL에 없습니다|오류: 이미지 복사 사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.|도구를 사용 하 여 업데이트 hello SAS Url 것이 좋습니다.|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|이미지 복사 중 오류 - "st" 및 "se" 매개 변수가 SAS URL에 없습니다|오류: 이미지 복사 사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.|에 시작 및 끝 날짜가 hello SAS Url 업데이트|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|이미지 복사 중 오류 - “sp=rl”이 SAS URL에 없습니다|오류: 이미지 복사 제공 된 SAS Uri를 사용 하 여 toodownload 수 없습니다. blob|"읽기" 및 "목록으로 설정 하는 권한이 있는 hello SAS Url을 업데이트 합니다.|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|이미지 복사 중 오류 - SAS URL은 VHD 이름에 공백을 포함합니다|오류: 이미지 복사 사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.|공백 없이 hello SAS Url을 업데이트 합니다.|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|이미지 복사 중 오류 – SAS URL 권한 부여 오류|오류: 이미지 복사 Tooauthorization 오류 인해 수 없습니다. toodownload blob|Hello SAS Url을 다시 생성|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>다음 단계
Hello SKU 세부 정보를 완료 한 후에 앞으로 toohello을 이동할 수 있습니다 [Azure 마켓플레이스 마케팅 콘텐츠 가이드][link-pushstaging]합니다. 콘텐츠, 가격 및 기타 정보 필요한 전에 너무 마케팅 hello hello 게시 프로세스의 해당 단계에서 제공한**3 단계: 준비 단계에 제공 VM 테스트**배포 하기 전에 다양 한 사용 사례 시나리오를 테스트할 있습니다, 공용 표시 여부에 대 한 제안을 toohello Azure 마켓플레이스 hello 및 구매 합니다.  

## <a name="see-also"></a>참고 항목
* [시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
