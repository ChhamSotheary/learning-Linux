# មេរៀនទី ៤៖ Users, Groups និង Permissions

## គោលបំណងមេរៀន

បន្ទាប់ពីរៀនចប់ អ្នកអាច៖

- ពិនិត្យ user និង groups ដែលកំពុងប្រើ។
- អាន ownership និង permission ក្នុង ls -l។
- ពន្យល់ read, write និង execute permissions។
- កែ permission លើឯកសារសាកល្បងដោយប្រើ symbolic និង numeric modes។
- យល់ពី umask និងគោលការណ៍ least privilege។

## ១. Users និង Groups

Linux ប្រើ user accounts ដើម្បីកំណត់អត្តសញ្ញាណដំណើរការ និងម្ចាស់ឯកសារ។ Groups ជួយផ្ដល់សិទ្ធិទៅក្រុមអ្នកប្រើជំនួសឱ្យការកំណត់ម្នាក់មួយៗ។

ពិនិត្យ identity របស់អ្នក៖

~~~bash
whoami
id
groups
~~~

id បង្ហាញ UID, GID និង groups របស់ user បច្ចុប្បន្ន។ UID 0 ជាធម្មតាសម្រាប់ root account។ ការប្រើ root មានសិទ្ធិខ្ពស់ ហើយអាចប៉ះពាល់ប្រព័ន្ធទាំងមូល។

## ២. អាន ls -l

បង្កើត file សាកល្បង រួចពិនិត្យ៖

~~~bash
mkdir -p "$HOME/linux-practice/lesson-04"
cd "$HOME/linux-practice/lesson-04"
touch notes.txt
ls -l notes.txt
~~~

Output អាចមានទម្រង់ដូចជា៖

~~~text
-rw-r--r-- 1 sam users 0 ... notes.txt
~~~

- តួអក្សរដំបូងបង្ហាញប្រភេទ item; - ជា regular file, d ជា directory។
- តួអក្សរបីបន្ទាប់ជាសិទ្ធិរបស់ owner។
- បីបន្ទាប់ជាសិទ្ធិរបស់ group។
- បីចុងក្រោយជាសិទ្ធិរបស់ others។
- បន្ទាប់មកមានចំនួន links, owner, group, size, time និង name។

លទ្ធផលពិតអាស្រ័យលើ user និង filesystem របស់អ្នក។

## ៣. Read, Write និង Execute

សម្រាប់ regular file៖

- r (read): អានមាតិកា។
- w (write): កែប្រែមាតិកា។
- x (execute): ដំណើរការជា program/script ប្រសិនបើប្រភេទ file និងបរិស្ថានអនុញ្ញាត។

សម្រាប់ directory៖

- r: រាយឈ្មោះ entries។
- w: បង្កើត/លុប/ប្ដូរឈ្មោះ entries ក្នុង directory (ជាមួយ execute access ផងដែរ)។
- x: ចូលឆ្លង directory និងចូលដំណើរការ children តាម permissions ផ្សេងៗ។

ដូច្នេះ write permission លើ directory អាចមានន័យខុសពី write permission លើ file។

## ៤. Symbolic Permissions

chmod កែ permissions៖

~~~bash
chmod u+rw,go-rwx notes.txt
ls -l notes.txt
~~~

- u សំដៅ owner/user។
- g សំដៅ group។
- o សំដៅ others។
- a សំដៅទាំងអស់។
- + បន្ថែម permission, - ដក និង = កំណត់ឱ្យត្រូវតាម។

ក្នុង file សាកល្បង អាចសាកល្បងដក/បន្ថែម permission ហើយពិនិត្យដោយ ls -l។ កុំធ្វើលើ system files ឬ files ដែលចែករំលែកដោយមិនយល់ផលប៉ះពាល់។

## ៥. Numeric Permissions

Numeric mode ប្រើតម្លៃ៖ r=4, w=2, x=1។ បូកតម្លៃក្នុងក្រុម owner, group និង others៖

- 7 = rwx
- 6 = rw-
- 5 = r-x
- 4 = r--

ឧទាហរណ៍៖

~~~bash
chmod 640 notes.txt
ls -l notes.txt
~~~

640 មានន័យថា owner អាន/សរសេរ, group អាន, others គ្មានសិទ្ធិ។ កុំប្រើ mode ដូចជា 777 ជាទម្លាប់ ព្រោះវាអនុញ្ញាតសិទ្ធិច្រើនជាងចាំបាច់។

## ៦. umask និង Default Permissions

umask កំណត់សិទ្ធិដែលត្រូវដកចេញពី permissions លំនាំដើមពេលបង្កើត files/directories ថ្មី។ ពិនិត្យដោយ៖

~~~bash
umask
umask -S
~~~

លទ្ធផលអាចខុសគ្នាតាម distribution និងការកំណត់ shell។ កុំប្ដូរ umask ជាអចិន្ត្រៃយ៍ដោយមិនយល់ផលប៉ះពាល់លើ files ថ្មីៗទាំងអស់។

## ៧. Ownership និង sudo

ឯកសារមាន owner និង group។ chown/chgrp អាចកែ ownership ប៉ុន្តែជាញឹកញាប់ទាមទារ privileged access។ ក្នុងមេរៀននេះ សូមពិនិត្យ ownership ដោយ ls -l និង id ប៉ុណ្ណោះ។ កុំប្រើ sudo chown លើ system paths ឬធ្វើតាម command មិនស្គាល់។

ប្រើ sudo តែពេលចាំបាច់ សម្រាប់កិច្ចការដែលអ្នកយល់ និងមានសិទ្ធិធ្វើ។ Least privilege មានន័យថាប្រើសិទ្ធិតិចបំផុតដែលអាចបំពេញការងារបាន។

## ៨. កិច្ចការអនុវត្ត

ក្នុង directory ផ្ទាល់ខ្លួន $HOME/linux-practice/lesson-04៖

1. រត់ whoami, id និង groups។
2. បង្កើត notes.txt និងសរសេរអត្ថបទសាកល្បង។
3. ពិនិត្យ permission ដោយ ls -l។
4. ប្រើ chmod 600 notes.txt រួចពិនិត្យម្ដងទៀត។
5. សាក symbolic mode ដើម្បីបន្ថែម read permission ទៅ group។
6. រត់ umask ហើយកត់ត្រាលទ្ធផល។
7. ពន្យល់ថា owner/group/others មានសិទ្ធិអ្វីនៅចុងលំហាត់។

## សង្ខេប

Permissions មានក្រុម owner, group និង others ជាមួយ read/write/execute។ ls -l បង្ហាញ ownership និង mode។ chmod អាចប្រើ symbolic ឬ numeric notation។ umask ប៉ះពាល់ default permissions។ ប្រើ least privilege និងកុំប្រើ privileged commands លើ files ដែលអ្នកមិនយល់។

## ឯកសារយោង

- [Linux chmod manual](https://man7.org/linux/man-pages/man1/chmod.1.html)
- [Linux umask manual](https://man7.org/linux/man-pages/man2/umask.2.html)
- [GNU Coreutils: chmod](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html)
