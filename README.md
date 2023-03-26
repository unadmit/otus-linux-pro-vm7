# Загрузка Linux
## 1. Попасть в систему без пароля несколькими способами.

Так как на стенде для выполнения домашних работ установлена CentOS без GUI и нет возможности подключиться к консольной сессии, были выполнены следующие действия с гипервизором для выполнения работы:
- Выполнено подключение к серверу гипервизора через HP iLo.
- Установлены компоненты графической оболочки CentOS с помощью следующих команд:
  ```
  yum -y groupinstall basic-desktop desktop-platform x11 fonts
  yum -y groupinstall kde-desktop
  echo startkde > ~/.xinitrc
  ```
- Запущена среда KDE командой
  ```
  startx
  ```
- Запущена ВМ BootSystemCentOS в VirtualBox Manager и в момент выбора ядра для загрузки ОС нажата клавиша "e".
![image](https://user-images.githubusercontent.com/122820579/227715415-ee306bce-c6b8-441c-bc22-794a4200336f.png)
- Способ 1. В конце строки, начинающейся с linux16 дописана команда "init=/bin/sh".
![image](https://user-images.githubusercontent.com/122820579/227716376-1bbb45b7-d25e-4ae8-b857-f4a12ca6a6c3.png)
- Нажато сочетание клавиш "ctrl+x".
![image](https://user-images.githubusercontent.com/122820579/227715855-ccf41e1c-d765-4a05-b662-360fcf9a52fb.png)
- Выполнено перемонтирование рутовой файловой системы в режим "Read-Write".
![image](https://user-images.githubusercontent.com/122820579/227715953-f727f2c9-0223-4208-a125-8c276763eecb.png)
- Способ 2. В конце строки, начинающейся с linux16 дописана команда rd.break.
![image](https://user-images.githubusercontent.com/122820579/227716427-98e1e931-c4e7-4026-83ac-b35161d32918.png)
- Нажато сочетание клавиш "ctrl+x". Выполняется вход в Emergency mode.
![image](https://user-images.githubusercontent.com/122820579/227716614-6a9ed8d7-1c51-4bf9-ab44-76271908169e.png)
- Выполнены команды перемонтирования корневой файловой системы:
  ```
  mount -o remount,rw /sysroot
  chroot /sysroot
  ```
  ![image](https://user-images.githubusercontent.com/122820579/227717157-6fa55cf4-4a7c-4cf2-b814-5c21834007c8.png)
-  Выполнен сброс пароля пользователя root и создание файла .autorelabel, что позволит обойти ограничения SELinux.
  ```
  passwd root
  touch /.autorelabel
  ```
  ![image](https://user-images.githubusercontent.com/122820579/227717399-e7f17576-485e-44c9-a26f-2f7ec8b4fa02.png)
- После перезагрузки действует новый пароль на пользователя root.
## 2. Утановить систему с LVM, после чего переименовать VG.
![image](https://user-images.githubusercontent.com/122820579/227774817-3f757ab3-b1bd-4dee-9ced-e9c242f41c32.png)
![image](https://user-images.githubusercontent.com/122820579/227775171-342b72d5-c3ba-45bc-a32f-0fdb77d0aa95.png)
![image](https://user-images.githubusercontent.com/122820579/227775709-04d17e8b-6659-4b01-b736-3481b434acc2.png)
![image](https://user-images.githubusercontent.com/122820579/227775834-d398f463-d49d-4a11-a3fd-0e09aa70139f.png)
![image](https://user-images.githubusercontent.com/122820579/227775945-ca2252df-0d63-44f2-8425-9cc540a1bc1b.png)
![image](https://user-images.githubusercontent.com/122820579/227776045-d44c4627-20b3-4adb-b0a2-27eecd3c3923.png)
## 3. Добавить модуль в initrd
![image](https://user-images.githubusercontent.com/122820579/227778931-2b62119d-24de-453a-8632-eade96f2efc5.png)
![image](https://user-images.githubusercontent.com/122820579/227779695-90fae482-f961-4050-a2ea-f3c8aefd795f.png)
![image](https://user-images.githubusercontent.com/122820579/227780232-69a34794-dc68-4f18-a8f0-fd5c2220b41e.png)
![image](https://user-images.githubusercontent.com/122820579/227780438-3bc59f02-e34a-4a99-83c9-9e59ee10d2d0.png)
![image](https://user-images.githubusercontent.com/122820579/227781019-1d9e9fa1-6dce-40e5-8ff9-7bf9a505e1a9.png)
![image](https://user-images.githubusercontent.com/122820579/227781119-7013fa26-a1b3-455d-b37d-e4d2b346abfe.png)
