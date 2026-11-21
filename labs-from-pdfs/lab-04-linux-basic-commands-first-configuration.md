# Lab ៤៖ ពាក្យបញ្ជា Linux មូលដ្ឋាន និងការកំណត់ប្រព័ន្ធដំបូង (RHEL 9.6)

Lab នេះបន្តពីការស្គាល់ Linux ក្នុង Lab ១–៣។ អ្នកនឹងហាត់បង្កើត និងស្វែងរកឯកសារ អាន manual, ភ្ជាប់ពាក្យបញ្ជាដោយ pipe, ពិនិត្យ process និងកំណត់ shell/hostname/timezone។ ពេលវេលាប្រហែល ១២០ នាទី។

## ១. គោលបំណង

ក្រោយអនុវត្ត អ្នកអាច៖

- រុករក directories និងប្រើ `mkdir`, `cd`, `pwd`, `touch`, `cp`, `mv`, `ls`, និង `find`។
- រកជំនួយដោយ `whatis`, `man`, `man -k`, និង `--help`។
- អាន ស្វែងរក រាប់ និងតម្រៀបអត្ថបទដោយ `cat`, `grep`, `wc`, `head`, `tail`, `cut`, `sort`, និង `uniq`។
- ពន្យល់ពីការបង្វែរលទ្ធផលទៅ file ដោយ `>` និង `>>`, និងការភ្ជាប់ command ដោយ `|`។
- ពិនិត្យព័ត៌មានប្រព័ន្ធ និងគ្រប់គ្រង process ដែលអ្នកចាប់ផ្តើម។
- កែ shell settings, hostname និង timezone ដោយយល់ថាការកំណត់ណាប៉ះ user និងការកំណត់ណាប៉ះប្រព័ន្ធទាំងមូល។

## ២. បរិស្ថាន និងសុវត្ថិភាព

### អ្វីដែលត្រូវមាន

- RHEL 9.6 VM ឈ្មោះឧទាហរណ៍ `rhel9-lab1` ពី Lab ១។
- User ធម្មតា `student01` ដែលអាចប្រើ `sudo` តាមការអនុញ្ញាតរបស់ថ្នាក់។
- ពេលវេលាប្រហែល ២ ម៉ោង។

មុនចាប់ផ្តើម សូមបង្កើត VirtualBox snapshot ឈ្មោះ `lab4-start` ដើម្បីអាចត្រឡប់ទៅសភាពដើម បើការកំណត់ខុស។ ពាក្យបញ្ជាក្នុង Lab នេះត្រូវវាយក្នុង terminal របស់ VM; កុំរត់លើ Windows host ឬ server ពិត។

**កុំបង្ហោះ screenshot សាធារណៈដែលមាន username, hostname, IP, account list ឬព័ត៌មានផ្ទាល់ខ្លួន។** បើគ្រូស្នើការបញ្ជូនការងារ សូមប្រើវិធីដែលគ្រូកំណត់ និងលាក់ព័ត៌មានដែលមិនចាំបាច់។

### ចំណាំអំពីសិទ្ធិ

- ពាក្យបញ្ជាធម្មតាដំណើរការជា user បច្ចុប្បន្ន។
- `sudo` បង្កើនសិទ្ធិសម្រាប់ command មួយ; ប្រើតែពេលចាំបាច់។
- បើ `sudo` ប្រាប់ថា user មិននៅក្នុង sudoers សូមឈប់ ហើយធ្វើតាមរបៀបដែលគ្រូ/អ្នកគ្រប់គ្រងបានអនុញ្ញាតក្នុង VM។ កុំស្វែងរកផ្លូវជុំវិញសិទ្ធិលើម៉ាស៊ីនដែលអ្នកមិនគ្រប់គ្រង។
- `>` សរសេរជំនួសមាតិកា file ចាស់។ `>>` បន្ថែមនៅខាងចុង។ ពិនិត្យ file មុនប្រើ `>`។
- ផ្នែកកែ hostname/timezone ជាការកំណត់ប្រព័ន្ធទាំងមូល។ ធ្វើតែក្នុង VM ដែលអ្នកទទួលខុសត្រូវ។

## ៣. ត្រៀមថតហាត់

