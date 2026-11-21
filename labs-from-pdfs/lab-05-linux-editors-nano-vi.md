# Lab ៥៖ ប្រើកម្មវិធីកែអត្ថបទ Linux (nano និង vi/vim)

នៅលើ Linux server ជាច្រើន អ្នកអាចមានតែ terminal ប៉ុណ្ណោះ។ Lab នេះបង្រៀនឱ្យកែ text files ដោយប្រើ `nano` និង `vi`/`vim`, រៀបចំ editor settings និងកែ file ប្រព័ន្ធដោយមាន backup និងផ្ទៀងផ្ទាត់លទ្ធផល។ ពេលវេលាប្រហែល ១២០ នាទី។

## ១. គោលបំណង

ក្រោយអនុវត្ត អ្នកអាច៖

- បង្កើត កែ រក្សាទុក និងបិទ file ក្នុង `nano`។
- ពន្យល់ Normal, Insert និង Command mode របស់ `vi`/`vim`។
- ប្រើពាក្យបញ្ជាសំខាន់ៗដើម្បីរក្សាទុក, ចេញ, ស្វែងរក, ជំនួស, លុប និង undo។
- រៀបចំ `~/.vimrc`, `~/.nanorc` និង variable `EDITOR`។
- ដំឡើង `vim-enhanced` ពី DVD repository offline ក្នុង RHEL VM។
- កែ `/etc/hosts` ដោយបង្កើត backup, បញ្ចូលទិន្នន័យត្រឹមត្រូវ និងផ្ទៀងផ្ទាត់ដោយ `getent`/`diff`។
- ពន្យល់មូលហេតុដែល `sudo echo ... >> file` មិនអាចលើសសិទ្ធិរបស់ shell បាន។

## ២. បរិស្ថាន និងការរៀបចំ

ត្រូវមាន៖

- RHEL 9.6 VM `rhel9-lab1` ពី Lab មុន។
- User ធម្មតា `student01` ដែលមានសិទ្ធិ sudo តាមការអនុញ្ញាត។
- RHEL 9.6 DVD ISO ភ្ជាប់ទៅ VM សម្រាប់ផ្នែកដំឡើង Vim។
- ពេលវេលាប្រហែល ២ ម៉ោង។

បង្កើត snapshot ឈ្មោះ `lab5-start` និងថតសម្រាប់ file ហាត់៖

~~~bash
mkdir -p ~/lab5
cd ~/lab5
pwd
~~~

សម្រាប់ការដំឡើង package offline ត្រូវមាន `/etc/yum.repos.d/dvd.repo` ដែលបានរៀបចំក្នុង Lab ១ និង DVD ISO ត្រឹមត្រូវ។ បើមិនមាន សូមកុំបិទ/ប្តូរ repository settings ដោយស្មាន; ត្រឡប់ទៅ Lab ១ ឬសួរគ្រូ។

**ផ្នែក D និង E ប៉ះ `/etc/hosts` ដែលជា configuration file របស់ប្រព័ន្ធ។** អនុវត្តតែក្នុង VM សាកល្បងដែលអ្នកគ្រប់គ្រង។ កុំកែ host ឬ server ពិត។ ប្រើតែ IP/hostname ដែលគ្រូបានផ្តល់ ហើយស្តារ backup នៅចុងលំហាត់។

## ៣. ផ្នែក A៖ កែ file ដោយ nano

### ជំហាន A1៖ បង្កើត និងសរសេរ file

~~~bash
cd ~/lab5
nano hello.txt
~~~

ក្នុង nano៖

1. វាយពីរបន្ទាត់ ឧទាហរណ៍ `Hello from Linux` និង `Week 5`។
2. ចុច **Ctrl+O** (Write Out) ដើម្បីរក្សាទុក។
3. ពេល nano សួរឈ្មោះ file ចុច **Enter** ដើម្បីទទួល `hello.txt`។
4. ចុច **Ctrl+X** ដើម្បីចេញ។

ត្រឡប់មក terminal រួចពិនិត្យ៖

~~~bash
cat -n hello.txt
~~~

`cat -n` បង្ហាញមាតិកាជាមួយលេខបន្ទាត់។ លទ្ធផលគួរតែបង្ហាញបន្ទាត់ទាំងពីរ និងលេខ 1, 2។

