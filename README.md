Для входа без пароля под root способом-1 необходимо удалить параметр console=ttyS0,115200n8 Копипаст не работает. Приложен скрин "sp_1".
Вход без пароля под root способом-2 приложены скрины "sp_2" и "sp_2.1"
Для входа без пароля под root способом-3 необходимо удалить параметр console=ttyS0,115200n8 Копипаст не работает. Приложен скрин "sp_3".
==================================================================================================
[vagrant@lvm ~]$ sudo -i
[root@lvm ~]# vgs
  VG         #PV #LV #SN Attr   VSize   VFree
  VolGroup00   1   2   0 wz--n- <38.97g    0 
[root@lvm ~]# vgrename VolGroup00 OtusRoot
  Volume group "VolGroup00" successfully renamed to "OtusRoot"
[root@lvm ~]# vi /etc/fstab 
[root@lvm ~]# vi /etc/default/grub 
[root@lvm ~]# vi /boot/grub2/grub.cfg 
[root@lvm ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree
  OtusRoot   1   2   0 wz--n- <38.97g    0 
[root@lvm ~]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)
Executing: /sbin/dracut -f -v /boot/initramfs-3.10.0-862.2.3.el7.x86_64.img 3.10.0-862.2.3.el7.x86_64
*** Creating image file ***
*** Creating image file done ***
*** Creating initramfs image file '/boot/initramfs-3.10.0-862.2.3.el7.x86_64.img' done ***
[root@lvm ~]# reboot
Connection to 127.0.0.1 closed by remote host.
[vagrant@lvm ~]$ sudo -i
[root@lvm ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree
  OtusRoot   1   2   0 wz--n- <38.97g    0 
==========================================================================================================
[vagrant@lvm ~]$ sudo -i
[root@lvm ~]# vgs
  VG       #PV #LV #SN Attr   VSize   VFree
  OtusRoot   1   2   0 wz--n- <38.97g    0 
[root@lvm ~]# mkdir /usr/lib/dracut/modules.d/01test
[root@lvm ~]# vi module-setup.sh
[root@lvm ~]# cp module-setup.sh ^C
[root@lvm ~]# cp module-setup.sh /usr/lib/dracut/modules.d/01test
[root@lvm ~]# cd /usr/lib/dracut/modules.d/01test
[root@lvm 01test]# ls
module-setup.sh
[root@lvm 01test]# vi test.sh
[root@lvm 01test]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)
Executing: /sbin/dracut -f -v /boot/initramfs-3.10.0-862.2.3.el7.x86_64.img 3.10.0-862.2.3.el7.x86_64
*** Creating image file ***
*** Creating image file done ***
*** Creating initramfs image file '/boot/initramfs-3.10.0-862.2.3.el7.x86_64.img' done ***
[root@lvm 01test]# lsinitrd -m /boot/initramfs-$(uname -r).img | grep test
test
-------------------------------------------------------------------------------------------
В методичке опечатка - Перезагрузиться и руками выключить опции rghb и quiet. Верно - rhgb
-------------------------------------------------------------------------------------------
