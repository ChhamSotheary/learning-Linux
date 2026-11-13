# មេរៀនទី ៣៖ Linux Filesystem និងការគ្រប់គ្រងឯកសារ

## គោលបំណងមេរៀន

បន្ទាប់ពីរៀនចប់ អ្នកអាច៖

- ពន្យល់ពី filesystem hierarchy និងទីតាំងសំខាន់ៗ។
- ប្រើ absolute និង relative paths។
- មើលឯកសារ/ថត រួមទាំង hidden files។
- បង្កើត directory និង file សាកល្បង។
- ចម្លង និងប្ដូរឈ្មោះឯកសារដោយមានការប្រុងប្រយ័ត្ន។
- ប្រើ wildcards ដើម្បីជ្រើស filenames។

## ១. Linux Filesystem Tree

Linux រៀបចំឯកសារជា tree ដែលចាប់ផ្ដើមពី root directory សញ្ញា /។ Directory សំខាន់ៗរួមមាន៖

- /home: home directories របស់អ្នកប្រើធម្មតា។
- /etc: system configuration files។
- /var: ទិន្នន័យដែលផ្លាស់ប្ដូរជាបន្តបន្ទាប់ ដូចជា logs និង cache។
- /tmp: ឯកសារបណ្ដោះអាសន្ន។
- /usr: កម្មវិធី និងឯកសារចែករំលែកជាច្រើន។
- /bin និង /sbin: commands សំខាន់ៗ; នៅ distributions ថ្មីៗ អាចភ្ជាប់ទៅ /usr។
- /dev: interfaces ទៅកាន់ devices។
- /proc និង /sys: ទិដ្ឋភាពនៃព័ត៌មាន kernel/processes និងឧបករណ៍។

កុំកែ ឬលុប files ក្នុង system directories ប្រសិនបើមិនយល់ពីតួនាទី និងមិនមានផែនការស្ដារឡើងវិញ។

## ២. Absolute និង Relative Paths

Absolute path ចាប់ផ្ដើមពី /។ ឧទាហរណ៍ /home/sam/projects។

Relative path បកស្រាយពីទីតាំងបច្ចុប្បន្ន៖

- . សំដៅ directory បច្ចុប្បន្ន។
- .. សំដៅ parent directory។
- ~ ជា shell shortcut ទៅ home directory របស់ user បច្ចុប្បន្ន។

ពិនិត្យទីតាំងដោយ pwd មុនរត់ command ដែលបង្កើត ឬផ្លាស់ទីឯកសារ។

~~~bash
pwd
printf '%s
' "$HOME"
cd "$HOME"
pwd
~~~

## ៣. មើលឯកសារ និង Directory

~~~bash
ls
ls -l
ls -la
ls -lh
~~~

- ls បង្ហាញ items ក្នុង directory។
- -l បង្ហាញព័ត៌មានលម្អិត។
- -a រួមបញ្ចូល hidden files ដែលឈ្មោះចាប់ផ្ដើមដោយ dot។
- -h បង្ហាញទំហំអានងាយជាមួយ -l លើ coreutils implementations ជាច្រើន។

Options អាចមានភាពខុសគ្នាតាម implementation; ប្រើ man ls ដើម្បីពិនិត្យ។

## ៤. បង្កើត Directory និង Files សាកល្បង

បង្កើត workspace សម្រាប់មេរៀន៖

~~~bash
mkdir -p "$HOME/linux-practice/lesson-03"
cd "$HOME/linux-practice/lesson-03"
pwd
~~~

បង្កើត files សាកល្បង៖

~~~bash
touch notes.txt
mkdir drafts
printf '%s
' "Linux practice notes" > notes.txt
cat notes.txt
~~~

សញ្ញា > បញ្ជូន output ទៅ file ហើយអាចសរសេរជំនួសមាតិកាចាស់។ ក្នុងលំហាត់នេះ ប្រើតែ file សាកល្បងដែលបានបង្កើតថ្មី។ សញ្ញា >> បន្ថែមនៅចុង file។

## ៥. ចម្លង និងប្ដូរឈ្មោះ

~~~bash
cp notes.txt notes-backup.txt
mv notes-backup.txt drafts/
mv notes.txt lesson-notes.txt
~~~

