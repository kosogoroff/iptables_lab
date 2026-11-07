# network_lab - Репозиторий для развёртывания лабораторного стенда домашнего задания к занятию "30. Фильтрация трафика - iptables"

Для развёртывания лабораторного стенда выполните команды:

```
git clone https://github.com/kosogoroff/iptables_lab.git
cd iptables_lab
vagrant up
chmod +x generate_inventory.sh
./generate_inventory.sh
ansible-playbook -i inventory.ini ansible/playbook.yml
```

Для создания репозитория использованы команды:

```
[admin_insta11@mv334 iptables_lab]$ git init
подсказка: Using 'master' as the name for the initial branch. This default branch name
подсказка: is subject to change. To configure the initial branch name to use in all
подсказка: of your new repositories, which will suppress this warning, call:
подсказка: 
подсказка: 	git config --global init.defaultBranch <name>
подсказка: 
подсказка: Names commonly chosen instead of 'master' are 'main', 'trunk' and
подсказка: 'development'. The just-created branch can be renamed via this command:
подсказка: 
подсказка: 	git branch -m <name>
Инициализирован пустой репозиторий Git в /home/admin_insta11/iptables_lab/.git/
[admin_insta11@mv334 iptables_lab]$ 
[admin_insta11@mv334 iptables_lab]$ git add  .
[admin_insta11@mv334 iptables_lab]$ git commit -m "first commit"
[master (корневой коммит) 45fb529] first commit
 13 files changed, 443 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 Vagrantfile
 create mode 100644 ansible.cfg
 create mode 100644 ansible/playbook.yml
 create mode 100644 ansible/templates/00-installer-config.yaml
 create mode 100644 ansible/templates/50-vagrant_centralRouter.yaml
 create mode 100644 ansible/templates/50-vagrant_centralServer.yaml
 create mode 100644 ansible/templates/50-vagrant_inetRouter.yaml
 create mode 100644 ansible/templates/50-vagrant_inetRouter2.yaml
 create mode 100644 ansible/templates/iptables_rules.ipv4
 create mode 100755 generate_inventory.sh
 create mode 100644 inventory.ini
[admin_insta11@mv334 iptables_lab]$ git branch -M main
[admin_insta11@mv334 iptables_lab]$ git remote add origin https://github.com/kosogoroff/iptables_lab.git
[admin_insta11@mv334 iptables_lab]$ 
[admin_insta11@mv334 iptables_lab]$ git push -u origin main

(gnome-ssh-askpass:139444): dbind-WARNING **: 22:42:39.380: Couldn't connect to accessibility bus: Empty address ''

(gnome-ssh-askpass:139465): dbind-WARNING **: 22:42:48.697: Couldn't connect to accessibility bus: Empty address ''
Перечисление объектов: 17, готово.
Подсчет объектов: 100% (17/17), готово.
При сжатии изменений используется до 24 потоков
Сжатие объектов: 100% (15/15), готово.
Запись объектов: 100% (17/17), 5.14 КиБ | 1.03 МиБ/с, готово.
Total 17 (delta 3), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/kosogoroff/iptables_lab.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
[admin_insta11@mv334 iptables_lab]$ 


```
