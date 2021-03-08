Assignment name  : microshell
Expected files   : *.c *.h
Allowed functions: malloc, free, write, close, fork, waitpid, signal, kill, exit, chdir, execve, dup, dup2, pipe, strcmp, strncmp
--------------------------------------------------------------------------------------

- Executable's path will be absolute or relative but your program must not build a path (from the PATH variable for example)
- 파이프 `|`와 세미콜론 `;` 구현
	- 아무것도 없이 `|`를 쓰거나 `;`의 앞이나 뒤에 바로 `|`를 쓰는 등의 케이스는 테스트하지 않을 것입니다.
- 옵션 없이 경로만 받는 `cd` 명령어 구현
	- cd 명령어의 인자의 개수가 잘못됐으면 STDERR 에 `error: cd: bad arguments\n` 출력
	- cd 명령이 실패하면 STDERR 에 `error: cd: cannot change directory to path_to_change\n`
	- cd 명령 바로 앞이나 뒤엔 파이프(`|`)가 오지않음
- You don't need to manage any type of wildcards (*, ~ etc...)
- You don't need to manage environment variables ($BLA ...)
- execve, chdir를 제외한 system call이 에러를 반환할 경우, STDERR에 `error: fatal\n` 출력 후 프로그램 exit
- execve가 실패한다면 STDERR에 `error: cannot execute executable_that_failed\n` 출력 (executable_that_failed 실패한 명령의 경로이니까 execve의 첫번째 인자겠죠?)
- Your program should be able to manage more than hundreds of "|" even if we limit the number of "open files" to less than 30.

이렇게 실행된다
```
$>./microshell /bin/ls "|" /usr/bin/grep microshell ";" /bin/echo i love my microshell
microshell
i love my microshell
$>
```
Hints:
Don't forget to pass the environment variable to execve

Hints:
Do not leak file descriptors!
