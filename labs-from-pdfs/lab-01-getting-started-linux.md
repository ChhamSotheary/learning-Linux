# Lab ១៖ ចាប់ផ្តើម Linux និងស្គាល់ប្រព័ន្ធ

## ១. គោលបំណង

បន្ទាប់ពី Lab នេះ អ្នកអាច៖

- ចាប់ផ្តើម និងចូលប្រើ Linux VM។
- ពិនិត្យថា login ជា user ណា, hostname អ្វី, កំពុងនៅ directory ណា និងប្រើ kernel/distribution/version អ្វី។
- រុករក root directory tree និងស្គាល់តួនាទីរបស់ /etc, /var/log និង /home។
- បង្កើត local DVD repository សម្រាប់ RHEL-like VM ដែលដំណើរការ offline។
- រៀបចំ server information report ពី command output។

ពេលវេលាដើមប្រហែល ៩០ នាទី។ សម្រាប់ការសិក្សាដោយខ្លួនឯង អាចបែងចែកជា ២ វគ្គ៖ ដំឡើង VM ម្តង និងរៀន command/report ម្តង។

## ២. Linux និង distribution

Linux ជា kernel ដែលគ្រប់គ្រង CPU, memory, process និង devices។ Distribution (distro) គឺជា OS package ដែលរួមបញ្ចូល kernel, command-line tools, installer, package manager, service manager និង software ផ្សេងៗ។ RHEL, AlmaLinux, Rocky Linux, Ubuntu និង Debian សុទ្ធតែប្រើ Linux kernel តែ configuration និង package manager ខុសគ្នា។

RHEL family ប្រើ RPM packages និង DNF ជាទូទៅ; Debian/Ubuntu family ប្រើ DEB និង APT។ ដូច្នេះ command **dnf** ក្នុង Lab នេះមិនមែនជាជម្រើស universal សម្រាប់ Linux គ្រប់ distro ទេ។

## ៣. រៀបចំ VM

ឯកសារដើមណែនាំ VirtualBox VM ប្រហែល ២ CPU, RAM ២ GB និង virtual disk ២០ GB ដោយប្រើ RHEL 9 Binary DVD ISO។ AlmaLinux 9 ឬ Rocky Linux 9 អាចប្រើជាជម្រើសដែលមាន command ស្រដៀងគ្នា។ ត្រូវគោរពលក្ខខណ្ឌ download របស់ distribution ដែលអ្នកជ្រើស ហើយ verify ISO checksum តាមប្រភពផ្លូវការមុនប្រើ។

VM មាន disk និម្មិតរបស់វា ដាច់ពី disk ពិតរបស់ host តាម virtualizer។ ទោះជាយ៉ាងណា ត្រូវពិនិត្យថាអ្នកកំពុង command នៅក្នុង VM ត្រឹមត្រូវ មុនប្ដូរ storage។

### Installation outline

1. បង្កើត VM ថ្មី ឈ្មោះច្បាស់លាស់ ឧ. rhel9-lab1។
2. កំណត់ CPU, memory និង virtual disk។
3. ភ្ជាប់ Binary DVD ISO ទៅ optical drive។ Binary DVD មាន package សម្រាប់ offline install; boot/minimal ISO អាចទាមទារ network repository។
4. ចាប់ផ្តើម installer ហើយជ្រើស installation source ជា local media។
5. សម្រាប់ Lab ដំបូង ប្រើ installation destination automatic ដើម្បីកុំឱ្យប៉ះ disk ផ្សេង។ មេរៀន partitions/RAID នឹងរៀនលើ VM ដាច់ដោយឡែក។
6. កំណត់ root password ឯកជន និងបង្កើត user ធម្មតា ឧ. student01។ កុំដាក់ password ពិតនៅក្នុង screenshot ឬ GitHub។
7. បន្ទាប់ពីដំឡើង រក្សាទុក snapshot ឈ្មោះ lab1-start។

## ៤. Local DVD repository សម្រាប់ការងារ offline

VM ដែលមិនបាន register និងមិនមាន internet អាចមិនឃើញ online repositories។ សម្រាប់មេរៀននេះ អាច mount DVD ISO ជា local repository ដើម្បីដំឡើង package ដូចជា tree ដោយមិនភ្ជាប់ network។

សូមពិនិត្យឈ្មោះ optical device ជាមុន៖

~~~bash
lsblk
~~~

បើវាជា /dev/sr0 ហើយ ISO បានភ្ជាប់៖

~~~bash
sudo mkdir -p /mnt/dvd
sudo mount /dev/sr0 /mnt/dvd
~~~

បង្កើត repo file នៅ /etc/yum.repos.d/dvd.repo ជាមួយខ្លឹមសារតាម DVD layout របស់ distro៖

~~~ini
[dvd-BaseOS]
name=DVD BaseOS
baseurl=file:///mnt/dvd/BaseOS
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[dvd-AppStream]
name=DVD AppStream
baseurl=file:///mnt/dvd/AppStream
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
~~~

ផ្លូវ repository និង signing key ខាងលើសម្រាប់ RHEL 9 តាមឯកសារដើម។ Alma/Rocky អាចប្រើ key path ឬ repo structure ខុស។ កុំបិទ GPG checking ដើម្បីរំលង error; ពិនិត្យ ISO, mount path និង key path ជាមុន។

សាកល្បង៖

~~~bash
sudo dnf clean all
sudo dnf repolist
sudo dnf install tree
tree -L 1 /
~~~

រំពឹងថា repolist បង្ហាញ dvd-BaseOS និង dvd-AppStream។ បើ dnf បរាជ័យ ពិនិត្យថា ISO នៅតែភ្ជាប់ និង /mnt/dvd មាន directory BaseOS និង AppStream។