### ជំហាន A2៖ បង្ហាញលេខបន្ទាត់ពេលកែ

~~~bash
nano -l hello.txt
~~~

Option `-l` បង្ហាញលេខបន្ទាត់នៅខាងឆ្វេង។ ក្នុង nano អ្នកអាច៖

- ចុច **Ctrl+K** ដើម្បីកាត់បន្ទាត់បច្ចុប្បន្ន។
- ចុច **Ctrl+U** ដើម្បីបិទភ្ជាប់បន្ទាត់ដែលបានកាត់។
- ចុច **Ctrl+W** ដើម្បីស្វែងរកអត្ថបទ។
- ចុច **Ctrl+O**, Enter ដើម្បីរក្សាទុក។
- ចុច **Ctrl+X** ដើម្បីចេញ។

នៅខាងក្រោម nano សញ្ញា `^` មានន័យថាចុច Ctrl ជាមួយអក្សរបន្ទាប់។ ឧទាហរណ៍ `^O` មានន័យថា Ctrl+O។ សាកល្បងកែបន្ទាត់ ហើយផ្ទៀងផ្ទាត់ម្ដងទៀតដោយ `cat -n hello.txt`។

## ៤. ផ្នែក B៖ ប្រើ vi (ឬ Vim)

### ៤.១ ស្គាល់ modes

`vi`/`vim` ជា modal editor មាន mode ផ្សេងៗ។ Mode ជាអ្វីដែលកំណត់ថាប៊ូតុងដែលអ្នកចុចមានន័យជាអក្សរ ឬពាក្យបញ្ជា។

- **Normal mode**៖ mode ចាប់ផ្តើម; គ្រាប់ចុចធ្វើជាពាក្យបញ្ជា (ឧ. `dd`, `x`, `u`)។
- **Insert mode**៖ វាយអក្សរទៅក្នុង file; ចុច `i` ឬ `o` ដើម្បីចូល។
- **Command-line mode**៖ ចុច `:` ក្នុង Normal mode រួចវាយពាក្យបញ្ជា ដូចជា `:wq`។
- **Esc**៖ ចេញពី Insert mode ទៅ Normal mode។ បើមិនច្បាស់ថាកំពុង mode ណា ចុច Esc មួយ ឬពីរដង។

### ជំហាន B1៖ សរសេរបន្ទាត់ដំបូង រួចរក្សាទុក

~~~bash
cd ~/lab5
vi school.txt
~~~

ក្នុង editor៖

1. ចុច `i` ដើម្បីចូល Insert mode។
2. វាយ `Norton University`។
3. ចុច Esc ដើម្បីត្រឡប់ Normal mode។
4. វាយ `:wq` រួចចុច Enter។ `w` សរសេរ file; `q` ចេញ។

ពិនិត្យពី terminal៖

~~~bash
cat school.txt
~~~

### ជំហាន B2៖ បន្ថែមបន្ទាត់ដោយ `o`

~~~bash
vi school.txt
~~~

1. ក្នុង Normal mode ចុច `o` ដើម្បីបើកបន្ទាត់ថ្មីខាងក្រោម ហើយចូល Insert mode។
2. វាយ `Phnom Penh`។
3. ចុច Esc រួចរក្សាទុក/ចេញដោយ `:wq` និង Enter។

### ជំហាន B3៖ ស្វែងរក និងប្តូរពាក្យទាំងអស់

បើក file ហើយរត់ command ពី Normal mode៖

~~~vim
:%s/Norton/NORTON/g
~~~

- `:` ចូល command-line mode។
- `%` មានន័យថាគ្រប់បន្ទាត់។
- `s` ជា substitute។
- `Norton` ជាអត្ថបទដែលត្រូវរក; `NORTON` ជាអត្ថបទថ្មី។
- `g` ប្តូររាល់ការផ្គូផ្គងក្នុងបន្ទាត់នីមួយៗ មិនមែនតែមួយលើមួយបន្ទាត់ទេ។

ចុច Enter ដើម្បីអនុវត្ត។ ការរក case-sensitive ដូច្នេះ `norton` អក្សរតូចនឹងមិនត្រូវនឹង `Norton` ទេ។

