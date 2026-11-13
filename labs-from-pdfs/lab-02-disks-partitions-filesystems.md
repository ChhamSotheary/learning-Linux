# Lab ២៖ Disk, Partition និង Filesystem

## ១. គោលបំណង

បន្ទាប់ពី Lab នេះ អ្នកអាច៖

- អានទំនាក់ទំនងរវាង disk, partition, filesystem និង mount point។
- ពិនិត្យ /etc/fstab និងពន្យល់ fields ទាំងប្រាំមួយ។
- បន្ថែម virtual disk ទីពីរ, បង្កើត GPT partition, format ជា XFS និង mount នៅ /data។
- ធ្វើឱ្យ mount បន្តក្រោយ reboot ដោយប្រើ UUID។
- រៀបចំ partition plan សម្រាប់ file server តូច។

## ២. គោលគំនិតមូលដ្ឋាន

លំដាប់ទូទៅ៖

~~~text
Physical/virtual disk → partition → filesystem → mount point → files
~~~

- **Disk** ជា block device ដែលផ្តល់ storage; ក្នុង VM វាជា virtual disk file។
- **Partition** ជាផ្នែកដែលកំណត់ព្រំដែនក្នុង disk។
- **Filesystem** ដូចជា XFS ឬ ext4 រៀបចំ metadata និង file data ក្នុង partition។
- **Mount point** ជា directory ដែល filesystem ថ្មីត្រូវបង្ហាញក្នុង tree របស់ Linux។
- **UUID** ជា identifier របស់ filesystem/partition ដែលជាទូទៅមានស្ថិរភាពជាងឈ្មោះ /dev/sdX ដែលអាចប្ដូរលំដាប់។

ការបង្កើត filesystem ដោយ **mkfs** សរសេរ metadata ថ្មី ហើយអាចបំផ្លាញ data ចាស់លើ partition នោះ។ **fdisk** សរសេរ partition table; វាមិនមែនជា command សម្រាប់អានតែប៉ុណ្ណោះទេ។

## ៣. Safety និងបរិស្ថាន

Lab នេះត្រូវការ RHEL 9 VM ពី Lab ១, user មាន sudo និង virtual disk ទំនេរប្រហែល ២ GB។ បង្កើត snapshot ឈ្មោះ lab2-start មុនចាប់ផ្តើម។

**ឈ្មោះ /dev/sdb ក្នុង PDF គ្រាន់តែជាឧទាហរណ៍។** VM របស់អ្នកអាចបង្ហាញឈ្មោះផ្សេង។ មុន command ដែលសរសេរ partition ឬ format សូមពិនិត្យ lsblk ហើយបញ្ជាក់ថា device ថ្មីគ្មាន mount point និងជាទំហំដែលអ្នកទើបបន្ថែម។ កុំរត់ fdisk, mkfs ឬ mount ដោយចម្លង /dev/sda ពីឧទាហរណ៍។

## ៤. ពិនិត្យ disk និង mount ដែលមានស្រាប់

~~~bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
df -hT
sudo fdisk -l /dev/sda
sudo blkid
findmnt /
cat /etc/fstab
free -h
~~~