បង្កើតថតឯកសារហាត់ និងចូលទៅក្នុងវា៖

~~~bash
mkdir -p ~/lab4/docs ~/lab4/backup
cd ~/lab4
pwd
~~~

- `~` សម្គាល់ home directory របស់ user បច្ចុប្បន្ន។
- `mkdir -p` បង្កើតថតកណ្ដាលដែលមិនទាន់មាន ដោយមិនបង្ហាញ error បើថតមានរួច។
- `cd` ប្តូរ directory ក្នុង shell។
- `pwd` បង្ហាញផ្លូវពេញនៃទីតាំងបច្ចុប្បន្ន។

រំពឹងថា `pwd` បង្ហាញផ្លូវដែលបញ្ចប់ដោយ `/lab4`។

## ៤. ផ្នែក A៖ ឯកសារ ថត និងការស្វែងរក

ធ្វើជំហានខាងក្រោមតាមលំដាប់។ សូមពិនិត្យលទ្ធផលរាល់ដំណាក់កាល មុនបន្ត។

### ជំហាន A1៖ បង្កើត file សាកល្បង

~~~bash
cd ~/lab4
touch a.txt b.txt c.txt
ls -l
~~~

`touch` បង្កើត file ទទេ បើ file មិនមាន។ បើមានរួច វាធ្វើបច្ចុប្បន្នភាពម៉ោងកែប្រែ។ `ls -l` បង្ហាញសិទ្ធិ, owner, ទំហំ និងឈ្មោះ file។

### ជំហាន A2៖ ចម្លង និងផ្លាស់ទី

~~~bash
cp a.txt backup/
mv b.txt docs/
ls -R
~~~

- `cp` ចម្លង `a.txt` ទៅថត `backup`; ឯកសារដើមនៅតែមានក្នុង `~/lab4`។
- `mv` ផ្លាស់ទី `b.txt` ទៅថត `docs`; ឥឡូវវាមិននៅក្នុងថតដើមទៀតទេ។
- `ls -R` រាយមាតិកាថត និងថតរងទាំងអស់។

រូបរាងសង្ខេបគួរមាន៖

~~~text
~/lab4/
├── a.txt
├── c.txt
├── backup/
│   └── a.txt
└── docs/
    └── b.txt
~~~

### ជំហាន A3៖ មើលព័ត៌មាន file និងប្រើ wildcard

~~~bash
ls -l
ls *.txt
~~~

- `ls -l` បង្ហាញព័ត៌មានលម្អិត។
- `*.txt` ជា wildcard: shell ជំនួសវាដោយឈ្មោះ file ទាំងអស់ក្នុងថតបច្ចុប្បន្នដែលបញ្ចប់ដោយ `.txt`។
- នៅចំណុចនេះ `ls *.txt` គួរបង្ហាញ `a.txt` និង `c.txt`; `b.txt` ត្រូវបានផ្លាស់ទៅ `docs/` ហើយ។

### ជំហាន A4៖ ស្វែងរក file និងថត

~~~bash
find /etc -name hosts
find ~ -type d
~~~

- `find /etc -name hosts` ស្វែងរកឈ្មោះ `hosts` ក្រោម `/etc`; ជាទូទៅលទ្ធផលមាន `/etc/hosts`។
- `find ~ -type d` បង្ហាញថតនៅក្នុង home directory និងថតរងរបស់វា។
- ប្រព័ន្ធខ្លះអាចបង្ហាញ warning ប្រសិនបើ user មិនមានសិទ្ធិចូលថតមួយចំនួន។ សម្រាប់លំហាត់នេះ សូមយកចិត្តទុកដាក់លើ path ដែលបានរកឃើញ។

## ៥. ផ្នែក B៖ Manual, អត្ថបទ និង redirection

### ជំហាន B1៖ រកជំនួយពី manual

~~~bash
whatis passwd
man 5 passwd
~~~

`whatis` បង្ហាញសេចក្តីពិពណ៌នាខ្លីពី manual entries ដែលរកឃើញ។ `man 5 passwd` បើកទំព័រ section 5 ស្តីពីទម្រង់ file `/etc/passwd`; ចុច `q` ដើម្បីចេញពី manual។

