---
title: "StorSimple 저장소 계정 관리 | Microsoft Docs"
description: "StorSimple 관리자 구성 페이지를 사용하여 저장소 계정에 대한 보안 키를 추가, 편집, 삭제 또는 회전하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 68b767c9c93f2daff476a21029b9813f347590b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-storage-account"></a>StorSimple 관리자 서비스를 사용하여 저장소 계정 관리
## <a name="overview"></a>개요
**구성** 페이지는 StorSimple 관리자 서비스에서 만들 수 있는 모든 글로벌 서비스 매개 변수를 표시합니다. 이러한 매개 변수는 서비스에 연결된 모든 장치에 적용할 수 있으며 다음을 포함합니다.

* 저장소 계정 
* 대역폭 템플릿 
* 액세스 제어 레코드 

이 자습서에서는 **구성** 페이지를 사용하여 저장소 계정을 추가, 편집 또는 삭제하거나, 저장소 계정에 대한 보안 키를 회전하는 방법에 대해 설명합니다.

 ![구성 페이지](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

저장소 계정은 클라우드 서비스 공급자와 저장소 계정에 액세스하기 위해 장치가 사용하는 자격 증명을 포함합니다. Microsoft Azure 저장소 계정의 경우 계정 이름 및 기본 액세스 키와 같은 자격 증명이 있습니다. 

**구성** 페이지에서 청구 구독에 대해 만들어진 모든 저장소 계정이 다음 정보를 포함하여 테이블 형식으로 표시됩니다.

* **이름** – 만들어졌을 때 계정에 할당된 고유 이름입니다.
* **SSL 사용** – SSL 사용 및 장치와 클라우드 사이의 통신이 보안 채널을 통해 이루어지는지 여부입니다.
* **사용 볼륨** – 저장소 계정을 사용하는 볼륨의 수입니다.

저장소 계정 관련하여 **구성** 페이지에서 수행할 수 있는 가장 일반적인 작업은 다음과 같습니다.

* 저장소 계정 추가 
* 저장소 계정 편집 
* 저장소 계정 삭제 
* 저장소 계정의 키 회전 

## <a name="types-of-storage-accounts"></a>저장소 계정 유형
StorSimple 장치에서 사용할 수 있는 저장소 계정에는 다음과 같은 세 종류가 있습니다.

* **자동 생성된 저장소 계정** – 이름 제안 시, 서비스를 처음 만들 때 이 저장소 계정 유형이 자동으로 생성됩니다. 이 저장소 계정을 만드는 방법에 대해 자세히 알아보려면 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough.md)에서 [1단계: 새 서비스 만들기](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)를 참조하세요. 
* **서비스 구독의 저장소 계정** – 이러한 계정은 서비스와 동일한 구독과 연결된 Azure 저장소 계정입니다. 이러한 저장소 계정을 만드는 방법에 대해 더 알아보려면 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요. 
* **서비스 구독 외의 저장소 계정** - 이러한 계정은 서비스와 연결되지 않았고 서비스가 만들어지기 전에 존재했던 Azure 저장소 계정입니다.

## <a name="add-a-storage-account"></a>저장소 계정 추가
저장소 계정(지정된 클라우드 서비스 공급자를 통해)에 연결된 액세스 자격 증명 및 친숙한 고유 이름을 제공하여 저장소 계정을 추가할 수 있습니다. 장치와 클라우드 사이에서 네트워크 통신을 위한 보안 채널을 만들기 위해 SSL(Secure Sockets Layer) 모드를 사용하는 옵션도 있습니다.

특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다. 하지만 저장소 계정을 만든 후에는 클라우드 서비스 공급자를 변경할 수 없습니다.

저장소 계정을 저장하는 동안 해당 서비스는 클라우드 서비스 공급자와 통신을 시도합니다. 사용자가 지정한 자격 증명 및 액세스 자료가 이 때 인증됩니다. 인증에 성공하는 경우에만 저장소 계정이 만들어집니다. 인증에 실패하는 경우 그에 따른 오류 메시지가 표시됩니다.

