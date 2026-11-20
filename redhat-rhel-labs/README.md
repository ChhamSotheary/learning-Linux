# មន្ទីរពិសោធន៍ Linux ១៤ មេរៀន (RHEL)

ឯកសារនេះរៀបចំផែនការអនុវត្ត Linux ជាភាសាខ្មែរ ដោយផ្អែកលើចំណងជើង Lab ទាំង ១៤ ដែលមានក្នុងរូបភាពសិក្សា។ វាជាសេចក្ដីណែនាំសម្រាប់ហាត់ដោយខ្លួនឯង មិនមែនជាការចម្លងសៀវភៅ Lab ផ្លូវការរបស់ Red Hat ទេ។

> **បរិស្ថានណែនាំ៖** Red Hat Enterprise Linux (RHEL) 9/10 នៅក្នុង VirtualBox VM។ ប្រើ snapshot មុន Lab ដែលប្ដូរ users, permissions, services, network ឬ storage។ កុំអនុវត្តលើម៉ាស៊ីន production។

## ផែនទី Lab ទាំង ១៤

| ល.រ | ចំណងជើងជាភាសាខ្មែរ | ចំណុចសំខាន់ |
|---:|---|---|
| ១ | [ចូលប្រើ Command Line](01-access-command-line.md) | ចូល Terminal, ស្គាល់ shell និងរត់ command ដំបូង |
| ២ | គ្រប់គ្រង Files និង Directories | បង្កើត មើល ចម្លង ផ្លាស់ទី និងស្វែងរកឯកសារ |
| ៣ | ស្វែងរកជំនួយសម្រាប់ Command Line | ប្រើ man, --help, info និង help |
| ៤ | កែសម្រួលអត្ថបទ និងប្រើ Pipelines | ប្រើ editor, grep, sort, wc និង pipe |
| ៥ | គ្រប់គ្រង Local Users និង Groups | ពិនិត្យ និងគ្រប់គ្រង accounts/groups |
| ៦ | គ្រប់គ្រង File Permissions | អាន/កែ mode, owner និង group |
| ៧ | តាមដាន និងគ្រប់គ្រង Processes | សង្កេត និងគ្រប់គ្រង process |
| ៨ | គ្រប់គ្រង Services និង Daemons | ពិនិត្យ service ជាមួយ systemctl |
| ៩ | កំណត់រចនាសម្ព័ន្ធ និងការពារ SSH | SSH connection, keys និងការកំណត់សុវត្ថិភាព |
| ១០ | វិភាគ និងរក្សាទុក Logs | អាន system logs និង journal |
| ១១ | គ្រប់គ្រង Network Configuration | ពិនិត្យ IP, routes និង DNS |
| ១២ | បង្រួម និងផ្ទេរ Files | ប្រើ tar, gzip និងការផ្ទេរឯកសារ |
| ១៣ | គ្រប់គ្រង Software ដោយ DNF | ស្វែងរក ដំឡើង និងធ្វើបច្ចុប្បន្នភាព packages |
| ១៤ | ចូលប្រើ Linux File Systems | ស្គាល់ filesystem, mount និង disk usage |

## តំណភ្ជាប់ទៅមេរៀនក្នុង Repository

មេរៀនខាងក្រោមមានខ្លឹមសារពាក់ព័ន្ធរួចហើយនៅក្នុងវគ្គសិក្សានេះ៖

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
