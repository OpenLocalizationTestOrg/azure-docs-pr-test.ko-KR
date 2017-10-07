---
title: "Azure 데이터 레이크 저장소에 저장 된 aaaSecuring 데이터 | Microsoft Docs"
description: "그룹 및 액세스를 사용 하 여 Azure 데이터 레이크 저장소의 데이터를 toosecure 목록을 제어 하는 방법에 대해 알아봅니다"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Azure 데이터 레이크 저장소에 저장된 데이터 보호
Azure 데이터 레이크 저장소의 데이터를 보호하는 것은 3단계로 이루어진 방법입니다.

1. Azure Active Directory(AAD)에 보안 그룹을 만들어 시작합니다. 이러한 보안 그룹을 사용 하는 Azure 포털의 tooimplement 역할 기반 액세스 제어 (RBAC). 자세한 내용은 [Microsoft Azure의 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.
2. Hello AAD 보안 그룹 toohello Azure 데이터 레이크 저장소 계정을 할당 합니다. Hello 포털 또는 Api에서 hello 포털 및 관리 작업에서 toohello Data Lake 저장소 계정 액세스를 제어합니다.
3. Hello 데이터 레이크 저장소 파일 시스템의 액세스 제어 목록 (Acl)으로 hello AAD 보안 그룹을 할당 합니다.
4. 또한 데이터 레이크 저장소의 hello 데이터에 액세스할 수 있는 클라이언트에 대 한 IP 주소 범위를 설정할 수도 있습니다.

이 문서는 toouse 작업 위의 Azure 포털 tooperform hello hello 하는 방법에 지침을 제공 합니다. 데이터 레이크 저장소 hello 계정 및 데이터 수준에서 보안을 구현 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 데이터 레이크 저장소의 보안](data-lake-store-security-overview.md)합니다. Azure Data Lake Store에서 ACL을 구현하는 방법에 대한 자세한 내용은 [Data Lake Store에서 Access Control 개요](data-lake-store-access-control.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Azure Active Directory의 보안 그룹 만들기
방법에 대 한 지침은 toocreate AAD 보안 그룹 및 방법을 tooadd 사용자 toohello 그룹 참조 [Azure Active Directory에서 보안 그룹 관리](../active-directory/active-directory-accessmanagement-manage-groups.md)합니다.

> [!NOTE] 
> Hello Azure 포털을 사용 하 여 Azure ad에서 사용자와 다른 그룹 tooa 그룹을 추가할 수 있습니다. 그러나에서 주문 tooadd 서비스 보안 주체 tooa 그룹, 사용 하십시오 [Azure AD PowerShell 모듈](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md)합니다.
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>사용자 또는 보안 그룹 tooAzure Data Lake 저장소 계정 할당
를 사용자를 할당 하거나 보안 그룹을 tooAzure Data Lake 저장소 계정 hello Azure 포털 및 Azure 리소스 관리자 Api를 사용 하 여 hello 계정에 대 한 액세스 toohello 관리 작업을 제어 합니다. 

1. Azure 데이터 레이크 저장소 계정을 엽니다. Hello 왼쪽된 창에서 클릭 **찾아보기**, 클릭 **데이터 레이크 저장소**, hello 데이터 레이크 저장소 블레이드에서 hello 계정 이름 toowhich 원하는 tooassign 사용자 또는 보안 그룹을 클릭 합니다.

2. Data Lake Store 계정 설정 블레이드에서 **액세스 제어(IAM)**를 클릭합니다. 기본 목록으로 hello 블레이드 **구독 관리자** 소유자로 그룹입니다.
   
    ![보안 그룹 tooAzure 데이터 레이크 저장소 계정을 지정 하는](./media/data-lake-store-secure-data/adl.select.user.icon.png "보안 그룹 tooAzure Data Lake 저장소 계정에 할당")

    그룹 및 할당 관련 역할은 두 가지 방법으로 tooadd.
   
    * 사용자/그룹 toohello 계정을 추가 하 고 다음는 역할 할당 또는
    * 역할을 추가 하 고 사용자/그룹 toorole를 할당 합니다.
     
    이 섹션의 의견에 귀 hello 첫 번째 방식에서 그룹을 추가 하 고 다음 역할을 할당 합니다. 유사한 단계 toofirst 선택 하는 역할을 수행할 수 있으며 그룹 toothat 역할을 할당 합니다.
4. Hello에 **사용자** 블레이드에서 클릭 **추가** tooopen hello **액세스 추가** 블레이드입니다. Hello에 **액세스 추가** 블레이드에서 클릭 **역할을 선택**, 한 다음 hello 사용자/그룹에 대 한 역할을 선택 합니다.
   
    ![Hello 사용자에 대 한 역할을 추가](./media/data-lake-store-secure-data/adl.add.user.1.png "hello 사용자의 역할을 추가 합니다.")
   
    hello **소유자** 및 **참가자** 역할 hello 데이터 레이크 계정에 액세스 tooa 다양 한 관리 기능을 제공 합니다. 이 데이터 레이크 hello에에서 대 한 데이터와 상호 작용을 위해 추가할 수 있습니다 toohello * * 판독기 * * 역할입니다. 이러한 역할 hello 범위는 제한 된 toohello 관리 작업 관련된 toohello Azure 데이터 레이크 저장소 계정입니다.
   
    데이터에 대 한 hello 사용자가 수행할 수 있는 작업이 개별 파일 시스템 사용 권한을 정의 합니다. 따라서 읽기 역할을 가진 사용자만 관리 설정 보기 hello 계정과 연결 된 하지만 수 잠재적으로 읽고 쓸 수 파일 시스템 권한을 toothem 할당을 기준으로 하는 데이터입니다. 데이터 레이크 저장소 파일 시스템 권한을에 설명 되어 [Acl toohello Azure 데이터 레이크 저장소 파일 시스템으로 보안 그룹을 할당](#filepermissions)합니다.
5. Hello에 **액세스 추가** 블레이드에서 클릭 **사용자 추가** tooopen hello **사용자 추가** 블레이드입니다. 이 블레이드를 Azure Active Directory에서 만든 hello 보안 그룹을 찾습니다. 그룹 toosearch 많지 hello 그룹 이름에 상위 toofilter hello에 hello 텍스트 상자를 사용 합니다. **선택**을 클릭합니다.
   
    ![보안 그룹 추가](./media/data-lake-store-secure-data/adl.add.user.2.png "보안 그룹 추가")
   
    Tooadd 나열 되어 있지 않은 그룹/사용자를 원하는 경우 초대할 수 있습니다 이러한 hello를 사용 하 여 **초대** 아이콘과 hello 사용자/그룹에 대 한 hello 전자 메일 주소를 지정 합니다.
6. **확인**을 클릭합니다. 아래 표시 된 대로 추가 하는 hello 보안 그룹에 표시 됩니다.
   
    ![추가된 보안 그룹](./media/data-lake-store-secure-data/adl.add.user.3.png "추가된 보안 그룹")

7. 이제 사용자/보안 그룹에 대 한 액세스 toohello Azure 데이터 레이크 저장소 계정이 있습니다. Tooprovide 액세스 toospecific 사용자 원한다 면 추가할 수 있습니다 toohello 보안 그룹입니다. 마찬가지로, 사용자에 대 한 toorevoke 액세스 하려는 경우 hello 보안 그룹에서 제거할 수 있습니다. 또한 여러 보안 그룹 tooan 계정을 할당할 수 있습니다. 

## <a name="filepermissions"></a>Acl toohello Azure 데이터 레이크 저장소 파일 시스템으로 보안 그룹 또는 사용자 지정
사용자/보안 그룹 toohello Azure 데이터 레이크 파일 시스템을 할당 하 여 Azure 데이터 레이크 저장소에 저장 된 hello 데이터의 액세스 제어를 설정할 수 있습니다.

1. 데이터 레이크 저장소 계정 블레이드에서 **데이터 탐색기**를 클릭합니다.
   
    ![Data Lake Store 계정에 디렉터리 만들기](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake Store 계정에 디렉터리 만들기")
2. Hello에 **데이터 탐색기** 블레이드에서 hello 파일 또는 폴더를 원하는 tooconfigure hello ACL 마우스 클릭 한 다음 클릭 **액세스**합니다. 클릭 해야 tooassign ACL tooa 파일 **액세스** hello에서 **파일 미리 보기** 블레이드입니다.
   
    ![Data Lake 파일 시스템에 ACL 설정](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake 파일 시스템에 ACL 설정")
3. hello **액세스** 블레이드 hello 표준 액세스를 나열 하 고 사용자 지정 액세스 toohello 루트 이미 할당 되었습니다. Hello 클릭 **추가** 아이콘 tooadd 사용자 지정 수준 Acl 합니다.
   
    ![표준 및 사용자 지정 액세스 나열](./media/data-lake-store-secure-data/adl.acl.2.png "표준 및 사용자 지정 액세스 나열")
   
   * **표준 액세스** hello UNIX 스타일 액세스를 지정할 수 있는 읽기, 쓰기 상태가, 실행 (rwx) toothree 고유 사용자 클래스: 소유자, 그룹 및 다른 사용자입니다.
   * **사용자 지정 액세스** 특정 명명 된 사용자 또는 그룹 및 뿐만 아니라 hello 파일의 소유자 또는 그룹에 대 한 tooset 권한을 사용 하면 toohello POSIX Acl에 해당 합니다. 
     
     자세한 내용은 [HDFS ACL](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists)을 참조하세요. Data Lake Store에서 ACL이 구현되는 방법에 대한 자세한 내용은 [Data Lake Store의 Access Control](data-lake-store-access-control.md)을 참조하세요.
4. Hello 클릭 **추가** 아이콘 tooopen hello **추가 사용자 지정 액세스** 블레이드입니다. 이 블레이드에 클릭 **사용자 또는 그룹 선택**, 한 다음 **사용자 또는 그룹 선택** 블레이드를 Azure Active Directory에서 만든 hello 보안 그룹을 찾습니다. 그룹 toosearch 많지 hello 그룹 이름에 상위 toofilter hello에 hello 텍스트 상자를 사용 합니다. Hello 그룹 tooadd 하 고을 클릭 한 다음 클릭 **선택**합니다.
   
    ![그룹 추가](./media/data-lake-store-secure-data/adl.acl.3.png "그룹 추가")
5. 클릭 **Select 권한만**hello 권한 선택한 tooassign hello 사용 권한을 기본값으로 ACL 제거할지 ACL, 또는 둘 다에 액세스 합니다. **확인**을 클릭합니다.
   
    ![사용 권한을 toogroup 할당](./media/data-lake-store-secure-data/adl.acl.4.png "toogroup 사용 권한 할당")
   
    Data Lake Store의 사용 권한 및 기본/액세스 ACL에 대한 자세한 내용은 [Data Lake Store에서 액세스 제어](data-lake-store-access-control.md)를 참조하세요.
6. Hello에 **추가 사용자 지정 액세스** 블레이드에서 클릭 **확인**합니다. hello 새로 추가 된 hello 연결 된 사용 권한 가진 그룹 이제 hello에 나열 됩니다 **액세스** 블레이드입니다.
   
    ![사용 권한을 toogroup 할당](./media/data-lake-store-secure-data/adl.acl.5.png "toogroup 사용 권한 할당")
   
   > [!IMPORTANT]
   > 아래에서 항목이 9를 하나만 사용할 수 있습니다 hello 현재 릴리스에서 **사용자 지정 액세스**합니다. 사용자 toosecurity 그룹 추가 9 개 이상 사용자 tooadd을 원하는 경우 보안 그룹을 만든 hello Data Lake 저장소 계정에 대 한 액세스 toothose 보안 그룹을 제공 합니다.
   > 
   > 
7. 필요한 경우 hello 그룹을 추가한 후에 hello 액세스 권한을 수정할 수 있습니다. 각 사용 권한에 대 한 확인란을 선택 하거나 선택 취소 hello tooremove 여부에 따라 지 (읽기, 쓰기, 실행)를 입력 하거나 해당 권한을 toohello 보안 그룹에 할당 합니다. 클릭 **저장** toosave hello 변경 또는 **취소** tooundo hello 변경 합니다.

## <a name="set-ip-address-range-for-data-access"></a>데이터 액세스에 대한 IP 주소 범위를 설정합니다.
Azure 데이터 레이크 저장소 네트워크 수준에서 액세스 tooyour 데이터 저장소를 toofurther 잠금이 있습니다. 방화벽을 설정하고 IP 주소를 지정하며 신뢰할 수 있는 클라이언트에 대한 범위를 정의할 수 있습니다. 활성화 되 면 hello IP 주소가 정의 된 범위 내에 있는 클라이언트만 toohello 저장소를 연결할 수 있습니다.

![방화벽 설정 및 IP 액세스](./media/data-lake-store-secure-data/firewall-ip-access.png "방화벽 설정 및 IP 주소")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정에 대한 보안 그룹 제거
Azure Data Lake 저장소 계정에서 보안 그룹을 제거 하면 hello Azure 포털 및 Azure 리소스 관리자 Api를 사용 하 여 hello 계정에 대 한 액세스 toohello 관리 작업에만 변경 됩니다.

1. Data Lake Store 계정 블레이드에서 **설정**을 클릭합니다. Hello에서 **설정** 블레이드에서 클릭 **사용자**합니다.
   
    ![보안 그룹 tooAzure 데이터 레이크 계정 할당](./media/data-lake-store-secure-data/adl.select.user.icon.png "보안 그룹 tooAzure 데이터 레이크 계정 할당")
2. Hello에 **사용자** 블레이드 tooremove 원하는 hello 보안 그룹을 클릭 합니다.
   
    ![보안 그룹 tooremove](./media/data-lake-store-secure-data/adl.add.user.3.png "보안 그룹 tooremove")
3. Hello 보안 그룹에 대 한 hello 블레이드에서 클릭 **제거**합니다.
   
    ![제거된 보안 그룹](./media/data-lake-store-secure-data/adl.remove.group.png "제거된 보안 그룹")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Azure 데이터 레이크 저장소 파일 시스템에서 보안 그룹 ACL 제거
Azure 데이터 레이크 저장소 파일 시스템에서 보안 그룹 Acl을 제거 하면 변경한 toohello 데이터 hello Data Lake 저장소에에서 액세스 합니다.

1. 데이터 레이크 저장소 계정 블레이드에서 **데이터 탐색기**를 클릭합니다.
   
    ![Data Lake 계정에 디렉터리 만들기](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake 계정에 디렉터리 만들기")
2. Hello에 **데이터 탐색기** 블레이드에서 hello 파일 또는 tooremove hello ACL을 원하는 폴더를 클릭 한 다음 사용자 계정 블레이드에서 hello를 클릭 **액세스** 아이콘입니다. 파일에 대 한 ACL을 tooremove를 눌러야 **액세스** hello에서 **파일 미리 보기** 블레이드입니다.
   
    ![Data Lake 파일 시스템에 ACL 설정](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake 파일 시스템에 ACL 설정")
3. Hello에 **액세스** 블레이드 hello에서 **사용자 지정 액세스** 섹션에서 원하는 tooremove hello 보안 그룹을 클릭 합니다. Hello에 **사용자 지정 액세스** 블레이드에서 클릭 **제거** 클릭 하 고 **확인**합니다.
   
    ![사용 권한을 toogroup 할당](./media/data-lake-store-secure-data/adl.remove.acl.png "toogroup 사용 권한 할당")

## <a name="see-also"></a>참고 항목
* [Azure Data Lake Store 개요](data-lake-store-overview.md)
* [Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [데이터 레이크 저장소와 함께 Azure HDInsight 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell을 사용하여 데이터 레이크 저장소 시작](data-lake-store-get-started-powershell.md)
* [.NET SDK를 사용하여 데이터 레이크 저장소 시작](data-lake-store-get-started-net-sdk.md)
* [Data Lake Store에 대한 진단 로그 액세스](data-lake-store-diagnostic-logs.md)

