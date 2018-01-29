---
title: "Azure API 관리 정책 샘플 - 로깅을 위해 Stackify에 오류 보내기 | Microsoft Docs"
description: "Azure API 관리 정책 샘플 - 오류 로깅 정책을 추가하여 로깅을 위해 Stackify에 오류를 보내는 방법을 보여 줍니다."
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 34319e43789d0f2c7d3e48a0277926eb598e88fc
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2017
---
# <a name="send-errors-to-stackify-for-logging"></a>로깅을 위해 Stackify에 오류 보내기

이 문서에서는 오류 로깅 정책을 추가하여 로깅을 위해 Stackify에 오류를 보내는 방법을 설명하는 Azure API 관리 정책 샘플을 보여 줍니다. 정책 코드를 설정하거나 편집하려면 [정책 설정 또는 편집](../set-edit-policies.md)에 설명된 단계를 따릅니다. 다른 예제를 보려면 [정책 샘플](../policy-samples.md)을 참조하세요.

## <a name="policy"></a>정책

코드를 **on-error** 블록에 붙여넣습니다.

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Log errors to Stackify.policy.xml)]

## <a name="next-steps"></a>다음 단계

APIM 정책에 대해 자세히 알아보기:

+ [변환 정책](../api-management-transformation-policies.md)
+ [정책 샘플](../policy-samples.md)