### ជំហាន B4៖ បើកលេខបន្ទាត់ និងស្វែងរក

ក្នុង Normal mode៖

~~~vim
:set number
/Phnom
~~~

- `:set number` បង្ហាញលេខបន្ទាត់។
- `/Phnom` ចាប់ផ្តើមស្វែងរកទៅមុខ; ចុច Enter ដើម្បីបញ្ជាក់។ ចុច `n` ដើម្បីទៅលទ្ធផលបន្ទាប់ ប្រសិនបើមាន។

### ជំហាន B5៖ លុបបន្ទាត់ និង undo

ក្នុង Normal mode ទៅកាន់បន្ទាត់ `Phnom Penh`, រួច៖

~~~vim
dd
u
~~~

- `dd` លុបបន្ទាត់បច្ចុប្បន្ន។
- `u` undo ការកែចុងក្រោយ។
- អ្នកអាចសង្កេតថាបន្ទាត់ត្រឡប់មកវិញ។

បន្ទាប់មករក្សាទុក និងចេញ៖

~~~vim
:wq
~~~

ពិនិត្យលទ្ធផល៖

~~~bash
cat school.txt
~~~

ឯកសារគួរមាន `NORTON University` និង `Phnom Penh`។

### ជំហាន B6៖ ចេញដោយមិនរក្សាទុក

បើក file ម្ដងទៀត៖

~~~bash
vi school.txt
~~~

ក្នុង Normal mode ចុច `x` មួយចំនួន ដើម្បីលុបតួអក្សរនៅក្រោម cursor ក្នុង buffer បណ្ដោះអាសន្ន។ បន្ទាប់មកចេញដោយមិនរក្សាទុក៖

~~~vim
:q!
~~~

`q!` បោះចោលការកែដែលមិនបានរក្សាទុក។ ផ្ទៀងផ្ទាត់ថា file នៅដដែល៖

~~~bash
cat school.txt
~~~

**គន្លឹះសង្គ្រោះ៖** បើចៃដន្យចូល Insert mode ហើយមិនដឹងចេញយ៉ាងណា ចុច Esc; បន្ទាប់មកប្រើ `:q!` ដើម្បីចេញដោយបោះចោលការកែ ឬ `:wq` ដើម្បីរក្សាទុក។

## ៥. ផ្នែក C៖ ដំឡើង និងកំណត់ Vim/Nano

### ជំហាន C1៖ ពិនិត្យ editor និង DVD

ពិនិត្យថា `vi` មានហើយ និងរក optical device៖

~~~bash
vi --version | head -n 1
lsblk -f
~~~

នៅក្នុង `lsblk -f` រក device ប្រភេទ CD/DVD ដែលមាន RHEL ISO។ ឈ្មោះ `/dev/sr0` គ្រាន់តែឧទាហរណ៍; ប្រព័ន្ធអ្នកអាចបង្ហាញឈ្មោះផ្សេង។

បើមិនទាន់បាន mount ISO សូមធ្វើតែក្នុង VM ហើយប្រើឈ្មោះ device ដែលបានផ្ទៀងផ្ទាត់៖

~~~bash
sudo mkdir -p /mnt/dvd
sudo mount -o ro /dev/sr0 /mnt/dvd
findmnt /mnt/dvd
ls /mnt/dvd
~~~

`-o ro` mount ជា read-only។ បើ device របស់អ្នកមិនមែន `/dev/sr0` កុំចម្លង command នោះដោយផ្ទាល់; ជំនួសវាដោយឈ្មោះពិតពី `lsblk -f`។ `/mnt/dvd` គួរមាន folders ដូចជា `BaseOS` និង `AppStream`។

### ជំហាន C2៖ ដំឡើង vim-enhanced ពី repository offline

បញ្ជាក់ថា DVD repository ដែលបានកំណត់ក្នុង Lab ១ បង្ហាញក្នុងបញ្ជី៖

~~~bash
sudo dnf repolist
~~~

បន្ទាប់មកដំឡើង package និងផ្ទៀងផ្ទាត់៖

~~~bash
sudo dnf install vim-enhanced
rpm -q vim-enhanced
~~~

