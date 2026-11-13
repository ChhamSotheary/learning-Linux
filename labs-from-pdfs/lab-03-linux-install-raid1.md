# Lab ៣៖ ដំឡើង Linux ជាមួយ Partition ដាច់ដោយឡែក និង RAID 1

## ១. គោលបំណង

នៅចុងបញ្ចប់ អ្នកអាច៖

- រៀបចំ VM ថ្មីសម្រាប់ការដំឡើង Linux ដោយសុវត្ថិភាព។
- បែងចែក /boot, swap, / និង /home ក្នុង installer។
- ពន្យល់ RAID 1 និងគណនាទំហំប្រើបាន។
- ពិនិត្យ Linux software RAID ដោយ lsblk, /proc/mdstat និង mdadm។
- សាកល្បង disk failure និង recovery ក្នុង VM បោះចោលប៉ុណ្ណោះ។
- ប្រៀបធៀប RAID និង backup។

## ២. RAID 1 ជាអ្វី?

RAID 1 គឺការសរសេរទិន្នន័យដូចគ្នាទៅ disk ច្រើនជាសមាជិក mirror។ បើ mirror មាន disk ពីរទំហំ 10 GB នោះទំហំប្រើសម្រាប់ data ប្រហែល 10 GB មុនគិត overhead; មិនមែន 20 GB ទេ។ RAID អាចជួយឱ្យ array នៅដំណើរការពេល disk មួយខូច ប៉ុន្តែមិនជំនួស backup ទេ៖ ការលុបឯកសារ, malware ឬ filesystem corruption អាចត្រូវបានសរសេរទៅ mirror ទាំងអស់។

RAID 1 គឺជាការការពារប្រឆាំងនឹង disk failure មួយ ក្នុងលក្ខខណ្ឌថា disk មួយទៀត និង controller ដំណើរការ។ RAID មិនធានាថា OS នឹង boot បានគ្រប់ configuration ទេ; ការកំណត់ bootloader និង firmware ត្រូវបានសាកល្បងផងដែរ។

## ៣. បរិស្ថានសាកល្បង និងការប្រុងប្រយ័ត្ន

Lab នេះត្រូវការ VirtualBox, RHEL 9 Binary DVD ISO និងកន្លែងទំនេរប្រហែល 25 GB សម្រាប់ VM និង virtual disks ពីរទំហំ 10 GB។ បង្កើត VM ថ្មីឈ្មោះ rhel9-raid ដាច់ពី VM ក្នុង Lab 1 និង Lab 2។ កំណត់ CPU 2, RAM 2 GB ឬច្រើនជាងនេះ ហើយបន្ថែម virtual disks 10 GB ចំនួនពីរ។ អាចបិទ network adapter សម្រាប់ការដំឡើង offline។

**ធ្វើតែជាមួយ VM សាកល្បងដែលអាចលុបបាន។ កុំដក disk ឬសរសេរ RAID commands លើកុំព្យូទ័រពិត ឬ production server។** មុន simulation ត្រូវថត snapshot ហើយផ្ទៀងផ្ទាត់ឈ្មោះ array និង member disks ជាក់ស្តែង។ ឈ្មោះ md126, md127 ឬ /dev/sdb4 ក្នុងឯកសារគ្រាន់តែជាឧទាហរណ៍; លទ្ធផលរបស់អ្នកអាចខុស។

## ៤. គ្រោង partition ក្នុងលំហាត់

ឧទាហរណ៍លំហាត់ប្រើ៖

| Mount point / type | ទំហំគោលដៅ | ការកំណត់ |
|---|---:|---|
| /boot | 1 GiB | Standard partition, XFS |
| swap | 1 GiB | Standard swap |
| / | 5 GiB | RAID 1, XFS |
| /home | 2 GiB | RAID 1, XFS |

/ និង /home ត្រូវបានដាក់លើ RAID 1 តាមគោលបំណងមេរៀន។ /boot ត្រូវបានទុកជា standard partition ក្នុងឧទាហរណ៍នេះ ដើម្បីឱ្យការរៀនសាមញ្ញ។ វាមិនមែនជាគំរូ production សម្រាប់គ្រប់ម៉ាស៊ីនទេ។ ប្រព័ន្ធ UEFI ជាទូទៅត្រូវការ EFI System Partition ដែលមាន filesystem និង mount point ផ្សេង; របៀបដាក់ boot partitions លើ RAID អាស្រ័យលើ installer, bootloader និងគោលការណ៍របស់ប្រព័ន្ធ។

## ៥. ដំឡើងក្នុង VirtualBox

