# Простой и элегантый способ обойти все блядкие блокировки от РКН на любом дистрибутиве linux

Примечание: РАБОТАЕТ АБСОЛЮТНО ВСЕ НА ЛЮБОМ ПРОВАЙДЕРЕ! ВОЙСЫ В ДС, ЮТУБ, ТВИТТЕР И ТД

Хочется сразу сказать ПОШЕЛ НАХУЙ РКН. 

А теперь к сути:

Манипуляции подходят для любого дистрибутива linux, в том числе и на дристрибутивах, не имеющих systemd 

Нам понадобится AmneziaWg, а точнее его аналог под линукс (https://github.com/amnezia-vpn/amneziawg-linux-kernel-module) 
так же ставим Awg-tools (https://github.com/amnezia-vpn/amneziawg-tools)

Само собой на страницах AWG и AWG-tools есть максимально подробные и понятные способы установки и сборки

После установки переходим на эту прекрасную страницу (https://github.com/ImMALWARE/bash-warp-generator) и по инструкции генерируем WARP.conf

Перебрасываем его в путь /etc/amnezia/amneziawg/ 

Прописываем "sudo awg-quick up WARP"

Готово! После этих действий не вы сосете РКН, а он вам 

Для отмены сервиса прописываем "sudo awg-quick down WARP"

Примечание номер 2: Если вам максимально впадлу делать все эти действия, загляните на страницу с клиентом AmneziaVPN (https://github.com/amnezia-vpn/amnezia-client)

Есть удобный бинарник для линукс, который кстати работает на wayland! Но все же максимальная стабильность данной проги выражается на debian-based дистрибутивах, так как изначально под него и заточено


Примечание номер 3: Совсем недавно пересел на NixOs и понял что нашел свой дистрибутив, поэтому щас будет гайд на обьеб РКН на 
NixOs

Переключаемся на unstable канал, после из репозитория скачиваем и устанавливаем amneziawg-tools и amneziawg-go (на удачу)
и самый главный аспект, это модуль ядра 

Я использую ядро zen, поэтому и модуль для ядра соответственно zen (но есть модули для обычного ядра, xanmod и хуё моё куча разных)

Сам модуль сначала скачиваем как дефол пакет: 

 environment.systemPackages = [
    pkgs.linuxKernel.packages.linux_zen.amneziawg
  ];

Затем в конфигурации добавляем эту богостроку 

boot.extraModulePackages = with config.boot.kernelPackages ; [ amneziawg ] ; 

(более подробно можете рассмотреть в моей конфигурации NixOs, которая есть в профиле)
(НАСТОЯТЕЛЬНО РЕКОМЕНДУЮ ОБОСРАТЬ И ВЫСМЕЯТЬ МОЙ КОНФИГ ДЛЯ NIXOS, А ТАК ЖЕ УКАЗАТЬ НА ОШИБКИ, ЕСЛИ ОНИ ЕСТЬ!!!)

Готово! Теперь осталось лишь создать путь /etc/amnezia/amneziawg, а после вкинуть туда WARP (ну и само собой sudo awg-quick up WARP)
