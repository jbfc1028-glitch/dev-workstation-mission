# Dev Workstation Mission

## 1. 프로젝트 개요

이 저장소는 개발 워크스테이션 구축 과제 결과물이다.  
터미널 기본 조작, 파일 권한, Docker 설치/운영, Dockerfile 기반 웹 서버 제작, 포트 매핑, 바인드 마운트, Docker 볼륨, Git/GitHub 연동을 실습하고 기록한다.

## 2. 실행 환경

| 항목 | 내용 |
|---|---|
| OS | Windows |
| Shell/Terminal | PowerShell, Git Bash |
| Editor | VSCode |
| Docker | 추후 기록 |
| Git | 추후 기록 |

## 3. 수행 항목 체크리스트

- [ ] 터미널 기본 조작
- [ ] 파일/디렉토리 권한 실습
- [ ] Docker 설치 점검
- [ ] Docker 기본 운영 명령
- [ ] hello-world 컨테이너 실행
- [ ] ubuntu 컨테이너 실습
- [ ] 포트 매핑 접속 확인
- [ ] Dockerfile 기반 커스텀 이미지 제작
- [ ] 바인드 마운트 반영 확인
- [ ] Docker 볼륨 영속성 확인
- [ ] G Git 설정
- [ ]itHub/VSCode 연동

## 4. 터미널 기본 조작 로그

작성 예정

## 5. 권한 실습

파일(`secret.txt`)과 디렉토리(`private-dir`)를 대상으로 권한 변경 명령을 실습했다.

### 실행 명령

```bash
cd permissions-practice
ls -la

touch secret.txt
mkdir -p private-dir
ls -l

chmod 600 secret.txt
chmod 700 private-dir
ls -l

chmod 644 secret.txt
chmod 755 private-dir
ls -l
```

### 실행 결과 요약

처음 `permissions-practice` 폴더 안에는 `secret.txt` 파일이 존재했다.

```text
-rw-r--r-- 1 user group 46 Nov 11 12:34 secret.txt
```

`touch secret.txt` 명령으로 파일의 수정 시간이 갱신되었고, `mkdir -p private-dir` 명령으로 디렉토리를 생성했다.

```text
drwxr-xr-x 1 user group  0 Nov 11 12:48 private-dir/
-rw-r--r-- 1 user group 46 Nov 11 12:48 secret.txt
```

이후 다음 명령으로 권한 변경을 시도했다.

```bash
chmod 600 secret.txt
chmod 700 private-dir
```

예상되는 권한 변화는 다음과 같다.

| 대상 | 명령 | 예상 권한 | 의미 |
|---|---|---|---|
| `secret.txt` | `chmod 600 secret.txt` | `rw-------` | 소유자만 읽기/쓰기 가능 |
| `private-dir` | `chmod 700 private-dir` | `rwx------` | 소유자만 접근 가능 |

하지만 Windows Git Bash 환경에서 실행한 결과, `ls -l` 출력은 다음과 같이 기존 권한 표시와 동일하게 나타났다.

```text
drwxr-xr-x 1 user group  0 Nov 11 12:48 private-dir/
-rw-r--r-- 1 user group 46 Nov 11 12:48 secret.txt
```

마지막으로 권한을 일반적인 기본 권한 형태로 되돌리는 명령을 실행했다.

```bash
chmod 644 secret.txt
chmod 755 private-dir
```

최종 출력은 다음과 같았다.

```text
drwxr-xr-x 1 user group  0 Nov 11 12:48 private-dir/
-rw-r--r-- 1 user group 46 Nov 11 12:48 secret.txt
```

### 권한 해석

| 권한 | 의미 |
|---|---|
| `600` | 소유자만 읽기/쓰기 가능 |
| `644` | 소유자는 읽기/쓰기, 그룹과 기타 사용자는 읽기 가능 |
| `700` | 소유자만 읽기/쓰기/실행 가능 |
| `755` | 소유자는 읽기/쓰기/실행, 그룹과 기타 사용자는 읽기/실행 가능 |

### 정리

- `chmod 600 secret.txt`와 `chmod 700 private-dir` 명령을 실행했다.
- 그러나 Windows Git Bash 환경에서는 `chmod` 결과가 `ls -l` 출력에 기대한 형태로 반영되지 않았다.
- 이는 Windows의 파일 시스템 권한 처리 방식과 Git Bash의 권한 표시 방식이 Linux 환경과 다를 수 있기 때문이다.
- 권한 명령의 의미는 이해했고, `600`, `644`, `700`, `755`의 차이를 정리했다.
## 6. Docker 설치 및 점검

작성 예정

## 7. Docker 기본 운영 명령

작성 예정

## 8. Dockerfile 기반 웹 서버

작성 예정

## 9. 바인드 마운트 실습

작성 예정

## 10. Docker 볼륨 영속성 검증

작성 예정

## 11. Git 설정 및 GitHub/VSCode 연동

작성 예정

## 12. 트러블슈팅

### 문제 1. chmod 실행 후 권한 표시가 바뀌지 않음

#### 문제 상황

`chmod 600 secret.txt`, `chmod 700 private-dir` 명령을 실행했지만 `ls -l` 결과에서 권한 표시가 바뀌지 않았다.

```bash
chmod 600 secret.txt
chmod 700 private-dir
ls -l
```

실행 결과는 다음과 같이 기존 권한과 동일하게 표시되었다.

```text
drwxr-xr-x 1 user group  0 Nov 11 12:48 private-dir/
-rw-r--r-- 1 user group 46 Nov 11 12:48 secret.txt
```

#### 원인

Windows Git Bash 환경에서는 Linux와 달리 `chmod` 명령의 결과가 `ls -l` 출력에 그대로 반영되지 않을 수 있다.  
Windows의 NTFS 권한 체계와 Linux의 권한 체계가 다르기 때문이다.

#### 해결 및 정리

권한 변경 명령 자체는 실습했고, 각 권한 숫자의 의미를 정리했다.

- `600`: 소유자만 읽기/쓰기 가능
- `644`: 소유자는 읽기/쓰기, 나머지는 읽기 가능
- `700`: 소유자만 읽기/쓰기/실행 가능
- `755`: 소유자는 읽기/쓰기/실행, 나머지는 읽기/실행 가능

Windows Git Bash에서는 출력이 기대와 다를 수 있으므로, 실습 결과에는 실제 출력과 함께 환경 차이를 기록했다.

## 13. 학습 내용 정리

작성 예정