លេខ section មានន័យខុសគ្នា៖ section 1 ជាពាក្យបញ្ជារបស់អ្នកប្រើ; section 5 ជាទម្រង់ file និង configuration។ ដូច្នេះ `passwd` និង `passwd` ក្នុង section 5 អាចពិពណ៌នារឿងផ្សេងគ្នា។

សាកស្វែងរក manual ដែលពាក់ព័ន្ធ hostname៖

~~~bash
man -k hostname
~~~

បើមិនឃើញលទ្ធផល សន្ទស្សន៍ man page អាចមិនទាន់បង្កើត។ ក្នុង VM ដែលអ្នកគ្រប់គ្រង អាចធ្វើបច្ចុប្បន្នភាពវាដោយ៖

~~~bash
sudo mandb
man -k hostname
~~~

### ជំហាន B2៖ មើលជំនួយខ្លី

~~~bash
ls --help | head -n 5
~~~

- `ls --help` បង្ហាញជម្រើសខ្លីៗរបស់ command។
- `|` ផ្ញើ output របស់ command ខាងឆ្វេងទៅ command ខាងស្តាំ។
- `head -n 5` បង្ហាញតែ ៥ បន្ទាត់ដំបូង។

### ជំហាន B3៖ សរសេរ បន្ថែម និងអាន file

~~~bash
cd ~/lab4
echo "Norton University" > school.txt
echo "Phnom Penh" >> school.txt
cat school.txt
wc -l school.txt
grep Norton school.txt
~~~

រំពឹងថា file មានពីរបន្ទាត់៖

~~~text
Norton University
Phnom Penh
~~~

- `>` បង្កើត file ថ្មី ឬសរសេរជំនួសមាតិកាចាស់ទាំងអស់។
- `>>` បន្ថែមបន្ទាត់នៅចុង file ដោយរក្សាបន្ទាត់ចាស់។
- `cat` បង្ហាញមាតិកា file។
- `wc -l` រាប់ចំនួនបន្ទាត់; នៅទីនេះលទ្ធផលគួរតែ 2។
- `grep Norton` បង្ហាញតែបន្ទាត់ដែលមានអក្សរ Norton។

**ចាំ៖** ពិនិត្យ file មុនប្រើ `>` ដើម្បីជៀសការលុបមាតិកាចាស់ដោយចៃដន្យ។

### ជំហាន B4៖ អានចុង និងដើម file ប្រព័ន្ធ

~~~bash
head -n 3 /etc/passwd
tail -n 3 /etc/passwd
~~~

`head` បង្ហាញបីបន្ទាត់ដំបូង; `tail` បង្ហាញបីបន្ទាត់ចុងក្រោយ។ `/etc/passwd` មានព័ត៌មាន account ដែលប្រព័ន្ធប្រើ ដូច្នេះកុំចែករំលែក output ឬ screenshot ដោយមិនពិនិត្យថាមានទិន្នន័យឯកជនឬអត់។

## ៦. ផ្នែក C៖ Pipe និងឧបករណ៍អត្ថបទ

Pipe `|` ភ្ជាប់ output របស់ command មួយទៅ input របស់ command បន្ទាប់។ វាធ្វើឱ្យអាចសង្ខេប ឬត្រងលទ្ធផលដោយមិនចាំបាច់បង្កើត file បណ្ដោះអាសន្ន។

### ជំហាន C1៖ រាប់ចំនួន entries

~~~bash
ls /etc | wc -l
~~~

`ls /etc` រាយឈ្មោះ entries ក្នុង `/etc`; `wc -l` រាប់បន្ទាត់ដែលទទួលបាន។ លទ្ធផលអាស្រ័យលើ RHEL installation។

### ជំហាន C2៖ ស្វែងរក user ក្នុង account file

~~~bash
grep student01 /etc/passwd
~~~

វាបង្ហាញបន្ទាត់ account ដែលមានឈ្មោះ `student01` ប្រសិនបើ user នោះមានក្នុងប្រព័ន្ធ។ `/etc/passwd` ជា account metadata; password hash មិនរក្សាទុកនៅទីនេះលើ RHEL សម័យថ្មីទេ តែទិន្នន័យនៅតែគួរចាត់ទុកជាព័ត៌មានប្រព័ន្ធ។

