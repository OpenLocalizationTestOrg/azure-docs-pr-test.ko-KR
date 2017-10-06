---
title: "데이터 레이크 저장소의 액세스 제어의 aaaOverview | Microsoft Docs"
description: "Azure Data Lake Store에서 액세스 제어가 작동하는 방식을 이해합니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Azure Data Lake Store에서 액세스 제어

Azure 데이터 레이크 저장소 hello POSIX 액세스 제어 모델에서 파생 HDFS에서 파생 되는 액세스 제어 모델을 구현 합니다. 이 문서에 데이터 레이크 저장소에 대 한 hello 액세스 제어 모델의 기본 사항 hello 요약 되어 있습니다. hello HDFS 액세스 제어 모델에 대해 자세히 toolearn 참조 [HDFS 권한을 가이드](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)합니다.

## <a name="access-control-lists-on-files-and-folders"></a>파일 및 폴더에 대한 액세스 제어 목록

**액세스 ACL** 및 **기본 ACL**이라는 두 가지 ACL(액세스 제어 목록)이 있습니다.

* **Acl 액세스**: 이러한 컨트롤 액세스 tooan 개체입니다. 파일과 폴더에는 모두 액세스 ACL이 있습니다.

* **기본 Acl**:는 "템플릿" Acl의 해당 폴더 아래에 만들어진 모든 자식 항목에 대 한 hello 액세스 Acl을 결정 하는 폴더와 관련 된 합니다. 파일에는 기본 ACL이 없습니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

액세스 Acl와 기본 Acl이 hello 있는 동일한 구조입니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> 부모의 기본 ACL 변경 hello hello ACL 액세스 또는 이미 존재 하는 자식 항목의 기본 ACL 영향을 주지 않습니다.
>
>

## <a name="users-and-identities"></a>사용자 및 ID

모든 파일 및 폴더에는 이러한 ID에 대한 고유한 사용 권한이 있습니다.

* hello 파일의 사용자를 소유 하는 hello
* hello 소유 그룹
* 명명된 사용자
* 명명된 그룹
* 기타 모든 사용자

사용자 및 그룹의 hello id에는 Azure Active Directory (Azure AD) id가 있습니다. ","의 사용자 데이터 레이크 저장소의 hello 컨텍스트 수, 하나는 Azure AD 사용자 또는 Azure AD 보안 그룹 의미 합니다.

## <a name="permissions"></a>권한

파일 시스템 개체에 hello 권한이 **읽기**, **쓰기**, 및 **Execute**, 다음 표에 hello와 같이 파일 및 폴더에 사용할 수 있습니다:

|            |    파일     |   폴더 |
|------------|-------------|----------|
| **읽기(R)** | 파일의 hello 내용을 읽을 수 있습니다. | 필요한 **읽기** 및 **Execute** toolist hello 내용의 hello 폴더|
| **쓰기(W)** | 쓰거나 tooa 파일을 추가할 수 있습니다. | 필요한 **쓰기** 및 **Execute** toocreate 자식 폴더에에서 있는 항목 |
| **실행(X)** | 데이터 레이크 저장소의 hello 컨텍스트에서 모든 것은 아닙니다. | 폴더의 필요한 tootraverse hello 자식 항목 |

### <a name="short-forms-for-permissions"></a>사용 권한에 대한 짧은 형식

**RWX** 가 사용 되는 tooindicate **읽기, 쓰기 + 실행**합니다. 더 압축 된 숫자 형식에는 존재 **읽기 = 4**, **쓰기 = 2**, 및 **Execute = 1**, hello 합 hello 사용 권한을 나타냅니다. 다음은 몇 가지 예입니다.

| 숫자 형식 | 짧은 형식 |      의미     |
|--------------|------------|------------------------|
| 7            | RWX        | 읽기 + 쓰기 + 실행 |
| 5            | R-X        | 읽기 + 실행         |
| 4            | R--        | 읽기                   |
| 0            | ---        | 사용 권한 없음         |


### <a name="permissions-do-not-inherit"></a>사용 권한은 상속하지 않습니다.

데이터 레이크 저장소에서 사용 되는 hello POSIX 스타일 모델에서 항목에 대 한 권한은 hello 항목 자체에 저장 됩니다. 즉, 항목에 대 한 권한은 hello 구성 항목은 부모에서 상속할 수 없습니다.

