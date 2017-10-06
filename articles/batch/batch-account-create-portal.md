---
title: "hello Azure 포털에에서 포함 된 일괄 처리 계정 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure 배치 계정에 Azure 포털 toorun hello hello 클라우드에서 대규모 병렬 작업에 알아봅니다"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Azure 포털 hello로 일괄 처리 계정 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](batch-account-create-portal.md)
> * [배치 관리 .NET](batch-management-dotnet.md)
>
>

Hello에 toocreate Azure 배치 계정 하는 방법에 대해 알아봅니다 [Azure 포털][azure_portal], 계산 시나리오에 맞는 hello 계정 속성을 선택 합니다. 액세스 키 및 계정 Url toofind 중요 한 계정 속성의 같은 위치에 대해 알아봅니다.

일괄 처리 계정 및 시나리오에 대 한 배경 참조 hello [기능 개요](batch-api-basics.md)합니다.



## <a name="create-a-batch-account"></a>배치 계정 만들기

Hello 포털 toocreate 일괄 처리 계정을 사용 하 여 hello 2 중 하나에 *할당 모드 풀*: **서비스 일괄** 모드 또는 최신 hello **사용자 구독** 더 필요한 모드 구성입니다. 이러한 두 모드에 대 한 정보를 참조 hello [기능 개요](batch-api-basics.md#account)합니다. Hello 사용자 구독 모드의 기능에 대 한 참조도 hello [블로그 게시물](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/)합니다.

## <a name="batch-service-mode"></a>배치 서비스 모드



1. Toohello 로그인 [Azure 포털][azure_portal]합니다.
2. **새로 만들기** > **계산** > **배치 서비스**를 클릭합니다.

    ![Hello Marketplace에서에서 일괄 처리][marketplace_portal]
3. hello **새 일괄 처리 계정** 블레이드가 표시 됩니다. 각 블레이드 요소의 아래 hello 설명을 참조 하십시오.

    ![배치 계정 만들기][account_portal]

    a. **계정 이름**: hello 일괄 처리 계정 이름을 선택 하면 hello hello 계정이 생성 되는 Azure 지역 내에서 고유 해야 합니다. (참조 **위치** 아래). hello 계정 이름은 소문자 나 숫자를 포함할 수 있으며 3 ~ 24 자가 하 여야 합니다.

    b. **구독**: hello 어떤 toocreate hello 일괄 처리 계정에서에서 구독 합니다. 하나의 구독만 보유하는 경우 기본적으로 선택됩니다.

    c. **풀 할당 모드**: **배치 서비스**를 선택합니다.

    c. **리소스 그룹**: 새 배치 계정에 대한 기존 리소스 그룹을 선택하거나 필요에 따라 새 리소스 그룹을 만듭니다.

    d. **위치**: hello 어떤 toocreate hello 일괄 처리 계정에에서 Azure 지역입니다. 구독 및 리소스 그룹에서 지 원하는 hello 영역만 옵션으로 표시 됩니다.

    e. **저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다. 대부분의 배치 계정에 사용하는 것이 좋습니다. 자세한 내용은 이 문서 뒷부분의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.

4. 클릭 **만들기** toocreate hello 계정.

   hello 포털이 나타냅니다 배포가 진행 중입니다. 완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.

## <a name="user-subscription-mode"></a>사용자 구독 모드

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Azure 배치 tooaccess hello 구독 (일회용 작업) 허용
사용자 구독 모드에서 첫 번째 일괄 처리 계정을 만든 경우 다음 단계 tooregister hello 일괄 처리와 구독을 수행 합니다. (이전에 동일한 작업을 하는 경우 건너 뛸 toohello 다음.)

1. Toohello 로그인 [Azure 포털][azure_portal]합니다.

2. 클릭 **더 서비스** > **구독**, toouse hello 일괄 처리 계정에 대 한 원하는 hello 구독을 클릭 합니다.

3. Hello에 **구독** 블레이드에서 클릭 **액세스 제어 (IAM)** > **추가**합니다.

    ![구독 액세스 제어][subscription_access]

4. Hello에 **사용 권한을 추가** 블레이드, 선택 hello **참가자** 역할, 일괄 처리 API hello에 대 한 검색 합니다. Hello API를 찾을 때까지 이러한 문자열에 대 한 검색:
    1. **MicrosoftAzureBatch**
    2. **Microsoft Azure Batch** - 최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello 일괄 처리 API에 대 한 hello id입니다. 

5. 일괄 처리 API hello를 찾은 후 선택 하 고 클릭 **저장**합니다.

    ![배치 권한 추가][add_permission]

### <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기
사용자 구독 모드에는 Azure 키 자격 증명 모음 필수가 toothe 속하는 hello 일괄 처리 계정 toobe 만든와 동일한 리소스 그룹입니다. Hello 리소스 그룹은 일괄 처리 인 영역에 있는지 확인 [사용 가능한](https://azure.microsoft.com/regions/services/) 및 구독을 지원 합니다.

1. Hello에 [Azure 포털][azure_portal], 클릭 **새로** > **보안 + Id** > **키 자격 증명 모음** .

2. Hello에 **키 자격 증명 모음 만들기** 블레이드에서 hello 주요 자격 증명 모음에 대 한 이름을 입력 하 고 일괄 처리 계정에 대해 원하는 hello 지역에서 리소스 그룹을 만듭니다. Hello 남은 설정에 기본값을 유지 한 다음 클릭 **만들기**합니다.

### <a name="create-a-batch-account"></a>배치 계정 만들기

1. Hello에 [Azure 포털][azure_portal], 클릭 **새로** > **계산** > **일괄처리서비스**.

    ![Hello Marketplace에서에서 일괄 처리][marketplace_portal]
3. hello **새 일괄 처리 계정** 블레이드가 표시 됩니다. 각 블레이드 요소의 아래 hello 설명을 참조 하십시오.

    ![배치 계정 만들기][account_portal_byos]

    a. **계정 이름**: hello 일괄 처리 계정 이름을 선택 하면 hello hello 계정이 생성 되는 Azure 지역 내에서 고유 해야 합니다. (참조 **위치** 아래). hello 계정 이름은 소문자 나 숫자를 포함할 수 있으며 3 ~ 24 자가 하 여야 합니다.

    b. **구독**: 둘 이상의 구독이 있는 경우 hello 일괄 처리 서비스에 등록 하는 hello 구독을 선택 합니다.

    c. **풀 할당 모드**: **사용자 구독**을 선택합니다.

    d. **주요 자격 증명 모음**: 선택 hello 주요 자격 증명 모음 hello 이전 섹션에서 일괄 처리 계정에 대해 생성 됩니다. 필요에 따라 새 키 자격 증명 모음을 만듭니다. Hello 자격 증명 모음을 선택한 후 hello 확인란 toogrant Azure 배치 액세스 toohello 주요 자격 증명 모음을 선택 합니다.

    c. **리소스 그룹**: hello 주요 자격 증명 모음을 만든 선택 hello 리소스 그룹입니다.

    d. **위치**: hello hello 일괄 처리 계정에 대 한 hello에 키 자격 증명 모음.를 만든 Azure 지역입니다.

    e. **저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다. 대부분의 배치 계정에 사용하는 것이 좋습니다. 자세한 내용은 아래의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.

4. 클릭 **만들기** toocreate hello 계정.

   hello 포털이 나타냅니다 배포가 진행 중입니다. 완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.



## <a name="view-batch-account-properties"></a>배치 계정 속성 보기
Hello 계정이 생성 된 후 hello를 열 수 있습니다 **일괄 처리 계정 블레이드** tooaccess 설정 및 속성에 해당 합니다. Hello 일괄 처리 계정 블레이드의 hello 왼쪽된 메뉴를 사용 하 여 모든 계정 설정 및 속성에 액세스할 수 있습니다.

![Azure 포털에서 배치 계정 블레이드][account_blade]

* **계정 URL을 일괄 처리**: hello로 응용 프로그램을 개발 하는 경우 [일괄 처리 Api](batch-apis-tools.md#azure-accounts-for-batch-development), 계정 URL tooaccess 일괄 처리 리소스가 필요 합니다. 일괄 처리 계정 URL 형식에 따라 hello에 있습니다.

    `https://<account_name>.<region>.batch.azure.com`

![포털에서 배치 계정 URL][account_url]

* **액세스 키** (일괄 처리 서비스 모드): tooauthenticate 액세스 tooyour 일괄 처리 계정 응용 프로그램에서 계정 액세스 키 필요 합니다. (Azure Active Directory 인증을 사용하는 사용자 구독 모드에서는 이 설정을 사용할 수 없습니다.)

    일괄 처리 계정 액세스 키를 입력 tooview 또는 regenerate `keys` hello 왼쪽된 메뉴에 **검색** hello 일괄 처리 계정 블레이드에서 상자 다음 선택 **키**합니다.

    ![Azure 포털에서 배치 계정 키][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>연결된 Azure Storage 계정

필요에 따라 범용 Azure 저장소 계정 tooyour 일괄 처리 계정을 연결할 수 있습니다. hello [응용 프로그램 패키지](batch-application-packages.md) 일괄 처리의 기능은 hello와 마찬가지로 Azure Blob 저장소를 사용 하 여 [일괄 처리 파일 규칙.NET](batch-task-output.md) 라이브러리입니다. 이러한 옵션 기능 일괄 처리 작업을 실행 하는 hello 응용 프로그램 배포 및 생성 하는 hello 데이터 유지 지원 합니다.

배치 계정에서 배타적으로 사용할 수 있도록 새로운 저장소 계정을 만드는 것이 좋습니다.

![범용 저장소 계정 만들기][storage_account]

> [!NOTE]
> Azure 일괄 처리에는 현재 hello 일반적인 용도의 스토리지 계정 유형만을 지원합니다. 이 계정 유형은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)의 5단계 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)에서 설명하고 있습니다.
>
>

> [!WARNING]
> 연결 된 저장소 계정의 hello 선택 키를 다시 생성할 때는 주의 해야 합니다. 하나의 저장소 계정 키를 다시 생성 하 고 클릭 **키 동기화** hello에 저장소 계정 블레이드를 연결 합니다. 5 분 tooallow hello 키 toopropagate toohello 프로그램 풀의 계산 노드를 다시 생성 하 고 동기화 대기 hello 필요한 경우 다른 키입니다. 모두 다시 생성 하는 경우 키 hello에서 동일한 시간, 계산 노드 수 toosynchronize 어느 키 수 없게 되 고 toohello 저장소 계정 액세스를 잃게 됩니다.
>
>

![ 저장소 계정 키 다시 생성][4]

## <a name="batch-service-quotas-and-limits"></a>배치 서비스 할당량 및 제한
있는지와 Azure 구독 및 기타 Azure 서비스 인식, 특정 사항은 [할당량 및 제한](batch-quota-limit.md) tooBatch 계정을 적용 합니다. 일괄 처리 계정에 대 한 현재 할당량 hello 계정에서 hello 포털에 나타나는 **속성**합니다.

![Azure 포털에서 배치 계정 할당량][quotas]



또한 이러한 할당량 중 많은 hello Azure 포털에에서 제출 된 무료 제품 지원 요청으로 간단히 증가할 수 있습니다. 참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 할당량 증가 요청에 대 한 내용은 합니다.

## <a name="other-batch-account-management-options"></a>다른 배치 계정 관리 옵션
또한 toousing hello Azure 포털, 만들고 및 hello 다음과 같이 일괄 처리 계정을 관리할 수도 있습니다.

* [배치 PowerShell cmdlets](batch-powershell-cmdlets-get-started.md)
* [Azure CLI](batch-cli-get-started.md)
* [배치 관리 .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>다음 단계
* Hello 참조 [배치 기능 개요](batch-api-basics.md) toolearn 일괄 처리 서비스 개념 및 기능에 대 한 자세한 합니다. hello 문서 hello 기본 일괄 처리 리소스 풀, 계산 노드, 작업, 작업 등을 설명 하 고 대규모 계산 작업 실행을 사용할 수 있는 서비스의 기능 hello에 대 한 개요를 제공 합니다.
* Hello를 사용 하 여 일괄 처리 사용이 가능한 응용 프로그램 개발의 hello 기본 사항 알아보기 [일괄 처리.NET 클라이언트 라이브러리](batch-dotnet-get-started.md) 또는 [Python](batch-python-tutorial.md)합니다. 이러한 소개 문서 여러 계산 노드에 hello 일괄 처리 서비스 tooexecute 작업을 사용 하 고 Azure 저장소를 사용 하 여 작업 파일 준비 및 검색을 포함 하는 작업 중인 응용 프로그램을 안내해 줍니다.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "저장소 계정 키 다시 생성"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
