---
title: "aaaAzure 클라우드 셸 (미리 보기) 개요 | Microsoft Docs"
description: "Azure 클라우드 셸 hello 간략하게 설명 합니다."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Azure Cloud Shell(미리 보기) 개요
Azure Cloud Shell은 Azure 리소스를 관리하기 위한 브라우저에서 액세스할 수 있는 대화형 셸입니다.

![](media/overview-pic.png)

## <a name="features"></a>기능
### <a name="browser-based-shell-experience"></a>브라우저 기반 셸 환경
셸 수 있도록 액세스 tooa 브라우저 기반 명령줄 환경을 Azure 관리 작업을 고려를 사용 하 여 빌드한 클라우드입니다. Hello 클라우드만 제공할 수 방식으로 로컬 컴퓨터에서 제한 되지 않는 클라우드 셸 toowork를 활용 합니다.

### <a name="pre-configured-azure-workstation"></a>Azure 미리 구성된 워크스테이션
사용자가 더 빠르게 작업할 수 있도록 Cloud Shell은 널리 사용되는 명령줄 도구 및 언어 지원이 미리 설치되어 제공됩니다.

[보기 hello 전체 도구 목록 Azure 클라우드 셸용 여기입니다.](features.md#tools)

### <a name="automatic-authentication"></a>자동 인증
클라우드 셸을 안전 하 게 Azure CLI 2.0 hello 통해 즉시 액세스 tooyour 리소스에 대 한 각 세션에서 자동으로 인증합니다.

### <a name="connect-your-azure-file-storage"></a>Azure File Storage 연결
클라우드 셸 컴퓨터 임시 되며 결과적으로 Azure 파일 공유 toobe로 탑재 해야 `clouddrive` toopersist $Home 디렉터리입니다.
첫 번째 실행에서 클라우드 셸 메시지 toocreate 사용자 대신 리소스 그룹, 저장소 계정 및 파일 공유를 표시 합니다. 이는 일회성 단계이며 모든 세션에서 자동으로 연결됩니다. 

#### <a name="create-new-storage"></a>새 저장소 만들기
![](media/basic-storage.png)

Azure 파일 공유를 사용하여 기본 5GB 디스크 이미지를 포함하는 LRS(로컬 중복 저장소) 계정이 자동으로 만들어질 수 있습니다. hello 파일 공유로 탑재할 `clouddrive` 파일에 대 한 공유 hello 디스크 이미지와의 상호 작용 사용된 toosync 되 고 $Home 디렉터리를 유지 합니다. 일반 저장소 비용이 적용됩니다.

세 가지 리소스가 자동으로 만들어집니다.
1. 리소스 그룹: `cloud-shell-storage-<region>`
2. 저장소 계정: `cs<uniqueGuid>`
3. 파일 공유: `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> SSH 키와 같이 $Home 디렉터리의 모든 파일은 탑재된 파일 공유에 저장된 사용자 디스크 이미지에서 유지됩니다. $Home 디렉터리 및 탑재된 파일 공유에서 파일을 저장하는 경우 모범 사례를 적용합니다.

#### <a name="use-existing-resources"></a>기존 리소스 사용
![](media/advanced-storage.png)

고급 옵션에는 가능 하면 tooassociate 기존 리소스 tooCloud 셸도 제공 됩니다. Hello 저장소 설정 프롬프트가 나타나면 "Show advanced settings" tooselect 추가 옵션을 클릭 합니다. 드롭다운이 필터링되면서 할당된 Cloud Shell 하위 지역 및 로컬/전역 중복 저장소 계정이 표시됩니다.

[Cloud Shell 저장소, 파일 공유 업데이트 및 파일 업로드/다운로드에 대해 자세히 알아봅니다.](persisting-shell-storage.md)

## <a name="concepts"></a>개념
* Cloud Shell은 세션 별, 사용자 단위 기준으로 제공된 임시 컴퓨터에서 실행됩니다.
* Cloud Shell은 대화형 작업 없이 20분 후에 시간이 초과됩니다.
* Cloud Shell은 첨부된 파일 공유를 사용하여 액세스할 수 있습니다.
* Cloud Shell은 사용자 계정 별로 하나의 컴퓨터를 할당합니다.
* 사용 권한은 일반적인 Linux 사용자로 설정됩니다.

[Cloud Shell의 모든 기능에 대해 자세히 알아봅니다.](features.md)

## <a name="examples"></a>예
* 만들기 또는 편집 스크립트 tooautomate Azure 관리
* Azure Portal 및 Azure CLI 2.0을 통해 리소스를 동시에 관리합니다.
* Azure CLI를 2.0을 사용해 보세요.

[Hello 셸 클라우드 빠른 시작에서 이러한 모든 예를 사용 합니다.](quickstart.md)

## <a name="pricing"></a>가격
클라우드 셸을 호스트 하는 hello 컴퓨터는 무료, 탑재 된 Azure 파일의 필수 공유 toopersist $Home 디렉터리입니다. 일반 저장소 비용이 적용됩니다.

## <a name="supported-browsers"></a>지원되는 브라우저
Cloud Shell은 Chrome, Edge 및 Safari에 권장됩니다. 클라우드 Shell은 Chrome, Firefox, Safari, IE, 및 가장자리에 대 한 지원 되지만, 클라우드 셸은 주체 toospecific 브라우저 설정입니다.

## <a name="troubleshooting"></a>문제 해결
1. Azure Active Directory 구독을 사용할 경우 저장소를 만들 수 없는 경우 due tooError: 400 DisallowedOperation 합니다. tooresolve이 저장소 리소스를 만들 수 있는 Azure 구독을 사용 하십시오. AD 구독 수 없습니다. toocreate Azure 리소스가 있습니다.

알려진 특별한 제한 사항은 [Cloud Shell 제한 사항](limitations.md)을 방문하세요.
