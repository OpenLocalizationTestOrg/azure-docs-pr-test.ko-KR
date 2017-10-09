---
title: "hello Azure 포털에서에서 함수 앱 aaaCreate | Microsoft Docs"
description: "Azure 앱 서비스의 hello 포털에서 새 함수 응용 프로그램을 만듭니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Hello Azure 포털에서에서 함수 응용 프로그램 만들기

Azure 기능 앱 hello Azure 앱 서비스 인프라를 사용 합니다. 이 항목에서는 toocreate hello Azure 포털에서에서 함수 앱. 함수 응용 프로그램은 개별 함수의 hello 실행을 호스팅하는 hello 컨테이너입니다. Hello 호스팅 앱 서비스 계획에서에서 함수 응용 프로그램을 만들 때 함수 앱 응용 프로그램 서비스의 모든 hello 기능을 사용할 수 있습니다.

## <a name="create-a-function-app"></a>함수 앱 만들기

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

함수 앱을 만들 때 문자, 숫자 및 하이픈만 포함할 수 있는 유효한 **앱 이름**을 제공해야 합니다. 밑줄(**_**)은 허용되는 문자가 아닙니다.

저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다. 저장소 계정 이름은 Azure 내에서 고유해야 합니다. 

Hello 함수 앱을 만든 후에 하나 이상의 다른 언어에서는 개별 함수를 만들 수 있습니다. 함수를 만들 [hello 포털을 사용 하 여](functions-create-first-azure-function.md#create-function), [연속 배포](functions-continuous-deployment.md), 또는 [FTP로 업로드](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)합니다.

## <a name="service-plans"></a>서비스 계획

Azure Functions에는 소비 계획 및 App Service 계획이라는 두 가지 서비스 계획이 있습니다. hello 소비 계획 코드가 실행 되는 경우 필요한 toohandle 부하로 눈금 아웃 한 다음 눈금-코드 실행 중이지 않을 때 계산 능력을 자동으로 할당 합니다. 앱 서비스 계획 hello 함수 앱 서비스 앱 액세스 tooall hello 기능을 제공합니다. 함수 앱이 만들어지면 서비스 계획을 선택해야 하며 현재는 변경할 수 없습니다. 자세한 내용은 [Azure Functions 호스팅 계획 선택](functions-scale.md)을 참조하세요.

앱 서비스 계획에 toorun JavaScript 함수를 계획 하는 경우 더 적은 코어를 사용 하 여 계획을 선택 해야 합니다. 자세한 내용은 참조 hello [함수에 대 한 JavaScript 참조](functions-reference-node.md#choose-single-core-app-service-plans)합니다.

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>저장소 계정 요구 사항

앱 서비스에서 함수 응용 프로그램을 만들 때 만들거나 해야 Blob, 큐 및 테이블 저장소 지 원하는 tooa 범용 하는 Azure 저장소 계정을 연결 합니다. 내부적으로 함수는 트리거 관리 및 함수 실행 로깅 등의 작업을 위해 Storage를 사용합니다. Blob 전용 저장소 계정, Azure Premium Storage 및 ZRS 복제를 포함한 범용 저장소 계정과 같은 일부 저장소 계정은 큐 및 테이블을 지원하지 않습니다. 이러한 계정은 함수 응용 프로그램을 만들 때의 저장소 계정 블레이드 hello에서에서 필터링 됩니다.

>[!NOTE]
>Hello 소비 호스팅 계획을 사용할 경우 함수 코드와 바인딩 구성 파일 hello 주 저장소 계정에서 Azure 파일 저장소에 저장 됩니다. Hello 주 저장소 계정을 삭제 하면이 콘텐츠는 삭제 되 고 복구할 수 없습니다.

저장소 계정 유형에 대 한 자세한 정보는 toolearn 참조 [hello Azure 저장소 서비스 소개](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)합니다. 

## <a name="next-steps"></a>다음 단계

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



