---
title: "[Linux Commands] 40 Essential Linux Commands"
excerpt: "자주 사용하는 리눅스 커맨드 알아보기"
date: 2023-6-27
last_modified_at: 2023-6-27
categories:
  - essay
tags:
  - handy-function
  - linux
  - commands
---

## 0. What Is a Linux Command?

**`Linux Command`는 텍스트 및 프로세스를 통해 시스템과 상호 작용하는 콘솔인 `CLI`에서 실행되는 프로그램 또는 유틸리티이다.** Windows의 `Command Prompt` 응용 프로그램과 유사하다.

줄 끝에서 `Enter` 키를 누르면, Linux 명령이 터미널에서 실행된다. 패키지 설치에서 사용자 관리 및 파일 조작에 이르기까지 다양한 작업을 수행하는 명령을 실행할 수 있다.

Linux 명령의 일반 구문은 다음과 같다.

```console
CommandName [option(s)] [parameter(s)]
```

`command`에는 `option`이나 `parameter`가 포함될 수 있다. 어떤 경우에는 그것들 없이도 여전히 실행될 수 있다. command의 가장 일반적인 세 부분은 다음과 같다.

* `CommandName`은 수행하려는 규칙이다.
* `Option` or `flag`는 command의 작업을 수정한다. 이를 호출하려면, `hyphens (-)` 또는 `double hyphens (--)`를 사용한다.
* `Parameter` or `argument`는 command에 필요한 정보를 지정한다.

모든 Linux command는 대소문자를 구분한다. (case-sensitive)

## 1. sudo command: superuser do

superuser do의 줄임말인 `sudo`는 관리 또는 루트(root) 권한이 필요한 작업을 수행할 수 있는 가장 인기 있는 기본 Linux command 중 하나이다.

sudo를 사용할 때, 시스템은 사용자에게 암호로 자신을 인증하라는 메시지를 표시한다. 그런 다음, Linux 시스템은 타임스탬프(timestamp)를 추적기로 기록한다. 기본적으로 모든 루트 사용자는 세션당 15분 동안 sudo 명령을 실행할 수 있다.

자신을 인증하지 않고 명령줄에서 sudo를 실행하고 하면, 시스템에서 활동을 보안 이벤트로 기록한다. 

일반적인 구문은 다음과 같다.

```console
sudo (command)
```

또는 다음과 같은 option을 추가할 수도 있다.
* `-k` or `-reset-timestamp`는 타임스탬프 파일을 무효화한다.
* `-g` or `-group=group`은 지정된 그룹 이름 또는 ID로 명령을 실행한다.
* `-h` or `-host=host`는 호스트(host)에서 명령을 실행한다.

## 2. pwd command: print working directory

`pwd` command를 사용하여 현재 작업 디렉토리의 경로를 찾을 수 있다. pwd를 입력하면 전체 현재 경로, 즉 슬래시(/)로 시작하는 모든 디렉토리의 경로가 반환된다. 예를 들어, `/home/username`이다.

pwd command는 다음 구문을 사용한다.

```console
pwd [option]
```

허용되는 두 가지 option이 있다.

* `-L` or `-logical`은 기호 링크를 포함하여 환경 변수 내용을 출력한다.
* `-P` or `-physical`은 현재 디렉토리의 실제 경로를 출력한다.

## 3. cd command: change directory

Linux 파일 및 디렉토리를 탐색하려면 `cd` command를 사용한다. 현재 작업 디렉토리에 따라, 전체 경로 또는 디렉토리 이름이 필요하다.

옵션 없이 이 명령을 실행하면, 홈 폴더로 이동한다. 이는 sudo 권한이 있는 사용자만 실행할 수 있다.

현재 `/home/username/Documents`에 있고, Documents의 하위 디렉토리인 Photos로 이동하려고 한다고 가정한다. 이렇게 하려면 다음 명령을 입력한다.

```console
cd Photos
```

완전히 새로운 디렉터리 `/home/username/Movies`로 전환하려면, cd 다음에 디렉터리의 절대 경로를 입력해야 한다.

```console
cd /home/username/Movies
```

탐색에 도움이 되는 몇 가지 shortcut은 다음과 같다.