- `dnf install` បន្ថែម package និង dependencies តាម repository ដែលបើក។
- `rpm -q` បង្ហាញ package name/version បើបានដំឡើង។
- បើ DNF មិនរក package បាន សូមពិនិត្យថា ISO ត្រូវបានភ្ជាប់, mounted និង `dvd.repo` មាន base URL ត្រឹមត្រូវ។ កុំបិទ security checks ឬប្រើ repository មិនស្គាល់។

អាចដក DVD mount ចេញក្រោយដំឡើងរួច៖

~~~bash
sudo umount /mnt/dvd
~~~

ធ្វើតែបើមិនមាន process កំពុងប្រើ DVD repository។

### ជំហាន C3៖ បង្កើត `~/.vimrc`

~~~bash
vim ~/.vimrc
~~~

ចូល Insert mode ហើយបញ្ចូល៖

~~~vim
set number
set tabstop=4
set shiftwidth=4
set expandtab
syntax on
set hlsearch
~~~

រក្សាទុកដោយ Esc បន្ទាប់មក `:wq` និង Enter។

- `set number` បង្ហាញលេខបន្ទាត់។
- `set tabstop=4` បង្ហាញ tab ទំហំស្មើ 4 columns។
- `set shiftwidth=4` កំណត់ទំហំ indent ពេលប្រើ `>`/`<`។
- `set expandtab` បម្លែង Tab ដែលវាយទៅជា spaces ក្នុង Vim។
- `syntax on` បើក syntax highlighting សម្រាប់ file type ដែលស្គាល់។
- `set hlsearch` បន្លិចលទ្ធផលស្វែងរក។

សាកល្បងថាការកំណត់បានអាន៖

~~~bash
vim school.txt
~~~

អ្នកគួរឃើញលេខបន្ទាត់។ ចេញដោយ `:q` បើមិនបានកែ file។

### ជំហាន C4៖ បង្កើត `~/.nanorc`

~~~bash
nano ~/.nanorc
~~~

បញ្ចូល៖

~~~text
set linenumbers
set tabsize 4
set autoindent
~~~

រក្សាទុកដោយ Ctrl+O, Enter ហើយចេញដោយ Ctrl+X។ ការកំណត់នេះបង្ហាញលេខបន្ទាត់, កំណត់ទំហំ tab និងបន្ត indentation ដោយស្វ័យប្រវត្តិ។

### ជំហាន C5៖ កំណត់ editor លំនាំដើមសម្រាប់ session

កំណត់សម្រាប់ terminal បច្ចុប្បន្ន ហើយពិនិត្យ៖

~~~bash
export EDITOR=vim
echo "$EDITOR"
~~~

ដើម្បីរក្សាទុកសម្រាប់ bash sessions ថ្មីៗ អាចបន្ថែមទៅ `~/.bashrc` បន្ទាប់ពីពិនិត្យថាមិនមានរួច៖

~~~bash
grep -n 'EDITOR=vim' ~/.bashrc
printf '%s\n' 'export EDITOR=vim' >> ~/.bashrc
source ~/.bashrc
echo "$EDITOR"
~~~

បើបន្ទាត់មានស្រាប់ សូមកុំបន្ថែមស្ទួន។ `EDITOR` ជា environment variable ដែលកម្មវិធីខ្លះប្រើសម្រេចថាបើក text editor មួយណា; វាមិនប្ដូរ editor សម្រាប់ user ផ្សេងទេ។

## ៦. ផ្នែក D៖ កែ `/etc/hosts` ដោយសុវត្ថិភាព

`/etc/hosts` ជា file ដែលផ្គូផ្គង IP address ទៅ hostname មុនពេលសួរ DNS តាមលំដាប់ resolution របស់ប្រព័ន្ធ។ វាជា file របស់ root; ដូច្នេះត្រូវមានសិទ្ធិ admin ដើម្បីកែ។

### ជំហាន D1៖ ពិនិត្យ និងបម្រុងទុក

~~~bash
sudo grep -n 'rhel9-srv' /etc/hosts
sudo cp -p /etc/hosts /etc/hosts.bak
~~~

បន្ទាត់ដំបូងពិនិត្យថាឈ្មោះមានរួចឬអត់។ `grep` មិនរកឃើញក៏អាចបញ្ចេញ exit status nonzero ដែលជារឿងធម្មតា។ បន្ទាត់ទីពីរបង្កើត backup មុនកែ។

