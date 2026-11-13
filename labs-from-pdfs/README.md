# Lab Linux ពីឯកសារសាកល្បងសាកលវិទ្យាល័យ

ថតនេះរៀបចំ Lab ៣ មេរៀនពីឯកសារបង្រៀន Linux System Administration Module 1–3 ជាភាសាខ្មែរ។ ខ្លឹមសារត្រូវបានរៀបចំឡើងវិញជាមេរៀន មានគោលបំណង ពន្យល់គំនិត ជំហានអនុវត្ត លទ្ធផលរំពឹង សំណួរត្រួតពិនិត្យ និងចម្លើយសម្រាប់ពិនិត្យខ្លួនឯង។

## មេរៀនក្នុងថត

1. [Lab ១៖ ចាប់ផ្តើម Linux និងស្គាល់ប្រព័ន្ធ](lab-01-getting-started-linux.md)
2. [Lab ២៖ Disk, Partition និង Filesystem](lab-02-disks-partitions-filesystems.md)
3. [Lab ៣៖ Partition ដាច់ដោយឡែក និង RAID 1](lab-03-separate-partitions-raid1.md)

## បរិស្ថានដែលមេរៀននេះរំពឹង

ឯកសារដើមរៀបចំសម្រាប់ RHEL 9 ឬ AlmaLinux/Rocky Linux 9 ក្នុង VirtualBox។ វគ្គសិក្សា Linux ផ្នែកផ្សេងក្នុង repo អាចប្រើ Ubuntu/Debian; command ផ្នែក package manager និង installer នឹងខុសគ្នា។ មេរៀនទាំងនេះរក្សាបរិស្ថាន RHEL-like ដើម្បីឱ្យស្របតាម Lab ប្រភព។

## សុវត្ថិភាពមុនអនុវត្ត

- អនុវត្តក្នុង VM ដែលអ្នកអាចបោះចោល ឬស្ដារពី snapshot បាន។ កុំប្រើ disk របស់ Windows/host ឬ server ពិត។
- មុន command ដែលប្ដូរ disk សូមពិនិត្យ **lsblk** និងបញ្ជាក់ឈ្មោះ disk ថ្មីម្តងទៀត។
- **fdisk** កែ partition table ហើយ **mkfs** លុប filesystem/data លើ device ដែលបានជ្រើស។
- Lab RAID បង្កើត និងសាក fail លើ software RAID ក្នុង VM ប៉ុណ្ណោះ។
- កុំ commit screenshot ដែលបង្ហាញឈ្មោះអ្នកប្រើ, hostname, IP ឬទិន្នន័យផ្ទាល់ខ្លួនទៅ GitHub សាធារណៈ។
- សេចក្ដីណែនាំ submit ក្នុងឯកសារដើមជាការងារសម្រាប់ថ្នាក់រៀន។ សូមអនុវត្តតាមការណែនាំរបស់គ្រូសម្រាប់ការបញ្ជូនការងារ; វាមិនមែនជាបញ្ជាឱ្យបង្ហោះព័ត៌មានផ្ទាល់ខ្លួនជាសាធារណៈទេ។

## ផែនការរៀន

រៀន Lab ១ មុន ដើម្បីស្គាល់ OS/command និងបង្កើត VM។ Lab ២ បន្ថែម virtual disk ទីពីរ ដើម្បីរៀន partition និង mount។ Lab ៣ បង្កើត VM ថ្មីដែលមាន disk ពីរ សម្រាប់សិក្សា RAID 1។ កុំប្រើ VM Lab ១/២ ជំនួស VM ថ្មីរបស់ Lab ៣។