* `cd ~[username]`은 다른 사용자의 홈 디렉토리로 이동한다.
* `cd ..`은 한 디렉토리 위로 이동한다.
* `cd-`은 이전 디렉토리로 이동한다.

## 4. ls command: list

`ls` command는 시스템 내의 파일과 디렉토리를 나열한다. flag나 parameter 없이 실행하면, 현재 작업 디렉토리의 내용이 표시된다.

다른 디렉토리의 내용을 보려면, ls 다음에 원하는 경로를 입력한다. 예를 들어, Documents 폴더의 파일을 보려면, 다음을 입력한다.

```console
ls /home/username/Documents
```

다음은 ls 명령과 함께 사용할 수 있는 몇 가지 option이다.

* `ls -R`은 하위 디렉토리의 모든 파일을 나열한다.
* `ls -a`는 보이는 파일 외에 숨겨진 파일을 보여준다.
* `ls -lh`는 MB, GB, TB와 같이 쉽게 읽을 수 있는 형식으로 파일 크기를 표시한다.

## 5. cat command: concatenate

Concatenate 또는 `cat`은 가장 자주 사용되는 Linux command 중 하나이다. 파일 내용을 나열, 결합 및 표준 출력에 기록한다. cat 명령을 실행하려면, cat 뒤에 파일 이름과 확장자를 입력한다. 예를 들어:

```console
cat filename.txt
```

다음은 cat 명령어을 사용하는 다른 방법이다.

* `cat > filename.txt`는 새로운 파일을 만든다.
* `cat filename1.txt filename.txt > filename3.txt`는 1과 2를 병합하고 출력을 3에 저장한다.
* `tac filename.txt`는 내용을 역순으로 표시한다.

## 6. cp command: copy

`cp` command를 사용하여 파일 또는 디렉토리와 그 내용을 복사한다. 다음은 사용 사례이다.

현재 디렉토리에서 다른 파일로 한 파일을 복사하려면, cp 다음에 파일 이름 및 대상 디렉토리를 입력한다. 예를 들어:

```console
cp filename.txt /home/username/Documents
```

여러 파일을 디렉토리에 복사하려면, 파일 이름 다음에 대상 디렉토리를 입력한다.

```console
cp filename1.txt filename2.txt filename3.txt /home/username/Documents
```

파일 내용을 동일한 디렉토리의 새 파일로 복사하려면, cp 다음에 소스 파일 및 대상 파일을 입력한다.

```console
cp filename1.txt filename2.txt
```

전체 디렉토리를 복사하려면, 소스 디렉토리를 입력하기 전에 `-R` flag를 전달하고 대상 디렉토리를 입력한다.

```console
cp -R /home/username/Documents /home/username/Documents_backup
```

## 7. mv command: move

`mv` command의 기본 용도는 파일과 디렉토리를 이동하고 이름을 바꾸는 것이다. 또한, 실행 시 출력을 생성하지 않는다.

간단히 mv 뒤에 파일 이름과 대상 디렉토리를 입력한다. 예를 들어, filename.txt를 /home/username/Documents 디렉토리로 이동하려고 한다.

```console
mv filename.txt /home/username/Documents
```

mv command을 사용하여 파일 이름을 바꿀 수도 있다.

```console
mv old_filename.txt new_filename.txt
```

## 8. mkdir command: make directory

`mkdir` command를 사용하여 한 번에 하나 이상의 디렉토리를 생성하고 각각에 대한 권한을 설정한다. 이 commmand을 실행하는 사용자는 상위 디렉토리에 새 폴더를 만들 수 있는 권한이 있어야 한다. 그렇지 않으면, 권한 거부 오류가 발생할 수 있다.

기본 구문은 다음과 같다:

```console
mkdir [option] directory_name
```

예를 들어, Music이라는 디렉토리를 생성하려고 한다.

```console
mkdir Music
```

Music 내부에 Songs라는 새 디렉토리를 만들려면, 다음 command를 사용한다.

```console
mkdir Music/Songs
```

mkdir 명령은 다음과 같은 많은 옵션을 허용한다.

* `-p` or `-parents`는 두 개의 기존 폴더 사이에 디렉토리를 만든다. 예를 들어, `mkdir -p Music/2020/Songs`는 새로운 "2020" 디렉토리를 만든다.
* `-m`은 파일 권한을 설정한다. 예를 들어, 모든 사용자에 대해 전체 읽기, 쓰기 및 실행 권한이 있는 디렉토리를 생성하려면, `mkdir -m777 directory_name`을 입력한다.
* `-v`는 생성된 각 디렉토리에 대한 메시지를 출력한다.