### ជំហាន D2៖ បន្ថែម hostname ដែលគ្រូបានផ្តល់

បើឈ្មោះមិនមានរួច សូមបើក file ដោយ root៖

~~~bash
sudo vim /etc/hosts
~~~

ក្នុង Vim៖ ចុច Esc, `G` ដើម្បីទៅចុង file, `o` ដើម្បីបង្កើតបន្ទាត់ថ្មី និងចូល Insert mode។ បញ្ចូលទម្រង់៖

~~~text
<IP ដែលគ្រូផ្ដល់> rhel9-srv
~~~

អាសយដ្ឋាន `192.168.56.10` ក្នុង PDF គ្រាន់តែជាឧទាហរណ៍; កុំប្រើវា ប្រសិនបើគ្រូបានផ្ដល់ IP ផ្សេង ឬបណ្ដាញ VM របស់អ្នកមិនប្រើវា។ ត្រូវមាន space/tab រវាង IP និង hostname។ ចុច Esc រួច `:wq` និង Enter ដើម្បីរក្សាទុក។

### ជំហាន D3៖ ផ្ទៀងផ្ទាត់ និងមើលភាពខុសគ្នា

~~~bash
getent hosts rhel9-srv
diff -u /etc/hosts.bak /etc/hosts
~~~

- `getent hosts` សួរប្រព័ន្ធ name-service configuration ដើម្បីរក hostname; រំពឹងឃើញ IP ដែលអ្នកបានកំណត់ និងឈ្មោះ `rhel9-srv`។
- `diff -u` ប្រៀបធៀប backup ជាមួយ file ថ្មី។ បន្ទាត់បន្ថែមនឹងមានសញ្ញា `+`។
- លេខក្នុង output ដូច `2a3` អាចខុសតាមចំនួនបន្ទាត់ដែល file ដើមមាន។ នេះជាលេខបង្ហាញទីតាំងភាពខុសគ្នា មិនមែនជាកំហុសទេ។

បើឈ្មោះមិន resolve ឬអ្នកសរសេរខុស សូមបើក file កែវា ហើយរត់ `getent` និង `diff` ម្ដងទៀត។ នៅចុងលំហាត់ អ្នកអាចស្តារ file ដើមដោយ៖

~~~bash
sudo cp -p /etc/hosts.bak /etc/hosts
getent hosts rhel9-srv
diff -u /etc/hosts.bak /etc/hosts
~~~

បន្ទាប់ពីស្តារ `getent` អាចមិនបង្ហាញ hostname នោះទៀត។ `diff` គួរមិនបង្ហាញភាពខុសគ្នា។

## ៧. ផ្នែក E៖ កែអត្ថបទដោយ command line និងយល់ពី redirection

ធ្វើលំហាត់នេះក្រោយបាន backup `/etc/hosts` ក្នុងផ្នែក D។ ប្រើតែ VM និងអាសយដ្ឋានដែលគ្រូផ្តល់។

### ជំហាន E1៖ បន្ថែមបន្ទាត់ដោយ `tee`

~~~bash
echo "10.0.0.5 web1" | sudo tee -a /etc/hosts
~~~

`tee -a` ទទួលអត្ថបទពី pipe ហើយបន្ថែមទៅ file ជាមួយសិទ្ធិ root។ IP `10.0.0.5` ក្នុងឧទាហរណ៍គឺ placeholder ប៉ុណ្ណោះ; ជំនួសដោយ IP ដែលគ្រូបានផ្តល់ ហើយប្រើឈ្មោះសាកល្បងដែលមិនទាន់មានក្នុង file។

ពិនិត្យបន្ទាត់៖

~~~bash
grep -n 'web1' /etc/hosts
getent hosts web1
~~~

### ជំហាន E2៖ ជំនួសអត្ថបទដោយ sed

~~~bash
sudo sed -i 's/web1/web2/' /etc/hosts
grep -n 'web2' /etc/hosts
getent hosts web2
~~~