## <a name="common-scenarios-related-toopermissions"></a>일반적인 시나리오 관련된 toopermissions

다음은 사용 권한을 이해 몇 가지 일반적인 시나리오 toohelp tooperform 데이터 레이크 저장소 계정에 대해 특정 작업을 필요 합니다.

### <a name="permissions-needed-tooread-a-file"></a>사용 권한 tooread 파일 필요

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Hello 파일 toobe 읽기에 대 한 호출자에 게 요구 hello **읽기** 사용 권한.
* 모든 hello 폴더 구조의 폴더에에서 hello 파일을 포함 하는 hello에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.

### <a name="permissions-needed-tooappend-tooa-file"></a>사용 권한 tooappend tooa 파일 필요

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Hello 파일 toobe에 추가에 대 한 hello 호출자에 게 요구 **쓰기** 사용 권한.
* 모든 hello hello 파일을 포함 하는 폴더에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.

### <a name="permissions-needed-toodelete-a-file"></a>사용 권한 toodelete 파일 필요

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Hello 상위 폴더에 대 한 호출자에 게 요구 hello **쓰기 / 실행** 사용 권한.
* Hello 파일의 경로 있는 다른 폴더를 hello 모두에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.



> [!NOTE]
> 사용할 수 없는 것으로 hello 두 이전 조건이 충족 되는 필수 toodelete hello 파일에 대 한 권한이 작성 합니다.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>사용 권한 필요 tooenumerate 폴더

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Hello 폴더 tooenumerate에 대 한 호출자에 게 요구 hello **읽기 + Execute** 사용 권한.
* 상위 폴더를 hello 모두에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Hello Azure 포털에서에서 사용 권한 보기

Hello에서 **데이터 탐색기** hello Data Lake 저장소 계정이의 블레이드에서 클릭 **액세스** toosee hello Acl 파일 또는 폴더에 대 한 합니다. 클릭 **액세스** hello에 대 한 Acl toosee hello **카탈로그** hello 아래에 폴더 **mydatastore** 계정.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

이 블레이드를 hello 맨 위 섹션에 있는 hello 사용 권한 개요를 보여 줍니다. (Hello 스크린 샷 hello 사용자 Bob입니다.) 그런 다음, hello 액세스 권한은 표시 됩니다. Hello에서 그 후 **액세스** 블레이드에서 클릭 **간단한 보기** toosee hello 간단한 보기가 있습니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

클릭 **고급 보기** toosee hello 더 높은 수준의 보기 hello 개념의 기본 Acl, 마스크 및 상위 사용자 표시 됩니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>hello 상위 사용자

상위 권한을 사용자에 hello 대부분 모든 hello 사용자의 hello Data Lake 저장소에에서 있습니다. 슈퍼 사용자의 권한은 다음과 같습니다.

* RWX 권한이 너무**모든** 파일 및 폴더.
* 파일이 나 폴더에 대 한 hello 권한을 변경할 수 있습니다.
* Hello 사용자 소유 또는 소유 파일이 나 폴더의 그룹을 변경할 수 있습니다.

Azure에서 Data Lake Store 계정에는 다음을 포함하여 몇 가지 Azure 역할이 있습니다.

* 소유자
* 참가자
* 읽기 권한자

