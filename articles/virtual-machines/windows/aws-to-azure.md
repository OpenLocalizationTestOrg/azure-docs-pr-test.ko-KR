---
title: Windows AWS Vm tooAzure aaaMove | Microsoft Docs
description: "웹 서비스 AWS (Amazon) EC2 Windows 인스턴스 tooAzure Azure PowerShell을 사용 하 여 가상 컴퓨터를 이동 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>PowerShell을 사용 하 여 웹 서비스 AWS (Amazon) tooAzure에서 Windows VM 이동

프로그램 워크 로드를 호스트에 대 한 Azure 가상 컴퓨터를 평가 하는 경우 기존 웹 서비스 AWS (Amazon) EC2 Windows VM 인스턴스를 내보내려면 다음 hello 가상 하드 디스크 (VHD) tooAzure 업로드할 수 있습니다. 한 번 hello VHD 업로드, 만들 수 있습니다는 새 VM Azure의 hello VHD에서. 

이 항목에서 AWS tooAzure 단일 VM 이동에 대해 설명 합니다. 최대 규모로 AWS tooAzure toomove Vm 참조 [서비스 AWS (Amazon Web) tooAzure Azure 사이트 복구에서 가상 컴퓨터를 마이그레이션할](../../site-recovery/site-recovery-migrate-aws-to-azure.md)합니다.

## <a name="prepare-hello-vm"></a>Hello VM 준비 
 
일반화 된 만들고 특수화할 Vhd tooAzure 업로드할 수 있습니다. 각 유형에 AWS에서 내보내기 전에 hello VM을 준비 해야 합니다. 

- **일반화된 VHD** - 일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다. Toouse hello VHD 이미지 toocreate로 가져오려는 경우에서 새 Vm을 수행 해야 합니다. 
 
    * [Windows VM을 준비합니다](prepare-for-upload-vhd-image.md).  
    * Sysprep를 사용 하 여 hello 가상 컴퓨터를 일반화 합니다.  

 
- **VHD를 특수화할** -특수 VHD hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 관리 합니다. Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다.  
    * [Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md)합니다. **없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다. 
    * 모든 게스트 가상화 도구와 hello (즉, VMware 도구)를 VM에 설치 된 에이전트를 제거 합니다. 
    * Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다. 이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다.  


## <a name="export-and-download-hello-vhd"></a>내보내기 및 hello VHD를 다운로드 합니다. 

Hello EC2 인스턴스 tooa Amazon S3 버킷에서 VHD를 내보냅니다. Hello Amazon 설명서 항목에 설명 된 hello 단계에 따라 [인스턴스도는 VM 사용 하 여 VM 가져오기/내보내기 내보내기](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) 및 실행된 hello [-인스턴스-내보내기-작업 만들기](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) 명령 tooexport hello EC2 인스턴스 tooa VHD 파일입니다. 

hello 내보낸된 VHD 파일에에서 저장 됩니다 hello Amazon S3 버킷을 지정 합니다. hello 기본 구문 미만인 내보내는 hello VHD에 대 한 바꾸면 hello 자리 표시자 텍스트에 <brackets> 정보를 사용 합니다.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Hello VHD를 내보낸 후 hello 지침에 따라 [다운로드 하는 방법 개체 S3 버킷을에서?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello S3 버킷을에서 toodownload hello VHD 파일입니다. 

> [!IMPORTANT]
> AWS는 hello VHD를 다운로드 하기 위한 데이터 전송 요금이 청구 합니다. 자세한 내용은 [Amazon S3 요금](https://aws.amazon.com/s3/pricing/)을 참조하세요.


## <a name="next-steps"></a>다음 단계

이제 hello VHD tooAzure 업로드 하 고 새 VM을 만들 수 있습니다. 

- 너무 소스에서 Sysprep을 실행 한 경우**일반화** 참조 내보내기 전에 [일반화 된 VHD를 업로드 하 고 Azure에서 새 Vm toocreate 사용](upload-generalized-managed.md)
- 내보내기 전에 Sysprep를 실행 하지 않은 경우 hello VHD 것으로 간주 됩니다 **특수**, 참조 [특수 VHD tooAzure 업로드 하 고 새 VM 만들기](create-vm-specialized.md)

 
