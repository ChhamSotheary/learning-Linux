# មន្ទីរពិសោធន៍ Linux ១៤ មេរៀន (RHEL)

ឯកសារនេះរៀបចំផែនការអនុវត្ត Linux ជាភាសាខ្មែរ ដោយផ្អែកលើចំណងជើង Lab ទាំង ១៤ ដែលមានក្នុងរូបភាពសិក្សា។ វាជាសេចក្ដីណែនាំសម្រាប់ហាត់ដោយខ្លួនឯង មិនមែនជាការចម្លងសៀវភៅ Lab ផ្លូវការរបស់ Red Hat ទេ។

> **បរិស្ថានណែនាំ៖** Red Hat Enterprise Linux (RHEL) 9/10 នៅក្នុង VirtualBox VM។ ប្រើ snapshot មុន Lab ដែលប្ដូរ users, permissions, services, network ឬ storage។ កុំអនុវត្តលើម៉ាស៊ីន production។

## ផែនទី Lab ទាំង ១៤

| ល.រ | ចំណងជើងជាភាសាខ្មែរ | មេរៀន |
|---:|---|---|
| ១ | ចូលប្រើ Command Line | [បើកមេរៀន](01-access-command-line.md) |
| ២ | គ្រប់គ្រង Files និង Directories | [បើកមេរៀន](02-manage-files-directories.md) |
| ៣ | ស្វែងរកជំនួយសម្រាប់ Command Line | [បើកមេរៀន](03-command-line-help.md) |
| ៤ | កែសម្រួលអត្ថបទ និងប្រើ Pipelines | [បើកមេរៀន](04-edit-text-pipelines.md) |
| ៥ | គ្រប់គ្រង Local Users និង Groups | [បើកមេរៀន](05-local-users-groups.md) |
| ៦ | គ្រប់គ្រង File Permissions | [បើកមេរៀន](06-file-permissions.md) |
| ៧ | តាមដាន និងគ្រប់គ្រង Processes | [បើកមេរៀន](07-processes.md) |
| ៨ | គ្រប់គ្រង Services និង Daemons | [បើកមេរៀន](08-services-daemons.md) |
| ៩ | កំណត់រចនាសម្ព័ន្ធ និងការពារ SSH | [បើកមេរៀន](09-ssh-security.md) |
| ១០ | វិភាគ និងរក្សាទុក Logs | [បើកមេរៀន](10-logs.md) |
| ១១ | គ្រប់គ្រង Network Configuration | [បើកមេរៀន](11-network-configuration.md) |
| ១២ | បង្រួម និងផ្ទេរ Files | [បើកមេរៀន](12-archive-transfer.md) |
| ១៣ | គ្រប់គ្រង Software ដោយ DNF | [បើកមេរៀន](13-dnf-software.md) |
| ១៤ | ចូលប្រើ Linux File Systems | [បើកមេរៀន](14-linux-filesystems.md) |

## តំណភ្ជាប់ទៅមេរៀនក្នុង Repository

- [Terminal និង Command Line](../02-terminal-command-line/lesson.md)
- [Filesystem និងការគ្រប់គ្រងឯកសារ](../03-filesystem-file-management/lesson.md)
- [Users, Groups និង Permissions](../04-users-groups-permissions/lesson.md)
- [Package Management](../05-package-management/lesson.md)
- [Processes, Services និង Logs](../06-processes-services-logs/lesson.md)
- [Networking Fundamentals](../07-networking-fundamentals/lesson.md)

## របៀបប្រើ Lab

1. បើក RHEL VM ហើយ login ដោយ user ធម្មតា។
2. អានគោលបំណង និង command មុនពេលវាយ។
3. រត់ command មួយៗ ហើយពិនិត្យលទ្ធផល។
4. កត់ត្រា command, output និងអ្វីដែលបានរៀន។
5. បើ command មួយស្នើឱ្យប្រើ sudo ឬប្ដូរការកំណត់ប្រព័ន្ធ ត្រូវយល់ពីផលប៉ះពាល់ជាមុន។
6. បញ្ចប់ Lab មួយហើយទើបបន្ត Lab បន្ទាប់។

**ចំណាំអំពី Distribution៖** Lab នេះផ្តោតលើ RHEL និងប្រើ DNF/systemd ជាឧទាហរណ៍។ Ubuntu/Debian អាចប្រើ APT ជំនួស DNF ហើយ package names ឬលទ្ធផលខ្លះអាចខុសគ្នា។
