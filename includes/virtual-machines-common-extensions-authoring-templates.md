## <a name="overview-of-azure-resource-manager-templates"></a>Azure 리소스 관리자 템플릿 개요
Azure 리소스 관리자 템플릿을 사용 하면 toodeclaratively Json 언어에서 리소스 간의 종속성 hello를 정의 하 여 hello Azure IaaS 인프라를 지정 합니다. Azure 리소스 관리자 템플릿 자세한 개요는 다음 toohello 문서를 참조 하십시오.

[리소스 그룹 개요](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>VM 확장에 대한 샘플 템플릿 코드 조각
Azure 리소스 관리자 템플릿 부분 만들어야 하는 대로 VM 확장을 배포 toodeclaratively hello 확장 구성 hello 서식 파일에 지정 합니다.
다음은 확장 구성 hello를 지정 하는 hello 형식입니다.

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

위의 hello 알 수 있듯이 hello 확장 템플릿이 두 주요 부분을 포함 되어 있습니다.

1. 확장 이름, 게시자 및 버전
2. 확장 구성

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Hello 게시자, 형식 및 모든 확장에 대 한 typeHandlerVersion 식별
Azure VM 확장은 Microsoft에서 게시 하 고 신뢰할 수 있는 3rd 파티 게시자 및 각 확장의 게시자, 유형 및 hello typeHandlerVersion으로 고유 하 게 식별 합니다. 다음과 같이 결정될 수 있습니다.  

