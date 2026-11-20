# Lab ១៖ ចូលប្រើ Command Line (Access the Command Line)

## គោលបំណង

បន្ទាប់ពីបញ្ចប់ Lab នេះ អ្នកអាច៖

- បើក Terminal និងស្គាល់ Command Line Interface (CLI)។
- ស្គាល់ថា Terminal និង Shell មានតួនាទីខុសគ្នា។
- រត់ command មូលដ្ឋាន និងអាន output។
- ពិនិត្យ user និងទីតាំងបច្ចុប្បន្ន។

## ១. តើ Command Line ជាអ្វី?

**Command Line** គឺជាវិធីបញ្ជាប្រព័ន្ធដោយវាយអត្ថបទជាពាក្យបញ្ជា ជំនួសឱ្យការចុចលើប៊ូតុងតាម Graphical User Interface (GUI)។

- **Terminal**៖ កម្មវិធីដែលបង្ហាញផ្ទាំងសម្រាប់វាយ និងមើលអត្ថបទ។
- **Shell**៖ កម្មវិធីដែលអាន និងបកស្រាយ command ដូចជា Bash។
- **Command**៖ ពាក្យបញ្ជាដែលស្នើឱ្យប្រព័ន្ធធ្វើការងារ។

## ២. បើក Terminal

នៅក្នុង RHEL Desktop៖

1. Login ទៅកាន់ Desktop។
2. បើក Activities ឬ Applications។
3. ស្វែងរកពាក្យ Terminal ហើយបើកវា។
4. អ្នកអាចសាក shortcut `Ctrl + Alt + T` ប្រសិនបើ Desktop Environment គាំទ្រ។

បើអ្នកប្រើ RHEL Server ដែលគ្មាន GUI អ្នកអាចចូលតាម console/VM terminal ឬ SSH ដែលបានកំណត់រួច។

Prompt អាចមានទម្រង់ប្រហាក់ប្រហែល៖

```text
student@rhel:~$
```

Prompt មិនដូចគ្នាទាំងអស់ទេ។ សញ្ញា `$` ជាទូទៅបង្ហាញថាកំពុងប្រើ user ធម្មតា។ កុំវាយ prompt ជាផ្នែកនៃ command។

## ៣. សាកល្បង Command ដំបូង

វាយ command ទាំងនេះម្តងមួយៗ៖

```bash
whoami
```

បង្ហាញឈ្មោះ user ដែលកំពុង login។

```bash
pwd
```

បង្ហាញទីតាំង directory បច្ចុប្បន្ន (Print Working Directory)។

```bash
hostname
```

បង្ហាញឈ្មោះម៉ាស៊ីន។

```bash
date
```

បង្ហាញកាលបរិច្ឆេទ និងម៉ោងរបស់ប្រព័ន្ធ។

```bash
echo "Hello Linux"
```

បង្ហាញអត្ថបទ Hello Linux នៅលើ Terminal។

លទ្ធផលពិតប្រាកដរបស់ `whoami`, `pwd`, `hostname` និង `date` អាស្រ័យលើការកំណត់ VM របស់អ្នក។

## ៤. ស្គាល់ Shell

រត់៖

```bash
echo "$SHELL"
ps -p "$$" -o comm=
```

- `echo "$SHELL"` បង្ហាញ shell ដែលបានកំណត់ក្នុង environment។
- `ps -p "$$" -o comm=` បង្ហាញឈ្មោះ process របស់ shell ដែលកំពុងដំណើរការ។

នៅក្នុង RHEL ជាទូទៅអ្នកនឹងជួប Bash ប៉ុន្តែអាចមាន shell ផ្សេងទៀត។

## ៥. រចនាសម្ព័ន្ធ Command

ទម្រង់ទូទៅ៖

```text
command [option] [argument]
```

ឧទាហរណ៍៖

```bash
ls -l /etc
```

- `ls` ជា command សម្រាប់រាយឈ្មោះឯកសារ។
- `-l` ជា option សម្រាប់បង្ហាញព័ត៌មានលម្អិត។
- `/etc` ជា argument ដែលបញ្ជាក់ទីតាំង។

## ៦. លំហាត់អនុវត្ត

រត់ command ខាងក្រោម ហើយកត់ចម្លើយ៖

```bash
whoami
pwd
hostname
date
echo "I am learning Linux"
```

សំណួរអនុវត្ត៖

1. តើ command មួយណាបង្ហាញឈ្មោះ user?
2. តើ command មួយណាបង្ហាញទីតាំងបច្ចុប្បន្ន?
3. តើ Shell មានតួនាទីអ្វី?
4. តើ Terminal និង Shell ខុសគ្នាយ៉ាងដូចម្តេច?

## ៧. ការត្រួតពិនិត្យ

- [ ] ខ្ញុំអាចបើក Terminal បាន។
- [ ] ខ្ញុំអាចរត់ command ដោយមិនវាយ prompt។
- [ ] ខ្ញុំយល់ពីលទ្ធផលរបស់ `whoami` និង `pwd`។
- [ ] ខ្ញុំអាចពន្យល់ពី Terminal, Shell និង Command។

## សុវត្ថិភាព

Lab នេះប្រើតែ command សម្រាប់អានព័ត៌មាន មិនត្រូវការសិទ្ធិ root ឬ `sudo` ទេ។ កុំប្រើ command ដែលអ្នកមិនយល់ ជាពិសេស command ដែលលុបឯកសារ ឬកែ system configuration។

## សង្ខេប

Command Line អនុញ្ញាតឱ្យអ្នកគ្រប់គ្រង Linux តាមរយៈ command។ Terminal ជាផ្ទាំងទទួល/បង្ហាញអត្ថបទ ខណៈ Shell ជាអ្នកបកស្រាយ command។ `whoami`, `pwd`, `hostname`, `date` និង `echo` ជា command ដំបូងដែលគួរចេះ។

**Lab បន្ទាប់៖** [Lab ២ — គ្រប់គ្រង Files និង Directories](README.md)។
