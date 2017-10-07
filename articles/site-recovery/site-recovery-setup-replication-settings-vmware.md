---
title: "Azure Site Recovery에 대 한 복제 설정을 aaaSet | Microsoft Docs"
description: "Toodeploy 사이트 복구 tooorchestrate 복제, 장애 조치 및 복구 VMM에서 Hyper-v Vm의 클라우드 tooAzure 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>VMware tooAzure에 대 한 복제 정책 관리


## <a name="create-a-replication-policy"></a>복제 정책 만들기

1. **관리** > **Site Recovery 인프라**를 선택합니다.
2. **VMware 및 실제 컴퓨터의 경우** 아래에서 **복제 정책**을 선택합니다.
3. **+ 복제 정책**을 선택합니다.

    ![복제 정책 만들기](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Hello 정책 이름을 입력 합니다.

5. **RPO 임계값**, hello RPO 제한을 지정 합니다. 연속 복제가 이 제한을 초과하면 경고가 생성됩니다.
6. **복구 지점 보존**, (시간) 지정 hello 각 복구 지점에 대 한 hello 보존 윈도의 기간입니다. 보호 된 컴퓨터 수 있는 보존 기간 내 tooany 데이터 요소를 복구 합니다.

    > [!NOTE]
    > 컴퓨터가 복제 된 toopremium 저장소에 대 한 too24 시간 보존을 모두 지원 합니다. 컴퓨터가 복제 된 toostandard 저장소에 대 한 too72 시간 보존을 모두 지원 합니다.

    > [!NOTE]
    > 장애 복구에 대한 복제 정책은 자동으로 생성됩니다.

7. **앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.

8. **확인**을 클릭합니다. hello 정책 30 too60 초 내에 만들어야 합니다.

![복제 정책 생성](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>복제 정책과 구성 서버 연결
1. Hello 복제 정책 toowhich 선택 tooassociate hello 구성 서버를 선택 합니다.
2. **연결**을 클릭합니다.
![구성 서버 연결](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. 서버 hello 목록에서 hello 구성 서버를 선택 합니다.
4. **확인**을 클릭합니다. 하나의 tootwo 분에서 hello 구성 서버를 연결 해야 합니다.

![구성 서버 연결](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>복제 정책 편집
1. Tooedit 복제 설정을 검색할 hello 복제 정책을 선택 합니다.
![복제 정책 편집](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. **설정 편집**을 클릭합니다.
![복제 정책 설정 편집](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. 필요에 따라 hello 설정을 변경 합니다.
4. **Save**를 클릭합니다. hello 정책 2 toofive 분 저장 하도록, Vm 수에 따라는 해당 복제 정책을 사용 하는 합니다.

![복제 정책 저장](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>복제 정책에서 구성 서버 분리
1. Hello 복제 정책 toowhich 선택 tooassociate hello 구성 서버를 선택 합니다.
2. **분리**를 클릭합니다.
3. 서버 hello 목록에서 hello 구성 서버를 선택 합니다.
4. **확인**을 클릭합니다. 하나의 tootwo 분에서 hello 구성 서버를 분리 해야 합니다.

    > [!NOTE]
    > Hello 정책을 사용 하 여 하나 이상의 복제 된 항목이 없는 경우 구성 서버를 분리할 수 없습니다. Hello 구성 서버를 분리 하기 전에 hello 정책을 사용 하 여 복제 된 항목이 없는 있는지 확인 합니다.

## <a name="delete-a-replication-policy"></a>복제 정책 삭제

1. Hello 복제 정책을 선택 toodelete 되도록 합니다.
2. **삭제**를 클릭합니다. hello 정책 30 too60 초 내에 삭제 해야 합니다.

    > [!NOTE]
    > 구성 서버가 연결 tooit 하나 이상 있는 경우에 복제 정책을 삭제할 수 없습니다. Hello 정책을 사용 하 여 복제 된 항목이 없습니다 및 hello 정책 삭제 하기 전에 구성 서버를 연결 된 모든 hello 삭제 있는지 확인 합니다.
