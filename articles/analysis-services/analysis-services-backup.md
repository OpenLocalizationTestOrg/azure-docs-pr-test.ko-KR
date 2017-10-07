---
title: "aaaAzure Analysis Services 데이터베이스 백업 및 복원 | Microsoft Docs"
description: "설명 방법을 toobackup 및 복원 Azure Analysis Services 데이터베이스입니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>백업 및 복원

온-프레미스 Analysis Services의 경우와 동일 hello 많은 Azure Analysis Services의 테이블 형식 모델 데이터베이스를 백업 합니다. hello 주요 차이점은 백업 파일을 저장 합니다. 백업 파일을 tooa 컨테이너에 저장 된 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다. 이미 있는 저장소 계정과 컨테이너를 사용하거나 서버에 대한 저장소 설정을 구성할 때 만들 수 있습니다.

> [!NOTE]
> 저장소 계정을 만들면 새로운 유료 서비스가 발생할 수 있습니다. toolearn 더 참조 [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/blobs/)합니다.
> 
> 

백업은 abf 확장명으로 저장됩니다. 메모리 내 테이블 형식 모델의 경우 모델 데이터와 메타데이터가 모두 저장됩니다. DirectQuery 테이블 형식 모델의 경우 모델 메타데이터만 저장됩니다. 백업 압축 및 암호화, 선택한 hello 옵션에 따라 수 있습니다. 



## <a name="configure-storage-settings"></a>저장소 설정 구성
를 백업 하기 전에 서버에 대 한 tooconfigure 저장소 설정 해야 합니다.


### <a name="tooconfigure-storage-settings"></a>tooconfigure 저장소 설정
1.  Azure Portal > **설정**에서 **백업**을 클릭합니다.

    ![설정의 백업](./media/analysis-services-backup/aas-backup-backups.png)

2.  **사용**을 클릭한 다음 **저장소 설정**을 클릭합니다.

    ![사용](./media/analysis-services-backup/aas-backup-enable.png)

3. 저장소 계정을 선택하거나 새로 만듭니다.

4. 컨테이너를 선택하거나 새로 만듭니다.

    ![컨테이너 선택](./media/analysis-services-backup/aas-backup-container.png)

5. 백업 설정을 저장합니다.

    ![백업 설정 저장](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>백업

### <a name="toobackup-by-using-ssms"></a>SSMS를 사용 하 여 toobackup

1. SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **백업**을 클릭합니다.

2. **데이터베이스 백업** > **백업 파일**에서 **찾아보기**를 클릭합니다.

3. Hello에 **파일 저장** 대화 상자에서 hello 폴더 경로 확인 하 고 hello 백업 파일에 대 한 이름을 입력 합니다. 

4. Hello에 **Backup Database** 대화 상자에서 옵션을 선택 합니다.

    **파일 덮어쓰기** -hello의이 옵션 toooverwrite 백업 파일을 선택 합니다. 이름이 같은 합니다. 이 옵션을 선택 하지 않으면 저장 하는 hello 파일 가질 수 없습니다 이름과 같은 이름을 hello에에서 이미 있는 hello 동일한 파일로 위치 합니다.

    **압축 적용** -이 옵션 toocompress hello 백업 파일을 선택 합니다. 백업 파일을 압축하면 디스크 공간은 절약되지만 CPU 사용률이 약간 더 높아집니다. 

    **백업 파일을 암호화** -이 옵션 tooencrypt hello 백업 파일을 선택 합니다. 이 옵션에는 사용자가 제공한 암호 toosecure hello 백업 파일이 필요 합니다. hello 암호 복원 작업 이외의 다른 도구를 hello 백업 데이터의 읽을 수 없습니다. Tooencrypt 백업을 선택 하면 hello 암호를 안전한 위치에 저장 합니다.

5. 클릭 **확인** toocreate hello 백업 파일을 저장 합니다.


### <a name="powershell"></a>PowerShell
[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet을 사용합니다.

## <a name="restore"></a>복원
를 복원할 때는 백업 파일이 서버에 구성 된 hello 저장소 계정에 있어야 합니다. Toomove는 온-프레미스 위치 tooyour 저장소 계정에서 백업 파일을 필요한 경우 사용 [Microsoft Azure 저장소 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) 또는 hello [AzCopy](../storage/common/storage-use-azcopy.md) 명령줄 유틸리티입니다. 



> [!NOTE]
> Hello 모델의 역할에서 모든 hello에 대 한 도메인 사용자가 제거 하 고 추가할 해야 온-프레미스 서버에서 복원 하는 경우 Azure Active Directory 사용자로 toohello 역할을 백업 합니다.
> 
> 

### <a name="toorestore-by-using-ssms"></a>SSMS를 사용 하 여 toorestore

1. SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭합니다.

2. Hello에 **Backup Database** 대화에 **백업 파일**, 클릭 **찾아보기**합니다.

3. Hello에 **데이터베이스 파일 찾기** 대화 상자에서 원하는 toorestore 선택 hello 파일입니다.

4. **데이터베이스 복원**선택, hello 데이터베이스입니다.

5. 옵션을 지정합니다. 보안 옵션을 백업할 때 사용한 hello 백업 옵션 일치 해야 합니다.


### <a name="powershell"></a>PowerShell

[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet을 사용합니다.


## <a name="related-information"></a>관련 정보

[Azure Storage 계정](../storage/common/storage-create-storage-account.md)  
[고가용성](analysis-services-bcdr.md)     
[Azure Analysis Services 관리](analysis-services-manage.md)