1. បង្កើត VM ថ្មី ហើយភ្ជាប់ RHEL 9 Binary DVD ISO។
2. ភ្ជាប់ virtual disk ទំហំ 10 GB ចំនួនពីរទៅ VM។
3. ចាប់ផ្តើមពី ISO ហើយជ្រើស Install Red Hat Enterprise Linux 9។
4. ជ្រើសភាសា និង keyboard ដែលសមស្រប។
5. ចូល Installation Destination ហើយបញ្ជាក់ថាបានជ្រើសតែ virtual disks ពីររបស់ VM នេះ។
6. ជ្រើស Custom partitioning ហើយបង្កើត mount points តាមតារាងខាងលើ។
7. សម្រាប់ / និង /home ជ្រើស RAID ជា device type និង RAID1 ជា level; បញ្ជាក់ថា member partitions ត្រូវបានដាក់លើ disks ទាំងពីរ។
8. កំណត់ /boot និង swap ជា standard តាមឧទាហរណ៍លំហាត់។
9. ពិនិត្យ Installation Summary ឱ្យត្រូវ មុនចុច Begin Installation។
10. កំណត់ root password និងអ្នកប្រើធម្មតាតាមតម្រូវការថ្នាក់។
11. បន្ទាប់ពីបញ្ចប់ ដក ISO ចេញពី virtual optical drive ហើយ reboot។
12. បង្កើត snapshot ឈ្មោះ lab3-installed មុនចាប់ផ្តើមការសាកល្បង failure។

Installer របស់ RHEL អាចផ្លាស់ប្តូរ UI ឬស្លាកជម្រើសតាមកំណែ។ ប្រសិនបើ installer មិនអនុញ្ញាត layout ដូចគ្នា សូមកុំបង្ខំ; កត់ត្រា UI និងពិនិត្យតម្រូវការ UEFI/BIOS, partition type និងទំហំ disk ជាមុន។

## ៦. ផ្ទៀងផ្ទាត់ RAID ក្រោយ boot

រត់ commands ដែលអានស្ថានភាព៖

~~~bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
cat /proc/mdstat
df -hT / /home
sudo mdadm --detail /dev/md127
~~~

ឈ្មោះ array អាចជា /dev/md126, /dev/md127 ឬឈ្មោះផ្សេង។ ស្វែងរកឈ្មោះពិតក្នុង lsblk និង /proc/mdstat មុនប្រើ mdadm --detail។ កុំចម្លង md127 ដោយស្មានថាត្រឹមត្រូវ។

- **lsblk** បង្ហាញ disk, partitions និង RAID device ជា tree។
- **/proc/mdstat** បង្ហាញ software RAID arrays និងស្ថានភាព sync។
- **df -hT** បង្ហាញ filesystem ដែល mount នៅ / និង /home។
- **mdadm --detail** បង្ហាញសមាជិក array និងស្ថានភាពរបស់វា។
- ស្ថានភាព **[UU]** ជាទូទៅបង្ហាញថាសមាជិកទាំងពីរមានវត្តមាន។
- ស្ថានភាព **[U_]** ឬ **[_U]** មានន័យថាសមាជិកមួយខ្វះ/មិនសកម្ម; ពិនិត្យ output លម្អិត មុនធ្វើអ្វីបន្ថែម។

រក្សា snapshot មុន simulation ហើយកត់ត្រាឈ្មោះ array និង partitions របស់សមាជិកតាម output ពិត។

## ៧. សាកល្បង disk failure ក្នុង VM បោះចោល

ផ្នែកនេះបង្កើតស្ថានភាព degraded ដោយចេតនា។ ធ្វើតែលើ array /home ក្នុង VM សាកល្បងដែលមាន snapshot។ កុំធ្វើលើ array / ឬ disk ពិត។ មុនចាប់ផ្តើម៖

1. ពិនិត្យ lsblk, /proc/mdstat និង sudo mdadm --detail ដើម្បីស្វែងរក array /home ពិត និង member partition របស់វា។
2. កត់ត្រាឈ្មោះពិត—កុំប្រើ /dev/mdX ឬ /dev/sdb4 ទាំងស្រុងដោយមិនជំនួសវា។
3. ផ្ទៀងផ្ទាត់ម្ដងទៀតថា array នោះគឺ /home នៅក្នុង VM lab។
4. បង្កើត snapshot ឬធានាថាអាច restore បាន។

គំរូខាងក្រោមត្រូវជំនួស /dev/mdX និង /dev/sdY# ដោយឈ្មោះពិតដែលបានផ្ទៀងផ្ទាត់៖

~~~bash
sudo mdadm /dev/mdX --fail /dev/sdY#
cat /proc/mdstat
sudo mdadm --detail /dev/mdX
ls /home
~~~

កុំដំណើរការបន្ទាត់ failure រហូតដល់បានផ្ទៀងផ្ទាត់ឈ្មោះទាំងពីរ។ សង្កេតស្ថានភាព degraded ហើយពិនិត្យថាឯកសារក្នុង /home នៅអាចអានបាន។ RAID មិនដូចគ្នានឹង disk ដែលអាចដកចេញរូបរាងកាយទេ; command នេះសម្គាល់ member ជា failed ក្នុង software RAID។

## ៨. ដក member ដែល failed និងបន្ថែមវិញ

នៅតែប្រើតែ VM សាកល្បង និង member ដែលបានផ្ទៀងផ្ទាត់៖

~~~bash
sudo mdadm /dev/mdX --remove /dev/sdY#
sudo mdadm /dev/mdX --add /dev/sdY#
watch cat /proc/mdstat
~~~