### ជំហាន C3៖ ទាញយក username ចេញពី file

~~~bash
cut -d: -f1 /etc/passwd | head -n 3
~~~

- `cut` បំបែក field តាម delimiter `:`។
- `-f1` ជ្រើស field ទីមួយ គឺ username។
- `head -n 3` បង្ហាញតែបី username ដំបូង។
- លទ្ធផលជាក់ស្តែងអាស្រ័យលើប្រព័ន្ធ; កុំចាត់ទុកឈ្មោះជាក់លាក់ថាត្រូវគ្រប់ RHEL VM។

### ជំហាន C4៖ តម្រៀបបន្ទាត់

~~~bash
cat /etc/passwd | sort | head -n 3
~~~

`sort` តម្រៀបបន្ទាត់អក្ខរក្រម ហើយ `head` យកបីបន្ទាត់ដំបូងក្រោយតម្រៀប។ នេះបង្ហាញថា pipe អនុញ្ញាតឱ្យដាក់ command តូចៗជាច្រើនជាជំហាន។

### ជំហាន C5៖ រាប់តម្លៃដដែល

~~~bash
cd ~/lab4
printf "b\na\nb\n" > names.txt
sort names.txt | uniq -c
~~~

លទ្ធផលគួរបង្ហាញថា `a` មានមួយដង និង `b` មានពីរដង។ `uniq` រាប់តែបន្ទាត់ដដែលដែលនៅជាប់គ្នា; ដូច្នេះប្រើ `sort` មុន ដើម្បីដាក់តម្លៃដូចគ្នានៅជាប់គ្នា។

### ជំហាន C6៖ រាប់ process

~~~bash
ps -e | wc -l
~~~

`ps -e` បង្ហាញ process ទាំងអស់ដែលអាចមើលឃើញ; `wc -l` រាប់បន្ទាត់។ លេខអាចខុសគ្នារាល់ពេល ហើយអាចរាប់ header ផងដែរ។

## ៧. ផ្នែក D៖ ព័ត៌មានប្រព័ន្ធ និង process

### ជំហាន D1៖ ពិនិត្យប្រព័ន្ធ

~~~bash
hostname
uname -r
uptime
free -h
df -h /
~~~

- `hostname` បង្ហាញឈ្មោះម៉ាស៊ីន។
- `uname -r` បង្ហាញ Linux kernel release។
- `uptime` បង្ហាញថាប្រព័ន្ធដំណើរការយូរប៉ុន្មាន និង load averages។
- `free -h` បង្ហាញ memory និង swap ជាទម្រង់ងាយអាន។
- `df -h /` បង្ហាញទំហំ filesystem ដែលផ្ទុក root directory។
- លេខ memory/disk និង uptime ប្រែប្រួលទៅតាម VM។

### ជំហាន D2៖ បង្កើត process សាកល្បងដែលអ្នកគ្រប់គ្រង

~~~bash
sleep 300 &
SLEEP_PID=$!
echo "$SLEEP_PID"
ps -p "$SLEEP_PID"
~~~

`sleep 300` រង់ចាំ ៣០០ វិនាទី។ `&` ដាក់វាឱ្យដំណើរការខាងក្រោយ ដើម្បីឱ្យ shell អាចទទួល command បន្ទាប់។ `$!` គឺ PID របស់ process ខាងក្រោយដែលទើបចាប់ផ្តើម។ `ps -p` ពិនិត្យតែ PID នោះ។

ចំណាំ៖ `SLEEP_PID` ជា shell variable សម្រាប់ session នេះ; វាមិនត្រូវដាក់ជាលេខ PID ថេរទេ។

### ជំហាន D3៖ បញ្ឈប់តែ process ដែលបានបង្កើត

~~~bash
kill -TERM "$SLEEP_PID"
wait "$SLEEP_PID" 2>/dev/null || :
ps -p "$SLEEP_PID"
~~~