## ៥. Command ដំបូងៗ និងអត្ថន័យ

~~~bash
whoami
hostname
pwd
date
echo $SHELL
uname -r
cat /etc/os-release
ls
ls -l /
man ls
~~~

- **whoami** បង្ហាញ effective username របស់ command បច្ចុប្បន្ន។
- **hostname** បង្ហាញឈ្មោះម៉ាស៊ីន។
- **pwd** បង្ហាញ current working directory។
- **date** បង្ហាញ date/time តាម timezone/config។
- **echo $SHELL** បង្ហាញ shell ដែលកំណត់សម្រាប់ login user; shell បច្ចុប្បន្នអាចមានភាពខុសតាម session។
- **uname -r** បង្ហាញ kernel release មិនមែន distro version។
- **/etc/os-release** បង្ហាញ distro identity/version។
- **ls -l /** បង្ហាញ entries នៅ root directory ជាមួយ metadata។
- **man ls** បើក manual; ចុច q ដើម្បីចេញ។

Linux គោរពអក្សរធំ/តូច៖ File.txt និង file.txt អាចជាឯកសារខុសគ្នា។ ចន្លោះក្នុង path ក៏សំខាន់ដែរ។ Tab completion និង arrow-up ជួយកាត់បន្ថយការវាយខុស។

## ៦. រុករក directory tree

Linux បង្ហាញ filesystem ជា tree តែមួយ ចាប់ផ្តើមពី /. Disk ឬ partition ផ្សេងត្រូវបាន mount ទៅ directory មួយក្នុង tree នេះ។

~~~bash
cd /
pwd
ls
cd /etc
pwd
ls | head -n 10
cd /var/log
pwd
ls
cd /home
ls
cd ~
pwd
cd /tmp
cd ..
pwd
~~~

- **/** ជា root នៃ directory tree។
- **/etc** ផ្ទុក system-wide configuration។
- **/var/log** ជាទីតាំង log ទូទៅ។
- **/home** ជាផ្ទះរបស់ users ធម្មតា។
- **/root** ជា home directory របស់ root account មិនមែនជា root of filesystem។
- **/tmp** សម្រាប់ temporary files; កុំសន្មតថាវាត្រូវរក្សាទុកជាអចិន្ត្រៃយ៍។
- **~** ជាផ្លូវកាត់ទៅ home directory របស់ user បច្ចុប្បន្ន។
- **..** មានន័យថា parent directory។

## ៧. រាយការណ៍ព័ត៌មាន server

~~~bash
hostname
cat /etc/os-release
uname -r
whoami
date
df -h /
free -h
uptime
~~~

**df -h /** បង្ហាញ filesystem space សម្រាប់ root mount; **free -h** បង្ហាញ memory/swap summary; **uptime** បង្ហាញរយៈពេលចាប់ពី boot និង load averages។ លទ្ធផល username, hostname, kernel version និង resource sizes ខុសគ្នាតាម VM។ កុំ copy sample result ជំនួសលទ្ធផលរបស់ម៉ាស៊ីនអ្នក។

មុនកែ production server គួរពិនិត្យថាតើមាន backup/snapshot, ផែនការ rollback និងការអនុម័តសមស្របដែរឬទេ។

## ៨. កំហុសដែលជួបញឹកញាប់

- Installer ស្នើ network repository៖ ប្រហែលប្រើ boot ISO ជំនួស Binary DVD ISO។
- **mount: no medium found**៖ ISO មិនបាន attach ទៅ optical drive។
- **dnf repolist** មិនឃើញ DVD៖ ពិនិត្យ mount point, repo file និង path BaseOS/AppStream។
- GPG error៖ ពិនិត្យ key/repo metadata; កុំបិទ signature checks ដើម្បីបង្ខំដំឡើង។
- **cd** មិនដំណើរការ៖ ពិនិត្យ path, អក្សរធំតូច និងចន្លោះ។
- Screenshot បង្ហាញព័ត៌មានផ្ទាល់ខ្លួន៖ កុំបញ្ចូលក្នុង public repository; លុប/blur មុន share។

## ៩. សំណួរត្រួតពិនិត្យ

1. Linux kernel ខុសពី Linux distribution ដូចម្តេច?
2. Kernel គ្រប់គ្រងអ្វីខ្លះ?
3. Shell មានតួនាទីអ្វី?
4. ហេតុអ្វី Linux filesystem ត្រូវបានហៅថា tree មួយដែលចាប់ផ្តើមពី /?
5. ឈ្មោះ command package manager របស់ RHEL family និង Debian family ជាអ្វី?
6. តើ /etc, /var/log និង /home ប្រើសម្រាប់អ្វី?
7. **uname -r** បង្ហាញ kernel ឬ distro version?

<details>
<summary>ចម្លើយសម្រាប់ពិនិត្យខ្លួនឯង</summary>

1. Linux ជា kernel; distro ជាកញ្ចប់ OS ដែលរួមមាន kernel និង user-space software/tools។
2. Kernel គ្រប់គ្រង process, memory, device និងការចូលប្រើ hardware។
3. Shell អាន command របស់ user ហើយចាប់ផ្តើមកម្មវិធី/command។
4. គ្រប់ file/device/mount ស្ថិតក្រោម root /; disk ផ្សេងត្រូវ mount នៅក្នុង tree នេះ។
5. RHEL family ប្រើ **dnf/rpm**; Debian family ប្រើ **apt/dpkg** ជាទូទៅ។
6. **/etc** configuration, **/var/log** logs, **/home** user home directories។
7. **uname -r** បង្ហាញ kernel release។

</details>
