# Lab ៣៖ ស្វែងរកជំនួយសម្រាប់ Command Line (Get Command-Line Help)

## គោលបំណង
ស្គាល់វិធីស្វែងរកជំនួយដោយ `man`, `--help`, `info` និង shell built-in `help`។

## ១. Manual pages
```bash
man ls
```
ប្រើ PageUp/PageDown ឬព្រួញដើម្បីអាន ហើយចុច `q` ដើម្បីចេញ។ ក្នុង man page អាចស្វែងរកពាក្យដោយវាយ `/word` រួច Enter។

## ២. Help រហ័ស
```bash
ls --help
cp --help
```
ជម្រើស `--help` បង្ហាញសេចក្ដីណែនាំខ្លីៗសម្រាប់ command ជាច្រើន ប៉ុន្តែមិនមែន command ទាំងអស់សុទ្ធតែគាំទ្រដូចគ្នាទេ។

## ៣. Shell built-ins
```bash
help cd
type cd
```
`cd` ជា Bash built-in ដូច្នេះ `help cd` មានប្រយោជន៍។ `type` ប្រាប់ថាឈ្មោះមួយជា built-in, alias ឬ executable។

## ៤. Info pages និងការស្វែងរក
```bash
info coreutils
man -k directory
apropos directory
```
`info` អាចបង្ហាញឯកសារណែនាំលម្អិត។ `man -k` និង `apropos` ស្វែងរកតាមពាក្យពិពណ៌នា ប្រសិនបើ man-db និង manual database មានដំឡើង។

## ៥. អាន SYNOPSIS
នៅក្នុង manual ស្វែងរកផ្នែក NAME, SYNOPSIS, DESCRIPTION, OPTIONS និង EXAMPLES។ សញ្ញា `[]` ជាទូទៅបង្ហាញ argument ស្រេចចិត្ត; អានការពន្យល់ជាក់លាក់របស់ command មុនប្រើ។

## លំហាត់
1. បើក `man pwd` ហើយកត់ត្រា SYNOPSIS។
2. ប្រើ `ls --help` ដើម្បីរក option សម្រាប់បង្ហាញ hidden files។
3. ប្រើ `help cd` ហើយពន្យល់ថាហេតុអ្វីវាខុសពី `man cd`។
4. ស្វែងរក manual ដែលពាក់ព័ន្ធនឹងពាក្យ `copy` ដោយ `man -k copy`។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចចេញពី man pager ដោយ `q`។
- [ ] ខ្ញុំដឹងពេលណាត្រូវប្រើ `help` និង `man`។
- [ ] ខ្ញុំអាចស្វែងរក option មុនដំណើរការ command។

**ចំណាំ៖** ប្រសិនបើ manual មិនមាន សូមពិនិត្យ package documentation របស់ RHEL និងកុំសន្មតថា command មាន option ដោយមិនបានផ្ទៀងផ្ទាត់។
