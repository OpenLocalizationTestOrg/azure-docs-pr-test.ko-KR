Hello를 사용 하 여 연결 성공 했는지를 확인할 수 있습니다 [az 네트워크 vpn 연결 표시](/cli/azure/network/vpn-connection#show) 명령입니다. Hello 예에서 '-이름 ' tootest hello 연결의 toohello 이름을 참조 합니다. Hello 연결이 설정 되 고 hello 프로세스의 경우 연결 상태에 '연결' 보여 줍니다. Hello 상태가 변경 too'Connected hello 연결이 설정 되 면 '.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