`sed -i` កែ file ដោយផ្ទាល់។ គំរូ `s/web1/web2/` ជំនួសការផ្គូផ្គងដំបូងក្នុងបន្ទាត់នីមួយៗដែលមាន `web1`; វាដំណើរការលើ file ទាំងមូល។ ពិនិត្យថា hostname និង IP នៅត្រឹមត្រូវ កុំប្រើវាលើ file ដែលមិនបានពិនិត្យ។

បញ្ចប់ដោយស្តារ backup ដែលបានធ្វើក្នុង Part D៖

~~~bash
sudo cp -p /etc/hosts.bak /etc/hosts
diff -u /etc/hosts.bak /etc/hosts
~~~

`diff` មិនបង្ហាញ output បើ file ដូចគ្នា។ នេះស្តារកំណែ `/etc/hosts` មុន Part D/E។

### ជំហាន E3៖ មូលហេតុដែល `sudo echo ... >> file` បរាជ័យ

កុំប្រើ command ខាងក្រោមដើម្បីកែ file ប្រព័ន្ធ៖

~~~bash
sudo echo hello >> /etc/hosts
~~~

វាអាចបរាជ័យដោយ Permission denied។ Shell បកស្រាយ `>> /etc/hosts` មុនចាប់ផ្តើម `sudo echo`; ដូច្នេះសិទ្ធិ root មិនត្រូវបានប្រើសម្រាប់ redirection ទេ។ វិធីសមស្របគឺបញ្ជូន text ទៅ `sudo tee -a` ដូចជាជំហាន E1—តែធ្វើបន្ទាប់ពី backup និងប្រើបន្ទាត់ដែលមានទម្រង់ hosts ត្រឹមត្រូវ។

**កុំបន្ថែមពាក្យ `hello` ដាច់ដោយឡែកទៅ `/etc/hosts`** ព្រោះវាមិនមែនជាបន្ទាត់ IP/hostname ត្រឹមត្រូវ។

### ជំហានជម្រើស៖ កែដោយ GUI

បើប្រើ desktop ហើយកម្មវិធី Gedit (ឬ editor GUI ដែល distro ផ្តល់) មានស្រាប់ អាចបើក file ហាត់ដូចនេះ៖

~~~bash
gedit hello.txt &
~~~

នេះជាជម្រើសសម្រាប់ desktop ប៉ុណ្ណោះ; server គ្មាន GUI អាចមិនមាន command `gedit`។

## ៨. ផ្នែក F៖ សំណួរពិនិត្យ និងចម្លើយ

សាកឆ្លើយសំណួរទាំងនេះ មុនបើកចម្លើយគំរូ៖

1. តើគ្រាប់ចុចណារក្សាទុក និងចេញពី nano?
2. គ្រាប់ចុចណាចាប់ផ្តើមវាយអក្សរក្នុង vi?
3. តើ command ណារក្សាទុក និងចេញពី vi?
4. តើ command ណាចេញពី vi ដោយមិនរក្សាទុក?
5. តើ command ណាជំនួស `Norton` ទៅ `NORTON` ទូទាំង file?
6. `rpm -q vim-enhanced` បង្ហាញអ្វី?
7. `echo "$EDITOR"` បង្ហាញអ្វី?
8. `getent hosts rhel9-srv` បង្ហាញអ្វី?
9. `2a3` ក្នុង output របស់ diff មានន័យអ្វី?
10. ហេតុអ្វី `sudo echo hello >> /etc/hosts` បរាជ័យ?

<details>
<summary>ចម្លើយគំរូ</summary>

1. Ctrl+O រក្សាទុក; Ctrl+X ចេញពី nano។
2. `i` ចូល Insert mode។
3. `:wq` រក្សាទុកហើយចេញ។
4. `:q!` ចេញដោយបោះចោលការកែដែលមិនបានរក្សាទុក។
5. `:%s/Norton/NORTON/g`។
6. ឈ្មោះ និងកំណែ package បើបានដំឡើង; បើមិនមាន វាប្រាប់ថា package មិនបានដំឡើង។
7. តម្លៃ `EDITOR`; រំពឹង `vim` បន្ទាប់ពីកំណត់រួច។
8. បន្ទាត់ hostname-to-address ដែលប្រព័ន្ធ resolve; IP ត្រូវតែដូចដែលបានកំណត់។
9. ក្នុង unified diff វាបង្ហាញការបន្ថែម (append) ក្រោយបន្ទាត់ទី 2 នៃ file ដើម ដើម្បីក្លាយជាបន្ទាត់ទី 3 ក្នុង file ថ្មី។ លេខអាចប្រែប្រួល។
10. Shell ជាអ្នកបើក file សម្រាប់ `>>` មុន `sudo` ចាប់ផ្តើម; ប្រើ `sudo tee -a` បន្ទាប់ពី backup និងផ្តល់បន្ទាត់ hosts ត្រឹមត្រូវ។

