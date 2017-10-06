---
title: "Azure 포털 hello로 Azure 미디어 서비스 계정 aaaCreate | Microsoft Docs"
description: "이 자습서에서는 hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정을 만드는 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기
> [!div class="op_single_selector"]
> * [포털](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
> 
> 

Azure 포털 hello tooquickly Azure 미디어 서비스 (AMS) 계정을 만들어야 하는 방법을 제공 합니다. 사용자 계정 tooaccess toostore 있습니다를 사용 하도록 설정, 암호화, 인코딩, 관리 및 Azure에서 미디어 콘텐츠를 스트리밍하는 미디어 서비스를 사용할 수 있습니다. 미디어 서비스 계정을 만들면 hello 시간에도 연결 된 저장소 계정 만들기 (또는 기존 집합을 사용) hello에 미디어 서비스 계정 hello와 동일한 지리적 지역입니다.

이 문서는 몇 가지 일반적인 개념을 설명 하 고 hello Azure 포털으로 toocreate 미디어 서비스 계정 하는 방법을 보여 줍니다.

## <a name="concepts"></a>개념
미디어 서비스에 액세스하려면 다음 두 개의 관련 계정이 필요합니다.

* Media Services 계정. Azure에서 사용할 수 있는 사용자 계정에서는 미디어 서비스 클라우드 기반 tooa 집합을 액세스할 수 있는 합니다. 미디어 서비스 계정은 실제 미디어 콘텐츠를 저장하지 않습니다. 대신 사용자 계정에 hello 미디어 콘텐츠 및 작업을 처리 하는 미디어에 대 한 메타 데이터를 저장합니다. Hello 계정을 만들면 hello 시간에 사용 가능한 Media Services 지역을 선택 합니다. 선택한 hello 지역이 사용자 계정에 대 한 hello 메타 데이터 레코드를 저장 하는 데이터 센터입니다.
  
* Azure 저장소 계정. 저장소 계정은 hello에 있어야 hello 미디어 서비스 계정으로 동일한 지리적 지역입니다. Media Services 계정을 만들 때 기존 저장소 계정을 하거나 선택할 수 있습니다 hello에 동일한 지역 하거나 만들 수 있습니다 hello에 새 저장소 계정을 같은 지역입니다. 미디어 서비스 계정을 삭제 하면 관련 된 저장소 계정의 blob hello 삭제 되지 않습니다.

> [!NOTE]
> 다른 지역에서 Azure Media Services 기능의 사용 가용성에 대한 정보는 [데이터 센터에서 AMS 기능의 사용 가용성](scenarios-and-availability.md#availability)을 참조하세요.

## <a name="create-an-ams-account"></a>AMS 계정 만들기
이 hello 단계 섹션 표시 방법을 toocreate는 AMS 계정.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. **+새로 만들기** > **웹 + 모바일** > **Media Services**를 클릭합니다.
   
    ![미디어 서비스 만들기](./media/media-services-create-account/media-services-new1.png)
3. **미디어 서비스 계정 만들기** 에 필요한 값을 입력합니다.
   
    ![미디어 서비스 만들기](./media/media-services-create-account/media-services-new3.png)
   
   1. **계정 이름**, hello 새 AMS 계정의 hello 이름을 입력 합니다. 미디어 서비스 계정 이름이 모든 소문자 또는 공백 없이 숫자 하며 3 too24 자.
   2. 구독에 hello 각기 다른 Azure 구독에 대 한 액세스를 해야 하는 중에서 선택 합니다.
   3. **리소스 그룹**를 기존 또는 새 리소스를 hello 선택 합니다.  리소스 그룹은 수명 주기, 권한 및 정책을 공유하는 리소스의 컬렉션입니다. [여기](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
   4. **위치**, 선택 hello 사용된 toostore 미디어 서비스 계정에 대 한 미디어 및 메타 데이터 레코드 hello 될 지리적 지역입니다. 이 영역의 사용된 tooprocess 되며 여 미디어입니다. Hello 사용 가능한 미디어 서비스 영역 으로만 hello 드롭다운 목록 상자에 나타납니다. 
   5. **저장소 계정**, 미디어 서비스 계정에서 미디어 콘텐츠 hello 저장소 계정 tooprovide blob 저장소를 선택 합니다. Hello에 기존 저장소 계정을 선택할 수 있습니다 또는 미디어 서비스 계정와 동일한 지리적 지역에 저장소 계정을 만들 수 있습니다. 새 저장소 계정에에서 만들어집니다 hello 동일 지역입니다. 이름은 저장소 계정에 대 한 hello 규칙을 hello 미디어 서비스 계정 동일 합니다.
      
       저장소에 대한 자세한 내용은 [여기](../storage/common/storage-introduction.md)를 참조하세요.
   6. 선택 **Pin toodashboard** hello 계정 배포의 toosee hello 진행 상황입니다.
4. 클릭 **만들기** hello hello 양식 맨 아래에 있습니다.
   
    Hello 계정을 성공적으로 만들어지면 개요 페이지를 로드 합니다. Hello에서 스트리밍 끝점 테이블 hello 계정을 갖습니다 스트리밍 끝점 hello에 기본 **Stopped** 상태입니다. 

    >[!NOTE]
    >AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 
   
## <a name="toomanage-your-ams-account"></a>toomanage AMS 계정

toomanage AMS 계정 (예를 들어 toohello AMS API를 프로그래밍 방식으로 연결, 비디오를 업로드, 자산 인코딩, 콘텐츠 보호 구성, 작업 진행 상황을 모니터링) 선택 **설정을** hello hello 포털의 왼쪽에 있습니다. Hello에서 **설정**, tooone hello 사용할 수 있는 블레이드를 이동 (예: **API 액세스**, **자산**, **작업**, **콘텐츠 보호**).


## <a name="next-steps"></a>다음 단계

이제 AMS 계정에 파일을 업로드할 수 있습니다. 자세한 내용은 [파일 업로드](media-services-portal-upload-files.md)를 참조하세요.

Tooaccess AMS API를 프로그래밍 방식으로 계획 하는 경우 참조 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

