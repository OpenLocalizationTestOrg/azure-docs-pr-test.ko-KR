---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-개요 aaaSQL | Microsoft Docs"
description: "이 문서에서는 Azure Virtual Machines의 SQL Server 가용성 그룹을 소개합니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Azure Virtual Machines의 SQL Server Always On 가용성 그룹 소개 #

이 문서에서는 Azure Virtual Machines의 SQL Server 가용성 그룹을 소개합니다. 

Always On 가용성 그룹에 Azure 가상 컴퓨터는 온-프레미스 가용성 그룹에 비슷한 tooAlways 합니다. 자세한 내용은 [Always On 가용성 그룹(SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요. 

hello 다이어그램 hello 부분의 전체 SQL Server 가용성 그룹에서 Azure 가상 컴퓨터를 보여 줍니다.

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

hello 주요 차이점 Azure 가상 컴퓨터의 가용성 그룹은 Azure 가상 컴퓨터는 hello에 대 한 요구는 [부하 분산 장치](../../../load-balancer/load-balancer-overview.md)합니다. hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 보유합니다. 가용성 그룹을 여러 개 있는 경우 그룹마다 수신기가 필요합니다. 하나의 부하 분산 장치가 여러 수신기를 지원할 수 있습니다.

Azure 가상 컴퓨터에는 SQL Server 가용성 aroup 준비 toobuild 러 우면 toothese 자습서를 참조 하십시오.

## <a name="automatically-create-an-availability-group-from-a-template"></a>템플릿에서 자동으로 가용성 그룹 만들기

[자동으로 Azure VM의 Always On 가용성 그룹 구성 - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Azure Portal에서 수동으로 가용성 그룹 만들기

또한 직접 만들 수 있습니다 hello 가상 컴퓨터 hello 서식 파일 없이 합니다. 먼저 hello 필수 다음 hello 가용성 그룹을 만듭니다. Hello 다음 항목을 참조 하십시오. 

- [Azure Virtual Machines의 SQL Server Always On 가용성 그룹에 대한 필수 구성 요소 구성](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [만들 Always On 가용성 그룹 tooimprove 고가용성 및 재해 복구](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>다음 단계

[다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-availability-group-dr.md).