`kill -TERM` ស្នើឱ្យ process នោះបញ្ចប់។ `wait` រង់ចាំ child process ឱ្យចប់; `|| :` ធ្វើឱ្យ shell មិនឈប់លើ exit status ដែលកើតឡើងព្រោះ process ត្រូវបានបញ្ឈប់។ បើ `ps` មិនបង្ហាញ process ទៀត នោះវាបានចប់។ ប្រើតែ PID ដែលអ្នករក្សាទុកពី `sleep 300`; កុំចម្លង PID របស់ process មិនស្គាល់។

## ៨. ផ្នែក E៖ ការកំណត់ដំបូង

### ជំហាន E1៖ Shell variables និង PATH

~~~bash
echo "$HOME"
echo "$USER"
MYSCHOOL=Norton
echo "$MYSCHOOL"
export MYSCHOOL
echo "$PATH"
~~~

- `HOME` ជា home directory របស់ user។
- `USER` ជាឈ្មោះ user បច្ចុប្បន្ន។
- `MYSCHOOL=Norton` បង្កើត shell variable; **មិនដាក់ដកឃ្លាជុំវិញ `=`**។
- `export MYSCHOOL` អនុញ្ញាតឱ្យ process កូនទទួល variable នេះ។
- `PATH` ជាបញ្ជី directories ដែល shell ស្វែងរកពេលអ្នកវាយ command។

Variable ដែលបង្កើតក្នុង terminal មិនត្រូវបានរក្សាទុកពេលបិទ session ទេ លុះត្រាតែអ្នកកំណត់វាក្នុង startup file។

### ជំហាន E2៖ បម្រុងទុក និងកែ `~/.bashrc`

ដំបូងពិនិត្យថា file មាន ហើយបង្កើត backup៖

~~~bash
ls -l ~/.bashrc
cp ~/.bashrc ~/.bashrc.bak
~~~

បន្ទាប់មកពិនិត្យថាបន្ទាត់ទាំងនេះមិនទាន់មាន មុនបន្ថែម ដើម្បីកុំបង្កើត alias ឬ setting ស្ទួន៖

~~~bash
grep -n "alias ll=" ~/.bashrc
grep -n "HISTTIMEFORMAT" ~/.bashrc
~~~

បើមិនទាន់មាន បន្ថែម៖

~~~bash
printf '%s\n' "alias ll='ls -lh'" >> ~/.bashrc
printf '%s\n' 'export HISTTIMEFORMAT="%F %T "' >> ~/.bashrc
source ~/.bashrc
ll
history | tail -n 3
~~~

- `alias ll='ls -lh'` បង្កើត shorthand `ll` សម្រាប់បង្ហាញ file លម្អិត និងទំហំងាយអាន។
- `HISTTIMEFORMAT` កំណត់ទម្រង់ម៉ោងដែល `history` បង្ហាញសម្រាប់ command history។
- `source ~/.bashrc` អានការកំណត់ថ្មីក្នុង shell បច្ចុប្បន្ន ដោយមិនចាំបាច់ logout/login។
- ការបង្ហាញម៉ោងក្នុង history ពឹងលើថាតើ bash បានរក្សា timestamp សម្រាប់ពាក្យបញ្ជាមុនៗឬអត់។

បើត្រូវ rollback ការកែ សូមពិនិត្យ backup ហើយស្តារវិញដោយ៖

~~~bash
cp ~/.bashrc.bak ~/.bashrc
source ~/.bashrc
~~~

### ជំហាន E3៖ កំណត់ hostname ក្នុង VM

~~~bash
sudo hostnamectl set-hostname rhel9-lab1
hostname
cat /etc/hostname
~~~

`hostnamectl set-hostname` កំណត់ឈ្មោះម៉ាស៊ីនឱ្យនៅស្ថិតស្ថេរ។ ប្រើឈ្មោះដែលគ្រូកំណត់ ប្រសិនបើខុសពីឧទាហរណ៍។ កុំប្ដូរ hostname លើម៉ាស៊ីន ឬ server ដែលអ្នកមិនគ្រប់គ្រង។

### ជំហាន E4៖ មើល និងកំណត់ timezone

~~~bash
timedatectl
sudo timedatectl set-timezone Asia/Phnom_Penh
timedatectl
~~~

