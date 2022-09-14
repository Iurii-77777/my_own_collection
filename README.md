## **Задача.**
#### Подготовка к выполнению.
```
Выполнено. Через ide pycharm преднастройка выполняется автоматически.
```
## **Задача 1-4.** 
#### В виртуальном окружении создать новый my_own_module.py файл. Наполнить его содержимым. 
#### Заполните файл в соответствии с требованиями ansible так, чтобы он выполнял основную задачу: module должен создавать текстовый файл на удалённом хосте по пути, определённом в параметре path, с содержимым, определённым в параметре content. 
#### Проверьте module на исполняемость локально.
```
(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/8-4$ python library/my_new_module.py input.json 

{"changed": true, "original_message": "some data multi line", "message": "file was written", "invocation": {"module_args": {"content": "some data multi line", "path": "/tmp/test.txt"}}}

```
## **Задача 5-6.**
#### Напишите single task playbook и используйте module в нём. Проверьте через playbook на идемпотентность.
```
(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/8-4$ ansible-playbook sitefork.yml --diff
[WARNING]: Unable to parse /etc/ansible/inventory as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [test my_new_module] *****************************************************************************************************************************************************************************************************

TASK [do a remote copy] *******************************************************************************************************************************************************************************************************
changed: [localhost]

PLAY RECAP ********************************************************************************************************************************************************************************************************************
localhost                  : ok=1    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/8-4$ ansible-playbook sitefork.yml --diff
[WARNING]: Unable to parse /etc/ansible/inventory as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [test my_new_module] *****************************************************************************************************************************************************************************************************

TASK [do a remote copy] *******************************************************************************************************************************************************************************************************
ok: [localhost]

PLAY RECAP ********************************************************************************************************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/8-4$ 
```
## **Задача 7-11**
#### Выйдите из виртуального окружения.
#### Инициализируйте новую collection
#### В данную collection перенесите свой module в соответствующую директорию.
#### Single task playbook преобразуйте в single task role и перенесите в collection. У role должны быть default всех параметров module
#### Создайте playbook для использования этой role.
```
(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/8-4$ deactivate 
```
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4$ ansible-galaxy collection init my_namespace.my_collection
- Collection my_namespace.my_collection was created successfully
```
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4$ tree
.
└── my_namespace
    └── my_collection
        ├── docs
        ├── galaxy.yml
        ├── input.json
        ├── library
        │   └── my_new_module.py
        ├── plugins
        │   ├── modules
        │   └── README.md
        ├── README.md
        ├── roles
        │   └── my-role
        │       ├── defaults
        │       │   └── main.yml
        │       ├── handlers
        │       │   └── main.yml
        │       ├── meta
        │       │   └── main.yml
        │       ├── tasks
        │       │   └── main.yml
        │       └── vars
        │           └── main.yml
        ├── sitefork.yml
        └── site.yml

13 directories, 12 files
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4$ 
```
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ ansible-playbook site.yml 
[WARNING]: Unable to parse /etc/ansible/inventory as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [localhost] ******************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************
ok: [localhost]

TASK [my-role : START my_new_module] **********************************************************************************************************************************
changed: [localhost]

PLAY RECAP ************************************************************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ ansible-playbook site.yml 
[WARNING]: Unable to parse /etc/ansible/inventory as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [localhost] ******************************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************************
ok: [localhost]

TASK [my-role : START my_new_module] **********************************************************************************************************************************
ok: [localhost]

PLAY RECAP ************************************************************************************************************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
## **Задача 12**
#### Выложите в свой репозиторий, поставьте тег 1.0.0 на этот коммит.
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git remote -v
origin  https://github.com/Iurii-77777/my_own_collection.git (fetch)
origin  https://github.com/Iurii-77777/my_own_collection.git (push)
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git tag -a 1.0.0 -m "for_netology"
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git add .
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git commit -m "final for netology"
[main 54f5b66] final for netology
 13 files changed, 324 insertions(+), 127 deletions(-)
 rewrite README.md (99%)
 create mode 100644 galaxy.yml
 create mode 100644 input.json
 create mode 100644 library/my_new_module.py
 create mode 100644 plugins/README.md
 create mode 100644 roles/my-role/defaults/main.yml
 create mode 100644 roles/my-role/handlers/main.yml
 create mode 100644 roles/my-role/meta/.galaxy_install_info
 create mode 100644 roles/my-role/meta/main.yml
 create mode 100644 roles/my-role/tasks/main.yml
 create mode 100644 roles/my-role/vars/main.yml
 create mode 100755 site.yml
 create mode 100644 sitefork.yml
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git tag
1.0.0
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ git push origin 1.0.0
Username for 'https://github.com': iurii-77777
Password for 'https://iurii-77777@github.com': 
Перечисление объектов: 1, готово.
Подсчет объектов: 100% (1/1), готово.
Запись объектов: 100% (1/1), 165 байтов | 165.00 КиБ/с, готово.
Всего 1 (изменения 0), повторно использовано 0 (изменения 0)
To https://github.com/Iurii-77777/my_own_collection.git
 * [new tag]         1.0.0 -> 1.0.0
```
## **Задача 13**
#### Создайте .tar.gz этой collection: ansible-galaxy collection build в корневой директории collection.
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4/my_namespace/my_collection$ ansible-galaxy collection build
Created collection for my_namespace.my_collection at /home/iurii-devops/PycharmProjects/ansible/prod8-4/my_namespace/my_collection/my_namespace-my_collection-1.0.0.tar.gz

```
## **Задача 14-16**
#### Создайте ещё одну директорию любого наименования, перенесите туда single task playbook и архив c collection.
#### Установите collection из локального архива: ansible-galaxy collection install <archivename>.tar.gz
#### Запустите playbook, убедитесь, что он работает.
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4test$ ansible-galaxy collection install my_namespace-my_collection-1.0.0.tar.gz 
Starting galaxy collection install process
Process install dependency map
Starting collection install process
Installing 'my_namespace.my_collection:1.0.0' to '/home/iurii-devops/.ansible/collections/ansible_collections/my_namespace/my_collection'
my_namespace.my_collection:1.0.0 was installed successfully

```
```
iurii-devops@Host-SPB:~/PycharmProjects/ansible/prod8-4test$ tree
.
├── docs
├── FILES.json
├── input.json
├── library
│   └── my_new_module.py
├── MANIFEST.json
├── my_namespace-my_collection-1.0.0.tar.gz
├── plugins
│   ├── modules
│   └── README.md
├── README.md
├── roles
│   └── my-role
│       ├── defaults
│       │   └── main.yml
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── tasks
│       │   └── main.yml
│       └── vars
│           └── main.yml
├── sitefork.yml
└── site.yml

11 directories, 14 files

```
## **Задача 17**
#### В ответ необходимо прислать ссылку на репозиторий с collection.
```

```