</details>

## ៩. ផ្នែក G៖ កិច្ចការពិត—បង្កើត Server Notes

### ជំហាន G1៖ បង្កើត file កំណត់ចំណាំ

~~~bash
cd ~/lab5
vi server-notes.txt
~~~

ចុច `i` រួចសរសេរបួនបន្ទាត់៖

1. Hostname របស់ VM ដែលបានបញ្ជាក់ដោយ `hostname`។
2. គោលបំណងរបស់ server សាកល្បង (ឧ. `Linux lab VM`)។
3. ឈ្មោះ admin ជាអត្ថបទសាកល្បង ឬតួនាទី (កុំបញ្ចូលព័ត៌មានផ្ទាល់ខ្លួនដែលមិនចាំបាច់)។
4. កាលបរិច្ឆេទថ្ងៃនេះ ពិនិត្យដោយ `date +%F`។

ចុច Esc, រក្សាទុកដោយ `:wq`, ហើយពិនិត្យ៖

~~~bash
cat server-notes.txt
~~~

### ជំហាន G2៖ បម្រុងទុក និងប្រៀបធៀបការកែ

~~~bash
cp server-notes.txt server-notes.bak
vi server-notes.txt
~~~

បន្ថែមបន្ទាត់មួយ ដូចជា `Purpose: practice text editing`; ចុច Esc និង `:wq`។ បន្ទាប់មក៖

~~~bash
diff -u server-notes.bak server-notes.txt
~~~

Output របស់ diff គួរបង្ហាញបន្ទាត់ថ្មី។ លេខបន្ទាត់ពឹងលើ file របស់អ្នក។

### ជំហាន G3៖ ពន្យល់ចម្លើយ

1. ហេតុអ្វី system administrator គួរចេះ terminal editor?
2. ហេតុអ្វីត្រូវចម្លង file មុនកែ?
3. Esc ធ្វើអ្វីក្នុង vi?
4. ហេតុអ្វីប្រើ `sudo vim /etc/hosts` ជំនួស `vim /etc/hosts`?
5. `vi` និង `vim` ខុសគ្នាដូចម្តេច?

<details>
<summary>ចម្លើយគំរូ</summary>

1. Server ជាច្រើនគ្មាន desktop; configuration files និង scripts ជា text files។
2. Backup អនុញ្ញាតឱ្យស្តារកំណែចាស់ ហើយ `diff` បង្ហាញអ្វីដែលបានផ្លាស់។
3. ចេញពី Insert mode ហើយត្រឡប់ទៅ Normal mode។
4. `/etc/hosts` ជាកម្មសិទ្ធិ root; user ធម្មតាមិនអាចរក្សាទុកការកែទៅ file នោះបានទេ។
5. `vi` ជា editor ប្រពៃណី/តូចដែលមានលើប្រព័ន្ធជាច្រើន; `vim` ជា “Vi IMproved” ដែលបន្ថែមមុខងារ។ នៅ RHEL, package `vim-enhanced` ផ្តល់ Vim ដែលមានមុខងារបន្ថែម។

</details>

## ១០. ផ្នែក H៖ អនុវត្តបន្ថែមលើ LabEx (ជាជម្រើស)

លំហាត់ LabEx ខាងក្រោមត្រូវការ internet និងរត់ក្នុង environment ដាច់ដោយឡែក។ ឈ្មោះ ឬកំណែ RHEL អាចខុសពី VM របស់អ្នក; ពិនិត្យមុនចាប់ផ្តើម៖

| LabEx | អ្វីដែលអនុវត្ត |
|---|---|
| Edit Text and Use Pipelines | Vim, redirection និង pipe |
| Access the Command Line | មូលដ្ឋាន shell |
| Get Command-Line Help | `man` pages និង `--help` |
| Manage Files and Directories | ការធ្វើការជាមួយ files និង directories |

