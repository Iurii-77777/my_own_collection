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
(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/ansible-8-4-role (fork)$ python library/my_new_module.py input.json 

{"changed": true, "original_message": "some data multi line", "message": "file was written", "invocation": {"module_args": {"content": "some data multi line", "path": "/tmp/test.txt"}}}

```
```
(venv) iurii-devops@Host-SPB:~/PycharmProjects/ansible/venv/ansible-8-4-role (fork)$  tree
.
├── group_vars
│   ├── all
│   │   └── vars.yml
│   ├── elasticsearch
│   │   └── vars.yml
│   └── kibana
│       └── vars.yml
├── info
│   └── readme.md
├── input.json
├── inventory
│   └── prod.yml
├── library
│   └── my_new_module.py
├── __pycache__
├── README.md
├── requirements.yml
├── roles
│   ├── elastic-role
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── molecule
│   │   │   ├── default
│   │   │   │   ├── converge.yml
│   │   │   │   ├── molecule.yml
│   │   │   │   └── verify.yml
│   │   │   └── old
│   │   │       ├── converge.yml
│   │   │       ├── molecule.yml
│   │   │       └── verify.yml
│   │   ├── README.md
│   │   ├── requirements.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   │   └── elk.sh.j2
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── java
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── molecule
│   │   │   ├── default
│   │   │   │   ├── converge.yml
│   │   │   │   ├── molecule.yml
│   │   │   │   └── verify.yml
│   │   │   └── oracle
│   │   │       ├── converge.yml
│   │   │       ├── molecule.yml
│   │   │       └── verify.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   │   └── jdk.sh.j2
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   └── kibana-role
│       ├── defaults
│       │   └── main.yml
│       ├── files
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── molecule
│       │   └── default
│       │       ├── converge.yml
│       │       ├── molecule.yml
│       │       └── verify.yml
│       ├── README.md
│       ├── tasks
│       │   └── main.yml
│       ├── templates
│       │   └── kib.sh.j2
│       ├── tests
│       │   ├── inventory
│       │   └── test.yml
│       └── vars
│           └── main.yml
├── sitefork.yml
├── site.yml
└── templates
    ├── elk.sh.j2
    ├── jdk.sh.j2
    └── kib.sh.j2
```
## **Задача 5-6.**
#### Напишите single task playbook и используйте module в нём. Проверьте через playbook на идемпотентность.
```

```