Azure 포털에서 만든 Resource Manager 저장소 계정은 StorSimple에서도 지원됩니다. Resource Manager 저장소 계정은 볼륨 컨테이너를 만들려고 할 때 드롭다운 목록에서 선택할 수 있도록 표시되지 않으며, Azure 클래식 포털에서 만든 저장소 계정만 표시됩니다. 아래에 설명된 저장소 계정 추가 절차에 따라 Resource Manager 저장소 계정을 추가해야 합니다.

> [!NOTE]
> 저장소 계정을 추가하기 위한 절차는 사용하는 StorSimple 소프트웨어 버전에 따라 다릅니다. StorSimple 버전에 대한 올바른 절차를 수행해야 합니다.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>저장소 계정 편집
볼륨 컨테이너에서 사용되는 저장소 계정을 편집할 수 있습니다. 현재 사용 중인 저장소 계정을 편집할 경우 수정할 수 있는 유일한 필드는 저장소 계정에 대한 액세스 키입니다. 새 저장소 액세스 키를 제공할 수 있으며 업데이트된 설정을 저장할 수 있습니다.

#### <a name="to-edit-a-storage-account"></a>저장소 계정을 편집하려면
1. 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성**을 클릭합니다.
2. **저장소 계정 추가/편집**을 클릭합니다.
3. **저장소 계정 추가/편집** 대화 상자에서:
   
   1. **저장소 계정**드롭다운 목록에서 수정하려는 기존 계정을 선택합니다. 서비스를 처음 만들 때 자동으로 생성된 저장소 계정이 포함될 수도 있습니다.
   2. 필요에 따라 **SSL 모드 사용** 선택을 수정할 수 있습니다.
   3. 저장소 계정 액세스 키를 회전하도록 선택할 수 있습니다. 키 회전을 수행하는 방법에 대한 자세한 내용은 [저장소 계정의 키 회전](#key-rotation-of-storage-accounts) 을 참조하세요.
   4. 확인 아이콘 ![확인 아이콘](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) 을 클릭하여 설정을 저장합니다. 설정은 **구성** 페이지에서 업데이트됩니다. **저장** 을 클릭하여 새로 업데이트된 설정을 저장합니다.
      
      ![저장소 계정 편집](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>저장소 계정 삭제
> [!IMPORTANT]
> 볼륨 컨테이너에서 사용하지 않는 경우에만 저장소 계정을 삭제할 수 있습니다. 저장소 계정을 볼륨 컨테이너에서 사용 중인 경우 먼저 볼륨 컨테이너를 삭제하고 연결된 저장소 계정을 삭제합니다.
> 
> 

#### <a name="to-delete-a-storage-account"></a>저장소 계정을 삭제하려면
1. StorSimple 관리자 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성**을 클릭합니다.
2. 저장소 계정의 테이블 형식 목록에서 삭제하려는 계정을 마우스로 가리킵니다.
3. 삭제 아이콘(**x**)이 해당 저장소 계정의 맨 오른쪽 열에 표시됩니다. **x** 아이콘을 클릭하여 자격 증명을 삭제합니다.
4. 확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다. 테이블 형식 목록이 변경 내용을 반영하도록 업데이트됩니다.

## <a name="key-rotation-of-storage-accounts"></a>저장소 계정의 키 회전
보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다. 

> [!NOTE]
> 다음의 키 회전 정보 및 회전 절차는 Microsoft Azure 저장소 계정에만 적용 됩니다. 다른 클라우드 서비스 공급자를 사용하는 경우에 해당 공급자의 대시보드를 통해 저장소 계정 키를 관리할 수 있습니다.
> 
> 

각 Microsoft Azure 구독에 하나 이상의 연결된 저장소 계정을 만들 수 있습니다. 이러한 계정에 대한 액세스는 해당 저장소 계정에 대한 구독 및 액세스 키를 통해 제어됩니다. 

저장소 계정을 만들면 Microsoft Azure에서 두 개의 512비트 저장소 액세스 키를 생성합니다. 이 키는 저장소 계정에 액세스하는 경우 인증에 사용됩니다. 두 개의 저장소 액세스 키가 있으면 저장소 서비스나 해당 서비스에 대한 액세스에 중단 없이 키를 다시 생성할 수 있습니다. 현재 사용 중인 키는 *기본* 키이며 백업 키는 *보조* 키라고 합니다. Microsoft Azure StorSimple 장치가 클라우드 저장소 서비스 공급자에 액세스할 때 이러한 두 키 중 하나를 제공해야 합니다.

## <a name="what-is-key-rotation"></a>키 회전 정의
일반적으로 응용 프로그램은 데이터 액세스에 키 중 하나만 사용합니다. 특정 시간이 지나면 응용 프로그램이 두 번째 키를 사용하도록 전환할 수 있습니다. 두 번째 키로 응용 프로그램을 전환한 후 첫 번째 키를 사용 중지한 다음 새 키를 생성합니다. 이러한 방식으로 두 키를 사용하면 가동 중지 시간 없이 응용 프로그램이 데이터에 액세스할 수 있습니다.

저장소 계정 키는 항상 암호화된 형태로 서비스에 저장됩니다. 하지만 StorSimple 관리자 서비스를 통해 재설정할 수 있습니다. 서비스는 StorSimple 관리자 서비스를 처음 만들 때 생성한 기본 저장소 계정뿐 아니라 저장소 계정에서 만든 계정을 비롯하여 동일한 구독의 모든 저장소 계정에 대해 기본 키 및 보조 키를 가져올 수 있습니다. StorSimple 관리자 서비스는 Azure 클래식 포털에서 항상 이러한 키를 가져와 암호화된 방법으로 저장합니다.

## <a name="rotation-workflow"></a>회전 워크플로
Microsoft Azure 관리자가 저장소 계정에 직접 액세스하여(Microsoft Azure 저장소 서비스를 통해) 기본 키 또는 보조 키를 다시 생성하거나 변경할 수 있습니다. StorSimple 관리자 서비스는이 변경을 자동으로 표시하지 않습니다.

StorSimple 관리자 서비스에 변경을 알리려면 StorSimple 관리자 서비스에 액세스하고 저장소 계정에 액세스한 다음 기본 또는 보조 키(변경된 키에 따라 다름)를 동기화해야 합니다. 그러면 서비스는 최신 키를 가져오고 해당 키를 암호화하여 장치에 암호화된 키를 보냅니다.

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service-azure-only"></a>서비스와 동일한 구독에서 저장소 계정에 대한 키를 동기화하려면(Azure에만 해당)
1. **서비스** 페이지에서 **구성** 탭을 클릭합니다.
2. **저장소 계정 추가/편집**을 클릭합니다.
3. 대화 상자에서 다음을 수행합니다.
   
   1. 동기화하려는 키가 있는 저장소 계정을 선택합니다. 표시되면 저장소 계정 키가 암호화됩니다.
   2. StorSimple 관리자 서비스에서 이전에 Microsoft Azure 저장소 서비스에서 변경된 키를 업데이트해야 합니다. 기본 액세스 키가 변경(다시 생성)된 경우 **기본 키 동기화**를 클릭합니다. 보조키가 변경된 경우 **보조 키 동기화**를 클릭합니다.
      
      ![키 동기화](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a>서비스 구독 외의 저장소 계정에 대한 키를 동기화하려면
1. **서비스** 페이지에서 **구성** 탭을 클릭합니다.
2. **저장소 계정 추가/편집**을 클릭합니다.
3. 대화 상자에서 다음을 수행합니다.
   
   1. 업데이트하려는 액세스 키가 있는 저장소 계정을 선택합니다.
   2. StorSimple 관리자 서비스에서 저장소 액세스 키를 업데이트해야 합니다. 이 경우 저장소 액세스 키를 볼 수 있습니다. **저장소 계정 액세스 키**상자에 새 키를 입력합니다. 
   3. 변경 내용을 저장합니다. 이제 저장소 계정 액세스 키가 업데이트됩니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.
* [StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.

