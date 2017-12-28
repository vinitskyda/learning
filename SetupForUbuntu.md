# Настройка локального сервера:
1. Установить зависимости:
```
sudo apt-get install git git-core curl ssh
```
2. Установить *nvm*:
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
3. Подгрузить конфиг *bashrc*:
```
source ~/.bashrc
```
4. Установить *nodejs*:
```
nvm install v6.10.2
```
5. Указать версию *nodejs* по умолчанию:
```
nvm alias default v6.10.2
```
6. Установить *rvm*:
```
\curl -sSL https://get.rvm.io | bash
```
7. Дописать конфиг *bashrc*:
```
echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> ~/.bashrc
```
8. Подгрузить конфиг *bashrc*:
```
source ~/.bashrc
```
9. Установить *ruby*:
```
rvm install 2.1.5
```
10. Указать версию *ruby* по умолчанию:
```
rvm use --default 2.1.5
```
11. Сгенерировать *ssh* ключ: https://help.github.com/articles/connecting-to-github-with-ssh/
12. Настроить профиль *git*:
```
git config --global user.name "Your name and lastname"
git config --global user.email "your_email@uchi.ru"
```
13. Склонировать репозиторий:
```
git clone git@github.com:uchiru/content-ext.git
```
14. Доставить зависимости гемов:
```
gem install bundle bundler
```
15. Установить *yarn*: https://yarnpkg.com/lang/en/docs/install/
16. Установить *docker*: https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/
17. Настроить при необходимости права для файла `/var/run/docker.sock ` (после вызова команды необходимо ребутнуть систему):
```
sudo usermod -a -G docker $USER
```
18. Авторизоваться на https://verdaccio.uchi.ru/ (использовать логин/пароль от cms, логин - это первая часть @uchi.ru-почты, например `sidorov` для почты `sidorov@uchi.ru`):
```
npm adduser --registry  https://verdaccio.uchi.ru --scope @uchiru
```
19. Перейти в папку с репозиторием и запустить сервер:
```
cd ~/<путь до папки с репозиторием>/content
./run s
```
20. Убедиться, что сервер работает корректно: http://localhost:4567/