- **lsblk** បង្ហាញ disk/partition ជា tree។
- **df -hT** បង្ហាញទំហំប្រើ/ទំនេរ និង filesystem type របស់ mount។
- **fdisk -l** បង្ហាញ partition table; **-l** មានន័យថារាយបញ្ជី មិនចូល interactive edit។
- **blkid** បង្ហាញ UUID និង filesystem signatures។
- **findmnt /** បង្ហាញ source device របស់ root mount។
- **cat /etc/fstab** អាន config សម្រាប់ mount នៅ boot។
- **free -h** បង្ហាញ memory/swap; swap ជា virtual memory area មិនមែន file data filesystem ធម្មតាទេ។

ឈ្មោះ sda, sdb អាចខុសតាម VM/device discovery។ ប្រើ UUID និង lsblk ដើម្បីផ្គូផ្គងតួនាទី មិនសន្និដ្ឋានតាមឈ្មោះតែមួយ។

## ៥. /etc/fstab មាន fields ប្រាំមួយ

ឧទាហរណ៍ទម្រង់៖

~~~text
UUID=...  /data  xfs  defaults  0  0
~~~

Fields តាមលំដាប់៖

1. **Device/spec**៖ UUID, label ឬ device path។
2. **Mount point**៖ directory ដូចជា /data។
3. **Filesystem type**៖ ដូចជា xfs, ext4, swap។
4. **Mount options**៖ ដូចជា defaults និង options ផ្សេង។
5. **dump**៖ field ចាស់សម្រាប់ dump utility; ជាទូទៅប្រើ 0។
6. **fsck pass**៖ លំដាប់ filesystem check នៅ boot; តម្លៃត្រូវអាស្រ័យលើ filesystem/config។ សម្រាប់ XFS តាមឧទាហរណ៍នេះគឺ 0។

Whitespace បំបែក fields។ កុំដាក់ UUID គំរូជំនួស UUID ពិតរបស់ partition របស់អ្នក។

## ៦. បន្ថែម virtual disk ថ្មី

1. បិទ VM ដោយច្បាស់លាស់ មិន suspend។
2. ក្នុង VirtualBox បន្ថែម virtual disk VDI ថ្មី ទំហំ 2 GB ទៅ controller។
3. ចាប់ VM វិញ។
4. ពិនិត្យ៖

~~~bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
~~~

ស្វែងរក disk ថ្មីទំហំប្រហែល 2 GB ដែលមិនមាន partitions/mounts។ បើមិនច្បាស់ សូមឈប់ ហើយកុំបន្តទៅ fdisk។

## ៧. បង្កើត GPT partition និង filesystem XFS

ដំណាក់កាលនេះបំផ្លាញ partition table/filesystem នៅលើ disk ដែលជ្រើស។ ធ្វើតែក្នុង VM សាកល្បង និងលើ disk ថ្មីដែលបានផ្ទៀងផ្ទាត់។

~~~bash
sudo fdisk /dev/sdX
~~~

ជំនួស /dev/sdX ដោយឈ្មោះ disk ថ្មីដែលបានបញ្ជាក់ពី lsblk។ ក្នុង fdisk៖

- **g** បង្កើត GPT partition table ថ្មីលើ disk នោះ។
- **n** បង្កើត partition ថ្មី។
- ចុច Enter ដើម្បីទទួល default partition number/first sector។
- សម្រាប់ last sector វាយ **+1G** ដើម្បីបង្កើតប្រហែល 1 GiB។
- **p** ពិនិត្យតារាងមុនសរសេរ។
- **w** សរសេរចូល disk និងចេញ។ មុន w អ្នកអាចប្រើ **q** ដើម្បីចេញដោយមិនរក្សាការកែប្រែ។

ក្រោយចេញ៖

~~~bash
lsblk -f
~~~

បញ្ជាក់ថាបានបង្កើត partition មួយ ដូចជា /dev/sdX1 ហើយវាជា partition របស់ disk ថ្មី។ បន្ទាប់មក format៖

~~~bash
sudo mkfs.xfs /dev/sdX1
~~~

**mkfs.xfs** បង្កើត XFS filesystem ហើយសម្អាត metadata ចាស់លើ partition ដែលបានបញ្ជាក់។ ពិនិត្យ /dev/sdX1 ឱ្យត្រឹមមុន Enter។

## ៨. Mount និងសាកល្បងទិន្នន័យ

~~~bash
sudo mkdir -p /data
sudo mount /dev/sdX1 /data
findmnt /data
df -hT /data
echo "Hello Linux Lab" | sudo tee /data/hello.txt
cat /data/hello.txt
~~~

រំពឹងថា findmnt បង្ហាញ source partition និង df -hT បង្ហាញ type xfs ជាមួយទំហំប្រហែល 1 GB។ Unmount/mount វិញសម្រាប់សាកល្បងថា data នៅតែមាននៅលើ disk៖

~~~bash
sudo umount /data
sudo mount /dev/sdX1 /data
cat /data/hello.txt
~~~

Unmount មិនលុប filesystem ទេ; វាគ្រាន់តែដក filesystem ចេញពីទីតាំង mount។

## ៩. Mount ជាអចិន្ត្រៃយ៍ដោយ UUID

ស្វែងរក UUID ពិត៖

~~~bash
sudo blkid /dev/sdX1
~~~

កែ /etc/fstab បន្ថែមបន្ទាត់ដែលប្រើ UUID នោះ និង mount point /data។ បន្ទាប់មកសាក config មុន reboot៖

~~~bash
sudo umount /data
sudo mount -a
findmnt /data
df -hT /data
~~~

**mount -a** ព្យាយាម mount entries ដែលសមស្របក្នុង fstab។ បើវាបង្ហាញ error កុំ reboot; កែ path/UUID/type/options ជាមុន ហើយសាកឡើងវិញ។ បន្ទាប់ពីជោគជ័យ ទើប reboot ក្នុង VM ហើយផ្ទៀងផ្ទាត់ findmnt /data។

បន្ទាត់ fstab ខុសអាចធ្វើឱ្យ boot ចូល emergency mode។ រក្សា snapshot និងដឹងពីរបៀប restore ឬកែ config ក្នុង emergency mode មុនកែ file។

## ១០. រចនា partition plan

ឧទាហរណ៍ file server disk 100 GB តាមលំហាត់៖

| Mount point | Filesystem | ទំហំឧទាហរណ៍ | មូលហេតុ |
|---|---|---:|---|
| /boot | XFS | 1 GB | ផ្ទុក boot files |
| swap | swap | 4 GB | ជា swap area; ទំហំត្រូវគិតតាម RAM/workload |
| / | XFS | 20 GB | ប្រព័ន្ធ និងកម្មវិធី |
| /var | XFS | 15 GB | បំបែក logs/data ដែលអាចកើនឡើង |
| /home | XFS | 60 GB | ឯកសារអ្នកប្រើ និងគ្រប់គ្រង backup ដាច់ដោយឡែក |

តួលេខនេះគ្រាន់ជាឧទាហរណ៍ សម្រាប់លំហាត់ បូកសរុបតិចជាង 100 GB។ Production sizing ត្រូវផ្អែកលើ workload, log retention, backup, filesystem overhead និង growth មិនមែនចម្លងតារាងនេះដោយផ្ទាល់។

## ១១. សំណួរត្រួតពិនិត្យ

1. MBR និង GPT ខុសគ្នាដូចម្តេច?
2. Partition ខុសពី filesystem ដូចម្តេច?
3. ហេតុអ្វីប្រើ UUID ក្នុង fstab ជាង /dev/sdX?
4. mount -a ធ្វើអ្វី ហើយហេតុអ្វីសាកមុន reboot?
5. តើ mkfs.xfs ប៉ះពាល់ដល់ data នៅលើ partition ដូចម្តេច?
6. ហេតុអ្វី /home ឬ /var អាចដាក់ partition ដាច់ដោយឡែក?
7. តើអ្នកធ្វើអ្វី បើ mount -a បង្ហាញ error?

<details>
<summary>ចម្លើយសម្រាប់ពិនិត្យខ្លួនឯង</summary>

1. MBR ជាទម្រង់ចាស់ មានកម្រិតទំហំប្រហែល 2 TiB និង primary partitions ចំនួនកំណត់; GPT គាំទ្រ disks ធំ និង partitions ច្រើនជាង។ តម្លៃជាក់លាក់អាស្រ័យលើ tool/OS។
2. Partition ជាផ្នែកនៃ disk; filesystem ជាទម្រង់ metadata/data ដែលសរសេរនៅក្នុង partition។
3. /dev/sdX អាចប្តូរឈ្មោះតាមលំដាប់រកឃើញ device; UUID ជួយឱ្យ mount សំដៅទៅ filesystem ត្រឹមត្រូវ។
4. វាព្យាយាម mount fstab entries; ការសាកមុន reboot ធ្វើឱ្យរក typo ដោយមិនធ្វើឱ្យ boot ជាប់។
5. mkfs.xfs សរសេរ filesystem ថ្មី ហើយអាចបំផ្លាញទិន្នន័យ filesystem ចាស់លើ target partition។
6. អាចគ្រប់គ្រងទំហំ, backup, reinstall និងបញ្ហា log/data growth ដាច់ពី root filesystem។
7. កុំ reboot; ពិនិត្យ error, UUID, mount point, type និង options ហើយសាក mount -a ម្តងទៀតក្នុង VM។

</details>
