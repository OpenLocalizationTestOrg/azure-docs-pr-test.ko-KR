---
title: "Azure 저장소와 Azure PowerShell aaaUsing | Microsoft Docs"
description: "Toouse toocreate Azure 저장소에 대 한 Azure PowerShell cmdlet을 hello 하 및 저장소 계정, 관리 하는 방법을 알아봅니다 blob, 테이블, 큐 및 파일 사용 저장소 분석을 구성 및 쿼리하고 공유 액세스 서명을 생성 합니다."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Azure 저장소와 함께 Azure PowerShell 사용
## <a name="overview"></a>개요
Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다. 작업 기반 명령줄 셸 및 시스템 관리를 위해 특별히 설계된 스크립트 언어로, Powershell을 제어 하 고 Azure 서비스와 응용 프로그램의 hello 관리 자동화 쉽게 수 있습니다. 예를 들어 hello cmdlet tooperform hello hello를 통해 수행할 수 있는 동일한 작업을 사용할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.

이 가이드에서는 살펴볼 것 어떻게 toouse hello [Azure 저장소 Cmdlet](/powershell/module/azurerm.storage/#storage) tooperform 다양 한 Azure 저장소와 개발 및 관리 작업입니다.

이 가이드에서는 이전에 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) 및 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx)을 사용해 본 경험이 있다고 가정합니다. hello 가이드 toodemonstrate hello 사용의 Azure 저장소에 있는 PowerShell 스크립트의 수를 제공합니다. 각 스크립트를 실행 하기 전에 구성에 따라 hello 스크립트 변수를 업데이트 해야 합니다.

