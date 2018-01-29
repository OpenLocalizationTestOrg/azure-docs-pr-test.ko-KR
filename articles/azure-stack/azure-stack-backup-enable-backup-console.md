---
title: "관리 포털에서 Azure 스택에 대 한 백업을 사용 하도록 설정 | Microsoft Docs"
description: "오류가 발생 하는 경우 Azure 스택 복원할 수 있도록 관리 포털을 통해 인프라 백업 서비스를 설정 합니다."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 56C948E7-4523-43B9-A236-1EF906A0304F
ms.service: azure-stack
ms.workload: naS
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: mabrigg
ms.openlocfilehash: 456a0db9771f5963c8d4375d54a22257f6ca1c56
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="enable-backup-for-azure-stack-from-the-administration-portal"></a>관리 포털에서 Azure 스택에 대 한 백업을 사용 하도록 설정

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*

Azure 스택 백업을 생성할 수 있도록 관리 포털을 통해 인프라 백업 서비스를 활성화 합니다. 오류가 발생할 경우 환경을 복원 하는 이러한 백업을 사용할 수 있습니다.

> [!Note]  
> 콘솔을 통해 백업을 사용 하기 전에 백업 서비스를 구성 해야 합니다. PowerShell을 사용 하 여 백업 서비스를 구성할 수 있습니다. 자세한 내용은 참조 [PowerShell과 함께 Azure 스택에 대 한 백업 사용](azure-stack-backup-enable-backup-powershell.md)합니다.

## <a name="enable-backup"></a>백업을 사용 하도록 설정

1. 스택 Azure 관리 포털을 열고 [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external)합니다.
2. 선택 **더 많은 서비스** > **인프라 백업**합니다. 선택 **구성** 에 **인프라 백업** 블레이드입니다.

    ![Azure 스택-백업 컨트롤러 설정](media\azure-stack-backup\azure-stack-backup-settings.png)에서도 확인할 수 있습니다.

3. 경로를 입력는 **백업 저장소 위치**합니다. 에 대 한 별도 장치에서 호스팅되는 파일 공유의 경로를 범용 명명 규칙 (UNC) 문자열을 사용 합니다. UNC 문자열 공유 파일 또는 장치와 같은 리소스의 위치를 지정합니다. 서비스에 대 한 IP 주소를 사용할 수 있습니다. 재해 발생 후 백업 데이터의 가용성을 보장 하려면 장치의 별도 위치에 있어야 합니다.
    > [!Note]  
    > 사용자 환경에서 엔터프라이즈 환경에 Azure 스택 인프라 네트워크에서 이름 확인을 지 원하는 경우 IP 것이 아니라 FQDN을 사용할 수 있습니다.
4. 형식에서 **Username** 도메인과 사용자 이름을 사용 하 여 합니다. 예: `Contoso\administrator`
5. 형식에서 **암호** 사용자에 대 한 합니다.
5. 암호를 다시 한 번 입력 **암호 확인**합니다.
6. 에 미리 공유한 키를 제공 하는 **암호화 키** 상자입니다. 이 키를 사용 하 여 백업 파일이 암호화 됩니다. 이 키는 안전한 위치에 저장 했는지 확인 합니다. 를 처음으로이 키를 설정 하거나 나중에 키를 회전 후이 인터페이스에서이 키를 볼 수 없습니다. 사전 공유 키를 생성 하려면 명령에 대 한 스크립트에 따라 [PowerShell과 함께 Azure 스택에 대 한 백업 사용](azure-stack-backup-enable-backup-powershell.md#generate-a-new-encryption-key)합니다. 
7. 선택 **확인** 백업 컨트롤러 설정을 저장할 수 있습니다.

Azure 스택 도구를 다운로드 하 고 다음 PowerShell cmdlet을 실행 해야 백업을 실행 하려면 **시작 AzSBackup** Azure 스택 관리 노드에 있는 합니다. 자세한 내용은 참조 [Azure 스택 백업을](azure-stack-backup-back-up-azure-stack.md )합니다.

## <a name="next-steps"></a>다음 단계

 - 백업을 실행 방법을 설명 합니다. 참조 [Azure 스택 백업을](azure-stack-backup-back-up-azure-stack.md )합니다.
- 백업 실행 되었는지 확인 방법을 설명 합니다. 참조 [관리 포털에서 완료 된 확인 백업](azure-stack-backup-back-up-azure-stack.md )합니다.