- `timedatectl` បង្ហាញម៉ោង, timezone, និងស្ថានភាព time synchronization។
- `set-timezone` កំណត់ timezone របស់ប្រព័ន្ធទៅ Phnom Penh។
- ការផ្លាស់ប្តូរនេះប៉ះអ្នកប្រើទាំងអស់ក្នុង VM។

**កុំចម្លងម៉ោងចាស់ដែលបោះពុម្ពក្នុង PDF ទៅ system clock របស់អ្នក។** លំហាត់ដើមមានការណែនាំបិទ NTP ហើយកំណត់ម៉ោងដោយដៃ សម្រាប់ server offline ប៉ុណ្ណោះ។ ធ្វើផ្នែកនោះតែបើគ្រូតម្រូវ និងក្នុង VM សាកល្បង៖ ប្រើកាលបរិច្ឆេទ/ម៉ោងបច្ចុប្បន្នដែលត្រឹមត្រូវសម្រាប់តំបន់ម៉ោងរបស់ VM, កត់ត្រាថា NTP ត្រូវបានបិទ, ហើយបើភ្ជាប់ network វិញ ត្រូវបើក synchronization ត្រឡប់មកវិញដោយ `sudo timedatectl set-ntp true`។ ម៉ោងខុសអាចប៉ះ logs, certificates និងការផ្ទៀងផ្ទាត់កម្មវិធី។

បើគ្រូតម្រូវឱ្យកំណត់ម៉ោងដោយដៃ ក្នុង VM offline សាកល្បង៖

~~~bash
sudo timedatectl set-ntp false
timedatectl
sudo timedatectl set-time "YYYY-MM-DD HH:MM:SS"
timedatectl
~~~

ក្នុង command ទីបី ជំនួសអក្សរ `YYYY-MM-DD HH:MM:SS` ដោយថ្ងៃ និងម៉ោងពិតរបស់អ្នក (តាម format ឆ្នាំ-ខែ-ថ្ងៃ ម៉ោង:នាទី:វិនាទី)។ កុំរត់ placeholder តាមន័យដើម និងកុំប្រើម៉ោងចាស់ក្នុង PDF។ ក្រោយធ្វើ lab និងភ្ជាប់ network វិញ បើក NTP ម្តងទៀត៖

~~~bash
sudo timedatectl set-ntp true
timedatectl
~~~

## ៩. ផ្នែក F៖ តារាងចម្លើយសម្រាប់ពិនិត្យ

សាកល្បងឆ្លើយសំណួរដោយមើល output របស់ VM របស់អ្នក មុនបើកចម្លើយគំរូ។

1. `ls *.txt` បង្ហាញ file ណាខ្លះក្រោយ Part A?
2. `find /etc -name hosts` រកឃើញអ្វី?
3. `man 5 passwd` ពន្យល់អំពីអ្វី?
4. `wc -l school.txt` បង្ហាញប៉ុន្មាន?
5. `>` និង `>>` ខុសគ្នាដូចម្តេច?
6. `cut -d: -f1 /etc/passwd | head -n 3` បង្ហាញអ្វី?
7. `sort names.txt | uniq -c` រាប់អ្វី?
8. `uname -r` បង្ហាញព័ត៌មានអ្វី?
9. `free -h` បង្ហាញព័ត៌មានអ្វី?
10. `df -h /` បង្ហាញទំហំទំនេរនៅទីណា?
11. តើ PID របស់ process `sleep` របស់អ្នកជាអ្វី?
12. តម្លៃ directory ដំបូងក្នុង `PATH` របស់អ្នកជាអ្វី?
13. `timedatectl` បង្ហាញ timezone អ្វី?

<details>
<summary>ចម្លើយគំរូសម្រាប់ផ្ទៀងផ្ទាត់</summary>