이 가이드의 hello 첫 번째 섹션에서 Azure 저장소 및 PowerShell 빠른 보기를 제공합니다. 자세한 내용 및 지침은 hello에서 시작 [Azure PowerShell을 사용 하 여 Azure 저장소에 대 한 필수 구성 요소](#prerequisites-for-using-azure-powershell-with-azure-storage)합니다.

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>5분 안에 Azure 저장소 및 PowerShell 시작하기
이 섹션에서는 5 분 후에 PowerShell 통해 Azure 저장소 tooaccess 합니다.

**새 tooAzure:** Microsoft Azure 구독 및 해당 구독과 연결 된 Microsoft 계정을 가져옵니다. Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.

Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.

**Microsoft Azure 구독 및 계정을 만든 후:**

1. 다운로드 하 여 hello 최신 설치 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)합니다.
2. 시작 Windows PowerShell 통합된 스크립팅 환경 (ISE): 로컬 컴퓨터에서 이동 toohello **시작** 메뉴. 형식 **관리 도구** toorun 클릭 것입니다. Hello에 **관리 도구** 창을 마우스 오른쪽 단추로 클릭 **Windows PowerShell ISE**, 클릭 **관리자 권한으로 실행**합니다.
3. **Windows PowerShell ISE**, 클릭 **파일** > **새로** toocreate 새 스크립트 파일입니다.
4. 이제 기본 PowerShell 명령을 tooaccess Azure 저장소를 보여 주는 간단한 스크립트를 하겠습니다. hello 스크립트 Azure 계정 자격 증명 tooadd Azure 계정 toohello 로컬 PowerShell 환경을 요청 우선 합니다. 그런 다음 hello 스크립트 hello 기본 Azure 구독 설정 하 고 Azure에서 새 저장소 계정을 만드는 됩니다. 다음으로 hello 스크립트는 새 컨테이너를이 새 저장소 계정에서 만들고 기존 이미지 파일 (blob) toothat 컨테이너를 업로드 합니다. 해당 컨테이너의 모든 blob를 나열 하는 hello 스크립트, 후 로컬 컴퓨터에서 새 대상 디렉터리를 만들 되며 hello 이미지 파일을 다운로드 합니다.
5. 다음 코드 섹션 hello에서 hello 설명 간의 hello 스크립트를 선택 **#begin** 및 **#end**합니다. Toocopy CTRL + C를 눌러 해당 toohello 클립보드 합니다.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. **Windows PowerShell ISE**, CTRL + V toocopy hello 스크립트 키를 누릅니다. **파일** > **저장**을 클릭합니다. Hello에 **다른 이름으로 저장** 대화 상자 창에서 "mystoragescript."와 같은 hello 스크립트 파일의 형식 hello 이름 **Save**를 클릭합니다.
7. 이제, 구성 설정에 기반 하 여 tooupdate hello 스크립트 변수 해야 합니다. Hello를 업데이트 해야 **$SubscriptionName** 변수를 사용자의 구독입니다. Hello 스크립트에 지정 된 대로 다른 변수 hello를 유지 하거나 원하는 대로 업데이트할 수 있습니다.
   
   * **$SubscriptionName:** 변수를 사용자 고유의 구독 이름으로 업데이트해야 합니다. Hello 구독의 세 가지 방법으로 toolocate hello 이름 다음의 하나를 따릅니다.
     
    a. **Windows PowerShell ISE**, 클릭 **파일** > **새로** toocreate 새 스크립트 파일입니다. 복사 hello 다음 스크립트 toohello 새 스크립트 파일을 클릭 하 여 **디버그** > **실행**합니다. hello 다음 스크립트는 먼저 Azure 계정 자격 증명 tooadd Azure 계정 toohello 로컬 PowerShell 환경 묻고 모든 hello 구독 연결된 toohello 로컬 PowerShell 세션을 표시 합니다. 이 자습서를 수행 하면서 toouse 되도록 hello 구독의 hello 이름 메모를 수행 합니다.
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. hello에서 구독 이름을 toolocate 및 복사 [Azure 포털](https://portal.azure.com)hello hello 왼쪽에 허브 메뉴에서 클릭 **구독**합니다. 이 가이드의 hello 스크립트를 실행 하는 동안 toouse 되도록 구독 hello 이름을 복사 합니다.
     
     ![Azure portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. hello에서 구독 이름을 toolocate 및 복사 [Azure 클래식 포털](https://manage.windowsazure.com/), 아래로 스크롤하여 클릭 **설정을** hello hello 포털의 왼쪽에 있습니다. 클릭 **구독** toosee 구독 목록이 있습니다. 이 가이드에서 제공 하는 hello 스크립트를 실행 하는 동안 toouse를 원하는 구독의 hello 이름을 복사 합니다.
     
     ![Azure 클래식 포털](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 저장소 계정에 대 한 새 이름을 입력 합니다. **중요:** hello hello 저장소 계정의 이름으로 Azure에서 고유 해야 합니다. 소문자여야 합니다.
   * **$Location:** hello 스크립트에 제공 "West US" hello를 사용 하거나 미국 동부, 유럽 북부, 등 다른 Azure 위치를 선택 합니다.
   * **$ContainerName:** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 컨테이너에 대해 새 이름을 입력 합니다.
   * **$ImageToUpload:** 로컬 컴퓨터에 같은 경로 tooa 그림을 입력: "C:\Images\HelloWorld.png"입니다.
   * **$DestinationFolder:** Enter와 같은 Azure 저장소에서 다운로드 경로 tooa 로컬 디렉터리 toostore 파일: "C:\DownloadImages"입니다.
8. Hello "mystoragescript.ps1" 파일에 있는 hello 스크립트 변수를 업데이트 한 후 클릭 **파일** > **저장**합니다. 클릭 **디버그** > **실행** 하거나 키를 눌러 **F5** toorun hello 스크립트입니다.  

Hello 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다. 다음 스크린 샷 hello 출력을 예를 보여 줍니다.

![Blob 다운로드](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> hello "Azure 저장소 및 시작 PowerShell 5 분 이내에" 섹션에 제공 된 간략 한 소개 방법 toouse Azure 저장소와 Azure PowerShell. 자세한 내용 및 지침은 좋습니다 tooread hello를 다음 섹션.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Azure 저장소에서 Azure PowerShell을 사용하기 위한 필수 구성 요소
위에서 설명한 것 처럼는 Azure 구독 및 계정 toorun hello PowerShell cmdlet이이 가이드에 제공 해야 합니다.

Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다. 설치 및 Azure PowerShell을 설정에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 다운로드 및 설치 하거나는 toohello 최신 Azure PowerShell 모듈을이 가이드를 사용 하기 전에 업그레이드는 것이 좋습니다.

Hello 표준 Windows PowerShell 콘솔 또는 Windows PowerShell 통합 스크립팅 환경 (ISE) hello hello cmdlet을 실행할 수 있습니다. 예를 들어 tooopen **Windows PowerShell ISE**toohello 시작 메뉴를 이동, 관리 도구를 입력 한 toorun 클릭 것입니다. Hello 관리 도구 창 Windows PowerShell ISE를 마우스 오른쪽 단추로 클릭 하 고 관리자 권한으로 실행을 클릭 합니다.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Azure에서 toomanage 저장소 계정 하는 방법

PowerShell 사용한 Azure에서 저장소 계정 관리에 대해 살펴보겠습니다.

### <a name="how-tooset-a-default-azure-subscription"></a>어떻게 tooset 기본 Azure 구독
Azure PowerShell을 사용 하 여 Azure 저장소의 경우 필요한 tooauthenticate Azure Active Directory 인증 또는 인증서 기반 인증을 통해 Azure 사용 하 여 클라이언트 환경 toomanage 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자습서입니다. 이 가이드에서는 hello Azure Active Directory 인증을 사용 합니다.

1. Windows PowerShell ISE에서 다음 명령을 tooadd hello Azure 계정 toohello 로컬 PowerShell 환경을 입력 합니다.

    ```powershell
    Add-AzureAccount
    ```

2. Hello "tooMicrosoft Azure에에서 로그인" 창, hello 전자 메일 주소를 입력 및 해당 계정과 연결 된 암호입니다. Azure 인증 및 hello 자격 증명 정보를 저장 하 고 hello 창을 닫습니다.

3. 다음 명령은 tooview hello Azure 로컬 PowerShell 환경에서 계정 및 계정 나열 되어 있는지 확인 하는 hello를 실행 합니다.
   
    ```powershell
    Get-AzureAccount
    ```
4. 그런 다음, hello cmdlet tooview 다음 모든 hello 구독 연결된 toohello 로컬 PowerShell 세션을 실행 하 고 구독 나열 되어 있는지 확인:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset 기본 Azure 구독 hello Select-azuresubscription cmdlet을 실행 하는 중:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Hello Get-azuresubscription cmdlet을 실행 하 여 hello hello 기본 구독 이름을 확인 합니다.

    ```powershell
    Get-AzureSubscription -Default
    ```

7. 사용할 수 있는 PowerShell cmdlet을 실행 하는 Azure 저장소에 대 한 hello 모든 toosee:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>어떻게 toocreate 새 Azure 저장소 계정
Azure 저장소 toouse 저장소 계정이 필요 합니다. 컴퓨터 tooconnect tooyour 구독을 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.

1. Hello Get AzureLocation cmdlet toofind 모든 hello 사용 가능한 데이터 센터 위치를 실행 합니다.

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. 다음으로 hello 새로 AzureStorageAccount cmdlet toocreate를 새 저장소 계정을 실행 합니다. hello 다음 예제에서는 새 저장소 계정을 만듭니다 hello "West US" 데이터 센터에 있습니다.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> 사용자의 저장소 계정 hello 이름은 Azure 내에서 고유 해야 하며 소문자 여야 합니다. 명명 규칙 및 제한에 대해서는 [Azure Storage 계정 정보](../storage-create-storage-account.md) 및 [컨테이너, Blob, 메타데이터 이름 명명 및 참조](http://msdn.microsoft.com/library/azure/dd135715.aspx)를 참조하세요.
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>어떻게 tooset 기본 Azure 저장소 계정
구독에서 여러 저장소 계정을 사용할 수 있습니다. 그 중 하나를 선택 하 고 hello 기본 저장소 계정 저장소 모든 hello에 대 한 명령을 hello에 동일한으로 설정할 수 있습니다 PowerShell 세션입니다. 이렇게 하면 toorun hello Azure PowerShell 저장소 명령을 hello 저장소 컨텍스트를 명시적으로 지정 하지 않고 있습니다.

1. 구독에 대 한 기본 저장소 계정을 tooset hello 집합 AzureSubscription cmdlet을 실행할 수 있습니다.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. 그런 다음, hello Get-azuresubscription cmdlet tooverify hello 저장소 계정의 기본 구독 계정에 연결 되어 있는지를 실행 합니다. 이 명령은 현재 저장소 계정을 포함 하 여 hello 현재 구독에서 hello 구독 속성을 반환 합니다.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>어떻게 toolist 모든 Azure 저장소 계정에 구독
각 Azure 구독 too100 저장소 계정이 있을 수 있습니다. Hello 제한에 최신 정보를 참조 하십시오. [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md)합니다.

Hello hello 이름과 hello 현재 구독에 대 한 hello 저장소 계정의 상태 아웃 cmdlet toofind 다음을 실행 합니다.

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>어떻게 toocreate Azure 저장소 컨텍스트
Azure 저장소 컨텍스트가 PowerShell tooencapsulate hello 저장소 자격 증명에는 개체입니다. Hello 저장소 계정 및 액세스 키를 명시적으로 지정 하지 않고 있습니다 tooauthenticate 요청을 통해 저장소 컨텍스트를 사용 하 여 모든 후속 cmdlet을 실행 하는 동안 합니다. 저장소 계정 이름과 액세스 키, SAS(공유 액세스 서명) 토큰, 연결 문자열, 익명 등을 다양한 방식으로 저장소 컨텍스트를 만들 수 있습니다. 자세한 내용은 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)를 참조하세요.  

저장소 컨텍스트 hello 세 가지 방법으로 toocreate 다음 중 하나를 사용 합니다.

* Hello 실행 [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind Azure 저장소 계정에 대 한 기본 저장소 액세스 키 hello 아웃 합니다. 그런 다음 호출 하는 hello [새로 AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate 저장소 컨텍스트:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Azure 저장소 컨테이너에 대 한 공유 액세스 서명 토큰을 생성 하 고 toocreate 저장소 컨텍스트를 사용 합니다.

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    자세한 내용은 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 및 [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

* 일부 경우에 새 저장소 컨텍스트를 만들 때 toospecify hello 서비스 끝점을 할 수 있습니다. 저장소 계정에 대 한 사용자 지정 도메인 이름을 hello Blob 서비스에 등록 하거나 toouse 공유 액세스 서명을 저장소 리소스에 액세스 하기 위해 할 수 있습니다. 연결 문자열에 hello 서비스 끝점을 설정 하 고 다음과 같이 toocreate 새 저장소 컨텍스트를 사용 합니다.

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

방법에 대 한 자세한 내용은 tooconfigure 저장소 연결 문자열 참조 [연결 문자열 구성](../storage-configure-connection-string.md)합니다.

컴퓨터를 설정 하 고 학습 방법을 toomanage 구독 및 Azure PowerShell을 사용 하 여 저장소 계정 toohello 어떻게 toomanage Azure blob는 다음 섹션 toolearn 이동한 다음 blob 스냅숏을 합니다.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>어떻게 tooretrieve 및 재생성 Azure 저장소 키
Azure 저장소 계정과 두 계정 키를 함께 제공합니다. 다음 cmdlet tooretrieve hello 키에 사용할 수 있습니다.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

다음 cmdlet tooretrieve 특정 키 hello를 사용 합니다. 유효한 값은 Primary 및 Secondary입니다.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Tooregenerate 원하는 경우 키를 hello 다음 cmdlet을 사용 합니다. -KeyType에 대한 유효한 값은 "Primary" 및 "Secondary"입니다.

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>어떻게 toomanage Azure blob
Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다. 이 섹션에서는 hello Azure Blob 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다. 자세한 내용은 [.NET을 사용하여 Blob Storage 시작](../blobs/storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.

### <a name="how-toocreate-a-container"></a>어떻게 toocreate 컨테이너
Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다. Hello New-azurestoragecontainer cmdlet을 사용 하 여 개인 컨테이너를 만들 수 있습니다.

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> 익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다. 익명 tooprevent tooblobs, 집합 hello 권한 매개 변수를 너무 액세스**오프**합니다. 기본적으로 hello 새 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다. tooallow 익명 공용 읽기 tooblob 리소스에 액세스 하지만 toocontainer 메타 데이터 또는 toohello 목록이 아니라 hello 컨테이너의 blob, hello 권한 매개 변수를 너무 설정**Blob**합니다. tooallow 전체 공용 읽기 액세스 tooblob 리소스, 컨테이너 메타 데이터 및 hello hello 컨테이너의 blob 목록, hello 권한 매개 변수를 너무 설정**컨테이너**합니다. 자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md)합니다.
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>어떻게 tooupload blob 컨테이너에
Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다. 자세한 내용은 [블록 Blob,추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.

tooupload blob tooa 컨테이너에서 hello를 사용할 수 있습니다 [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. 기본적으로이 명령은 hello 로컬 파일 tooa 블록 blob을 업로드합니다. toospecify hello 유형 hello blob hello-BlobType 매개 변수를 사용할 수 있습니다.

hello 다음 실행 하는 예제 hello [Get-childitem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget 모든 hello hello 지정 된 폴더에 파일을 다음으로 전달 toohello 다음 cmdlet hello 파이프라인 연산자를 사용 하 여 합니다. hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet hello 로컬 파일 tooyour 컨테이너에 업로드 합니다.

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Toodownload는 컨테이너에서 blob 하는 방법
다음 예제는 hello toodownload 컨테이너에서 blob 하는 방법을 보여 줍니다. 연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름 및 해당 기본 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다. 그런 다음 hello 예제 hello를 사용 하 여 blob 참조를 검색 [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. 다음으로 hello 사용 하 여 예제 hello [Get AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) hello 로컬 대상 폴더로 cmdlet toodownload blob 합니다.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>저장소 컨테이너 tooanother 하나에서 toocopy blob 하는 방법
저장소 계정 및 지역에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다. hello 다음 예제에서 두 개의 다른 저장소 계정에서 하나의 저장 컨테이너 tooanother toocopy blob 방법을입니다. hello 예제 먼저 원본 및 대상 저장소 계정에 대 한 변수를 설정 하 고 그런 다음 각 계정에 대 한 저장소 컨텍스트를 만듭니다. Hello 예제 hello를 사용 하 여 hello 소스 컨테이너 toohello 대상 컨테이너에서 blob를 복사 하는 다음으로, [시작 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. hello 예제 hello 원본 및 대상 저장소 계정 및 컨테이너 이미 있다고 가정 합니다.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

이 예제에서는 비동기 복사본을 수행합니다. Hello를 실행 하 여 각 복사본의 hello 상태를 모니터링할 수 있습니다 [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>보조 위치에서 toocopy blob 하는 방법
Hello RA GRS를 활성화 계정의 보조 위치에서 blob을 복사할 수 있습니다.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>어떻게 toodelete blob
toodelete blob 가져오려면 먼저 blob 참조를에 hello 제거 AzureStorageBlob cmdlet을 호출 합니다. 다음 예에서는 hello 특정된 컨테이너의 모든 hello blob을 삭제 합니다. hello 예에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다. Hello 예제 hello를 사용 하 여 blob 참조를 검색 하는 다음으로, [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [제거 AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blob에서 Azure 저장소의 컨테이너입니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Toomanage Azure blob 스냅숏을 방법
Azure를 사용하면 Blob의 스냅숏을 만들 수 있습니다. 스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다. 스냅숏이 생성된 후에는 읽거나 복사하거나 삭제할 수 있지만 수정할 수는 없습니다. 스냅숏은 시점에 표시 된 대로 blob 방법을 tooback를 제공 합니다. 자세한 내용은 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요.

### <a name="how-toocreate-a-blob-snapshot"></a>어떻게 toocreate blob 스냅숏
toocreate는 blob의 스냅숏은 blob 참조를 먼저 가져온 고 hello 호출 `ICloudBlob.CreateSnapshot` 메서드를 합니다. hello 다음 예제에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다. Hello 예제 hello를 사용 하 여 blob 참조를 검색 하는 다음으로, [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드 toocreate 스냅숏으로 합니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>어떻게 toolist blob의 스냅숏
Blob에 대해 원하는 수 만큼 많은 스냅샷을 만들 수 있습니다. Blob tootrack와 연결 된 hello 스냅숏을 표시 하 여 최신 스냅숏을 합니다. hello 다음 예제에서는 미리 정의 된 blob 및 호출 hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) 해당 blob의 toolist hello 스냅숏을 cmdlet.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>어떻게 toocopy blob의 스냅숏
Blob toorestore hello 스냅숏에 대 한 스냅숏을 복사할 수 있습니다. 자세한 내용 및 제한 사항에 대해서는 [Blob의 스냅숏 만들기](http://msdn.microsoft.com/library/azure/hh488361.aspx)를 참조하세요. hello 다음 예제에서는 먼저 저장소 계정에 대 한 변수를 설정 하 고 저장소 컨텍스트를 만듭니다. 다음으로 hello 예제는 hello 컨테이너 및 blob 이름 변수를 정의합니다. hello를 사용 하 여 blob 참조를 검색 하는 hello 예제 [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet을 실행 하는 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 메서드 toocreate 스냅숏으로 합니다. 그런 다음 hello 실행 하는 예제 hello [시작 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) hello ICloudBlob 개체를 사용 하 여 hello 원본 blob에 대 한 blob의 cmdlet toocopy hello 스냅숏을 합니다. 있는지 tooupdate hello 변수 기반 hello 예제를 실행 하기 전에 구성 합니다. 다음 예에서는 해당 hello에서는 원본 및 대상 컨테이너는 hello 가정 하 고 hello 원본 blob가 이미 존재 합니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Toomanage Azure blob 하는 방법을 배웠습니다 하 고 Azure PowerShell을 사용 하 여 스냅숏을 blob toohello 다음 섹션 toolearn 방법 toomanage 테이블, 큐 및 파일을 이동 합니다.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Azure toomanage 테이블과 테이블 엔터티
Azure 테이블 저장소 서비스에 사용할 수 있는 NoSQL 데이터 저장소는 비관계형 구조적된 데이터의 거 대 한 집합 toostore 및 쿼리 합니다. hello hello 서비스의 주요 구성 요소는 테이블, 엔터티 및 속성 됩니다. 테이블은 엔터티 컬렉션입니다. 엔터티는 속성의 집합입니다. 각 엔터티는 모든 이름-값 쌍으로 된 too252 속성을 가질 수 있습니다. 이 섹션에서는 hello Azure 테이블 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다. 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx) 및 [.NET을 사용 하 여 Azure 테이블 저장소 시작](../../cosmos-db/table-storage-how-to-use-dotnet.md)합니다.

다음 하위 섹션으로 구성 하는 hello, Azure PowerShell을 사용 하 여 Azure 테이블 저장소 toomanage을 서비스 하는 방법을 알아봅니다. hello 가이드에서 다루는 시나리오 포함 **만드는**, **삭제**, 및 **검색** **테이블**,으로 **추가**, **쿼리**, 및 **테이블 엔터티 삭제**합니다.

### <a name="how-toocreate-a-table"></a>어떻게 toocreate 테이블
모든 테이블은 Azure 저장소 계정에 있어야 합니다. hello 다음 예제에서는 어떻게 toocreate Azure 저장소의 테이블입니다. 연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다. Hello 사용 하 여 다음으로, [새로 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure 저장소의 테이블입니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>어떻게 tooretrieve 테이블
저장소 계정에서 한 테이블 또는 모든 테이블을 쿼리하고 검색할 수 있습니다. hello 다음 예제에서는 방법을 사용 하 여 지정 된 테이블 tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

매개 변수 없이 hello AzureStorageTable Get cmdlet을 호출 하는 경우 저장소 계정에 대 한 저장소 테이블을 모두 가져옵니다.

### <a name="how-toodelete-a-table"></a>어떻게 toodelete 테이블
Hello를 사용 하 여 저장소 계정에서 테이블을 삭제할 수 [제거 AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>어떻게 toomanage 테이블 엔터티
현재, Azure PowerShell는 toomanage 테이블 엔터티 cmdlet을 직접 제공 하지 않습니다. tooperform 테이블 엔터티에 대 한 작업을 hello에 지정 된 hello 클래스를 사용할 수 있습니다 [.NET 용 Azure 저장소 클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)합니다.

#### <a name="how-tooadd-table-entities"></a>어떻게 tooadd 테이블 엔터티
먼저 tooadd은 엔터티 tooa 테이블 엔터티 속성을 정의 하는 개체를 만듭니다. Too255 속성을 3 개의 시스템 속성을 포함 하 여 있을 수 있는 엔터티: **PartitionKey**, **RowKey**, 및 **타임 스탬프**합니다. 삽입 하 고 hello 값을 업데이트 하는 일을 담당 **PartitionKey** 및 **RowKey**합니다. hello 서버 관리의 hello 값 **타임 스탬프**를 수정할 수 없습니다. 함께 hello **PartitionKey** 및 **RowKey** 테이블 내의 모든 엔터티를 고유 하 게 식별 합니다.

* **PartitionKey**: hello 엔터티에 저장 되어 있는 hello 파티션을 결정 합니다.
* **RowKey**: hello 파티션 내의 hello 엔터티를 고유 하 게 식별 합니다.

Too252 엔터티에 대 한 사용자 지정 속성을 정의할 수 있습니다. 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.

hello 다음 예제에서는 어떻게 tooadd 엔터티 tooa 테이블입니다. hello 예제에는 tooretrieve employee 테이블 hello 하 한에 몇 개의 엔터티를 추가 하는 방법을 보여줍니다. 먼저, 연결 tooAzure 저장소를 설정 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다. 다음으로 hello를 사용 하 여 테이블을 지정 하는 hello 검색 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Hello 테이블이 존재 하지 않는 경우 hello [새로 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet은 사용 되는 toocreate Azure 저장소의 테이블입니다. 다음으로 hello 예제 각 엔터티의 파티션과 행 키는 지정 하 여 tooadd 엔터티 toohello 테이블 엔터티 추가 사용자 지정 함수를 정의 합니다. 엔터티 추가 hello 함수 호출 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) hello cmdlet [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) 클래스 toocreate 엔터티 개체입니다. Hello 예제 hello를 호출 하는 나중 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) 이 엔터티 개체 tooadd 메서드 것 tooa 테이블입니다.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>어떻게 tooquery 테이블 엔터티
tooquery 테이블을 사용 하 여 hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) 클래스입니다. hello 다음 예에서는 가정 어떻게 hello에 지정 된 hello 스크립트 이미 실행 한이 가이드의 tooadd 엔터티 섹션. 연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 컨텍스트를 사용 하 여 합니다. 다음으로 hello를 사용 하 여 tooretrieve hello 이전에 만든 "직원" 테이블 시도 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. 호출 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery 클래스에 새 쿼리 개체를 만듭니다. hello 예제 값이 문자열 필터에 지정 된 대로 1 인에 'ID' 열이 있어야 하는 hello 엔터티를 찾습니다. 자세한 내용은 [테이블 및 엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd894031.aspx)를 참조하세요. 이 쿼리를 실행 하면 hello 필터 조건과 일치 하는 모든 엔터티를 반환 합니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>어떻게 toodelete 테이블 엔터티
파티션 및 행 키를 사용하여 엔터티를 삭제할 수 있습니다. hello 다음 예에서는 가정 어떻게 hello에 지정 된 hello 스크립트 이미 실행 한이 가이드의 tooadd 엔터티 섹션. 연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 컨텍스트를 사용 하 여 합니다. 다음으로 hello를 사용 하 여 tooretrieve hello 이전에 만든 "직원" 테이블 시도 [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Hello 테이블이 있을 경우 hello 호출 하 여 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) 메서드 tooretrieve 엔터티는 파티션 및 행 키 값에 기반 합니다. 그런 다음 hello 엔터티 toohello 전달 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) 메서드 toodelete 합니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>방법 toomanage Azure 큐 및 메시지 큐
Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다. 이 섹션에서는 hello Azure 큐 저장소 서비스 개념에 익숙하다고 이미 한다고 가정 합니다. 자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](../storage-dotnet-how-to-use-queues.md)을 참조하세요.

이 섹션 안내해 toomanage Azure 큐 저장소 서비스 Azure PowerShell을 사용 하 여 하는 방법. hello 가이드에서 다루는 시나리오 포함 **삽입** 및 **삭제** 메시지를 큐와 **만드는**, **삭제**, 및 **대기열 검색**합니다.

### <a name="how-toocreate-a-queue"></a>어떻게 toocreate 큐
hello 다음 예에서는 먼저 설정 연결 tooAzure 저장소 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다. 다음으로 호출 [새로 AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 'queuename' 라는 큐.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Azure 큐 서비스에 대한 명명 규칙에 대해서는 [큐 및 메타데이터 이름 지정](http://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.

### <a name="how-tooretrieve-a-queue"></a>어떻게 tooretrieve 큐
쿼리할 수 있으며 특정 큐 또는 저장소 계정에 모든 hello 큐 목록을 검색할 수 있습니다. hello 다음 예제에서는 방법을 사용 하 여 지정 된 큐 tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Hello를 호출 하는 경우 [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) 매개 변수 없이 cmdlet을 모든 hello 큐 목록을 가져옵니다.

### <a name="how-toodelete-a-queue"></a>어떻게 toodelete 큐
toodelete는 큐와 모든 hello 메시지에 포함 된, hello 제거 AzureStorageQueue cmdlet을 호출 합니다. 다음 예제는 hello 사용 하 여 지정 된 큐 toodelete 제거 AzureStorageQueue cmdlet hello 하는 방법을 보여 줍니다.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>어떻게 tooinsert 큐에 메시지
기존 큐에 메시지 tooinsert hello의 새 인스턴스를 먼저 만든 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스입니다. 그런 다음 호출 하는 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 메서드. 문자열(UTF-8 형식) 또는 바이트 배열에서 CloudQueueMessage를 만들 수 있습니다.

다음 예제는 hello tooadd tooa 큐 메시지 하는 방법을 보여 줍니다. 연결 tooAzure 저장소를 먼저 설정 하는 hello 예제 hello 저장소 계정 이름과 액세스 키를 포함 하는 hello 저장소 계정 컨텍스트를 사용 하 여 합니다. 다음으로 hello를 사용 하 여 hello 지정 된 큐를 검색 [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Hello 큐가 있는 hello 경우 [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet은 사용 되는 toocreate hello 인스턴스의 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 클래스입니다. Hello 예제 hello를 호출 하는 나중 [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 이 메시지 개체 tooadd 메서드 것 tooa 큐입니다. 큐를 검색 하 고 'MessageInfo' hello 메시지를 삽입 하는 코드는 다음과 같습니다.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Hello에서 toode queue 다음 어떻게 메시지
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. Hello를 호출 하는 경우 [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) 메서드를 hello 다음에 메시지가 큐입니다. 반환 된 메시지 **GetMessage** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) 메서드. 이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. 코드 호출 **DeleteMessage** 직후 hello 메시지를 처리 합니다.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>방법 toomanage Azure 파일 공유 및 파일
Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 응용 프로그램에 대 한 공유 저장소를 제공 합니다. Microsoft Azure 가상 컴퓨터 및 클라우드 서비스를 통해 탑재 된 공유 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 및 온-프레미스 응용 프로그램 hello 파일 저장소 API 또는 Azure PowerShell을 통해 공유에 파일 데이터에 액세스할 수 있습니다.

Azure File Storage에 대한 자세한 내용은 [Windows에서 Azure File Storage 시작](../storage-dotnet-how-to-use-files.md) 및 [파일 서비스 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)를 참조하세요.

## <a name="how-tooset-and-query-storage-analytics"></a>어떻게 tooset 및 쿼리 저장소 분석
사용할 수 있습니다 [Azure Storage Analytics](../storage-analytics.md) Azure 저장소 계정 및 요청에 대 한 로그 데이터에 대 한 toocollect 메트릭을 전송 tooyour 저장소 계정입니다. 저장소 계정 및 저장소 로깅 toodiagnose 저장소 메트릭을 toomonitor hello 상태를 사용 하 여 수 있으며 저장소 계정을 사용 하 여 문제를 해결할 수 있습니다. 사용 하 여 모니터링을 구성할 수 있습니다 hello Azure 포털 또는 Windows PowerShell 또는 프로그래밍 방식으로 hello 저장소 클라이언트 라이브러리를 사용 합니다. 저장소 로깅에는 저장소 계정에 성공 및 실패 한 요청에 대 한 toorecord 세부 정보를 사용 하면를 서버 쪽을 발생 합니다. 이러한 로그 읽기, 쓰기 및 삭제 작업에 대해 사용자 테이블, 큐 및 blob으로 실패 한 요청에 대 한 hello 이유의 toosee 세부 정보를 사용 합니다.

tooenable 보기 저장소 메트릭 데이터 PowerShell을 사용 하 여 확인 하려면 어떻게 해야 toolearn [어떻게 tooenable 저장소 메트릭을 PowerShell을 사용 하 여](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)합니다.

tooenable 및 검색 하 고 저장소 로깅을 사용 하 여 데이터 PowerShell을 확인 하려면 어떻게 해야 toolearn [어떻게 tooenable 저장소 PowerShell을 사용 하 여 로깅을](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) 및 [저장소 로깅 로그 데이터 찾기](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)합니다.
저장소 메트릭 및 저장소 tootroubleshoot 저장소 문제를 기록 사용에 대 한 자세한 내용은 참조 하십시오. [모니터링, 진단 및 문제 해결 Microsoft Azure 저장소](../storage-monitoring-diagnosing-troubleshooting.md)합니다.

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>어떻게 toomanage 공유 액세스 서명 (SAS) 및 저장 된 액세스 정책
공유 액세스 서명이 Azure 저장소를 사용 하 여 모든 응용 프로그램에 대 한 hello 보안 모델의 중요 한 부분이 됩니다. 제한 된 권한 tooyour 저장소 계정 tooclients hello 계정 키 없는 제공 하는 데 유용 합니다. 기본적으로 hello 소유자만 hello 저장소 계정의 blob, 테이블 및 해당 계정 내에서 큐를 액세스할 수 있습니다. 서비스 또는 응용 프로그램을 필요한 경우 toomake 이러한 리소스 사용 가능한 tooother 클라이언트 액세스 키를 공유 하지 않고 세 가지 옵션이 있습니다.

* 컨테이너의 사용 권한 toopermit 익명 읽기 권한을 toohello 컨테이너와 그 blob를 설정 합니다. 테이블 또는 큐에 대해서는 이렇게 할 수 없습니다.
* 특정 시간 간격에 대 한 제한 된 액세스 권한 toocontainers, blob, 큐 및 테이블을 부여 하는 공유 액세스 서명을 사용 합니다.
* 컨테이너 또는 해당 blob에 대 한, 큐 또는 테이블에 대 한 저장 된 액세스 정책 tooobtain 추가 수준을 공유 액세스 서명에 대 한 제어를 사용 합니다. hello 저장 된 액세스 정책을 사용 하면 toochange hello 시작 시간, 만료 시간 또는 서명에 대 한 사용 권한 또는 toorevoke 뒤 발행 된 합니다.

공유 액세스 서명은 다음 두 가지 형식 중 하나일 수 있습니다.

* **임시 SAS**:는 임시 SAS, hello 시작 시간, 만료 시간을 만들고 SAS hello에 대 한 권한을 모두 hello SAS URI에 지정 됩니다. 이 유형의 SAS는 컨테이너, Blob, 테이블 또는 큐에서 만들 수 있으며, 취소할 수 없습니다.
* **저장 된 액세스 정책 사용 하 여 SAS**: 저장 된 액세스 정책은 리소스 컨테이너는 blob 컨테이너, 테이블 또는 큐-에서 정의 되 고 하나 이상의 공유 액세스 서명에 대 한 toomanage 제약 조건을 사용할 수 있습니다. 저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 제약 조건을 상속-hello 시작 시간, 만료 시간 및 사용 권한-hello 저장 된 액세스 정책을 정의 합니다. 이 유형의 SAS는 취소할 수 있습니다.

자세한 내용은 참조 [공유 액세스 서명 (SAS)를 사용 하 여](../storage-dotnet-shared-access-signature-part-1.md) 및 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md)합니다.

Hello 다음 섹션에서는 살펴보겠습니다 어떻게 toocreate Azure 테이블에 대 한 공유 액세스 서명 토큰 및 저장 된 액세스 정책. Azure PowerShell은 컨테이너, Blob, 큐에 대해 유사한 cmdlet을 제공합니다. 이 섹션의 toorun hello 스크립트 다운로드 hello [Azure PowerShell 버전 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) 이상.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>어떻게 정책 기반 toocreate 공유 액세스 서명 토큰입니다.
Hello 새로 AzureStorageTableStoredAccessPolicy cmdlet toocreate 새 저장 된 액세스 정책을 사용 합니다. 그런 다음 hello 호출 [새로 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate Azure 저장소 테이블에 대 한 새 정책 기반의 공유 액세스 서명 토큰입니다.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>어떻게 toocreate 특별 한 (비 재생산할) 공유 액세스 서명 토큰
사용 하 여 hello [새로 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate 새 임시 (비 재생산할) 공유 액세스 서명 토큰을 Azure 저장소 테이블:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>어떻게 toocreate 저장 된 액세스 정책
Azure 저장소 테이블에 대 한 새로운 AzureStorageTableStoredAccessPolicy hello cmdlet toocreate 새 저장 된 액세스 정책을 사용 합니다.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>어떻게 tooupdate 저장 된 액세스 정책
Azure 저장소 테이블에 대 한 hello 집합 AzureStorageTableStoredAccessPolicy cmdlet tooupdate 기존 저장 된 액세스 정책을 사용 합니다.

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>어떻게 toodelete 저장 된 액세스 정책
Azure 저장소 테이블에 저장된 된 액세스 정책을 제거 AzureStorageTableStoredAccessPolicy hello cmdlet toodelete를 사용 합니다.

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>어떻게 미국 정부 및 Azure 중국에 대 한 Azure 저장소 toouse
[미국 정부용 Azure Government](https://azure.microsoft.com/features/gov/), [글로벌 Azure용 AzureCloud](https://portal.azure.com) 및 [중국의 21Vianet에서 운영하는 Azure용 AzureChinaCloud](http://www.windowsazure.cn/) 등의 Azure 환경은 Microsoft Azure의 독자적인 배포입니다. 미국 정부 및 Azure 중국을 위한 새로운 Azure 환경을 배포할 수 있습니다.

Azure 저장소와 AzureChinaCloud toouse toocreate AzureChinaCloud와 연결 된 저장소 컨텍스트가 필요 합니다. 이러한 단계 tooget 시작을 수행 합니다.

1. Hello 실행 [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 사용 가능한 Azure 환경:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Azure 중국 계정 tooWindows PowerShell을 추가 합니다.
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. AzureChinaCloud 계정에 대한 저장소 컨텍스트를 만듭니다.
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Azure 저장소와 [미국 Azure Government](https://azure.microsoft.com/features/gov/)에서 Azure 저장소를 사용하려면 새 환경을 정의한 다음 이 환경으로 새 저장소 컨텍스트를 생성해야 합니다.

1. Hello 실행 [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 사용 가능한 Azure 환경:

    ```powershell
    Get-AzureEnvironment
    ```

2. Azure 미국 정부 계정 tooWindows PowerShell을 추가 합니다.
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. AzureUSGovernment 계정에 대한 저장소 컨텍스트를 만듭니다.
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
자세한 내용은 다음을 참조하세요.

* [Microsoft Azure Government 개발자 가이드](../../azure-government/documentation-government-developer-guide.md)
* [중국 서비스에서 응용 프로그램을 만들 때의 차이점 개요](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>다음 단계
이 가이드에서 배운 어떻게 toomanage Azure PowerShell 포함 Azure Storage. 다음은 자세한 내용을 확인할 수 있는 몇 가지 관련 항목 및 리소스입니다.

* [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 저장소 PowerShell Cmdlet(영문)](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell 참조](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