បិទការមើលដោយចុច Ctrl+C បន្ទាប់ពីឃើញ recovery ចប់។ តាមដានរហូតស្ថានភាពត្រឡប់ទៅ **[UU]** ហើយប្រើ lsblk និង mdadm --detail ផ្ទៀងផ្ទាត់។ ប្រសិនបើ disk virtual ត្រូវបានដកចេញពី VM មែន អ្នកត្រូវភ្ជាប់/បង្កើត disk ជំនួស និង partition តាមរបៀបសមស្រប មុនបន្ថែមចូល array; កុំប្រើ command ដោយសន្មតថា member ចាស់នៅតែមាន។

បើស្ថានភាពមិនច្បាស់ សូមឈប់ មើល mdadm --detail និងកំណត់ហេតុ ហើយ restore snapshot។ កុំសាក command ផ្សេងៗលើ array ដែលអ្នកមិនទាន់ស្គាល់។

## ៩. ការប្រៀបធៀប RAID levels

- **RAID 1**៖ mirror; អាចប្រើ disk 2 ឬច្រើនតាម implementation; usable capacity តាមសមត្ថភាព mirror ដែលអនុវត្តបាន។
- **RAID 5**៖ ត្រូវការ disk យ៉ាងតិច 3; parity ចែកចាយ; usable capacity ប្រហែលទំហំ disk តូចបំផុត × (ចំនួន disk − 1)។
- **RAID 6**៖ ត្រូវការ disk យ៉ាងតិច 4; parity ពីរ; អាចអត់ទ្រាំ failure ច្រើនជាង RAID 5 ក្នុងលក្ខខណ្ឌសមស្រប។
- **RAID 10**៖ ត្រូវការ disk យ៉ាងតិច 4 ក្នុងការរៀបចំទូទៅ; combine mirror និង striping; usable capacity ជាទូទៅប្រហែលពាក់កណ្តាល មុន overhead។

ចំនួនអតិបរមានៃ disk failure ដែល array អាចអត់ទ្រាំបាន អាស្រ័យលើ layout និងទីតាំង disk ដែលខូច។ សូមកុំយកសេចក្តីសង្ខេបខាងលើជំនួសឯកសារ design របស់ storage system ពិត។

## ១០. RAID មិនមែនជា Backup

RAID ផ្តល់ availability ពេល hardware disk ខូច តាមកម្រិតដែល level នោះគាំទ្រ។ Backup ជាច្បាប់ចម្លងដែលអាចស្ដារទិន្នន័យពីការលុបខុស, malware, file corruption, ការខូចម៉ាស៊ីន ឬគ្រោះថ្នាក់តំបន់។ File ដែលលុបលើ RAID 1 នឹងត្រូវលុបពី mirror ផ្សេងដែរ។ ប្រព័ន្ធពិតត្រូវមាន backup ដាច់ពី host/storage ដើម និងធ្វើ restore test ជាប្រចាំ។

## ១១. សំណួរត្រួតពិនិត្យ

1. បើ mirror RAID 1 មាន disk 10 GB ពីរ តើទំហំ data ប្រហែលប៉ុន្មាន ហេតុអ្វី?
2. តើ [UU] និង [U_] ប្រាប់អ្វី?
3. ហេតុអ្វី simulation ត្រូវធ្វើលើ /home ក្នុង VM បោះចោល?
4. តើ RAID 1 ជំនួស backup បានទេ? ផ្តល់ឧទាហរណ៍។
5. តើហេតុអ្វីមិនគួរសន្មតថា array ឈ្មោះ /dev/md127 ជានិច្ច?
6. តើ UEFI អាចត្រូវការផ្នែក partition បន្ថែមអ្វី?
7. បន្ទាប់ពីបន្ថែម member វិញ តើត្រូវពិនិត្យអ្វីមុននិយាយថា recovery ចប់?

<details>
<summary>ចម្លើយសម្រាប់ពិនិត្យខ្លួនឯង</summary>

1. ប្រហែល 10 GB មុន overhead ព្រោះទិន្នន័យត្រូវបាន mirror ទៅ disks ទាំងពីរ។
2. [UU] បង្ហាញថាសមាជិកទាំងពីរមានសកម្មភាព; [U_] បង្ហាញថាសមាជិកមួយមិនមាន/មិនសកម្ម។ ពិនិត្យ mdadm detail ជាមួយ។
3. ដើម្បីកាត់បន្ថយហានិភ័យបាត់បង់ប្រព័ន្ធ ឬទិន្នន័យពិត និងអាច restore snapshot បាន។
4. មិនបានទេ; ការលុបឯកសារខុសអាច replicate ទៅ mirrors ដូច្នេះត្រូវមាន backup ផ្សេង។
5. ឈ្មោះ array អាចបែងចែកខុសគ្នាតាម boot និងការរកឃើញ device; ត្រូវប្រើ output ពិត។
6. ជាទូទៅត្រូវការ EFI System Partition; ការរៀបចំ boot លើ RAID អាស្រ័យលើ firmware និង bootloader។
7. តាមដាន /proc/mdstat រហូត recovery ចប់ និងស្ថានភាព array ត្រឡប់ជា [UU] ហើយផ្ទៀងផ្ទាត់ mdadm --detail។

</details>
