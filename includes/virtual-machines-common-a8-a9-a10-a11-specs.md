

## <a name="deployment-considerations"></a>배포 고려 사항
* **Azure 구독** – 몇 가지 계산 집약적인 인스턴스를 둘 이상의 toodeploy 종 량 제 구독 또는 기타 구입 옵션을 고려 합니다. [Azure 무료 계정](https://azure.microsoft.com/free/)을 사용하는 경우, 제한된 수의 Azure 계산 코어만 사용할 수 있습니다.

* **가격 및 가용성** -이러한 VM 크기 hello 표준 가격 책정 계층에만 제공 됩니다. Azure 지역에서 사용할 수 있는 제품에 대해서는 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 확인하세요. 
* **코어 할당량** – hello 기본값에서 Azure 구독에서 tooincrease hello 코어 할당량을 할 수 있습니다. 구독은 hello hello H 시리즈를 포함 하 여 특정 VM 크기 제품군에서 배포할 수 있는 코어 수가 제한도 될 수 있습니다. toorequest 할당량 증가 [온라인 고객 지원 요청을 개시](../articles/azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다. (기본 제한은 구독 범주에 따라 달라질 수 있습니다.)
  
  > [!NOTE]
  > 대규모 용량이 필요한 경우 Azure 지원에 문의합니다. Azure 할당량은 신용 제한이며 용량 보증이 아닙니다. 할당량에 관계 없이 사용하는 코어에 대해서만 요금이 청구됩니다.
  > 
  > 
* **가상 네트워크** – Azure는 [가상 네트워크](https://azure.microsoft.com/documentation/services/virtual-network/) 필요 하지 않음 toouse hello 계산 집약적인 인스턴스는 합니다. 그러나 대부분의 배포에 대 한 최소한 클라우드 기반의 Azure 가상 네트워크에서 필요한 또는 tooaccess 해야 하는 경우에 사이트 간 연결 온-프레미스 리소스. 필요에 따라 새 가상 네트워크를 toodeploy hello 인스턴스를 만듭니다. 계산 집약적인 Vm tooa 가상 네트워크는 선호도 그룹에 추가 하는 것은 지원 되지 않습니다.
* **크기 조정** –의 특수 한 하드웨어 인해만 크기를 조정할 수 계산 집약적인 인스턴스 hello 내에서 동일한 제품군 (H 시리즈 또는 계산 집약적인 A 시리즈) 크기입니다. 예를 들어 H 시리즈 크기 tooanother 하나를 사용 하는 H 시리즈 VM 조정할 수 있습니다. 또한 계산 집약적인 비 크기 tooa 계산 집약적인 크기에서 크기 조정도 지원 되지 않습니다.  
