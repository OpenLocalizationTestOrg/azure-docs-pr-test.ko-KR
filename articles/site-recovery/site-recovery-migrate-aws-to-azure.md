---
title: "AWS tooAzure에서 Vm aaaMigrate | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 toomigrate 가상 컴퓨터가 실행 중에 Azure Site Recovery를 사용 하 여 웹 서비스 AWS (Amazon) tooAzure 합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>웹 서비스 AWS (Amazon) tooAzure Azure 사이트 복구에서 가상 컴퓨터 마이그레이션

이 문서에서는 toomigrate AWS Windows hello로 tooAzure 가상 컴퓨터 인스턴스 하는 방법을 설명 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

마이그레이션은 장애 조치 AWS tooAzure에서 효과적으로 합니다. 장애 복구 컴퓨터 tooAWS 없으며 지속적인 복제가 없습니다. 이 문서에서는 hello hello Azure 포털에서에서 마이그레이션 단계를 설명 하 고에 대 한 hello 지침에 따라 [물리적 컴퓨터 tooAzure 복제](site-recovery-vmware-to-azure.md)합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>지원되는 운영 체제

사이트 복구에 사용 되는 toomigrate EC2 인스턴스 hello 다음 운영 체제 중 하나를 실행 될 수 있습니다.

- Windows(64비트만 해당)
    - Windows Server 2008 R2 SP1+(Citrix PV 드라이버 또는 AWS PV 드라이버만 해당. **RedHat PV 드라이버를 실행하는 인스턴스가 지원되지 않습니다**)Windows Server 2012 Windows Server 2012 R2
- Linux(64비트만 해당)
    - Red Hat Enterprise Linux 6.7(HVM 가상화된 인스턴스만 해당)

## <a name="prerequisites"></a>필수 조건

이 배포에 대해 필요한 사항은 다음과 같습니다.

* **구성 서버**: hello 구성 서버와 Windows Server 2012 r 2를 실행 하는 An Amazon EC2 VM을 배포 합니다. 기본적으로 hello 다른 Azure Site Recovery 구성 요소 (프로세스 서버 및 마스터 대상 서버) 설치 된 hello 구성 서버를 배포할 때. 이 문서에서는 hello hello Azure 포털에서에서 마이그레이션 단계를 설명 하 고에 대 한 hello 지침에 따라 [자세한 정보](site-recovery-components.md)

* **EC2 인스턴스**: Amazon EC2 가상 컴퓨터 인스턴스를 원하는 toomigrate hello 합니다.

## <a name="deployment-steps"></a>배포 단계

1. Recovery Services 자격 증명 모음을 만듭니다.
2. hello EC2 인스턴스의 보안 그룹 구성 된 규칙 tooallow 통신 toodeploy hello 구성 서버 하려는 hello 인스턴스와 toomigrate, 원하는 hello EC2 인스턴스 사이 있어야 합니다.

3. Hello에 동일한 Amazon 가상 사설 클라우드 EC2 인스턴스로 ASR 구성 서버를 배포 합니다. Hello VMware 참조 실제 / 구성 서버 배포 요구 사항에 대 한 tooAzure 필수 구성 요소입니다.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  구성 서버에는 AWS에 배포 하 고 복구 서비스 자격 증명 모음에 등록 되 면 아래와 같이 hello 구성 서버 및 사이트 복구 인프라 프로세스 서버 표시 됩니다.

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Hello 구성 서버를 배포한 후 (것에 대 한 too15 minustes 걸릴 수도 있습니다 tooappear), toomigrate 원하는 hello Vm과 통신할 수 있는지 확인 합니다.

6. [복제 설정을 지정합니다](site-recovery-setup-replication-settings-vmware.md).

7. 복제를 사용 하도록 설정: hello toomigrate 원하는 Vm에 대 한 복제를 사용 하도록 설정 합니다. Hello EC2 콘솔에서 가져올 수 hello 개인 IP 주소를 사용 하 여 hello EC2 인스턴스를 검색할 수 있습니다.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Hello EC2 인스턴스를 보호 하 고 hello 복제 tooAzure 완료 되 면 [테스트 장애 조치 실행](site-recovery-test-failover-to-azure.md) toovalidate Azure에서 응용 프로그램의 성능입니다.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. AWS tooAzure에서 각 VM에 대 한 장애 조치를 실행 합니다. 필요에 따라 복구 계획을 만드는 하 고 AWS tooAzure에서 장애 조치 toomigrate 여러 가상 컴퓨터를 실행할 수 있습니다. [자세히 알아봅니다](site-recovery-create-recovery-plans.md) .

10. 마이그레이션에 대 한 장애 조치 toocommit이 필요는 없습니다. Hello 마이그레이션을 완료 옵션을 선택 하는 대신, 원하는 toomigrate 각 컴퓨터에 대 한 합니다. hello 마이그레이션을 완료 동작 hello 마이그레이션 프로세스를 완료 하 고, hello 컴퓨터에 대 한 복제를 제거, hello 컴퓨터에 대 한 청구 하는 사이트 복구를 중지 합니다.

    ![마이그레이션](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>다음 단계

- [마이그레이션된 컴퓨터 tooenable 복제 준비](site-recovery-azure-to-azure-after-migration.md) 재해 복구 요구에 따라 tooanother 영역입니다.
- [Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.
