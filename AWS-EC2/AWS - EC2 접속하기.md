# AWS - EC2 원격 접속하기
AWS - EC2 터미널에서 원격 접속하는 방법\
`os: 리눅스`
```Bash
sudo chmod 400 (AWS 키 페어 경로)
```

```Bash
ssh -i (AWS 키 페어 경로) ubuntu@(EC2 IP주소)
```

