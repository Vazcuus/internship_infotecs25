# Ansible

1. Установка пакета ansible-core2.15.13 через pip3 
    Более актуальные версии Ansible >=2.17 вызывают ошибки и проблемы в зависимостях, при работе
с управляемыми хостами, имеющими устаревшую версию Python.

2. Оформление задач в install_docker.yml (ansible-playbook)

3. Настройка файла hosts для подключения к управляемому хосту по ssh.
    /hosts:
        client01 ansible_host=192.168.1.26 ansible_user=vagrant ansible_ssh_private_key_file=/home/lion/.ssh/client01