## 9. rmdir command: remove directory

빈 디렉토리를 영구적으로 삭제하려면, `rmdir` command를 사용한다. 이 command를 실행하는 사용자는 상위 디렉토리에서 sudo 권한이 있어야 한다.

예를 들어, 이름이 personal1인 빈 하위 디렉토리와 기본 폴더인 mydir을 제거하려고 한다.

```console
rmdir -p mydir/personal1
```

## 10. rm command: remove

`rm` command는 디렉토리 내의 파일을 삭제하는 데 사용된다. 이 command를 수행하는 사용자에게 쓰기 권한이 있는지 확인한다.

이렇게 하면 파일이 제거되고 실행 취소할 수 없으므로, 디렉토리의 위치를 기억한다.

일반적인 구문은 다음과 같다.

```console
rm filename
```

여러 파일을 제거하려면, 다음 command를 입력한다.

```console
rm filename1 filename2 filename3
```

추가할 수 있는 허용 가능한 option은 다음과 같다.

* `-i`는 파일을 삭제하기 전에 시스템 확인 메시지를 표시한다.
* `-f`는 시스템이 확인 없이 제거하도록 허용한다.
* `-r`는 파일과 디렉터리를 재귀적으로 삭제한다.

## 11. touch command: create

`touch` command를 사용하면, 빈 파일을 생성하거나, Linux 커맨드라인에서 타임스탬프를 생성 및 수정할 수 있다.

예를 들어, 다음 명령을 입력하여, Documents 디렉토리에 Web이라는 HTML 파일을 만든다.

```console
touch /home/username/Documents/Web.html
```

## 12. locate command: find

`locate` command는 데이터베이스 시스템에서 파일을 찾을 수 있다.

또한, `-i` argument를 추가하면 대소문자 구분이 해제되므로, 정확한 이름을 기억하지 못하더라도 파일을 검색할 수 있다.

두 개 이상의 단어가 포함된 콘텐츠를 찾으려면, `asterisk (*)`를 사용한다. 예를 들어:

```console
locate -i school*note
```

이 명령은 대문자 또는 소문자를 사용하는지 여부에 관계없이, school 및 note라는 단어가 포함된 파일을 검색한다.

## 13. find command: find

`find` command를 사용하여 특정 디렉토리 내의 파일을 검색하고 후속 작업을 수행한다. 일반적인 구문은 다음과 같다:

```console
file [option] [path] [expression]
```

예를 들어, 홈 디렉토리와 하위 폴더에서 notes.txt라는 파일을 찾으려고 한다.

```console
find /home -name notes.txt
```

find를 사용할 때의 다른 변형은 다음과 같다.

* `find -name filename.txt`를 사용하여 현재 디렉토리에서 파일을 찾는다.
* `find ./ -type d -name directoryname`을 사용하여 디렉토리를 찾는다.

## 14. grep command: search text

목록에 있는 또 다른 기본 Linux command는 `grep` 또는 전역 정규식 출력(global regular expression print)이다. 특정 파일의 모든 텍스트를 검색하여 단어를 찾을 수 있다.

grep command가 일치 항목을 찾으면, 특정 패턴을 포함하는 모든 행을 출력한다. 이 command는 대용량 로그 파일을 필터링하는 데 도움이 된다.

예를 들어, notepad.txt 파일에서 blue라는 단어를 검색하려고 한다:

```console
grep blue notepad.txt
```

명령의 출력에는 blue가 포함된 줄이 표시된다.

## 15. df command: disk free

`df` command를 사용하여 백분율 및 킬로바이트(KB)로 표시되는 시스템의 디스크 공간 사용량을 알 수 있다. 일반적인 구문은 다음과 같다:

```console
df [options] [file]
```

예를 들어, 현재 디렉토리의 시스템 디스크 공간 사용량을 사람이 읽을 수 있는 형식으로 보려면, 다음 명령을 입력한다:

```console
df -h
```

다음은 사용할 수 있는 몇 가지 허용되는 옵션이다.