cp បង្កើតច្បាប់ចម្លង។ mv អាចផ្លាស់ទី ឬប្ដូរឈ្មោះ។ ពិនិត្យ target paths ដោយប្រុងប្រយ័ត្ន; mv អាចជំនួសឯកសារដែលមានស្រាប់ ប្រសិនបើប្រើមិនប្រុងប្រយ័ត្ន។

ពិនិត្យលទ្ធផល៖

~~~bash
find "$HOME/linux-practice/lesson-03" -maxdepth 2 -type f -print
~~~

## ៦. Filenames, Spaces និង Hidden Files

ប្រើ quotes សម្រាប់ filenames ដែលមាន space៖

~~~bash
touch "project notes.txt"
ls -l "project notes.txt"
~~~

Hidden file នៅ Linux ជាទូទៅមានឈ្មោះចាប់ផ្ដើមដោយ dot។ ឧទាហរណ៍ .config។ បង្ហាញដោយ ls -a។ កុំលាក់ឯកសារដែលមាន sensitive data ដោយគិតថា hidden មានន័យថា protected; permissions ជាអ្នកកំណត់សិទ្ធិចូលប្រើ។

## ៧. Wildcards

Shell អាចពង្រីក wildcard មុនបញ្ជូន arguments ទៅ command៖

- * ត្រូវនឹងអក្សរច្រើនតួក្នុងឈ្មោះ។
- ? ត្រូវនឹងតួអក្សរមួយ។
- [abc] ត្រូវនឹងតួអក្សរមួយក្នុងក្រុម។

ឧទាហរណ៍មើល files .txt ក្នុង directory បច្ចុប្បន្ន៖

~~~bash
printf '%s
' ./*.txt
~~~

បើគ្មានឈ្មោះណាត្រូវនឹង pattern shell behavior អាចខុសគ្នា។ ត្រួតពិនិត្យ command expansion មុនប្រើ wildcard ជាមួយ commands ដែលផ្លាស់ប្ដូរ ឬលុបទិន្នន័យ។

## ៨. លុបឯកសារ និងសុវត្ថិភាព

ការលុបដោយ command line ជាញឹកញាប់មិនមាន Trash ឱ្យស្ដារឡើងវិញ។ មុនប្រើ rm ត្រូវពិនិត្យ៖

- តើទីតាំងបច្ចុប្បន្នត្រឹមត្រូវទេ?
- តើ filename/path ត្រឹមត្រូវទេ?
- តើ wildcard នឹងត្រូវនឹង files អ្វីខ្លះ?
- តើមាន backup ឬទិន្នន័យអាចស្ដារវិញទេ?

កុំប្រើ rm -rf លើ system paths ឬ command ដែលអ្នកមិនយល់។ លំហាត់មេរៀននេះមិនទាមទារឱ្យលុបឯកសារទេ។

## ៩. កិច្ចការអនុវត្ត

1. បង្កើត $HOME/linux-practice/lesson-03។
2. បង្កើត notes.txt និង drafts directory។
3. សរសេរបន្ទាត់មួយទៅ notes.txt ហើយអានវាដោយ cat។
4. ចម្លង notes.txt ទៅ notes-copy.txt។
5. ផ្លាស់ទី copy ទៅ drafts/។
6. ប្ដូរឈ្មោះ notes.txt ទៅ lesson-notes.txt។
7. ប្រើ ls -la និង find ដើម្បីរាយឯកសារទាំងអស់។
8. ប្រើ printf '%s
' ./*.txt ដើម្បីពិនិត្យ wildcard result។
9. សរសេរ absolute path របស់ workspace និង relative path របស់ drafts។

## ១០. សង្ខេប

Linux filesystem ចាប់ផ្ដើមពី root /។ Absolute path ចាប់ផ្ដើមពី / ខណៈ relative path ពឹងលើ working directory។ ls និង find ជួយពិនិត្យ files; mkdir និង touch បង្កើត; cp ចម្លង; mv ផ្លាស់ទី/ប្ដូរឈ្មោះ។ Quotes និងការពិនិត្យ path ជួយជៀសវាងកំហុស។

## ឯកសារយោង

- [Linux Filesystem Hierarchy, man-pages](https://man7.org/linux/man-pages/man7/hier.7.html)
- [GNU Coreutils Manual](https://www.gnu.org/software/coreutils/manual/coreutils.html)
