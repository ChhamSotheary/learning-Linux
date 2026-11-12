# មេរៀនទី ១៖ សេចក្ដីផ្ដើមអំពី Linux

## គោលបំណងមេរៀន
បន្ទាប់ពីរៀនចប់ អ្នកអាច៖
- ពន្យល់ថា Linux ជាអ្វី និងតួនាទីរបស់ Kernel។
- ស្គាល់ Kernel, Shell, Terminal និង Distribution។
- ស្គាល់ Linux Distribution ពេញនិយម។
- បើក Terminal និងប្រើ Command មូលដ្ឋានបាន។

## ១. Linux ជាអ្វី?

Linux គឺជា **Kernel (ស្នូលប្រព័ន្ធប្រតិបត្តិការ)** ដែលគ្រប់គ្រងធនធានកុំព្យូទ័រ ដូចជា CPU, RAM, Storage និងឧបករណ៍ Hardware ផ្សេងៗ។ ជាទូទៅ ពេលយើងនិយាយថា Linux OS យើងសំដៅលើ Linux Kernel រួមជាមួយកម្មវិធី និងឧបករណ៍ផ្សេងៗ ដែលបង្កើតជា **Distribution (Distro)**។

ឧទាហរណ៍៖ Ubuntu, Debian, Fedora, Linux Mint និង Arch Linux។

## ២. ប្រវត្តិសង្ខេប
- Linus Torvalds បានចាប់ផ្ដើមអភិវឌ្ឍ Linux Kernel នៅឆ្នាំ 1991។
- Linux ត្រូវបានអភិវឌ្ឍដោយសហគមន៍ និងអ្នករួមចំណែកជាច្រើន។
- Linux ត្រូវបានប្រើប្រាស់លើ Server, Cloud, Supercomputer និង Embedded Devices។

## ៣. សមាសធាតុសំខាន់ៗ

| ពាក្យ | អត្ថន័យ |
|---|---|
| Kernel | គ្រប់គ្រង Hardware និងធនធានប្រព័ន្ធ |
| Shell | បកស្រាយ និងដំណើរការ Command |
| Terminal | ផ្ទាំងសម្រាប់បញ្ចូល និងបង្ហាញ Command |
| Distribution | ប្រព័ន្ធដែលរួមមាន Kernel និងកម្មវិធីចាំបាច់ |
| File System | របៀបរៀបចំ និងរក្សាទុកឯកសារ |
| Open Source | Source Code អាចសិក្សា និងកែប្រែតាម License |

## ៤. Linux Distribution ពេញនិយម
- **Ubuntu**៖ សមស្របសម្រាប់អ្នកចាប់ផ្ដើម និង Server។
- **Debian**៖ ល្បីខាងស្ថិរភាព។
- **Fedora**៖ ផ្ដល់បច្ចេកវិទ្យាថ្មីៗ។
- **Linux Mint**៖ មាន Desktop ងាយស្រួលប្រើ។
- **Arch Linux**៖ ផ្ដល់ការគ្រប់គ្រងលម្អិត និងត្រូវការចំណេះដឹងបន្ថែម។

## ៥. បើក Terminal

- Ubuntu Desktop៖ ចុច Ctrl + Alt + T។
- Windows៖ អាចប្រើ WSL2 ដើម្បីបើក Linux Terminal។
- Virtual Machine៖ បើក Terminal នៅក្នុង Linux VM។

## ៦. Command ដំបូងៗ

### បង្ហាញ Username បច្ចុប្បន្ន
```bash
whoami
```
Command នេះបង្ហាញឈ្មោះ User ដែលកំពុង Login។

### បង្ហាញទីតាំង Folder បច្ចុប្បន្ន
```bash
pwd
```
ពាក្យពេញគឺ Present Working Directory។

### បង្ហាញព័ត៌មាន Kernel
```bash
uname -a
```
បង្ហាញព័ត៌មាន Kernel និងប្រព័ន្ធ។

### បង្ហាញព័ត៌មាន Distribution
```bash
cat /etc/os-release
```
បង្ហាញឈ្មោះ និង Version របស់ Linux Distribution។

### បង្ហាញថ្ងៃ និងម៉ោង
```bash
date
```

### បង្ហាញ Version របស់ Kernel
```bash
uname -r
```

## ៧. របៀបទទួលជំនួយពី Command

```bash
man pwd
```
បើក Manual របស់ Command `pwd`។ ចុច `q` ដើម្បីចេញ។

```bash
pwd --help
```
បង្ហាញជំនួយខ្លីៗ ប្រសិនបើ Command គាំទ្រ Option នេះ។

## ៨. របៀបអាន Command

ឧទាហរណ៍៖
```bash
uname -r
```
- `uname` គឺជា Command។
- `-r` គឺជា Option ដែលស្នើឱ្យបង្ហាញ Kernel Release។

ចំណាំ៖ អក្សរធំ និងអក្សរតូចក្នុង Linux ជាទូទៅមានភាពខុសគ្នា (case-sensitive)។ ឧទាហរណ៍ `File.txt` និង `file.txt` អាចជាឯកសារពីរផ្សេងគ្នា។

## ៩. សុវត្ថិភាពពេលអនុវត្ត
- រៀនក្នុង Ubuntu/Debian VM ឬ WSL2។
- ប្រើគណនីធម្មតាសម្រាប់ការងារប្រចាំថ្ងៃ។
- កុំប្រើ `sudo` ប្រសិនបើមិនយល់ពី Command។
- មុនកែប្រែ ឬលុបឯកសារសំខាន់ ត្រូវមាន Backup។
- អនុវត្តតែលើប្រព័ន្ធដែលអ្នកមានសិទ្ធិប្រើប្រាស់។

## ១០. កិច្ចការអនុវត្ត
1. បើក Terminal។
2. រត់ `whoami` ហើយកត់ត្រា Username។
3. រត់ `pwd` ហើយពន្យល់ទីតាំងដែលបានបង្ហាញ។
4. រត់ `uname -r` ហើយកត់ត្រា Kernel Version។
5. រត់ `cat /etc/os-release` ដើម្បីស្គាល់ Distribution។
6. បើក `man date` ហើយសាកចេញដោយចុច `q`។
7. ពន្យល់ភាពខុសគ្នារវាង Kernel និង Shell ជាពាក្យផ្ទាល់ខ្លួន។

## ១១. សង្ខេប
Linux Kernel គ្រប់គ្រងធនធានប្រព័ន្ធ។ Shell ទទួល និងបកស្រាយ Command។ Terminal ជាផ្ទាំងសម្រាប់ទាក់ទងជាមួយ Shell។ Distribution គឺជាប្រព័ន្ធ Linux ដែលរួមបញ្ចូល Kernel និងកម្មវិធីចាំបាច់។

## ពាក្យគន្លឹះ
Linux Kernel, Shell, Terminal, Distribution, Open Source, Command Line, Operating System។