* `df -m`은 파일 시스템 사용량에 대한 정보를 MB 단위로 표시한다.
* `df -k`는 파일 시스템 사용량을 KB 단위로 표시한다.
* `df -T`는 새 열에 파일 시스템 유형을 표시한다.

## 16. du command: disk usage

파일이나 디렉토리가 차지하는 공간을 확인하려면, `du` command를 사용한다. 이 명령을 실행하여 스토리지를 과도하게 사용하는 시스템 부분을 식별할 수 있다.

`du` command를 사용할 때, 디렉토리 경로를 지정해야 한다. 예를 들어 /home/user/Documents를 확인하려면 다음을 입력한다.

```console
du /home/user/Documents
```

du command에 flag를 추가하면, 다음과 같이 작업이 수정된다:

* `-s`는 지정된 폴더의 총 크기를 제공한다.
* `-m`은 폴더 및 파일 정보를 MB 단위로 제공한다.
* `k`는 정보를 KB로 표시한다.
* `-h`는 표시된 폴더 및 파일의 마지막 수정 날짜를 알려준다.

## 17. head command: print headline

`head` command를 사용하면, 텍스트의 처음 10줄을 볼 수 있다. 옵션을 추가하면, 표시되는 줄 수를 변경할 수 있다. head command는 파이프(piped) 데이터를 CLI로 출력하는 데에도 사용된다.

일반적인 구문은 다음과 같다.

```console
head [option] [file]
```

예를 들어, 현재 디렉토리에 있는 note.txt의 처음 10줄을 보려면, 다음과 같이 한다:

```console
head note.txt
```

다음은 추가할 수 있는 몇 가지 option이다:

* `-n` or `-lines`는 첫 번째 사용자 정의 라인 수를 출력한다. 예를 들어, filename.txt의 처음 다섯 줄을 표시하려면, `head -n 5 filename.txt`를 입력한다.
* `-c` or `-bytes`는 각 파일의 첫 번째 사용자 지정 바이트 수를 출력한다.
* `-q` or `-quiet`는 파일 이름을 지정하는 헤더를 인쇄하지 않는다.

## 18. tail command: print tailline

`tail` command는 파일의 마지막 10줄을 표시한다. 이를 통해, 사용자는 파일에 새 데이터가 있는지 확인하거나, 오류 메시지를 읽을 수 있다.

일반적인 형식은 다음과 같다:

```console
tail [option] [file]
```

예를 들어, colors.txt 파일의 마지막 10줄을 표시하려고 한다:

```console
tail -n colors.txt
```

## 19. diff command: difference

difference의 줄임말인 `diff` command는 파일의 두 내용을 한 줄씩 비교한다. 이를 분석한 후, 일치하지 않는 부분을 표시한다.

프로그래머는 종종 diff command를 사용하여, 전체 소스 코드를 다시 작성하는 대신 프로그램을 변경한다.

일반적인 형식은 다음과 같다:

```console
diff [option] file1 file2
```

예를 들어, 두 개의 텍스트 파일(note.txt와 note_update.txt)을 비교하려고 한다.

```console
diff note.txt note_update.txt
```

추가할 수 있는 몇 가지 option은 다음과 같다.

* `-c`는 컨텍스트 형식으로 두 파일 간의 차이점을 표시한다.
* `-u`는 중복 정보 없이 출력을 표시한다.
* `-i`는 diff command가 대소문자를 구분하지 않도록 한다.

## 20. tar command: tape archiving

`tar` command는 여러 파일을 ZIP과 유사한 일반적인 Linux 형식인 TAR 파일로 아카이브(archive)하며, 선택적 압축을 제공한다.

기본 구문은 다음과 같다:

```console
tar [options] [archive_file] [file or directory to be archived]
```

예를 들어, /home/user/Documents 디렉토리에 newarchive.tar라는 새 TAR 아카이브를 생성하려고 한다.

```console
tar -cvf newarchive.tar /home/user/Documents
```

tar command는 다음과 같은 많은 option을 허용한다.

* `-x`는 파일을 추출한다.
* `-t`는 파일의 내용을 나열한다.
* `-u`는 기존 아카이브 파일을 아카이브하고 추가한다.

## 100. References

[40 Essential Linux Commands That Every User Should Know](https://www.hostinger.com/tutorials/linux-commands)