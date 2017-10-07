---
title: "Linux 용 AAD에서 회사 또는 학교 id aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Linux 가상 컴퓨터와 Azure Active Directory toouse에 회사 또는 학교 id입니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a>회사 또는 학교 id를 Azure Active Directory toouse Linux vm에서 만들기
있고 사용 hello MSDN Azure 크레딧-활용 Azure 계정 tootake hello를 만든 개인 Azure 계정 키를 만들거나 개인 MSDN 구독이 있는 경우는 *Microsoft 계정* identity toocreate 것입니다. -Azure의 많은 뛰어난 기능 [리소스 그룹 템플릿](../../azure-resource-manager/resource-group-overview.md) -한 가지 예는 회사 또는 학교 계정 (Azure Active Directory에서 관리 하는 id)를 필요한 toowork 합니다. 다행히 새 회사 또는 학교 toocreate를 사용할 수 있는 기본 Azure Active Directory 도메인으로 제공 되 hello 개인 Azure 계정에 대 한 가장 큰 이점 중 하나 때문에, 새 회사 또는 학교 계정 toocreate 아래 hello 지침을 따를 수 있습니다. 필요로 하는 Azure 기능과 함께 사용할 수 있는 계정입니다.

그러나 최근 변경 내용을 쉽게 가능한 toomanage hello를 사용 하 여 Azure 계정 유형으로 구독 `azure login` 설명 하는 대화형 로그인 방법을 [여기](../../xplat-cli-connect.md)합니다. 해당 메커니즘을 사용할 수 있습니다 또는 hello 설명 하는 지침을 따라야 합니다. 수도 있습니다 [Windows Vm과 Azure Active Directory toouse에 회사 또는 학교 id를 만들](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

