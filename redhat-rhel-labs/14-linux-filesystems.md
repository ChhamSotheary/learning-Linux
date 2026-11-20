# Lab ១៤៖ ចូលប្រើ Linux File Systems (Access Linux File Systems)

## គោលបំណង
ស្គាល់ filesystem, mount point, disk usage និង block devices ដោយផ្តោតលើការពិនិត្យ មិនធ្វើ format disk ពិត។

## ១. ពិនិត្យ disk និង mount
```bash
lsblk
findmnt
df -hT
```
`lsblk` រាយ block devices, `findmnt` បង្ហាញ mount tree, `df -hT` បង្ហាញទំហំ filesystem និងប្រភេទ។

## ២. ពិនិត្យ inode usage
```bash
df -i
```
Filesystem អាចអស់ inodes ទោះបីនៅសល់ទំហំ bytes ក៏ដោយ។ Inode ផ្ទុក metadata របស់ file។

## ៣. ពិនិត្យ directory usage
```bash
du -sh "$HOME"
du -h --max-depth=1 "$HOME" 2>/dev/null
```
`du` ប៉ាន់ប្រមាណទំហំដែល files ប្រើ។ លទ្ធផលអាចខុសពី `df` ព្រោះវិធីគណនា និង mounted filesystems ខុសគ្នា។

## ៤. ស្វែងយល់ពី mount point
Linux បង្ហាញ filesystem ដែលបាន mount ជាផ្នែកមួយនៃ directory tree។ ឧទាហរណ៍ `/`, `/home`, `/boot` អាចស្ថិតលើ filesystem ផ្សេងៗគ្នា។ ប្រើ៖
```bash
findmnt /
findmnt /home
```
ទីតាំង និងលទ្ធផលអាស្រ័យលើការរៀបចំ disk របស់ VM។

## ៥. ពិនិត្យ filesystem types
```bash
lsblk -f
blkid
```
`lsblk -f` បង្ហាញ filesystem type, label និង UUID ប្រសិនបើមាន។ `blkid` បង្ហាញ metadata របស់ block devices។

## លំហាត់
1. រក root filesystem និង mount point។
2. កត់ filesystem type របស់ root។
3. ពិនិត្យទំហំដោយ `df -hT`។
4. ពិនិត្យ inode ដោយ `df -i`។
5. ពន្យល់ភាពខុសគ្នារវាង `df` និង `du`។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ `lsblk`, `findmnt`, `df`។
- [ ] ខ្ញុំយល់ពី filesystem និង mount point។
- [ ] ខ្ញុំអាចពិនិត្យទំហំ និង inode usage។

**សុវត្ថិភាពសំខាន់៖** Lab នេះមិនត្រូវការ `mkfs`, `fdisk`, `parted`, `wipefs` ឬ `dd` ទេ។ កុំ format ឬកែ partition របស់ disk ដែលមានទិន្នន័យ។ ប្រសិនបើចង់ហាត់ disk management សូមប្រើ virtual disk ថ្មីទទេ និង snapshot VM ជាមុន។
