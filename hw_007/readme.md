1. `strace /bin/bash -c 'cd /tmp'` -> `chdir("/tmp")`
2.  ```
     /home/vagrant/.magic.mgc
     /home/vagrant/.magic
     /etc/magic
     /usr/share/misc/magic.mgc
    ```
3.  Создадим скрипт: test_script.sh, который раз в 10 секунд будет писать в файл output.txt строку.
    ```
    ps -elf | grep test_script -> PID = 2175
    rm output.txt
    vagrant@vagrant:~$ lsof -p 2175
    COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
    test_scri 2175 vagrant  255r   REG  253,0      117 1048614 /home/vagrant/test_script.sh (deleted)
  
    echo '' > /proc/2175/fd/255
    ```

4. Зомби процессы будут отображаться с таблице процессаов (ps), но не будут занимать ресурсы ОС.
5. ```
   sudo apt-get install bpfcc-tools
   vagrant@vagrant:~$ sudo /usr/sbin/opensnoop-bpfcc
    PID    COMM               FD ERR PATH
    898    vminfo              4   0 /var/run/utmp
    620    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
    620    dbus-daemon        21   0 /usr/share/dbus-1/system-services
    620    dbus-daemon        -1   2 /lib/dbus-1/system-services
    620    dbus-daemon        21   0 /var/lib/snapd/dbus-1/system-services/
   ```
6. `uname({sysname="Linux", nodename="vagrant", release="5.4.0-91-generic", version="#102-Ubuntu SMP Fri Nov 5 16:31:28 UTC 2021", machine="x86_64", domainname="(none)"}) = 0`
   ```
   sudo apt-get install manpages-dev
   man 2 uname -> Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.
   
   ```
7. Последовательность команд через `;` выполняет послдовательно команды.
   `&&` - логическое И, то есть в примере: `test -d /tmp/some_dir && echo Hi` - поскокльку нет директории /tmp/some_dir, то в stdout не будет выведено Hi.
   Если выполнить `test -d ~/.ssh/ && echo Hi` - то в выводе будет Hi, т.к. директория ~/.ssh/ существует.
   
   `set -e` - выход, если команда завершается с ненулевым статусом. Нет смысла применять `set -e` с `&&`, посокльку при ошибке прекратится выполнение всех команд. 

8. `set -euxo pipefail`:
   -e - выход, если команда завершается с ненулевым статусом
   -u - считать неустановленные переменные ошибкой при подстановке
   -x - печатать команды и их аргументы по мере их выполнения
   -o pipefail - статус последней команды для выхода с ненулевым статусом или ноль, если ни одна команда не вышла с ненулевым статусом
   Хорошо было бы использовать в сценариях, т.к. расширяется логирование и сценарий завершится при наличии ошибок. 

9. Наиболее часто встречающиеся статусы у процессов в системе:
   
   I - фоновые процессы ядра
   
   S - процессы, ожидающие завершения