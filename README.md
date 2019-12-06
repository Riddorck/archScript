-|- Basic installation -|-

#01#    loadkeys           it                                                               [Imposta la tastiera it TEMPORANEAMENTE]
#02#    fdisk              -l                                                               [Segnare partizione - Ignorare rom, loop o airoot]
#03#    parted             [partizione #02#] mklabel msdos                                   [Solitamente /dev/sda]
#04#    parted             [partizione #02#] mktable msdos
#05#    parted             [partizione #02#] mkpart primary ext4 1M 100%
#06#    fdisk              -l                                                               [Segnare nuova partizione - Ignorare rom, loop o airoot]
#07#    mkfs.ext4          [partizione #06#]                                                [Solitamente /dev/sda1]
#08#    mount              [partizione #06#] /mnt
#09#    pacstrap           /mnt base base-devel                                             [Installa pacchetti di base] [Mirror list a /etc/pacman.d/mirrorlist]
#10#    genfstab           -U /mnt >> /mnt/etc/fstab
#11#    arch-chroot        /mnt                                                             [Entra in chroot]
#12#    ln                 -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime
#13#    hwclock            --systohc
#14#    nano               /etc/locale.gen                                                  [Decommenta le lingue che vuoi (it_IT.UTF-8 UTF-8)]
#15#    locale-gen
#16#    nano               /etc/locale.conf                                                 [Imposta la variable (LANG=it_IT.UTF-8)]
#17#    nano               /etc/vconsole.conf                                               [Imposta la variable (KEYMAP=it)]
#18#    nano               /etc/hostname                                                    [Aggiungi l'hostname del pc]
#19#    passwd                                                                              [Imposta la password di root (root)]
#20#    pacman             -S grub
#21#    grub-install       [partizione #02#]
#22#    grub-mkconfig      -o /boot/grub/grub.cfg                                           [Nota bene: grub.cfg va rigenerato dopo ogni cambiamento a /etc/default/grub o ai file in /etc/grub.d/]
#23#    exit
#24#    pacman             -Sy xorg xorg-xinit xorg-xsetroot
#25#    pacman             -Sy i3 alsa-utils net-tools acpi linux-headers
#26#    pacman             -Sy dhcpcd dhclient wpa_supplicant wpa_actiond iproute
#27#    pacman             -Sy wget terminator git dmenu ttf-freefont
#28#    pacman             -Sy xbindkeys wireless_tools
#29#    pacman             -Sy thunar viewnior chromium notepadqq eclipse
#30#    pacman             -Sy thunar-archive-plugin unrar p7zip file-roller thunar-volman
#31#    pacman             -Sy libreoffice vlc qt4 virtualbox keepass
#32# @  pacman             -S virtualbox-guest-utils                                        [Solo se si usa VirtualBox]
#33#    useradd            -m [user]
#34#    passwd             [user #32#]
#35#    EDITOR=nano visudo                                                                  [Aggiungere riga: [user #32#] ALL=(ALL:ALL) ALL]
#36#    cp                 /etc/X11/xinit/xinitrc /home/[user #32#]/.xinitrc
#37#    nano               /home/[user #32#]/.xinitrc                                       [Aggiungere comandi da eseguire all'avvio di X (setxkbmap it & [a capo] imwheel --kill & [a capo] exec i3)]
#38#    nano               /home/[user #32#]/.bash_profile                                  [Aggiungere comandi da eseguire al login ([[ -f ~/.bashrc ]] && . ~/.bashrc [a capo] if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then [a capo] exec startx [a capo] fi)]
#39#    systemctl          enable dhcpcd
#40#    wget               "https://github.com/Riddorck/Utils/blob/master/aur-install.sh"
#41#    sh                 aur-install.sh package-query [user #32#]
#42#    sh                 aur-install.sh yaourt [user #32#]
#43#    rm                 aur-install.sh
#44#    yaourt             -S spotify imwheel
#45#    reboot



---        ---        ---        ---



-|- Rimuovere un pacchetto -|-

pacman -Rns


-|- Aggiornare sistema -|-

pacman -Syyu


-|- TODO -|-
