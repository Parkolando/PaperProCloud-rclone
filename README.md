# PaperProCloud rclone

리디 페이퍼 프로(Android 4.4, ARMv7)용 [rclone](https://rclone.org) 빌드를 배포하는 저장소예요. 리디 페이퍼 프로 클라우드 확장이 클라우드 설정에서 rclone을 고를 때 [릴리스](https://github.com/Parkolando/PaperProCloud-rclone/releases)의 `rclone-armv7.gz`를 자동으로 내려받아요. 직접 받을 필요는 없어요.

## 원본과 다른 점

rclone v1.75.2의 진입점에 DNS 설정 한 가지만 더했어요. Android의 Go 정적 바이너리는 `/etc/resolv.conf`가 없어서 DNS 서버를 찾지 못하기 때문에, 환경 변수 `RCLONE_ANDROID_DNS`가 있으면 그 서버로 묻게 했어요(`main.go`).

## 빌드

Go 1.27.2 이상이 필요해요.

```powershell
.\build.ps1   # rclone-armv7, rclone-armv7.gz, SHA-256 출력
```

`GOOS=linux GOARCH=arm GOARM=7 CGO_ENABLED=0`, `-trimpath -buildvcs=false -ldflags "-s -w"`로 빌드해요. 확장은 압축을 푼 파일의 SHA-256이 자기가 아는 값과 같을 때만 설치해요.

## 라이선스

rclone은 Nick Craig-Wood와 기여자들의 프로그램이에요([MIT](LICENSE)). 이 저장소의 변경도 같은 MIT 라이선스예요. Go 표준 라이브러리는 [BSD 라이선스](Go-LICENSE.txt)예요.