1. `a.txt` និង `c.txt`; `b.txt` ត្រូវបានផ្លាស់ទៅ `docs/`។
2. ជាទូទៅ `/etc/hosts`; output អាចមាន warning ពីសិទ្ធិ directory ផ្សេង។
3. ទម្រង់ និង field របស់ file `/etc/passwd`។
4. 2 បន្ទាត់ ព្រោះមាន `Norton University` និង `Phnom Penh`។
5. `>` សរសេរជំនួស file; `>>` បន្ថែមទៅខាងចុង។
6. Username បីដំបូងក្នុង file; ឈ្មោះជាក់លាក់អាចខុសតាម distro។
7. ចំនួនដងដែលបន្ទាត់នីមួយៗកើតឡើង៖ មួយ `a` និងពីរ `b`។
8. កំណែ Linux kernel ដែលកំពុងដំណើរការ។
9. Memory និង swap ជាទម្រង់ងាយអាន។
10. Root filesystem ដែល mount នៅ `/`។
11. ចម្លើយផ្ទាល់ខ្លួនពីតម្លៃ `$SLEEP_PID`; PID ខុសគ្នាតាម run។
12. ចម្លើយផ្ទាល់ខ្លួន; ប្រើ `printf '%s\n' "$PATH" | cut -d: -f1` ដើម្បីមើល។
13. បន្ទាប់ពីកំណត់ timezone គួរតែ `Asia/Phnom_Penh` បើប្រព័ន្ធមាន timezone data នោះ។

</details>

## ១០. ផ្នែក G៖ កិច្ចការពិត—បង្កើតរបាយការណ៍ប្រព័ន្ធ

### ជំហាន G1៖ បង្កើត report

~~~bash
cd ~/lab4
hostname > report.txt
timedatectl | grep "Time zone" >> report.txt
uptime >> report.txt
free -h >> report.txt
df -h / >> report.txt
ps -e | wc -l >> report.txt
cat report.txt
~~~

ពន្យល់លំដាប់៖

1. បន្ទាត់ដំបូងចាប់ផ្តើម report ថ្មី ហើយសរសេរ hostname។
2. បន្ទាត់បន្ទាប់ៗប្រើ `>>` ដើម្បីបន្ថែម timezone, uptime, memory, disk usage និងចំនួន process។
3. `cat report.txt` បង្ហាញអ្វីដែលបានប្រមូល។
4. រាល់លេខអាចខុសគ្នាតាម VM និងពេលដែលអ្នករត់ command។

បើចង់រត់ report ម្តងទៀត សូមដឹងថា `hostname > report.txt` នឹងសរសេរជំនួស report ចាស់។ នេះជាការចាប់ផ្តើម report ថ្មីដោយចេតនា។

### ជំហាន G2៖ ឆ្លើយសំណួរពន្យល់

1. ហេតុអ្វីគួររត់ `ls` មុន `rm`?
2. Pipe ធ្វើអ្វី?
3. `shutdown -h now` និង `shutdown -r +5` មានលទ្ធផលខុសគ្នាដូចម្តេច?
4. ហេតុអ្វីគួរប្រើ `sudo` តែពេលចាំបាច់?
5. ហេតុអ្វីគួរបម្រុងទុក `~/.bashrc` មុនកែ?
6. ហេតុអ្វីម៉ោងត្រឹមត្រូវសំខាន់សម្រាប់ server offline?

<details>
<summary>ចម្លើយគំរូ</summary>

1. `ls` ជួយបញ្ជាក់ថា file ណានឹងត្រូវលុប; Linux មិនមាន recycle bin សម្រាប់ការលុបពី terminal ទេ។
2. វាបញ្ជូន output របស់ command មួយទៅ command បន្ទាប់។
3. `shutdown -h now` បិទប្រព័ន្ធឥឡូវនេះ; `shutdown -r +5` កំណត់ reboot ក្រោយ ៥ នាទី។ កុំសាកទាំងនេះក្នុង VM ដែលកំពុងត្រូវការ។
4. ដើម្បីកាត់បន្ថយហានិភ័យកំហុសដែលមានសិទ្ធិខ្ពស់។
5. អាចស្តារការកំណត់ចាស់ បើបន្ថែម syntax ខុស។
6. Logs និង certificate validation អាចអាស្រ័យលើម៉ោង; server offline មិនអាច sync ជាមួយ time server បាន។

</details>

## ១១. ផ្នែក H៖ អនុវត្តបន្ថែមលើ LabEx (ជាជម្រើស)

