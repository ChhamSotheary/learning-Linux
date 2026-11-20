# Lab ២៖ គ្រប់គ្រង Files និង Directories (Manage Files and Directories)

## គោលបំណង
- មើលឯកសារ និងថតដោយប្រើ `ls`។
- បង្កើតថត និងឯកសារសាកល្បង។
- ចម្លង ផ្លាស់ទី ប្ដូរឈ្មោះ និងស្វែងរកឯកសារ។
- ប្រើ absolute path, relative path និង wildcards ដោយប្រុងប្រយ័ត្ន។

## ១. ពិនិត្យទីតាំងបច្ចុប្បន្ន
```bash
pwd
ls
ls -la
ls -lh
```
`pwd` បង្ហាញ working directory។ `ls -la` រួមបញ្ចូល hidden files និងព័ត៌មានលម្អិត។

## ២. បង្កើត workspace សម្រាប់ Lab
```bash
mkdir -p "$HOME/rhel-labs/lab02/drafts"
cd "$HOME/rhel-labs/lab02"
pwd
touch notes.txt
printf '%s\n' "ខ្ញុំកំពុងរៀន Linux" > notes.txt
cat notes.txt
```
ប្រើតែ directory សាកល្បងនេះ។ សញ្ញា `>` សរសេរជំនួសមាតិកា file ខណៈ `>>` បន្ថែមនៅខាងចុង។

## ៣. ចម្លង ផ្លាស់ទី និងប្ដូរឈ្មោះ
```bash
cp notes.txt notes-copy.txt
mv notes-copy.txt drafts/
mv notes.txt lesson-notes.txt
find "$HOME/rhel-labs/lab02" -maxdepth 2 -type f -print
```
`cp` ចម្លង, `mv` ផ្លាស់ទី ឬប្ដូរឈ្មោះ, `find` ស្វែងរកឯកសារ។ ពិនិត្យគោលដៅមុនប្រើ `mv` ព្រោះវាអាចជំនួសឯកសារដែលមានរួច។

## ៤. ឈ្មោះមានដកឃ្លា និង wildcard
```bash
touch "project notes.txt"
ls -l "project notes.txt"
printf '%s\n' ./*.txt
```
ប្រើ quotes ជុំវិញ filename ដែលមាន space។ `*` តំណាងឱ្យតួអក្សរច្រើន; `?` តំណាងឱ្យតួអក្សរមួយ។ ពិនិត្យ wildcard result មុនប្រើជាមួយ command ដែលកែប្រែទិន្នន័យ។

## ៥. លំហាត់
1. បង្កើត directory `$HOME/rhel-labs/lab02/reports`។
2. បង្កើត `report.txt` ហើយសរសេរបន្ទាត់មួយចូលទៅក្នុងវា។
3. ចម្លងវាទៅ `reports/`។
4. បង្ហាញឯកសារទាំងអស់ដោយ `find`។
5. សរសេរពន្យល់ខុសគ្នារវាង `cp` និង `mv`។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ `pwd`, `ls -la`។
- [ ] ខ្ញុំអាចបង្កើត directory/file។
- [ ] ខ្ញុំអាចចម្លង និងប្ដូរឈ្មោះ file។
- [ ] ខ្ញុំយល់ពីការប្រុងប្រយ័ត្នចំពោះ `>` និង wildcard។

**សុវត្ថិភាព៖** Lab នេះមិនត្រូវការលុបឯកសារទេ។ កុំប្រើ `rm -rf` លើ path ដែលមិនបានពិនិត្យ។