សម្រាប់ការបញ្ជូនការងារទៅថ្នាក់ សូមអនុវត្តតាមទម្រង់ដែលគ្រូបានកំណត់។ កុំដាក់ screenshots ដែលមានព័ត៌មាន account, hostname ឬ IP ទៅ repository សាធារណៈ។

## ១១. ការបញ្ជូនការងារ (បើគ្រូតម្រូវ)

- បំពេញតារាង Part F និងចម្លើយសំណួរ Part G។
- Screenshot 1៖ nano បើក file ហើយបង្ហាញអត្ថបទ និងលេខបន្ទាត់។
- Screenshot 2៖ terminal បង្ហាញលទ្ធផល `cat school.txt` ក្រោយកែ និងរក្សាទុក។
- Screenshot 3៖ terminal បង្ហាញ `getent hosts` និង `diff` ក្រោយកែ `/etc/hosts`។
- ឯកសារដើមណែនាំឈ្មោះ `Lab5_YourName_StudentID`; អនុវត្តតាម format ដែលគ្រូប្រាប់។
- កុំបង្ហោះ screenshot សាធារណៈ បើវាបង្ហាញព័ត៌មានផ្ទាល់ខ្លួន ឬ network របស់អ្នក។

## ១២. បញ្ហាទូទៅ និងការស្តារឡើងវិញ

- **វាយអក្សរហើយបាត់ទៅ ឬគ្រាប់ចុចកំពុងធ្វើ command**៖ អ្នកអាចនៅ Normal mode; ចុច `i` ដើម្បីវាយអត្ថបទ។
- **មិនអាចចេញពី vi**៖ ចុច Esc; បន្ទាប់មកវាយ `:q!` ឬ `:wq` ហើយ Enter។
- **មានសារ swap file**៖ អាចមាន session ចាស់ ឬ Vim មុនបិទមិនត្រឹមត្រូវ។ កុំលុប `.swp` ដោយស្វ័យប្រវត្តិ; ពិនិត្យថាមាន editor ផ្សេងកំពុងកែ file ដែរឬទេ ហើយសង្គ្រោះមាតិកាបើចាំបាច់។
- **Permission denied ពេលរក្សាទុក `/etc/hosts`**៖ ចេញដោយ `:q!` មុនកែតាមវិធីសមស្រប; បើអ្នកមានសិទ្ធិប្រើ sudo សូមបើក file ដោយ `sudo vim /etc/hosts`។
- **DNF មិនរក `vim-enhanced`**៖ ពិនិត្យថា DVD ISO បានភ្ជាប់/mount, repository file មាន, base URL ត្រឹមត្រូវ និង repo បាន enable។
- **`getent` មិនបង្ហាញឈ្មោះ**៖ ពិនិត្យ spelling, spaces ក្នុង hosts line, IP ដែលប្រើ និងថាតើ file ត្រូវបានរក្សាទុកឬអត់។
- **`sudo echo ... >> file` បង្ហាញ Permission denied**៖ នេះបង្ហាញថា redirection ធ្វើដោយ shell; ប្រើ `sudo tee -a` តែសម្រាប់បន្ទាត់ត្រឹមត្រូវ និងក្រោយ backup។
- **Gedit មិនស្គាល់**៖ VM អាចជា server គ្មាន GUI ឬ package មិនបានដំឡើង; ប្រើ nano/vi ដូចគោលបំណង Lab។

## ១៣. សង្ខេប

`nano` ជា editor ងាយចាប់ផ្តើមដែលបង្ហាញ shortcut នៅលើអេក្រង់។ `vi`/`vim` មាន modes ដាច់ពីគ្នា: ប្រើ Normal mode សម្រាប់ commands, Insert mode សម្រាប់វាយអត្ថបទ និង `:...` សម្រាប់ command line។ មុនកែ configuration file ត្រូវបម្រុងទុក, កែតែក្នុងប្រព័ន្ធដែលអ្នកគ្រប់គ្រង, ប្រើតម្លៃដែលគ្រូបានផ្តល់, បន្ទាប់មក verify និងស្តារ backup ពេលលំហាត់ចប់។