LabEx ក្នុងឯកសារដើមត្រូវការ internet និងប្រើបរិស្ថានផ្ទាល់ខ្លួន។ បើចូលប្រើបាន សូមធ្វើលំហាត់ដែលមានឈ្មោះស្រដៀងនឹង៖

| LabEx | អ្វីដែលអនុវត្ត |
|---|---|
| Access the Command Line | ចូលប្រើ terminal និងរត់ command |
| Manage Files and Directories | បង្កើត ចម្លង ផ្លាស់ទី និងលុប file |
| Get Command-Line Help | `man` pages និង `--help` |
| Monitor and Manage Processes | `ps`, `top`, និង `kill` |
| Edit Text and Use Pipelines | redirection និង pipe |

ឈ្មោះ និងកំណែ distro ក្នុង LabEx អាចខុសពី RHEL 9.6 VM របស់អ្នក។ សូមពិនិត្យមេរៀនដែលបានផ្តល់ និងកុំសន្មតថា output ដូចគ្នាទាំងស្រុង។

## ១២. ការបញ្ជូនការងារ (បើគ្រូតម្រូវ)

- បំពេញតារាង Part F និងចម្លើយ Part G។
- Screenshot 1៖ terminal បន្ទាប់ពីបញ្ឈប់ process `sleep`។
- Screenshot 2៖ លទ្ធផល `timedatectl` ក្រោយការកំណត់ timezone។
- Screenshot 3៖ terminal បង្ហាញ `cat report.txt`។
- ប្រើឈ្មោះ file តាមគ្រូកំណត់; ឯកសារដើមណែនាំទម្រង់ `Lab4_YourName_StudentID`។
- ពិនិត្យ និងលាក់ព័ត៌មានឯកជនមុនបញ្ជូន។ កុំដាក់ screenshot ទាំងនេះក្នុង GitHub សាធារណៈ។

## ១៣. បញ្ហាទូទៅ និងវិធីដោះស្រាយ

- **command not found**៖ ពិនិត្យអក្ខរាវិរុទ្ធ និងអក្សរតូច/ធំ; មើល `command --help` ឬ `man command`។
- **No such file or directory**៖ រត់ `pwd` និង `ls`; ពិនិត្យថាកំពុងនៅ directory ត្រឹមត្រូវ។
- **Permission denied**៖ ពិនិត្យ path និងសិទ្ធិ; ប្រើ `sudo` តែបើការងារត្រូវការសិទ្ធិគ្រប់គ្រង និងអ្នកមានសិទ្ធិនោះ។
- **`>` លុបបន្ទាត់ចាស់**៖ វាជាឥរិយាបថធម្មតា; ស្តារពី backup ឬបង្កើត file ម្តងទៀត។ ប្រើ `>>` បើចង់បន្ថែម។
- **`man -k` មិនរកឃើញ**៖ សាក `sudo mandb` ក្នុង VM រួចស្វែងរកម្ដងទៀត។
- **`timedatectl set-time` មិនដំណើរការ**៖ NTP អាចកំពុង sync; កុំបិទ sync លើម៉ាស៊ីនដែលអ្នកមិនគ្រប់គ្រង។ សម្រាប់ lab offline សូមសួរគ្រូពីពេលវេលាត្រឹមត្រូវ។
- **screen capture បង្ហាញព័ត៌មានផ្ទាល់ខ្លួន**៖ កុំបង្ហោះ; ថតឡើងវិញដោយលាក់ ឬដកព័ត៌មានមិនចាំបាច់តាមវិធីដែលគ្រូអនុញ្ញាត។

## ១៤. សង្ខេប

ក្នុង Lab នេះ អ្នកបានប្រើ file commands និង wildcard, អាន manual, បង្កើត file ដោយ redirection, បញ្ជូន output ដោយ pipe, ពិនិត្យ system resources និងបញ្ឈប់ process ដែលខ្លួនចាប់ផ្តើម។ អ្នកក៏បានកែ `~/.bashrc`, hostname និង timezone ក្នុង VM។ មេរៀនសុវត្ថិភាពសំខាន់គឺ៖ មើលគោលដៅមុនសរសេរ, ធ្វើ backup មុនកែ configuration, និងប្រើ `sudo` តែពេលចាំបាច់។
