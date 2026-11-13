# មេរៀនទី ៥៖ Package Management

## គោលបំណងមេរៀន
- ពន្យល់ពី package manager និង repository។
- ស្វែងរក និងមើលព័ត៌មាន package។
- ស្គាល់ package commands ក្នុង Ubuntu/Debian, Fedora និង Arch។
- យល់ពីភាពខុសគ្នារវាង refresh metadata និង upgrade packages។
- ដំឡើង/លុប package ដោយប្រុងប្រយ័ត្នក្នុង VM ដែលអ្នកគ្រប់គ្រង។

## ១. Package Manager និង Repository

Package គឺជាបណ្ដុំកម្មវិធី និង metadata ដែលអាចដំឡើង ធ្វើបច្ចុប្បន្នភាព និងដកចេញបាន។ Package manager ដោះស្រាយ dependencies និងកត់ត្រាស្ថានភាព packages។ Repository ជាប្រភព packages ដែល distribution ឬអ្នកគ្រប់គ្រងកំណត់។

ប្រើ repository ដែលទុកចិត្តបាន។ ការបន្ថែម third-party repository អាចផ្ដល់ software ប៉ុន្តែបង្កើន trust boundary និង security risk។

## ២. ស្គាល់ Distribution

~~~bash
cat /etc/os-release
~~~

- Ubuntu និង Debian ជាទូទៅប្រើ APT។
- Fedora ជាទូទៅប្រើ DNF។
- Arch Linux ជាទូទៅប្រើ pacman។

កុំចម្លង command របស់ distribution មួយទៅមួយទៀតដោយសន្មតថាដំណើរការដូចគ្នា។

## ៣. Ubuntu/Debian និង APT

~~~bash
apt search curl
apt show curl
apt list --installed
~~~

ក្នុង VM ដែលអ្នកគ្រប់គ្រង អាច refresh repository metadata និងដំឡើង package៖

~~~bash
sudo apt update
sudo apt install curl
~~~

apt update ទាញយកព័ត៌មាន repository ថ្មី; វាមិន upgrade packages ទាំងអស់ដោយខ្លួនឯងទេ។ Upgrade packages ជាការផ្លាស់ប្ដូរផ្សេង ហើយអាចដំឡើងកំណែថ្មី៖

~~~bash
sudo apt upgrade
~~~

មុនយល់ព្រម សូមពិនិត្យ packages ដែលនឹងដំឡើង កែ ឬដកចេញ។ សម្រាប់ automation scripts សូមប្រើ apt-get ឬ API ដែលឯកសាររបស់ distribution ណែនាំ ជំនួស output សម្រាប់ interactive use។

## ៤. Fedora និង DNF

~~~bash
dnf search curl
dnf info curl
sudo dnf install curl
dnf check-update
sudo dnf upgrade
~~~

DNF អាចស្នើឱ្យពិនិត្យ transaction មុនបន្ត។ អានបញ្ជី packages មុន confirm។

## ៥. Arch Linux និង pacman

~~~bash
pacman -Ss curl
pacman -Si curl
pacman -Q
~~~

ធ្វើ full system upgrade តាម workflow របស់ Arch៖

~~~bash
sudo pacman -Syu
~~~

ក្នុង Arch ជាទូទៅត្រូវធ្វើ full upgrade ជាជាង partial upgrade ដែលអាចបង្ក incompatibility។ អាន Arch documentation មុនកែ package database ឬបន្ថែម repository។

## ៦. ពិនិត្យ package ដែលបានដំឡើង

~~~bash
command -v curl
curl --version
~~~

បើ package មិនត្រូវការ អាចដកវាចេញតាម package manager របស់ distro។ ការដក package អាចដក dependencies ឬប៉ះកម្មវិធីផ្សេង; អាន transaction summary មុនបញ្ជាក់។ ក្នុងលំហាត់នេះ អ្នកអាចប្រើតែ search/show commands មិនចាំបាច់ install ឬដកអ្វីទេ។

## ៧. Security និង Maintenance

- ធ្វើ update តាម maintenance policy របស់ម៉ាស៊ីន។
- ប្រើ repository ផ្លូវការ ឬប្រភពដែល organization ទុកចិត្ត។
- កុំបិទ signature verification ដើម្បីបង្ខំ install package។
- កុំរត់ curl-to-shell scripts ដោយ sudo ដោយមិនពិនិត្យ script និងប្រភព។
- កត់ត្រា package និង version សម្រាប់ server administration។
- សាកល្បង update ក្នុង staging/VM មុន production។
- Backup និងមាន recovery plan មុន major upgrades។

## ៨. កិច្ចការអនុវត្ត

1. រត់ cat /etc/os-release ដើម្បីស្គាល់ distro។
2. ជ្រើសផ្នែក APT, DNF ឬ pacman តាម distro របស់អ្នក។
3. ប្រើ search/info command ដើម្បីស្វែងរក curl និងមើលព័ត៌មាន package។
4. រត់ command ពិនិត្យ installed packages ដែលត្រូវនឹង distro។
5. ពន្យល់ភាពខុសគ្នារវាង metadata update និង package upgrade។
6. ក្នុង VM សាកល្បងប៉ុណ្ណោះ បើចង់ install curl; អាន transaction summary មុនបញ្ជាក់។
7. កត់ត្រា repository source និង version ដែលបានឃើញ។

## សង្ខេប

Package manager គ្រប់គ្រងការដំឡើង និង dependencies ពី repositories។ Commands ខុសគ្នាតាម distribution។ Metadata refresh និង package upgrade ជាជំហានខុសគ្នា។ អាន transaction summary និងប្រើ trusted repositories មុនផ្លាស់ប្ដូរប្រព័ន្ធ។

## ឯកសារយោង

- [Ubuntu package management](https://help.ubuntu.com/community/AptGet/Howto)
- [DNF Command Reference](https://dnf.readthedocs.io/en/latest/command_ref.html)
- [Arch Linux pacman](https://wiki.archlinux.org/title/Pacman)
