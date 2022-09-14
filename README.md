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
```

```
