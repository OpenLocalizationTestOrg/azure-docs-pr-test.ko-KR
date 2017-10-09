> [!NOTE]
> * hello VPN 게이트웨이 공용 IP 주소는 이전 SKU tooa에서 마이그레이션할 때 변경 됩니다 새로운 SKU입니다.
> * 클래식 VPN 게이트웨이 toohello 마이그레이션할 수 없는 새 Sku입니다. 클래식 VPN 게이트웨이에 사용할 수 있음 hello (이전) 레거시 Sku입니다.
> 

Azure VPN의 크기를 조정할 수 없는 이전 Sku hello와 새 SKU 제품군 hello 간 게이트웨이 합니다. Toohello를 마이그레이션할 수 hello hello Sku의 이전 버전을 사용 하는 hello 리소스 관리자 배포 모델에서 VPN 게이트웨이 사용 하도록 설정한 경우 새 Sku입니다. toomigrate, 가상 네트워크에 대 한 hello 기존 VPN 게이트웨이 삭제 하면 새로 만듭니다.

마이그레이션 워크플로:

1. 모든 연결 toohello 가상 네트워크 게이트웨이 제거 합니다.
2. Hello 이전 VPN 게이트웨이 삭제 합니다.
3. Hello 새 VPN 게이트웨이 만듭니다.
4. Hello 새 VPN 게이트웨이 IP 주소 (사이트 간 연결의 경우)을 온-프레미스 VPN 장치를 업데이트 합니다.
5. Hello toothis 게이트웨이 연결할 모든 VNet 대 VNet 로컬 네트워크 게이트웨이에 대해 게이트웨이 IP 주소 값을 업데이트 합니다.
6. 이 VPN 게이트웨이 통해 toohello 가상 네트워크를 연결 하는 P2S 클라이언트에 대 한 새 클라이언트 VPN 구성 패키지를 다운로드 합니다.
7. Hello 연결 toohello 가상 네트워크 게이트웨이 다시 만듭니다.
