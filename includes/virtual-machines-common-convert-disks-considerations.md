
* hello 변환 hello VM의 다시 시작이 필요한, 하므로 기존 유지 관리 기간 중에 Vm의 hello 마이그레이션을 예약 합니다. 

* hello 변환 반환 하지 않습니다. 

* 있는지 tootest hello 변환 되어야 합니다. 프로덕션 환경에서 hello 마이그레이션을 수행 하기 전에 테스트 가상 컴퓨터를 마이그레이션하십시오.

* Hello 변환 하는 동안 VM hello 할당 취소 합니다. hello VM hello 변환 후에 시작 될 때 새 IP 주소를 받습니다. 필요한 경우 다음을 할 수 있습니다 [고정 IP 주소 할당](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello VM입니다.

* hello 원래 Vhd 및 변환 하기 전에 hello VM에서 사용 하는 hello 저장소 계정 삭제 되지 않습니다. Tooincur 요금이 계속 있습니다. 이러한 아티팩트에 대 한 요금이 청구 되 tooavoid hello 변환 완료 되었는지 확인 한 후 hello 원래 VHD blob을 삭제 합니다.
