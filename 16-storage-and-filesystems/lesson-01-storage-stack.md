# មេរៀនទី ១៖ ពី Block Device ទៅ Mount Point

ទិន្នន័យផ្លូវ storage អាចមាន disk/device → partition → encryption/LVM/RAID layer → filesystem → mount point → file។ មិនមែនគ្រប់ម៉ាស៊ីនប្រើ layer ទាំងអស់នេះទេ។ កំហុសមួយកម្រិតអាចបង្ហាញជាបញ្ហានៅកម្រិតខ្ពស់ជាង។

~~~bash
lsblk -f
findmnt
df -hT
df -i
~~~

df -h បង្ហាញ block capacity; df -i បង្ហាញ inode usage។ Disk អាចមាន space នៅសល់ តែ inode អស់ ឬមាន file លុបហើយនៅតែបើកដោយ process។

កុំរត់ mkfs, fsck លើ mounted filesystem, ឬប្ដូរ partition លើ disk ដែលមានទិន្នន័យ។ សាកល្បងតែ disk image/VM ដែលអាចបោះចោលបាន។

## លំហាត់

ជ្រើស mount point មួយ ហើយប្រើ lsblk/findmnt ដើម្បីតាមពី source device ទៅ filesystem type។ ប្រៀបធៀប blocks និង inode usage។
