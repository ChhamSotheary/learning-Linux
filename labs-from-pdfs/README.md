# Lab Linux ពីឯកសារសាកល្បងសាកលវិទ្យាល័យ

ថតនេះរៀបចំ Lab ជាភាសាខ្មែរ ដោយមានគោលបំណង ពន្យល់គំនិត ជំហានអនុវត្ត សុវត្ថិភាព លទ្ធផលរំពឹង និងសំណួរពិនិត្យខ្លួនឯង។

## មេរៀនក្នុងថត

1. [Lab ១៖ ចាប់ផ្តើម Linux និងស្គាល់ប្រព័ន្ធ](lab-01-getting-started-linux.md)
2. [Lab ២៖ Disk, Partition និង Filesystem](lab-02-disks-partitions-filesystems.md)
3. [Lab ៣៖ Partition ដាច់ដោយឡែក និង RAID 1](lab-03-linux-install-raid1.md)
4. [RAID Levels៖ មគ្គុទ្ទេសក៍ជារូបភាព](raid-levels-visual-guide.md) — ប្រៀបធៀប RAID 0, 1, 5, 6 និង 10 ដោយគំនូសបង្ហាញ និងឧទាហរណ៍គណនាទំហំ។

## បរិស្ថានដែលមេរៀននេះរំពឹង

Lab ១–៣ ផ្អែកលើ RHEL 9 ឬ AlmaLinux/Rocky Linux 9 ក្នុង VirtualBox។ វគ្គ Linux ផ្នែកផ្សេងក្នុង repository អាចប្រើ Ubuntu/Debian; package manager និង installer ខុសគ្នា។ មេរៀននេះរក្សាបរិស្ថាន RHEL-like ដើម្បីស្របតាមឯកសារដើម។

## សុវត្ថិភាពមុនអនុវត្ត

- អនុវត្តក្នុង VM ដែលអ្នកអាចបោះចោល ឬស្ដារពី snapshot បាន។ កុំប្រើ disk របស់ Windows/host ឬ server ពិត។
- មុន command ដែលប្ដូរ disk សូមពិនិត្យ **lsblk** និងបញ្ជាក់ឈ្មោះ disk ថ្មីម្តងទៀត។
- **fdisk** កែ partition table ហើយ **mkfs** បង្កើត filesystem ថ្មីលើ device ដែលបានជ្រើស ដែលអាចបំផ្លាញទិន្នន័យចាស់។
- Lab RAID បង្កើត និងសាក fail លើ software RAID ក្នុង VM ប៉ុណ្ណោះ។
- កុំ commit screenshot ដែលបង្ហាញឈ្មោះអ្នកប្រើ, hostname, IP ឬទិន្នន័យផ្ទាល់ខ្លួនទៅ GitHub សាធារណៈ។
- សេចក្ដីណែនាំ submit ក្នុងឯកសារដើមជាការងារសម្រាប់ថ្នាក់រៀន។ សូមអនុវត្តតាមការណែនាំរបស់គ្រូសម្រាប់ការបញ្ជូនការងារ; កុំបង្ហោះព័ត៌មានផ្ទាល់ខ្លួនជាសាធារណៈ។

## ផែនការរៀន

រៀន Lab ១ មុន ដើម្បីស្គាល់ OS និង command។ Lab ២ បន្ថែម virtual disk ទីពីរ ដើម្បីរៀន partition និង mount។ Lab ៣ បង្កើត VM ថ្មីដែលមាន disk ពីរ សម្រាប់ RAID 1។ បន្ទាប់មករៀន [មគ្គុទ្ទេសក៍ RAID Levels](raid-levels-visual-guide.md) ដើម្បីប្រៀបធៀប RAID ផ្សេងៗ។