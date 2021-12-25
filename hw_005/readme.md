1. Done
2. Done
3. Done
4. Done:
```
➜  vagrant vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'bento/ubuntu-20.04' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'bento/ubuntu-20.04'
    default: URL: https://vagrantcloud.com/bento/ubuntu-20.04
==> default: Adding box 'bento/ubuntu-20.04' (v202112.19.0) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202112.19.0/providers/virtualbox.box
==> default: Box download is resuming from prior download progress
==> default: Successfully added box 'bento/ubuntu-20.04' (v202112.19.0) for 'virtualbox'!
==> default: Importing base box 'bento/ubuntu-20.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'bento/ubuntu-20.04' version '202112.19.0' is up to date...
==> default: Setting the name of the VM: vagrant_default_1640245847584_18644
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /Users/em/Documents/vagrant
```

5. Ресурсы по умолчанию:
   Процессоров: 2
   Оперативная память: 1024 MB
   Видео память: 4 MB
   Storage (virtual size): 64 GB
   
6. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
   Добавить в Vagrantfile строки:
   ```
   config.memory = 2048
   config.cpus = 4
   ```
   
7. Done:
   ```
   ➜  vagrant vagrant ssh
    Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-91-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/advantage

    System information as of Fri 24 Dec 2021 09:23:33 PM UTC

    System load:  0.0                Processes:             120
    Usage of /:   11.9% of 30.88GB   Users logged in:       0
    Memory usage: 19%                IPv4 address for eth0: 10.0.2.15
    Swap usage:   0%

    This system is built by the Bento project by Chef Software
    More information can be found at https://github.com/chef/bento
   ```
8. Какой переменной можно задать длину журнала history: **HISTFILESIZE**
   Строки мануала: **716 - 720**
   Что делает директива ignoreboth в bash: 
   **ignoreboth - это сокращение для ignorespace and ignoredups.**
   То есть не сохранять в истории строки, начинающиеся с пробела и,
   если строка совпадает с предыдущей в истори, то она не сохранится (не будет дубликатов)
   
9. Скобки `{}` - зарезервированые символы, применяются для:
   - списков `{ list; }` (230-234 строки мануала)
   - получения элементов списка: ${my_list[2]} (874 строка мануала)
   - построения последовательностей: {x..y[..incr]} (930 строка мануала)
   - манипуляций с переменными (с 978 строки мануала раздел Parameter Expansion)
   - группировки вывода составных команд (compound command) (строка мануала 348)
   
10. Как создать однократным вызовом touch 100000 файлов?
    Надо использовавть построение последодввательности, например:
    ```
    touch {1..100000}
    ```
    Получится ли аналогичным образом создать 300000?
    Нет, поскольку такая команда привысит лимит ARG_MAX:
    ```
    touch {1..300000}
    -bash: /usr/bin/touch: Argument list too long
    ```
    
11. Что делает конструкция [[ -d /tmp ]]?
    Вернёт true, если существует директория /tmp
    
12. ```
    mkdir -p /tmp/new_path_directory
    cp -p /usr/bin/bash /tmp/new_path_directory/bash
    nano ~/.bashrc
    # add line to ~/.bashrc file:
    export PATH="/tmp/new_path_directory:$PATH"
    source ~/.bashrc
    type -a bash   
    ```

13. Чем отличается планирование команд с помощью batch и at?
    at - выполняет команды в указанное время
    batch - выполняет команды, когда позволяет уровень загрузки системы
    
14. Done
    ```
    ➜  vagrant vagrant halt
    ==> default: Attempting graceful shutdown of VM...
    ```
   