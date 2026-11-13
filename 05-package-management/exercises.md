# លំហាត់មេរៀនទី ៥៖ Package Management

## ផ្នែក A៖ សំណួរ
1. Package និង repository មានន័យដូចម្តេច?
2. តើ apt update ធ្វើអ្វី? តើវាដូច apt upgrade ដែរឬទេ?
3. តើ distro អ្វីខ្លះប្រើ DNF និង pacman?
4. ហេតុអ្វីត្រូវអាន transaction summary មុន install/upgrade?
5. ហេតុអ្វីការបិទ signature verification មានហានិភ័យ?

## ផ្នែក B៖ អនុវត្តតាម Distribution

ស្គាល់ distro ជាមុន៖

~~~bash
cat /etc/os-release
~~~

ជ្រើស command តាម distro របស់អ្នក៖

**Ubuntu/Debian**
~~~bash
apt search curl
apt show curl
apt list --installed
~~~

**Fedora**
~~~bash
dnf search curl
dnf info curl
dnf list installed
~~~

**Arch Linux**
~~~bash
pacman -Ss curl
pacman -Si curl
pacman -Q
~~~

កត់ត្រា package description, version និង repository។ សម្រាប់លំហាត់នេះ មិនចាំបាច់ install ឬ upgrade package ទេ។

## ផ្នែក C៖ Scenario

អ្នកទទួលបាន command ដែលបន្ថែម third-party repository ហើយ install package ជាមួយ sudo។ តើអ្នកនឹងពិនិត្យអ្វីខ្លះមុនរត់វា?

## លក្ខខណ្ឌបញ្ចប់
- អាចកំណត់ package manager តាម distro។
- អាចស្វែងរក និងអាន package metadata។
- អាចពន្យល់ភាពខុសគ្នារវាង metadata refresh និង upgrade។
- អាចពិនិត្យ transaction និង repository trust មុនផ្លាស់ប្ដូរប្រព័ន្ធ។
