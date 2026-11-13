# មេរៀនទី ៩៖ Disk, Filesystem និង Backup

## គោលបំណង

- មើល disks, partitions, mounts និងទំហំ storage។
- យល់ពី filesystem និង mount point។
- បង្កើត archive backup សម្រាប់ directory សាកល្បង។
- ផ្ទៀងផ្ទាត់ archive និងស្ដារទៅ directory ថ្មី។
- ស្គាល់ហានិភ័យនៃ partition/format commands។

## ១. Disk និង Partition

Disk ជាឧបករណ៍ផ្ទុកទិន្នន័យ។ Partition បែងចែក disk ទៅតំបន់ logical។ Filesystem រៀបចំឯកសារក្នុង partition ឬ volume។ Mount point ជា directory ដែល filesystem ត្រូវបានភ្ជាប់ទៅក្នុង Linux tree។

មើល block devices ដោយ៖

~~~bash
lsblk
lsblk -f
~~~

កុំសន្មតថាឈ្មោះ /dev/sda ឬ /dev/nvme0n1 ជា disk ដដែលនៅគ្រប់ម៉ាស៊ីន។ ឈ្មោះឧបករណ៍អាចផ្លាស់ប្ដូរតាម hardware និង boot order។

## ២. ទំហំ Filesystem និង Directory

~~~bash
df -h
du -sh "$HOME"
du -h --max-depth=1 "$HOME"
~~~

- df បង្ហាញទំហំ filesystem ដែល mount។
- du ប៉ាន់ស្មានទំហំដែល files/directories ប្រើ។
- -h បង្ហាញទំហំអានងាយ។
- --max-depth គាំទ្រដោយ GNU du; options អាចខុសគ្នាតាម implementation។

ពេល disk ពេញ សូមពិនិត្យ log/cache និងទីតាំងធំៗ។ កុំលុប file ប្រព័ន្ធដោយមិនដឹងថាវាត្រូវការដោយ service ឬអត់។

## ៣. Mount និង /etc/fstab

~~~bash
findmnt
mount
~~~

findmnt បង្ហាញ mount tree។ mount ដោយគ្មាន arguments ជាទូទៅបង្ហាញ mounted filesystems។ /etc/fstab ជា configuration សម្រាប់ filesystems ដែលគួរ mount តាម policy/boot configuration។ កុំកែ /etc/fstab ដោយមិនមាន backup និងយល់ពី UUID, filesystem type និង mount options; កំហុសអាចបណ្ដាលឱ្យ boot ឬ mount បរាជ័យ។

## ៤. Backup ជាមួយ tar

បង្កើត data សាកល្បង៖

~~~bash
mkdir -p "$HOME/linux-practice/lesson-09/source"
printf '%s\n' "Backup practice" > "$HOME/linux-practice/lesson-09/source/note.txt"
~~~

បង្កើត gzip-compressed archive ក្នុងថត backup៖

~~~bash
mkdir -p "$HOME/linux-practice/lesson-09/backups"
tar -czf "$HOME/linux-practice/lesson-09/backups/practice.tar.gz" -C "$HOME/linux-practice/lesson-09/source" .
~~~

- c បង្កើត archive។
- z ប្រើ gzip compression។
- f បញ្ជាក់ archive filename។
- -C ប្ដូរទីតាំងមុនចាប់ផ្ដើមបន្ថែម files។

## ៥. ផ្ទៀងផ្ទាត់ និង Restore

មើលមាតិកា archive ដោយមិនស្រង់ចេញ៖

~~~bash
tar -tzf "$HOME/linux-practice/lesson-09/backups/practice.tar.gz"
~~~

ស្រង់ទៅ directory ថ្មីដែលទទេ៖

~~~bash
mkdir -p "$HOME/linux-practice/lesson-09/restored"
tar -xzf "$HOME/linux-practice/lesson-09/backups/practice.tar.gz" -C "$HOME/linux-practice/lesson-09/restored"
~~~

មុន extract archive ដែលមិនទុកចិត្ត សូមពិនិត្យ filenames ដោយ tar -tzf ហើយប្រយ័ត្ន path traversal និង files ដែលអាច overwrite ទិន្នន័យ។ ក្នុងលំហាត់នេះ archive គឺបង្កើតដោយខ្លួនឯង និង restore ទៅថតថ្មី។

Backup មួយមិនទាន់ជាផែនការ backup ពេញលេញទេ។ ត្រូវគិតពីការរក្សាទុកទីតាំងដាច់ដោយឡែក, encryption ប្រសិនបើមាន sensitive data, retention និងការសាក restore ជាប្រចាំ។

## ៦. កុំរត់ Disk Commands ដោយមិនយល់

Commands ដូចជា mkfs, fdisk, parted, wipefs និង dd អាចលុប ឬសរសេរជំនួសទិន្នន័យលើឧបករណ៍។ កុំរត់វាលើ disk ពិតសម្រាប់មេរៀននេះ។ ប្រសិនបើត្រូវរៀន partitioning សូមប្រើ disposable VM disk ដាច់ដោយឡែក និងមាន backup ដែលបានផ្ទៀងផ្ទាត់។

## ៧. កិច្ចការអនុវត្ត

1. ប្រើ lsblk -f ដើម្បីមើល devices និង filesystem types។
2. ប្រើ df -h ដើម្បីពិនិត្យទំហំទំនេរ។
3. ប្រើ du -sh "$HOME" ដើម្បីមើលទំហំ home directory។
4. បង្កើត directory source មាន files សាកល្បង។
5. បង្កើត tar.gz archive ទៅ backups directory។
6. មើល contents ដោយ tar -tzf។
7. Restore ទៅ directory ថ្មី ហើយអាន restored note។
8. ពន្យល់ហេតុអ្វី backup ត្រូវសាក restore មុនចាត់ទុកថាអាចប្រើបាន។

## សង្ខេប

lsblk មើល block devices; df និង du ពិនិត្យ storage usage; findmnt មើល mounts។ tar អាចបង្កើត, list និង restore archives។ ផ្ទៀងផ្ទាត់ backup និងសាក restore។ Disk formatting/partitioning commands អាចបំផ្លាញទិន្នន័យ ត្រូវធ្វើតែក្នុង disposable environment។

## ឯកសារយោង

- [lsblk manual](https://man7.org/linux/man-pages/man8/lsblk.8.html)
- [findmnt manual](https://man7.org/linux/man-pages/man8/findmnt.8.html)
- [GNU tar manual](https://www.gnu.org/software/tar/manual/)