Hello에 있는 모든 사용자 **소유자** 데이터 레이크 저장소 계정에 대 한 역할은 자동으로 해당 계정에 대 한 상위 사용자입니다. toolearn 더 참조 [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.
Toocreate 상위 사용자 권한이 있는 사용자 지정 역할 기반 액세스 제어 (RBAC) 역할을 사용 하도록 하려는 경우 다음 권한을 toohave hello가 필요 합니다.
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>hello 소유 사용자

hello 항목을 만든 hello 사용자는 자동으로 hello 담당 hello 항목의 사용자입니다. 소유 사용자는 다음을 수행할 수 있습니다.

* 소유 하 고 있는 파일의 hello 권한을 변경 합니다.
* Hello 소유 사용자 hello 대상 그룹의 멤버 이기도으로 그룹을 소유 하는 파일을 소유 하는 hello를 변경 합니다.

> [!NOTE]
> 사용자 소유 hello *없습니다* hello 담당 소유한 다른 파일의 사용자를 변경 합니다. 상위 사용자만 파일 또는 폴더의 사용자를 소유 하는 hello를 변경할 수 있습니다.
>
>

## <a name="hello-owning-group"></a>hello 소유 그룹

Hello POSIX Acl, 모든 사용자가 그룹에 연결 된"주." 예를 들어 사용자 "alice" toohello "finance" 그룹을 속해 있을 수 있습니다. Alice toomultiple 그룹에도 속해 수 있지만 한 그룹의 주 그룹으로 항상 지정 됩니다. POSIX, Alice가 파일을 만들 때 해당 파일의 그룹을 소유 하는 hello 설정 됩니다 tooher 주 그룹, 즉이 경우 "finance"로 지정 합니다.

새 파일 시스템 항목을 만들면 데이터 레이크 저장소 그룹을 소유 하는 값 toohello를 할당 합니다.

* **사례 1**: hello 루트 폴더 "/"입니다. 이 폴더는 Data Lake Store 계정이 만들어질 때 생성됩니다. 이 경우 hello 소유 그룹 hello 계정을 만든 toohello 사용자를 설정 됩니다.
* **사례 2** (다른 모든 경우): 새 항목이 생성 되 면 hello 소유 그룹 hello 부모 폴더에서 복사 됩니다.

hello 소유 그룹으로 변경할 수 있습니다.
* 모든 슈퍼 사용자
* hello hello 소유 사용자 hello 대상 그룹의 구성원 이기도 한 경우 사용자가 소유 합니다.

## <a name="access-check-algorithm"></a>액세스 검사 알고리즘

다음 그림 hello Data Lake 저장소 계정에 대 한 hello 액세스 검사 알고리즘을 나타냅니다.

![Data Lake Store ACL 알고리즘](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>hello 마스크 및 "유효 사용 권한"

hello **마스크** 는 RWX은 값에 대 한 액세스를 사용 하는 toolimit **명명 된 사용자**, hello **소유 그룹**, 및 **명명 된 그룹** 라인인 경우 hello 액세스 검사 알고리즘을 수행 합니다. 다음은 hello hello 마스크에 대 한 주요 개념입니다.

* hello 마스크 "유효 사용 권한입니다."를 만듭니다. 즉, 액세스 권한 확인의 hello 시 hello 사용 권한을 수정합니다.
* hello 마스크 hello 파일 소유자 및 모든 상위 사용자가 직접 편집할 수 있습니다.
* hello 마스크 권한을 toocreate hello 유효 사용 권한을 제거할 수 있습니다. hello 마스크 *없습니다* 권한을 toohello 유효 사용 권한을 추가 합니다.

몇 가지 예를 살펴보겠습니다. 다음 예제는 hello에서 hello mask가 설정 되어 너무**RWX**, 해당 hello 엔터티를 의미 하는 모든 사용 권한을 제거 하지 않습니다. 명명 된 사용자, 그룹을 소유 하 고 명명 된 그룹 hello에 대 한 유효 사용 권한 hello hello 액세스 검사 하는 동안 변경 되지 않습니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

다음 예제는 hello에서 hello mask가 설정 되어 너무**R-X**합니다. 즉, 해당 it **hello 쓰기 권한이 해제** 에 대 한 **명명 된 사용자**, **소유 그룹**, 및 **그룹 이라는** 액세스 hello 시 확인 합니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

참조용으로 다음 파일 또는 폴더에 대 한 hello 마스크 hello Azure 포털에에서 나타나는입니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> 새 데이터 레이크 저장소 계정, ACL 액세스 hello에 대 한 hello 마스크 및 hello 루트의 ACL 기본에 대 한 폴더 ("/") tooRWX의 기본값입니다.
>
>

## <a name="permissions-on-new-files-and-folders"></a>새 파일 및 폴더에 대한 사용 권한

기존 폴더에 새 파일이 나 폴더를 만들면 hello 기본 ACL hello 상위 폴더에 따라 결정 됩니다.

- 자식 폴더의 기본 ACL 및 액세스 ACL
- 자식 파일의 액세스 ACL(파일에 기본 ACL이 없는 경우)

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>hello 자식 파일 또는 폴더의 ACL 액세스

자식 파일 또는 폴더를 만들 때 기본 ACL hello 부모 hello hello 자식 파일 또는 폴더의 ACL 액세스도 복사 됩니다. 또한 경우 **다른** hello 부모의 기본 ACL에서에서 사용자에 게 RWX 권한이, hello 자식 항목의 ACL 액세스에서에서 제거 됩니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

대부분의 시나리오에서 hello 이전 정보는 ACL 자식 항목의 액세스를 결정 하는 방법에 대 한 tooknow 하기만 하면는입니다. 하지만 POSIX 시스템 및 원하는 toounderstand 심층 분석이 변환을 구현 하는 방법에 대해 잘 알고 있다면 hello 섹션을 참조 [Umask의 역할을 새 파일 및 폴더에 대 한 ACL 액세스 hello 만드는](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) 이 문서의 뒷부분에 나오는 합니다.


### <a name="a-child-folders-default-acl"></a>자식 폴더의 기본 ACL

부모 폴더 아래의 자식 폴더를 만들면 기본 ACL toohello 자식 폴더를 그대로 hello 부모 폴더의 기본 ACL은 통해 복사 됩니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Data Lake Store에서 ACL을 이해하기 위한 고급 항목

다음은 몇 가지 고급 항목 toohelp 데이터 레이크 저장소 파일 또는 폴더에 대 한 Acl의 결정 방식을 이해 해야 합니다.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>새 파일 및 폴더에 대 한 ACL 액세스 hello 만드는 Umask의 역할

POSIX 규격 시스템에서 hello 일반 개념은 해당 umask 사용에 대 한 tootransform hello 권한을 hello 부모 폴더에는 9 비트 값은 **사용자 소유**, **소유 그룹**, 및  **다른** 새 자식 파일 또는 폴더의 ACL 액세스 hello에 있습니다. umask의 hello 비트 hello 자식 항목의 액세스 ACL에 해제는 비트 tooturn를 식별합니다. 따라서 사용 tooselectively 방지에 대 한 사용 권한 hello 전파 **사용자 소유**, **소유 그룹**, 및 **다른**합니다.

일반적으로 HDFS 시스템 hello umask 관리자에 의해 제어 되는 사이트 전체 구성 옵션입니다. Data Lake Store는 변경할 수 없는 **계정 전체 umask** 를 사용합니다. 데이터 레이크 저장소에 대 한 다음 테이블에서는 hello hello 마스크 해제 합니다.

| 사용자 그룹  | 설정 | 새 자식 항목의 액세스 ACL에 미치는 영향 |
|------------ |---------|---------------------------------------|
| 소유 사용자 | ---     | 영향 없음                             |
| 소유 그룹| ---     | 영향 없음                             |
| 다른       | RWX     | 읽기 + 쓰기 + 실행 제거         |

hello 다음 그림에서는 실행이이 umask 보여 줍니다. hello 한 순수 효과 tooremove **읽기, 쓰기 + 실행** 에 대 한 **다른** 사용자입니다. Umask hello에 대 한 비트를 지정 하지 않아 **사용자 소유** 및 **소유 그룹**, 이러한 사용 권한은 변환 되지 않습니다.

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>hello 스티커 비트

hello 스티커 비트 POSIX 파일 시스템의 고급 기능입니다. 데이터 레이크 저장소의 hello 컨텍스트에서 그럴 가능성은 해당 hello 스티커 비트를 수행 해야 합니다.

hello 다음 표에 hello 스티커 비트 데이터 레이크 저장소에서 작동 하는 방법을 있습니다.

| 사용자 그룹         | 파일    | 폴더 |
|--------------------|---------|-------------------------|
| 고정 비트 **끄기** | 영향 없음   | 영향을 주지 않습니다.           |
| 고정 비트 **켜기**  | 영향 없음   | 제외 하 고 누구도 **상위 사용자** 및 hello **사용자 소유** 가 삭제 또는 해당 자식 항목의 이름을 바꾸면 자식 항목의 합니다.               |

hello 스티커 비트 hello Azure 포털에에서 표시 되지 않습니다.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Data Lake Store의 ACL에 대한 일반적인 질문

Data Lake Store의 ACL에 대해 자주 제기하는 몇 가지 질문은 다음과 같습니다.

### <a name="do-i-have-tooenable-support-for-acls"></a>Acl에 대 한 지원을 tooenable 있습니까?

아니요. ACL을 통한 액세스 제어는 항상 Data Lake Store 계정에 대하여 켜져 있습니다.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>사용 권한을 필요한 toorecursively delete 폴더와 해당 내용?

* hello 부모 폴더가 있어야 **쓰기 / 실행** 사용 권한.
* 삭제 폴더 toobe hello와 그 안의 모든 폴더에 필요 하므로 **읽기, 쓰기 + 실행** 사용 권한.

> [!NOTE]
> 쓰기 권한이 toodelete 파일 폴더에 필요 하지 않습니다. 또한 루트 폴더 hello "/" 수 **되지** 삭제할 수 있습니다.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>파일 또는 폴더의 hello 소유자가 누군지 않습니까?

파일 또는 폴더의 hello 작성자 hello 소유자가 됩니다.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>어떤 그룹의 파일이 나 폴더를 만들 때 그룹을 소유 하는 hello로 설정 되어 있습니까?

hello 소유 그룹 hello 부모 폴더는 hello 아래의 새 파일 또는 폴더가 생성 되는 그룹을 소유 하는 hello에서 복사 됩니다.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>파일의 사용자를 소유 하는 hello 저는 없 hello RWX 권한이 필요 합니다. 어떻게 해야 합니까?

hello 소유 권한을 변경할 수 있습니다 hello hello 파일 toogive의 자체 RWX 권한이 필요 합니다.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Acl을 확인할 때 hello Azure 포털에서에서 사용자 이름 보이지만 Guid, Api를 통해 나타나는 이유는 무엇입니까?

Hello Acl의 항목은 Azure AD에서 toousers에 해당 하는 Guid로 저장 됩니다. hello Api 그대로 hello Guid를 반환 합니다. 가능 하면 친숙 한 이름으로 Guid hello를 변환 하 여 hello Azure 포털에 toomake Acl 보다 쉽게 toouse 하려고 시도 합니다.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>경우에 따라 보이지 이유 hello Acl에서 Guid hello Azure 포털을 사용 중일 때?

GUID는 hello 사용자는 더 이상 Azure AD에 존재 하지 않는 경우에 표시 됩니다. 일반적으로이 hello 사용자 hello 회사를 떠난 또는 Azure AD에서 자신의 계정을 삭제 된 경우 발생 합니다.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Data Lake Store는 ACL의 상속을 지원하나요?

아니요.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>마스크와 umask hello 차이 무엇입니까?

| 마스크 | umask|
|------|------|
| hello **마스크** 속성은 모든 파일 및 폴더에서 사용할 수 있습니다. | hello **umask** hello Data Lake 저장소 계정이의 속성입니다. 따라서에 없는 경우 단일 umask만 hello 데이터 레이크 저장소    |
| hello 담당 사용자 또는 그룹은 파일 또는 상위 사용자의 소유 하 여 파일 또는 폴더에 hello 마스크 속성을 변경할 수 있습니다. | 모든 사용자는 슈퍼 사용자도가 hello umask 속성을 수정할 수 없습니다. 변경할 수 없는 상수 값입니다.|
| 작업 파일이 나 폴더에 있는 사용자는 hello 오른쪽 tooperform 여부 런타임 toodetermine에 hello 액세스 검사 알고리즘 중 hello 마스크 속성이 사용 됩니다. hello 마스크의 hello 역할은 액세스 권한 확인의 hello 시간에 toocreate "유효 사용 권한"입니다. | hello umask 액세스 검사 하는 동안 전혀 사용 되지 않습니다. hello umask는 사용 되는 toodetermine hello 폴더의 새 자식 항목의 ACL 액세스입니다. |
| hello 마스크는 toonamed 사용자, 명명 된 그룹 및 소유 사용자 액세스 권한 확인의 hello 시 적용 되는 3 비트 RWX 값입니다.| hello umask는 9 비트 값 그룹을 소유 하는 사용자, 소유 toohello 적용 되 고 **다른** 새 자식입니다.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>POSIX 액세스 제어 모델에 대한 어디서 자세히 알아볼 수 있나요?

* [Linux의 POSIX 액세스 제어 목록](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)(영문)

* [HDFS 권한 가이드](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)(영문)

* [POSIX FAQ](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [Ubuntu의 POSIX ACL](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL: Linux의 액세스 제어 목록 사용](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)(영문)

## <a name="see-also"></a>참고 항목

* [Azure 데이터 레이크 저장소 개요](data-lake-store-overview.md)
