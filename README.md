# SSH-Add-Key-Connection

### Шаг 1: Генерация SSH ключа ###

`ssh-keygen -t ed25519 -C "your_email@example.com"`

Если `ed25519` не поддерживается, можете использовать `rsa` ключ:
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
## ##
Задайте имя файла: `id_ed25519` или `id_rsa`

Задайте парольную фразу (passphrase): можно довбавить, но не обязательно.

Ключ создан: После этого в вашем домашнем каталоге `(~/.ssh/)` появятся два файла:
- `id_ed25519` (или `id_rsa`): ваш приватный ключ. Храните его в секрете!
- `id_ed25519.pub` (или `id_rsa.pub`): ваш публичный ключ. Его вы будете загружать на GitHub.

### Шаг 2: Добавление SSH ключа на GitHub ###
Скопируйте публичный ключ: Вы можете просмотреть содержимое публичного ключа с помощью команды:
`cat ~/.ssh/id_ed25519.pub`
или
`cat ~/.ssh/id_rsa.pub`
Cкопируйте текст

## Перейдите в настройки GitHub: ##
  - Войдите в свой аккаунт на GitHub.
  - Нажмите на вашу аватарку в правом верхнем углу.
  - Выберите “Settings”.
  - В левом меню выберите “SSH and GPG keys”.

## Добавьте новый ключ: ##
  - Нажмите кнопку “New SSH key”.
  - В поле “Title” введите понятное название для вашего ключа (например, “Ubuntu Laptop”).
  - В поле “Key” вставьте скопированный публичный ключ.
  - Нажмите “Add SSH key”.

### Шаг 3: Настройка SSH агента (опционально, но рекомендуется) ###

SSH-агент позволяет вам не вводить парольную фразу каждый раз при использовании ключа.

1. Запустите SSH-агента:
`eval $(ssh-agent -s)`
 
2. Добавьте приватный ключ в агент:
`ssh-add ~/.ssh/id_ed25519`
или
`ssh-add ~/.ssh/id_rsa`
 
Вам может понадобиться ввести парольную фразу от вашего ключа.
 
3. Автоматизировать запуск агента: чтобы не запускать агента каждый раз, можете добавить команды в .bashrc:

 `if [ -z "$SSH_AUTH_SOCK" ] ; then
    eval $(ssh-agent -s)
    ssh-add ~/.ssh/id_ed25519 
 fi`

И перезапустите терминал.

### Шаг 4: Проверка соединения ###

1. Проверьте соединение с GitHub: Введите следующую команду:
`ssh -T git@github.com`
Если все настроено правильно, вы увидите сообщение:
`Hi your_username! You've successfully authenticated, but GitHub does not provide shell access.`

